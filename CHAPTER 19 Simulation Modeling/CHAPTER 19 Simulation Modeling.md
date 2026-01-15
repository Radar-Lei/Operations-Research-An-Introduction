## CHAPTER 19 Simulation Modeling

### 19.1 MONTE CARLO SIMULATION

A forerunner to present-day simulation is the Monte Carlo experiment, a modeling scheme that estimates stochastic or deterministic parameters based on random sampling. Examples of Monte Carlo applications include evaluation of multiple integrals, estimation of the constant $\pi \left( { \cong  {3.14159}}\right)$ , and matrix inversion.

This section uses an example to demonstrate the Monte Carlo technique. The objective of the example is to emphasize the statistical nature of simulation.

## Example 19.1-1

We will use Monte Carlo sampling to estimate the area of the following circle:

$$
{\left( x - 1\right) }^{2} + {\left( y - 2\right) }^{2} = {25}
$$

The radius of the circle is $r = 5\mathrm{\;{cm}}$ , and its center is $\left( {x, y}\right)  = \left( {1,2}\right)$ .

The procedure for estimating the area requires enclosing the circle tightly in a square whose side equals the diameter of the circle, as shown in Figure 19.1. The corner points are determined from the geometry of the square.

The estimation of the area of the circle is based on a sampling experiment that gives equal chance to selecting any point in the square. If $m$ out of $n$ sampled points fall within the circle, then

$$
\left( \begin{matrix} \text{ Approximate } \\  \text{ area of the circle } \end{matrix}\right)  = \frac{m}{n}\left( \begin{matrix} \text{ Area of } \\  \text{ the square } \end{matrix}\right)  = \frac{m}{n}\left( {{10} \times  {10}}\right)
$$

To ensure that all the points in the square are equally probable, the coordinates $x$ and $y$ of a point in the square are represented by the following uniform distributions:

$$
{f}_{1}\left( x\right)  = \frac{1}{10}, - 4 \leq  x \leq  6
$$

$$
{f}_{2}\left( y\right)  = \frac{1}{10}, - 3 \leq  y \leq  7
$$

![bo_d56m5ljef24c73bhe69g_1_511_197_441_439_0.jpg](bo_d56m5ljef24c73bhe69g_1_511_197_441_439_0.jpg)

FIGURE 19.1

Monte Carlo estimation of the area of a circle

TABLE 19.1 A Short List of 0-1 Random Numbers

<table><tr><td>.0589</td><td>.3529</td><td>.5869</td><td>.3455</td><td>.7900</td><td>.6307</td></tr><tr><td>.6733</td><td>.3646</td><td>.1281</td><td>.4871</td><td>.7698</td><td>.2346</td></tr><tr><td>.4799</td><td>.7676</td><td>.2867</td><td>.8111</td><td>.2871</td><td>.4220</td></tr><tr><td>.9486</td><td>.8931</td><td>.8216</td><td>.8912</td><td>.9534</td><td>.6991</td></tr><tr><td>.6139</td><td>.3919</td><td>.8261</td><td>.4291</td><td>.1394</td><td>.9745</td></tr><tr><td>.5933</td><td>.7876</td><td>.3866</td><td>.2302</td><td>.9025</td><td>.3428</td></tr><tr><td>.9341</td><td>.5199</td><td>.7125</td><td>.5954</td><td>.1605</td><td>.6037</td></tr><tr><td>.1782</td><td>.6358</td><td>.2108</td><td>.5423</td><td>.3567</td><td>.2569</td></tr><tr><td>.3473</td><td>.7472</td><td>.3575</td><td>.4208</td><td>.3070</td><td>.0546</td></tr><tr><td>.5644</td><td>.8954</td><td>.2926</td><td>.6975</td><td>.5513</td><td>.0305</td></tr></table>

The determination of a sample $\left( {x, y}\right)$ is based on the use of independent 0-1 random numbers. Table 19.1 lists a sample of such numbers which we will use in the examples in this chapter. For the purpose of general simulation, special arithmetic operations are used to generate (pseudo) 0-1 random numbers, as will be shown in Section 19.4.

A pair of 0-1 random numbers, ${R}_{1}$ and ${R}_{2}$ , can be used to generate a random point $\left( {x, y}\right)$ in the square by using the following formulas:

$$
x =  - 4 + \left\lbrack  {6 - \left( {-4}\right) }\right\rbrack  {R}_{1} =  - 4 + {10}{R}_{1}
$$

$$
y =  - 3 + \left\lbrack  {7 - \left( {-3}\right) }\right\rbrack  {R}_{2} =  - 3 + {10}{R}_{2}
$$

To demonstrate the application of the procedure, consider ${R}_{1} = {.0589}$ and ${R}_{2} = {.6733}$ .

$$
x =  - 4 + {10}{R}_{1} =  - 4 + {10} \times  {.0589} =  - {3.411}
$$

$$
y =  - 3 + {10}{R}_{2} =  - 3 + {10} \times  {.6733} = {3.733}
$$

This point falls inside the circle because

$$
{\left( -{3.411} - 1\right) }^{2} + {\left( {3.733} - 2\right) }^{2} = {22.46} < {25}
$$

Remarks. The accuracy of the area estimate can be enhanced by using procedures from ordinary statistical experiments:

1. Increase the sample size, $n$ .

2. Use replications, $N$ .

The discussion in Example 19.1-1 poses two questions regarding the simulation experiment:

1. How large should the sample size be?

2. How many replications are needed?

There are some formulas in statistical theory for determining $n$ and $N$ , and they depend on the nature of the simulation experiment as well as the desired confidence level. However, as in any statistical experiment, the golden rule is that higher values of $n$ and $N$ mean more accurate simulation results. In the end, the sample size will depend on the cost associated with conducting the simulation experiment. Generally speaking, however, a selected sample size is considered "adequate" if it produces a relatively "small" standard deviation.

It is necessary to express the results as a confidence interval to account for the random variation in the output of the experiment. Letting $\bar{A}$ and $s$ be the mean and variance of $N$ replications, then, given a confidence level $\alpha$ , the confidence interval for the true area $A$ is

$$
\bar{A} - \frac{s}{\sqrt{N}}{t}_{\frac{\alpha }{2}, N - 1} \leq  A \leq  \bar{A} + \frac{s}{\sqrt{N}}{t}_{\frac{\alpha }{2}, N - 1}
$$

The parameter ${t}_{\frac{\alpha }{2}, N - 1}$ is determined from the $t$ -distribution tables given a confidence level $\alpha$ and $N - 1$ degrees of freedom (see the $t$ -table in Appendix A or use excelStatTables.xls). Note that $N$ equals the number of replications, which is distinct from the sample size $n$ .

## Excel Moment

The computations associated with each sample in Example 19.1-1 are voluminous. Excel template excelCircle.xls (with VBA macros) is used to test the effect of sample size and number of replications on the accuracy of the area estimate. The input data include the circle radius, $r$ ; and its center $\left( {{cx},{cy}}\right)$ ; sample size, $n$ ; number of replications, $N$ ; and the confidence level, $\alpha$ . The entry Steps in cell D4 allows executing several samples in the same run. For example, if $n = {30},{000}$ and Steps $= 3$ , the template will automatically produce output for $n = {30},{000},{60},{000}$ , and 90,000. New estimates are realized each time the command button Press to Execute Monte Carlo is clicked because Excel refreshes the seed of the random number generator.

Figure 19.2 summarizes the results for 5 replications and sample sizes of 30,000,60,000, and 90,000 . The exact area is ${78.54}{\mathrm{\;{cm}}}^{2}$ , and the Monte Carlo results show that the mean estimated areas for the three sample sizes are slightly different.

Figure 16.2 gives the 95% confidence intervals for each $n$ . For example, the confidence interval 78.452 $\leq  A \leq  {78.68}$ corresponds to $n = {90},{000}$ , with $N = 5,\bar{A} = {78.566}{\mathrm{\;{cm}}}^{2}$ , and $s = {.092}\mathrm{\;{cm}}$ , and ${t}_{{.025},4} = {2.776}$ . In general, to realize reasonable accuracy in the estimation of the confidence interval, the value of $N$ should be at least 5 .

## Aha! Moment. Retirement Planning Online: The Monte Carlo Way!

In days past, a financial advisor was a real person with whom an investor could meet face to face to discuss financial plans for retirements. Though real-person advising continues to thrive (particularly for large investors), the trend now, especially for small investors, is to seek financial advice online. Available software estimates post-retirement cash flow based on historical time-based financial information about stocks and bonds and the like, together with the annual contributions to the retirement fund, anticipated retirement date, and other pertinent data. But the most important element of the model is how it accounts for the volatility (ups and downs) of the stock market based on foreseen and unforeseen events. This is a complex stochastic process that describes the ever-present uncertainty in the market behavior over time. In practice, almost all available retirement calculators translate market volatility as simple percentage estimates that reflect the degree of uncertainty in the market. These percentages are the basis for the use of random (or Monte Carlo) sampling to simulate the stock market behavior. Practically all financial brokers use some version of a (Monte Carlo-based) data-driven black box simulator. But in the end, the output, as in any simulation model, is simply the result of a peculiar statistical experiment (see Section 19.6), and is thus bound by the limitations of the design and execution of such experiments. As such, the quality of proposed advices is dependent on the robustness of the model and the accuracy of the input data driving the model.

