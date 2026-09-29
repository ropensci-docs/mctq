# Compute MCTQ local time of mid-sleep

**\[maturing\]**

`msl()` computes the **local time of mid-sleep** for standard, micro,
and shift versions of the Munich ChronoType Questionnaire (MCTQ).

Please note that, although we tried to preserve the original authors'
naming pattern for the MCTQ functions, the name `ms` provokes a
dangerous name collision with the
[`ms()`](https://lubridate.tidyverse.org/reference/hms.html) function (a
function for parsing minutes and seconds components). That's why we
named it `msl`. `msl()` and
[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) are the only
exceptions, all the other `mctq` functions maintain a strong naming
resemblance with the original authors' naming pattern.

## Usage

``` r
msl(so, sd)
```

## Arguments

- so:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep onset** from a standard,
  micro, or shift version of the MCTQ questionnaire. You can use
  [`so()`](https://docs.ropensci.org/mctq/reference/so.md) to compute it
  for the standard or shift version.

- sd:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration** from a standard, micro,
  or shift version of the MCTQ questionnaire. You can use
  [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to compute
  it for any MCTQ version.

## Value

An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
corresponding to the vectorized sum of `so` and `(sd / 2)` in a circular
time frame of 24 hours.

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
Juda, Vetter, & Roenneberg (2013), and The Worldwide Experimental
Platform (n.d.) guidelines for `msl()` (\\MSW\\ or \\MSF\\) computation
are as follows.

### Notes

- This computation must be applied to each section of the questionnaire.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$MS\_{W/F} = SO\_{W/F} + \frac{SD\_{W/F}}{2}\$\$

Where:

- \\MS\_{W/F}\\ = Local time of mid-sleep on work **or** work-free days.

- \\SO\_{W/F}\\ = Local time of sleep onset on work **or** work-free
  days.

- \\SD\_{W/F}\\ = Sleep duration on work **or** work-free days.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

### For the shift version of the MCTQ

\$\$MS\_{W/F}^{M/E/N} = SO\_{W/F}^{M/E/N} +
\frac{SD\_{W/F}^{M/E/N}}{2}\$\$

Where:

- \\MS\_{W/F}^{M/E/N}\\ = Local time of mid-sleep between two days in a
  particular shift **or** between two free days after a particular
  shift.

- \\SO\_{W/F}^{M/E/N}\\ = Local time of sleep onset between two days in
  a particular shift **or** between two free days after a particular
  shift.

- \\SD\_{W/F}^{M/E/N}\\ = Sleep duration between two days in a
  particular shift **or** between two free days after a particular
  shift.

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

so <- hms::parse_hm("23:30")
sd <- lubridate::dhours(8)
msl(so, sd)
#> 03:30:00
#> 03:30:00 # Expected

so <- hms::parse_hm("01:00")
sd <- lubridate::dhours(10)
msl(so, sd)
#> 06:00:00
#> 06:00:00 # Expected

so <- hms::as_hms(NA)
sd <- lubridate::dhours(7.5)
msl(so, sd)
#> NA
#> NA # Expected

## Vector example

so <- c(hms::parse_hm("00:10"), hms::parse_hm("01:15"))
sd <- c(lubridate::dhours(9.25), lubridate::dhours(5.45))
msl(so, sd)
#> 04:47:30
#> 03:58:30
#> [1] 04:47:30 # Expected
#> [1] 03:58:30 # Expected
```
