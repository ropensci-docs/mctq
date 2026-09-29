# Compute MCTQ average weekly light exposure

**\[maturing\]**

`le_week()` computes the **average weekly light exposure** for the
standard version of the Munich ChronoType Questionnaire (MCTQ).

## Usage

``` r
le_week(le_w, le_f, wd)
```

## Arguments

- le_w:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **light exposure on workdays** from a
  standard version of the MCTQ questionnaire.

- le_f:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **light exposure on work-free days** from
  a standard version of the MCTQ questionnaire.

- wd:

  An
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`numeric`](https://rdrr.io/r/base/numeric.html) object or an
  [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
  to the **number of workdays per week** from a standard version of the
  MCTQ questionnaire.

## Value

A [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
object corresponding to the vectorized weighted mean of `le_w` and
`le_f` with `wd` and `fd(wd)` as weights.

## Details

**Standard MCTQ** functions were created following the guidelines in
Roenneberg, Wirz-Justice, & Merrow (2003), Roenneberg, Allebrandt,
Merrow, & Vetter (2012), and from The Worldwide Experimental Platform
(theWeP, n.d.).

**\\\mu\\MCTQ** functions were created following the guidelines in
Ghotbi et al. (2020), in addition to the guidelines used for the
standard MCTQ.

**MCTQ\\^{Shift}\\** functions were created following the guidelines in
Juda, Vetter, & Roenneberg (2013), in addition to the guidelines used
for the standard MCTQ.

See the References section to learn more.

### Class requirements

The `mctq` package works with a set of object classes specially created
to hold time values. These classes can be found in the
[lubridate](https://lubridate.tidyverse.org/reference/lubridate-package.html)
and [hms](https://hms.tidyverse.org/reference/hms-package.html)
packages. Please refer to those package documentations to learn more
about them.

### Rounding and fractional time

Some operations may produce an output with fractional time (e.g.,
`"19538.3828571429s (~5.43 hours)"`, `01:15:44.505`). If you want, you
can round it with `mctq:::round_time()`.

Our recommendation is to avoid rounding, but, if you do, make sure that
you only round your values after all computations are done. That way you
avoid [round-off errors](https://en.wikipedia.org/wiki/Round-off_error).

## Guidelines

Roenneberg, Allebrandt, Merrow, & Vetter (2012) and The Worldwide
Experimental Platform (n.d.) guidelines for `le_week()` (\\LE\_{week}\\)
computation are as follows.

### Notes

- The average weekly light exposure (\\LE\_{week}\\) is the weighted
  average of the light exposure on work and work-free days in a week.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### Computation

\$\$LE\_{week} = \frac{(LE_W \times WD) + (LE_F \times FD)}{7}\$\$

Where:

- \\LE\_{week}\\ = Average weekly light exposure.

- \\LE_W\\ = Light exposure on workdays.

- \\LE_F\\ = Light exposure on work-free days.

- \\WD\\ = Number of workdays per week ("I have a regular work schedule
  and work \_\_\_ days per week").

- \\FD\\ = Number of work-free days per week.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

## References

Ghotbi, N., Pilz, L. K., Winnebeck, E. C., Vetter, C., Zerbini, G.,
Lenssen, D., Frighetto, G., Salamanca, M., Costa, R., Montagnese, S., &
Roenneberg, T. (2020). The \\\mu\\MCTQ: an ultra-short version of the
Munich ChronoType Questionnaire. *Journal of Biological Rhythms*,
*35*(1), 98-110.
[doi:10.1177/0748730419886986](https://doi.org/10.1177/0748730419886986)

Juda, M., Vetter, C., & Roenneberg, T. (2013). The Munich ChronoType
Questionnaire for shift-workers (MCTQ\\^{Shift}\\). *Journal of
Biological Rhythms*, *28*(2), 130-140.
[doi:10.1177/0748730412475041](https://doi.org/10.1177/0748730412475041)

Roenneberg T., Allebrandt K. V., Merrow M., & Vetter C. (2012). Social
jetlag and obesity. *Current Biology*, *22*(10), 939-43.
[doi:10.1016/j.cub.2012.03.038](https://doi.org/10.1016/j.cub.2012.03.038)

Roenneberg, T., Wirz-Justice, A., & Merrow, M. (2003). Life between
clocks: daily temporal patterns of human chronotypes. *Journal of
Biological Rhythms*, *18*(1), 80-90.
[doi:10.1177/0748730402239679](https://doi.org/10.1177/0748730402239679)

The Worldwide Experimental Platform (n.d.). MCTQ.
<https://www.thewep.org/documentations/mctq/>

## See also

Other MCTQ functions:
[`fd()`](https://docs.ropensci.org/mctq/reference/fd.md),
[`gu()`](https://docs.ropensci.org/mctq/reference/gu.md),
[`msf_sc()`](https://docs.ropensci.org/mctq/reference/msf_sc.md),
[`msl()`](https://docs.ropensci.org/mctq/reference/msl.md),
[`napd()`](https://docs.ropensci.org/mctq/reference/napd.md),
[`sd24()`](https://docs.ropensci.org/mctq/reference/sd24.md),
[`sd_overall()`](https://docs.ropensci.org/mctq/reference/sd_overall.md),
[`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md),
[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md),
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
[`sjl_weighted()`](https://docs.ropensci.org/mctq/reference/sjl_weighted.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

le_w <- lubridate::dhours(1.5)
le_f <- lubridate::dhours(3.7)
wd <- 5
le_week(le_w, le_f, wd)
#> [1] "7662.85714285714s (~2.13 hours)"
#> [1] "7662.85714285714s (~2.13 hours)" # Expected

le_w <- lubridate::dhours(3)
le_f <- lubridate::dhours(1.5)
wd <- 6
le_week(le_w, le_f, wd)
#> [1] "10028.5714285714s (~2.79 hours)"
#> [1] "10028.5714285714s (~2.79 hours)" # Expected

le_w <- lubridate::dhours(5.6)
le_f <- lubridate::as.duration(NA)
wd <- 3
le_week(le_w, le_f, wd)
#> [1] NA
#> [1] NA # Expected

## Vector example

le_w <- c(lubridate::dhours(3), lubridate::dhours(2.45))
le_f <- c(lubridate::dhours(3), lubridate::dhours(3.75))
wd <- c(4, 5)
le_week(le_w, le_f, wd)
#> [1] "10800s (~3 hours)"               "10157.1428571429s (~2.82 hours)"
#> [1] "10800s (~3 hours)" # Expected
#> [2] "10157.1428571429s (~2.82 hours)" # Expected

## Checking second output from vector example

if (requireNamespace("stats", quietly = TRUE)) {
    i <- 2
    x <- c(le_w[i], le_f[i])
    w <- c(wd[i], fd(wd[i]))
    lubridate::as.duration(stats::weighted.mean(x, w))
}
#> [1] "10157.1428571429s (~2.82 hours)"
#> [1] "10157.1428571429s (~2.82 hours)" # Expected

## Converting the output to `hms`

le_w <- lubridate::dhours(1.25)
le_f <- lubridate::dhours(6.23)
wd <- 3
le_week(le_w, le_f, wd)
#> [1] "14744.5714285714s (~4.1 hours)"
#> [1] "14744.5714285714s (~4.1 hours)" # Expected

hms::hms(as.numeric(le_week(le_w, le_f, wd)))
#> 04:05:44.571429
#> 04:05:44.571429 # Expected

## Rounding the output at the seconds level

le_w <- lubridate::dhours(3.4094)
le_f <- lubridate::dhours(6.2345)
wd <- 2
le_week(le_w, le_f, wd)
#> [1] "19538.3828571429s (~5.43 hours)"
#> [1] "19538.3828571429s (~5.43 hours)" # Expected

mctq:::round_time(le_week(le_w, le_f, wd))
#> [1] "19538s (~5.43 hours)"
#> [1] "19538s (~5.43 hours)" # Expected
```