<table><tr><td>4</td><td>B</td><td>C</td><td>D</td><td>E</td></tr><tr><td>1</td><td colspan="4">Monte Carlo Estimation of the Area of a Circle</td></tr><tr><td>2</td><td colspan="4">Input data</td></tr><tr><td>3</td><td>Nbr. Replications, N =</td><td>5</td><td>$\alpha  =$</td><td>0.025</td></tr><tr><td>4</td><td>Sample size, n =</td><td>30,000</td><td>Steps =</td><td>3</td></tr><tr><td>5</td><td>Radius, r =</td><td>5</td><td></td><td></td></tr><tr><td>6</td><td>Center, cx =</td><td>1</td><td></td><td></td></tr><tr><td>7</td><td>Center, cy =</td><td>2</td><td></td><td></td></tr><tr><td>8</td><td colspan="4">Output results</td></tr><tr><td>9</td><td>Exact area =</td><td>78.540</td><td></td><td></td></tr><tr><td>10</td><td colspan="2">Press to Execute Monte Carlo</td><td></td><td></td></tr><tr><td>11</td><td colspan="2">Monte Carlo Calculations:</td><td></td><td></td></tr><tr><td>12</td><td></td><td>n=30000</td><td>n=60000</td><td>n=90000</td></tr><tr><td>13</td><td>Replication 1</td><td>78.590</td><td>78.543</td><td>78.536</td></tr><tr><td>14</td><td>Replication 2</td><td>78.447</td><td>78.695</td><td>78.731</td></tr><tr><td>15</td><td>Replication 3</td><td>78.747</td><td>78.648</td><td>78.534</td></tr><tr><td>16</td><td>Replication 4</td><td>78.363</td><td>78.500</td><td>78.512</td></tr><tr><td>17</td><td>Replication 5</td><td>78.540</td><td>78.420</td><td>78.517</td></tr><tr><td colspan="5">18</td></tr><tr><td>19</td><td>Mean =</td><td>78.537</td><td>78.561</td><td>78.566</td></tr><tr><td>20</td><td>Std. Deviation =</td><td>0.142</td><td>0.118</td><td>0.092</td></tr><tr><td colspan="5">21</td></tr><tr><td>22</td><td>95% lower conf. limit =</td><td>78.361</td><td>78.415</td><td>78.452</td></tr><tr><td>23</td><td>95% upper conf. limit =</td><td>78.714</td><td>78.708</td><td>78.680</td></tr></table>

FIGURE 19.2

Excel output of Monte Carlo estimation of the area of a circle (file excelCircle.xls)

### 19.2 TYPES OF SIMULATION

The execution of present-day simulation is based on the idea of sampling used with the Monte Carlo method. It differs in that it deals with the study of the behavior of real systems as a function of time. Two distinct types of simulation models exist.

1. Continuous models deal with systems whose behavior changes continuously with time. These models usually use difference-differential equations to describe the interactions among the different elements of the system. A typical example deals with the study of world population dynamics.

2. Discrete models deal primarily with the study of waiting lines, with the objective of determining such measures as the average waiting time and length of the queue. These measures change only when a customer enters or leaves the system. The instants at which changes take place occur at specific discrete points in time (arrivals and departure events), giving rise to the name discrete event simulation.

This chapter presents the basics of discrete event simulation, including a description of the components of a simulation model, collection of simulation statistics, and the statistical aspect of the simulation experiment. The chapter also emphasizes the role of the computer and simulation languages in the execution of simulation models.

### 19.3 ELEMENTS OF DISCRETE EVENT SIMULATION

The ultimate goal of simulation is to estimate some desirable measures of performance that describe the behavior of the simulated system. For example, in a service facility, the associated measures of performance can include the average waiting time until a customer is served, the average length of the queue, and the average utilization of the service facility. This section shows how the statistics of the simulated system are collected based on the concept of events.

#### 19.3.1 Generic Definition of Events

All discrete event simulations describe, directly or indirectly, queuing situations in which customers arrive (for service), wait in a queue (if necessary), and then receive service before leaving the service facility. As such, any discrete event simulation, regardless of the complexity of the system it describes, reduces to dealing with two basic events: arrivals and departures. The following example illustrates the use of the arrival and departure events to describe a system consisting of distinct queues.

## Example 19.3-1

---

Metalco Jobshop receives two types of jobs: regular and rush. All jobs are processed on two

consecutive machines with ample buffer areas. Rush jobs always assume nonpreemptive priority

over regular jobs.

			This situation consists of two tandem queues representing the two machines. At first, one

may be inclined to identify the events of the situation as

				A11: A regular job arrives at machine 1.

				A21: A rush job arrives at machine 1.

---

![bo_d56m5ljef24c73bhe69g_5_393_197_1086_169_0.jpg](bo_d56m5ljef24c73bhe69g_5_393_197_1086_169_0.jpg)

FIGURE 19.3

Example of the occurrence of simulation events on the timescale

D11: A regular job departs machine 1.

D21: A rush job departs machine 1.

A12: A regular job arrives at machine 2.

A22: A rush job arrives at machine 2.

D12: A regular job departs machine 2.

D22: A rush job departs machine 2.

In reality, there are only two events: an arrival of a (new) job at the shop and a departure of a (completed) job from a machine. First notice that events ${D11}$ and ${A12}$ are actually one and the same. The same applies to D21 and A22. Next, in discrete simulation we can use one event (arrival or departure) for both types of jobs and simply "tag" the event with an attribute that identifies the job type as either regular or rush. (We can think of the attribute in this case as a personal identification descriptor, and indeed it is.) Given this reasoning, the events of the model reduce to (1) an arrival $A$ (at the shop) and (2) a departure $D$ (from a machine). The actions associated with the arrival event depend on the type of arriving job (rush or regular) and the availability of a machine. Similarly, the processing of the departure event will depend on the machine and the status of waiting jobs.

Having defined the basic events of a simulation model, we show how the model is executed. Figure 19.3 gives a schematic representation of typical occurrences of events on the simulation timescale. After all the actions associated with a current event have been performed, the simulation advances by "jumping" to the next chronological event. In essence, the execution of the simulation occurs at the instants at which the events occur.

How does the simulation determine the occurrence time of the events? The arrival events are separated by the interarrival time (the interval between successive arrivals), and the departure events are a function of the service time in the facility. These times may be deterministic (e.g., a train arriving at a station every 5 minutes) or probabilistic (e.g., the random arrival of customers at a bank). If the time between events is deterministic, the determination of their occurrence times is straightforward. If it is probabilistic, we use a special procedure to sample from the corresponding probability distribution. This point is discussed in the next section.

#### 19.3.2 Sampling from Probability Distributions

Randomness in simulation arises when the interval, $t$ , between successive events is probabilistic. This section presents three methods for generating successive random samples $\left( {t = {t}_{1},{t}_{2},\ldots }\right)$ from a probability distribution $f\left( t\right)$ :

1. Inverse method.

2. Convolution method.

3. Acceptance-rejection method.

![bo_d56m5ljef24c73bhe69g_6_451_197_1059_426_0.jpg](bo_d56m5ljef24c73bhe69g_6_451_197_1059_426_0.jpg)

FIGURE 19.4

Sampling from a probability distribution by the inverse method

The inverse method is particularly suited for analytically tractable probability density functions, such as the exponential and the uniform. The remaining two methods deal with more complex cases, such as the normal and the Poisson. All three methods are rooted in the use of independent and identically distributed uniform 0-1 random numbers.

This section will present the first two methods only. Details of the acceptance-rejection method can be found in Law (2007).

Inverse method. To obtain a random sample $x$ from the (continuous or discrete) probability density function $f\left( x\right)$ , the inverse method first determines a closed-form expression of the cumulative density function $F\left( x\right)  = P\{ y \leq  x\}$ , where $0 \leq  F\left( x\right)  \leq  1$ , for all defined values of $y$ . It can be proved that the random variable $z = F\left( x\right)$ is uniformly distributed in the interval $0 \leq  z \leq  1$ . Based on this result, a random sample from $f\left( x\right)$ is determined using the following steps $\left( {{F}^{-1}\text{ is the inverse of }F}\right.$ ):

Step 1. Generate a 0-1 random number, $R$ .

Step 2. Compute the desired sample $x = {F}^{-1}\left( R\right)$ .

Figure 19.4 illustrates the procedures for both a continuous and a discrete random distribution.

## Example 19.3-2 (Exponential Distribution)

---

The exponential probability density function $f\left( t\right)  = \lambda {e}^{-{\lambda t}}, t > 0$ represents the interarrival

time $t$ at a facility with a mean value of $\frac{1}{\lambda }$ . The cumulative density function is

$$
F\left( t\right)  = {\int }_{0}^{t}\lambda {e}^{-{\lambda x}}{dx} = 1 - {e}^{-{\lambda t}}, t > 0
$$

Setting $R = F\left( t\right)$ , we can solve for $t$ as

$$
t =  - \left( \frac{1}{\lambda }\right) \ln \left( {1 - R}\right)
$$

---

For example, for $\lambda  = 4$ customers per hour and $R = {.9}$ , the time period until the next arrival occurs is

$$
{t}_{1} =  - \left( \frac{1}{4}\right) \ln \left( {1 - {.9}}\right)  = {.577}\text{ hour } = {34.5}\text{ minutes }
$$

Note that $\ln \left( {1 - R}\right)$ may be replaced with $\ln \left( R\right)$ because $1 - R$ is the complement of $R$ .

Convolution method. The basic idea of the convolution method is to express the desired sample as the statistical sum of other easy-to-sample random variables. Typical among these distributions are the Erlang and the Poisson, whose samples can be obtained from the exponential distribution samples.

## Example 19.3-3 (Erlang Distribution)

The $m$ -Erlang random variable is defined as the statistical sum (convolutions) of $m$ independent and identically distributed exponential random variables. Let $y$ represent the $m$ -Erlang random variable; then

$$
y = {y}_{1} + {y}_{2} + \cdots  + {y}_{m}
$$

The random variables ${y}_{i}, i = 1,2,\ldots , m$ , are independent and identically distributed exponentials with the following probability density function:

$$
f\left( {y}_{i}\right)  = \lambda {e}^{-\lambda {y}_{i}},{y}_{i} > 0, i = 1,2,\ldots , m
$$

From Example 19.3-2, a sample from the $i$ th exponential distribution is computed as

$$
{y}_{i} =  - \left( \frac{1}{\lambda }\right) \ln \left( {R}_{i}\right) , i = 1,2,\ldots , m
$$

Thus, the $m$ -Erlang sample is computed as

$$
y =  - \left( \frac{1}{\lambda }\right) \left\{  {\ln \left( {R}_{1}\right)  + \ln \left( {R}_{2}\right)  + \cdots  + \ln \left( {R}_{m}\right) }\right\}
$$

