# Our World in Data {#owid}


## The package `owidR`

> We study the R package `owidR` for importing data from Our World in Data.

Warnings: The package does not work properly though there was no problem in AY2022.

## References

The package official site contains other links. When you quote the package, use the link to the official site.

* Package Official Site: https://CRAN.R-project.org/package=owidR
  - ReadMe: https://cran.r-project.org/web/packages/owidR/readme/README.html
  - Manual: https://cran.r-project.org/web/packages/owidR/owidR.pdf
  - Vignette: [Create and Analyse a Dataset](https://cran.r-project.org/web/packages/owidR/vignettes/example-analysis.html)
* [owidR: Import Data from Our World in Data](https://rdrr.io/cran/owidR/)
  - Man page and source codes
  
In general, README gives a short introduction to the package, a Manual, the comprehensive descriptions of each function, and a Vignette, a practical introduction containing examples and applications.

## Introduction

>This package acts as an interface to [Our World in Data](https://ourworldindata.org) datasets, allowing for an easy way to search through data used in over 3,000 charts and load them into the R environment.

### Setup

#### Installation

Run the following for the first time


```r
install.packages("owidR")
```

#### Load the package


```r
library(owidR)
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

The package automatically load a part of `tidyverse`, e.g., `dplyr`, `ggplot`, .... Since it works well with the scheme`tidyverse`, it is better to load `tidyverse` with it.

The creator of this package also suggests loading packages `plm` for panels of data, and `texreg` for displaying models, but let us start without them until we actually use them. For panel data, see, for example, the site](https://www.aptech.com/blog/introduction-to-the-fundamentals-of-panel-data/).

### Core functions

#### List of core functions

In this package, `chart` is close to data, and `chart id` is a data indicator.

* owid: Get a dataset used in an OWID chart
* owid_covid: Get the Our World in Data covid-19 dataset
* owid_search: Search the data sources used in OWID charts
* owid_source: A function to get source information from an OWID dataset and display it in the R console.
* pal_owid: Colour palettes based on the colours used by Our World in Data
* view_chart: A function that opens the original OWID chart in your browser
* world_map_data: Function that returns a simple feature collection of class sf. Map data is from naturalearthdata.com. Designed to be used internally.

#### Usage

##### `owid_search`

Search the data sources used in OWID charts

```
owid_search(term)
```

* Example

Since the output is long, I cut it off to the first six rows using `head()`.


```r
owid_search("emissions") %>% head()
#>      titles                                               
#> [1,] "Methane emissions from agriculture"                 
#> [2,] "Nitrous oxide emissions from agriculture"           
#> [3,] "Per capita nitrous oxide emissions from agriculture"
#> [4,] "Air pollutant emissions"                            
#> [5,] "Emissions of air pollutants"                        
#> [6,] "Emissions of air pollutants"                        
#>      chart_id                              
#> [1,] "methane-emissions-agriculture"       
#> [2,] "nitrous-oxide-agriculture"           
#> [3,] "per-capita-nitrous-oxide-agriculture"
#> [4,] "air-pollutant-emissions"             
#> [5,] "emissions-of-air-pollutants"         
#> [6,] "emissions-of-air-pollutants-oecd"
```

A matrix is returned. If the list is long, it is easier to see the pairs of the titles and chart_ids by adding `as_tibble()`.


```r
owid_search("emissions") %>% as_tibble()
#> # A tibble: 187 × 2
#>    titles                                           chart_id
#>    <chr>                                            <chr>   
#>  1 Methane emissions from agriculture               methane…
#>  2 Nitrous oxide emissions from agriculture         nitrous…
#>  3 Per capita nitrous oxide emissions from agricul… per-cap…
#>  4 Air pollutant emissions                          air-pol…
#>  5 Emissions of air pollutants                      emissio…
#>  6 Emissions of air pollutants                      emissio…
#>  7 Emissions of particulate matter                  emissio…
#>  8 Global sulphur dioxide (SO₂) emissions by world… so-emis…
#>  9 Sulphur dioxide (SO₂) emissions                  so2-emi…
#> 10 Sulphur oxide (SO₂) emissions                    sulphur…
#> # ℹ 177 more rows
```

If the list is not long, you do not need to add `as_tibble()`. However, note that you need to keep in mind that the title and the chart_id consists of a pair, and you need to use the chart_id to download the data using `owid`.


```r
owid_search("human rights")
#>      titles                                                                             
#> [1,] "Human rights index vs. electoral democracy index"                                 
#> [2,] "Confirmed killings of human rights defenders, journalists and trade unionists"    
#> [3,] "Countries with accredited independent national human rights institutions"         
#> [4,] "Distribution of human rights index"                                               
#> [5,] "Human rights index"                                                               
#> [6,] "Human rights index"                                                               
#> [7,] "Human rights index vs. GDP per capita"                                            
#> [8,] "Share of countries with accredited independent national human rights institutions"
#>      chart_id                                                                   
#> [1,] "human-rights-index-vs-electoral-democracy-index"                          
#> [2,] "cases-of-killed-human-rights-defenders-journalists-trade-unionists"       
#> [3,] "countries-with-independent-national-human-rights-institution"             
#> [4,] "distribution-human-rights-index-vdem"                                     
#> [5,] "human-rights-index-vdem"                                                  
#> [6,] "human-rights-index-population-weighted"                                   
#> [7,] "human-rights-index-vs-gdp-per-capita"                                     
#> [8,] "share-countries-accredited-independent-national-human-rights-institutions"
```


##### `owid`

Get a dataset used in an OWID chart

```
owid(chart_id = NULL, rename = NULL, tidy.date = TRUE, ...)
```

`chard_id`: The chart_id as returned by owid_search, which is combined with '-'. Don't mix up with the chart titles.

`rename`: Rename the value column. Currently only works if their is just one value col- umn.

* Example


```r
emissions <- owid("per-capita-ghg-emissions")
```


```r
emissions
```


```r
rights <- owid("human-rights-scores")
```


```r
rights
```

**Note.**

1. You can use `rename` to change column names. For example, 


```r
owid("per-capita-ghg-emissions", rename = "ghgPcap")
```

2. Since until after importing the data, you never know the original column name, and how many columns are for indicators. It is natural to change column names using `dpyr::rename`. In the next example, I used `Total including LUCF`. However, 'Total including LUCF' and "Total including LUCF" work as well.


```r
emissions %>% rename(ghgPcap = `Per-capita greenhouse gas emissions in CO2 equivalents`)
```

3. If there are more than one variables to rename, use vector notation as follows. Here `top_n(1)` is same as `slice(1)`, and gives the first row only.


```r
owid("electoral-democracy") %>% top_n(1)
```


```r
owid("electoral-democracy", rename = c("electoral_democracy", "vdem_high", "vdem_low"))
```


4. You can use `dplyr::rename`, and keep the record of renaming column names.


```r
(democracy <- owid("electoral-democracy"))
```



```r
democracy <- democracy %>% 
  rename(`electoral_democracy` = `Electoral democracy`,  
         `vdem_high` = `electdem_vdem_high_owid`, 
         `electdem_vdem_low_owid` = `electdem_vdem_low_owid`)
democracy
```


##### `owid_source`

A function to get source information from an OWID dataset and display it in the R console.

```
owid_source(data)
```

* Example


```r
owid_source(emissions)
```



```r
owid_source(rights)
```



##### `view_chart`

A function that opens the original OWID chart in your browser

```
view_chart(x)
```

* `x` Either a tibble returned by `owid()`, or a `chart_id`.

* Example

The first one uses the chart, i.e., the tibble returned by `owid()`, and the second, `chart_id`. You can also embed in your R Markdown file by copying Embed `iframe` clink from `Share` botton at the bottom right corner.


```r
firearm_suicide <- owid("suicide-rate-by-firearm")
    view_chart(firearm_suicide)
```

<iframe src="https://ourworldindata.org/grapher/suicide-rate-by-firearm" loading="lazy" style="width: 100%; height: 600px; border: 0px none;"></iframe>


```r
view_chart("electoral-democracy")
```

<iframe src="https://ourworldindata.org/grapher/electoral-democracy?country=ARG~AUS~BWA~CHN" loading="lazy" style="width: 100%; height: 600px; border: 0px none;"></iframe>


```r
view_chart("share-of-individuals-using-the-internet")
```

<iframe src="https://ourworldindata.org/grapher/share-of-individuals-using-the-internet" loading="lazy" style="width: 100%; height: 600px; border: 0px none;"></iframe>


##### `pal_owid`

Colour palettes based on the colours used by Our World in Data

##### `owid_covid`

owid_covid: Get the Our World in Data covid-19 dataset

```
owid_covid()
```

See the detail at the [GitHub site](https://github.com/owid/covid-19-data/tree/master/public/data#data-on-covid-19-coronavirus-by-our-world-in-data).

* Example


```r
covid <- owid_covid()
```


```r
covid %>% filter(location == "Japan")
#> # A tibble: 1,428 × 67
#>    iso_code continent location date       total_cases
#>    <chr>    <chr>     <chr>    <date>           <dbl>
#>  1 JPN      Asia      Japan    2020-01-03          NA
#>  2 JPN      Asia      Japan    2020-01-04          NA
#>  3 JPN      Asia      Japan    2020-01-05          NA
#>  4 JPN      Asia      Japan    2020-01-06          NA
#>  5 JPN      Asia      Japan    2020-01-07          NA
#>  6 JPN      Asia      Japan    2020-01-08          NA
#>  7 JPN      Asia      Japan    2020-01-09          NA
#>  8 JPN      Asia      Japan    2020-01-10          NA
#>  9 JPN      Asia      Japan    2020-01-11          NA
#> 10 JPN      Asia      Japan    2020-01-12          NA
#> # ℹ 1,418 more rows
#> # ℹ 62 more variables: new_cases <dbl>,
#> #   new_cases_smoothed <dbl>, total_deaths <dbl>,
#> #   new_deaths <dbl>, new_deaths_smoothed <dbl>,
#> #   total_cases_per_million <dbl>,
#> #   new_cases_per_million <dbl>,
#> #   new_cases_smoothed_per_million <dbl>, …
```

## Examples

The following is based on the presentation and the first two R Notebook files created by Professor Kaizoji.

### Human Rights- modified from  README

Lets use the core functions to get data on how human rights have changed over time. First by searching for charts on human rights.


```r
owid_search("human rights") %>% as_tibble()
#> # A tibble: 8 × 2
#>   titles                                            chart_id
#>   <chr>                                             <chr>   
#> 1 Human rights index vs. electoral democracy index  human-r…
#> 2 Confirmed killings of human rights defenders, jo… cases-o…
#> 3 Countries with accredited independent national h… countri…
#> 4 Distribution of human rights index                distrib…
#> 5 Human rights index                                human-r…
#> 6 Human rights index                                human-r…
#> 7 Human rights index vs. GDP per capita             human-r…
#> 8 Share of countries with accredited independent n… share-c…
```

Let’s use the human rights protection dataset.


```r
rights <- owid("human-rights-protection")
rights
```

ggplot2 makes it easy to visualise our data.



```r
rights %>% 
  filter(entity %in% c("United Kingdom", "France", "United States", "Japan")) %>%  
  ggplot(aes(year, `Human rights protection`, colour = entity)) +
  geom_line()
```


### Internet - modified from vignette



```r
owid_search("internet") %>% as_tibble()
#> # A tibble: 8 × 2
#>   titles                                            chart_id
#>   <chr>                                             <chr>   
#> 1 Landline Internet subscriptions                   landlin…
#> 2 Landline Internet subscriptions by download speed landlin…
#> 3 Landline Internet subscriptions per 100 people    broadba…
#> 4 Landline Internet subscriptions per 100 people, … landlin…
#> 5 Number of people using the Internet               number-…
#> 6 Share of US adults who use the Internet, by age   share-u…
#> 7 Share of primary schools with access to the Inte… primary…
#> 8 Share of the population using the Internet        share-o…
```

Get a dataset used in an OWID chart.


```r
owid("share-of-individuals-using-the-internet") %>% top_n(1)
```


```r
internet <- owid("share-of-individuals-using-the-internet", rename = "internet_use")
internet
```

Get source information on an OWID dataset


```r
owid_source(internet)
```

A function that opens the original OWID chart in your browser.


```r
view_chart(internet)
```

<iframe src="https://ourworldindata.org/grapher/share-of-individuals-using-the-internet" loading="lazy" style="width: 100%; height: 600px; border: 0px none;"></iframe>

Plot an owid dataset.  The first is the simplest, and the second uses oied theme.


```r
internet %>% filter(entity == "World") %>%
  ggplot(aes(year, internet_use))+ geom_line() 
```


```r
internet %>% filter(entity == "World") %>%
  ggplot(aes(year, internet_use))+ geom_line() +
  labs(title = "Share of the World Population \nusing the Internet",
       y = "Individuals using the Internet \n(% of population)") +
  scale_y_continuous(limits = c(0, 100))
```


```r
internet %>% 
  filter(entity %in% c("United Kingdom", "Spain", "Russia", "Egypt", "Nigeria")) %>% 
  ggplot(aes(year, internet_use, color =  entity)) + geom_line() +
  labs(title = "Share of Population with Using the Internet",
       y = "Individuals using the Internet \n(% of population)",
       color = "country") +
  scale_y_continuous(limits = c(0, 100), labels = scales::label_number(suffix = "%"))
```

Creating a choropleth map.


```r
owid_map(internet, year = 2017) +
  labs(title = "Share of Population Using the Internet, 2017")
```

### Democracy - modified from vignette


```r
owid_search("democrac") %>% as_tibble()
#> # A tibble: 93 × 2
#>    titles                                           chart_id
#>    <chr>                                            <chr>   
#>  1 Child mortality rate vs. electoral democracy     child-m…
#>  2 People living in democracies and non-democracies world-p…
#>  3 Age of democracy                                 age-of-…
#>  4 Age of democracy                                 age-of-…
#>  5 Age of democracy                                 age-of-…
#>  6 Age of electoral democracy                       age-of-…
#>  7 Age of electoral democracy                       age-of-…
#>  8 Age of liberal democracy                         age-of-…
#>  9 Citizen satisfaction with democracy              citizen…
#> 10 Citizen support for democracy                    citizen…
#> # ℹ 83 more rows
```


```r
owid("electoral-democracy") %>% top_n(1)
```


```r
democracy <- owid("electoral-democracy", rename = c("electoral_democracy", "vdem_high", "vdem_low"))
democracy
```


```r
owid_source(democracy)
```


```r
owid_map(democracy, year = 2015, palette = "YlGn") +
  labs(title = "Electoral Democracy")
```


```r
democracy %>% 
  filter(entity %in% c("United Kingdom", "Spain", "Russia", "Egypt", "Nigeria")) %>%
  ggplot(aes(year, electoral_democracy, color = entity)) + geom_line() +
  labs(title = "Electoral Democracy", y = "", color = "country") +
  scale_y_continuous(limits = c(0, 1), labels = scales::label_number(suffix = "%"))
```



```r
gdp <- owid("gdp-per-capita-worldbank", rename = "gdp")

gov_exp <- owid("total-gov-expenditure-gdp-wdi", rename = "gov_exp")

age_dep <- owid("age-dependency-ratio-of-working-age-population", rename = "age_dep")

unemployment <- owid("unemployment-rate", rename = "unemp")
```

Mutating joins

left_join(): includes all rows in x.

**References**

* See https://dplyr.tidyverse.org/reference/mutate-joins.html.
* Posit Primers - Tidy your data: https://posit.cloud/learn/primers/4
  - Join Data Sets: https://posit.cloud/learn/primers/4.3


```r
data <- internet %>% 
  left_join(democracy) %>% 
  left_join(gdp) %>% 
  left_join(gov_exp) %>% 
  left_join(age_dep) %>% 
  left_join(unemployment)
```

Drawing scatter plot


```r
data %>% 
  filter(year == 2015) %>% 
  ggplot(aes(internet_use, electoral_democracy)) +
  geom_point(colour = "#57677D", na.rm = TRUE) +
  geom_smooth(method = "lm", colour = "#DC5E78", na.rm = TRUE) +
  labs(title = "Relationship Between Internet Use \nand electoral_democracy", x = "Internet Use", y = "electoral_democracy")
```



```r
data %>% 
  filter(year == 2015) %>% 
  ggplot(aes(gdp, internet_use)) +
  geom_point(colour = "blue") +
  geom_smooth(method = "gam", colour = "red", level = 0.0) +
  labs(title = "Relationship Between Internet Use and GDP", x = "GDP", y = "Internet Use")
```



```r
model1 <- lm(electoral_democracy ~ internet_use, data)
summary(model1)
```

```r
model2 <- lm(gdp ~ internet_use, data)
summary(model2)
```

Creating a table of the results of the regression analysis using `texreg`.
For the first time, install the pacage `texreg`.


```r
install.packages("texreg")
```



```r
library(texreg)
#> Version:  1.38.6
#> Date:     2022-04-06
#> Author:   Philip Leifeld (University of Essex)
#> 
#> Consider submitting praise using the praise or praise_interactive functions.
#> Please cite the JSS article in your publications -- see citation("texreg").
#> 
#> Attaching package: 'texreg'
#> The following object is masked from 'package:tidyr':
#> 
#>     extract
```



```r
models <- list("Model 1" = model1,
               "Model 2" = model2)
screenreg(models, stars = NULL)
```
