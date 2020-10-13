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
