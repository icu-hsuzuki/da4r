# Transforming {#transforming}

> The `dplyr` is a package to transform data. It can combine data as well. We will treat the second feature late in Chapter \@ref(tidyr). The package `dplyr` is a part of the `tidyverse` packages, and you do not need to install it separately.


```r
library(tidyverse)
#> ── Attaching core tidyverse packages ──── tidyverse 2.0.0 ──
#> ✔ dplyr     1.1.3     ✔ readr     2.1.4
#> ✔ forcats   1.0.0     ✔ stringr   1.5.0
#> ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
#> ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
#> ✔ purrr     1.0.2     
#> ── Conflicts ────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
#> ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


## `dplyr` [Overview](https://dplyr.tidyverse.org)

dplyr is a grammar of data manipulation, providing a consistent set of verbs that help you solve the most common data manipulation challenges:

* `select()` picks variables based on their names.
* `filter()` picks cases based on their values.
* `mutate()` adds new variables that are functions of existing variables
* `summarise()` reduces multiple values down to a single summary.
* `arrange()` changes the ordering of the rows.
* `group_by()` takes an existing tbl and converts it into a grouped tbl.

You can learn more about them in vignette("dplyr"). As well as these single-table verbs, dplyr also provides a variety of two-table verbs, which you can learn about in vignette("two-table").

If you are new to dplyr, the best place to start is [the data transformation chapter in R for data science](http://r4ds.had.co.nz/transform.html).


## [`select`](https://dplyr.tidyverse.org/reference/select.html): Subset columns using their names and types

Helper Function	| Use	| Example
---|-------|--------
-	| Columns except	| select(babynames, -prop)
:	| Columns between (inclusive)	| select(babynames, year:n)
contains() |	Columns that contains a string |	select(babynames, contains("n"))
ends_with()	| Columns that ends with a string	| select(babynames, ends_with("n"))
matches()	| Columns that matches a regex |	select(babynames, matches("n"))
num_range()	| Columns with a numerical suffix in the range | Not applicable with babynames
one_of() |	Columns whose name appear in the given set |	select(babynames, one_of(c("sex", "gender")))
starts_with()	| Columns that starts with a string	| select(babynames, starts_with("n"))



## [`filter`](https://dplyr.tidyverse.org/reference/filter.html): Subset rows using column values

Logical operator	| tests	| Example
--|-----|---
>	| Is x greater than y? |	x > y
>=	| Is x greater than or equal to y? |	x >= y
<	| Is x less than y?	| x < y
<=	| Is x less than or equal to y? | 	x <= y
==	| Is x equal to y? |	x == y
!=	| Is x not equal to y? |	x != y
is.na()	| Is x an NA?	| is.na(x)
!is.na() |	Is x not an NA? |	!is.na(x)



## [`arrange`](https://dplyr.tidyverse.org/reference/arrange.html) and `Pipe %>%`

* `arrange()` orders the rows of a data frame by the values of selected columns.

Unlike other `dplyr` verbs, `arrange()` largely ignores grouping; you need to explicitly mention grouping variables (`or use .by_group = TRUE) in order to group by them, and functions of variables are evaluated once per data frame, not once per group.

* [`pipes`](https://r4ds.had.co.nz/pipes.html) in R for Data Science.



## [`mutate`](https://dplyr.tidyverse.org/reference/mutate.html) 

* Create, modify, and delete columns

* Useful mutate functions

  - +, -, log(), etc., for their usual mathematical meanings

  - lead(), lag()

  - dense_rank(), min_rank(), percent_rank(), row_number(), cume_dist(), ntile()

  - cumsum(), cummean(), cummin(), cummax(), cumany(), cumall()

  - na_if(), coalesce()### `group_by()` and `summarise()`



## [`group_by`](https://dplyr.tidyverse.org/reference/group_by.html)



## [`summarise` or `summarize`](https://dplyr.tidyverse.org/reference/summarise.html)

#### Summary functions

So far our summarise() examples have relied on sum(), max(), and mean(). But you can use any function in summarise() so long as it meets one criteria: the function must take a vector of values as input and return a single value as output. Functions that do this are known as summary functions and they are common in the field of descriptive statistics. Some of the most useful summary functions include:

1. Measures of location - mean(x), median(x), quantile(x, 0.25), min(x), and max(x)
2. Measures of spread - sd(x), var(x), IQR(x), and mad(x)
3. Measures of position - first(x), nth(x, 2), and last(x)
4. Counts - n_distinct(x) and n(), which takes no arguments, and returns the size of the current group or data frame.
5. Counts and proportions of logical values - sum(!is.na(x)), which counts the number of TRUEs returned by a logical test; mean(y == 0), which returns the proportion of TRUEs returned by a logical test.


  - if_else(), recode(), case_when()

