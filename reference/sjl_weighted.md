# Compute MCTQ absolute social jetlag across all shifts

**\[maturing\]**

`sjl_weighted()` computes the **absolute social jetlag across all
shifts** for the shift version of the Munich ChronoType Questionnaire
(MCTQ).

## Usage

``` r
sjl_weighted(sjl, n_w)
```

## Arguments

- sjl:

  A [`list`](https://rdrr.io/r/base/list.html) object with
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  elements corresponding to the **social jetlag in each shift** from a
  shift version of the MCTQ questionnaire (you can use
  [`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md) to compute
  it). `sjl` elements and values must be paired with `n` elements and
  values.

- n_w:

  A [`list`](https://rdrr.io/r/base/list.html) object with
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`integer`](https://rdrr.io/r/base/integer.html) or
  [`double`](https://rdrr.io/r/base/double.html) elements corresponding
  to the **number of days worked in each shift within a shift cycle**
  from a shift version of the MCTQ questionnaire. `n` elements and
  values must be paired with `sjl` elements and values.

## Value

A [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
object corresponding to the vectorized weighted mean of `sjl` with `n_w`
as weights.

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

## Operation

The shift version of the MCTQ was developed for shift-workers rotating
through morning-, evening-, and night-shifts, but it also allows
adaptations to other shift schedules (Juda, Vetter, & Roenneberg, 2013).
For this reason, `sjl_weighted()` must operate with any shift
combination.

Considering the requirement above, `sjl_weighted()` was developed to
only accept [`list`](https://rdrr.io/r/base/list.html) objects as
arguments. For this approach to work, both `sjl` and `n_w` arguments
must be lists with paired elements and values, i.e., the first element
of `sjl` (e.g., `sjl_m`) must be paired with the first element of `n_w`
(e.g., `n_w_m`). The function will do the work of combining them and
output a weighted mean.

## Guidelines

Juda, Vetter, & Roenneberg (2013) and The Worldwide Experimental
Platform (n.d.) guidelines for `sjl_weighted()` (\\\emptyset
SJL\_{weighted}\\) computation are as follows.

### Notes

- The absolute social jetlag across all shifts (\\\emptyset
  SJL\_{weighted}\\) is the weighted average of all absolute social
  jetlags.

- The authors describe an equation for a three-shift schedule, but this
  may not be your case. That's why this function works a little bit
  differently (see the Operation section), allowing you to compute a
  weighted average with any shift combination.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### Computation

\$\$\emptyset SJL\_{weighted} = \frac{(\| SJL^{M} \| \times
n\_{W}^{M}) + (\| SJL^{E} \| \times n\_{W}^{E}) + (\| SJL^{N} \| \times
n\_{W}^{N})}{n\_{W}^{M} + n\_{W}^{E} + n\_{W}^{N}}\$\$

Where:

- \\\emptyset SJL\_{weighted}\\ = Absolute social jetlag across all
  shifts.

- \\SJL^{M/E/N}\\ = Absolute social jetlag in each shift.

- \\n\_{W}^{M/E/N}\\ = Number of days worked in each shift within a
  shift cycle.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days, \\M\\ = Morning shift;
\\E\\ = Evening shift; \\N\\ = Night shift.

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
[`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md),
[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md),
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

sjl <- list(sjl_m = lubridate::dhours(1.25),
            sjl_e = lubridate::dhours(0.5),
            sjl_n = lubridate::dhours(3))
n_w <- list(n_w_m = 3, n_w_e = 1, n_w_n = 4)
sjl_weighted(sjl, n_w)
#> [1] "7312.5s (~2.03 hours)"
#> [1] "7312.5s (~2.03 hours)" # Expected

sjl <- list(sjl_m = lubridate::dhours(1.25),
            sjl_e = lubridate::as.duration(NA),
            sjl_n = lubridate::dhours(3))
n_w <- list(n_w_m = 3, n_w_e = 1, n_w_n = 4)
sjl_weighted(sjl, n_w)
#> [1] NA
#> [1] NA # Expected

## Vector example

sjl <- list(sjl_m = c(lubridate::dhours(2), lubridate::dhours(2.45)),
            sjl_e = c(lubridate::dhours(3.21), lubridate::as.duration(NA)),
            sjl_n = c(lubridate::dhours(1.2), lubridate::dhours(5.32)))
n_w <- list(n_w_m = c(1, 3), n_w_e = c(4, 1), n_w_n = c(3, 3))
sjl_weighted(sjl, n_w)
#> [1] "8298s (~2.31 hours)" NA                   
#> [1] "8298s (~2.31 hours)" NA # Expected

## Checking the first output from vector example

if (requireNamespace("stats", quietly = TRUE)) {
    i <- 1
    x <- c(sjl[["sjl_m"]][i], sjl[["sjl_e"]][i], sjl[["sjl_n"]][i])
    w <- c(n_w[["n_w_m"]][i], n_w[["n_w_e"]][i], n_w[["n_w_n"]][i])
    lubridate::as.duration(stats::weighted.mean(x, w))
}
#> [1] "8298s (~2.31 hours)"
#> [1] "8298s (~2.31 hours)" # Expected

## Converting the output to hms

sjl <- list(sjl_m = lubridate::dhours(0.25),
            sjl_e = lubridate::dhours(1.2),
            sjl_n = lubridate::dhours(4.32))
n_w <- list(n_w_m = 4, n_w_e = 2, n_w_n = 1)

sjl_weighted(sjl, n_w)
#> [1] "3970.28571428571s (~1.1 hours)"
#> [1] "3970.28571428571s (~1.1 hours)" # Expected

hms::as_hms(as.numeric(sjl_weighted(sjl, n_w)))
#> 01:06:10.285714
#> 01:06:10.285714 # Expected

## Rounding the output at the seconds level

mctq:::round_time(sjl_weighted(sjl, n_w))
#> [1] "3970s (~1.1 hours)"
#> [1] "3970s (~1.1 hours)" # Expected

mctq:::round_time(hms::as_hms(as.numeric(sjl_weighted(sjl, n_w))))
#> 01:06:10
#> 01:06:10 # Expected
```
