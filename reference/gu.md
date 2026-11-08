# Compute MCTQ local time of getting out of bed

**\[maturing\]**

`gu()` computes the **local time of getting out of bed** for standard
and shift versions of the Munich ChronoType Questionnaire (MCTQ).

## Usage

``` r
gu(se, si)
```

## Arguments

- se:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep end** from a standard or
  shift version of the MCTQ questionnaire.

- si:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the "**sleep inertia**" or **time to get up**
  from a standard or shift version of the MCTQ questionnaire.

## Value

An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
corresponding to the vectorized sum of `se` and `si` in a circular time
frame of 24 hours.

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
guidelines for `gu()` (\\GU\\) computation are as follows.

### Notes

- This computation must be applied to each section of the questionnaire.

- MCTQ\\^{Shift}\\ uses \\TGU\\ (time to get up) instead of \\SI\\
  (sleep inertia). For the purpose of this computation, both represent
  the same thing.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$GU\_{W/F} = SE\_{W/F} + SI\_{W/F}\$\$

Where:

- \\GU\_{W/F}\\ = Local time of getting out of bed on work **or**
  work-free days.

- \\SE\_{W/F}\\ = Local time of sleep end on work **or** work-free days.

- \\SI\_{W/F}\\ = Sleep inertia on work **or** work-free days ("after
  \_\_\_ min, I get up").

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

### For the shift version of the MCTQ

\$\$GU\_{W/F}^{M/E/N} = SE\_{W/F}^{M/E/N} + TGU\_{W/F}^{M/E/N}\$\$

Where:

- \\GU\_{W/F}^{M/E/N}\\ = Local time of getting out of bed between two
  days in a particular shift **or** between two free days after a
  particular shift.

- \\SE\_{W/F}^{M/E/N}\\ = Local time of sleep end between two days in a
  particular shift **or** between two free days after a particular
  shift.

- \\TGU\_{W/F}^{M/E/N}\\ = Time to get up after sleep end between two
  days in a particular shift **or** between two free days after a
  particular shift ("after \_\_\_ min, I get up").

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
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

gu(hms::parse_hm("08:00"), lubridate::dminutes(10))
#> 08:10:00
#> 08:10:00 # Expected
gu(hms::parse_hm("11:45"), lubridate::dminutes(90))
#> 13:15:00
#> 13:15:00 # Expected
gu(hms::as_hms(NA), lubridate::dminutes(90))
#> NA
#> NA # Expected

## Vector example

se <- c(hms::parse_hm("12:30"), hms::parse_hm("23:45"))
si <- c(lubridate::dminutes(10), lubridate::dminutes(70))
gu(se, si)
#> 12:40:00
#> 00:55:00
#> 12:40:00 # Expected
#> 00:55:00 # Expected
```
