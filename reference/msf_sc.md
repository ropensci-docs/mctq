# Compute MCTQ sleep-corrected local time of mid-sleep on work-free days

**\[maturing\]**

`msf_sc()` computes the **sleep-corrected local time of mid-sleep on
work-free days** for standard, micro, and shift versions of the Munich
ChronoType Questionnaire (MCTQ).

When using the shift version of the MCTQ, replace the value of `sd_week`
to `sd_overall`, as instructed in the Arguments section.

## Usage

``` r
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
```

## Arguments

- msf:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of mid-sleep on work-free days**
  from a standard, micro, or shift version of the MCTQ questionnaire.
  You can use [`msl()`](https://docs.ropensci.org/mctq/reference/msl.md)
  to compute it.

- sd_w:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration on work days** from a
  standard, micro, or shift version of the MCTQ questionnaire. You can
  use [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to
  compute it.

- sd_f:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **sleep duration on work-free days** from
  a standard, micro, or shift version of the MCTQ questionnaire. You can
  use [`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) to
  compute it.

- sd_week:

  A
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the **average weekly sleep duration** from a
  standard or micro version of the MCTQ questionnaire (you can use
  [`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md) to
  compute it) **or** the **overall sleep duration of a particular
  shift** from a shift version of the MCTQ questionnaire (you can use
  [`sd_overall()`](https://docs.ropensci.org/mctq/reference/sd_overall.md)
  to compute it).

- alarm_f:

  A [`logical`](https://rdrr.io/r/base/logical.html) object
  corresponding to the **alarm clock use on work-free days** from a
  standard, micro, or shift version of the MCTQ questionnaire. Note
  that, if `alarm_f == TRUE`, `msf_sc` cannot be computed, `msf_sc()`
  will return `NA` for these cases. For the \\\mu\\MCTQ, this value must
  be set as `FALSE` all times, since the questionnaire considers only
  the work-free days when the respondent does not use an alarm (e.g.,
  `alarm_f = rep(FALSE, length(msf))`).

## Value

An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
corresponding to the MCTQ chronotype or sleep-corrected local time of
mid-sleep on work-free days.

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
Platform (n.d.) guidelines for `msf_sc()` (\\MSF\_{sc}\\) computation
are as follows.

### Notes

- For all cases, \\MSF\_{sc}\\ cannot be computed if the participant
  wakes up with an alarm clock on work-free days (\\Alarm_F\\).

- For MCTQ\\^{Shift}\\, the computation below must be applied to each
  shift section of the questionnaire.

- \\MSF\_{sc}\\ is a proxy for the subject chronotype in standard and
  micro versions of the MCTQ.

- The basis for estimating chronotype in shift-workers is the mid-sleep
  on work-free days after evening shifts (\\MSF^E\\). In case work
  schedules do not comprise evening shifts, Juda, Vetter, &
  Roenneberg (2013) propose to derive it from the \\MSF\_{sc}\\ of other
  shifts (e.g., by using a linear model). Unfortunately, the `mctq`
  package can't help you with that, as it requires a closer look at your
  data.

- \\MSF\_{sc}\\ depends on developmental and environmental conditions
  (e.g., age, light exposure). For epidemiological and genetic studies,
  \\MSF\_{sc}\\ must be normalized for age and sex to make populations
  of different age and sex compositions comparable (Roenneberg,
  Allebrandt, Merrow, & Vetter, 2012).

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$\textrm{If } Alarm\_{F} = True \\ , \\ MSF\_{sc} = \textrm{Not
Available (NA)}\$\$ \$\$\textrm{Else if } SD_F \leq SD_W \\ , \\
MSF\_{sc} = MSF\$\$ \$\$\textrm{Else } \\ , \\ MSF\_{sc} = MSF -
\frac{SD_F - SD\_{week}}{2}\$\$

Where:

- \\MSF\_{sc}\\ = Sleep-corrected local time of mid-sleep on work-free
  days.

- \\Alarm\_{F}\\ = A [`logical`](https://rdrr.io/r/base/logical.html)
  value indicating if the respondent uses an alarm clock to wake up on
  work-free days.

- \\MSF\\ = Local time of mid-sleep on work-free days.

- \\SD_W\\ = Sleep duration on workdays.

- \\SD_F\\ = Sleep duration on work-free days.

- \\SD\_{week}\\ = Average weekly sleep duration.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

Note that, since:

\$\$MSF = SO\_{F} + \frac{SD\_{F}}{2}\$\$

Where:

- \\MSF\\ = Local time of mid-sleep on work-free days.

- \\SO\_{F}\\ = Local time of sleep onset on work-free days.

- \\SD\_{F}\\ = Sleep duration on work-free days.

The last condition of the \\MSF\_{sc}\\ computation can be simplified
to:

\$\$MSF\_{sc} = SO\_{F} + \frac{SD\_{F}}{2} - \frac{SD\_{F} -
SD\_{week}}{2}\$\$ \$\$MSF\_{sc} = SO\_{F} + \frac{SD\_{F}}{2} -
\frac{SD\_{F}}{2} + \frac{SD\_{week}}{2}\$\$ \$\$MSF\_{sc} = SO\_{F} +
\frac{SD\_{week}}{2}\$\$

### For the shift version of the MCTQ

\$\$\textrm{If } Alarm\_{F}^{M/E/N} = True \\ , \\ MSF\_{sc}^{M/E/N} =
\textrm{Not Available (NA)}\$\$ \$\$\textrm{Else if } SD\_{F}^{M/E/N}
\leq SD\_{W}^{M/E/N} \\ , \\ MSF\_{sc}^{M/E/N} = MSF^{M/E/N}\$\$
\$\$\textrm{Else } \\ , \\ MSF\_{sc}^{M/E/N} = MSF^{M/E/N} -
\frac{SD\_{F}^{M/E/N} - \emptyset SD^{M/E/N}}{2}\$\$

Where:

- \\MSF\_{sc}^{M/E/N}\\ = Sleep-corrected local time of mid-sleep
  between two free days after a particular shift.

- \\Alarm\_{F}^{M/E/N}\\ = A
  [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent uses an alarm clock to wake up between two free days
  after a particular shift.

- \\MSF^{M/E/N}\\ = Local time of mid-sleep between two free days after
  a particular shift.

- \\SD\_{W}^{M/E/N}\\ = Sleep duration between two days in a particular
  shift.

- \\SD\_{F}^{M/E/N}\\ = Sleep duration between two free days after a
  particular shift.

- \\\emptyset SD^{M/E/N}\\ = Overall sleep duration of a particular
  shift.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days, \\M\\ = Morning shift;
\\E\\ = Evening shift; \\N\\ = Night shift.

Note that, since:

\$\$MSF^{M/E/N} = SO\_{F}^{M/E/N} + \frac{SD\_{F}^{M/E/N}}{2}\$\$

Where:

- \\MSF^{M/E/N}\\ = Local time of mid-sleep between two free days after
  a particular shift.

- \\SO\_{F}^{M/E/N}\\ = Local time of sleep onset between two free days
  after a particular shift.

- \\SD\_{F}^{M/E/N}\\ = Sleep duration between two free days after a
  particular shift.

The last condition of the \\MSF\_{sc}^{M/E/N}\\ computation can be
simplified to:

\$\$MSF\_{sc}^{M/E/N} = SO\_{F}^{M/E/N} + \frac{SD\_{F}^{M/E/N}}{2} -
\frac{SD\_{F}^{M/E/N} - \emptyset SD^{M/E/N}}{2}\$\$
\$\$MSF\_{sc}^{M/E/N} = SO\_{F}^{M/E/N} + \frac{SD\_{F}^{M/E/N}}{2} -
\frac{SD\_{F}^{M/E/N}}{2} + \frac{\emptyset SD^{M/E/N}}{2}\$\$
\$\$MSF\_{sc}^{M/E/N} = SO\_{F}^{M/E/N} + \frac{\emptyset
SD^{M/E/N}}{2}\$\$

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

msf <- hms::parse_hms("04:00:00")
sd_w <- lubridate::dhours(6)
sd_f <- lubridate::dhours(7)
sd_week <- lubridate::dhours(6.29)
alarm_f <- FALSE
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
#> 03:38:42
#> 03:38:42 # Expected

msf <- hms::parse_hm("01:00:00")
sd_w <- lubridate::dhours(5.5)
sd_f <- lubridate::dhours(9)
sd_week <- lubridate::dhours(6.75)
alarm_f <- FALSE
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
#> 23:52:30
#> 23:52:30 # Expected

msf <- hms::parse_hms("05:40:00")
sd_w <- lubridate::dhours(7.5)
sd_f <- lubridate::dhours(10)
sd_week <- lubridate::dhours(8.5)
alarm_f <- TRUE
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
#> NA
#> NA # Expected (`msf_sc` cannot be computed if `alarm_f == TRUE`)

## Vector example

msf <- c(hms::parse_hms("03:45:00"), hms::parse_hm("04:45:00"))
sd_w <- c(lubridate::dhours(9), lubridate::dhours(6.45))
sd_f <- c(lubridate::dhours(5), lubridate::dhours(10))
sd_week <- c(lubridate::dhours(8.5), lubridate::dhours(9.2))
alarm_f <- c(FALSE, FALSE)
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
#> 03:45:00
#> 04:21:00
#> 03:45:00 # Expected
#> 04:21:00 # Expected

## Rounding the output at the seconds level

msf <- hms::parse_hms("05:40:00")
sd_w <- lubridate::dhours(5.43678)
sd_f <- lubridate::dhours(9.345111)
sd_week <- lubridate::dhours(7.5453)
alarm_f <- FALSE
msf_sc(msf, sd_w, sd_f, sd_week, alarm_f)
#> 04:46:00.3402
#> 04:46:00.3402 # Expected

mctq:::round_time(msf_sc(msf, sd_w, sd_f, sd_week, alarm_f))
#> 04:46:00
#> 04:46:00 # Expected
```
