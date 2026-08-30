# A fictional \\\mu\\MCTQ dataset

**\[maturing\]**

A fictional dataset, **for testing and learning purposes**, composed of
basic/measurable and computed variables of the Munich ChronoType
Questionnaire (MCTQ) micro (\\\mu\\) version.

This data was created following the guidelines in Ghotbi et al. (2020),
in addition to the guidelines in Roenneberg, Wirz-Justice, & Merrow
(2003), Roenneberg, Allebrandt, Merrow, & Vetter (2012), Jankowski
(2017), and The Worldwide Experimental Platform (n.d.). See the
References and Details sections to learn more.

## Usage

``` r
micro_mctq
```

## Format

A [`tibble`](https://dplyr.tidyverse.org/reference/reexports.html) with
19 columns and 50 rows:

- id:

  A unique [`integer`](https://rdrr.io/r/base/integer.html) value to
  identify each respondent in the dataset.  
    
  Type: Control.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- shift_work:

  A
  [`logical`](https://rdrr.io/r/base/logical.html)` value indicating if the respondent has been a shift- or night-worker in the past three months. \cr \cr Statement (`EN`): "I have been a shift- or night-worker in the past three months: Yes ( ___ ) No ( ___ )". \cr \cr Type: Basic. \cr \cr R class: [`logical\`\][`base::logical()`](https://rdrr.io/r/base/logical.html).

- wd:

  Number of **workdays** per week.  
    
  Statement (`EN`): "Normally, I work \_\_\_ days/week".  
    
  Type: Basic.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- fd:

  Number of **work-free days** per week.  
    
  Type: Computed.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- so_w:

  Local time of sleep onset on **workdays**.  
    
  Statement (`EN`): "On WORKDAYS ... I normally fall asleep at \_\_\_ :
  \_\_\_ AM/PM (this is NOT when you get into bed, but rather when you
  fall asleep)".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- se_w:

  Local time of sleep end on **workdays**.  
    
  Statement (`EN`): "On WORKDAYS ... I normally wake up at \_\_\_ :
  \_\_\_ AM/PM (this is NOT when you get out of bed, but rather when you
  wake up)".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sd_w:

  Sleep duration on **workdays**.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- msw:

  Local time of mid-sleep on **workdays**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- so_f:

  Local time of sleep onset on **work-free days** when the respondent
  **doesn't** use an alarm clock to wake up.  
    
  Statement (`EN`): "On WORK-FREE DAYS when I DON'T use an alarm clock
  ... I normally fall asleep at \_\_\_ : \_\_\_ AM/PM (this is NOT when
  you get into bed, but rather when you fall asleep)".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- se_f:

  Local time of sleep end on **work-free days** when the respondent
  **doesn't** use an alarm clock to wake up.  
    
  Statement (`EN`): "On WORK-FREE DAYS when I DON'T use an alarm clock
  ... I normally wake up at \_\_\_ : \_\_\_ AM/PM (this is NOT when you
  get out of bed, but rather when you wake up)".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sd_f:

  Sleep duration on **work-free days** when the respondent **doesn't**
  use an alarm clock to wake up.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- msf:

  Local time of mid-sleep on **work-free days** when the respondent
  **doesn't** use an alarm clock to wake up.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sd_week:

  Average weekly sleep duration.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- sloss_week:

  Weekly sleep loss.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- msf_sc:

  Sleep-corrected local time of mid-sleep on **work-free days**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sjl_rel:

  Relative social jetlag.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- sjl:

  Absolute social jetlag.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- sjl_sc_rel:

  Jankowski's relative sleep-corrected social jetlag.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- sjl_sc:

  Jankowski's sleep-corrected social jetlag.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

## Source

Created by Daniel Vartanian (package author).

## Details

`micro_mctq` is a tidied, validated, and transformed version of
`raw_data("micro_mctq.csv")`.

### Guidelines

To learn more about the Munich ChronoType Questionnaire (MCTQ), see
Roenneberg, Wirz-Justice, & Merrow (2003), Roenneberg, Allebrandt,
Merrow, & Vetter (2012), Roenneberg et al. (2015), and Roenneberg, Pilz,
Zerbini, & Winnebeck (2019).

To know about different MCTQ versions, see Juda, Vetter, & Roenneberg
(2013) and Ghotbi et.al (2020).

To learn about the sleep-corrected social jetlag, see Jankowski (2017).

If you're curious about the variable computations and want to have
access to the full questionnaire, see The Worldwide Experimental
Platform (n.d.).

### Data building and data wrangling

This dataset was created by randomized sampling (see
[`random_mctq()`](https://docs.ropensci.org/mctq/reference/random_mctq.md))
and by manual insertions of special cases. Its purpose is to demonstrate
common cases and data issues that researchers may find in their MCTQ
data, in addition to be a suggested data structure for MCTQ data.

You can see the `micro_mctq` build and data wrangling processes
[here](https://github.com/ropensci/mctq/blob/main/data-raw/micro_mctq.R).

### Variable naming

The naming of the variables took into account the naming scheme used in
MCTQ publications, in addition to the guidelines of the [tidyverse style
guide](https://style.tidyverse.org/).

### Variable classes

The `mctq` package works with a set of object classes specially created
to hold time values. These classes can be found in the
[hms](https://hms.tidyverse.org/reference/hms-package.html) and
[lubridate](https://lubridate.tidyverse.org/reference/lubridate-package.html)
package.

### `Duration` objects

If you prefer to view
[`Duration`](https://lubridate.tidyverse.org/reference/duration.html)
objects as [`hms`](https://hms.tidyverse.org/reference/hms.html)
objects, run
[`pretty_mctq(micro_mctq)`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md).

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

Roenneberg, T., Keller, L. K., Fischer, D., Matera, J. L., Vetter, C., &
Winnebeck, E. C. (2015). Human activity and rest in situ. In A. Sehgal
(Ed.), *Methods in Enzymology* (Vol. 552, pp. 257-283). Academic Press.
[doi:10.1016/bs.mie.2014.11.028](https://doi.org/10.1016/bs.mie.2014.11.028)

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

Other datasets:
[`shift_mctq`](https://docs.ropensci.org/mctq/reference/shift_mctq.md),
[`std_mctq`](https://docs.ropensci.org/mctq/reference/std_mctq.md)
