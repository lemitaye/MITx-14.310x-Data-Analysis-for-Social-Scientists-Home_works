Module 3: Home Work
================
Lemi Daba
10/14/2020

Preamble
--------

In this problem set we will guide you through different ways of
accessing real data sets and how to summarize and describe it properly.
First we will go through some of the data that is collected by the World
Bank. We will do some cleaning on the data before we start analyzing it.
Then, we will try to do a simple web scraping exercise where we will
analyze the data as well.

Let’s start with this dataset from the World Bank. Please download and
save this file in a folder where you can get it easily.

This dataset is a truncated version of one you can find on the [World
Bank Gender Statistics
website](https://datacatalog.worldbank.org/dataset/gender-statistics).
You may visit the website and explore other datasets they offer.
**However, for the purposes of this assignment, please use the file in
this set of instructions**, since the dataset on the World Bank website
may have been updated in the time since this problem set and answer key
was posted.

**NOTE**: It is important to work in the same directory that the files
are or to use the whole path when you specify opening a data set. To
know which directory you are currently working in, you can use the
command `getwd()`. Similarly, in order to set a different directory, you
can use the command `setwd()`.

For the purpose of analyzing the data, we are going to use the packages
**utils** and **tidyverse**. Once you have uploaded the data to R you
are going to see there are multiple indicators of gender, countries and
years in the data. In this case we are just interested in analyzing the
data for one indicator that is the *Adolescent Fertility Rate*, in the
data the indicator code for this variable is called SP.ADO.TFRT . This
indicator measures the annual number of births to women 15 to 19 years
of age per 1,000 women in that age group. It represents the risk of
childbearing among adolescent women 15 to 19 years of age. It is also
referred to as the age-specific fertility rate for women aged 15-19.
Once you have completed this problem set you’ll have more information of
how this rate has evolved over time and how it varies across different
groups of countries.

Take a look at the following lines of code, whose main purpose is to
upload the data in a data frame and to choose the proper indicator.
Please, try to understand the code and then run it in your computer.
Remember to set the directory accordingly to the folder where you saved
the files.

    #Preliminaries
    rm(list=ls())
    library("utils")
    library("tidyverse")

    setwd("-----------")

    #Getting the data
    gender_data <- as_tibble(read.csv("Gender_StatsData.csv"))

**Using the code, answer the following questions:**

Question 1
----------

What is the purpose of the line `rm(list = ls())`?

### Answer

This command removes all current objects in the Global Environment. It
is usually useful when we want to start a new analysis with a clean
slate.

Question 2
----------

The first thing you want to figure out when you look at a new dataset is
how it is organized. If your dataset is stored as a tibble, you can
simply print the object and it will print in a nice-looking format.

Alternatively, you can also use the built-in R commands such as `str()`,
which allows you to see the structure of an object in R. Likewise, the
commands `head()` and `tail()` will allow you to see the first six and
last six observations of your data frame respectively. Another useful
function is the function `dim()`, which will give you the number of rows
and columns in your dataset. Take the time to explore the data using
these commands and others.

Which of the following statements best describes how your data is
organized? Note that we use “indicator” to mean something that is being
measured (e.g. fertility rate, enrollment rate, etc.).

### Answer

``` r
library(tidyverse)
library(utils)

gender_data <- read_csv("Gender_StatsData.csv")
```

With tibbles we can view the first few observations without using
`head()`:

``` r
gender_data
```

    ## # A tibble: 7,101 x 64
    ##       X1 Country.Name Country.Code Indicator.Name Indicator.Code X1960 X1961
    ##    <dbl> <chr>        <chr>        <chr>          <chr>          <dbl> <dbl>
    ##  1     1 Arab World   ARB          Adolescent fe~ SP.ADO.TFRT    134.  135. 
    ##  2     2 Arab World   ARB          Age at first ~ SP.DYN.SMAM.FE  NA    NA  
    ##  3     3 Arab World   ARB          Age at first ~ SP.DYN.SMAM.MA  NA    NA  
    ##  4     4 Arab World   ARB          Age dependenc~ SP.POP.DPND     88.2  89.6
    ##  5     5 Arab World   ARB          Age populatio~ SP.POP.AG00.F~  NA    NA  
    ##  6     6 Arab World   ARB          Age populatio~ SP.POP.AG00.M~  NA    NA  
    ##  7     7 Arab World   ARB          Age populatio~ SP.POP.AG01.F~  NA    NA  
    ##  8     8 Arab World   ARB          Age populatio~ SP.POP.AG02.F~  NA    NA  
    ##  9     9 Arab World   ARB          Age populatio~ SP.POP.AG02.M~  NA    NA  
    ## 10    10 Arab World   ARB          Age populatio~ SP.POP.AG03.F~  NA    NA  
    ## # ... with 7,091 more rows, and 57 more variables: X1962 <dbl>, X1963 <dbl>,
    ## #   X1964 <dbl>, X1965 <dbl>, X1966 <dbl>, X1967 <dbl>, X1968 <dbl>,
    ## #   X1969 <dbl>, X1970 <dbl>, X1971 <dbl>, X1972 <dbl>, X1973 <dbl>,
    ## #   X1974 <dbl>, X1975 <dbl>, X1976 <dbl>, X1977 <dbl>, X1978 <dbl>,
    ## #   X1979 <dbl>, X1980 <dbl>, X1981 <dbl>, X1982 <dbl>, X1983 <dbl>,
    ## #   X1984 <dbl>, X1985 <dbl>, X1986 <dbl>, X1987 <dbl>, X1988 <dbl>,
    ## #   X1989 <dbl>, X1990 <dbl>, X1991 <dbl>, X1992 <dbl>, X1993 <dbl>,
    ## #   X1994 <dbl>, X1995 <dbl>, X1996 <dbl>, X1997 <dbl>, X1998 <dbl>,
    ## #   X1999 <dbl>, X2000 <dbl>, X2001 <dbl>, X2002 <dbl>, X2003 <dbl>,
    ## #   X2004 <dbl>, X2005 <dbl>, X2006 <dbl>, X2007 <dbl>, X2008 <dbl>,
    ## #   X2009 <dbl>, X2010 <dbl>, X2011 <dbl>, X2012 <dbl>, X2013 <dbl>,
    ## #   X2014 <dbl>, X2015 <dbl>, X2016 <dbl>, X2017 <dbl>, X <lgl>

(We can get a more exteded view with `View(gender_data)` in RStudio.)
Here, let’s use knitr’s `kable` command to get a nice formatted tabular
view of the first 15 observations in our data.

``` r
knitr::kable(gender_data[1:15, ])
```

|  X1 | Country.Name | Country.Code | Indicator.Name                                                | Indicator.Code    |     X1960 |     X1961 |    X1962 |     X1963 |     X1964 |     X1965 |     X1966 |     X1967 |     X1968 |     X1969 |    X1970 |     X1971 |     X1972 |     X1973 |     X1974 |     X1975 |     X1976 |     X1977 |     X1978 |     X1979 |    X1980 |    X1981 |    X1982 |    X1983 |    X1984 |    X1985 |    X1986 |    X1987 |    X1988 |    X1989 |    X1990 |    X1991 |    X1992 |    X1993 |    X1994 |    X1995 |    X1996 |    X1997 |    X1998 |    X1999 |    X2000 |    X2001 |    X2002 |   X2003 |    X2004 |    X2005 |    X2006 |    X2007 |    X2008 |    X2009 |    X2010 |    X2011 |    X2012 |    X2013 |    X2014 |    X2015 |    X2016 |    X2017 | X   |
|----:|:-------------|:-------------|:--------------------------------------------------------------|:------------------|----------:|----------:|---------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|---------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|--------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|---------:|:----|
|   1 | Arab World   | ARB          | Adolescent fertility rate (births per 1,000 women ages 15-19) | SP.ADO.TFRT       | 134.22361 | 134.83863 | 135.5709 | 135.44464 | 135.27490 | 134.94717 | 134.23360 | 133.36223 | 130.87250 | 128.41216 | 126.0751 | 123.83898 | 121.76496 | 119.62902 | 117.47265 | 115.23584 | 112.91609 | 110.52381 | 106.66121 | 102.85523 | 99.13658 | 95.51899 | 91.96122 | 88.18633 | 84.39776 | 80.58370 | 76.71829 | 72.84313 | 71.56606 | 70.32371 | 69.46716 | 68.21199 | 67.31459 | 65.25606 | 63.17755 | 60.90790 | 58.76574 | 56.59019 | 55.74007 | 54.93289 | 54.16982 | 53.31340 | 52.48572 | 52.0346 | 51.62959 | 51.26730 | 50.87727 | 50.54339 | 50.31699 | 50.10461 | 49.90012 | 49.72376 | 49.53907 | 49.11124 | 48.64754 | 48.11455 | 47.44007 |       NA | NA  |
|   2 | Arab World   | ARB          | Age at first marriage, female                                 | SP.DYN.SMAM.FE    |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   3 | Arab World   | ARB          | Age at first marriage, male                                   | SP.DYN.SMAM.MA    |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   4 | Arab World   | ARB          | Age dependency ratio (% of working-age population)            | SP.POP.DPND       |  88.20581 |  89.64473 |  90.9445 |  92.06363 |  92.89288 |  93.36446 |  94.24178 |  94.63345 |  94.68551 |  94.56361 |  94.3360 |  94.59772 |  94.61873 |  94.45822 |  94.18243 |  93.85107 |  93.68274 |  93.43655 |  93.11851 |  92.70133 | 92.16788 | 91.88224 | 91.43619 | 90.87598 | 90.26319 | 89.62859 | 89.37816 | 89.02484 | 88.58989 | 88.04431 | 87.48134 | 86.72618 | 86.05812 | 84.90675 | 83.59814 | 81.94642 | 80.57681 | 79.14266 | 77.67581 | 76.19787 | 74.71481 | 73.21952 | 71.74723 | 70.3091 | 68.92062 | 67.60288 | 66.41868 | 65.27545 | 64.23529 | 63.36503 | 62.69472 | 62.34170 | 62.16885 | 62.11819 | 62.08986 | 62.01723 | 62.05748 | 61.91618 | NA  |
|   5 | Arab World   | ARB          | Age population, age 0, female, interpolated                   | SP.POP.AG00.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   6 | Arab World   | ARB          | Age population, age 0, male, interpolated                     | SP.POP.AG00.MA.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   7 | Arab World   | ARB          | Age population, age 01, female, interpolated                  | SP.POP.AG01.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   8 | Arab World   | ARB          | Age population, age 02, female, interpolated                  | SP.POP.AG02.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|   9 | Arab World   | ARB          | Age population, age 02, male, interpolated                    | SP.POP.AG02.MA.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  10 | Arab World   | ARB          | Age population, age 03, female, interpolated                  | SP.POP.AG03.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  11 | Arab World   | ARB          | Age population, age 03, male, interpolated                    | SP.POP.AG03.MA.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  12 | Arab World   | ARB          | Age population, age 04, female, interpolated                  | SP.POP.AG04.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  13 | Arab World   | ARB          | Age population, age 04, male, interpolated                    | SP.POP.AG04.MA.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  14 | Arab World   | ARB          | Age population, age 05, female, interpolated                  | SP.POP.AG05.FE.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |
|  15 | Arab World   | ARB          | Age population, age 05, male, interpolated                    | SP.POP.AG05.MA.IN |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |        NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |      NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA |       NA | NA  |

It seems each observation corresponds to a country-indicator
combination. To confirm our suspicion, let’s count the observations in
each country-indicator combination and see if any of them contain more
than one observation:

``` r
gender_data %>%
  count(Country.Code, Indicator.Code) %>%
  filter(n > 1)
```

    ## # A tibble: 0 x 3
    ## # ... with 3 variables: Country.Code <chr>, Indicator.Code <chr>, n <int>

So the variables `Country.Code` and `Indicator.Code` do indeed uniquely
identify each observation.

Question 3
----------

Now, generate a tibble called “`teenager_fr`”, which contains only the
adolescent fertility rate indicator for each country-year. Please fill
in the blank with the correct code.

### Answer

``` r
teenager_fr <- filter(
  gender_data,
  Indicator.Code == "SP.ADO.TFRT"
)

teenager_fr
```

    ## # A tibble: 263 x 64
    ##       X1 Country.Name Country.Code Indicator.Name Indicator.Code X1960 X1961
    ##    <dbl> <chr>        <chr>        <chr>          <chr>          <dbl> <dbl>
    ##  1     1 Arab World   ARB          Adolescent fe~ SP.ADO.TFRT    134.  135. 
    ##  2    28 Caribbean s~ CSS          Adolescent fe~ SP.ADO.TFRT    147.  147. 
    ##  3    55 Central Eur~ CEB          Adolescent fe~ SP.ADO.TFRT     46.1  45.4
    ##  4    82 Early-demog~ EAR          Adolescent fe~ SP.ADO.TFRT    116.  117. 
    ##  5   109 East Asia &~ EAS          Adolescent fe~ SP.ADO.TFRT     65.9  65.0
    ##  6   136 East Asia &~ EAP          Adolescent fe~ SP.ADO.TFRT     75.2  74.5
    ##  7   163 East Asia &~ TEA          Adolescent fe~ SP.ADO.TFRT     76.6  75.9
    ##  8   190 Euro area    EMU          Adolescent fe~ SP.ADO.TFRT     27.1  28.2
    ##  9   217 Europe & Ce~ ECS          Adolescent fe~ SP.ADO.TFRT     41.2  41.9
    ## 10   244 Europe & Ce~ ECA          Adolescent fe~ SP.ADO.TFRT     47.3  47.8
    ## # ... with 253 more rows, and 57 more variables: X1962 <dbl>, X1963 <dbl>,
    ## #   X1964 <dbl>, X1965 <dbl>, X1966 <dbl>, X1967 <dbl>, X1968 <dbl>,
    ## #   X1969 <dbl>, X1970 <dbl>, X1971 <dbl>, X1972 <dbl>, X1973 <dbl>,
    ## #   X1974 <dbl>, X1975 <dbl>, X1976 <dbl>, X1977 <dbl>, X1978 <dbl>,
    ## #   X1979 <dbl>, X1980 <dbl>, X1981 <dbl>, X1982 <dbl>, X1983 <dbl>,
    ## #   X1984 <dbl>, X1985 <dbl>, X1986 <dbl>, X1987 <dbl>, X1988 <dbl>,
    ## #   X1989 <dbl>, X1990 <dbl>, X1991 <dbl>, X1992 <dbl>, X1993 <dbl>,
    ## #   X1994 <dbl>, X1995 <dbl>, X1996 <dbl>, X1997 <dbl>, X1998 <dbl>,
    ## #   X1999 <dbl>, X2000 <dbl>, X2001 <dbl>, X2002 <dbl>, X2003 <dbl>,
    ## #   X2004 <dbl>, X2005 <dbl>, X2006 <dbl>, X2007 <dbl>, X2008 <dbl>,
    ## #   X2009 <dbl>, X2010 <dbl>, X2011 <dbl>, X2012 <dbl>, X2013 <dbl>,
    ## #   X2014 <dbl>, X2015 <dbl>, X2016 <dbl>, X2017 <dbl>, X <lgl>

Question 3 (continued)
----------------------

What is the equivalent base-R function ? (select one)

(Choices are not shown here.)

### Answer

Out of the three alternatives presented, `subset()` is the equivalent
base-R function to dplyr’s `filter()`. The following code gives the same
result as using `filter()` above.

``` r
subset(gender_data, Indicator.Code == "SP.ADO.TFRT")
```

    ## # A tibble: 263 x 64
    ##       X1 Country.Name Country.Code Indicator.Name Indicator.Code X1960 X1961
    ##    <dbl> <chr>        <chr>        <chr>          <chr>          <dbl> <dbl>
    ##  1     1 Arab World   ARB          Adolescent fe~ SP.ADO.TFRT    134.  135. 
    ##  2    28 Caribbean s~ CSS          Adolescent fe~ SP.ADO.TFRT    147.  147. 
    ##  3    55 Central Eur~ CEB          Adolescent fe~ SP.ADO.TFRT     46.1  45.4
    ##  4    82 Early-demog~ EAR          Adolescent fe~ SP.ADO.TFRT    116.  117. 
    ##  5   109 East Asia &~ EAS          Adolescent fe~ SP.ADO.TFRT     65.9  65.0
    ##  6   136 East Asia &~ EAP          Adolescent fe~ SP.ADO.TFRT     75.2  74.5
    ##  7   163 East Asia &~ TEA          Adolescent fe~ SP.ADO.TFRT     76.6  75.9
    ##  8   190 Euro area    EMU          Adolescent fe~ SP.ADO.TFRT     27.1  28.2
    ##  9   217 Europe & Ce~ ECS          Adolescent fe~ SP.ADO.TFRT     41.2  41.9
    ## 10   244 Europe & Ce~ ECA          Adolescent fe~ SP.ADO.TFRT     47.3  47.8
    ## # ... with 253 more rows, and 57 more variables: X1962 <dbl>, X1963 <dbl>,
    ## #   X1964 <dbl>, X1965 <dbl>, X1966 <dbl>, X1967 <dbl>, X1968 <dbl>,
    ## #   X1969 <dbl>, X1970 <dbl>, X1971 <dbl>, X1972 <dbl>, X1973 <dbl>,
    ## #   X1974 <dbl>, X1975 <dbl>, X1976 <dbl>, X1977 <dbl>, X1978 <dbl>,
    ## #   X1979 <dbl>, X1980 <dbl>, X1981 <dbl>, X1982 <dbl>, X1983 <dbl>,
    ## #   X1984 <dbl>, X1985 <dbl>, X1986 <dbl>, X1987 <dbl>, X1988 <dbl>,
    ## #   X1989 <dbl>, X1990 <dbl>, X1991 <dbl>, X1992 <dbl>, X1993 <dbl>,
    ## #   X1994 <dbl>, X1995 <dbl>, X1996 <dbl>, X1997 <dbl>, X1998 <dbl>,
    ## #   X1999 <dbl>, X2000 <dbl>, X2001 <dbl>, X2002 <dbl>, X2003 <dbl>,
    ## #   X2004 <dbl>, X2005 <dbl>, X2006 <dbl>, X2007 <dbl>, X2008 <dbl>,
    ## #   X2009 <dbl>, X2010 <dbl>, X2011 <dbl>, X2012 <dbl>, X2013 <dbl>,
    ## #   X2014 <dbl>, X2015 <dbl>, X2016 <dbl>, X2017 <dbl>, X <lgl>

`which()` returns the position of the elements (i.e., row number/column
number/array index) in a logical vector which are TRUE, whereas
`match()` returns the position of first occurrence of its first argument
in its second.

Question 4
----------

Since we are not interested in any other variables and the gender\_data
dataset is quite large, you might want to get rid of it instead of
asking R to keep it stored in memory.

Which of the following is the correct code for getting rid of the object
`gender_data`?

(Choices are not displayed here.)

### Answer

Use `rm()` to remove objects from the global environment. So
`rm(gender_data)` achieves the desired result.
