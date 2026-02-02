Lab 03 - Nobel laureates
================
Lily Botha
02/01/2026

### Load packages and data

``` r
library(tidyverse) 
```

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

Here is a link to the [lab
instructions](https://datascience4psych.github.io/DataScience4Psych/lab03.html).

### Exercise 1

There are 935 observations and 26 variables. Each row represents a
person/laureate.

### Exercise 2

``` r
nobel_living <- nobel %>% 
  filter(is.na(died_date), 
         !is.na(country), 
         gender != "org"
  )
```

### Exercise 3

There are a substantial amount of Chemistry, Medicine, and Physics Nobel
prizes that were won in countries other than the US. This doesn’t
support the Buzzfeed article claim that most living Nobel laureates were
based in the US when they won their prizes.

``` r
nobel_living <- nobel_living %>% 
  mutate(country_us = if_else(country == "USA", "USA", "Other")
  ) 
#create new variable based on if statement: if country = "USA", set country_us to "USA", if not, set to "Other"
```

``` r
nobel_living_science <- nobel_living %>% 
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics")
  ) 
#filter by observations within a specific column (category)
```

``` r
nobel_living_science %>% 
  ggplot(aes(x = category, fill = country_us)) + 
  geom_bar() + 
  labs(
    title = "Category of Nobel Prize vs. Location Won",
    subtitle = "where Nobel laureates were based when they won", 
    x = "Country", 
    y = "Frequency", 
    fill = "Country"
  ) + 
  coord_flip()
```

![](lab-03_files/figure-gfm/bar_plot-1.png)<!-- -->

### Exercise 4

``` r
born_country_us <- nobel_living_science %>% 
  mutate(born_country_us = if_else(born_country == "USA", "USA", "Other")
  )
```

…

### Exercise 5

…

### Exercise 6

…
