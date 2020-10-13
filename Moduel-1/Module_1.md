Module 1: Home Work
================
Lemi Daba
10/12/2020

## Queston 12

Suppose that you want R to display ‘’Hello world\!’’ Drag and drop the
phrases to create the correct R input. Note that there may be multiple
ways to write this in R but we want you to use this command
specifically.

### Answer

``` r
print("Hello World!")
```

    ## [1] "Hello World!"

## Question 13

If you run the following code in R, what does the object my\_sqrt
contain?

    z <- c(pi, 205, 149, -2)
    y <- c(z, 555, z)
    y <- 2 * y + 760
    my_sqrt <- sqrt(y - 1)

### Answer

Let’s run the code and observe the output.

``` r
z <- c(pi, 205, 149, -2)
y <- c(z, 555, z)
y <- 2 * y + 760
my_sqrt <- sqrt(y - 1)

my_sqrt
```

    ## [1] 27.66375 34.19064 32.51154 27.47726 43.23193 27.66375 34.19064 32.51154
    ## [9] 27.47726

It appears our output is a vector of length 9.

## Question 14

Assume that you tell R to divide zero by zero, what would you get?

### Answer

Let’s try it\!

``` r
0/0
```

    ## [1] NaN

As can be observed, the result is `NaN` or Not a Number. `NaN` is one of
four special values for doubles in R. The other three are `NA`, `Inf`
and `-Inf`.

## Question 15

If you have a missing value and you try to add it to a number, what
result would you get?

### Answer

Let’s give it a try\!

``` r
2 + NA
```

    ## [1] NA

As you can see the answer is `NA`, a missing value. This is true in
genera. Any arithmetic operation with a missing value returns a missing
value.

## Question 16

We have asked the age of a group of 12 students. While 10 of them
provided us with this information, 2 of them did not. We have
constructed the vector age that captures this information.

    age <- c(12, 28, 35, 27, NA, 25, 32, 45, 31, 23, NA, 34)

If we were interested in getting the vector without the missing values,
which of the following lines of code would be useful to achieve this
purpose? (Select all that apply)

### Answer

Let’s locate (find the index position) of the missing values first.

``` r
which(is.na(age))
```

    ## [1]  5 11

So the 5th and 11th entries are missing. Then all of the following are
alternatives to extract only the non-missing values in `age`.

``` r
age[-c(5, 11)]  # the - sign removes the 5th and 11th entries
```

    ##  [1] 12 28 35 27 25 32 45 31 23 34

``` r
age[c(-5, -11)] # the - signs removes the 5th and 11th entries
```

    ##  [1] 12 28 35 27 25 32 45 31 23 34

``` r
age[c(1, 2, 3, 4, 6, 7, 8, 9, 10, 12)]  # subsets based on the given index values
```

    ##  [1] 12 28 35 27 25 32 45 31 23 34

``` r
age[!is.na(age)]  # uses logical subsetting to extract non-missing values (most efficient)
```

    ##  [1] 12 28 35 27 25 32 45 31 23 34

## Question 17

Download the data “CitesforSara.csv” into RStudio. This dataset includes
paper-level citations from 1969 to 1998. First, read the CSV file into R
using these commands:

    library(tidyverse)
    papers <- as_tibble(read_csv("[YOURFILEPATH]/CitesforSara.csv"))

Great\! Let’s create a simplified dataset which only keeps the following
variables contained in the papers dataset in this order: journal, year,
cites, title, and au1. Use the method `select()` to accomplish this. Set
this output to the variable `papers_select.` Drag and drop to create the
code. Note that there may be more than one way to do this but there is
only one correct answer from the following drag-and-drop options.

### Answer

Based on the drag and drop template:

