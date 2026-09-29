# Compute MCTQ average weekly sleep duration

**\[maturing\]**

`sd_week()` computes the **average weekly sleep duration** for the
standard and micro versions of the Munich ChronoType Questionnaire
(MCTQ).

See
[`sd_overall()`](https://docs.ropensci.org/mctq/reference/sd_overall.md)
to compute the overall sleep duration of a particular shift for the
shift version of the MCTQ.

## Usage

``` r
sd_week(sd_w, sd_f, wd)
```

## Arguments

- sd_w:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration on workdays** from a
  standard or micro version of the MCTQ questionnaire. You can use
  [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to compute
  it.

- sd_f:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration on work-free days** from
  a standard or micro version of the MCTQ questionnaire. You can use
  [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to compute
  it.

- wd:

  An
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`numeric`](https://rdrr.io/r/base/numeric.html) object or an
  [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
  to the **number of workdays per week** from a standard or micro
  version of the MCTQ questionnaire.

## Value

A [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
object corresponding to the vectorized weighted mean of `sd_w` and
`sd_f` with `wd` and `fd(wd)` as weights.

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

Roenneberg, Allebrandt, Merrow, & Vetter (2012), Ghotbi et al. (2020),
and The Worldwide Experimental Platform (n.d.) guidelines for
`sd_week()` (\\SD\_{week}\\) computation are as follows.

### Notes

- The average weekly sleep duration is the weighted average of the sleep
  durations on work and work-free days in a week.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### Computation

\$\$SD\_{week} = \frac{(SD\_{W} \times WD) + (SD\_{F} \times FD)}{7}\$\$

Where:

- \\SD\_{week}\\ = Average weekly sleep duration.

- \\SD\_{W}\\ = Sleep duration on workdays.

- \\SD\_{F}\\ = Sleep duration on work-free days.

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
[`le_week()`](https://docs.ropensci.org/mctq/reference/le_week.md),
[`msf_sc()`](https://docs.ropensci.org/mctq/reference/msf_sc.md),
[`msl()`](https://docs.ropensci.org/mctq/reference/msl.md),
[`napd()`](https://docs.ropensci.org/mctq/reference/napd.md),
[`sd24()`](https://docs.ropensci.org/mctq/reference/sd24.md),
[`sd_overall()`](https://docs.ropensci.org/mctq/reference/sd_overall.md),
[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md),
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
[`sjl_weighted()`](https://docs.ropensci.org/mctq/reference/sjl_weighted.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

sd_w <- lubridate::dhours(4)
sd_f <- lubridate::dhours(8)
wd <- 5
sd_week(sd_w, sd_f, wd)
#> [1] "18514.2857142857s (~5.14 hours)"
#> [1] "18514.2857142857s (~5.14 hours)" # Expected

sd_w <- lubridate::dhours(7)
sd_f <- lubridate::dhours(7)
wd <- 4
sd_week(sd_w, sd_f, wd)
#> [1] "25200s (~7 hours)"
#> [1] "25200s (~7 hours)" # Expected

sd_w <- lubridate::as.duration(NA)
sd_f <- lubridate::dhours(10)
wd <- 6
sd_week(sd_w, sd_f, wd)
#> [1] NA
#> [1] NA # Expected

## Vector example

sd_w <- c(lubridate::dhours(4.5), lubridate::dhours(5.45))
sd_f <- c(lubridate::dhours(8), lubridate::dhours(7.3))
wd <- c(3, 7)
sd_week(sd_w, sd_f, wd)
#> [1] "23400s (~6.5 hours)"  "19620s (~5.45 hours)"
#> [1] "23400s (~6.5 hours)"  "19620s (~5.45 hours)" # Expected

## Checking second output from vector example

if (requireNamespace("stats", quietly = TRUE)) {
    i <- 2
    x <- c(sd_w[i], sd_f[i])
    w <- c(wd[i], fd(wd[i]))
    lubridate::as.duration(stats::weighted.mean(x, w))
}
#> [1] "19620s (~5.45 hours)"
#> [1] "19620s (~5.45 hours)" # Expected

## Converting the output to 'hms'

sd_w <- lubridate::dhours(5.45)
sd_f <- lubridate::dhours(9.5)
wd <- 5
x <- sd_week(sd_w, sd_f, wd)
x
#> [1] "23785.7142857143s (~6.61 hours)"
#> [1] "23785.7142857143s (~6.61 hours)" # Expected
hms::as_hms(as.numeric(x))
#> 06:36:25.714286
#> 06:36:25.714286 # Expected

## Rounding the output at the seconds level

sd_w <- lubridate::dhours(4.5)
sd_f <- lubridate::dhours(7.8)
wd <- 3
sd_week(sd_w, sd_f, wd)
#> [1] "22988.5714285714s (~6.39 hours)"
#> [1] "22988.5714285714s (~6.39 hours)" # Expected

mctq:::round_time(sd_week(sd_w, sd_f, wd))
#> [1] "22989s (~6.39 hours)"
#> [1] "22989s (~6.39 hours)" # Expected
```
