---
title: "Sampling, resampling and hypothesis testing"
date: "2020-04-06"
categories: 
  - "python3"
  - "sampling"
  - "statistics"
tags: 
  - "bootstrapping"
  - "hypothesis-testing"
  - "python"
---

Continuing on the list of posts on statistics and quantitative analysis, this is a compilation of some routines for statistical analyses in Python. This work will be done using scipy.stats and numpy libraries. These codes are inspired by Allen Downey's Think Stats [book](http://greenteapress.com/thinkstats2/thinkstats2.pdf) and [lectures](https://www.youtube.com/watch?v=He9MCbs1wgE).

Typically, in real life statistical applications, we do not have access to the dataset from the entire population. Instead, what we have is a small subset of the population, also called a sample.

<script src="https://gist.github.com/ajey091/a6e8cd334daaa03a4bfa9a070d0d39f8.js"></script>

## Drawing samples from a normal distribution

<script src="https://gist.github.com/ajey091/356a0f7e01dac119734098b9634f78c0.js"></script>

We will first create an arbitrary normal distribution. This distribution is a representation of the male heights in the United States.

<script src="https://gist.github.com/ajey091/3453fec63655ae90fc1256d676751de4.js"></script>

![stats1.png](/assets/images/stats1.png)

Now, we would like to draw/sample some values from the distribution.

<script src="https://gist.github.com/ajey091/fb4ddc91848d05335b5c3c804b3b7a61.js"></script>

![stats2.png](/assets/images/stats2.png)

As long as our sample size is large enough, the sampled distribution resembles that of the original population distribution.

## Resampling methods - Bootstrapping

We had the convenience of having access to the actual distribution of the data and its mean, standard deviation. This data was sourced from a large database of heights of US men (~300000 samples).

But typically, we do not have access to the distribution. Estimates of central tendency (mean) and dispersion (standard deviation) in those cases are not readily available. In such cases when we just have a reasonably sized dataset (let's say 1000 data points), we have to resort to resampling methods, the most common one being Bootstrapping. In bootstrapping, we resample from the same dataset WITH REPLACEMENT and compute our estimates. Thanks to Central Limit Theorem (CLT), we end up with a normal distribution of the estimate (as long as we sample enough times). CLT states that when independent random variables are added, their normalized sum tends toward a normal distribution. The place where CLT shines is that the initial distribution does not have to be normal for the estimates to be normally distributed. In fact, we don't even need to know the type of distribution of the original dataset. But, typically, the farther away from a normal distribution the data is (think pareto distribution), more times we have to resample.

We will first obtain an estimate for mean and std for the normally distributed data, then for a random distribution.

The plan is to take a sample from the population (akin to what we would have in real life) and estimate some sample statistics using Bootstrapping.

<script src="https://gist.github.com/ajey091/e91935aa5c7afadb5689be6c455bdd24.js"></script>

```
Estimated statistic = 177.937
Standard error = 0.798
95% confidence interval = [176.33743211 179.39532095]
```

![stats3.png](/assets/images/stats3.png)

As expected, the standard error should decrease with increase in the number of sampled data. But it is pretty much immune to the number of iterations. Also, evidently, the confidence interval shrinks in size as we increase the size of the sampled data.

<script src="https://gist.github.com/ajey091/6acaa1e808763b00dc844c41da50a852.js"></script>

![stats4.png](/assets/images/stats4.png)

<script src="https://gist.github.com/ajey091/debf08b3b975c5db6fc4234cf8f0ba52.js"></script>

![stats5.png](/assets/images/stats5.png)

The remarkable thing about CLT is that the above method can be used to estimate any quantity, not just the mean. Median, standard deviation, coefficient of determination, you name it. This procedure simply involves changing the calculated statistic above. We will repeat the process for estimating the median.

<script src="https://gist.github.com/ajey091/3e4fbd12a67ef8419663bd4b43c71878.js"></script>

```
Estimated statistic = 177.437
Standard error = 0.973
95% confidence interval = [175.68731829 179.51358241]
```

![stats6.png](/assets/images/stats6.png)

## Some comments

It is important to understand what the confidence interval actually represents.

What the confidence level DOES NOT represent: The confidence level is not a suggestion about whether the estimated parameter lies within the interval or not. The confidence interval provides no indication about whether the estimate lies within the limit or not. Whether or not the estimate lies within the confidence interval is not a matter up for probability.

What the confidence level DOES mean: by definition, if we were to conduct an infinite number of experiments to find the value of the estimate, in 95% of the cases, the confidence interval will contain the true population parameter.

## Hypothesis testing

For hypothesis testing, we will make an initial hypothesis and test it against the null hypothesis.

To do this, we will use some data that I got from the NSFG - National Survey of Family Growth website. We are testing the hypothesis that first born babies are different than other babies. We have to choose a statistic to compare weights and we will use mean to accomplish this. Essentially, we are testing if the difference between the two datasets could be caused by random chance.

<script src="https://gist.github.com/ajey091/49527999991372f8230d9b009a48fb51.js"></script>

```
Mean weight of first born babies=7.201 lb
Mean weight of other born babies=7.326 lb
```

We will randomize the two datasets and then compare the difference in means between the two datasets over a 1000 iterations. We will then calculate the probability of the difference between the two groups being as big as the actual difference.

<script src="https://gist.github.com/ajey091/1f897cc44ed2077aa3b3fb898af79a68.js"></script>

```
p-value = 0.0000
```

The p-value we obtained is < 1e-4 which suggests that the observed difference between the first born baby weights and other baby weights is highly unlikely to be caused by chance alone.
