# Introduction to mctq

This article takes a quick tour of the Munich ChronoType Questionnaire
(MCTQ) main functions from the `mctq` package. Please see the function
documentation and other articles/vignettes for more details.

The same features presented here can also be used with \\\mu\\MCTQ. To
make it easy for newcomers, some MCTQ\\^{Shift}\\ functions and other
special functions are not shown.

We assume that you already have [R](https://www.r-project.org/)
installed and have some familiarity with R and MCTQ data. We also
strongly recommend using
[RStudio](https://posit.co/products/open-source/rstudio/) as your IDE
(Integrated Development Environment).

It’s helpful to have the standard MCTQ questionnaire and the guidelines
for standard MCTQ variable computation open while reading this article.
This will enhance your understanding of the data objects discussed. You
can download the MCTQ full standard version
[here](https://www.thewep.org/documentations/mctq/item/english-mctq-full).

## First things first

Let’s start with the basics. The first thing you must do to use `mctq`
is to have some MCTQ data and `mctq` installed and loaded.

Install `mctq` with:

``` r

install.packages("mctq")
```

Great! We now must load the package to memory to start using it. Do this
with:

``` r

library(mctq)
```

Now we just need to get some MCTQ data. For demonstration purposes,
we’re going to use a small and fictional raw standard MCTQ data provided
by the `mctq` package.

This dataset already has valid values. As for any data analysis, you
must have clean and valid data before using any analysis tool. If you
don’t know how to do that, we strongly recommend checking Hadley Wickham
and Garrett Grolemund free and online book [R for data
Science](https://r4ds.had.co.nz/) and the Coursera course from John
Hopkins University [Data Science: Foundations using
R](https://www.coursera.org/specializations/data-science-foundations-r)
(free for audit students).

Teaching you how to load your data in R is outside the scope of this
article. For that, we recommend checking the
[readr](https://readr.tidyverse.org/) package from
[tidyverse](https://www.tidyverse.org/).

Our fictional MCTQ data will be loaded with the code below. The naming
of the variables follows the same naming pattern used in MCTQ
publications. You can see the meaning of each variable by running
[`?std_mctq`](https://docs.ropensci.org/mctq/reference/std_mctq.md) in
your console (you can also see it in this
[link](https://docs.ropensci.org/mctq/reference/std_mctq.html)).

``` r

library(readr)

data <- readr::read_csv(
  mctq::raw_data("vignette_mctq.csv"),
  col_types = readr::cols(.default = "c")
)
```

## Converting your data

`mctq` makes use of the [lubridate](https://lubridate.tidyverse.org/)
and [hms](https://hms.tidyverse.org/) packages from
[tidyverse](https://www.tidyverse.org/), which provide special objects
to deal with date/time values in R. If your dataset does not conform to
this structure, you first need to convert your data to it.

Due to the circular nature of time, we strongly recommend that you use
appropriate temporal objects while dealing with date/time in R. That can
help you get rid of several computation mistakes while trying to adapt
your data from a base 10 to a system rooted in a base 12 numerical
system.

Teaching you how to parse/convert your data is outside the scope of this
article. Please refer to the
[lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) package documentation to learn more
about them. These two are essential packages to deal with date/time data
in R. We also recommend that you read the [Dates and
times](https://r4ds.had.co.nz/dates-and-times.html) chapter from Wickham
& Grolemund’s book “R for Data Science”.

Here we are interested in two types of time objects: `Duration` objects,
to store time spans, such as sleep latency, and `hms` objects, to store
local time values, such as bedtime.

But first, let’s take a look at the data, shall we? If you’re using
[RStudio](https://posit.co/products/open-source/rstudio/), you can run
the code above and then type `View(data)` in the console to explore it.

``` r

data
#> # A tibble: 5 × 20
#>   id    work  wd    bt_w  sprep_w slat_w se_w  si_w  alarm_w wake_before_w le_w 
#>   <chr> <chr> <chr> <chr> <chr>   <chr>  <chr> <chr> <chr>   <chr>         <chr>
#> 1 1     TRUE  5     22:50 23:20   30     06:55 25    TRUE    FALSE         01:00
#> 2 2     TRUE  2     21:25 21:30   5      05:05 5     TRUE    FALSE         02:00
#> 3 3     TRUE  5     22:30 23:10   50     08:00 15    TRUE    FALSE         02:15
#> 4 4     TRUE  2     00:45 01:10   15     08:55 20    TRUE    FALSE         01:55
#> 5 5     TRUE  7     22:40 22:40   5      08:20 5     TRUE    FALSE         02:00
#> # ℹ 9 more variables: bt_f <chr>, sprep_f <chr>, slat_f <chr>, se_f <chr>,
#> #   si_f <chr>, alarm_f <chr>, reasons_f <chr>, reasons_why_f <chr>, le_f <chr>
```

As you can see, our data came in different formats. For example, the
column `bt_w` (local time of going to bed on workdays) is in
`hours:minutes` format, while `slat_w` (sleep latency on workdays) is a
duration expressed in minutes.

Our fictional data will be parsed/converted with the code below. Please
note that the [lubridate](https://lubridate.tidyverse.org/) and
[hms](https://hms.tidyverse.org/) packages are equipped with easy tools
and great documentation to help you with this task.

``` r

library(dplyr)
library(hms)
library(lubridate)

data <-
  data |>
  dplyr::mutate(
    dplyr::across(c("id", "wd"), as.integer),
    dplyr::across(
      dplyr::matches("^work$|^alarm_|^wake_|^reasons_f$"),
      as.logical
    ),
    dplyr::across(dplyr::matches("^bt_|^sprep_|^se_"), hms::parse_hm),
    dplyr::across(
      dplyr::matches("^slat_|^si_"),
      ~ lubridate::dminutes(as.numeric(.x))
    ),
    dplyr::across(
      dplyr::matches("^le_"),
      ~ lubridate::as.duration(hms::parse_hm(.x))
    )
  )
```

Our data is now all set to start. Let’s take a look at it.

``` r

data
#> # A tibble: 5 × 20
#>      id work     wd bt_w   sprep_w slat_w              se_w  si_w               
#>   <int> <lgl> <int> <time> <time>  <Duration>          <tim> <Duration>         
#> 1     1 TRUE      5 22:50  23:20   1800s (~30 minutes) 06:55 1500s (~25 minutes)
#> 2     2 TRUE      2 21:25  21:30   300s (~5 minutes)   05:05 300s (~5 minutes)  
#> 3     3 TRUE      5 22:30  23:10   3000s (~50 minutes) 08:00 900s (~15 minutes) 
#> 4     4 TRUE      2 00:45  01:10   900s (~15 minutes)  08:55 1200s (~20 minutes)
#> 5     5 TRUE      7 22:40  22:40   300s (~5 minutes)   08:20 300s (~5 minutes)  
#> # ℹ 12 more variables: alarm_w <lgl>, wake_before_w <lgl>, le_w <Duration>,
#> #   bt_f <time>, sprep_f <time>, slat_f <Duration>, se_f <time>,
#> #   si_f <Duration>, alarm_f <lgl>, reasons_f <lgl>, reasons_why_f <chr>,
#> #   le_f <Duration>
```

## Workdays and work-free days variables

`mctq` provides a complete and consistent toolkit to process Munich
ChronoType Questionnaire (MCTQ) data. To start this process, we must
first compute some MCTQ variables related to each section of the
questionnaire.

We’re going to use direct assigning while computing the MCTQ variables,
just because is more straightforward for the examples. But, we recommend
assigning variables to your dataset by using the
[`mutate()`](https://dplyr.tidyverse.org/reference/mutate.html)
function, included in the [dplyr](https://dplyr.tidyverse.org/) package.

### `fd()`: Number of work-free days per week

[`fd()`](https://docs.ropensci.org/mctq/reference/fd.md) is a simple
function that allows you to compute the difference between the number of
days in a week (7) and the number of workdays per week (`wd`). It takes
only `wd` as argument.

The output must be the total of free days a respondent has in a week.

``` r

data$fd <- fd(data$wd)

# Comparing the result
data |> dplyr::select(wd, fd)
#> # A tibble: 5 × 2
#>      wd    fd
#>   <int> <int>
#> 1     5     2
#> 2     2     5
#> 3     5     2
#> 4     2     5
#> 5     7     0
```

### `so()`: Local time of sleep onset

[`so()`](https://docs.ropensci.org/mctq/reference/so.md) allows you to
compute the local time of sleep onset for workdays (`so_w`) and
work-free days (`so_f`). It takes two arguments: `sprep` (local time of
preparing to sleep) and `slat` (sleep latency or time to fall asleep
after preparing to sleep).

The output must be the sum of `sprep` and `slat` in a circular time
frame of 24 hours.

What is a circular time frame of 24 hours? Run `?cycle_time` in your
console or click in this
[link](https://docs.ropensci.org/mctq/reference/cycle_time.html) for a
detail explanation.

``` r

data$so_w <- so(data$sprep_w, data$slat_w)
data$so_f <- so(data$sprep_f, data$slat_f)

# Comparing the result
data |> dplyr::select(sprep_w, slat_w, so_w, sprep_f, slat_f, so_f)
#> # A tibble: 5 × 6
#>   sprep_w slat_w              so_w   sprep_f slat_f              so_f  
#>   <time>  <Duration>          <time> <time>  <Duration>          <time>
#> 1 23:20   1800s (~30 minutes) 23:50  00:15   300s (~5 minutes)   00:20 
#> 2 21:30   300s (~5 minutes)   21:35  23:20   600s (~10 minutes)  23:30 
#> 3 23:10   3000s (~50 minutes) 00:00  00:15   1500s (~25 minutes) 00:40 
#> 4 01:10   900s (~15 minutes)  01:25  00:55   1500s (~25 minutes) 01:20 
#> 5 22:40   300s (~5 minutes)   22:45  00:30   300s (~5 minutes)   00:35
```

### `gu()`: Local time of getting out of bed

[`gu()`](https://docs.ropensci.org/mctq/reference/gu.md) allows you to
compute the local time of getting out of bed for workdays (`gu_w`) and
work-free days (`gu_f`). It takes two arguments: `se` (local time of
sleep end) and `si` (sleep inertia).

The output must be the sum of `se` and `si` in a circular time frame of
24 hours.

Please note that, despite the name, `si` represents the time that the
respondent takes to get up after sleep end. We decided to maintain the
original names and abbreviations proposed by the MCTQ authors.

``` r

data$gu_w <- gu(data$se_w, data$si_w)
data$gu_f <- gu(data$se_f, data$si_f)

# Comparing the result
data |> dplyr::select(se_w, si_w, gu_w, se_f, si_f, gu_f)
#> # A tibble: 5 × 6
#>   se_w   si_w                gu_w   se_f   si_f                gu_f  
#>   <time> <Duration>          <time> <time> <Duration>          <time>
#> 1 06:55  1500s (~25 minutes) 07:20  10:10  1500s (~25 minutes) 10:35 
#> 2 05:05  300s (~5 minutes)   05:10  07:20  1200s (~20 minutes) 07:40 
#> 3 08:00  900s (~15 minutes)  08:15  10:05  900s (~15 minutes)  10:20 
#> 4 08:55  1200s (~20 minutes) 09:15  07:30  1200s (~20 minutes) 07:50 
#> 5 08:20  300s (~5 minutes)   08:25  07:55  1500s (~25 minutes) 08:20
```

### `sdu()`: Sleep duration

[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) allows you to
compute the sleep duration for workdays (`sd_w`) and work-free days
(`sd_f`). It takes two arguments: `so` (local time of sleep onset) and
`se` (local time of sleep end).

The output must be the difference between `se` and `so` in a circular
time frame of 24 hours.

Please note that, although we tried to preserve the original authors’
naming pattern for the MCTQ functions, the name `sd` provokes a
dangerous name collision with the widely used
[stats::sd](https://rdrr.io/r/stats/sd.html) (standard deviation)
function. That’s why we named it as `sdu`.
[`sdu()`](https://docs.ropensci.org/mctq/reference/sdu.md) and
[`msl()`](https://docs.ropensci.org/mctq/reference/msl.md) are the only
exceptions, all the other `mctq` functions maintain a strong naming
resemblance with the original authors’ naming pattern.

``` r

data$sd_w <- sdu(data$so_w, data$se_w)
data$sd_f <- sdu(data$so_f, data$se_f)

# Comparing the result
data |> dplyr::select(so_w, se_w, sd_w, so_f, se_f, sd_f)
#> # A tibble: 5 × 6
#>   so_w   se_w   sd_w                 so_f   se_f   sd_f                
#>   <time> <time> <Duration>           <time> <time> <Duration>          
#> 1 23:50  06:55  25500s (~7.08 hours) 00:20  10:10  35400s (~9.83 hours)
#> 2 21:35  05:05  27000s (~7.5 hours)  23:30  07:20  28200s (~7.83 hours)
#> 3 00:00  08:00  28800s (~8 hours)    00:40  10:05  33900s (~9.42 hours)
#> 4 01:25  08:55  27000s (~7.5 hours)  01:20  07:30  22200s (~6.17 hours)
#> 5 22:45  08:20  34500s (~9.58 hours) 00:35  07:55  26400s (~7.33 hours)
```

### `tbt()`: Total time in bed

[`tbt()`](https://docs.ropensci.org/mctq/reference/tbt.md) allows you to
compute total time in bed for workdays (`tbt_w`) and work-free days
(`tbt_f`). It takes two arguments: `bt` (local time of going to bed) and
`gu` (local time of getting out of bed).

The output must be the difference between `gu` and `bt` in a circular
time frame of 24 hours.

``` r

data$tbt_w <- tbt(data$bt_w, data$gu_w)
data$tbt_f <- tbt(data$bt_f, data$gu_f)

# Comparing the result
data |> dplyr::select(bt_w, gu_w, tbt_w, bt_f, gu_f, tbt_f)
#> # A tibble: 5 × 6
#>   bt_w   gu_w   tbt_w                bt_f   gu_f   tbt_f                
#>   <time> <time> <Duration>           <time> <time> <Duration>           
#> 1 22:50  07:20  30600s (~8.5 hours)  23:35  10:35  39600s (~11 hours)   
#> 2 21:25  05:10  27900s (~7.75 hours) 21:55  07:40  35100s (~9.75 hours) 
#> 3 22:30  08:15  35100s (~9.75 hours) 22:40  10:20  42000s (~11.67 hours)
#> 4 00:45  09:15  30600s (~8.5 hours)  23:15  07:50  30900s (~8.58 hours) 
#> 5 22:40  08:25  35100s (~9.75 hours) 00:30  08:20  28200s (~7.83 hours)
```

### `msl()`: Local time of mid-sleep

[`msl()`](https://docs.ropensci.org/mctq/reference/msl.md) allows you to
compute the local time of mid-sleep for workdays (`msw`) and work-free
days (`msf`). It takes two arguments: `so` (local time of sleep onset)
and `sd` (sleep duration).

The output must be the sum of `so` with the half of `sd` duration in a
circular time frame of 24 hours.

``` r

data$msw <- msl(data$so_w, data$sd_w)
data$msf <- msl(data$so_f, data$sd_f)

# Comparing the result
data |> dplyr::select(so_w, sd_w, msw, so_f, sd_f, msf)
#> # A tibble: 5 × 6
#>   so_w   sd_w                 msw      so_f   sd_f                 msf     
#>   <time> <Duration>           <time>   <time> <Duration>           <time>  
#> 1 23:50  25500s (~7.08 hours) 03:22:30 00:20  35400s (~9.83 hours) 05:15:00
#> 2 21:35  27000s (~7.5 hours)  01:20:00 23:30  28200s (~7.83 hours) 03:25:00
#> 3 00:00  28800s (~8 hours)    04:00:00 00:40  33900s (~9.42 hours) 05:22:30
#> 4 01:25  27000s (~7.5 hours)  05:10:00 01:20  22200s (~6.17 hours) 04:25:00
#> 5 22:45  34500s (~9.58 hours) 03:32:30 00:35  26400s (~7.33 hours) 04:15:00
```

## Combining workdays and work-free days variables

We now have computed all MCTQ variables for each section of the
questionnaire. Let’s move to some variables that summarize our findings
considering workdays and work-free days.

### `sd_week()`: Average weekly sleep duration

[`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md)
allows you to compute the average weekly sleep duration. It takes three
arguments: `sd_w` (sleep duration on workdays), `sd_f` (sleep duration
on work-free days), and `wd` (number of workdays per week).

The output must be the weighted mean of `sd_w` and `sd_f`, with `wd` and
`fd(wd)` as weights, in a circular time frame of 24 hours.

``` r

data$sd_week <- sd_week(data$sd_w, data$sd_f, data$wd)

# Comparing the result
data <-
  data |>
  dplyr::mutate(sd_week_rounded = mctq:::round_time(sd_week))

data |> dplyr::select(wd, sd_w, fd, sd_f, sd_week_rounded)
#> # A tibble: 5 × 5
#>      wd sd_w                    fd sd_f                 sd_week_rounded     
#>   <int> <Duration>           <int> <Duration>           <Duration>          
#> 1     5 25500s (~7.08 hours)     2 35400s (~9.83 hours) 28329s (~7.87 hours)
#> 2     2 27000s (~7.5 hours)      5 28200s (~7.83 hours) 27857s (~7.74 hours)
#> 3     5 28800s (~8 hours)        2 33900s (~9.42 hours) 30257s (~8.4 hours) 
#> 4     2 27000s (~7.5 hours)      5 22200s (~6.17 hours) 23571s (~6.55 hours)
#> 5     7 34500s (~9.58 hours)     0 26400s (~7.33 hours) 34500s (~9.58 hours)
```

### `sloss_week()`: Weekly sleep loss

[`sloss_week()`](https://docs.ropensci.org/mctq/reference/sloss_week.md)
allows you to compute the weekly sleep loss. It takes three arguments:
`sd_w` (sleep duration on workdays), `sd_f` (sleep duration on work-free
days), and `wd` (number of workdays per week).

If `sd_week`(average weekly sleep duration) is greater than `sd_w`, the
output must be the difference between `sd_week` and `sd_w` times `wd`.
Else, it must return the difference between `sd_week` and `sd_f` times
`fd(wd`) (number of free days per week). See
[`?sloss_week`](https://docs.ropensci.org/mctq/reference/sloss_week.md)
to learn more.

``` r

data$sloss_week <- sloss_week(data$sd_w, data$sd_f, data$wd)

# Comparing the result
data <-
  data |>
  dplyr::mutate(
    sloss_week_rounded = mctq:::round_time(sloss_week)
  )

data |> dplyr::select(wd, sd_w, fd, sd_f, sloss_week_rounded)
#> # A tibble: 5 × 5
#>      wd sd_w                    fd sd_f                 sloss_week_rounded    
#>   <int> <Duration>           <int> <Duration>           <Duration>            
#> 1     5 25500s (~7.08 hours)     2 35400s (~9.83 hours) 14143s (~3.93 hours)  
#> 2     2 27000s (~7.5 hours)      5 28200s (~7.83 hours) 1714s (~28.57 minutes)
#> 3     5 28800s (~8 hours)        2 33900s (~9.42 hours) 7286s (~2.02 hours)   
#> 4     2 27000s (~7.5 hours)      5 22200s (~6.17 hours) 6857s (~1.9 hours)    
#> 5     7 34500s (~9.58 hours)     0 26400s (~7.33 hours) 0s
```

### `le_week()`: Average weekly light exposure

[`le_week()`](https://docs.ropensci.org/mctq/reference/le_week.md)
allows you to compute the average weekly light exposure. It takes three
arguments: `le_w` (light exposure on workdays), `le_f` (light exposure
on work-free days), and `wd` (number of workdays per week).

The output must be the weighted mean of `le_w` and `le_f`, with `wd` and
`fd(wd)` as weights, in a circular time frame of 24 hours.

Please note that light exposure is measured only with the full version
of the standard MCTQ.

``` r

data$le_week <- le_week(data$le_w, data$le_f, data$wd)

# Comparing the result
data <-
  data |>
  dplyr::mutate(le_week_rounded = mctq:::round_time(le_week))

data |> dplyr::select(wd, le_w, fd, le_f, le_week_rounded)
#> # A tibble: 5 × 5
#>      wd le_w                   fd le_f                 le_week_rounded     
#>   <int> <Duration>          <int> <Duration>           <Duration>          
#> 1     5 3600s (~1 hours)        2 12000s (~3.33 hours) 6000s (~1.67 hours) 
#> 2     2 7200s (~2 hours)        5 12900s (~3.58 hours) 11271s (~3.13 hours)
#> 3     5 8100s (~2.25 hours)     2 9900s (~2.75 hours)  8614s (~2.39 hours) 
#> 4     2 6900s (~1.92 hours)     5 9300s (~2.58 hours)  8614s (~2.39 hours) 
#> 5     7 7200s (~2 hours)        0 7800s (~2.17 hours)  7200s (~2 hours)
```

### `msf_sc()`: Chronotype or sleep-corrected local time of mid-sleep on work-free days

[`msf_sc()`](https://docs.ropensci.org/mctq/reference/msf_sc.md) allows
you to compute the chronotype, or corrected local time of mid-sleep on
work-free days. It takes five arguments: `msf` (local time of mid-sleep
on work-free days), `sd_w` (sleep duration on workdays), `sd_f` (sleep
duration on work-free days), `sd_week`(average weekly sleep duration),
and `alarm_f` (a `logical` object indicating if the respondent uses an
alarm clock to wake up on work-free days).

If `sd_f` is less or equal than `sd_w`, the output must be `msf`. Else,
it must return `msf` minus the difference between `sd_f` and `sd_week`
divided by 2. `msf_sc` can only be computed if `alarm_f` is equal to
`FALSE` (the function will return `NA` when `alarm_f == TRUE`).

`msf_sc` applies a correction to `msf`, removing an estimation of the
effect from accumulated sleep debt on workdays that usually is
compensated on work-free days. See
[`?msf_sc`](https://docs.ropensci.org/mctq/reference/msf_sc.md) to learn
more.

``` r

data$msf_sc <- msf_sc(
  data$msf, data$sd_w, data$sd_f, data$sd_week, data$alarm_f
)

# Comparing the result
data <-
  data |>
  dplyr::mutate(msf_sc_rounded = mctq:::round_time(msf_sc))

data |> dplyr::select(msf, msf_sc_rounded)
#> # A tibble: 5 × 2
#>   msf      msf_sc_rounded
#>   <time>   <time>        
#> 1 05:15:00 04:16:04      
#> 2 03:25:00 03:22:09      
#> 3 05:22:30 04:52:09      
#> 4 04:25:00 04:25:00      
#> 5 04:15:00 04:15:00
```

### `sjl_rel()`: Relative social jetlag

[`sjl_rel()`](https://docs.ropensci.org/mctq/reference/sjl.md) allows
you to compute the relative social jetlag. It takes at least two
arguments: `msw` (local time of mid-sleep on workdays) and `msf` (local
time of mid-sleep on work-free days).

The output must be the difference between `msf` and `msw` in a circular
time frame of 24 hours.

In case you don’t know, social jet lag is a concept developed by
Wittmann et al. ([2006](https://doi.org/10.1080/07420520500545979)) that
represents the discrepancy between social and biological time.

The difference described above may seem trivial or easy to compute, but
it’s not. See the
[`vignette("sjl-computation", package = "mctq")`](https://docs.ropensci.org/mctq/articles/sjl-computation.md)
to learn more.

``` r

data$sjl_rel <- sjl_rel(data$msw, data$msf)

# Comparing the result
data |> dplyr::select(msw, msf, sjl_rel)
#> # A tibble: 5 × 3
#>   msw      msf      sjl_rel              
#>   <time>   <time>   <Duration>           
#> 1 03:22:30 05:15:00 6750s (~1.88 hours)  
#> 2 01:20:00 03:25:00 7500s (~2.08 hours)  
#> 3 04:00:00 05:22:30 4950s (~1.38 hours)  
#> 4 05:10:00 04:25:00 -2700s (~-45 minutes)
#> 5 03:32:30 04:15:00 2550s (~42.5 minutes)
```

### `sjl()`: Absolute social jetlag

[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md) allows you to
compute the absolute social jetlag. This function works the same way as
`sjl_rel`, but it returns an absolute value. In fact,
[`sjl_rel()`](https://docs.ropensci.org/mctq/reference/sjl.md) is just a
wrapper function to
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md), but with the
`abs` argument set as `FALSE`.

If you already have `sjl_rel` computed, you don’t really need to compute
it twice, you can just use `abs(sjl_rel)`. That’s what we’re going to do
with our data.

``` r

data$sjl <- abs(data$sjl_rel)

# Comparing the result
data |> dplyr::select(sjl_rel, sjl)
#> # A tibble: 5 × 2
#>   sjl_rel               sjl                  
#>   <Duration>            <Duration>           
#> 1 6750s (~1.88 hours)   6750s (~1.88 hours)  
#> 2 7500s (~2.08 hours)   7500s (~2.08 hours)  
#> 3 4950s (~1.38 hours)   4950s (~1.38 hours)  
#> 4 -2700s (~-45 minutes) 2700s (~45 minutes)  
#> 5 2550s (~42.5 minutes) 2550s (~42.5 minutes)
```

## Success!

We have now processed all the MCTQ standard variables proposed by the
MCTQ authors.

Before we look at the final data, let’s first reorder the columns to a
nice logical order and remove some `*_rounded` variables that we created
just for show.

``` r

data <-
  data |>
  dplyr::relocate(
    id, work, wd, fd,

    bt_w, sprep_w, slat_w, so_w, se_w, si_w, gu_w, alarm_w, wake_before_w,
    sd_w, tbt_w, le_w, msw,

    bt_f, sprep_f, slat_f, so_f, se_f, si_f, gu_f, alarm_f, reasons_f,
    reasons_why_f, sd_f, tbt_f, le_f, msf,

    sd_week, sloss_week, le_week, msf_sc, sjl_rel, sjl
  ) |>
  dplyr::select(-dplyr::ends_with("_rounded"))
```

And our final dataset is …

``` r

data
#> # A tibble: 5 × 37
#>      id work     wd    fd bt_w   sprep_w slat_w              so_w   se_w  
#>   <int> <lgl> <int> <int> <time> <time>  <Duration>          <time> <time>
#> 1     1 TRUE      5     2 22:50  23:20   1800s (~30 minutes) 23:50  06:55 
#> 2     2 TRUE      2     5 21:25  21:30   300s (~5 minutes)   21:35  05:05 
#> 3     3 TRUE      5     2 22:30  23:10   3000s (~50 minutes) 00:00  08:00 
#> 4     4 TRUE      2     5 00:45  01:10   900s (~15 minutes)  01:25  08:55 
#> 5     5 TRUE      7     0 22:40  22:40   300s (~5 minutes)   22:45  08:20 
#> # ℹ 28 more variables: si_w <Duration>, gu_w <time>, alarm_w <lgl>,
#> #   wake_before_w <lgl>, sd_w <Duration>, tbt_w <Duration>, le_w <Duration>,
#> #   msw <time>, bt_f <time>, sprep_f <time>, slat_f <Duration>, so_f <time>,
#> #   se_f <time>, si_f <Duration>, gu_f <time>, alarm_f <lgl>, reasons_f <lgl>,
#> #   reasons_why_f <chr>, sd_f <Duration>, tbt_f <Duration>, le_f <Duration>,
#> #   msf <time>, sd_week <Duration>, sloss_week <Duration>, le_week <Duration>,
#> #   msf_sc <time>, sjl_rel <Duration>, sjl <Duration>
```

If you’re using
[RStudio](https://posit.co/products/open-source/rstudio/), you can run
all the code showed above and then type `View(data)` in the console to
explore the final result.

If you don’t feel comfortable with the way `Duration` objects are
printed, `mctq` provides a utility function to help you. Just use
[`pretty_mctq()`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md)
to get a better view.

``` r

data |> pretty_mctq(round = FALSE)
#> # A tibble: 5 × 37
#>      id work     wd    fd bt_w   sprep_w slat_w so_w  se_w  si_w   gu_w  alarm_w
#>   <int> <lgl> <int> <int> <time> <time>  <time> <tim> <tim> <time> <tim> <lgl>  
#> 1     1 TRUE      5     2 22:50  23:20   30'00" 23:50 06:55 25'00" 07:20 TRUE   
#> 2     2 TRUE      2     5 21:25  21:30   05'00" 21:35 05:05 05'00" 05:10 TRUE   
#> 3     3 TRUE      5     2 22:30  23:10   50'00" 00:00 08:00 15'00" 08:15 TRUE   
#> 4     4 TRUE      2     5 00:45  01:10   15'00" 01:25 08:55 20'00" 09:15 TRUE   
#> 5     5 TRUE      7     0 22:40  22:40   05'00" 22:45 08:20 05'00" 08:25 TRUE   
#> # ℹ 25 more variables: wake_before_w <lgl>, sd_w <time>, tbt_w <time>,
#> #   le_w <time>, msw <time>, bt_f <time>, sprep_f <time>, slat_f <time>,
#> #   so_f <time>, se_f <time>, si_f <time>, gu_f <time>, alarm_f <lgl>,
#> #   reasons_f <lgl>, reasons_why_f <chr>, sd_f <time>, tbt_f <time>,
#> #   le_f <time>, msf <time>, sd_week <time>, sloss_week <time>, le_week <time>,
#> #   msf_sc <time>, sjl_rel <time>, sjl <time>
```

## Utilities

Before we end, it’s important to note that `mctq` also provides some
utility tools to help with your MCTQ data. Here are some of them.

- [`pretty_mctq()`](https://docs.ropensci.org/mctq/reference/pretty_mctq.md):
  Make a MCTQ dataset more presentable.
- [`random_mctq()`](https://docs.ropensci.org/mctq/reference/random_mctq.md):
  Build a random MCTQ case.

`mctq` also provides fictional datasets of the standard, micro, and
shift versions for testing and learning purposes.

- `std_mctq`: A fictional standard MCTQ dataset
  ([`?std_mctq`](https://docs.ropensci.org/mctq/reference/std_mctq.md)).
- `micro_mctq`: A fictional \\\mu\\MCTQ dataset
  ([`?micro_mctq`](https://docs.ropensci.org/mctq/reference/micro_mctq.md)).
- `shift_mctq`: A fictional MCTQ\\^{Shift}\\ dataset
  ([`?shift_mctq`](https://docs.ropensci.org/mctq/reference/shift_mctq.md)).

We encouraged you to read the documentation of the features above. You
may find it worth your time.
