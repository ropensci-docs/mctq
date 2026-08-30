# Compute MCTQ total time in bed

**\[maturing\]**

`tbt()` computes the **total time in bed** for standard and shift
versions of the Munich ChronoType Questionnaire (MCTQ).

## Usage

``` r
tbt(bt, gu)
```

## Arguments

- bt:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of going to bed** from a standard or
  shift version of the MCTQ questionnaire.

- gu:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of getting out of bed** from a
  standard or shift version of the MCTQ questionnaire. You can use
  [`gu()`](https://docs.ropensci.org/mctq/reference/gu.md) to compute
  it.

## Value

A [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
object corresponding to the vectorized difference between `gu` and `bt`
in a circular time frame of 24 hours.

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

Roenneberg, Allebrandt, Merrow, & Vetter (2012), Juda, Vetter, &
Roenneberg (2013), and The Worldwide Experimental Platform (n.d.)
guidelines for `tbt()` (\\TBT\\) computation are as follows.

### Notes

- This computation must be applied to each section of the questionnaire.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$TBT\_{W/F} = GU\_{W/F} - BT\_{W/F}\$\$

Where:

- \\TBT\_{W/F}\\ = Total time in bed on work **or** work-free days.

- \\GU\_{W/F}\\ = Local time of getting out of bed on work **or**
  work-free days.

- \\BT\_{W/F}\\ = Local time of going to bed on work **or** work-free
  days ("I go to bed at \_\_\_ o'clock").

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

### For the shift version of the MCTQ

\$\$TBT\_{W/F}^{M/E/N} = GU\_{W/F}^{M/E/N} - BT\_{W/F}^{M/E/N}\$\$

Where:

- \\TBT\_{W/F}^{M/E/N}\\ = Total time in bed between two days in a
  particular shift **or** between two free days after a particular
  shift.

- \\GU\_{W/F}^{M/E/N}\\ = Local time of getting out of bed between two
  days in a particular shift **or** between two free days after a
  particular shift.

- \\BT\_{W/F}^{M/E/N}\\ = Local time of going to bed between two days in
  a particular shift **or** between two free days after a particular
  shift ("I go to bed at \_\_\_ o'clock").

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
[`sjl_weighted()`](https://docs.ropensci.org/mctq/reference/sjl_weighted.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md)

## Examples

``` r
## Scalar example

bt <- hms::parse_hm("22:10")
gu <- hms::parse_hm("06:15")
tbt(bt, gu)
#> [1] "29100s (~8.08 hours)"
#> [1] "29100s (~8.08 hours)" # Expected

bt <- hms::parse_hm("01:20")
gu <- hms::parse_hm("14:00")
tbt(bt, gu)
#> [1] "45600s (~12.67 hours)"
#> [1] "45600s (~12.67 hours)" # Expected

bt <- hms::as_hms(NA)
gu <- hms::parse_hm("07:20")
tbt(bt, gu)
#> [1] NA
#> [1] NA # Expected

## Vector example

bt <- c(hms::parse_hm("23:50"), hms::parse_hm("02:30"))
gu <- c(hms::parse_hm("09:30"), hms::parse_hm("11:25"))
tbt(bt, gu)
#> [1] "34800s (~9.67 hours)" "32100s (~8.92 hours)"
#> [1] "34800s (~9.67 hours)" "32100s (~8.92 hours)" # Expected
```
