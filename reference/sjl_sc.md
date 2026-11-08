# Compute Jankowski's MCTQ sleep-corrected social jetlag

**\[maturing\]**

`sjl_sc()` computes the **Jankowski's (2017) sleep-corrected social
jetlag** for standard, micro, and shift versions of the Munich
ChronoType Questionnaire (MCTQ).

`sjl_sc_rel()` is just a wrapper for `sjl_sc()` with `abs = FALSE`.

Please note that the Jankowski (2017) did not proposed a "relative"
sleep-corrected social jetlag, but the user may consider using it.

## Usage

``` r
sjl_sc(so_w, se_w, so_f, se_f, abs = TRUE, method = "shorter")

sjl_sc_rel(so_w, se_w, so_f, se_f, method = "shorter")
```

## Arguments

- so_w:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep onset on workdays** from a
  standard, micro, or shift version of the MCTQ questionnaire. You can
  use [`so()`](https://docs.ropensci.org/mctq/reference/so.md) to
  compute it for the standard or shift version.

- se_w:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep end on workdays** from a
  standard, micro, or shift version of the MCTQ questionnaire.

- so_f:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep onset on work-free days**
  from a standard, micro, or shift version of the MCTQ questionnaire.
  You can use [`so()`](https://docs.ropensci.org/mctq/reference/so.md)
  to compute it for the standard or shift version.

- se_f:

  An [`hms`](https://hms.tidyverse.org/reference/hms.html) object
  corresponding to the **local time of sleep end on work-free days**
  from a standard, micro, or shift version of the MCTQ questionnaire.

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
  object corresponding to the absolute sleep-corrected social jetlag.

- If `abs = FALSE`, a
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
  object corresponding to the relative sleep-corrected social jetlag.

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

In an article published in 2017, Konrad S. Jankowski argued that the
original formula for computing the social jetlag (\\SJL\\) captures not
only the misalignment between social and biological time, but also the
sleep debt resulting from sleep deprivation during workdays. Jankowski
then proposed the following guideline for a sleep-corrected social
jetlag (\\SJL\_{sc}\\) computation.

### Notes

- The Jankowski's alternative is disputed. We recommend seeing
  Roenneberg, Pilz, Zerbini, & Winnebeck (2019) discussion about it (see
  item 3.4.2).

- For MCTQ\\^{Shift}\\, the computation below must be applied to each
  shift section of the questionnaire.

- Due to time arithmetic issues, `sjl_sc()` does a slightly different
  computation by default than those proposed by the author mentioned
  above. See
  [`vignette("sjl-computation", package = "mctq")`](https://docs.ropensci.org/mctq/articles/sjl-computation.md)
  for more details.

- If you are visualizing this documentation in plain text, you may have
  some trouble understanding the equations. You can see this
  documentation on the package
  [website](https://docs.ropensci.org/mctq/reference/).

### For standard and micro versions of the MCTQ

\$\$\textrm{If } SD\_{W} \> SD\_{F} \\ \\ \\ SE\_{W} \leq SE\_{F} \\ ,
\\ SJL\_{sc} = \| SE\_{F} - SE\_{W} \|\$\$ \$\$\textrm{Else } \\ , \\
SJL\_{sc} = \| SO\_{F} - SO\_{W} \|\$\$

Where:

- \\SJL\_{sc}\\ = Jankowski's sleep-corrected social jetlag.

- \\SO\_{W}\\ = Local time of sleep onset on workdays.

- \\SE\_{W}\\ = Local time of sleep end on workdays.

- \\SO\_{F}\\ = Local time of sleep onset on work-free days.

- \\SE\_{F}\\ = Local time of sleep end on work-free days.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days.

### For the shift version of the MCTQ

\$\$\textrm{If } SD_W^{M/E/N} \> SD_F^{M/E/N} \\ \\ \\ SE_W^{M/E/N} \leq
SE_F^{M/E/N} \\ , \\ SJL\_{sc}^{M/E/N} = \| SE_F^{M/E/N} - SE_W^{M/E/N}
\|\$\$ \$\$\textrm{Else } \\ , \\ \| SJL\_{sc}^{M/E/N} = SO_F^{M/E/N} -
SO_W^{M/E/N} \|\$\$

Where:

- \\SJL\_{sc}^{M/E/N}\\ = Jankowski's sleep-corrected social jetlag in a
  particular shift.

- \\SO_W^{M/E/N}\\ = Local time of sleep onset between two days in a
  particular shift.

- \\SE_W^{M/E/N}\\ = Local time of sleep end between two days in a
  particular shift.

- \\SO_F^{M/E/N}\\ = Local time of sleep onset between two free days
  after a particular shift.

- \\SE_F^{M/E/N}\\ = Local time of sleep end between two free days after
  a particular shift.

**\*** \\W\\ = Workdays; \\F\\ = Work-free days, \\M\\ = Morning shift;
\\E\\ = Evening shift; \\N\\ = Night shift.

## Methods for computing the sleep-corrected social jetlag

There are different approaches to compute the sleep-corrected social
jetlag (\\SJL\_{sc}\\). By default, `sjl_sc()` uses an approach that we
call "the shorter interval approach" (`"shorter"`).

The topics below provide a simple explanation of each method supported
by `sjl_sc()`. To get a detail understating of this methods, see
[`vignette("sjl-computation", package = "mctq")`](https://docs.ropensci.org/mctq/articles/sjl-computation.md).

- `"difference"`

By using `method = "difference"`, `sjl_sc()` will do the exact
computation proposed by Jankowski, i.e., \\SJL\_{sc}\\ will be computed
as the linear difference between \\SO_f\\/\\SE_f\\ and \\SO_W\\/\\SE_W\\
(see the Guidelines section).

**We do not recommend using this method**, as it has many limitations.

- `"shorter"`

This is the default method for `sjl_sc()`. It's based on the shorter
interval between \\SO_f\\/\\SE_f\\ and \\SO_W\\/\\SE_W\\, solving most
of the issues relating to \\SJL\_{sc}\\ computation.

- `"longer"`

The `"longer"` method uses the same logic of the `"shorter"` method,
but, instead of using the shorter interval between \\SO_f\\/\\SE_f\\ and
\\SO_W\\/\\SE_W\\, it uses the longer interval between the two,
considering a two-day window.

This method may help in special contexts, like when dealing with
shift-workers that have a greater than 12 hours distance between their
sleep hours.

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
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_weighted()`](https://docs.ropensci.org/mctq/reference/sjl_weighted.md),
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

so_w <- hms::parse_hm("02:00")
se_w <- hms::parse_hm("10:00")
so_f <- hms::parse_hm("01:00")
se_f <- hms::parse_hm("08:00")

sjl_sc(so_w, se_w, so_f, se_f)
#> [1] "3600s (~1 hours)"
#> [1] "3600s (~1 hours)" # Expected
sjl_sc(so_w, se_w, so_f, se_f, abs = FALSE)
#> [1] "-3600s (~-1 hours)"
#> [1] "-3600s (~-1 hours)" # Expected (negative sjl_sc)
sjl_sc_rel(so_w, se_w, so_f, se_f) # Wrapper function
#> [1] "-3600s (~-1 hours)"
#> [1] "-3600s (~-1 hours)" # Expected (negative sjl_sc)
sjl(msl(so_w, sdu(so_w, se_w)), msl(so_f, sdu(so_f, se_f)))
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected

so_w <- hms::parse_hm("22:00")
se_w <- hms::parse_hm("06:00")
so_f <- hms::parse_hm("01:00")
se_f <- hms::parse_hm("06:00") # sd_w > sd_f & se_w <= se_f

sjl_sc(so_w, se_w, so_f, se_f) # sjl_sc = | se_f - se_w |
#> [1] "0s"
#> [1] "0s" # Expected
sjl_sc(so_w, se_w, so_f, se_f, abs = FALSE)
#> [1] "0s"
#> [1] "0s" # Expected
sjl_sc_rel(so_w, se_w, so_f, se_f) # Wrapper function
#> [1] "0s"
#> [1] "0s" # Expected
sjl(msl(so_w, sdu(so_w, se_w)), msl(so_f, sdu(so_f, se_f)))
#> [1] "5400s (~1.5 hours)"
#> [1] "5400s (~1.5 hours)" # Expected

so_f <- hms::as_hms(NA)

sjl_sc(so_w, se_w, so_f, se_f)
#> [1] NA
#> [1] NA # Expected

## Vector example

so_w <- c(hms::parse_hm("00:00"), hms::parse_hm("01:00"))
se_w <- c(hms::parse_hm("08:00"), hms::parse_hm("07:00"))
so_f <- c(hms::parse_hm("01:00"), hms::parse_hm("01:00"))
se_f <- c(hms::parse_hm("09:00"), hms::parse_hm("09:00"))

sjl_sc(so_w, se_w, so_f, se_f)
#> [1] "3600s (~1 hours)" "0s"              
#> [1] "3600s (~1 hours)" "0s" # Expected
sjl_sc(so_w, se_w, so_f, se_f, abs = FALSE)
#> [1] "3600s (~1 hours)" "0s"              
#> [1] "3600s (~1 hours)" "0s" # Expected
sjl_sc_rel(so_w, se_w, so_f, se_f) # Wrapper function
#> [1] "3600s (~1 hours)" "0s"              
#> [1] "3600s (~1 hours)" "0s" # Expected
sjl(msl(so_w, sdu(so_w, se_w)), msl(so_f, sdu(so_f, se_f)))
#> [1] "3600s (~1 hours)" "3600s (~1 hours)"
#> [1] "3600s (~1 hours)" "3600s (~1 hours)" # Expected

## See other examples in '?sjl()'
```
