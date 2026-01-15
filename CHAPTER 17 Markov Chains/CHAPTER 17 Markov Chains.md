## CHAPTER 17 Markov Chains

## Real-Life Application—Forest Cover Change Prediction Using Markov Chain Model: A Case Study on Sub-Himalayan Town Gangtok, India

This case assesses the present and future land use and land cover in the sub-Himalayan capital Gangtok, India. Increasing population has resulted in converting forested land for agricultural use and urban development. Time-series satellite imageries, used for monitoring changes in environmental conditions, are the basis for representing the different states of forest changes (urbanization, agriculture, forest land) in terms of a Markov chain transition probabilities. The Markov chain model is then used to predict future land use in the study area. Case 15 in Chapter 26 on the website provides the details.

### 17.1 DEFINITION OF A MARKOV CHAIN

Let ${X}_{t}$ be a random variable that characterizes the state of the system at discrete points in time $t = 1,2,\ldots$ . The family of random variables $\left\{  {X}_{t}\right\}$ forms a stochastic process with a finite or infinite number of states.

## Example 17.1-1 (Machine Maintenance)

The condition of a machine at the time of the monthly preventive maintenance is fair, good, or excellent. For month $t$ , the stochastic process for this situation can be represented as follows:

$$
{X}_{t} = \left\{  \begin{array}{l} 0,\text{ if the condition is poor } \\  1,\text{ if the condition is fair } \\  2,\text{ if the condition is good } \end{array}\right\}  , t = 1,2,\ldots
$$

The random variable ${X}_{t}$ is finite because it represents three states: poor (0), fair (1), and good (2).

## Example 17.1-2 (Job Shop)

Jobs arrive randomly at a shop at the rate of 5 jobs per hour. The arrival process follows a Poisson distribution, which, theoretically, allows any number of jobs to arrive at the shop during the time interval $\left( {0, t}\right)$ . The infinite-state process describing the number of arriving jobs is ${X}_{t} = 0,1,2,\ldots , t > 0.$

