# Dealing with missing sections

This article shows a possible workaround to a common problem encountered
when dealing with a **standard** Munich ChronoType Questionnaire (MCTQ)
and **\\\mu\\MCTQ** data.

It’s helpful to have the standard MCTQ questionnaire and the guidelines
for standard MCTQ variable computation open while reading this article.
This will enhance your understanding of the data objects discussed. You
can download the MCTQ full standard version
[here](https://www.thewep.org/documentations/mctq/item/english-mctq-full)
and the guidelines for standard MCTQ variables
[here](https://www.thewep.org/documentations/mctq/item/mctq-variables).

## Working around missing sections

Although the standard and micro versions of the MCTQ asks for
respondents to complete the workdays and work-free days sections, even
when they do not have a regular work schedule (`wd = 0`) or have a 7
day/week work schedule (`wd = 7`), some of them may still end skipping
one of this parts of the questionnaire. In those cases,
[`sd_week()`](https://docs.ropensci.org/mctq/reference/sd_week.md),
[`sloss_week()`](https://docs.ropensci.org/mctq/reference/sloss_week.md),
[`le_week()`](https://docs.ropensci.org/mctq/reference/le_week.md),
[`msf_sc()`](https://docs.ropensci.org/mctq/reference/msf_sc.md),
[`sjl_rel()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_sc_rel()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
and [`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md)
will produce `NA` (Not Available) as output. That’s because those
computations combine workdays and work-free days variables.

For those special standard and micro MCTQ cases, where one section is
missing, a `NA` value is the correct output for the functions mentioned
above when `wd` (number of workdays per week) are `wd > 0 & wd < 7`, but
it may not be when `wd == 0` or `wd == 7`. While some researchers may
just invalidate these latter cases, we propose a different approach.

To illustrate this approach, consider the following.

If a respondent **does not have a regular work schedule** (`wd == 0`),
**only answered the work-free days section**, and **does not use an
alarm clock on their free days** (i.e., `alarm_f == FALSE`), it would be
fair to assume that there’s no sleep correction (`sc`) to be made,
therefore, their chronotype (`msf_sc`) must be equal to their midsleep
on work-free days (`msf`).

Following this same line of thought, we can also say that:

- `sd_week` (average weekly sleep duration) must be equal to `sd_f`
  (sleep duration on work-free days) since the respondent does not have
  workdays.
- `sloss_week` (weekly sleep loss) must be equal to `0s` since there’s
  no sleep debt.
- `le_week` (average weekly light exposure) must be equal to `le_f`
  (light exposure on work-free days) since there are no workdays.
- `sjl_rel` (relative social jet lag), `sjl` (absolute social jet lag),
  `sjl_sc_rel` (Jankowski’s relative sleep-corrected social jetlag), and
  `sjl_sc` (Jankowski’s sleep-corrected social jetlag) must be equal to
  `0s` since there’s no discrepancy between social and biological time.

Note that the [chronotype
computation](https://www.thewep.org/documentations/mctq/item/mctq-variables)
follows a similar line of thought.

The opposite scenario, i.e., when the respondent **works 7 days per
week** (`wd == 7`) and **only answered the workdays section**, can also
have different outputs.
[`sloss_week()`](https://docs.ropensci.org/mctq/reference/sloss_week.md),
[`msf_sc()`](https://docs.ropensci.org/mctq/reference/msf_sc.md),
[`sjl_rel()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl()`](https://docs.ropensci.org/mctq/reference/sjl.md),
[`sjl_sc_rel()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md),
and [`sjl_sc()`](https://docs.ropensci.org/mctq/reference/sjl_sc.md)
should still produce a `NA` as output since there’s no way to know the
real behavior of the respondent’s sleep-wake cycle. But, according to
this reasoning, `sd_week` and `le_week` can have different outputs.

- `sd_week` (average weekly sleep duration) must be equal to `sd_w`
  (sleep duration on workdays) since the respondent does not have
  work-free days.
- `le_week` (average weekly light exposure) must be equal to `le_w`
  (light exposure on work-free days) since the respondent does not have
  work-free days.

If you agree with this line of thought, we recommend creating dummy
variables to identify those two situations and then change the values as
mentioned. You can see this procedure in action with the [data wrangling
algorithms](https://github.com/ropensci/mctq/blob/main/data-raw/std_mctq.R#L958)
made to produce the fictional `std_mctq` dataset, provided by the `mctq`
package.

Please note that this workaround is not mentioned or endorsed by the
MCTQ authors. If you use it, you must mention this reasoning in your
methods section.
