# Statistical tests and experiment design

## Simple coin example and p-value
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_1.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)
P-value is the total probability to observe same likely or more rare outcomes under assumption of no effects (null hypothesis). 

Figure 1 illustrates what is a p-value of observing 13 heads out of 20 coin tosses assuming coin is fair (our null hypothesis)?

## Significance level and type I error
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_2.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)
P-values of observations when there is no effect (null hypothesis is correct) behave as random variable
uniformly distributed between 0 and 1 (true for continious observation, and assymptotically true for discrete observations with 
large number of possible outcomes). Figure above illustrates distribution of 1000 p-values obtained in independent coin flip trials. 
Each trial is 1000 fair coin flips. 

Significance level (vertical line) is the cutt-off theshold blow which we consider results highly unlikely under null 
hypothesis and reject it. It also means that for some observations we will reject null hypothesis even if 
it was correct (and results are simply due to random chance). For observations from red bin on the histogram
above we will wrongly reject null hypothesis even if it was correct (for all 1000 trials we used fair coin). 
This type of mistate called type I error.

## Minimal Detectable Effect (MDE) and type II error
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_3.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)
Illustration for statistical test to identify if coin is fair or not. We start from selecting 
how sensitive we want to be and how different from 0.5 should be probability of heads to consider
coin biased. In other words we select minimal detectable effect (MDE) for the test. In the example 
above it is 20%. Next we plot expected probability distributions for fair coin and for biased (at
minimal detectable level). We select a significance level (red area on the top graph), which gives
us range for the observations (vertical lines) to reject or accept null hypothesis (coin is fair)

Notice, that some observations when null hypothesis is accepted can be result of the distribution
for biased coin and we will falsly conclude that biased coin is fair. This is type II error. 
Total probability of such error is blue area under the curve. 

## Power of the experiment, False Discovery Rate
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_4.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)
Results of applying statistical test above to test fairness of 1000 coins (we know that 
500 of them are fair and 500 of them are biased). Only in 62% cases we correctly concluded
that actually biased coin is biased. This value is called power of the test. from all 310 + 56 = 366 
identified biased coins only 310 were actually biased. This fraction 85% is called false discovery rate.

If we want to increase the power of the test given significance level and selected minimal detectable
effect we need to obtain more data.


[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_5.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)

It’s very important to understand that getting statistically insignificant results doesn’t
mean that we don’t have an effect, or in other words it doesn’t proof our null hypothesis.
We might simply have not enough data to reject the null hypothesis, which can be very likely
if the expected effect is small.

## Problem with calculating p-value as you go 
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_6.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)

We are testing 1000 coins for bias/fairness but this time we check significance "as we go", calculating p-value after each flip (data in red). 
This approach drammatically increases type I error rate as well as false discovery rate.

## Design of experiment
[![figure 1](https://github.com/tokedo/stat-dojo/blob/master/design_of_experiment_basics/figures/figure_7.png)](https://github.com/tokedo/stat-dojo/tree/master/design_of_experiment_basics)
For any statistical test we can calculate any of four values from three other values. For example, during
 the design of A/B tests each experiment typically start from questions:
1) how small effects we want to be able reliably to detect? (this will give us minimal detectable effect)  
2) what should be the chance that we will implement in production the change that actually has no effect? This is significance level 𝛂 or type I error rate.  
3) what should be the chance that we will not detect actually useful change? This is parameter 𝛃 or type II error rate.  

Having these three values we can calculate required number of observations for the test. 
Make sure to use statistical test appropriate for the metrics you are measuring.
 