$$
=  - \left( \frac{1}{\lambda }\right) \ln \left( {\mathop{\prod }\limits_{{i = 1}}^{m}{R}_{i}}\right)
$$

To illustrate the use of the formula, suppose that $m = 3$ and $\lambda  = 4$ events per hour. The first 3 random numbers in column 1 of Table 19.1 yield ${R}_{1}{R}_{2}{R}_{3} = \left( {.0589}\right) \left( {.6733}\right) \left( {.4799}\right)  = {.0190}$ , which yields

$$
y =  - \left( \frac{1}{4}\right) \ln \left( {.019}\right)  = {.991}\mathrm{{hr}}
$$

## Example 19.3-4 (Poisson Distribution)

Section 18.4.1 shows that if the distribution of the time between the occurrences of successive events is exponential, then the distribution of the number of events per unit time is Poisson, and vice versa. We use this relationship to sample the Poisson distribution.

Assume that mean of the Poisson distribution is $\lambda$ events per unit time. It follows that the time between events is exponential with mean $\frac{1}{\lambda }$ time units. This means that a Poisson sample, $n$ , will occur during $t$ time units if, and only if,

Period till event $n$ occurs $\leq  t <$ Period till event $n + 1$ occurs

This condition translates to

$$
{t}_{1} + {t}_{2} + \cdots  + {t}_{n} \leq  t < {t}_{1} + {t}_{2} + \cdots  + {t}_{n + 1}, n > 0
$$

$$
0 \leq  t < {t}_{1}, n = 0
$$

The random variable ${t}_{i}, i = 1,2\ldots , n + 1$ , is a sample from the exponential distribution with mean $\frac{1}{\lambda }$ . From the result in Example 19.3-3, we have

$$
- \left( \frac{1}{\lambda }\right) \ln \left( {\mathop{\prod }\limits_{{i = 1}}^{n}{R}_{i}}\right)  \leq  t <  - \left( \frac{1}{\lambda }\right) \ln \left( {\mathop{\prod }\limits_{{i = 1}}^{{n + 1}}{R}_{i}}\right) , n > 0
$$

$$
0 \leq  t <  - \left( \frac{1}{\lambda }\right) \ln \left( {R}_{1}\right) , n = 0
$$

These expressions reduce to

$$
\mathop{\prod }\limits_{{i = 1}}^{n}{R}_{i} \geq  {e}^{-{\lambda t}} > \mathop{\prod }\limits_{{i = 1}}^{{n + 1}}{R}_{i}, n > 0
$$

$$
1 \geq  {e}^{-{\lambda t}} > {R}_{1}, n = 0
$$

To illustrate the implementation of the sampling process, suppose that $\lambda  = 4$ events per hour. To obtain a sample for a period $t = {.5}\mathrm{{hr}}$ , we first compute ${e}^{-{\lambda t}} = {.1353}$ . The random number ${R}_{1} = {.0589}$ is less than ${e}^{-{\lambda t}} = {.1353}$ . Hence, the corresponding sample is $n = 0$ .

## Example 19.3-5 (Normal Distribution)

The central limit theorem (see Section 14.4.4) states that the sum (convolution) of $n$ independent and identically distributed random variables becomes asymptotically normal as $n$ becomes sufficiently large. We use this result to generate samples from normal distribution with mean $\mu$ and standard deviation $\sigma$ .

Define

$$
x = {R}_{1} + {R}_{2} + \ldots  + {R}_{n}
$$

The random variable is asymptotically normal by the central limit theorem. Given that the uniform $\left( {0,1}\right)$ random number $R$ has a mean of $\frac{1}{2}$ and a variance of $\frac{1}{12}$ , it follows that the mean and variance of $x$ are $\frac{n}{2}$ and $\frac{n}{12}$ , respectively. Thus, a random sample, $y$ , from a normal distribution $N\left( {\mu ,\sigma }\right)$ , with mean $\mu$ and standard deviation $\sigma$ , can be computed from $x$ as

$$
y = \mu  + \sigma \left( \frac{x - \frac{n}{2}}{\sqrt{\frac{n}{12}}}\right)
$$

In practice, we take $n = {12}$ for convenience, which reduces the formula to

$$
y = \mu  + \sigma \left( {x - 6}\right)
$$

To illustrate the use of this method, suppose that we wish to generate a sample from $N\left( {{10},2}\right)$ (mean $\mu  = {10}$ and standard deviation $\sigma  = 2$ ). Taking the sum of the first 12 random numbers in columns 1 and 2 of Table 19.1, we get $x = {6.1094}$ . Thus, $y = {10} + \; 2\left( {{6.1094} - 6}\right)  = {10.2188}.$

Box-Muller normal sampling formula. The disadvantage of the preceding procedure is that it requires generating 12 random numbers per normal sample, which is computationally inefficient. A more efficient procedure calls for using the transformation

$$
x = \cos \left( {{2\pi }{R}_{2}}\right) \sqrt{-2\ln \left( {R}_{1}\right) }
$$

Box and Muller (1958) prove that $x$ is a standard $N\left( {0,1}\right)$ . Thus, $y = \mu  + {\sigma x}$ will produce a sample from $N\left( {\mu ,\sigma }\right)$ . The new procedure is more efficient because it requires two 0-1 random numbers only. Actually, this method is even more efficient than stated, because Box and Muller prove that the given formula produces another $N\left( {0,1}\right)$ sample if $\sin \left( {{2\pi }{R}_{2}}\right)$ replaces $\cos \left( {{2\pi }{R}_{2}}\right)$ .

To illustrate the implementation of the Box-Muller procedure to the normal distribution $N\left( {{10},2}\right)$ , the first two random numbers in column 1 of Table 19.1 yield the following $N\left( {0,1}\right)$ samples:

$$
{x}_{1} = \cos \left( {{2\pi } \times  {.6733}}\right) \sqrt{-2\ln \left( {.0589}\right) } \approx   - {1.103}
$$

$$
{x}_{2} = \sin \left( {{2\pi } \times  {.6733}}\right) \sqrt{-2\ln \left( {.0589}\right) } \approx   - {2.109}
$$

Thus, the corresponding $N\left( {{10},2}\right)$ samples are

$$
{y}_{1} = {10} + 2\left( {-{1.103}}\right)  = {7.794}
$$

$$
{y}_{2} = {10} + 2\left( {-{2.109}}\right)  = {5.782}
$$

### 19.4 GENERATION OF RANDOM NUMBERS

Uniform $\left( {0,1}\right)$ random numbers play a key role in sampling from distributions. True 0-1 random numbers can be generated by electronic devices only. However, because simulation models are executed on the computer, the use of electronic devices to generate random numbers is much too slow for that purpose. Additionally, electronic devices are activated by laws of chance, making it impossible to duplicate the same sequence of random numbers at will. This point is important because debugging, verification, and validation of the simulation model often require duplicating the random numbers sequence.

The only feasible way for generating 0-1 random numbers for use in simulation is based on arithmetic operations. Such numbers are not truly random because the entire sequence can be generated in advance. It is thus more appropriate to refer to them as pseudorandom numbers.

The most common arithmetic operation for generating $\left( {0,1}\right)$ random numbers is the multiplicative congruential method. Given the parameters ${u}_{0}, b, c$ , and $m$ , a pseudorandom number ${R}_{n}$ can be generated from the formulas:

$$
{u}_{n} = \left( {b{u}_{n - 1} + c}\right) {\;\operatorname{mod}\;\left( m\right) }, n = 1,2,\ldots
$$

$$
{R}_{n} = \frac{{u}_{n}}{m}, n = 1,2,\ldots
$$

The initial value ${u}_{0}$ is usually referred to as the seed of the generator.

Variations of the multiplicative congruential method that improve the quality of the generator can be found in Law (2007).

## Example 19.4-1

Generate three random numbers based on the multiplicative congruential method using $b = 9$ , $c = 5$ , and $m = {12}$ . The seed is ${u}_{0} = {11}$ .

$$
{u}_{1} = \left( {9 \times  {11} + 5}\right) {\;\operatorname{mod}\;{12}} = 8,{R}_{1} = \frac{8}{12} = {.6667}
$$

$$
{u}_{2} = \left( {9 \times  8 + 5}\right) {\;\operatorname{mod}\;{12}} = 5,{R}_{2} = \frac{5}{12} = {.4167}
$$

$$
{u}_{3} = \left( {9 \times  5 + 5}\right) {\;\operatorname{mod}\;{12}} = 2,{R}_{3} = \frac{2}{12} = {.1667}
$$

## Excel Moment

Excel template excelRN.xls implements the multiplicative congruential method. Figure 19.5 generates the sequence associated with the parameters of Example 19.4-1. Notice that the cycle length is exactly 4, after which the sequence repeats itself. The point to be made here is that the selected values of ${u}_{0}, b, c$ , and $m$ are critical in determining the (statistical) quality of the generator and its cycle length. Thus, "casual" implementation of the congruential formula is not recommended. Instead, one must use a reliable and tested generator. All commercial computer programs are equipped with dependable random number generators.

FIGURE 19.5

Excel random numbers output for the data of Example 19.4-1 (file excelRN.xls)

<table><tr><td>4</td><td>A</td><td>B</td></tr><tr><td>1</td><td colspan="2">Multiplicative Congruential Method</td></tr><tr><td>2</td><td colspan="2">Input data(B7<=1000)</td></tr><tr><td>3</td><td>b =</td><td>9</td></tr><tr><td>4</td><td>c =</td><td>5</td></tr><tr><td>5</td><td>u0 =</td><td>11</td></tr><tr><td>6</td><td>m =</td><td>12</td></tr><tr><td>7</td><td>How many numbers?</td><td>10</td></tr><tr><td>8</td><td colspan="2">Output results</td></tr><tr><td>9</td><td colspan="2">Press to Generate Sequence</td></tr><tr><td>10</td><td colspan="2">Generated random numbers:</td></tr><tr><td>11</td><td>1</td><td>0.66667</td></tr><tr><td>12</td><td>2</td><td>0.41667</td></tr><tr><td>13</td><td>3</td><td>0.16667</td></tr><tr><td>14</td><td>4</td><td>0.91667</td></tr><tr><td>15</td><td>5</td><td>0.66667</td></tr><tr><td>16</td><td>6</td><td>0.41667</td></tr><tr><td>17</td><td>7</td><td>0.16667</td></tr><tr><td>18</td><td>8</td><td>0.91667</td></tr><tr><td>19</td><td>9</td><td>0.66667</td></tr><tr><td>20</td><td>10</td><td>0.41667</td></tr></table>