``` r
papers_select <- select(papers, journal, year, cites, title, au1)

# Let's see our data set:
papers_select
```

    ## # A tibble: 4,182 x 5
    ##    journal          year cites title                                au1         
    ##    <chr>           <dbl> <dbl> <chr>                                <chr>       
    ##  1 American-Econo~  1993    31 Jeux Sans Frontieres:  Tax Competit~ Kanbur,-Ravi
    ##  2 American-Econo~  1993     4 Changes in Economic Instability in ~ James,-John~
    ##  3 American-Econo~  1993    28 Factor Shares and Savings in Endoge~ Bertola,-Gi~
    ##  4 American-Econo~  1993    10 Strategic Discipline in Monetary Po~ Garfinkel,-~
    ##  5 American-Econo~  1993     5 Will Affirmative-Action Policies El~ Coate,-Step~
    ##  6 American-Econo~  1993    21 Mergers and Market Power:  Evidence~ Kim,-E.-Han 
    ##  7 American-Econo~  1993    45 A Search-Theoretic Approach to Mone~ Kiyotaki,-N~
    ##  8 American-Econo~  1993    13 An Experimental Test of the Public-~ Andreoni,-J~
    ##  9 American-Econo~  1993     5 A General Experiment on Bargaining ~ Kahn,-Lawre~
    ## 10 American-Econo~  1993     2 Nominal-Contracting Theories of Une~ Keane,-Mich~
    ## # ... with 4,172 more rows

## Quesion 18

Let’s take a look at some of the most popular papers. Using the
`filter()` method, how many records exist where there are greater than
or equal to 100 citations?

### Answer

``` r
papers_select %>%
  filter(cites >= 100)
```

    ## # A tibble: 205 x 5
    ##    journal          year cites title                                au1         
    ##    <chr>           <dbl> <dbl> <chr>                                <chr>       
    ##  1 American-Econo~  1994   117 Is Inequality Harmful for Growth?    Persson,-To~
    ##  2 Econometrica     1971   149 Further Evidence on the Estimation ~ Nerlove,-Ma~
    ##  3 Econometrica     1971   170 The Use of Variance Components Mode~ Maddala,-G.~
    ##  4 Econometrica     1971   155 Investment Under Uncertainty         Lucas,-Robe~
    ##  5 Econometrica     1971   139 Some Statistical Models for Limited~ Cragg,-John~
    ##  6 Econometrica     1971   108 Identification in Parametric Models  Rothenberg,~
    ##  7 Econometrica     1972   164 Methods of Estimation for Markets i~ Fair,-Ray-C.
    ##  8 Econometrica     1972   150 Existence of Equilibrium of Plans, ~ Radner,-Roy 
    ##  9 Econometrica     1973   361 Manipulation of Voting Schemes: A G~ Gibbard,-Al~
    ## 10 Econometrica     1973   107 On a Class of Equilibrium Condition~ Kramer,-Ger~
    ## # ... with 195 more rows

As observed in the header, there are 205 records with at least 100
citations.

## Question 19

Use the `group_by()` function to group papers by journal. How many total
citations exist for the journal “Econometrica”?

### Answer

``` r
papers_select %>%
  group_by(journal) %>%
  summarise(tot_cites = sum(cites, na.rm = TRUE))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 7 x 2
    ##   journal                            tot_cites
    ##   <chr>                                  <dbl>
    ## 1 American-Economic-Review                3738
    ## 2 Econometrica                           75789
    ## 3 Journal-of-Political-Economy            3398
    ## 4 Quarterly-Journal-of-Economics          8844
    ## 5 Review-of-Economic-Studies             21937
    ## 6 Review-of-Economics-and-Statistics      8473
    ## 7 <NA>                                      14

The journal Econometrica has 75789 total citations.

## Question 20

How many distinct primary authors (*au1*) exist in this dataset? Note:
do not remove `NA` values.

### Answer

``` r
papers_select %>%
  summarise(n_distinct(au1))
```

    ## # A tibble: 1 x 1
    ##   `n_distinct(au1)`
    ##               <int>
    ## 1              2332

There are 2332 distinct primary authors.

## Question 21

Use the *dpylr* `contains()` method to create a new dataset called
`papers_female` which contains only the columns from papers containing
the string “female”. Drag and drop to create the code. Note that there
may be more than one way to do this but there is only one correct answer
from the following drag-and-drop options.

### Answer

Based on the drag-and-drop template:

``` r
paper_female <- select(papers, contains("female"))

paper_female
```

    ## # A tibble: 4,182 x 3
    ##    female1 female2 female3
    ##      <dbl>   <dbl>   <dbl>
    ##  1       0       0      NA
    ##  2       0      NA      NA
    ##  3       0      NA      NA
    ##  4       1       0      NA
    ##  5       0       0      NA
    ##  6       0       0      NA
    ##  7       0       0      NA
    ##  8       0      NA      NA
    ##  9       0       0      NA
    ## 10       0      NA      NA
    ## # ... with 4,172 more rows
