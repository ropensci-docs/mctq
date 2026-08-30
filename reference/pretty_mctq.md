# Make an MCTQ dataset more presentable

**\[maturing\]**

`pretty_mctq()` helps you to transform your Munich ChronoType
Questionnaire (MCTQ) data in many ways. See the Arguments and Details
section to learn more.

## Usage

``` r
pretty_mctq(data, round = TRUE, hms = TRUE)
```

## Arguments

- data:

  A [`data.frame`](https://rdrr.io/r/base/data.frame.html) object.

- round:

  (optional) a [`logical`](https://rdrr.io/r/base/logical.html) value
  indicating if
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  and [`hms`](https://hms.tidyverse.org/reference/hms.html) objects must
  be rounded at the seconds level (default: `TRUE`).

- hms:

  (optional) a [`logical`](https://rdrr.io/r/base/logical.html) value
  indicating if
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  and [`difftime`](https://rdrr.io/r/base/difftime.html) objects must be
  converted to [`hms`](https://hms.tidyverse.org/reference/hms.html)
  (default: `TRUE`).

## Value

A transformed [`data.frame`](https://rdrr.io/r/base/data.frame.html)
object, as indicated in the arguments.

## Details

### Rounding

Please note that by rounding MCTQ values you discard data. That is to
say that if you need to redo a computation, or do new ones, your values
can be off by a couple of seconds (see [round-off
error](https://en.wikipedia.org/wiki/Round-off_error)).

Round your values only if and when you want to present them more
clearly, like in graphical representations. You can also round values to
facilitate data exporting to text formats (like `.csv`), but note that
this will come with a precision cost.

Note also that `pretty_mctq()` uses
[`round()`](https://rdrr.io/r/base/Round.html) for rounding, which uses
uses the IEC 60559 standard (*"go to the even digit"*) for rounding off
a 5. Therefore, `round(0.5)` is equal to 0 and `round(-1.5)` is equal to
-2. See [`?round`](https://rdrr.io/r/base/Round.html) to learn more.

## See also

Other utility functions:
[`random_mctq()`](https://docs.ropensci.org/mctq/reference/random_mctq.md),
[`raw_data()`](https://docs.ropensci.org/mctq/reference/raw_data.md)

## Examples

``` r
data <- data.frame(
    a = 1,
    b = lubridate::duration(1.12345),
    c = hms::hms(1.12345)
    )

## Rounding time objects from `data`

pretty_mctq(data, round = TRUE, hms = FALSE)
#>   a  b        c
#> 1 1 1s 00:00:01

## Converting non-'hms' time objects from 'data' to 'hms'

pretty_mctq(data, round = FALSE, hms = TRUE)
#>   a              b              c
#> 1 1 00:00:01.12345 00:00:01.12345
```
