Module 5: Home Work
================
Lemi Daba
10/18/2020

Question 1
----------

A manufacturer receives a shipment of 100 parts from a vendor. The
shipment will be unacceptable if more than five of the parts are
defective. The manufacturer is going to randomly select $ K $ parts from
the shipment for inspection, and the shipment will be accepted if no
defective parts are found in the sample.

How large does $ K $ have to be to ensure that the probability that the
manufacturer accepts an unacceptable shipment is less than 0.1?

*Hint: We recommend using R to plug in different values of $ K $.*

### Answer

Let $ X $ be the number of defectives out of a sample of $ K $ parts.
Then $ X $ follows the hypergeometric distribution, since this is a
problem of sampling without replacement.

It helps to think about this problem from the perspective of the
manufacturer (the one who does the inspection). So suppose you are the
manufacturer. Your goal is to minimize the probability of accepting an
unacceptable shipment. A shipment is unacceptable if there are more than
five defective parts; so we need 6 or more parts to be defective for the
problem to be relevant. Now think of the different scenarios in terms of
the true number of defective parts in the whole shipment under which it
is more likely that you make an error (i.e., accept a faulty shipment.)
The worst case scenario is when there are 6 defective and 94
non-defective parts. In this case you are less likely to find defective
parts in your sample, while the shipment is still unacceptable, and
hence, more likely to make an error. So to find the smallest $ K $ that
covers all cases, we’ll assume there are 6 defective parts. Then the
probability of finding no defective parts out of the $ K $ parts sampled
is given as:

<!-- $$P(X = 0) = \frac{ \binom{6}{0} \binom{94}{K} }{ \binom{100}{K} }$$ -->

As $ K $ increases (as we sample more parts for inspection) the
probability of finding at least one defect (i.e, the probability that at
least one of the 6 defective parts will be in our sample) increases, and
hence, the probability of finding no defective parts (and wrongly
conclude that the shipment is acceptable) decreases. So we are looking
for the smallest $ K $ such that this probability is just below 0.1. We
use the R command `dhyper()` (look-up the documentation) to calculate
the probabilities of finding no defective parts for different values of
$ K $.

``` r
K <- 10:50  # We will consider the range 10-50 parts
prob <- dhyper(x = 0, m = 6, n = 94, k = K)  # calculate the probability of zero defects for each number in K
valid <- (prob < 0.1) # create a logical vector based on the given condition

A <- as.data.frame( cbind(K, prob, valid) ) # create a data-frame by binding the vectors K, prob, and valid
A
```

    ##     K       prob valid
    ## 1  10 0.52230475     0
    ## 2  11 0.48748443     0
    ## 3  12 0.45462031     0
    ## 4  13 0.42362347     0
    ## 5  14 0.39440806     0
    ## 6  15 0.36689122     0
    ## 7  16 0.34099302     0
    ## 8  17 0.31663637     0
    ## 9  18 0.29374700     0
    ## 10 19 0.27225331     0
    ## 11 20 0.25208640     0
    ## 12 21 0.23317992     0
    ## 13 22 0.21547005     0
    ## 14 23 0.19889543     0
    ## 15 24 0.18339709     0
    ## 16 25 0.16891837     0
    ## 17 26 0.15540490     0
    ## 18 27 0.14280450     0
    ## 19 28 0.13106715     0
    ## 20 29 0.12014489     0
    ## 21 30 0.10999180     0
    ## 22 31 0.10056393     0
    ## 23 32 0.09181924     1
    ## 24 33 0.08371754     1
    ## 25 34 0.07622045     1
    ## 26 35 0.06929132     1
    ## 27 36 0.06289519     1
    ## 28 37 0.05699877     1
    ## 29 38 0.05157032     1
    ## 30 39 0.04657964     1
    ## 31 40 0.04199804     1
    ## 32 41 0.03779823     1
    ## 33 42 0.03395434     1
    ## 34 43 0.03044183     1
    ## 35 44 0.02723742     1
    ## 36 45 0.02431913     1
    ## 37 46 0.02166613     1
    ## 38 47 0.01925878     1
    ## 39 48 0.01707854     1
    ## 40 49 0.01510794     1
    ## 41 50 0.01333054     1

``` r
library(tidyverse)

A %>%
  filter(valid == 1) %>%
  filter(row_number() == 1)
```

    ##    K       prob valid
    ## 1 32 0.09181924     1

So the smallest value of $ K $ for which the probability of finding no
defect is below 0.1 is 32. We can also see this graphically.

``` r
theme_set(theme_light())

ggplot(A, aes(K, prob, color = as_factor(valid) ) ) +
  geom_point() +
  geom_hline(aes(yintercept = 0.1)) +
  geom_text( aes(label = ifelse(
      K == 32,
      paste0( "(", K, ",", " ", round(prob, 3), ")" ),
      ""
  ), hjust=1, vjust=1)) +    
  labs(
    x = "K (sample size)",
    y = "Probability of finding 0 defects"
  )
```

![](Module_5_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

Question 2
----------

Now suppose that the manufacturer decides to accept the shipment if
there is at most one defective part in the sample. How large does $ K $
have to be to ensure that the probability that the manufacturer accepts
an unacceptable shipment is less than 0.1? As above, a shipment is
unacceptable if there are more than 5 defective parts.

### Answer