### 19.5 MECHANICS OF DISCRETE SIMULATION

This section details how typical statistics are collected in a simulation model. The vehicle of explanation is a single-queue model. Section 19.5.1 uses a numeric example to detail the actions and computations that take place in a single-server queuing simulation model. Because of the tedious computations that typify the execution of a simulation model, Section 19.5.2 shows how the single-server model is modeled and executed using an Excel spreadsheet.

#### 19.5.1 Manual Simulation of a Single-Server Model

## Example 19.5-1

The interarrival time of customers at HairKare Barbershop is exponential with mean 15 minutes. The shop is operated by only one barber, and it takes between 10 and 15 minutes, uniformly distributed, to do a haircut. Customers are served on a first-in, first-out (FIFO) basis. The objective of the simulation is to compute the following measures of performance:

1. The average utilization of the shop.

2. The average number of waiting customers.

3. The average time a customer waits in queue.

In the remainder of this section, the barbershop situation in Example 19.5-1 is used to describe the logic of the simulation model, detailing the actions associated with the arrival and departure events. Concurrently, the presentation details how the simulation statistical data/observations are collected.

## Arrival Event

1. Generate and store chronologically the occurrence time of the next arrival event (= current simulation time + interarrival time).

2. If the facility (barber) is idle

a. Start service and declare the facility busy. Update the facility utilization statistics.

b. Generate and store chronologically the time of the departure event for the customer (= current simulation time + service time).

3. If the facility is busy, place the customer in the queue, and update the queue statistics.

## Departure Event

1. If the queue is empty, declare the facility idle. Update the facility utilization statistics.

2. If the queue is not empty

a. Select a customer from the queue, and place it in the facility. Update the facility utilization and queue statistics.

b. Generate and store chronologically the occurrence time of the departure event for the customer (= current simulation time + service time).

From the data of the problem, the interarrival time is exponential with mean 15 minutes, and the service time is uniform between 10 and 15 minutes. Letting $p$ and $q$ represent random samples of interarrival and service times, then, as explained in Section 19.3.2, we get

$$
p =  - {15}\ln \left( R\right) \text{ minutes, }0 \leq  R \leq  1
$$

$$
q = {10} + {5R}\text{ minutes, }\;0 \leq  R \leq  1
$$

For the purpose of this example, we use $R$ from Table 19.1, starting with column 1. We also use the symbol $T$ to represent the simulation clock time. We further assume that the first customer arrives at $T = 0$ and that the facility starts empty.

Because the simulation computations are typically voluminous, the simulation is limited to the first 5 arrivals only. The example is designed to cover all possible situations that could arise in the course of the simulation. Later in Section 19.5.2, we introduce the template excelSingleServer.xls that allows experimenting with the model without the need to carry out the computations manually.

Arrival of customer 1 at $T = 0$ . Generate the arrival of customer 2 at

$$
T = 0 + {p}_{1} = 0 + \left\lbrack  {-{15}\ln \left( {.0589}\right) }\right\rbrack   = {42.48}\text{ minutes }
$$

Because the facility is idle at $T = 0$ , customer 1 starts service immediately. The departure time is thus computed as

$$
T = 0 + {q}_{1} = 0 + \left( {{10} + 5 \times  {.6733}}\right)  = {13.37}\text{ minutes }
$$

The chronological list of future events thus becomes

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>13.37</td><td>Departure of customer 1</td></tr><tr><td>42.48</td><td>Arrival of customer 2</td></tr></table>

Departure of customer 1 at $T = {13.37}$ . Because the queue is empty, the facility is declared idle. At the same time, we record that the facility has been busy between $T = 0$ and $T = {13.37}\mathrm{\;{min}}$ . The updated list of future events becomes

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>42.48</td><td>Arrival of customer 2</td></tr></table>

Arrival of customer 2 at $T = {42.48}$ . Customer 3 will arrive at

$$
T = {42.48} + \left\lbrack  {-{15}\ln \left( {.4799}\right) }\right\rbrack   = {53.49}\text{ minutes }
$$

Because the facility is idle, customer 2 starts service, and the facility is declared busy. The departure time is

$$
T = {42.48} + \left( {{10} + 5 \times  {.9486}}\right)  = {57.22}\text{ minutes }
$$

The list of future events is updated as

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>53.49</td><td>Arrival of customer 3</td></tr><tr><td>57.22</td><td>Departure of customer 2</td></tr></table>

Arrival of customer 3 at $T = {53.49}$ . Customer 4 will arrive at

$$
T = {53.49} + \left\lbrack  {-{15}\ln \left( {.6139}\right) }\right\rbrack   = {60.81}\text{ minutes }
$$

Because the facility is currently busy (until $T = {57.22}$ ), customer 3 is placed in queue at $T = {53.49}$ . The updated list of future events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>57.22</td><td>Departure of customer 2</td></tr><tr><td>60.81</td><td>Arrival of customer 4</td></tr></table>

Departure of customer 2 at $T = {57.22}$ . Customer 3 is taken out of the queue to start service. The waiting time is

$$
{W}_{3} = {57.22} - {53.49} = {3.73}\text{ minutes }
$$

The departure time is

$$
T = {57.22} + \left( {{10} + 5 \times  {.5933}}\right)  = {70.19}\text{ minutes }
$$

The updated list of future events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>60.81</td><td>Arrival of customer 4</td></tr><tr><td>70.19</td><td>Departure of customer 3</td></tr></table>

Arrival of customer 4 at $T = {60.81}$ . Customer 5 will arrive at

$$
T = {60.81} + \left\lbrack  {-{15}\ln \left( {.9341}\right) }\right\rbrack   = {61.83}\text{ minutes }
$$

Because the facility is busy until $T = {70.19}$ , customer 4 is placed in the queue. The updated list of future events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>61.83</td><td>Arrival of customer 5</td></tr><tr><td>70.19</td><td>Departure of customer 3</td></tr></table>

Arrival of customer 5 at $T = {61.83}$ . The simulation is limited to 5 arrivals, hence customer 6 arrival is not generated. The facility is still busy, hence the customer is placed in queue at $T = {61.83}$ . The updated list of events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>70.19</td><td>Departure of customer 3</td></tr></table>

Departure of customer 3 at $T = {70.19}$ . Customer 4 is taken out of the queue to start service. The waiting time is

$$
{W}_{4} = {70.19} - {60.81} = {9.38}\text{ minutes }
$$

The departure time is

$$
T = {70.19} + \left\lbrack  {{110} + 5 \times  {.1782}}\right\rbrack   = {81.08}\text{ minutes }
$$

The updated list of future events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>81.08</td><td>Departure of customer 4</td></tr></table>

Departure of customer 4 at $T = {81.08}$ . Customer 5 is taken out of the queue to start service. The waiting time is

$$
{W}_{5} = {81.08} - {61.83} = {19.25}\text{ minutes }
$$

The departure time is

$$
T = {81.08} + \left( {{10} + 5 \times  {.3473}}\right)  = {92.82}\text{ minutes }
$$

The updated list of future events is

<table><tr><td>Time, $T$</td><td>Event</td></tr><tr><td>92.82</td><td>Departure of customer 5</td></tr></table>

Departure of customer 5 at $T = {92.82}$ . There are no more customers in the system (queue and facility) and the simulation ends.

Figure 19.6 summarizes the changes in the length of the queue and the utilization of the facility as a function of the simulation time.

The queue length and the facility utilization are known as time-based variables because their variation is a function of time. As result, their average values are computed as

$$
\left( \begin{array}{l} \text{ Average value of a } \\  \text{ time-based variable } \end{array}\right)  = \frac{\text{ Area under curve }}{\text{ Simulated period }}
$$

Implementing this formula for the data in Figure 19.6, we get

$$
\left( \begin{matrix} \text{ Average queue } \\  \text{ length } \end{matrix}\right)  = \frac{{A}_{1} + {A}_{2}}{92.82} = \frac{32.36}{92.82} = {.349}\text{ customer }
$$

$$
\left( \begin{matrix} \text{ Average facility } \\  \text{ utilization } \end{matrix}\right)  = \frac{{A}_{3} + {A}_{4}}{92.82} = \frac{63.71}{92.82} = {.686}\text{ barber }
$$

![bo_d56m5ljef24c73bhe69g_15_418_201_1040_669_0.jpg](bo_d56m5ljef24c73bhe69g_15_418_201_1040_669_0.jpg)

FIGURE 19.6

Changes in queue length and facility utilization as a function of simulation time, $T$

The average waiting time in the queue is an observation-based variable whose value is computed as

$$
\left( \begin{matrix} \text{ Average value of an } \\  \text{ observation-based variable } \end{matrix}\right)  = \frac{\text{ Sum of observations }}{\text{ Number of observations }}
$$

Examination of Figure 19.6 reveals that the area under the queue-length curve actually equals the sum of the waiting time for the three customers who joined the queue; namely,

$$
{W}_{1} + {W}_{2} + {W}_{3} + {W}_{4} + {W}_{5} = 0 + 0 + {3.73} + {9.38} + {19.25} = {32.36}\text{ minutes }
$$

The average waiting time in the queue for all customers is thus computed as

$$
{\bar{W}}_{q} = \frac{32.36}{5} = {6.47}\text{ minutes }
$$

#### 19.5.2 Spreadsheet-Based Simulation of the Single-Server Model

This section develops a spreadsheet-based model for the single-server model. The objective of the development is to reinforce the ideas introduced in Section 19.5.1. Of course, a single-server model is a simple situation that can be modeled readily in a spreadsheet environment. Other situations require more involved modeling effort, a task that is facilitated by available simulation packages (see Section 19.7).

