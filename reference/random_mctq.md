# Build a random MCTQ case

**\[maturing\]**

`random_mctq` builds a fictional Munich ChronoType Questionnaire (MCTQ)
case composed of MCTQ basic/measurable variables.

This function is **for testing and learning purposes only**. Please
don't misuse it.

## Usage

``` r
random_mctq(model = "standard")
```

## Arguments

- model:

  A string indicating the data model to return. Valid values are:
  `"standard"`, "`shift"`, and `"micro"` (default: `"standard"`).

## Value

A named [`list`](https://rdrr.io/r/base/list.html) with elements
representing each MCTQ basic/measurable variable of the model indicated
in the `model` argument.

## Details

The case structure (variable names and classes) are the same as the
datasets provided by the `mctq` package. See
[`?std_mctq`](https://docs.ropensci.org/mctq/reference/std_mctq.md),
[`?micro_mctq`](https://docs.ropensci.org/mctq/reference/micro_mctq.md)
and
[`?shift_mctq`](https://docs.ropensci.org/mctq/reference/shift_mctq.md)
to learn more.

### Requirements

This function requires the
[`stats`](https://rdrr.io/r/stats/stats-package.html) package. This
won't be an issue for most people since the package comes with a
standard R installation.

If you don't have the
[`stats`](https://rdrr.io/r/stats/stats-package.html) package, you can
install it with `install.packages("stats")`.

### Cases

Random standard and micro MCTQ cases were created with the general
population in mind. The data was set to resemble the distribution
parameters shown in Roenneberg, Wirz-Justice, & Merrow (2003).

MCTQ\\^{Shift}\\ random cases were created based on the shift
configuration from "Study Site 1" shown in Vetter, Juda, & Roenneberg
(2012). The data was set to resemble the distribution parameters shown
in Juda, Vetter, & Roenneberg (2013).

You can see more about the distribution parameters used
[here](https://github.com/ropensci/mctq/blob/main/data-raw/random_mctq.R).

## References

Juda, M., Vetter, C., & Roenneberg, T. (2013). The Munich ChronoType
Questionnaire for shift-workers (MCTQ\\^{Shift}\\). *Journal of
Biological Rhythms*, *28*(2), 130-140.
[doi:10.1177/0748730412475041](https://doi.org/10.1177/0748730412475041)

Roenneberg, T., Wirz-Justice, A., & Merrow, M. (2003). Life between
clocks: daily temporal patterns of human chronotypes. *Journal of
Biological Rhythms*, *18*(1), 80-90.
[doi:10.1177/0748730402239679](https://doi.org/10.1177/0748730402239679)

Vetter, C., Juda, M., & Roenneberg, T. (2012). The influence of internal
time, time awake, and sleep duration on cognitive performance in
shiftworkers. *Chronobiology International*, *29*(8), 1127-1138.
[doi:10.3109/07420528.2012.707999](https://doi.org/10.3109/07420528.2012.707999)

## See also

Other utility functions:
[`pretty_mctq()`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md),
[`raw_data()`](https://docs.ropensci.org/mctq/reference/raw_data.md)

## Examples

``` r
if (FALSE) { # \dontrun{
random_mctq("standard")
random_mctq("micro")
random_mctq("shift")
} # }
```
