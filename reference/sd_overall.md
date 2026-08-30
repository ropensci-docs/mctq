# Compute MCTQ overall sleep duration (only for MCTQ\\^{Shift}\\)

**\[maturing\]**

`sd_overall()` computes the **overall sleep duration in a particular
shift** for the shift version of the Munich ChronoType Questionnaire
(MCTQ).

See [`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md)
to compute the average weekly sleep duration for the standard and micro
versions of the MCTQ.

## Usage

``` r
sd_overall(sd_w, sd_f, n_w, n_f)
```

## Arguments

- sd_w:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration between two days in a
  particular shift** from a shift version of the MCTQ questionnaire. You
  can use [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to
  compute it.

- sd_f:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration between two free days
  after a particular shift** from a shift version of the MCTQ
  questionnaire. You can use
  [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to compute
  it.

- n_w:

  An
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`numeric`](https://rdrr.io/r/base/numeric.html) object or an
  [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
  to the **number of days worked in a particular shift within a shift
  cycle** from a shift version of the MCTQ questionnaire.

- n_f:

  An
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`numeric`](https://rdrr.io/r/base/numeric.html) object or an
  [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
  to the **number of free days after a particular shift within a shift
  cycle** from a shift version of the MCTQ questionnaire.

## Value

A [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
object corresponding to the vectorized weighted mean of `sd_w` and
`sd_f` with `n_w` and `n_f` as weights.

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

Juda, Vetter, & Roenneberg (2013) and The Worldwide Experimental
Platform (n.d.) guidelines for `sd_overall()` (\\\emptyset SD\\)
computation are as follows.

### Notes

- This computation must be applied to each section of the questionnaire.
  If you're using the three-shift design proposed by the MCTQ authors,
  you need to compute three overall sleep duration (e.g., \\\emptyset
  SD^M\\; \\\emptyset SD^E\\; \\\emptyset SD^N\\).

- The overall sleep duration is the weighted average of the
  shift-specific mean sleep durations.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### Computation

\$\$\emptyset SD^{M/E/N} = \frac{(SD\_{W}^{M/E/N} \times
n\_{W}^{M/E/N}) + (SD\_{F}^{M/E/N} \times n\_{F}^{M/E/N})}{n_W^{M/E/N} +
n\_{F}^{M/E/N}}\$\$

Where:

- \\\emptyset SD^{M/E/N}\\ = Overall sleep duration in a particular
  shift.

- \\SD_W^{M/E/N}\\ = Sleep duration between two days in a particular
  shift.

- \\SD_F^{M/E/N}\\ = Sleep duration between two free days after a
  particular shift.

- \\n_W^{M/E/N}\\ = Number of days worked in a particular shift within a
  shift cycle.

- \\n_F^{M/E/N}\\ = Number of free days after a particular shift within
  a shift cycle.

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

sd_w <- lubridate::dhours(5)
sd_f <- lubridate::dhours(9)
n_w <- 2
n_f <- 2
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] "25200s (~7 hours)"
#> [1] "25200s (~7 hours)" # Expected

sd_w <- lubridate::dhours(3.45)
sd_f <- lubridate::dhours(10)
n_w <- 3
n_f <- 1
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] "18315s (~5.09 hours)"
#> [1] "18315s (~5.09 hours)" # Expected

sd_w <- lubridate::as.duration(NA)
sd_f <- lubridate::dhours(12)
n_w <- 4
n_f <- 4
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] NA
#> [1] NA # Expected

## Vector example

sd_w <- c(lubridate::dhours(4), lubridate::dhours(7))
sd_f <- c(lubridate::dhours(12), lubridate::dhours(9))
n_w <- c(3, 4)
n_f <- c(2, 4)
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] "25920s (~7.2 hours)" "28800s (~8 hours)"  
#> [1] "25920s (~7.2 hours)" "28800s (~8 hours)"  # Expected

## Checking second output from vector example

if (requireNamespace("stats", quietly = TRUE)) {
    i <- 2
    x <- c(sd_w[i], sd_f[i])
    w <- c(n_w[i], n_f[i])
    lubridate::as.duration(stats::weighted.mean(x, w))
}
#> [1] "28800s (~8 hours)"
#> [1] "28800s (~8 hours)" # Expected

## Converting the output to 'hms'

sd_w <- lubridate::dhours(4.75)
sd_f <- lubridate::dhours(10)
n_w <- 5
n_f <- 2
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] "22500s (~6.25 hours)"
#> [1] "22500s (~6.25 hours)" # Expected

hms::as_hms(as.numeric(sd_overall(sd_w, sd_f, n_w, n_f)))
#> 06:15:00
#> 06:15:00 # Expected

## Rounding the output at the seconds level

sd_w <- lubridate::dhours(5.9874)
sd_f <- lubridate::dhours(9.3)
n_w <- 3
n_f <- 2
sd_overall(sd_w, sd_f, n_w, n_f)
#> [1] "26324.784s (~7.31 hours)"
#> [1] "26324.784s (~7.31 hours)" # Expected

mctq:::round_time(sd_overall(sd_w, sd_f, n_w, n_f))
#> [1] "26325s (~7.31 hours)"
#> [1] "26325s (~7.31 hours)" # Expected
```