The presentation in Section 19.5.1 shows that the simulation model of the single-server facility requires two basic elements:

1. A chronological list of the model's events.

2. A graph that keeps track of the changes in facility utilization and queue length.

These two elements remain essential in the development of the spreadsheet-based (indeed, any computer-based) simulation model. The difference is that the implementation is realized in a manner that is compatible with the use of the computer. As in Section 19.5.1, customers are served in order of arrival (FIFO).

Figure 19.7 provides the output of excelSingleServer.xls. The input data allow representing the interarrival and service time in one of four ways: constant, exponential, uniform, and triangular. The triangular distribution is useful in that it can be used as a rough initial estimate of any distribution, simply by providing three estimates $a, b$ , and $c$ that represent the smallest, the most likely, and the largest values of the interarrival or service time. The only other information needed to drive the simulation is the length of the simulation run, which in this model is specified by the number of arrivals that can be generated in the model.

The spreadsheet calculations reserve one row for each arrival. The interarrival and service times for each arrival are generated from the input data. The first arrival is assumed to occur at $T = 0$ . Because the facility starts idle, the customer starts service immediately. The spreadsheet provides sufficient information to demonstrate the internal computations given in Section 19.5.1.

## FIGURE 19.7

Excel output of a single-server simulation model (file excelSingleServer.xls)

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>K</td><td>L</td><td>M</td><td>N</td><td>0</td><td>P</td><td>Q</td></tr><tr><td>1</td><td colspan="15">Simulation of a Single-Server Queueing Model</td></tr><tr><td>2</td><td colspan="2">Nbr of arrivals =</td><td colspan="6">20 <<Maximum 500</td><td colspan="7"></td></tr><tr><td>3</td><td colspan="8">Enter x in column A to select interarrival pdf:</td><td>Nbr</td><td>InterAvIT</td><td>ServiceT</td><td>AMIT</td><td>DepartT</td><td>Wq</td><td>Ws</td></tr><tr><td>4</td><td></td><td>Constant =</td><td></td><td></td><td></td><td></td><td></td><td></td><td>1</td><td>3.73</td><td>12.83</td><td>0.00</td><td>12.83</td><td>0.00</td><td>12.83</td></tr><tr><td>5</td><td>X</td><td>Exponential:</td><td>$\lambda  =$</td><td>0.067</td><td></td><td></td><td></td><td></td><td>2</td><td>5.37</td><td>14.71</td><td>3.73</td><td>27.55</td><td>9.10</td><td>23.82</td></tr><tr><td>6</td><td></td><td>Uniform:</td><td>a =</td><td></td><td>b =</td><td></td><td></td><td></td><td>3</td><td>3.86</td><td>12.21</td><td>9.09</td><td>39.75</td><td>18.45</td><td>30.66</td></tr><tr><td>7</td><td></td><td>Triangular:</td><td>a =</td><td></td><td>b =</td><td></td><td>c =</td><td></td><td>4</td><td>14.10</td><td>11.18</td><td>12.95</td><td>50.94</td><td>26.80</td><td>37.98</td></tr><tr><td>8</td><td colspan="8">Enter x in column A to select service time pdf:</td><td>5</td><td>7.35</td><td>14.92</td><td>27.05</td><td>65.85</td><td>23.88</td><td>38.80</td></tr><tr><td>9</td><td></td><td>Constant =</td><td></td><td></td><td></td><td></td><td></td><td></td><td>6</td><td>35.70</td><td>14.22</td><td>34.41</td><td>60.07</td><td>31.45</td><td>45.67</td></tr><tr><td>10</td><td></td><td>Exponential</td><td>$\mu  =$</td><td></td><td></td><td></td><td></td><td></td><td>7</td><td>0.60</td><td>14.50</td><td>70.11</td><td>94.58</td><td>9.97</td><td>24,47</td></tr><tr><td>11</td><td>X</td><td>Uniform:</td><td>a =</td><td>10</td><td>b =</td><td>15</td><td></td><td></td><td>8</td><td>4.25</td><td>13.35</td><td>70.71</td><td>107.93</td><td>23.87</td><td>37.22</td></tr><tr><td>12</td><td></td><td>Triangular:</td><td>a =</td><td></td><td>b =</td><td></td><td>c =</td><td></td><td>9</td><td>4.85</td><td>12.45</td><td>74.96</td><td>120.38</td><td>32 97</td><td>45.41</td></tr><tr><td>13</td><td colspan="8">Output Summary</td><td>10</td><td>7.43</td><td>11.57</td><td>79.81</td><td>131.94</td><td>40.56</td><td>52.13</td></tr><tr><td>14</td><td></td><td>Av. facility utilization $=$</td><td></td><td></td><td>0.98</td><td colspan="3" rowspan="10">Press F9 to trigger a new simulation run.</td><td>11</td><td>8.99</td><td>14.65</td><td>87.24</td><td>146.59</td><td>44.70</td><td>59.34</td></tr><tr><td>15</td><td></td><td>Percent idleness (%) =</td><td></td><td></td><td>1.95</td><td>12</td><td>49.78</td><td>12.85</td><td>96.23</td><td>159.43</td><td>50.36</td><td>63.20</td></tr><tr><td>16</td><td></td><td></td><td></td><td></td><td></td><td>13</td><td>0.42</td><td>14.12</td><td>146.01</td><td>173.55</td><td>13.43</td><td>27.54</td></tr><tr><td>17</td><td></td><td>Av. queue length, Lq =</td><td></td><td></td><td>1.57</td><td>14</td><td>8.77</td><td>13.69</td><td>146.43</td><td>187.24</td><td>27.13</td><td>40.82</td></tr><tr><td>18</td><td></td><td>Av. nbr in system. Ls =</td><td></td><td></td><td>2.55</td><td>15</td><td>11.19</td><td>10.50</td><td>155.20</td><td>197.75</td><td>32.05</td><td>42.55</td></tr><tr><td>19</td><td></td><td>Av. queue time. Wg =</td><td></td><td></td><td>21.24</td><td>16</td><td>42.82</td><td>13.78</td><td>166.38</td><td>211.53</td><td>31.36</td><td>45.14</td></tr><tr><td>20</td><td></td><td>Av. system time. Ws =</td><td></td><td></td><td>34.47</td><td>17</td><td>19.87</td><td>12.29</td><td>209.20</td><td>223.82</td><td>2.33</td><td>14.62</td></tr><tr><td>21</td><td></td><td>Sum(ServiceTime) =</td><td></td><td></td><td>264.65</td><td>18</td><td>9.25</td><td>12.95</td><td>229.07</td><td>242.03</td><td>0.00</td><td>12.95</td></tr><tr><td>22</td><td></td><td>Sum(Wq) =</td><td></td><td></td><td>424.80</td><td>19</td><td>13.98</td><td>12.99</td><td>238.33</td><td>255.02</td><td>3.70</td><td>16.69</td></tr><tr><td>23</td><td></td><td>Sum(Ws) =</td><td></td><td></td><td>68944</td><td>20</td><td>58.46</td><td>14.88</td><td>252.31</td><td>269.90</td><td>2.71</td><td>17.59</td></tr></table>

Another spreadsheet was developed for simulating multiserver models (excelMultiServer.xls). The design of the template is based on the same ideas used in the single-server case. However, the determination of the departure time is not as straightforward and requires the use of VBA macros.

## Excel Moment

In Example 18.6-5 and Problems 18-69 and 18-77, a case is made for the operational advantage of using service pools under the Poisson assumptions, even under very high facility utilization rates (i.e., $\frac{\rho }{c} \rightarrow  1$ ). In the remarks following Example 18.6-5, I made the (unsubstantiated) claim that service pools can lead efficient mode of operation even if the queuing situation does not follow the Poisson model. The literature is void of mathematical arguments that could invalidate this claim. This chapter offers an opportunity to get a feel as to whether the claim may be plausible. Specifically, excel spreadsheets excelSingleServer.xls and excelMultiServer.xls simulate the single-server and multiple-server queues with constant, exponential, uniform, and triangular interarrival and service times. You are encouraged to design an experiment that will "substantiate" or "refute" the claim. Keep in mind that you are just running an experiment and not seeking a proof.

### 19.6 METHODS FOR GATHERING STATISTICAL OBSERVATIONS

Simulation is a statistical experiment, and its output must be interpreted using proper statistical inference tools (e.g., confidence intervals and hypothesis testing). To accomplish this task, a simulation experiment must satisfy three conditions:

1. Observations are drawn from stationary (identical) distributions.

2. Observations are sampled from a normal population.

3. Observations are independent.

In a strict sense, the simulation experiment does not satisfy any of these conditions. Nevertheless, we can ensure that these conditions remain statistically acceptable by restricting the manner in which the observations are gathered.

First, we consider the issue of stationary distributions. Simulation output is a function of the length of the simulated period. The initial period produces erratic behavior and is usually referred to as the transient or warm-up period. When the output stabilizes, the system operates under steady state. Unfortunately, there is no definitive way to predict the start point of steady state in advance. In general, a longer simulation run has better chance of reaching steady state - meaning that the problem is addressed by using a sufficiently large sample size.

Next, we consider the requirement that simulation observations are drawn from a normal population. This requirement is realized by using the central limit theorem (see Section 14.4.4), which confirms that the distribution of the average of a sample is asymptotically normal regardless of the parent population. The central limit theorem is thus the main tool we use for satisfying the normal distribution assumption.

The third condition deals with the independence of the observations. In simulation, an observation can be based on a single independent run or by subdividing a single run into subintervals each representing an observation. Each method has it advantages and disadvantages. The first method alleviates the question of independence but has the disadvantage of including the transient period in each observation. In the second method, the effect of the transient period is not as pronounced, but it inherently worsens the issue of independence. As will be explained subsequently in this section, a possible remedy calls for increasing the length of the simulation run.

The most common methods for collecting observations in simulation are

1. Subinterval method.

2. Replication method.

3. Regenerative (or cycles) method.

