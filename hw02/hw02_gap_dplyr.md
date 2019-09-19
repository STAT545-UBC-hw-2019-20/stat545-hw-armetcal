hw02\_gap\_dplyr
================
Avril Metcalfe-Roach
18 September 2019

# Exercise 1: Dplyr package

## Data Initialization

``` r
raw_data <- gapminder %>% 
  as_tibble()
```

## 1.1 - Subset gapminder to 3 countries, 1970s.

### Countries: Canada, India, Italy

``` r
filtered <- raw_data %>% 
  filter(country %in% c("Canada","India","Italy"), 
         year %in% c(1970:1979))
```

## 1.2 - Select country, gdpPercap using %\>%

``` r
country_gdp <- filtered %>% 
  select(country,gdpPercap)
```

## 1.3 - Countries with drops in life expectancy

### Note: Countries are included if they have ever experienced a recorded drop in life expectancy.
