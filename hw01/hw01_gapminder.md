hw01\_gapminder
================
Avril Metcalfe-Roach
10 September 2019

## Formatting the preliminary dataset

``` r
raw_data <- gapminder %>% 
  as_tibble()
```

## Plotting Canadian life expectancy from 1952 to 2007

### Isolate Country, Life Exp, and Year columns

``` r
col_data <- raw_data %>% 
  select(country,year,lifeExp)
```

### Isolate Canadian data only

``` r
refined_data <- col_data %>% 
  filter(country=="Canada")
```

### Create scatterplot

#### Note: requires plotrix package.

``` r
attach(refined_data) # Defines dataset as current object
plot_title <- "Canadian Life Expectancy from 1952 to 2007"
x_title <- "Year"
y_title <- "Life Expectancy (years)"
plot(year, lifeExp, main=plot_title, xlab=x_title,ylab=y_title)

# Add line of best fit:
fit <- lm(lifeExp~year)
abline(fit, col="red")

# Add R squared value to plot:
rsq <- summary(fit)$adj.r.squared %>% 
  format(digits=3) %>% 
  as.character()
rsq_label <- paste("R^2: ",rsq)
plotrix::corner.label(rsq_label)
```

![](hw01_gapminder_files/figure-gfm/Life_vs_Year-1.png)<!-- -->

    ## $x
    ## [1] 1949.8
    ## 
    ## $y
    ## [1] 81.12912
