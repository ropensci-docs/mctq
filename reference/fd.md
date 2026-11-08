# Compute MCTQ work-free days

**\[maturing\]**

`fd()` computes the **number of work-free days per week** for standard
and micro versions of the Munich ChronoType Questionnaire (MCTQ).

## Usage

``` r
fd(wd)
```

## Arguments

- wd:

  An
  [integerish](https://mllg.github.io/checkmate/reference/checkIntegerish.html)
  [`numeric`](https://rdrr.io/r/base/numeric.html) object or an
  [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
  to the **number of workdays per week** from a standard or micro
  version of the MCTQ questionnaire.

## Value

An [`integer`](https://rdrr.io/r/base/integer.html) object corresponding
to the difference between the number of days in a week (7) and the
number of workdays (`wd`).

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

## Guidelines

Roenneberg, Allebrandt, Merrow, & Vetter (2012) and The Worldwide
Experimental Platform (n.d.) guidelines for `fd()` (\\FD\\) computation
are as follows.

\$\$FD = 7 - WD\$\$

Where:

- \\FD\\ = Number of work-free days per week.

- \\WD\\ = Number of workdays per week ("I have a regular work schedule
  and work \_\_\_ days per week").

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
[`so()`](https://docs.ropensci.org/mctq/reference/so.md),
[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md)

## Examples

``` r
## Scalar example

fd(5)
#> [1] 2
#> [1] 2 # Expected
fd(4)
#> [1] 3
#> [1] 3 # Expected
fd(as.numeric(NA))
#> [1] NA
#> [1] NA # Expected

## Vector example

fd(0:7)
#> [1] 7 6 5 4 3 2 1 0
#> [1] 7 6 5 4 3 2 1 0 # Expected
fd(c(1, NA))
#> [1]  6 NA
#> [1]  6 NA # Expected
```
