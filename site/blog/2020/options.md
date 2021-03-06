---
title: Expansion of CLI Options
date: 2020-07-07
tags:
    - blog
---

Hello VisiDaters!

Recently, Saul has pushed a re-work of the CLI options to the `develop` branch. I am particularly excited about this change, and so I wanted to cover it in detail.

I am going to be referencing two options; `-f`, alias for `--filetype`, and `-d`, alias for `--delimiter`.

By default, VisiData deduces the filetype of a source from its extension. `-f` allows you to manually declare the filetype, overriding deduction by extension. `-d` sets the delimiter for TSV files.

## The Additions

* `vd --help` will now open the manpage
* VisiData now supports the setting of sheet-specific options, as well as global, through the CLI.
* `vd -f json foo.json.gz` now applies to the inner filetype.


Historically, if you did,

~~~
vd -f csv foo.tsv bar.csv
~~~

the option `-f` would then get applied as a global option to every source.
There was no way to communicate to VisiData distinct filetypes for each source.

With the new additions, you can do this,

~~~
vd -f tsv foo.tsv -f csv bar.csv
~~~

Now, `-f tsv` would be applied to foo.tsv, and `-f csv` would be applied to bar.csv.


## How Sheet-Specific CLI Options Work

* `--option`s will apply as sheet-specific options to the sources which follow them.
* The final setting for a given option will be considered the CLI-given override setting. It will be applied to all sources loaded by the CLI, if that source does not have its own sheet-specific setting. This means that if an option is only set once, it will be applied to all of the sources.
* If an option is preceded by `-g` it will be set globally for all sheets in the session, just like in the previous versions of VisiData. Some special options, like `-p` (replay), are always going to be global, and will not require the `-g` prefix.

Examples:

To specify a different delimiter for each file,

~~~
vd -d '|' pipes.tsv -d ',' commas.tsv
~~~

To set a global delimiter,

~~~
vd pipes.tsv commas.tsv -g -d '|'
vd -g -d '|' pipes.tsv commas.tsv
~~~

To specify a filetype for all of the files provided through the CLI,

~~~
vd foo bar -f tsv
~~~

## Limitations

- there is no way to make an option apply only to the immediately following source
- nor a way to unset an option after setting it

As always, please let us know how you feel about it! [Share a tweet](https://twitter.com/VisiData), or stop by for a [chat in freenode #visidata](https://webchat.freenode.net/).

[written by Anja Boskovic 2020-07-07]
[updated by Anja Boskovic 2020-07-26]