The first two methods can be readily automated in all widely used simulation languages (see Section 19.7). On the other hand, the third method, though it addresses directly the issue of independence by seeking identical starting conditions for the different observations, may be difficult to implement in practice.

Sections 19.6.1 and 19.6.2 present the first two methods. Details of the third method can be found in Law (2007).

#### 19.6.1 Subinterval Method

Figure 19.8 illustrates the idea of the subinterval method. Suppose that the length of the simulation run is $T$ time units. The subinterval method first truncates an initial transient period, and then subdivides the remainder of the simulation run into $n$ equal subintervals (or batches). The average of a desired measure of performance (e.g., queue length or waiting time in queue) within each subinterval is then used to represent a single observation. Truncation of the initial transient period means that no statistical data are collected during that period.

The advantage of the subinterval method is that the effect of the transient (nonstationary) conditions is mitigated, particularly for the observations that are collected toward the end of the simulation run. The disadvantage is that successive batches with common boundary conditions are not necessarily independent. The problem can be alleviated by increasing the time base for each observation.

FIGURE 19.8

Collecting simulation data using the subinterval method

![bo_d56m5ljef24c73bhe69g_18_505_1737_953_399_0.jpg](bo_d56m5ljef24c73bhe69g_18_505_1737_953_399_0.jpg)

## Example 19.6-1

Figure 19.9 shows the change in queue length in a single-queue model as a function of the simulation time. The simulation run length is $T = {35}\mathrm{{hrs}}$ , and the length of the transient period is estimated to equal $5\mathrm{{hrs}}$ . The time base for an observation is 6 hrs, which produces $n = 5$ observation.

Let ${\bar{Q}}_{i}$ represent the average queue length in batch $i$ . Because the queue length is a time-based variable, we have

$$
{\bar{Q}}_{i} = \frac{{A}_{i}}{t}, i = 1,2,\ldots ,5
$$

where ${A}_{i}$ is the area under the queue-length curve associated with batch (observation) $i$ , and $t\left( { = 6}\right)$ is the time base per batch.

The data in Figure 19.9 produce the following observations:

<table><tr><td>Observation $i$</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td></tr><tr><td>${A}_{i}$ <br> ${\bar{Q}}_{i}$</td><td>14 <br> 2.33</td><td>10 <br> 1.67</td><td>11 <br> 1.83</td><td>6 <br> 1.00</td><td>15 <br> 2.50</td></tr><tr><td colspan="2">Sample mean $= {1.87}$</td><td colspan="4">Sample standard deviation $= {.59}$</td></tr></table>

The sample mean and variance can be used to compute a confidence interval, if desired. The computation of the sample variance in Example 19.6-1 is based on the following familiar formula:

$$
s = \sqrt{\frac{\mathop{\sum }\limits_{{i = 1}}^{n}{x}_{i}^{2} - n{\bar{x}}^{2}}{n - 1}}
$$

This formula is only an approximation of the true standard deviation because it ignores the effect of autocorrelation between the successive batches. The exact formula can be found in Law (2007).

#### 19.6.2 Replication Method

In the replication method, each observation is represented by an independent simulation run in which the transient period is truncated, as illustrated in Figure 19.10. The computation of the observation averages for each batch is the same as in the subinterval method. The only difference is that the standard variance formula is applicable because the batches are not independent.

## FIGURE 19.9

Change in queue length with simulation time in Example 19.6-1

![bo_d56m5ljef24c73bhe69g_19_348_1794_1179_376_0.jpg](bo_d56m5ljef24c73bhe69g_19_348_1794_1179_376_0.jpg)

![bo_d56m5ljef24c73bhe69g_20_342_195_1272_379_0.jpg](bo_d56m5ljef24c73bhe69g_20_342_195_1272_379_0.jpg)

FIGURE 19.10

Collecting simulation data using the replication method

The advantage of the replication method is that each simulation run is driven by a distinct 0-1 random number stream, which yields statistically independent observations. The disadvantage is that each observation may be biased by the initial effect of the transient conditions. Such a problem may be alleviated by making the run length sufficiently large.

### 19.7 SIMULATION LANGUAGES

Execution of simulation models entails two distinct types of computations: (1) file manipulations that deal with the chronological storage and processing of model events, and (2) arithmetic and bookkeeping computations associated with generation of random samples and collection of model statistics. The first type of computation involves extensive logic in the development of list processing, and the second type entails tedious and time-consuming calculations. The nature of these computations makes the computer an essential tool for executing simulation models, and, in turn, prompts the development of special computer simulation languages for performing these computations conveniently and efficiently.

Available discrete simulation languages fall into two broad categories:

1. Event scheduling.

2. Process oriented.

In event scheduling languages, the user details the actions associated with the occurrence of each event, in much the same way they are given in Example 19.5-1. The main role of the language in this case is (1) automation of sampling from distributions, (2) storage and retrieval of events in chronological order, and (3) collection of model statistics.

Process-oriented languages use blocks or nodes that can be linked together to form a network that describes the movements of transactions or entities (i.e., customers) in the system. For example, the three most prominent blocks/nodes in any process-simulation language are a source from which transactions are created, a queue where they can wait if necessary, and a facility where service is performed. Each of these blocks/nodes is defined with all the information needed to drive the simulation automatically. For example, once the interarrival time for the source is specified, a process-oriented language automatically "knows" when arrival events will occur. In effect, each block/node of the model has standing instructions that define how and when transactions are moved in the simulation network.

Process-oriented languages are internally driven by the same actions used in event-scheduling languages. The difference is that these actions are automated to relieve the user of the tedious computational and logical details. In a way, we can regard process-oriented languages as being based on the input-output concept of the "black box" approach. This essentially means that process-oriented languages trade modeling flexibility for simplicity and ease of use.

Event-scheduling languages (such as SIMSCRIPT, SLAM, and SIMAN) are outdated and are rarely used in practice. Recently, a new language called DEEDS (Elizandro and Taha, 2008) is based on the novice approach of using an Excel spreadsheet to drive event scheduling. DEEDS allows the modeling flexibility of event-driven simulation languages while achieving the intuitive nature of a process-oriented language.

The predominant process-oriented commercial package is Arena. It uses extensive user interface to simplify the process of creating a simulation model. It also provides animation capabilities where changes in the system can be observed visually. However, to an experienced simulation professional, these interfaces may appear to reduce the development of a simulation model to a "slow-motion" pace. It is not surprising that some users continue to prefer writing simulation models in higher-level programming languages.

Remarks. Most simulation languages come equipped with animation that exhibits simultaneous event movements of objects or transactions (e.g., products transiting among processing machines). Representation of transaction movements can be abstract (e.g., simple bullets traversing the model components with numeric counters recording the frequency of visitations along their routes) or a full-fledged near-real 3D animation.

Animation can play a role in the verification phase of the model development, at times pinpointing irregularities in the movements of the transaction. However, this potential advantage can lose its flair in complex models, with the visual display getting cluttered with transactions moving randomly all over the place. Add to this the fact that human patience for watching a simulation animation usually reaches its limit in scant few minutes, no matter how realistic the display may be.

Some argue that animation is a "perfect" tool for convincing management of the viability of simulation modeling. This argument treats the simulation model as a "black box," requiring only input data to produce output results. It does not educate the user about what simulation can or cannot do or about the complexity of the simulation experiment, not to mention the length of time and effort needed to produce a working model. These factors are of paramount importance when it comes to securing management's long-term support of simulation projects.

## BIBILIOGRAPHY

Banks, J., J. Carson, B. Nelson, and D. Nicol, Discrete-Event System Simulation, 4th ed, Prentice Hall, NJ, 2005.

Box, G., and M. Muller, "A Note on the Generation of Random Normal Deviates," Annals of Mathematical Statistics, Vol. 29, pp. 610-611, 1958.

Elizandro, D., and H. Taha, Simulation of Industrial Systems: Discrete Event Simulation Using Excel/VBA, Taylor and Francis, New York, 2008.

Law, A., Simulation Modeling & Analysis, 4th ed., McGraw-Hill, New York, 2007.

Rubenstein, R., B. Melamed, and A. Shapiro, Modern Simulation and Modeling, Wiley, New York, 1998.

Taha, H., Simulation Modeling and SIMNET, Prentice Hall, Upper Saddle River, NJ, 1988.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>19.1</td><td>19-1 to 19-9</td><td>19.5.1</td><td>19-36 to 19-39</td></tr><tr><td>19.2</td><td>19-10 to 19-11</td><td>19.5.2</td><td>19-40 to 19-42</td></tr><tr><td>19.3.1</td><td>19-12 to 19-15</td><td>19.6.1</td><td>19-43 to 19-44</td></tr><tr><td>19.3.2</td><td>19-16 to 19-33</td><td>19.6.2</td><td>19-45 to 19-49</td></tr><tr><td>19.4</td><td>19-34 to 19-35</td><td></td><td></td></tr></table>

19-1. In Example 19.1-1, estimate the area of the circle using the first two columns of the 0-1 random numbers in Table 19.1. (For convenience, go down each column, selecting ${R}_{1}$ first and then ${R}_{2}$ .) How does this estimate compare with the ones given in Figure 19.2?

19-2. Suppose that the equation of a circle is

$$
{\left( x - 4\right) }^{2} + {\left( y + 3\right) }^{2} = {25}
$$

(a) Define the corresponding distributions $f\left( x\right)$ and $f\left( y\right)$ , and then show how a sample point $\left( {x, y}\right)$ is determined using the $\left( {0,1}\right)$ random pair $\left( {{R}_{1},{R}_{2}}\right)$ .

(b) Use excelCircle.xls to estimate the area and the associated 95% confidence interval given $n = {100},{000}$ and $N = {10}$ .

19-3. Use Monte Carlo sampling to estimate the area of the lake shown in Figure 19.11. Base the estimate on the first two columns of $\left( {0,1}\right)$ random numbers in Table 19.1.

![bo_d56m5ljef24c73bhe69g_22_506_1732_663_429_0.jpg](bo_d56m5ljef24c73bhe69g_22_506_1732_663_429_0.jpg)

