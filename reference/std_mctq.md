# A fictional standard MCTQ dataset

**\[maturing\]**

A fictional dataset, **for testing and learning purposes**, composed of
basic/measurable and computed variables of the Munich ChronoType
Questionnaire (MCTQ) standard version.

This data was created following the guidelines in Roenneberg,
Wirz-Justice, & Merrow (2003), Roenneberg, Allebrandt, Merrow, & Vetter
(2012), Jankowski (2017), and The Worldwide Experimental Platform
(n.d.). See the References and Details sections to learn more.

## Usage

``` r
std_mctq
```

## Format

A [`tibble`](https://dplyr.tidyverse.org/reference/reexports.html) with
39 columns and 50 rows:

- id:

  A unique [`integer`](https://rdrr.io/r/base/integer.html) value to
  identify each respondent in the dataset.  
    
  Type: Control.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- work:

  A [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent has a regular work schedule.  
    
  Statement (`EN`): "I have a regular work schedule (this includes
  being, for example, a housewife or househusband): Yes ( \_\_\_ ) No (
  \_\_\_ )".  
    
  Type: Basic.  
    
  R class: [`logical`](https://rdrr.io/r/base/logical.html).

- wd:

  Number of **workdays** per week.  
    
  Statement (`EN`): "I have a regular work schedule and work \_\_\_ days
  per week".  
    
  Type: Basic.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- fd:

  Number of **work-free days** per week.  
    
  Type: Computed.  
    
  R class: [`integer`](https://rdrr.io/r/base/integer.html).

- bt_w:

  Local time of going to bed on **workdays**.  
    
  Statement (`EN`): "I go to bed at \_\_\_ o'clock'".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sprep_w:

  Local time of preparing to sleep on **workdays**.  
    
  Statement (`EN`): "I actually get ready to fall asleep at \_\_\_
  o'clock".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- slat_w:

  Sleep latency or time to fall asleep after preparing to sleep on
  **workdays**.  
    
  Statement (`EN`): "I need \_\_\_ minutes to fall asleep".  
    
  Type: Basic.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- so_w:

  Local time of sleep onset on **workdays**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- se_w:

  Local time of sleep end on **workdays**.  
    
  Statement (`EN`): "I wake up at \_\_\_ o'clock".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- si_w:

  "Sleep inertia" on **workdays**.  
    
  Despite the name, this variable represents the time the respondent
  takes to get up after sleep end.  
    
  Statement (`EN`): "After \_\_\_ minutes, I get up".  
    
  Type: Basic.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- gu_w:

  Local time of getting out of bed on **workdays**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- alarm_w:

  A [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent uses an alarm clock to wake up on **workdays**.  
    
  Statement (`EN`): "I use an alarm clock on workdays: Yes ( \_\_\_ ) No
  ( \_\_\_ )".  
    
  Type: Basic.  
    
  R class: [`logical`](https://rdrr.io/r/base/logical.html).

- wake_before_w:

  A [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent regularly wakes up **before** the alarm rings on
  **workdays**.  
    
  Statement (`EN`): "If "Yes": I regularly wake up BEFORE the alarm
  rings: Yes ( \_\_\_ ) No ( \_\_\_ )".  
    
  Type: Basic.  
    
  R class: [`logical`](https://rdrr.io/r/base/logical.html).

- sd_w:

  Sleep duration on **workdays**.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- tbt_w:

  Total time in bed on **workdays**.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- le_w:

  Light exposure on **workdays**.  
    
  Statement (`EN`): "On average, I spend the following amount of time
  outdoors in daylight (without a roof above my head)".  
    
  Type: Extra.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- msw:

  Local time of mid-sleep on **workdays**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- bt_f:

  Local time of going to bed on **work-free days**.  
    
  Statement (`EN`): "I go to bed at \_\_\_ o'clock'".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- sprep_f:

  Local time of preparing to sleep on **work-free days**.  
    
  Statement (`EN`): "I actually get ready to fall asleep at \_\_\_
  o'clock".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- slat_f:

  Sleep latency or time to fall asleep after preparing to sleep on
  **work-free days**.  
    
  Statement (`EN`): "I need \_\_\_ minutes to fall asleep".  
    
  Type: Basic.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- so_f:

  Local time of sleep onset on **work-free days**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- se_f:

  Local time of sleep end on **work-free days**.  
    
  Statement (`EN`): "I wake up at \_\_\_ o'clock".  
    
  Type: Basic.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- si_f:

  "Sleep inertia" on **work-free days**.  
    
  Despite the name, this variable represents the time the respondent
  takes to get up after sleep end.  
    
  Statement (`EN`): "After \_\_\_ minutes, I get up".  
    
  Type: Basic.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- gu_f:

  Local time of getting out of bed on **work-free days**.  
    
  Type: Computed.  
    
  R class: [`hms`](https://hms.tidyverse.org/reference/hms.html).

- alarm_f:

  A [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent uses an alarm clock to wake up on **work-free days**.  
    
  Statement (`EN`): "My wake-up time is due to the use of an alarm
  clock: Yes ( \_\_\_ ) No ( \_\_\_ )".  
    
  Type: Basic.  
    
  R class: [`logical`](https://rdrr.io/r/base/logical.html).

- reasons_f:

  A [`logical`](https://rdrr.io/r/base/logical.html) value indicating if
  the respondent has any particular reasons for why they **cannot**
  freely choose their sleep times on **work-free days**.  
    
  Statement (`EN`): "There are particular reasons why I **cannot**
  freely choose my sleep times on free days: Yes ( \_\_\_ ) No ( \_\_\_
  )".  
    
  Type: Basic.  
    
  R class: [`logical`](https://rdrr.io/r/base/logical.html).

- reasons_why_f:

  Particular reasons for why the respondent cannot freely choose their
  sleep times on **work-free days**.  
    
  Statement (`EN`): "If "Yes": Child(ren)/pet(s) ( \_\_\_ ) Hobbies (
  \_\_\_ ) Others ( \_\_\_ ), for example: \_\_\_".  
    
  Type: Basic.  
    
  R class: `character`.

- sd_f:

  Sleep duration on **work-free days**.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- tbt_f:

  Total time in bed on **work-free days**.  
    
  Type: Computed.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- le_f:

  Light exposure on **work-free days**.  
    
  Statement (`EN`): "On average, I spend the following amount of time
  outdoors in daylight (without a roof above my head)".  
    
  Type: Extra.  
    
  R class:
  [`Duration`](https://lubridate.tidyverse.org/reference/duration.html).

- msf:

  Local time of mid-sleep on **work-free days**.  
    
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

- le_week:

  Average weekly light exposure.  
    
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

`std_mctq` is a tidied, validated, and transformed version of
`raw_data("std_mctq.csv")`.

### Guidelines

To learn more about the Munich ChronoType Questionnaire (MCTQ), see
Roenneberg, Wirz-Justice, & Merrow (2003), Roenneberg, Allebrandt,
Merrow, & Vetter (2012), Roenneberg et al. (2015), and Roenneberg, Pilz,
Zerbini, & Winnebeck (2019).

To know about different MCTQ versions, see Juda, Vetter, & Roenneberg
(2013) and Ghotbi et al. (2020).

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

You can see the `std_mctq` build and data wrangling processes
[here](https://github.com/ropensci/mctq/blob/main/data-raw/std_mctq.R).

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
[`pretty_mctq(std_mctq)`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md).

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
[`micro_mctq`](https://docs.ropensci.org/mctq/reference/micro_mctq.md),
[`shift_mctq`](https://docs.ropensci.org/mctq/reference/shift_mctq.md)
