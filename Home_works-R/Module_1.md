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

``` r
z <- c(pi, 205, 149, -2)
y <- c(z, 555, z)
y <- 2 * y + 760
my_sqrt <- sqrt(y - 1)
```

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