FIGURE 19.11

Lake map for Problem 19-3

19-4. Consider the game in which two players, Jan and Jim, take turns in tossing a fair coin. If the outcome is heads, Jim gets \$10 from Jan. Otherwise, Jan gets \$10 from Jim.

*(a) How is the game simulated as a Monte Carlo experiment?

(b) Run the experiment for 5 replications of 10 tosses each. Use the first five columns of the 0-1 random numbers in Table 19.1, with each column corresponding to one replication.

(c) Establish a 95% confidence interval on Jan's winnings.

(d) Compare the confidence interval in (c) with Jan's expected theoretical winnings.

19-5. Consider the following definite integral:

$$
{\int }_{0}^{1}{x}^{4}{dx}
$$

(a) Develop the Monte Carlo experiment to estimate the value of the integral.

(b) Use the first four columns in Table 19.1 to evaluate the integral based on 4 replications of size 5 each. Compute a 95% confidence interval, and compare it with the exact value of the integral.

19-6. Simulate five wins or losses of the following game of craps: The player rolls two fair dice. If the outcome sum is 7 or 11, the player wins \$10. Otherwise, the player records the resulting sum (called point) and keeps on rolling the dice until the outcome sum matches the recorded point, in which case the player wins \$10. If a 7 is obtained prior to matching the point, the player loses \$10.

*19-7. The lead time for receiving an order can be 1 or 2 days, with equal probabilities. The demand per day assumes the values 0,1 , and 2 with the respective probabilities of .2,.7, and .1. Use the random numbers in Table 19.1 (starting with column 1) to estimate the joint distribution of the demand and lead time. From the joint distribution, estimate the pdf of demand during lead time. (Hint: The demand during lead time assumes discrete values from 0 to 4.)

19-8. Buffon needle experiment. A horizontal plane is ruled with parallel lines spaced $D\mathrm{\;{cm}}$ apart. A needle of length $d\mathrm{\;{cm}}\left( {d < D}\right)$ is dropped randomly on the plane. The objective of the experiment is to determine the probability that either end of the needle touches or crosses one of the lines. Define

$h =$ Perpendicular distance from the needle center to a (parallel) line $\theta  =$ Inclination angle of the needle with a line

(a) Show that the needle will touch or cross a line only if

$$
h \leq  \frac{d}{2}\sin \theta ,0 \leq  h \leq  \frac{D}{2},0 \leq  \theta  \leq  \pi
$$

(b) Design the Monte Carlo experiment, and provide an estimate of the desired probability.

(c) Use Excel to obtain 4 replications of size 10 each of the desired probability. Determine a 95% confidence interval for the estimate. Assume $D = {20}\mathrm{\;{cm}}$ and $d = {10}\mathrm{\;{cm}}.$

(d) Prove that the theoretical probability is given by the formula

$$
p = \frac{2d}{\pi D}
$$

(e) Use the result in (c) together with the formula in (d) to estimate $\pi$ .

19-9. Using the results in Figure 19.2 (Example 19.1-1) with $n = {60},{000}$ for estimating the area of a circle, design a Monte Carlo experiment for estimating the value of the constant $\pi$ . [Hint: (Area of a circle)/(Area of rectangle tightly enveloping the circle) $= \pi /4$ .]

19-10. Categorize the following situations as either discrete or continuous (or a combination of both). In each case, specify the objective of developing the simulation model.

*(a) Orders for an item arrive randomly at a warehouse. An order that cannot be filled immediately from available stock must await the arrival of new shipments.

(b) Goods arrive on pallets at a receiving bay of an automated warehouse. The pallets are loaded on a lower conveyor belt and lifted through an up-elevator to an upper conveyor that moves the pallets to corridors. The corridors are served by cranes that pick up the pallets from the conveyor and place them in storage bins.

(c) World population is affected by the availability of natural resources, food production, environmental conditions, educational level, health care, and capital investments.

19-11. Explain why you would agree or disagree with the following statement: "Most discrete event simulation models can be viewed in some form or another as queuing systems consisting of sources from which customers arrive, queues where customers may wait, and facilities where customers are served."

19-12. Identify the discrete events needed to simulate the following situation: Three types of jobs arrive from different sources. All three types are processed on a single machine, with the highest priority given to jobs from the first source, followed by source 2, then source 3.

19-13. Jobs arrive at a constant rate at a carousel conveyor system. Two service stations are spaced equally around the carousel. If the server is idle when a job arrives at the station, the job is removed from the conveyor for processing. Otherwise, the job continues to rotate on the carousel until a server becomes available. A processed job is stored in an adjacent shipping area. Identify the discrete events needed to simulate this situation.

19-14. Cars arrive at a two-lane, drive-in bank, where each lane can house a maximum of four cars. If the two lanes are full, arriving cars seek service elsewhere. If at any time one lane is at least two cars longer than the other, the last car in the longer lane will jockey to the last position in the shorter lane. The bank operates the drive-in facility from 8:00 A.M. to 3:00 P.M. each work day. Define the discrete events for the situation.

*19-15. The cafeteria at Elmdale Elementary provides a single-tray, fixed-menu lunch to all its pupils. Kids arrive at the dispensing window every 30 seconds. It takes 18 seconds to receive the lunch tray. Map the arrival-departure events on the time scale for the first five pupils.

*19-16. In Example 19.3-2, suppose that the first customer arrives at time 0 . Use the first three random numbers in column 1 of Table 19.1 to generate the arrival times of the next 3 customers, and graph the resulting events on the timescale.

*19-17. Uniform Distribution. Suppose that the time needed to manufacture a part on a machine is described by the following uniform distribution:

$$
f\left( t\right)  = \frac{1}{b - a}, a \leq  t \leq  b
$$

Determine an expression for the sample $t$ , given the random number $R$ .

19-18. Jobs are received randomly at a one-machine shop. The time between arrivals is exponential with mean 2 hrs. The time needed to manufacture a job is uniform between 1.1 and 2 hrs. Assuming that the first job arrives at time 0, determine the arrival and departure time for the first five jobs using the $\left( {0,1}\right)$ random numbers in column 1 of Table 19.1.

19-19. The demand for an expensive spare part of a passenger jet is0,1,2, or 3 units per month with probabilities .3, .3, 2, and .2, respectively. The airline maintenance shop starts operation with a stock of 6 units, and will bring the stock level back to 6 units immediately after it drops below 5 units.

*(a) Devise the procedure for sampling demand.

(b) How many months will elapse until the first replenishment occurs? Use successive values of $R$ from the first column in Table 19.1.

19-20. In a simulation situation, TV units are inspected for possible defects. There is a 70% chance that a unit will pass inspection, in which case it is sent to packaging. Otherwise, the unit is repaired. We can represent the situation symbolically in one of two ways.

goto REPAIR/.3, PACKAGE/.7 goto PACKAGE/.7, REPAIR/.3

These two representations appear equivalent. Yet, when a given sequence of $\left( {0,1}\right)$ random numbers is applied to the two representations, different decisions (REPAIR or PACKAGE) may result. Explain why.

19-21. A player tosses a fair coin repeatedly until a head occurs. The associated payoff is ${3}^{n}$ , where $n$ is the number of tosses until a head comes up.

(a) Devise the sampling procedure of the game.

(b) Use the random numbers in column 1 of Table 19.1 to determine the cumulative payoff after two heads occur.

19-22. Triangular Distribution. In simulation, the lack of data may make it impossible to determine the probability distribution associated with a simulation activity. In most of these situations, it may be easy to describe the desired variable by estimating its smallest, most likely, and largest values. These three values are sufficient to define a triangular distribution, which can then be used as "rough cut" estimation of the real distribution.

(a) Develop the formula for sampling from the following triangular distribution, whose respective parameters are $a, b$ , and $c$ :

