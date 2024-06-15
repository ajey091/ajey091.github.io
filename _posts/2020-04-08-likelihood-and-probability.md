---
title: "Likelihood and Probability"
date: "2020-04-08"
categories: 
  - "python3"
  - "sampling"
  - "statistics"
tags: 
  - "likelihood"
  - "math"
  - "probability"
  - "python"
---

The difference between the concepts of Likelihood and Probability tends to subtle, at least as a beginner. As always the goal here is to provide some clarification from a mathematical, intuitive standpoint and then write some code in Python to get our feet wet.

Probability is a numerical description of how likely an event is to occur. In probability theory, the probability of an event is usually denoted by the symbol \\( \theta \\). If we denote the observed outcomes by \\( O \\), then we are interested in finding the quantity $P(O|\theta)$. This is the probability of the observation given the initial probabilities of the individual events. For example, if we flip a **fair** coin 10 times, the probability of \\( O \\) being 5 heads and 5 tails is calculated as follows:

\\[ \binom{10}{5} \left(\frac{1}{2}\right)^5 \left(\frac{1}{2}\right)^5 = 0.246 \\]

But, typically, in real world processes, we do not know the probabilities \( \theta \) _a priori_. In such cases, we only have access to a sample of data \( O \) and we are interested in finding the probabilities. The process of finding the probabilities of the individual processes, given an observation is called Likelihood. Here, we are computing the quantity \( L(\theta|O) \). Likelihood becomes a very important quantity in statistics where sampling data is the norm.

When we have sampled a large enough dataset, we can create a likelihood function in terms of the unknown quantity $latex \\theta$. Then, we can invoke the very popular **Maximum Likelihood Estimation** method to compute the value of $latex \\theta$ which (literally) maximizes the likelihood of the given observation. In general, it is more convenient (numerically and computationally) to minimize the $latex log(likelihood)$ function than the likelihood itself. This works out since log of any function is strictly increasing, and hence the function and its log will have the same maximum values. We will write some code for a simple process and hopefully that should reinforce the above concepts.

Let's say we have a sample of data which form the output of a **biased** coin. We will create a Bernoulli process to produce the outputs of the said biased coin, sample some data from the process and find the probability of H/T.

\[gist https://gist.github.com/ajey091/2f7a3afc39948d2b2261c5939506f782\]

`[0 0 1 0 0 1 0 1 1 0 0 0 0 0 0 1 0 0 0 0 1 1 0 0 0 0 0 0 1 0 0 0 1 0 0 1 0 1 1 0 0 0 0 0 0 1 0 0 0 1 1 0 0 0 0 0 0 1 1 0 0 0 0 0 0 1 0 0 1 1 0 0 0 0 1 0 0 1 0 0 1 1 1 0 0 1 0 0 0 0 0 0 1 0 0 0 0 1 0 0]`

If we define the probability of H as $latex \\theta$, we have the conditional probability

$latex L(\\theta|O) = \\theta^{p}\*(1-\\theta)^{n-p}$

In the above expression, $latex n$ and $latex p$ are the total number of observations and frequency of H, respectively. Now, we can evaluate $latex L$ as a function of $latex \\theta$ and find the value of $latex \\theta$ that maximizes $latex L$.

\[gist https://gist.github.com/ajey091/28d8668e39cfefe3c2b55803d442185a\]

![Likelihood1.png](/assets/images/likelihood1.png)

We can see from the plot that $latex L$ is maximum at a value close to 0.3. We can differentiate $latex L$ to find its maximum. Or we can just use invoke the `scipy.optimize` function to find the maximum of the likelihood function.

\[gist https://gist.github.com/ajey091/678470772865758c09fb2ba1c8dcbb15\]

`Optimization terminated successfully. Current function value: -0.000000 Iterations: 21 Function evaluations: 42 The likelihood function is maximum at [0.28]`

As I mentioned earlier, it is usually easier to minimize the $latex log(likelihood)$ function since they have the same $latex \\theta$ value at which the maximum occurs.

$latex log(L) = p\*log(\\theta) + (n-p)\*log(1-\\theta)$

We will repeat the above process to find the value of $latex \\theta$ which maximizes $latex log(L)$.

\[gist https://gist.github.com/ajey091/c670f7275484c63135aaec1679850bfe\]

![Likelihood2.png](/assets/images/likelihood2.png)

`Optimization terminated successfully. Current function value: 59.295332 Iterations: 21 Function evaluations: 42 The likelihood function is maximum at [0.28]`

As expected, we find the maximum value at the same value of $latex \\theta$.

## Sampling

Now, because the Bernouilli process that we are using is a random process, the outcomes are different each time. To overcome the possible errors due to randomness, we will sample n values a large number of times (1000). Then using the concept of Central Limit Theorem, we will compute the mean, standard deviation, confidence interval and margin of error in the distribution of $latex \\theta$.

\[gist https://gist.github.com/ajey091/3b4e9b5e94f6e0c0c94868e184d12255\]

![Likelihood3.png](/assets/images/likelihood3.png)

We see a nice normal distribution of the $latex \\theta$ values resulting from sampling data a bunch of times.

\[gist https://gist.github.com/ajey091/9884c4b08e1fc6376e7611c0c8994fdd\]

`mean of $latex \theta$ = 0.2992 Standard error of $latex \theta$ = 0.015 95% Confidence interval of $latex \theta$ = [0.21 0.38025]`

## Margin of error

While we already covered mean, standard error and confidence intervals in the last post, the concept of margin of error still requires some attention. Margin of error is another statistic that gives a measure of the random sampling error. Evidently, it has an inverse relationship with the sample size, which is rather intuitive.

Margin of error : $latex MOE = z \* \\frac{\\sigma}{\\sqrt{n}}$

where, $latex z$ is the z-statistic for the 95% confidence level, and $latex \\sigma$ is the standard deviation in the sample. Note that $latex MOE \\propto \\frac{1}{\\sqrt{n}}$.

<script src="https://gist.github.com/ajey091/51bd13b54228e6e0a58ee74c6dfedd89.js"></script>

`Z-score for 95% confidence interval = 1.960 Margin of error=0.009`
