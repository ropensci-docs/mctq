# Get paths to `mctq` raw datasets

**\[maturing\]**

`mctq` comes bundled with raw fictional datasets for testing and
learning purposes. `raw_data()` makes it easy to access their paths.

## Usage

``` r
raw_data(file = NULL)
```

## Arguments

- file:

  (optional) a [`character`](https://rdrr.io/r/base/character.html)
  object indicating the raw data file name(s). If `NULL`, all raw data
  file names will be returned (default: `NULL`).

## Value

If `file == NULL`, a
[`character`](https://rdrr.io/r/base/character.html) object with all
file names available. Else, a string with the file name path.

## See also

Other utility functions:
[`pretty_mctq()`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md),
[`random_mctq()`](https://docs.ropensci.org/mctq/reference/random_mctq.md)

## Examples

``` r
if (FALSE) { # \dontrun{
## To list all raw data file names available

raw_data()

## To get the file path from a specific raw data

raw_data("std_mctq.csv")} # }
```
