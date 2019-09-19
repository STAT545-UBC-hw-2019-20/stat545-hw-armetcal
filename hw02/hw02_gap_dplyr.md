hw02\_gap\_dplyr
================
Avril Metcalfe-Roach
18 September 2019

# Exercise 1: Dplyr package

## Data Initialization

``` r
raw_data <- gapminder %>% 
  as_tibble()
head(raw_data, 5)
```

    ## # A tibble: 5 x 6
    ##   country     continent  year lifeExp      pop gdpPercap
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779.
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.

## 1.1 - Subset gapminder to 3 countries, 1970s.

### Countries: Canada, India, Italy

``` r
filtered <- raw_data %>% 
  filter(country %in% c("Canada","India","Italy"), 
         year %in% c(1970:1979))
filtered
```

    ## # A tibble: 6 x 6
    ##   country continent  year lifeExp       pop gdpPercap
    ##   <fct>   <fct>     <int>   <dbl>     <int>     <dbl>
    ## 1 Canada  Americas   1972    72.9  22284500    18971.
    ## 2 Canada  Americas   1977    74.2  23796400    22091.
    ## 3 India   Asia       1972    50.7 567000000      724.
    ## 4 India   Asia       1977    54.2 634000000      813.
    ## 5 Italy   Europe     1972    72.2  54365564    12269.
    ## 6 Italy   Europe     1977    73.5  56059245    14256.

## 1.2 - Select country, gdpPercap using %\>%

``` r
country_gdp <- filtered %>% 
  select(country,gdpPercap)
country_gdp
```

    ## # A tibble: 6 x 2
    ##   country gdpPercap
    ##   <fct>       <dbl>
    ## 1 Canada     18971.
    ## 2 Canada     22091.
    ## 3 India        724.
    ## 4 India        813.
    ## 5 Italy      12269.
    ## 6 Italy      14256.

## 1.3 - Countries with drops in life expectancy

``` r
exp_list <- gapminder$lifeExp
change <- diff(exp_list,lag=1,differences=1)
# Add NA value to beginning of change vector:
change_2 <- append(change,NA,after=0)
# Create new tibble with delta life expectancy as a column:
gapminder_lifeExp <- gapminder
gapminder_lifeExp$delta <- change_2
head(gapminder_lifeExp,5)
```

    ## # A tibble: 5 x 7
    ##   country     continent  year lifeExp      pop gdpPercap delta
    ##   <fct>       <fct>     <int>   <dbl>    <int>     <dbl> <dbl>
    ## 1 Afghanistan Asia       1952    28.8  8425333      779. NA   
    ## 2 Afghanistan Asia       1957    30.3  9240934      821.  1.53
    ## 3 Afghanistan Asia       1962    32.0 10267083      853.  1.66
    ## 4 Afghanistan Asia       1967    34.0 11537966      836.  2.02
    ## 5 Afghanistan Asia       1972    36.1 13079460      740.  2.07

``` r
# NOTE: INCLUDES APPARENT REDUCTIONS IN LIFE EXP DUE TO SWITCHING COUNTRIES!!!
gapminder_redExp <- gapminder_lifeExp %>% 
  filter(delta < 0)
```
