# Compute MCTQ weekly sleep loss

**\[maturing\]**

`sloss_week()` computes the **weekly sleep loss** for the standard and
micro versions of the Munich ChronoType Questionnaire (MCTQ).

## Usage

``` r
sloss_week(sd_w, sd_f, wd)
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
object corresponding to the weekly sleep loss.

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
Experimental Platform (n.d.) guidelines for `sloss_week()`
(\\SLoss\_{week}\\) computation are as follows.

### Notes

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### Computation

\$\$\textrm{If } SD\_{week} \> SD_W \\ , \\ SLoss\_{week} =
(SD\_{week} - SD_W) \times WD\$\$ \$\$\textrm{Else } \\ , \\
SLoss\_{week} = (SD\_{week} - SD_F) \times FD\$\$

Where:

- \\SLoss\_{week}\\: Weekly sleep loss.

- \\SD_W\\ = Sleep duration on workdays.

- \\SD_F\\ = Sleep duration on work-free days.

- \\SD\_{week}\\ = Average weekly sleep duration.

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

## Examples

``` r
## Scalar example

sd_w <- lubridate::dhours(6.5)
sd_f <- lubridate::dhours(7)
wd <- 4
sloss_week(sd_w, sd_f, wd)
#> [1] "3085.71428571429s (~51.43 minutes)"
#> [1] "3085.71428571429s (~51.43 minutes)" # Expected

sd_w <- lubridate::dhours(7)
sd_f <- lubridate::dhours(8)
wd <- 5
sloss_week(sd_w, sd_f, wd)
#> [1] "5142.85714285714s (~1.43 hours)"
#> [1] "5142.85714285714s (~1.43 hours)" # Expected

sd_w <- lubridate::dhours(NA)
sd_f <- lubridate::dhours(9.45)
wd <- 7
sloss_week(sd_w, sd_f, wd)
#> [1] NA
#> [1] NA # Expected

## Vector example

sd_w <- c(lubridate::dhours(7), lubridate::dhours(8))
sd_f <- c(lubridate::dhours(6.5), lubridate::dhours(8))
wd <- c(2, 0)
sloss_week(sd_w, sd_f, wd)
#> [1] "2571.42857142857s (~42.86 minutes)" "0s"                                
#> [1] "2571.42857142857s (~42.86 minutes)" "0s" # Expected

## Converting the output to 'hms'

sd_w <- lubridate::dhours(4)
sd_f <- lubridate::dhours(5)
wd <- 3
sloss_week(sd_w, sd_f, wd)
#> [1] "6171.42857142858s (~1.71 hours)"
#> [1] "6171.42857142858s (~1.71 hours)" # Expected

hms::as_hms(as.numeric(sloss_week(sd_w, sd_f, wd)))
#> 01:42:51.428571
#> 01:42:51.428571 # Expected

## Rounding the output at the seconds level

sd_w <- lubridate::dhours(5.8743)
sd_f <- lubridate::dhours(7.4324)
wd <- 6
sloss_week(sd_w, sd_f, wd)
#> [1] "4807.85142857144s (~1.34 hours)"
#> [1] "4807.85142857144s (~1.34 hours)" # Expected

mctq:::round_time(sloss_week(sd_w, sd_f, wd))
#> [1] "4808s (~1.34 hours)"
#> [1] "4808s (~1.34 hours)" # Expected
```