$$
f\left( x\right)  = \left\{  \begin{array}{ll} \frac{2\left( {x - a}\right) }{\left( {b - a}\right) \left( {c - a}\right) }, & a \leq  x \leq  b \\  \frac{2\left( {c - x}\right) }{\left( {c - b}\right) \left( {c - a}\right) }, & b \leq  x \leq  c \end{array}\right.
$$

(b) Generate three samples from a triangular distribution with parameters $\left( {1,3,7}\right)$ using the first three random numbers in column 1 of Table 19.1.

19-23. Consider a probability distribution that consists of a rectangle flanked on the left and right sides by two symmetrical right triangles. The respective ranges for the triangle on the left, the rectangle, and the triangle on the right are $\left\lbrack  {a, b}\right\rbrack  ,\left\lbrack  {b, c}\right\rbrack$ , and $\left\lbrack  {c, d}\right\rbrack$ , $a < b < c < d$ . Both triangles have the same height as the rectangle.

(a) Develop a sampling procedure.

(b) Determine five samples with $\left( {a, b, c, d}\right)  = \left( {1,2,4,6}\right)$ using the first five random numbers in column 1 of Table 19.1.

*19-24. Geometric Distribution. Show how a random sample can be obtained from the following geometric distribution:

$$
f\left( x\right)  = p{\left( 1 - p\right) }^{x}, x = 0,1,2,\ldots
$$

The parameter $x$ is the number of (Bernoulli) failures until a success occurs, and $p$ is the probability of a success, $0 < p < 1$ . Generate five samples for $p = {.6}$ , using the first five random numbers in column 1 of Table 19.1.

19-25. Weibull Distribution. Show how a random sample can be obtained from the Weibull distribution with the following probability density function:

$$
f\left( x\right)  = \alpha {\beta }^{-\alpha }{x}^{\alpha  - 1}{e}^{-{\left( x/\beta \right) }^{\alpha }}, x > 0
$$

where $\alpha  > 0$ is the shape parameter, and $\beta  > 0$ is the scale parameter.

*19-26. In Example 19.3-3, compute an Erlang sample, given $m = 3$ and $\lambda  = {10}$ events per hour. ${}^{1}$

19-27. In Example 19.3-4, generate three Poisson samples during a half-hour period, given that the mean of the Poisson is 9 events per hour.

19-28. In Example 19.4-5, generate two samples from $N\left( {7,2}\right)$ by using both the convolution method and the Box-Muller method.

19-29. Jobs arrive at Metalco Jobshop according to a Poisson distribution, with a mean of six jobs per day. Received jobs are assigned to the five machining centers of the shop on a strict rotational basis. Determine one sample of the interval between the arrival of jobs at the first machine center.

19-30. The ACT scores for the 1994 senior class at Springdale High are normal, with a mean of 27 points and a standard deviation of 3 points. Suppose that we draw a random sample of six seniors from that class. Use the Box-Muller method to determine the mean and standard deviation of the sample.

*19-31. Psychology professor Yataha is conducting a learning experiment in which mice are trained to find their way around a maze. The base of the maze is square. A mouse enters the maze at one of the four corners and must find its way through the maze to exit at the same point where it entered. The design of the maze is such that the mouse must pass by each of the remaining three corner points exactly once before it exits. The multipaths of the maze connect the four corners in a strict clockwise order. Professor Yataha estimates that the time the mouse takes to reach one corner point from another is uniformly distributed between 10 and 20 seconds, depending on the path it takes. Develop a sampling procedure for the time a mouse spends in the maze.

19-32. In Problem 19-31, suppose that once a mouse makes an exit from the maze, another mouse instantly enters. Develop a sampling procedure for the number of mice that exit the maze in 5 minute or less.

19-33. Negative Binomial. Show how a random sample can be determined from the negative binomial whose distribution is given as

$$
f\left( x\right)  = {C}_{x}^{r + x - 1}{p}^{r}{\left( 1 - p\right) }^{x}, x = 0,1,2,\ldots
$$

where $x$ is the number of failures until the $r$ th success occurs in a sequence of independent Bernoulli trials and $p$ is the probability of success, $0 < p < 1$ . (Hint: The negative binomial is the convolution of $r$ independent geometric samples. See Problem 19-24.)

*19-34. Use excelRN.xls with the following sets of parameters, and compare the results with those of Example 19.4-1:

$$
b = {17}, c = {111}, m = {103}\text{ , seed } = 7
$$

---

${}^{1}$ For Problems 19-26 to 19-33, use the random numbers in Table 19.1 starting with column 1.

---

19-35. Find a random number generator on your computer, and use it to generate 500 zero-one random numbers. Histogram the resulting values (using the Microsoft histogram tool, see Section 12.5) and visually convince yourself that the obtained numbers reasonably follow the $\left( {0,1}\right)$ uniform distribution. Actually, to test the sequence properly, you would need to apply the following tests: chi-square goodness of fit (see Section 14.5), runs test for independence, and correlation test - see Law (2007) for details.

19-36. Suppose that the barbershop in Example 19.5-1 is operated by two barbers, and customers are served on a FCFS basis. Suppose further that the time to get a haircut is uniformly distributed between 15 and 30 minutes. The interarrival time of customers is exponential, with a mean of 10 minutes. Simulate the system manually for 75 time units. From the results of the simulation, determine the average time a customer waits in queue, the average number of customers waiting, and the average utilization of the barbers. Use the random numbers in Table 19.1.

19-37. Classify the following variables as either observation based or time based:

*(a) Time-to-failure of an electronic component.

*(b) Inventory level of an item.

(c) Order quantity of an inventory item.

(d) Number of defective items in a lot.

(e) Time needed to grade test papers.

(f) Number of cars in the parking lot of a car-rental agency.

*19-38. The following table represents the variation in the number of waiting customers in a queue as a function of the simulation time.

<table><tr><td>Simulation time, $T\left( \mathrm{{hr}}\right)$</td><td>No. of waiting customers</td></tr><tr><td>$0 \leq  T \leq  3$</td><td>0</td></tr><tr><td>$3 < T \leq  4$</td><td>1</td></tr><tr><td>$4 < T \leq  6$</td><td>2</td></tr><tr><td>$6 < T \leq  7$</td><td>1</td></tr><tr><td>$7 < T \leq  {10}$</td><td>0</td></tr><tr><td>${10} < T \leq  {12}$</td><td>2</td></tr><tr><td>${12} < T \leq  {18}$</td><td>3</td></tr><tr><td>${18} < T \leq  {20}$</td><td>2</td></tr><tr><td>${20} < T \leq  {25}$</td><td>1</td></tr></table>

Compute the following measures of performance:

(a) The average length of the queue.

(b) The average waiting time in the queue for those who must wait.

19-39. Suppose that the barbershop described at the start of Example 19.5-1 is operated by three barbers. Assume further that the utilization of the servers (barbers) is summarized as given in the following table:

<table><tr><td>Simulation time, $T\left( \mathrm{{hr}}\right)$</td><td>No. of busy servers</td></tr><tr><td>$0 < T \leq  {10}$</td><td>0</td></tr><tr><td>${10} < T \leq  {20}$</td><td>1</td></tr><tr><td>${20} < T \leq  {30}$</td><td>2</td></tr><tr><td>${30} < T \leq  {40}$</td><td>0</td></tr><tr><td>${40} < T \leq  {60}$</td><td>1</td></tr><tr><td>${60} < T \leq  {70}$</td><td>2</td></tr><tr><td>${70} < T \leq  {80}$</td><td>3</td></tr><tr><td>${80} < T \leq  {90}$</td><td>1</td></tr><tr><td>${90} < T \leq  {100}$</td><td>0</td></tr></table>

Determine the following measures of performance:

(a) The average utilization of the facility.

(b) The average busy time of the facility.

(c) The average idle time of the facility.

19-40. Using the input data in Example 19.5-1, run the Excel simulator for 10 arrivals and graph the changes in facility utilization and queue length as a function of the simulation time. Verify that the areas under the curves equal the sum of the service times and the sum of the waiting times, respectively.

19-41. Simulate the $M/M/1$ model for 500 arrivals, given the arrival rate $\lambda  = 4$ customers per hour and the service rate $\mu  = 6$ departures per hour. Run 5 replications (by refreshing the spreadsheet-pressing F9) and determine a 95% confidence interval for all the measures of performance of the model. Compare the results with the steady-state theoretical values of the $M/M/1$ model.

19-42. Television units arrive on a conveyor belt every 15 minutes for inspection at a single-operator station. Detailed data for the inspection station are not available. However, the operator estimates that it takes 10 minutes "on the average" to inspect a unit. Under the worst conditions, the inspection time does not exceed 13 minutes, and for certain units, inspection time may be as low as 9 minutes.

(a) Use the Excel simulator to simulate the inspection of ${200}\mathrm{{TV}}$ units.

(b) Based on five replications, estimate the average number of units awaiting inspection and the average utilization of the inspection station.

19-43. In Example 19.6-1, use the subinterval method to compute the average waiting time in the queue for those who must wait.

*19-44. In a simulation model, the subinterval method is used to compute batch averages. The transient period is estimated to be 100 , and each batch has a time base of 100 time units as well. Using the following data, which provide the waiting times for customers as a function of the simulation time, estimate the 95% confidence interval for the mean waiting time.

<table><tr><td>Time interval</td><td>Waiting times</td></tr><tr><td>0-100</td><td>10,20,13,14,8,15,6,8</td></tr><tr><td>100-200</td><td>12,30,10,14,16</td></tr><tr><td>200-300</td><td>15, 17, 20, 22</td></tr><tr><td>300-400</td><td>10, 20, 30, 15, 25, 31</td></tr><tr><td>400-500</td><td>15, 17, 20, 14, 13</td></tr><tr><td>500-600</td><td>25,30,15</td></tr></table>

19-45. Patrons arrive randomly at a three-clerk post office. The interarrival time is exponential with mean 5 minutes. The time a clerk spends with a patron is exponential with a mean of 10 minutes. All arriving patrons form one queue and wait for the first available free clerk. Run a simulation model of the system for 480 minutes to determine the following: ${}^{2}$

(a) The average number of patrons waiting in the queue.

(b) The average utilization of the clerks.

(c) Compare the simulation results with those of the $M/M/c$ queuing model (Chapter 18) and with the spreadsheet MultiServerSimulator.xls.

---

${}^{2}$ Work Problems 19-45 to 19-49 using a simulation language of your choice or a higher-order programming language.

---

19-46. Television units arrive for inspection on a conveyor belt at the constant rate of 5 units per hour. The inspection time takes between 10 and 15 minutes, uniformly distributed. Past experience shows that 20% of inspected units must be adjusted and then sent back for reinspection. The adjustment time is also uniformly distributed between 6 and 8 minutes. Run a simulation model for 480 minutes to compute the following:

(a) The average time a unit takes until it passes inspection.

(b) The average number of times a unit must be reinspected before it exits the system.

19-47. A mouse is trapped in a maze and desperately "wants out." After trying between 1 and 3 minutes, uniformly distributed, there is a 30% chance that it will find the right path. Otherwise, it will wander around aimlessly for between 2 and 3 minutes, uniformly distributed, and eventually end up where it started, only to try once again. The mouse can "try freedom" as many times as it pleases, but there is a limit to everything. With so much energy expended in trying and retrying, the mouse is certain to expire if it does not make it within a period that is normally distributed, with a mean of 10 minutes and a standard deviation of 2 minutes. Write a simulation model to estimate the probability that the mouse will be free. For the purpose of estimating the probability, assume that 100 mice will be processed by the model.

19-48. In the final stage of automobile manufacturing, a car moving on a transporter is situated between two parallel workstations to allow work to be done on both the left and right sides of the car simultaneously. The operation times for the left and right sides are uniform between 15 and 20 minutes and 18 and 22 minutes, respectively. The transporter arrives at the stations area every 20 minutes. Simulate the process for 480 minutes to determine the utilization of the left and right stations.

19-49. Cars arrive at a one-bay car wash facility where the interarrival time is exponential, with a mean of 10 minutes. Arriving cars line up in a single lane that can accommodate at most five waiting cars. If the lane is full, newly arriving cars will go elsewhere. It takes between 10 and 15 minutes, uniformly distributed, to wash a car. Simulate the system for 960 minutes, and estimate the time a car spends in the facility.