Markov process. A stochastic process is a Markov process if a future state depends only on the immediately preceding state. This means that given the chronological times ${t}_{0},{t}_{1},\ldots ,{t}_{n}$ , the family of random variables $\left\{  {X}_{{t}_{n}}\right\}   = \left\{  {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right\}$ is a Markov process if

$$
P\left\{  {{X}_{{t}_{n}} = {x}_{n} \mid  {X}_{{t}_{n - 1}} = {x}_{n - 1},\ldots ,{X}_{{t}_{0}} = {x}_{0}}\right\}   = P\left\{  {{X}_{{t}_{n}} = {x}_{n} \mid  {X}_{{t}_{n - 1}} = {x}_{n - 1}}\right\}
$$

In a Markovian process with $n$ exhaustive and mutually exclusive states, the probabilities at a specific point in time $t = 0,1,2,\ldots$ are defined as

$$
{p}_{ij} = P\left\{  {{X}_{t} = j \mid  {X}_{t - 1} = i}\right\}  , i = 1,2,\ldots , n, j = 1,2,\ldots , n, t = 0,1,2,\ldots , T
$$

This is known as the one-step transition probability of moving from state $i$ at $t - 1$ to state $j$ at $t$ . By definition, we have

$$
\mathop{\sum }\limits_{j}{p}_{ij} = 1, i = 1,2,\ldots , n
$$

$$
{p}_{ij} \geq  0,\left( {i, j}\right)  = 1,2,\ldots , n
$$

The one-step transition probabilities can be presented in matrix form as:

$$
\mathbf{P} = \left( \begin{array}{lllll} {p}_{11} & {p}_{12} & {p}_{13} & \ldots & {p}_{1n} \\  {p}_{21} & {p}_{22} & {p}_{23} & \ldots & {p}_{2n} \\  \ldots & \ldots & \ldots & \ldots & \ldots \\  {p}_{n1} & {p}_{n2} & {p}_{n3} & \ldots & {p}_{nn} \end{array}\right)
$$

The matrix $\mathbf{P}$ defines a Markov chain. It has the property that all its transition probabilities ${p}_{ij}$ are stationary and independent over time. Although a Markov chain may include an infinite number of states, the presentation in this chapter is limited to finite chains only, as this is the only type needed in the text.

## Example 17.1-3 (The Gardener Problem)

Every year, during the March-through-September growing season, a gardener uses a chemical test to check soil condition. Depending on the outcome of the test, productivity for the new season can be one of three states: (1) good, (2) fair, and (3) poor. Over the years, the gardener has observed that last year's soil condition impacts current year's productivity and that the situation can be described by the following Markov chain:

![bo_d56m5fn7aajc73800nf0_2_738_196_477_316_0.jpg](bo_d56m5fn7aajc73800nf0_2_738_196_477_316_0.jpg)

The transition probabilities show that the soil condition can either deteriorate or stay the same but never improve. For example, if this year's soil condition is good (state 1), there is a 20% chance it will not change next year, a 50% chance it will be fair (state 2), and a 30% chance it will deteriorate to a poor condition (state 3). The gardener alters the transition probabilities $\mathbf{P}$ by using organic fertilizer. In this case, the transition matrix becomes:

$$
{\mathbf{P}}_{1} = \frac{1}{2}\left( \begin{matrix} {.30} & {.60} & {.10} \\  {.10} & {.60} & {.30} \\  {.05} & {.40} & {.55} \end{matrix}\right)
$$

The use of fertilizer can lead to improvement in soil condition.

## Aha! Moment: Spammers Go Markovian!

A while back I received an email from an unknown source. The message was syntactically correct but its content was nonsensical (e.g., "In a model, he has all solutions in parallel when it comes across 10 it emits 0."). I discarded the email and assumed that the sender's command of English was to blame. When the same experience was repeated in new emails, I decided to do a bit of research. It turned out that these syntactically correct but otherwise nonsensical inserts are totally computer generated and are used by spammers to bypass spam filters. Interestingly, the computer code used to generate these messages has its roots in Markov chains. The idea is to scan through a text (a paragraph, a chapter, or an entire book) to create a table that tallies the frequencies a word in the text is followed by other words. For example, in the text "It is not what you say; it is what you do." the states of the Markov chain are represented by 7 words ( 8 , if It and it are distinguishable) and two punctuations. There is a 100% chance that ${It}$ (or ${it}$ ) is followed by is, and a 50-50 chance that is is followed by either not or what. Following this logic, the entire Markov chain can be populated with the transition probabilities. Once done, a new text can be generated by starting at a random state (e.g., what) and then randomly deciding what the next word (or punctuation) should be. The next word is then used to decide on the succeeding word, and so on. Further refinements are of course needed to ensure that syntactical correctness and other desired features are accounted for.

Spammers are not the only users of this Markov model. The same model is used satirically as parody generator. The idea has also been used to compare styles of writing of different authors.

### 17.2 ABSOLUTE AND n-STEP TRANSITION PROBABILITIES

Given the transition matrix $\mathbf{P}$ of a Markov chain and the initial probabilities vector ${\mathbf{a}}^{\left( 0\right) } = \left\{  {{a}_{j}^{\left( 0\right) }, j = 1,2,\ldots , n}\right\}$ , the absolute probabilities ${\mathbf{a}}^{\left( n\right) } = \left\{  {{a}_{j}^{\left( n\right) }, j = 1,2,\ldots , n}\right\}$ after $n\left( { > 0}\right)$ transitions are computed as follows:

$$
{\mathbf{a}}^{\left( 1\right) } = {\mathbf{a}}^{\left( 0\right) }\mathbf{P}
$$

$$
{\mathbf{a}}^{\left( 2\right) } = {\mathbf{a}}^{\left( 1\right) }\mathbf{P} = {\mathbf{a}}^{\left( 0\right) }\mathbf{{PP}} = {\mathbf{a}}^{\left( 0\right) }{\mathbf{P}}^{2}
$$

$$
{\mathbf{a}}^{\left( 3\right) } = {\mathbf{a}}^{\left( 2\right) }\mathbf{P} = {\mathbf{a}}^{\left( 0\right) }{\mathbf{P}}^{2}\mathbf{P} = {\mathbf{a}}^{\left( 0\right) }{\mathbf{P}}^{3}
$$

$$
\text{ : }
$$

$$
{\mathbf{a}}^{\left( n\right) } = {\mathbf{a}}^{\left( 0\right) }{\mathbf{P}}^{n}
$$

The matrix ${\mathbf{P}}^{n}$ is known as the $n$ -step transition matrix. From these calculations, we can see that

$$
{\mathbf{P}}^{n} = {\mathbf{P}}^{n - 1}\mathbf{P}
$$

and

$$
{\mathbf{P}}^{n} = {\mathbf{P}}^{n - m}{\mathbf{P}}^{m},0 < m < n
$$

These are known as Chapman-Kolomogorov equations.

Example 17.2-1

The following transition matrix applies to the gardener problem with fertilizer (Example 17.1-3):

$$
\mathbf{P} = \frac{1}{2}\left( \begin{matrix} {.3} & {.60} & {.10} \\  {.30} & {.60} & {.30} \\  {.10} & {.60} & {.35} \end{matrix}\right)
$$

The initial condition of the soil is good-that is ${\mathbf{a}}^{\left( 0\right) } = \left( {1,0,0}\right)$ . Determine the absolute probabilities of the three states of the system after 1, 8, and 16 gardening seasons.

$$
{\mathbf{P}}^{8} = {\left( \begin{matrix} {.30} & {.60} & {.10} \\  {.10} & {.60} & {.30} \\  {.05} & {.40} & {.55} \end{matrix}\right) }^{8} = \left( \begin{matrix} {.101753} & {.525514} & {.372733} \\  {.101702} & {.525435} & {.372863} \\  {.101669} & {.525384} & {.372863} \end{matrix}\right)
$$

$$
{\mathbf{P}}^{16} = {\left( \begin{matrix} {.30} & {.60} & {.10} \\  {.10} & {.60} & {.30} \\  {.05} & {.40} & {.55} \end{matrix}\right) }^{16} = \left( \begin{matrix} {.101659} & {.52454} & {.372881} \\  {.101659} & {.52454} & {.372881} \\  {.101659} & {.52454} & {.372881} \end{matrix}\right)
$$

Thus, the required absolute probabilities are computed as

$$
{\mathbf{a}}^{\left( 1\right) } = \left( \begin{array}{lll} 1 & 0 & 0 \end{array}\right) \left( \begin{matrix} {.30} & {.60} & {.10} \\  {.10} & {.60} & {.30} \\  {.05} & {.40} & {.55} \end{matrix}\right)  = \left( \begin{array}{lll} {.30} & {.60} & {.1} \end{array}\right)
$$

$$
{\mathbf{a}}^{\left( 8\right) } = \left( \begin{array}{lll} 1 & 0 & 0 \end{array}\right) \left( \begin{array}{lll} {.101753} & {.525514} & {.372733} \\  {.101702} & {.525435} & {.372863} \\  {.101669} & {.525384} & {.372863} \end{array}\right)  = \left( \begin{array}{lll} {.101753} & {.525514} & {.372733} \end{array}\right) \tag{.372733}
$$

$$
{\mathbf{a}}^{\left( {16}\right) } = \left( \begin{array}{lll} 1 & 0 & 0 \end{array}\right) \left( \begin{array}{lll} {.101659} & {.52454} & {.372881} \\  {.101659} & {.52454} & {.372881} \\  {.101659} & {.52454} & {.372881} \end{array}\right)  = \left( \begin{array}{lll} {.101659} & {.52454} & {.372881} \end{array}\right)
$$

The rows of ${\mathbf{P}}^{8}$ and the vector of absolute probabilities ${\mathbf{a}}^{\left( 8\right) }$ are almost identical. The result is more evident for ${\mathbf{P}}^{16}$ . It demonstrates that, as the number of transitions increases, the absolute probabilities become independent of the initial ${\mathbf{a}}^{\left( 0\right) }$ . The resulting probabilities are known as the steady-state probabilities.

Remarks. The computations associated with Markov chains are tedious. Template excelMarkovChains.xls provides a general easy-to-use spreadsheet for carrying out these calculations (see the Excel Moment following Example 17.4-1).

### 17.3 CLASSIFICATION OF THE STATES IN A MARKOV CHAIN

The states of a Markov chain can be classified based on the transition probability ${p}_{ij}$ of $\mathbf{P}$ .

1. A state $j$ is absorbing if it is certain to return to itself in one transition-that is ${p}_{jj} = 1$ .

2. A state $j$ is transient if it can reach another state but cannot be reached back from another state. Mathematically, this will happen if $\mathop{\lim }\limits_{{n \rightarrow  \infty }}{p}_{ij}^{\left( n\right) } = 0$ , for all $i$ .

3. A state $j$ is recurrent if the probability of being revisited from other states is 1 . This can happen if, and only if, the state is not transient.

4. A state $j$ is periodic with period $t > 1$ if a return is possible only in $t,{2t},{3t},\ldots$ steps. This means that ${p}_{jj}^{\left( n\right) } = 0$ when $n$ is not divisible by $t$ .

Based on the given definitions, a finite Markov chain cannot consist of all-transient states because, by definition, the transient property requires entering other "trapping" states and never revisiting the transient state. The "trapping" state need not be a single absorbing state. For example, consider the chain

$$
\mathbf{P} = \left( \begin{array}{llll} 0 & 1 & 0 & 0 \\  0 & 0 & 1 & 0 \\  0 & 0 & {.3} & {.7} \\  0 & 0 & {.4} & {.6} \end{array}\right)
$$

States 1 and 2 are transient because they cannot be reentered once the system is "trapped" in states 3 and 4. States 3 and 4, in a way playing the role of an absorbing state, constitute a closed set. By definition, all the states of a closed set must communicate, which means that it is possible to go from any state to every other state in the set in one or more transitions-that is, ${p}_{ii}^{\left( n\right) } > 0$ for all $i \neq  j$ and $n \geq  1$ . Notice that each of states 3 and 4 can be absorbing if ${p}_{33} = {p}_{44} = 1$ . In such a case, each state forms a closed set.

A closed Markov chain is said to be ergodic if all its states are recurrent and aperiodic (not periodic). In this case, the absolute probabilities after $n$ transitions, ${\mathbf{a}}^{\left( n\right) } = {\mathbf{a}}^{\left( 0\right) }{\mathbf{P}}^{n}$ , always converge uniquely to a limiting (steady-state) distribution that is independent of the initial probabilities ${\mathbf{a}}^{\left( 0\right) }$ , as will be shown in Section 17.4.

## Example 17.3-1 (Absorbing and Transient States)

Consider the gardener Markov chain with no fertilizer:

$$
\mathbf{P} = \left( \begin{matrix} {.2} & {.5} & {.3} \\  0 & {.5} & {.5} \\  0 & 0 & 0 \end{matrix}\right)
$$

States 1 and 2 are transient because they can reach state 3 but can never be reached back. State 3 is absorbing because ${p}_{33} = 1$ . These classifications can also be seen when $\mathop{\lim }\limits_{{n \rightarrow  \infty }}{p}_{ij}^{\left( n\right) } = 0$ is computed. For example, consider

$$
{\mathbf{P}}^{100} = \left( \begin{array}{lll} 0 & 0 & 1 \\  0 & 0 & 1 \\  0 & 0 & 1 \end{array}\right)
$$

The result shows that, in the long run, the probability of reentering transient state 1 or 2 is zero, and the probability of being "trapped" in absorbing state 3 is certain.

## Example 17.3-2 (Periodic States)

We can test the periodicity of a state by computing ${\mathbf{P}}^{n}$ and observing the values of ${p}_{ii}^{\left( n\right) }$ for $n = 2,3,4,\ldots$ These values will be positive only at the corresponding period of the state. For example, consider

$$
\mathbf{P} = \left( \begin{matrix} 0 & {.6} & {.4} \\  0 & 1 & 0 \\  {.6} & {.4} & 0 \end{matrix}\right) ,{\mathbf{P}}^{2} = \left( \begin{matrix} {.24} & {.76} & 0 \\  0 & 1 & 0 \\  0 & {.76} & {.24} \end{matrix}\right) ,{\mathbf{P}}^{3} = \left( \begin{matrix} 0 & {.904} & {.0960} \\  0 & 1 & 0 \\  {.144} & {.856} & 0 \end{matrix}\right)
$$

$$
{\mathbf{P}}^{4} = \left( \begin{matrix} {.0567} & {.9424} & 0 \\  0 & 1 & 0 \\  0 & {.9424} & {.0576} \end{matrix}\right) ,{\mathbf{P}}^{5} = \left( \begin{matrix} 0 & {.97696} & {.02304} \\  0 & 1 & 0 \\  {.03456} & {.96544} & 0 \end{matrix}\right)
$$

The results show that ${p}_{11}$ and ${p}_{33}$ are positive for even values of $n$ and zero otherwise (you can confirm this observation by computing ${\mathbf{P}}^{n}$ for $n > 5$ ). This means that each of states 1 and 3 has period $t = 2$ .

### 17.4 STEADY-STATE PROBABILITIES AND MEAN RETURN TIMES OF ERGODIC CHAINS

In an ergodic Markov chain, the steady-state probabilities are defined as

$$
{\pi }_{j} = \mathop{\lim }\limits_{{n \rightarrow  \infty }}{a}_{j}^{\left( n\right) },\;j = 0,1,2,\ldots
$$

These probabilities, which are independent of $\left\{  {a}_{j}^{\left( 0\right) }\right\}$ , can be determined from the equations

$$
\pi  = \pi \mathbf{P}
$$

$$
\mathop{\sum }\limits_{j}{\pi }_{j} = 1
$$

(One of the equations in $\mathbf{\pi } = \mathbf{{\pi P}}$ is redundant.) What $\mathbf{\pi } = \mathbf{{\pi P}}$ says is that the probabilities $\mathbf{\pi }$ remain unchanged after an additional transition, and for this reason, they represent the steady-state distribution.

A direct by-product of the steady-state probabilities is the determination of the expected number of transitions before the system returns to a state $j$ for the first time. This is known as the mean first return time or the mean recurrence time, and it is computed in an $n$ -state Markov chain as

$$
{\mu }_{jj} = \frac{1}{{\pi }_{j}}, j = 1,2,\ldots , n
$$

## Example 17.4-1

To determine the steady-state probability distribution of the gardener problem with fertilizer (Example 17.1-3), we have

$$
\left( {{\pi }_{1}{\pi }_{2}{\pi }_{3}}\right)  = \left( {{\pi }_{1}{\pi }_{2}{\pi }_{3}}\right) \left( \begin{array}{lll} {.3} & {.6} & {.1} \\  {.1} & {.6} & {.3} \\  {.05} & {.4} & {.55} \end{array}\right)
$$

or

$$
{\pi }_{1} = {.3}{\pi }_{1} + {.1}{\pi }_{2} + {.05}{\pi }_{3}
$$

$$
{\pi }_{2} = {.6}{\pi }_{1} + {.6}{\pi }_{2} + {.4}{\pi }_{3}
$$

$$
{\pi }_{3} = {.1}{\pi }_{1} + {.3}{\pi }_{2} + {.55}{\pi }_{3}
$$

$$
{\pi }_{1} + {\pi }_{2} + {\pi }_{3} = 1
$$

(Any one of the first three equations is redundant.) The solution is ${\pi }_{1} = {0.1017},{\pi }_{2} = {0.5254}$ , and ${\pi }_{3} = {0.3729}$ -meaning that in the long run the soil condition will be good 10% of the time, fair 52% of the time, and poor 37% of the time.

The mean first return times are computed as

$$
{\mu }_{11} = \frac{1}{.1017} = {9.83},{\mu }_{22} = \frac{1}{.5254} = {1.9},{\mu }_{33} = \frac{1}{.3729} = {2.68}
$$

This means that, on the average, it will take approximately 10 gardening seasons for the soil to return to a good state, 2 seasons to return to a fair state, and 3 seasons to return to a poor state. These results point to a less promising outlook for the soil condition under the proposed use of fertilizers. A more aggressive program should improve the picture. For example, consider the following transition matrix in which the probabilities of moving to a good state are higher than in the previous matrix:

$$
\mathbf{P} = \left( \begin{array}{lll} {.35} & {.6} & {.05} \\  {.3} & {.6} & {.1} \\  {.25} & {.4} & {.35} \end{array}\right)
$$

In this case, ${\pi }_{1} = {0.31},{\pi }_{2} = {0.58}$ , and ${\pi }_{3} = {0.11}$ , which yields ${\mu }_{11} = {3.2},{\mu }_{22} = {1.7}$ , and ${\mu }_{33} = {8.9}$ , a reversal of the bleak outlook given previously.

![bo_d56m5fn7aajc73800nf0_7_376_205_1123_600_0.jpg](bo_d56m5fn7aajc73800nf0_7_376_205_1123_600_0.jpg)

FIGURE 17.1

Excel spreadsheet for Markov chain computations (file excelMarkov Chains.xls)

## Excel Moment

Figure 17.1 applies the general Excel template excelMarkovChains.xls to the gardener example. The template computes $n$ -step, absolute, and steady-state probabilities, and mean return time for any Markov chain. The steps are self-explanatory. In step 2a, you may override the default state codes $\left( {1,2,3,\ldots }\right)$ by a code of your choice, and then click the button located in cell L2. The new codes will automatically transfer throughout the spreadsheet when you execute step 4.

## Example 17.4-2 (Cost Model)

Consider the gardener problem with fertilizer (Example 17.1-3). The garden needs two bags of fertilizer if the soil is good. The amount is increased by 25% if the soil is fair and 60% if the soil is poor. The cost of the fertilizer is \$50 per bag. The gardener estimates an annual yield of \$250 if no fertilizer is used and \$420 if fertilizer is applied. Is it economical to use fertilizer?

Using the steady-state probabilities in Example 17.4-1, we get

$$
\text{ Expected annual cost of fertilizer } = 2 \times  \$ {50} \times  {\pi }_{1} + \left( {{1.25} \times  2}\right)  \times  \$ {50} \times  {\pi }_{2}
$$

$$
+ \left( {{1.60} \times  2}\right)  \times  \$ {50} \times  {\pi }_{3}
$$

$$
= {100} \times  {.1017} + {125} \times  {.5254} + {160} \times  {.3729}
$$

$$
= \$ {135.51}
$$

Differential increase in the annual value of the yield $= \$ {420} - \$ {250} = \$ {170}$

The use of fertilizer is recommended.

### 17.5 FIRST PASSAGE TIME

In Section 17.4, we used the steady-state probabilities to compute ${\mu }_{jj}$ , the mean first return time for state $j$ . In this section, we are concerned with the mean first passage time ${\mu }_{ij}$ , defined as the expected number of transitions to reach state $j$ from state $i$ for the first time. The calculations are rooted in the determination of the probability of at least one passage from state $i$ to state $j$ , defined as ${f}_{ij} = \mathop{\sum }\limits_{{n = 1}}^{\infty }{f}_{ij}^{\left( n\right) }$ , where ${f}_{ij}^{\left( n\right) }$ is the probability of a first passage from state $i$ to state $j$ in $n$ transitions.

1. If ${f}_{ij} < 1$ , it is not certain that the system will ever pass from state $i$ to state $j$ and ${\mu }_{ij} = \infty$ .

2. If ${f}_{ij} = 1$ , the Markov chain is ergodic, and the mean first passage time from state $i$ to state $j$ is computed as

$$
{\mu }_{ij} = \mathop{\sum }\limits_{{n = 1}}^{\infty }n{f}_{ij}^{\left( n\right) }
$$

A straightforward way to compute ${\mu }_{ij}$ is to use the following idea: a return from state $i$ to state $j$ can occur in one transition with probability ${p}_{ij}$ , or it can occur by transiting through another state $k$ with probability ${p}_{ik}$ followed by a transition from $k$ to $j$ , either directly or through (multiple) other states. In the first case the length of the transition is 1, and the second the expected transition length is $1 + {\mu }_{kj}$ . This translates into the following equation

$$
{\mu }_{ij} = 1{p}_{ij} + \mathop{\sum }\limits_{{k \neq  j}}\left( {1 + {\mu }_{kj}}\right) {p}_{ik} = \mathop{\sum }\limits_{k}{p}_{ik} + \mathop{\sum }\limits_{{k \neq  j}}{\mu }_{kj}{p}_{ik} = 1 + \mathop{\sum }\limits_{{k \neq  j}}{\mu }_{kj}{p}_{ik}
$$

or, for Markov chain with $m$ states, we have

$$
{\mu }_{ij} - \mathop{\sum }\limits_{{k \neq  j}}{\mu }_{kj}{p}_{ik} = 1, i, j = 1,2,\ldots , m
$$

These long-form equations reduce neatly to the following matrix form as is demonstrated in the Example 17.5-1

$$
\begin{Vmatrix}{\mu }_{ij}\end{Vmatrix} = {\left( \mathbf{I} - {\mathbf{N}}_{j}\right) }^{-1}\mathbf{1}, j \neq  i
$$

where

$\mathbf{I} = \left( {m - 1}\right)$ -identity matrix

${\mathbf{N}}_{j} =$ transition matrix $\mathbf{P}$ less its $j$ th row and $j$ th column of target state $j$

$\mathbf{1} = \left( {m - 1}\right)$ column vector with all elements equal to 1

The matrix operation ${\left( \mathbf{I} - {\mathbf{N}}_{j}\right) }^{-1}\mathbf{1}$ essentially sums the columns of ${\left( \mathbf{I} - {\mathbf{N}}_{j}\right) }^{-1}$ .

## Example 17.5-1

Consider the gardener Markov chain with fertilizers once again.

$$
\mathbf{P} = \left( \begin{array}{lll} {.30} & {.60} & {.10} \\  {.10} & {.60} & {.30} \\  {.05} & {.40} & {.55} \end{array}\right)
$$

To demonstrate the computation of the first passage time to a specific state from all others, consider the passage from states 2 and 3 (fair and poor) to state 1 (good)-meaning $j = 1$ .

First we use the long-form equations to justify the use of the matrix formula given above:

$$
{\mu }_{21} - {.60}{\mu }_{21} - {.30}{\mu }_{31} = 1
$$

$$
{\mu }_{31} - {.40}{\mu }_{21} - {.55}{\mu }_{31} = 1
$$

These equations can be written in matrix form as

$$
\left\lbrack  {\left( \begin{array}{ll} 1 & 0 \\  0 & 1 \end{array}\right)  - \left( \begin{array}{ll} {.60} & {.30} \\  {.40} & {.55} \end{array}\right) }\right\rbrack  \mathbf{\mu } = \left( \begin{array}{l} 1 \\  1 \end{array}\right)
$$

or,

$$
\left\lbrack  {\mathbf{I} - {\mathbf{N}}_{1}}\right\rbrack  \mathbf{\mu } = \mathbf{1} \Rightarrow  \mathbf{\mu } = {\left\lbrack  \mathbf{I} - {\mathbf{N}}_{1}\right\rbrack  }^{-1}\mathbf{1}
$$

Continuing with example,

$$
{\left( \mathbf{I} - {\mathbf{N}}_{1}\right) }^{-1} = {\left( \begin{array}{rr} {.4} &  - {.3} \\   - {.4} & {.45} \end{array}\right) }^{-1} = \left( \begin{array}{ll} {7.50} & {5.00} \\  {6.67} & {6.67} \end{array}\right)
$$

Thus,

$$
\left( \begin{array}{l} {\mu }_{21} \\  {\mu }_{31} \end{array}\right)  = \left( \begin{array}{ll} {7.50} & {5.00} \\  {6.67} & {6.67} \end{array}\right) \left( \begin{array}{l} 1 \\  1 \end{array}\right)  = \left( \begin{array}{l} {12.50} \\  {13.34} \end{array}\right)
$$

Thus, on the average, it will take 12.5 seasons to pass from fair to good soil, and 13.34 seasons to go from bad to good soil.

Similar calculations can be carried out to obtain ${\mu }_{12}$ and ${\mu }_{32}$ from $\left( {\mathbf{I} - {\mathbf{N}}_{2}}\right)$ and ${\mu }_{13}$ and ${\mu }_{23}$ from $\left( {\mathbf{I} - {\mathbf{N}}_{3}}\right)$ , as demonstrated in Excel moment below.

## Excel Moment

Excel template excelFirstPassTime.xls can be used to carry out the calculations of the mean first passage times. Figure 17.2 shows the calculations associated with Example 17.5-1. Step 2 of the spreadsheet automatically initializes the transition matrix $\mathbf{P}$ to zero values per the size given in step 1. In step 2a, you may override the default state codes in row 6 with a code of your choice. The code is then transferred automatically throughout the spreadsheet. After you enter the transition probabilities, step 3 creates the matrix $\mathbf{I} - \mathbf{P}$ . Step 4 is carried out entirely by you using $\mathbf{I} - \mathbf{P}$ as the source for creating $\mathbf{I} - {\mathbf{N}}_{j}\left( {j = 1,2\text{ , and 3 }}\right)$ . You can do so by copying the entire $\mathbf{I} - \mathbf{P}$ and its state codes and pasting it in the target location and then using appropriate Excel Cut and Paste operations to rid $\mathbf{I} - \mathbf{P}$ of row $j$ and column $j$ . For example, to create $\mathbf{I} - {\mathbf{N}}_{2}$ , first copy $\mathbf{I} - \mathbf{P}$ and its state codes to the selected target location. Next, highlight column 3 of the copied matrix, cut it, and paste it in column 2, thus eliminating column 2. Similarly, highlight row 3 of the resulting matrix, cut it, and then paste it in row 2, thus eliminating row 2. The created $\mathbf{I} - {\mathbf{N}}_{2}$ automatically carries its correct state code.

Once $\mathbf{I} - {\mathbf{N}}_{j}$ is created, the inverse, ${\left( \mathbf{I} - {\mathbf{N}}_{j}\right) }^{-1}$ , is computed in the target location. The associated operations are demonstrated by inverting $\left( {\mathbf{I} - {\mathbf{N}}_{1}}\right)$ in Figure 17.2:

1. Enter the formula $=$ MINVERSE(B18:C19) in E18.

2. Highlight E18:F19, the area where the inverse will reside.

3. Press F2.

4. Press CTRL + SHIFT + ENTER.

![bo_d56m5fn7aajc73800nf0_10_398_204_1165_1086_0.jpg](bo_d56m5fn7aajc73800nf0_10_398_204_1165_1086_0.jpg)

FIGURE 17.2

Excel spreadsheet calculations of first passage time of Example 17.5-1 (file excelFirstPassTime.xls)

The values of the first passage times from states 2 and 3 to state 1 are then computed by summing the rows of the inverse-that is, by entering = SUM(E18:F18) in H18 and then copying H18 into H19. After creating $\mathbf{I} - \mathbf{N}$ for $i = 2$ and $i = 3$ , the remaining calculations are automated by copying E18:F19 into E22:F23 and E26:F27, and copying H18:H19 into H22:H23 and H26:H27.

### 17.6 ANALYSIS OF ABSORBING STATES

In the gardener problem, without fertilizer the transition matrix is given as

$$
\mathbf{P} = \left( \begin{matrix} {.2} & {.5} & {.3} \\  0 & {.5} & {.5} \\  0 & 0 & 1 \end{matrix}\right)
$$

States 1 and 2 (good and fair soil conditions) are transient, and State 3 (poor soil condition) is absorbing, because once in that state the system will remain there indefinitely. A Markov chain may have more than one absorbing state. For example, an employee may remain employed with the same company until full retirement or may quit early (two absorbing states). In these types of chains, we are interested in determining the probability of reaching absorption and the expected number of transitions to absorption, given that the system starts in a specific transient state. For example, in the gardener Markov chain given above, if the soil is currently good, we will be interested in determining the average number of gardening seasons till the soil becomes poor and also the probability associated with this transition.

The analysis of Markov chains with absorbing states can be carried out conveniently using matrices. First, the Markov chain is partitioned in the following manner:

$$
\mathbf{P} = \left( \begin{matrix} \mathbf{N} & \mathbf{A} \\  \mathbf{0} & \mathbf{I} \end{matrix}\right)
$$

The arrangement requires all the absorbing states to occupy the southeast corner of the new matrix. For example, consider the following transition matrix:

$$
\mathbf{P} = \begin{array}{llll} 1 & 2 & 3 & 4 \\  2 & {.3} & {.4} & {.1} \\  0 & 1 & 0 & 0 \\  5 & {.3} & 0 & {.2} \\  0 & 0 & 0 & 1 \end{array}
$$

The matrix $\mathbf{P}$ can be rearranged and partitioned as

$$
{\mathbf{P}}^{ * } = \begin{array}{llll} 1 & 3 & 2 & 4 \\  2 & 4 & 3 & {.1} \\  3 & 0 & 3 & {.2} \\  4 & 0 & 0 & 1 \\  0 & 0 & 1 & 0 \\  0 & 0 & 0 & 1 \end{array}
$$

In this case, we have

$$
\mathbf{N} = \left( \begin{array}{ll} {.2} & {.4} \\  {.5} & 0 \end{array}\right) ,\mathbf{A} = \left( \begin{array}{ll} {.3} & {.1} \\  {.3} & {.2} \end{array}\right) ,\mathbf{I} = \left( \begin{array}{ll} 1 & 0 \\  0 & 1 \end{array}\right)
$$

Given the definition of $\mathbf{A}$ and $\mathbf{N}$ and the unit column vector1(of all 1 elements), it can be shown that

Expected time in state $j$ starting in state $i =$ element $\left( {i, j}\right)$ of ${\left( \mathbf{I} - \mathbf{N}\right) }^{-1}$

Expected time to absorption $= {\left( \mathbf{I} - \mathbf{N}\right) }^{-1}\mathbf{1}$

Probability of absorption $= {\left( \mathbf{I} - \mathbf{N}\right) }^{-1}\mathbf{A}$

Example 17.6-1

A product is processed on two sequential machines, I and II. Inspection takes place after a product unit is completed on either machine. There is a 5% chance that the unit will be junked before inspection. After inspection, there is a 3% chance the unit will be junked, and a 7% chance of being returned to the same machine for reworking. Else, a unit passing inspection on both machines is good.

---

${}^{1}$ Adapted from J. Shamblin and G. Stevens, Operations Research: A Fundamental Approach, McGraw-Hill, New York, Chapter 4, 1974.

---

(a) For a part starting at machine I, determine the average number of visits to each state.

(b) If a batch of 1000 units is started on machine I, determine the average number of completed good units.

For the Markov chain, the production process has 6 states: start at I (s1), inspect after I (i1), start at II (s2), inspect after II (i2), junk after inspection I or II $\left( J\right)$ , and good after II $\left( G\right)$ . States $J$ and $G$ are absorbing states. The transition matrix is given as

$$
\mathbf{P} = \begin{matrix} {s1} & {i1} & {s2} & {i2} & J & G \\  {s1} & {0.95} & 0 & 0 & {0.5} & 0 \\  {i1} & {.07} & 0 & {.9} & {0.3} & {0.3} \\  0 & 0 & 0 & {0.95} & {0.5} & {0.5} \\  0 & 0 & {0.07} & 0 & {0.3} & {0.9} \\  0 & 0 & 0 & 0 & 1 & 0 \\  0 & 0 & 0 & 0 & 0 & 1 \end{matrix}
$$

Thus,

![bo_d56m5fn7aajc73800nf0_12_634_1075_695_246_0.jpg](bo_d56m5fn7aajc73800nf0_12_634_1075_695_246_0.jpg)

Using the spreadsheet calculations in excelEx17.6-1.xls (see the Excel Moment following Example 17.5-1), we get

$$
{\left( \mathbf{I} - \mathbf{N}\right) }^{-1} = {\left( \begin{matrix} 1 &  - {.95} & 0 & 0 \\   - {.07} & 1 &  - {.9} & 0 \\  0 & 0 & 0 &  - {.95} \\  0 & 0 &  - {.07} & 1 \end{matrix}\right) }^{-1} = \left( \begin{matrix} {1.07} & {1.02} & {.98} & {0.93} \\  {0.07} & {1.07} & {1.03} & {0.98} \\  0 & 0 & {1.07} & {1.02} \\  0 & 0 & {1.07} & {1.02} \end{matrix}\right)
$$

$$
{\left( \mathbf{I} - \mathbf{N}\right) }^{-1}\mathbf{A} = \left( \begin{matrix} {1.07} & {1.02} & {.98} & {0.93} \\  {0.07} & {1.07} & {1.03} & {0.98} \\  0 & 0 & {1.07} & {1.02} \\  0 & 0 & {0.07} & {1.07} \end{matrix}\right) \left( \begin{matrix} {.05} & 0 \\  {.03} & 0 \\  {.05} & 0 \\  {.03} & {.9} \end{matrix}\right)  = \left( \begin{matrix} {.16} & {.84} \\  {.12} & {.88} \\  {.08} & {.92} \\  {.04} & {.96} \end{matrix}\right)
$$

The top row of ${\left( \mathbf{I} - \mathbf{N}\right) }^{-1}$ shows that, on the average, machine I is visited 1.07 times, inspection I is visited 1.02 times, machine II is visited .98 time, and inspection II is visited .93 time. The reason the number of visits in machine I and inspection I is greater than 1 is because of rework and reinspection. On the other hand, the corresponding values for machine II are less than 1 because some parts are junked before reaching machine II. Indeed, under perfect conditions (no parts junked and no rework), the matrix ${\left( \mathbf{I} - \mathbf{N}\right) }^{-1}$ will show that each station is visited exactly once (try it by assigning a transition probability of 1 for all the states). Of course, the duration of stay in each state could differ. For example, if the processing times at machines I and II are 20 and 30 minutes and if the inspection times at I and II are 5 and 7 minutes, then a part starting at machine 1 will be processed (i.e., either junked or completed) in ${1.07} \times  {20} + {1.02} \times  5 + \; {.98} \times  {30} + {.93} \times  7 = {62.41}$ minutes.

To determine the number of completed parts in a starting batch of 1000 pieces, we can see from the top row of ${\left( \mathbf{I} - \mathbf{N}\right) }^{-1}\mathbf{A}$ that

Probability of a piece being junked $= {.16}$

Probability of a piece being completed $= {.84}$

This means that ${1000} \times  {.84} = {840}$ pieces will be completed in a starting batch of 1000 .

## BIBLIOGRAPHY

Bini, D., E. Harold, and J. Palacios, Numerical Methods for Structured Markov Chains, Oxford University Press, New York, 2005.

Cyert, R., H. Davidson, and G. Thompson, "Estimation of the Allowance for Doubtful Accounts by Markov Chains," Management Science, Vol. 8, No. 4, pp. 287-303, 1963.

Grimmet, G., and D. Stirzaker, Probability and Random Processes, 2nd ed., Oxford University Press, Oxford, England, 1992.

Pfifer, P., and R. Cassaway, "Modeling Customer Relations with Markov Chains," Journal of Interactive Marketing, Vol. 14, No. 2, pp. 43-55, 2000.

Pliskin, J., and E. Tell, "Using Dialysis Need-Projection Model for Health Planning in Massachusetts," Interfaces, Vol. 11, No. 6, pp. 84-99, 1981.

Stewart, W., Introduction to the Numerical Solution of Markov Chains, Princeton University Press, Princeton, NJ, 1995.

Tijms, H., A First Course in Stochastic Models, Wiley, New York, 2003.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>17.1</td><td>17-1 to 17-4</td></tr><tr><td>17.2</td><td>17-5 to 17-9</td></tr><tr><td>17.3</td><td>17-10 to 17-12</td></tr><tr><td>17.4</td><td>17-13 to 17-28</td></tr><tr><td>17.5</td><td>17-29 to 17-33</td></tr><tr><td>17.6</td><td>17-34 to 17-45</td></tr></table>

17-1. An engineering professor acquires a new computer once every two years. The professor can choose from three models: ${M1},{M2}$ , and ${M3}$ . If the present model is ${M1}$ , the next computer can be ${M2}$ with probability .25 or ${M3}$ with probability .1. If the present model is ${M2}$ , the probabilities of switching to ${M1}$ and ${M3}$ are.5and.15, respectively. And, if the present model is ${M3}$ , then the probabilities of purchasing ${M1}$ and ${M2}$ are .7 and .2, respectively. Represent the situation as a Markov chain.

*17-2. A police car is on patrol in a neighborhood known for its gang activities. During a patrol, there is a 60% chance of responding in time to the location where help is needed; else regular patrol will continue. Upon receiving a call, there is a 10% chance for cancellation (in which case normal patrol is resumed) and a 30% chance that the car is already responding to a previous call. When the police car arrives at the scene, there is a 10% chance that the instigators will have fled (in which case the car returns back to patrol) and a 40% chance that apprehension is made immediately. Else, the officers will search the area. If apprehension occurs, there is a 60% chance of transporting the suspects to the police station; else they are released and the car returns to patrol. Express the probabilistic activities of the police patrol in the form of transition matrix.

17-3. Cyert and Associates (1963). Bank1 offers loans which are either paid when due or are delayed. If the payment on a loan is delayed by more than 4 quarters (1 year), Bank1 considers the loan a bad debt and writes it off. The following table provides a sample of Bank1's past experience with loans.

<table><tr><td>Loan amount</td><td>Quarters late</td><td>Payment history</td></tr><tr><td>\$20,000</td><td>0</td><td>\$2000 paid, \$3000 delayed by an extra quarter, \$3000 delayed by</td></tr><tr><td>\$50,000</td><td>1</td><td>2 extra quarters, and the rest delayed 3 extra quarters. <br> \$4000 paid, \$12,000 delayed by an extra quarter, \$6000 delayed</td></tr><tr><td>\$75,000</td><td>2</td><td>by 2 extra quarters, and the rest delayed by 3 extra quarters. <br> \$7500 paid, \$15,000 delayed by an extra quarter, and the rest</td></tr><tr><td></td><td></td><td>delayed by 2 extra quarters.</td></tr><tr><td>\$84,000</td><td>3</td><td>\$42,000 paid and the rest delayed by an extra quarter.</td></tr><tr><td>\$200,000</td><td>4</td><td>\$50,000 paid.</td></tr></table>

Express Bank1's loan situation as a Markov chain.

17-4. Pliskin and Tell (1981). Patients suffering from kidney failure can either get a transplant or undergo periodic dialysis. During any one year, 30% undergo cadaveric transplants, and 10% receive living-donor kidneys. In the year following a transplant, 30% of those who receive the cadaveric transplants and 15% of living-donor recipients go back to dialysis. Death percentages among the two groups are 20% and 10%, respectively. Of those in the dialysis pool, 10% die, and of those who survive more than one year after a transplant, 5% die and 5% go back to dialysis. Represent the situation as a Markov chain.

17-5. Consider Problem 17-1. Determine the probability that the professor will purchase the current model in 4 years.

*17-6. Consider Problem 17-2. If the police car is currently at a call scene, determine the probability that an apprehension will take place in two patrols.

17-7. Consider Problem 17-3. Suppose that Bank1 currently has \$1,000,000 worth of outstanding loans. Of these, \$300,000 have just been paid, \$150,000 are one quarter late, \$250,000 are two quarters late, \$200,000 are three quarters late, and the rest are over four quarters late. What would the picture of these loans be like after two cycles of loans?

17-8. Consider Problem 17-4.

(a) For a patient who is currently on dialysis, what is the probability of receiving a transplant in two years?

(b) For a patient who is currently a more-than-one-year survivor, what is the probability of surviving four more years?

17-9. A die-rolling game uses a 4-square grid. The squares are designated clockwise as $A, B$ , $C$ , and $D$ with monetary rewards of \$4,- \$2,- \$6, and \$9, respectively. Starting at square $A$ , roll the die to determine the next square to move to in a clockwise direction. For example, if the die shows 2, we move to square C. The game is repeated using the last square as a starting point.

(a) Express the problem as a Markov chain.

(b) Determine the expected gain or loss after the die is rolled 5 times.

17-10. Classify the states of the following Markov chains. If a state is periodic, determine its period:

*(a) $\left( \begin{array}{lll} 0 & 1 & 0 \\  0 & 0 & 1 \\  1 & 0 & 0 \end{array}\right)$

*(b) $\left( \begin{matrix} \frac{1}{2} & \frac{1}{4} & \frac{1}{4} & 0 \\  0 & 0 & 1 & 0 \\  \frac{1}{3} & 0 & \frac{1}{3} & \frac{1}{3} \\  0 & 0 & 0 & 1 \end{matrix}\right)$

(c) $\left( \begin{matrix} 0 & 1 & 0 & 0 & 0 & 0 \\  0 & {.5} & {.5} & 0 & 0 & 0 \\  0 & {.7} & {.3} & 0 & 0 & 0 \\  0 & 0 & 0 & 1 & 0 & 0 \\  0 & 0 & 0 & 0 & {.4} & {.6} \\  0 & 0 & 0 & 0 & {.2} & 8 \end{matrix}\right)$

(d) $\left( \begin{matrix} {.1} & 0 & {.9} \\  {.7} & {.3} & 0 \\  {.2} & {.7} & {.1} \end{matrix}\right)$

17-11. A game involves four balls and two urns. A ball in either urn has 50:50 chance of being transferred to the other urn. Represent the game as a Markov chain, and show that its states are periodic with period $t = 2$ .

17-12. A museum has six rooms of equal sizes arranged in the form of a grid with two rows and three columns. Each interior wall has a door that connects adjacent rooms. Museum guards move about the rooms through the interior doors. Represent the movements of each guard in the museum as a Markov chain, and show that its states are periodic with period $t = 2$ .

*17-13. On a sunny day, MiniGolf can gross \$2000 in revenues. If the day is cloudy, revenues drop by 20%. A rainy day will reduce revenues by 80%. If today's weather is sunny, there is an 80% chance it will remain sunny tomorrow with no chance of rain. If it is cloudy, there is a 20% chance that tomorrow will be rainy and a 30% chance it will be sunny. Rain will continue through the next day with a probability of .8 , but there is a 10% chance it may be sunny.

(a) Determine the expected daily revenues for MiniGolf.

(b) Determine the average number of days the weather will not be sunny.

17-14. Joe loves to eat out in area restaurants. His favorite foods are Mexican, Italian, Chinese, and Thai. On the average, Joe pays \$12.00 for a Mexican meal, \$17.00 for an Italian meal, \$11.00 for a Chinese meal, and \$13.00 for a Thai meal. Joe's eating habits are predictable: There is a 70% chance that today's meal is a repeat of yesterday's and equal probabilities of switching to one of the remaining three.

(a) How much does Joe pay on the average for his daily dinner?

(b) How often does Joe eat Mexican food?

17-15. Some ex-cons spend the rest of their lives either free, on trial, in jail, or on probation. At the start of each year, statistics show that there is 50% chance that a free ex-con will commit a new crime and go on trial. The judge may send the ex-con to jail with probability .6 or grant probation with probability .4. Once in jail, 10% of ex-cons will be set free for good behavior. Of those who are on probation, 10% commit new crimes and are arraigned for new trials, 50% will go back to finish their sentence for violating probation orders, and 10% will be set free for lack of evidence. Taxpayers underwrite the cost associated with the punishment of the ex-felons. It is estimated that a trial will cost about \$8000, an average jail sentence will cost \$25,000, and an average probation period will cost \$2000.

(a) Determine the expected cost per ex-con.

(b) How often does an ex-con return to jail? Go on trial? Be set free?

17-16. A store sells a special item whose daily demand can be described by the following pdf:

<table><tr><td>Daily demand, $D$</td><td>0</td><td>1</td><td>2</td><td>3</td></tr><tr><td>$P\{ D\}$</td><td>.1</td><td>.3</td><td>.4</td><td>.2</td></tr></table>

The store, using daily review, is comparing two ordering policies: (1) Order up to 3 units if the stock level is less than 2; else do not order. (2) Order 3 units if the stock level is zero; else do not order. The fixed ordering cost per shipment is \$300, and the cost of holding excess units per unit per day is \$3. Immediate delivery is expected.

(a) Which policy should the store adopt to minimize the total expected daily cost of ordering and holding?

(b) For the two policies, compare the average number of days between successive inventory depletions.

*17-17. There are three categories of income tax filers in the United States: those who never evade taxes, those who sometimes do it, and those who always do it. An examination of audited tax returns from 1 year to the next shows that of those who did not evade taxes last year, 95% continue to be in the same category this year, 4% move to the "sometimes" category, and the remainder move to the "always" category. For those who sometimes evade taxes, 6% move to "never," 90% stay the same, and 4% move to "always." As for the "always" evaders, the respective percentages are 0%, 10%, and 90%.

(a) Express the problem as a Markov chain.

(b) In the long run, what would be the percentages of "never," "sometimes," and "always" tax categories?

(c) Statistics show that a taxpayer in the "sometimes" category evades taxes on about \$5000 per return and in the "always" category on about \$12,000. Assuming that the taxpayer population is 70 millions and that the average income tax rate is 12%, determine the annual reduction in collected taxes due to evasion.

17-18. Warehouzer owns a renewable forest land for growing pine trees. Trees can fall into one of four categories depending on their age: baby (0-5 years), young (5-10 years), mature (11-15 years), and old (more than 15 years). Ten percent of baby and young trees die before reaching the next age group. For mature and old trees, 50% are harvested and only 5% die. Because of the renewal nature of the operation, all harvested and dead tree are replaced with new (baby) trees by the end of next 5-year cycle.

(a) Express the forest dynamics as a Markov chain.

(b) If the forest land can hold a total of 1,000,000 trees, determine the long-run composition of the forest.

(c) If a new tree is planted at the cost of \$1.50 per tree and a harvested tree has a market value of \$25, determine the average annual income from the forest operation.

17-19. Population dynamics is impacted by the continual movement of people who are seeking better quality of life or better employment. The city of Mobile has an inner-city population, a suburban population, and a surrounding rural population. The census taken in 10-year intervals shows that 10% of the rural population move to the suburbs and 5% to the inner city. For the suburban population, 30% move to rural areas and 15% to the inner city. The inner-city population would not move into suburbs, but 20% of them move to the quiet rural life.

(a) Express the population dynamics as a Markov chain.

(b) If the greater Mobile area currently includes 20,000 rural residents, 100,000 suburbanites, and 30,000 inner-city inhabitants, what will the population distribution be in 10 years? In 20 years?

(c) Determine the long-run population picture of Mobile.

17-20. A car rental agency has offices in Phoenix, Denver, Chicago, and Atlanta. The agency allows one- and two-way rentals so that cars rented in one location may end up in another. Statistics show that at the end of each week 70% of all rentals are two way. As for the one-way rentals: From Phoenix, 20% go to Denver, 60% to Chicago, and the rest goes to Atlanta; from Denver, 40% go to Atlanta and 60% to Chicago; from Chicago, 50% go to Atlanta and the rest to Denver; and from Atlanta, 80% go to Chicago, 10% to Denver, and 10% to Phoenix.

(a) Express the situation as a Markov chain.

(b) If the agency starts the week with 100 cars in each location, what will the distribution be like in two weeks?

(c) If each location is designed to handle a maximum of 110 cars, would there be a long-run space availability problem in any of the locations?

(d) Determine the average number of weeks that elapse before a car is returned to its originating location.

17-21. A bookstore restocks a popular book to a level of 100 copies at the start of each day. The data for the last 30 days provide the following end-of-day inventory position:1,2,0, 3,2,1,0,0,3,0,1,1,3,2,3,3,2,1,0,2,0,1,3,0,0,3,2,1,2,2.

(a) Represent the daily inventory as a Markov chain.

(b) Determine the steady-state probability that the bookstore will run out of books in any one day.

(c) Determine the expected daily inventory.

(d) Determine the average number of days between successive zero inventories.

17-22. In Problem 17-21, suppose that the daily demand can exceed supply, which gives rise to shortage (negative inventory). The end-of-day inventory level for the past 30 days is given as: $1,2,0, - 2,2,2, - 1, - 1,3,0,0,1, - 1, - 2,3,3, - 2, - 1,0,2,0, - 1,3,0,0,3, - 1,1,2, - 2$ .

(a) Express the situation as a Markov chain.

(b) Determine the long-term probability of a surplus inventory in a day.

(c) Determine the long-term probability of a shortage inventory in a day.

(d) Determine the long-term probability that the daily supply meets the daily demand exactly.

(e) If the holding cost per (end-of-day) surplus book is \$.15 per day and the penalty cost per shortage book is \$4.00 per day, determine the expected inventory cost per day.

17-23. A store starts a week with at least 3 PCs. The demand per week is estimated at 0 with probability .15, 1 with probability .2, 2 with probability .35, 3 with probability .25, and 4 with probability .05. Unfilled demand is backlogged. The store's policy is to place an order for delivery at the start of the following week whenever the inventory level drops below 3 PCs. The new replenishment always brings the stock back to 5 PCs.

(a) Express the situation as a Markov chain.

(b) Suppose that the week starts with 4 PCs. Determine the probability that an order will be placed at the end of two weeks.

(c) Determine the long-run probability that no order will be placed in any week.

(d) If the fixed cost of placing an order is \$200, the holding cost per PC per week is \$5, and the penalty cost per shortage PC per week is \$20, determine the expected inventory cost per week.

17-24. Solve Problem 17-23, assuming that the order size, when placed, is exactly 5 pieces.

17-25. In Problem 17-24, suppose that the demand for the PCs is0,1,2,3,4, or 5 with equal probabilities. Further assume that the unfilled demand is not backlogged, but that the penalty cost is still incurred.

(a) Express the situation as a Markov chain.

(b) Determine the long-run probability that a shortage will take place.

(c) If the fixed cost of placing an order is $\$ {200}$ , the holding cost per PC per week is \$5, and the penalty cost per shortage PC per week is \$20, determine the expected ordering and inventory cost per week.

17-26. The federal government tries to boost small business activities by awarding annual grants for projects. All bids are competitive, but the chance of receiving a grant is highest if the owner has not received any during the last three years and lowest if awards were given in each of the last three years. Specifically, the probability of getting a grant if none were awarded in the last 3 years is .9. It decreases to .8 if one grant was awarded, .7 if two grants were awarded, and only .5 if 3 were received.

(a) Express the situation as a Markov chain.

(b) Determine the expected number of awards per owner per year.

17-27. Jim Bob has a history of receiving many fines for driving violations. Unfortunately for Jim Bob, modern technology can keep track of his previous fines. As soon as he has accumulated 4 tickets, his driving license is revoked until he completes a new driver education class, in which case he starts with a clean slate. Jim Bob is most reckless immediately after completing the driver education class and he is invariably stopped by the police with a 50-50 chance of being fined. After each new fine, he tries to be more careful, which reduces the probability of a fine by .1.

(a) Express Jim Bob's problem as Markov chain.

(b) What is the average number of times Jim Bob is stopped by police before his license is revoked again?

(c) What is the probability that Jim Bob will lose his license?

(d) If each fine costs \$100, how much, on the average, does Jim Bob pay between successive suspensions of his license?

17-28. The daily weather in Fayettville, Arkansas, can be cloudy (C), sunny (S), rainy (R), or windy (W). Records over the past 90 days are CCSWRRWSSCCCRCSSWRCRRRR CWSSWRWWRCRRRRCWSSWRWCCSWRRWSSCCCRCSSWSSWRWWRCR RRRCWSSWRWCCSWRRWSSS. Based on these records, use a Markov chain to determine the probability that a typical day in Fayetteville will be cloudy, sunny, rainy, or windy.

*17-29. A mouse maze consists of the paths shown in Figure 17.3. Intersection 1 is the maze entrance, and intersection 5 is the exit. At any intersection, the mouse has equal probabilities of selecting any of the available paths. When the mouse reaches intersection 5, the experiment is repeated by reentering the maze at intersection 1.

(a) Express the maze as a Markov chain.

(b) Determine the probability that, starting at intersection 1, the mouse will reach the exit after three trials.

(c) Determine the long-run probability that the mouse will locate the exit intersection.

(d) Determine the average number of trials needed to reach the exit point from intersection 1.

17-30. In Problem 17-29, intuitively, if more options (routes) are added to the maze, will the average number of trials needed to reach the exit point increase or decrease? Demonstrate the answer by adding a route between intersections 3 and 4.

17-31. Jim and Joe start a game with five tokens, three for Jim and two for Joe. A coin is tossed, and if the outcome is heads, Jim gives Joe a token; else Jim gets a token from Joe. The game ends when Jim or Joe has all the tokens. At this point, there is 30% chance that Jim and Joe will continue to play the game, again starting with three tokens for Jim and two for Joe.

(a) Represent the game as a Markov chain.

(b) Determine the probability that Joe will win in three coin tosses. That Jim will win in three coin tosses.

![bo_d56m5fn7aajc73800nf0_19_366_1825_1235_348_0.jpg](bo_d56m5fn7aajc73800nf0_19_366_1825_1235_348_0.jpg)

(c) Determine the probability that a game will end in Jim's favor. Joe's favor.

(d) Determine the average number of coin tosses needed before Jim wins. Joe wins.

17-32. An amateur gardener with training in botany is tinkering with cross-pollinating pink irises with red, orange, and white irises. Annual experiments show that pink can produce 60% pink and 40% white; red can produce 40% red, 50% pink, and 10% orange; orange can produce 25% orange, 50% pink, and 25% white; and white can produce 50% pink and 50% white.

(a) Express the gardener situation as a Markov chain.

(b) If the gardener started the cross-pollination with equal numbers of each type of iris, what would the distribution be like after 5 years? In the long run?

(c) Determine the average number of years a red iris would take to produce a white bloom

*17-33. Customers tend to exhibit loyalty to product brands but may be persuaded through clever marketing and advertising to switch brands. Consider the case of three brands: $A, B$ , and $C$ . Customer "unyielding" loyalty to a given brand is estimated at 75%, giving the competitors only a 25% margin to realize a switch. Competitors launch their advertising campaigns once a year. For brand $A$ customers, the probabilities of switching to brands $B$ and $C$ are . 1 and .15, respectively. Customers of brand $B$ are likely to switch to $A$ and $C$ with probabilities .2 and .05, respectively. Brand $C$ customers can switch to brands $A$ and $B$ with equal probabilities.

(a) Express the situation as a Markov chain.

(b) In the long run, how much market share will each brand command?

(c) How long on the average will it take for a brand $A$ customer to switch to brand $B$ ? To brand $C$ ?

17-34. In Example 17.6-1, suppose that the labor cost for machines I and II is \$25 per hour and that for inspection is only \$15 per hour. Further assume that it takes 30 minutes and 20 minutes to process a piece on machines I and II, respectively. The inspection time at each of the two stations is 10 minutes. Determine the labor cost associated with a completed (good) piece.

*17-35. When I borrow a book from the city library, I try to return it after one week. Depending on the length of the book and my free time, there is a 30% chance that I keep it for another week. If I have had the book for two weeks, there is a 10% chance that I'll keep it for an additional week. Under no condition do I keep it for more than three weeks.

(a) Express the situation as a Markov chain.

(b) Determine the average number of weeks before returning a book to the library.

17-36. In Casino del Rio, a gambler can bet in whole dollars. Each bet will either gain \$1 with probability .4 or lose \$1 with probability .6. Starting with three dollars, the gambler will quit if all money is lost or the accumulation is doubled.

(a) Express the problem as a Markov chain.

(b) Determine the average number of bets until game ends.

(c) Determine the probability of ending the game with \$6. Of losing all \$3.

17-37. Jim must make five years worth of progress to complete his doctorate degree at ABC University. However, he enjoys the life of a student and is in no hurry to finish his degree. In any academic year there is a 50% chance he may take the year off and a 50% chance of pursuing the degree full time. After completing three academic years, there is a 30% chance that Jim may "bail out" and simply get a master's degree, a 20% chance of taking the next year off but continuing in the Ph.D. program, and 50% chance of attending school full time toward his doctorate.

(a) Express Jim's situation as a Markov chain.

(b) Determine the expected number of academic years before Jim's student life comes to an end.

(c) Determine the probability that Jim will end his academic journey with only a master's degree.

(d) If Jim's fellowship pays an annual stipend of \$18,000 (but only when he attends school), how much will he be paid before ending up with a degree?

17-38. An employee who is now 55 years old plans to retire at the age of 62, but does not rule out the possibility of quitting earlier. At the end of each year, he weighs his options (and state of mind regarding work). The probability of quitting after one year is only .1 but seems to increase by approximately .01 with each additional year.

(a) Express the problem as a Markov chain.

(b) What is the probability that the employee will stay with the company until planned retirement at age 62?

(c) At age 57, what is the probability that the employee will call it quits?

(d) At age 58, what is the expected number of years before the employee is off the payroll?

17-39. In Problem 17-3,

(a) Determine the expected number of quarters until a debt is either repaid or lost as bad debt.

(b) Determine the probability that a new loan will be written off as bad debt. Repaid in full.

(c) If a loan is 6 months old, determine the number of quarters until its status is settled.

17-40. In a men's singles tennis tournament, Andre and John are playing a match for the championship. The match is won when either player wins three out of five sets. Statistics show that there is 60% chance that Andre will win any one set.

(a) Express the match as a Markov chain.

(b) On the average, how long will the match last, and what is the probability that Andre will win the championship?

(c) If the score is 1 set to 2 in John's favor, what is the probability that Andre will win?

(d) In Part (c), determine the average number of sets till the match ends, and interpret the result.

*17-41. Students at U of A have expressed dissatisfaction with the fast pace at which the math department is teaching the one-semester Cal I. To cope with this problem, the math department is now offering Cal I in 4 modules. Students will set their individual pace for each module and, when ready, will take a test that will elevate them to the next module. The tests are given once every 4 weeks, so that a diligent student can complete all 4 modules in one semester. After a couple of years with this self-paced program, 20% of the students did not complete the first module on time. The percentages for modules 2 through 4 were ${22}\% ,{25}\%$ , and ${30}\%$ , respectively.

(a) Express the problem as a Markov chain.

(b) On the average, would a student starting with module 1 at the beginning of the current semester be able to take Cal II the next semester (Cal I is a prerequisite for Cal II)?

(c) Would a student who has completed only one module last semester be able to finish Cal I by the end of the current semester?

(d) Do you recommend extending the module idea to other basic classes? Explain.

17-42. At U of A, promotion from assistant to associate professor requires the equivalent of five points (years) of acceptable performance. Performance reviews are conducted once a year, and the candidate is given an average rating, a good rating, or an excellent rating. An average rating is the same as probation, and the candidate gains no points toward promotion. A good rating is equivalent to gaining one point, and an excellent rating adds two points. Statistics show that in any year 10% of the candidates are rated average and 70% are rated good, and the rest are rated excellent.

(a) Express the problem as a Markov chain.

(b) Determine the average number of years until a new assistant professor is promoted.

17-43. Pfifer and Carraway (2000). A company targets its customers through direct mail advertising. During the first year, the probability that the customer will make a purchase is .5, which decreases to .4 in year 2, .3 in year 3, and .2 in years 4 . If no purchases are made in four consecutive years, the customer is deleted from the mailing list. Making a purchase resets the count back to zero.

(a) Express the situation as a Markov chain.

(b) Determine the expected number of years a new customer will be on the mailing list.

(c) If a customer has not made a purchase in two years, determine the expected number of years on the mailing list.

17-44. An NC machine is designed to operate properly with power voltage setting between 108 and 112 volts. If the voltage falls outside this range, the machine will stop. The power regulator for the machine can detect variations in increments of one volt. Experience shows that change in voltage takes place once every 15 minutes. Within the admissible range (118 to 112 volts), voltage can go up by 1 volt, stay the same, or go down by one volt, all with equal probabilities.

(a) Express the situation as a Markov chain.

(b) Determine the probability that the machine will stop because the voltage is low. High.

(c) What should be the ideal voltage setting that will render the longest working duration for the machine?

17-45. Consider Problem 17-4, dealing with patients suffering from kidney failure. Determine the following measures:

(a) The expected number of years a patient stays on dialysis.

(b) The longevity of a patient who starts on dialysis.

(c) The life expectancy of a patient who survives 1 year or longer after a transplant.

(d) The expected number of years before an at-least-1-year transplant survivor goes back to dialysis or dies.

(e) The quality of life for those who survive a year or more after a transplant (presumably, spending fewer years on dialysis signifies a better quality of life).

This page intentionally left blank