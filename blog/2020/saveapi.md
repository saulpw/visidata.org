# save_ext()

[This post affects VisiData v2.-3dev.]

Recently, Saul established a consistent api structure for savers of file formats.

Now, the declaration for all `save_foo()` will take the form of:

```
def save_ext(p, *sheets())
```

Where `p` is a `visidata.Path()` object representing the file being written to, and `*sheets` will be the 1 sheet or more that are going to be saved.

This seemed like a great opportunity to take folks behind the scenes on the history of a very specific part of VisiData's api.

As developers, we strive for an api that remains stable for many versions to come. I thought it would be really interesting to share an example where the developer chose to alter a functon definition, as the software evolved.

## The history of save_() and multisave_()

The previous structure for savers looked like this:

```
def save_ext(sheet, p)
```

This was in-line with the standard model of *source* then *dest* found in many commandline tools.

It worked really well for a while. Then Saul added multisave to VisiData, a command that could save multiple sheets with a single incantation.

The existing `save_()` api was very much designed with a single sheet in mind. Python does have [args and kwargs magic variables](https://pythontips.com/2013/08/04/args-and-kwargs-in-python-explained/), but only for variables declared at the very end.

`sheets` could have been modified to be a list, but that would mean adding Is This a List checkers to every `save_`. This pays off when the default assumption is that you are going to get a list of objects. When the default assumption is that you are going to receive a single sheet, it feels frustrating.

This led to him creating a separate `multisave_ext()` that would be called with `g^S`. Most of them look like this:

```
def multisave_ext(p, *sheets)
```

This inconsistency between `save_ext()` and `multisave_ext()` had some side-effects. VisiData automatically detects which of these functions to call based on the ext provided. 

Here is an excerpt from one bit of the code:

```
for vs in vsheets:
    savefunc = getattr(vs, 'save_' + filetype, None
    if not savefunc:
        savefunc = lambda p,vs=vs,f=globalsavefunc: f(p, vs)
```

This code assumes a structure of `save_ext(p, sheet)`, which is not the case for a lot of savers. This was a bug waiting to happen.

This was the breaking point that lead to the decision to create a singular `save_ext()` api (OAFA!) which can handle single sheets and multiple sheets.

Saul mulled over some options for the new api. The other top contender was:

```
Foosheet.save_foo(vs, p, *other_sheets)
```

where `vs` is the `FooSheet` which is calling `save_foo()`. This one was really, really tempting because it would be backwards compatible with existing savers that Saul and other folks have writen. But...it did not make sense to arbitrarily prioritise one sheet over the others being saved.

And there you have it! Sometimes, when you try to avoid breaking changes, code can get more and more contrived. Occassionally, with a feature expansion, it is hard to avoid without leaving a bad taste in your mouth.

[Written by Anja Kefala 2020-02-13]