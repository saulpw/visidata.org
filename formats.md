# Supported Formats

|filetype            |format              |VisiData\_loader |VisiData saver  |version\_added |created  |creator             |PyPI dependencies   |
|--------------------|--------------------|-----------------|----------------|---------------|---------|--------------------|--------------------|
|[csv](#csv)    |Comma\-Separated Values|0\.28            |displayed text  |0\.28          |1972     |                    |                    |
|[json](#json)  |Javascript Object Notation \(JSON\)|0\.28            |typed           |0\.28          |2001     |Douglas Crockford   |                    |
|[tsv](#tsv)    |Tab\-Separated Values|0\.28            |displayed text  |0\.28          |         |                    |                    |
|xlsx                |Excel spreadsheets  |0\.28            |                |0\.28          |1987     |Microsoft           |openpyxl            |
|zip                 |ZIP archive format  |0\.28            |                |0\.28          |1989     |PKWARE              |                    |
|hdf5                |Hierarchical Data Format|0\.28            |                |0\.28          |199x     |NCSA                |h5py                |
|[sqlite](#sqlite)|sqlite              |0\.42            |                |0\.42          |2000     |D\. Richard Hipp    |                    |
|xls                 |Excel spreadsheets  |0\.42            |                |0\.42          |1987     |Microsoft           |xlrd                |
|[fixed](#fixed)|fixed width text    |0\.97            |                |0\.97          |         |                    |                    |
|[postgres](#postgres)|PostgreSQL database |0\.97            |                |0\.97          |1996     |                    |                    |
|[vd](#vd)      |VisiData command log|0\.97            |                |0\.97          |2017     |VisiData            |                    |
|[mbtiles](#mbtiles)|MapBox Tileset      |0\.98            |                |0\.98          |2011     |MapBox              |mapbox\-vector\-tile|
|pbf                 |Protocolbuffer Binary Format|0\.98            |                |0\.98          |2011     |OpenStreetMap       |                    |
|[shp](#shp)    |Shapefile geographic data|0\.98            |                |0\.98          |1993     |ESRI                |pyshp               |
|[html](#html)  |HTML tables         |0\.99            |displayed text  |0\.99          |1996     |Dave Raggett        |lxml                |
|md                  |markdown table      |                 |displayed text  |1\.1           |2008     |                    |                    |
|[png](#png)    |Portable Network Graphics \(PNG\) image|1\.1             |from png        |1\.1           |1996     |PNG Development Group|pypng               |
|[ttf](#ttf)    |TrueType Font       |1\.1             |                |1\.1           |1991     |Apple               |fonttools           |
|[dot](#pcap)   |Graphviz diagram    |                 |from pcap       |1\.2           |1991     |                    |                    |
|dta                 |Stata               |1\.2             |                |1\.2           |1985     |StataCorp           |pandas              |
|[geojson](#shp)|Geographic JSON     |                 |from shp        |1\.2           |2008     |                    |                    |
|sas7bdat            |Statistical Analysis System \(SAS\)|1\.2             |                |1\.2           |1976     |SAS Institute       |sas7bdat            |
|sav                 |SPSS statistics     |1\.2             |                |1\.2           |1968     |SPSS Inc            |                    |
|spss                |SPSS statistics     |1\.2             |                |1\.2           |1968     |SPSS Inc            |savReaderWriter     |
|xpt                 |Statistical Analysis System \(SAS\)|1\.2             |                |1\.2           |1976     |SAS Institute       |xport               |
|[jsonl](#json) |JSON Lines          |1\.3             |typed           |1\.3           |2013     |Ian Ward            |                    |
|[pandas](#pandas)|all formats supported by pandas library|1\.3             |                |1\.3           |2008     |Wes McKinney        |pandas              |
|[pcap](#pcap)  |network packet capture|1\.3             |                |1\.3           |1988     |LBNL                |dpkt dnslib         |
|pyprof              |Python Profile data |1\.3             |                |1\.3           |         |                    |                    |
|[xml](#xml)    |eXtensible Markup Language \(XML\)|1\.3             |from xml        |1\.3           |1998     |W3C                 |lxml                |
|yaml                |YAML Ain't Markup Language \(YAML\)|1\.3             |                |1\.3           |2001     |Clark Evans         |PyYAML              |
|frictionless        |Frictionless Data   |2\.0             |                |2\.0           |         |OpenKnowledge Institute|datapackage         |
|jira                |JIRA/Confluence table markup|                 |displayed text  |2\.0           |         |Atlassian           |                    |
|npy                 |NumPy array format  |2\.0             |typed           |2\.0           |         |                    |numpy               |
|tar                 |Unix Tape Archive   |2\.0             |                |2\.0           |         |                    |                    |
|usv                 |Unicode\-Separated Value|2\.0             |displayed text  |2\.0           |1993     |Unicode             |                    |
|xlsb                |Excel binary format |2\.0             |                |2\.0           |         |Microsoft           |xlrd                |

# Extra notes about formats

## tsv {#tsv}
- loader-specific options
    - `delimiter` (default: '\t') field delimiter to use for tsv/usv filetype
    - `row_delimiter` (default: '\n') row delimeter to use for tsv/usv filetype
    - `tsv_safe_newline` (default: '\u001e') replacement for newline character when saving to tsv
    - `tsv_safe_tab` (default: '\u001f') replacement for tab character when saving to tsv

## csv {#csv}
- loader-specific options
    - `csv_dialect` (default: 'excel') dialect passed to csv.reader
        - Accepted dialects are *excel-tab*, *unix*, and *excel*.
    - `csv_delimiter` (default: ',') delimiter passed to csv.reader
    - `csv_quotechar` (default: '"') quotechar passed to csv.reader
    - `csv_skipinitialspace` (default: True) skipinitialspace passed to csv.reader
    - `csv_escapechar` (default: None) escapechar passed to csv.reader
    - `csv_lineterminator` (default: '\r\n') lineterminator passed to csv.writer
    - `safety_first` (default: False) sanitize input/output to handle edge cases, with a performance cost

## fixed {#fixed}
- loader-specific options
    - `fixed_rows` (default: 1000) number of rows to detect fixed width columns from
    - `fixed_maxcols` (default: 0) max number of fixed-width columns to create (0 is no max)

## json {#json}
- loader-specific options
    - `json_indent` (default: None) indent to use when saving json
    - `json_sort_keys` (default: False) sort object keys when saving to json
    - `default_colname` (default: '') column name to use for non-dict rows
- Cells containing lists (e.g. `[3]`) or dicts (e.g. `{3}`) can be expanded into new columns with `(` and unexpanded with `)`.
- All expanded subcolumns must be closed (with `)`) to retain the same structure.

## xml {#xml}
- `v` show only columns in current row attributes
- `za` add column for xml attributes

## pcap {#pcap}
- loader-specific options
    - `pcap_internet` (default: 'n') (y/s/n) if save_dot includes all internet hosts separately (y), combined (s), or does not include the internet (n)

## postgres {#postgres}
- loader-specific options
    - `postgres_schema` (default: 'public') the desired schema for the Postgres database
- `vd postgres://`*username*`:`*password*`@`*hostname*`:`*port*`/`*database* opens a connection to the given postgres database.

## sqlite {#sqlite}
- supports saving for CREATE/INSERT (not wholesale updates)
- `z Ctrl+S` to commit any `add-row`/`edit-cell`/`delete-row`

## html {#html}
- loader-specific options
    - `html_title` (default: `'<h2>{sheet.name}</h2>'`) table header when saving to html
- load all `<table>`s in a web page as VisiData sheets.


## shp {#shp}
- Can be edited in raw data form. Images can be plotted with `.` (dot).
- **.shp** files can be saved as **geoJSON**.

## mbtiles {#mbtiles}
- Can be edited in raw data form. Images can be plotted with `.` (dot).

## png {#png}
- Can be edited in raw data form. Images can be plotted with `.` (dot).

## ttf {#ttf}
- Can be edited in raw data form. Images can be plotted with `.` (dot).

## pandas {#pandas}

VisiData has an adapter for **pandas**. To load a file format which is supported by **pandas**, pass `-f pandas data.foo`. This will call `pandas.read_foo()`.

For example:

~~~
vd -f pandas data.parquet
~~~

loads a parquet file. When using the **pandas** loader, the `.fileformat` file extension is mandatory.

## vd {#vd}
- Command history log format for a VisiData session.
- `Ctrl+D` to save the current session's CommandLog.
