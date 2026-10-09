# Compute MCTQ social jetlag

**\[maturing\]**

`sjl()` computes the **relative or absolute social jetlag** for
standard, micro, and shift versions of the Munich ChronoType
Questionnaire (MCTQ).

`sjl_rel()` is just a wrapper for `sjl()` with `abs = FALSE`.

## Usage

``` r
sjl(msw, msf, abs = TRUE, method = "shorter")

sjl_rel(msw, msf, method = "shorter")
```

## Arguments

- msw:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of mid-sleep on workdays** from a
  standard, micro, or shift version of the MCTQ questionnaire. You can
  use [`msl()`](https://docs.ropensci.org/mctq/reference/msl.md) to
  compute it.

- msf:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of mid-sleep on work-free days**
  from a standard, micro, or shift version of the MCTQ questionnaire.
  You can use [`msl()`](https://docs.ropensci.org/mctq/reference/msl.md)
  to compute it.

- abs:

  (optional) a [`logical`](https://rdrr.io/r/base/logical.html) object
  indicating if the function must return an absolute value (default:
  `TRUE`).

- method:

  (optional) a string indicating which method the function must use to
  compute the social jetlag. See the Methods section to learn more
  (default: `"shorter"`).

## Value

- If `abs = TRUE`, a
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the absolute social jetlag.

- If `abs = FALSE`, a
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the relative social jetlag.

The output may also vary depending on the `method` used.

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
guidelines for `sjl()` (\\SJL\_{rel}\\ and \\SJL\\) computation are as
follows.

### Notes

- For MCTQ\\^{Shift}\\, the computation below must be applied to each
  shift section of the questionnaire.

- Due to time arithmetic issues, `sjl()` does a slightly different
  computation by default than those proposed by the authors mentioned
  above. See
  [`vignette("sjl-computation", package = "mctq")`](https://docs.ropensci.org/mctq/articles/sjl-computation.md)
  for more details.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$SJL\_{rel} = MSF - MSW\$\$ \$\$SJL = \| MSF - MSW \|\$\$

Where:

- \\SJL\_{rel}\\ = Relative social jetlag.

- \\SJL\\ = Absolute social jetlag.

- \\MSW\\ = Local time of mid-sleep on workdays.

- \\MSF\\ = Local time of mid-sleep on work-free days.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

### For the shift version of the MCTQ

\$\$SJL\_{rel}^{M/E/N} = MSF^{M/E/N} - MSW^{M/E/N}\$\$ \$\$SJL^{M/E/N} =
\| MSF^{M/E/N} - MSW^{M/E/N} \|\$\$

Where:

- \\SJL\_{rel}^{M/E/N}\\ = Relative social jetlag in a particular shift.

- \\SJL^{M/E/N}\\ = Absolute social jetlag in a particular shift.

- \\MSW^{M/E/N}\\ = Local time of mid-sleep between two days in a
  particular shift.

- \\MSF^{M/E/N}\\ = Local time of mid-sleep between two free days after
  a particular shift.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days, \\M\\ = Morning shift;
\\E\\ = Evening shift; \\N\\ = Night shift.

## Methods for computing the social jetlag

There are different approaches to compute the social jetlag (\\SJL\\).
By default, `sjl()` uses an approach that we call "the shorter interval
approach" (`"shorter"`).

The topics below provide a simple explanation of each method supported
by `sjl()`. To get a detail understating of this methods, see
[`vignette("sjl-computation", package = "mctq")`](https://docs.ropensci.org/mctq/articles/sjl-computation.md).

- `"difference"`

By using `method = "difference"`, `sjl()` will do the exact computation
proposed by the MCTQ authors, i.e., \\SJL\\ will be computed as the
linear difference between \\MSF\\ and \\MSW\\ (see the Guidelines
section).

**We do not recommend using this method**, as it has many limitations.

- `"shorter"`

This is the default method for `sjl()`. It's based on the shorter
interval between \\MSW\\ and \\MSF\\, solving most of the issues
relating to \\SJL\\ computation.

- `"longer"`

The `"longer"` method uses the same logic of the `"shorter"` method,
but, instead of using the shorter interval between \\MSW\\ and \\MSF\\,
it uses the longer interval between the two, considering a two-day
window.

This method may help in special contexts, like when dealing with
shift-workers that have a greater than 12 hours distance between their
mid-sleep hours.

## References

Ghotbi, N., Pilz, L. K., Winnebeck, E. C., Vetter, C., Zerbini, G.,
Lenssen, D., Frighetto, G., Salamanca, M., Costa, R., Montagnese, S., &
Roenneberg, T. (2020). The \\\mu\\MCTQ: an ultra-short version of the
Munich ChronoType Questionnaire. *Journal of Biological Rhythms*,
*35*(1), 98-110.
[doi:10.1177/0748730419886986](https://doi.org/10.1177/0748730419886986)

Jankowski K. S. (2017). Social jet lag: sleep-corrected formula.
*Chronobiology International*, *34*(4), 531-535.
[doi:10.1080/07420528.2017.1299162](https://doi.org/10.1080/07420528.2017.1299162)

Juda, M., Vetter, C., & Roenneberg, T. (2013). The Munich ChronoType
Questionnaire for shift-workers (MCTQ\\^{Shift}\\). *Journal of
Biological Rhythms*, *28*(2), 130-140.
[doi:10.1177/0748730412475041](https://doi.org/10.1177/0748730412475041)

Roenneberg T., Allebrandt K. V., Merrow M., & Vetter C. (2012). Social
jetlag and obesity. *Current Biology*, *22*(10), 939-43.
[doi:10.1016/j.cub.2012.03.038](https://doi.org/10.1016/j.cub.2012.03.038)

Roenneberg, T., Pilz, L. K., Zerbini, G., & Winnebeck, E. C. (2019).
Chronotype and social jetlag: a (self-) critical review. *Biology*,
*8*(3), 54.
[doi:10.3390/biology8030054](https://doi.org/10.3390/biology8030054)

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
[`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
[`sjl_weighted()`](https://docs.ropensci.org/mctq/reference/sjl_weighted.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

msw <- hms::parse_hm("03:30")
msf <- hms::parse_hm("05:00")

sjl(msw, msf)
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected
sjl(msw, msf, abs = FALSE)
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected
sjl_rel(msw, msf) # Wrapper function
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected

msw <- hms::parse_hm("04:30")
msf <- hms::parse_hm("23:30")

sjl(msw, msf)
#> [1] "18000s (~5 hours)"
#> [1] "18000s (~5 hours)" # Expected
sjl(msw, msf, abs = FALSE)
#> [1] "-18000s (~-5 hours)"
#> [1] "18000s (~-5 hours)" # Expected
sjl_rel(msw, msf) # Wrapper function
#> [1] "-18000s (~-5 hours)"
#> [1] "18000s (~-5 hours)" # Expected

msw <- hms::as_hms(NA)
msf <- hms::parse_hm("05:15")

sjl(msw, msf)
#> [1] NA
#> [1] NA # Expected

## Vector example

msw <- c(hms::parse_hm("02:05"), hms::parse_hm("04:05"))
msf <- c(hms::parse_hm("23:05"), hms::parse_hm("04:05"))

sjl(msw, msf)
#> [1] "10800s (~3 hours)" "0s"               
#> [1] "10800s (~3 hours)" "0s" # Expected
sjl(msw, msf, abs = FALSE)
#> [1] "-10800s (~-3 hours)" "0s"                 
#> [1] "-10800s (~-3 hours)" "0s" # Expected
sjl_rel(msw, msf) # Wrapper function
#> [1] "-10800s (~-3 hours)" "0s"                 
#> [1] "-10800s (~-3 hours)" "0s" # Expected

## Using different methods

msw <- hms::parse_hm("19:15")
msf <- hms::parse_hm("02:30")

sjl(msw, msf, abs = FALSE, method = "difference")
#> [1] "-60300s (~-16.75 hours)"
#> [1] "-60300s (~-16.75 hours)" # Expected
sjl(msw, msf, abs = FALSE, method = "shorter") # Default method
#> [1] "26100s (~7.25 hours)"
#> [1] "26100s (~7.25 hours)" # Expected
sjl(msw, msf, abs = FALSE, method = "longer")
#> [1] "-60300s (~-16.75 hours)"
#> [1] "-60300s (~-16.75 hours)" # Expected

msw <- hms::parse_hm("02:45")
msf <- hms::parse_hm("04:15")

sjl(msw, msf, abs = FALSE, method = "difference")
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected
sjl(msw, msf, abs = FALSE, method = "shorter") # Default method
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected
sjl(msw, msf, abs = FALSE, method = "longer")
#> [1] "-81000s (~-22.5 hours)"
#> [1] "-81000s (~-22.5 hours)" # Expected

## Converting the output to 'hms'

msw <- hms::parse_hm("01:15")
msf <- hms::parse_hm("03:25")
sjl(msw, msf)
#> [1] "7800s (~2.17 hours)"
#> [1] "7800s (~2.17 hours)" # Expected

hms::as_hms(as.numeric(sjl(msw, msf)))
#> 02:10:00
#> 02:10:00 # Expected

## Rounding the output at the seconds level

msw <- hms::parse_hms("04:19:33.1234")
msf <- hms::parse_hms("02:55:05")
sjl(msw, msf)
#> [1] "5068.1234s (~1.41 hours)"
#> [1] "5068.12339997292s (~1.41 hours)" # Expected

mctq:::round_time(sjl(msw, msf))
#> [1] "5068s (~1.41 hours)"
#> [1] "5068s (~1.41 hours)" # Expected
```
