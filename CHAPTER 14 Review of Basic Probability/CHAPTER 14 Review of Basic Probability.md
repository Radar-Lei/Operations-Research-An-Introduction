## CHAPTER 14 Review of Basic Probability

### 14.1 LAWS OF PROBABILITY

Probability deals with random outcomes of an experiment. The conjunction of all the outcomes is the sample space, and a subset of the sample space is an event. As an illustration, the experiment of rolling a (six-faced) die produces the sample space \{1, 2, $3,4,5,6\}$ . The subset $\{ 1,3,5\}$ defines the event of turning up odd values.

An experiment may deal with a continuous sample space as well. For example, the time between failures of an electronic component may assume any nonnegative value.

If an event $E$ occurs $m$ times in an $n$ -trial experiment, then the probability of realizing the event $E$ is defined as

$$
P\{ E\}  = \mathop{\lim }\limits_{{n \rightarrow  \infty }}\frac{m}{n}
$$

The definition says that when the experiment is repeated an infinite number of times $\left( {n \rightarrow  \infty }\right)$ , the probability of realizing an event is $\frac{m}{n}$ . For example, the longer a fair coin is flipped, the closer will be the estimate of $P\{$ head $\}$ (or $P\{$ tail $\}$ ) to the theoretical value of 0.5 .

By definition,

$$
0 \leq  P\{ E\}  \leq  1
$$

An event $E$ is impossible if $P\{ E\}  = 0$ , and certain if $P\{ E\}  = 1$ . For example, in a six-faced die experiment, rolling a seven is impossible, but rolling a number in the range of 1 to 6 is certain. than 50-50 chance that at least two of you have the same birthday?" (see Problem 14-2). And so the game started with the students taking turns calling their birthdays and others raising their hands if they coincided. Of course, in some classes I "won" and in others my students did. And when they "won," there was a glee of satisfaction on their faces because they thought I was "proven" wrong. But my goal from the experiment was fulfilled just the same: "A better than 50-50 chance does not mean that the anticipated outcome will happen for certain," I told my students. "It only means that there is a greater chance it will happen; but, at the same time, there still is a positive probability that it won't. And that is what probability is all about: quantifying the degree of certainty/uncertainty regarding a proposition."

---

## Aha! Moment: Teaching (Probability) by Example: The Birthday Challenge!

I taught the introductory probability/statistics course many times. In the first class meeting, following a brief exchange of pleasantries, I took note of the size of the class, and if it exceeded 25 or so, I always posed a challenge to the students: "Who is willing to bet that there is a better

---

#### 14.1.1 Addition Law of Probability

The union of two events $E$ and $F$ is $E + F$ or $E \cup  F$ , and their intersection is ${EF}$ or $E \cap  F$ . The events $E$ and $F$ are mutually exclusive if the occurrence of one event precludes the occurrence of the other, or $P\{ {EF}\}  = 0$ . Based on these definitions, the addition law of probability can be stated as

$$
P\{ E + F\}  = \left\{  \begin{array}{ll} P\{ E\}  + P\{ F\} , & E\text{ and }F\text{ mutually exclusive } \\  P\{ E\}  + P\{ F\}  - P\{ {EF}\} , & \text{ otherwise } \end{array}\right.
$$

Example 14.1-1

Consider the experiment of rolling a die. The sample space of the experiment is $\{ 1,2,3,4,5,6\}$ . For a fair die, we have

$$
P\{ 1\}  = P\{ 2\}  = P\{ 3\}  = P\{ 4\}  = P\{ 5\}  = P\{ 6\}  = \frac{1}{6}
$$

Define

$$
E = \{ 1,2,3\text{ , or }4\}
$$

$$
F = \{ 3,4,\text{ or }5\}
$$

The event ${EF} = \{ 3$ or $4\}$ because the outcomes 3 and 4 are common between $E$ and $F$ . Thus,

$$
P\{ E\}  = P\{ 1\}  + P\{ 2\}  + P\{ 3\}  + P\{ 4\}  = \frac{1}{6} + \frac{1}{6} + \frac{1}{6} + \frac{1}{6} = \frac{2}{3}
$$

$$
P\{ F\}  = P\{ 3\}  + P\{ 4\}  + P\{ 5\}  = \frac{1}{2}
$$

$$
P\{ {EF}\}  = P\{ 3\}  + P\{ 4\}  = \frac{1}{3}
$$

$$
P\{ E + F\}  = P\{ E\}  + P\{ F\}  - P\{ {EF}\}  = \frac{2}{3} + \frac{1}{2} - \frac{1}{3} = \frac{5}{6}
$$

Intuitively, the result makes sense because $P\{ E + F\}  = P\{ 1,2,3,4,5\}  = \frac{5}{6}$ .

#### 14.1.2 Conditional Law of Probability

Given the two events $E$ and $F$ with $P\{ F\}  > 0$ , the conditional probability of $E$ given $F$ is computed as

$$
P\{ E \mid  F\}  = \frac{P\{ {EF}\} }{P\{ F\} },\;P\{ F\}  > 0
$$

If $E$ is a subset of $F$ , then $P\{ {EF}\}  = P\{ E\}$ . The two events are independent if, and only if,

$$
P\{ E \mid  F\}  = P\{ E\}
$$

In this case, the conditional probability law reduces to

$$
P\{ {EF}\}  = P\{ E\} P\{ F\}
$$

## Example 14.1-2

You are playing a game in which another person is rolling a die. You cannot see the die, but you are given information about the outcomes. Your job is to predict the outcome of each roll. Determine the probability that the outcome is 6 , given that you are told that the roll has turned up an even number.

Let $E = \{ 6\}$ , and define $F = \{ 2,4$ , or 6 $\}$ . Thus,

$$
P\{ E \mid  F\}  = \frac{P\{ {EF}\} }{P\{ F\} } = \frac{P\{ E\} }{P\{ F\} } = \left( \frac{1/6}{1/2}\right)  = \frac{1}{3}
$$

Note that $P\{ {EF}\}  = P\{ E\}$ because $E$ is a subset of $F$ .

### 14.2 RANDOM VARIABLES AND PROBABILITY DISTRIBUTIONS

The outcomes of an experiment can be naturally numeric (e.g., rolling a die) or can be represented by numeric code (e.g., flipping a coin, with the outcome head/tail coded as 0/1). The numeric representation of the outcomes defines what is known as a random variable.

A random variable, $x$ , may be discrete (as in die rolling) or continuous (as in time-to-failure of an equipment). Each continuous or discrete random variable $x$ is quantified by a probability density function (pdf), $f\left( x\right)$ or $p\left( x\right)$ , satisfying the following conditions:

<table><tr><td rowspan="2">Characteristic</td><td colspan="2">Random variable, $x$</td></tr><tr><td>Discrete</td><td>Continuous</td></tr><tr><td>Applicability range <br> Conditions for the pdf</td><td>$x = a, a + 1,\ldots , b$ <br> $p\left( x\right)  \geq  0,\mathop{\sum }\limits_{{x = a}}^{b}p\left( x\right)  = 1$</td><td>$a \leq  x \leq  b$ <br> $f\left( x\right)  \geq  0,{\int }_{a}^{b}f\left( x\right) {dx} = 1$</td></tr></table>

An important probability measure is the cumulative distribution function (CDF), defined as

$$
P\{ x \leq  X\}  = \left\{  \begin{array}{ll} P\left( X\right)  = \mathop{\sum }\limits_{{x = a}}^{X}p\left( x\right) , & x\text{ discrete } \\  F\left( X\right)  = {\int }_{a}^{X}f\left( x\right) {dx}, & x\text{ continuous } \end{array}\right.
$$

## Example 14.2-1

Consider the random variable $x = \{ 1,2,3,4,5,6\}$ representing the experiment of rolling a fair die. The associated pdf and CDF are

$$
p\left( x\right)  = \frac{1}{6}, x = 1,2,\ldots ,6
$$

$$
P\left( X\right)  = \frac{X}{6}, X = 1,2,\ldots ,6
$$

Figure 14.1 graphs the two functions. The pdf $p\left( x\right)$ is a uniform discrete function because all the values of the random variables occur with equal probabilities.

The continuous counterpart of uniform $p\left( x\right)$ is illustrated by the following experiment. A needle of length $l$ is pivoted in the center of a circle with diameter $l$ . After marking an arbitrary reference point on the circumference, the needle is spun clockwise, and the circumference distance, $x$ , from where the pointer stops to the marked point is measured. Because any stopping point on the circumference is equally likely to occur, the distribution of $x$ is uniform in the range $0 \leq  x \leq  {\pi l}$ with the following pdf:

$$
f\left( x\right)  = \frac{1}{\pi l},0 \leq  x \leq  {\pi l}
$$

The associated CDF, $F\left( X\right)$ , is computed as

$$
F\left( X\right)  = P\{ x \leq  X\}  = {\int }_{0}^{X}f\left( x\right) {dx} = {\int }_{0}^{X}\frac{1}{\pi l}{dx} = \frac{X}{\pi l},0 \leq  X \leq  {\pi l}
$$

Figure 14.2 graphs the two functions.

![bo_d56m56f7aajc73800ndg_3_353_1252_1191_929_0.jpg](bo_d56m56f7aajc73800ndg_3_353_1252_1191_929_0.jpg)

### 14.3 EXPECTATION OF A RANDOM VARIABLE

Given a real function $h\left( x\right)$ of a random variable $x$ , the expected value of $h\left( x\right)$ is computed as

$$
E\{ h\left( x\right) \}  = \left\{  \begin{array}{ll} \mathop{\sum }\limits_{{x = a}}^{b}h\left( x\right) p\left( x\right) , & x\text{ discrete } \\  {\int }_{a}^{b}h\left( x\right) f\left( x\right) {dx}, & x\text{ continuous } \end{array}\right.
$$

Example 14.3-1

During the first week of each month, I pay all my bills and answer a few letters. I usually buy 20 first-class mail stamps each month for this purpose. The number of stamps I actually use varies randomly between 10 and 24, with equal probabilities. Determine the average number of stamps left (i.e., average surplus) per month.

The pdf of the number of stamps used is

$$
p\left( x\right)  = \frac{1}{15}, x = {10},{11},\ldots ,{24}.
$$

The number of stamps left is

$$
h\left( x\right)  = \left\{  \begin{array}{l} {20} - x, x = {10},{11},\ldots ,{19} \\  0,\;\text{ otherwise } \end{array}\right.
$$

Thus,

$$
E\{ h\left( x\right) \}  = \frac{1}{15}\left\lbrack  {\left( {{20} - {10}}\right)  + \left( {{20} - {11}}\right)  + \left( {{20} - {12}}\right)  + \ldots  + \left( {{20} - {19}}\right) }\right\rbrack   + \frac{5}{15}\left( 0\right)  = 3\frac{2}{3}
$$

The product $\frac{5}{15}\left( 0\right)$ accounts for the outcome of being left with no stamps, which corresponds to the probability of using at least 20 stamps - that is,

$$
P\{ x \geq  {20}\}  = p\left( {20}\right)  + p\left( {21}\right)  + p\left( {22}\right)  + p\left( {23}\right)  + p\left( {24}\right)  = 5\left( \frac{1}{15}\right)  = \frac{5}{15}
$$

#### 14.3.1 Mean and Variance (Standard Deviation) of a Random Variable

The mean value $E\{ x\}$ is a measure of the central tendency (or weighted sum) of the random variable $x$ . The variance $\operatorname{var}\{ x\}$ is a measure of the dispersion or deviation of $x$ around its mean value. Its square root is known as the standard deviation of $x$ , stdDev $\{ x\}$ . A larger standard deviation implies higher uncertainty.

The formulas for the mean and variance can be derived from the general definition of $E\{ h\left( x\right) \}$ in Section 14.3 by substituting $h\left( x\right)  = x$ to obtain $E\{ x\}$ and by substituting $h\left( x\right)  = {\left( x - E\{ x\} \right) }^{2}$ to obtain $\operatorname{var}\{ x\}$ -that is

$$
E\{ x\}  = \left\{  \begin{array}{ll} \mathop{\sum }\limits_{{x = a}}^{b}{xp}\left( x\right) , & x\text{ discrete } \\  {\int }_{a}^{b}{xf}\left( x\right) {dx}, & x\text{ continuous } \end{array}\right.
$$

$$
\operatorname{var}\{ x\}  = \left\{  \begin{array}{ll} \mathop{\sum }\limits_{{x = a}}^{b}{\left( x - E\{ x\} \right) }^{2}p\left( x\right) , & x\text{ discrete } \\  {\int }_{a}^{b}{\left( x - E\{ x\} \right) }^{2}f\left( x\right) {dx}, & x\text{ continuous } \end{array}\right.
$$

$$
\operatorname{stdDev}\{ x\}  = \sqrt{\operatorname{var}\{ x\} }
$$

Example 14.3-2

We compute the mean and variance for each of the two experiments in Example 14.2-1.

Case 1 (Die Rolling). The pdf is $p\left( x\right)  = \frac{1}{6}, x = 1,2,\ldots ,6$ . Thus,

$$
E\{ x\}  = 1\left( \frac{1}{6}\right)  + 2\left( \frac{1}{6}\right)  + 3\left( \frac{1}{6}\right)  + 4\left( \frac{1}{6}\right)  + 5\left( \frac{1}{6}\right)  + 6\left( \frac{1}{6}\right)  = {3.5}
$$

$$
\operatorname{var}\{ x\}  = \left( \frac{1}{6}\right) \left\{  {{\left( 1 - {3.5}\right) }^{2} + {\left( 2 - {3.5}\right) }^{2} + {\left( 3 - {3.5}\right) }^{2} + {\left( 4 - {3.5}\right) }^{2}}\right.
$$

$$
\left. {+{\left( 5 - {3.5}\right) }^{2} + {\left( 6 - {3.5}\right) }^{2}}\right\}   = {2.917}
$$

$$
\operatorname{stdDev}\left( x\right)  = \sqrt{2.917} = {1.708}
$$

Case 2 (Needle Spinning). Suppose that the length of the needle is 1 inch. Then,

$$
f\left( x\right)  = \frac{1}{3.14},\;0 \leq  x \leq  {3.14}
$$

The mean and variance are

$$
E\left( x\right)  = {\int }_{0}^{3.14}x\left( \frac{1}{3.14}\right) {dx} = {1.57}\text{ inch }
$$

$$
\operatorname{var}\left( x\right)  = {\int }_{0}^{3.14}{\left( x - {1.57}\right) }^{2}\left( \frac{1}{3.14}\right) {dx} = {.822}{\text{ inch }}^{2}
$$

$$
\operatorname{stdDev}\left( x\right)  = \sqrt{.822} = {.906}\text{ inch }
$$

Excel Moment

Template excelStatTables.xls computes the mean, standard deviation, probabilities, and percentiles for 16 common pdfs, including the discrete and continuous uniform distributions. The use of the spreadsheet is self-explanatory.

#### 14.3.2 Joint Random Variables

Consider the two continuous random variables ${x}_{1}$ and ${x}_{2}$ , where ${a}_{1} \leq  {x}_{1} \leq  {b}_{1}$ and ${a}_{2} \leq  {x}_{2} \leq  {b}_{2}$ . Define $f\left( {{x}_{1},{x}_{2}}\right)$ as the joint pdf of ${x}_{1}$ and ${x}_{2}$ and ${f}_{1}\left( {x}_{1}\right)$ and ${f}_{2}\left( {x}_{2}\right)$ as their respective marginal pdfs. Then

$$
f\left( {{x}_{1},{x}_{2}}\right)  \geq  0,{a}_{1} \leq  {x}_{1} \leq  {b}_{1},{a}_{2} \leq  {x}_{2} \leq  {b}_{2}
$$

$$
{\int }_{{a}_{1}}^{{b}_{1}}d{x}_{1}{\int }_{{a}_{2}}^{{b}_{2}}d{x}_{2}f\left( {{x}_{1},{x}_{2}}\right)  = 1
$$

$$
{f}_{1}\left( {x}_{1}\right)  = {\int }_{{a}_{2}}^{{b}_{2}}f\left( {{x}_{1},{x}_{2}}\right) d{x}_{2}
$$

$$
{f}_{2}\left( {x}_{2}\right)  = {\int }_{{a}_{1}}^{{b}_{1}}f\left( {{x}_{1},{x}_{2}}\right) d{x}_{1}
$$

$$
f\left( {{x}_{1},{x}_{2}}\right)  = {f}_{1}\left( {x}_{1}\right) {f}_{2}\left( {x}_{2}\right) \text{ , if }{x}_{1}\text{ and }{x}_{2}\text{ are independent }
$$

The same formulas apply to discrete pdfs, replacing integration with summation.

For the special case $y = {c}_{1}{x}_{1} + {c}_{2}{x}_{2}$ , where the random variables ${x}_{1}$ and ${x}_{2}$ are jointly distributed according to the pdf $f\left( {{x}_{1},{x}_{2}}\right)$ , we can prove that

$$
E\left\{  {{c}_{1}{x}_{1} + {c}_{2}{x}_{2}}\right\}   = {c}_{1}E\left\{  {x}_{1}\right\}   + {c}_{2}E\left\{  {x}_{2}\right\}
$$

$$
\operatorname{var}\left\{  {{c}_{1}{x}_{1} + {c}_{2}{x}_{2}}\right\}   = {c}_{1}^{2}\operatorname{var}\left\{  {x}_{1}\right\}   + {c}_{2}^{2}\operatorname{var}\left\{  {x}_{2}\right\}   + 2{c}_{1}{c}_{2}\operatorname{cov}\left\{  {{x}_{1},{x}_{2}}\right\}
$$

where

$$
\operatorname{cov}\left\{  {{x}_{1},{x}_{2}}\right\}   = E\left\{  {\left( {{x}_{1} - E\left\{  {x}_{1}\right\}  }\right) \left( {{x}_{2} - E\left\{  {x}_{2}\right\}  }\right) }\right.
$$

$$
= E\left( {{x}_{1}{x}_{2} - {x}_{1}E\left\{  {x}_{2}\right\}   - {x}_{2}E\left\{  {x}_{1}\right\}   + E\left\{  {x}_{1}\right\}  E\left\{  {x}_{2}\right\}  }\right)
$$

$$
= E\left\{  {{x}_{1}{x}_{2}}\right\}   - E\left\{  {x}_{1}\right\}  E\left\{  {x}_{2}\right\}
$$

If ${x}_{1}$ and ${x}_{2}$ are independent, then $E\left\{  {{x}_{1}{x}_{2}}\right\}   = E\left\{  {x}_{1}\right\}  E\left\{  {x}_{2}\right\}$ and $\operatorname{cov}\left\{  {{x}_{1},{x}_{2}}\right\}   = 0$ . The converse is not true, in the sense that two dependent variables may have zero covariance.

## Example 14.3-3

A lot includes four defective $\left( D\right)$ items and six good $\left( G\right)$ ones. One item is selected randomly and tested. Next, a second item is selected from the remaining nine items and tested. Let ${x}_{1}$ and ${x}_{2}$ represent the outcomes of the first and second selections.

(a) Determine the joint and marginal pdfs of ${x}_{1}$ and ${x}_{2}$ .

(b) Suppose that a good item nets a revenue of \$5 and a defective item results in a loss of \$6. Determine the mean and variance of revenue following the testing of two items.

Let $p\left( {{x}_{1},{x}_{2}}\right)$ be the joint pdf of ${x}_{1}$ and ${x}_{2}$ , and define ${p}_{1}\left( {x}_{1}\right)$ and ${p}_{2}\left( {x}_{2}\right)$ as the respective marginal pdfs. First, we determine ${p}_{1}\left( {x}_{1}\right)$ as

$$
{p}_{1}\left( G\right)  = \frac{6}{10} = {.6},{p}_{1}\left( D\right)  = \frac{4}{10} = {.4}
$$

Next, we know that the second outcome ${x}_{2}$ depends on the first outcome ${x}_{1}$ . Hence, to determine ${p}_{2}\left( {x}_{2}\right)$ , we first determine the joint pdf $p\left( {{x}_{1},{x}_{2}}\right)$ (using the formula $P\{ {AB}\}  = P\{ A \mid  B\} P\{ B\}$ in Section 14.1.2), from which we can determine the marginal distribution ${p}_{2}\left( {x}_{2}\right)$ . Thus,

$$
P\left\{  {{x}_{2} = G \mid  {x}_{1} = G}\right\}   = \frac{5}{9}
$$

$$
P\left\{  {{x}_{2} = G \mid  {x}_{1} = B}\right\}   = \frac{6}{9}
$$

$$
P\left\{  {{x}_{2} = B \mid  {x}_{1} = G}\right\}   = \frac{4}{9}
$$

$$
P\left\{  {{x}_{2} = B \mid  {x}_{1} = B}\right\}   = \frac{3}{9}
$$

Next,

$$
p\left\{  {{x}_{2} = G,{x}_{1} = G}\right\}   = \frac{5}{9} \times  \frac{6}{10} = \frac{5}{15}
$$

$$
p\left\{  {{x}_{2} = G,{x}_{1} = B}\right\}   = \frac{6}{9} \times  \frac{4}{10} = \frac{4}{15}
$$

$$
p\left\{  {{x}_{2} = B,{x}_{1} = G}\right\}   = \frac{4}{9} \times  \frac{6}{10} = \frac{4}{15}
$$

$$
p\left\{  {{x}_{2} = B,{x}_{1} = B}\right\}   = \frac{3}{9} \times  \frac{4}{10} = \frac{2}{15}
$$

The expected revenue can be determined from the joint distribution by recognizing that $G$ produces \$5 and $B$ yields - \$6. Thus,

Expected revenue $= \left( {5 + 5}\right) \frac{5}{15} + \left( {5 - 6}\right) \frac{4}{15} + \left( {-6 + 5}\right) \frac{4}{15} + \left( {-6 - 6}\right) \frac{2}{15} = \$ {1.20}$

The same result can be determined by recognizing that the expected revenue for both selections equals the sum of the expected revenue for each individual selection (even though the two variables are not independent). These computations require determining the marginal distributions, ${p}_{1}\left( {x}_{1}\right)$ and ${p}_{2}\left( {x}_{2}\right)$ .

A convenient way to determine the marginal distributions is to present the joint distribution, $p\left( {{x}_{1},{x}_{2}}\right)$ , as a table and then add the respective columns and rows to determine $p\left( {x}_{1}\right)$ and $p\left( {x}_{2}\right)$ , respectively. Thus,

![bo_d56m56f7aajc73800ndg_7_647_694_591_320_0.jpg](bo_d56m56f7aajc73800ndg_7_647_694_591_320_0.jpg)

Now, the expected revenue is determined from the marginal distributions as

Expected revenue $=$ Selection 1 expected revenue + Selection 2 expected revenue

$$
= \left( {5 \times  {.6} - 6 \times  {.4}}\right)  + \left( {5 \times  {.6} - 6 \times  {.4}}\right)  = \$ {1.20}
$$

To compute the variance of the total revenue, we note that

$$
\text{ var }\{ \text{ revenue }\}  = \text{ var }\{ \text{ revenue 1 }\}  + \text{ var }\{ \text{ revenue 2 }\}  + 2\text{ cov }\{ \text{ revenue 1, revenue 2 }\}
$$

Because ${p}_{1}\left( {x}_{1}\right)  = {p}_{2}\left( {x}_{2}\right)$ , var $\{$ revenue 1 $\}  =$ var $\{$ revenue 2 $\}$ . To compute the variance, we use the following formula (see Problem 14-24):

$$
\operatorname{var}\{ x\}  = E\left\{  {x}^{2}\right\}   - {\left( E\{ x\} \right) }^{2}
$$

Thus,

$$
\operatorname{var}\{ \text{ revenue 1 \} } = \left\lbrack  {{5}^{2} \times  {.6} + {\left( -6\right) }^{2} \times  {.4}}\right\rbrack   - {.6}^{2} = {29.04}
$$

Next, to compute the covariance, we use the formula

$$
\operatorname{cov}\left\{  {{x}_{1},{x}_{2}}\right)  = E\left\{  {{x}_{1}{x}_{2}}\right\}   - E\left\{  {x}_{1}\right\}  E\left\{  {x}_{2}\right\}
$$

The term $E\left\{  {{x}_{1}{x}_{2}}\right\}$ can be computed from the joint pdf of ${x}_{1}$ and ${x}_{2}$ as

$$
\text{ Convariance } = \left\lbrack  {\left( {5 \times  5}\right) \left( \frac{5}{15}\right)  + \left( {5 \times   - 6}\right) \left( \frac{4}{15}\right)  + \left( {-6 \times  5}\right) \left( \frac{4}{15}\right) }\right.
$$

$$
+ \left. {\left( {-6 \times   - 6}\right) \left( \frac{2}{15}\right) }\right\rbrack   - {.6} \times  {.6} =  - {3.23}
$$

Thus,

$$
\text{ Variance } = {29.04} + {29.04} + 2\left( {-{3.23}}\right)  = {51.62}
$$

### 14.4 FOUR COMMON PROBABILITY DISTRIBUTIONS

In Sections 14.2 and 14.3, we discussed the (discrete and continuous) uniform distribution. This section presents four additional pdfs that are encountered often in operations research studies: discrete binomial and Poisson, and continuous exponential and normal.

#### 14.4.1 Binomial Distribution

A manufacturer produces an item in lots of $n$ items each. The fraction of defective items, $p$ , in each lot is estimated from historical data. We are interested in determining the pdf of the number of defectives in a lot.

There are ${C}_{x}^{n} = \frac{n!}{x!\left( {n - x}\right) !}$ distinct combinations of $x$ defectives in a lot of size $n$ , and the probability of realizing each combination is ${p}^{x}{\left( 1 - p\right) }^{n - x}$ . Thus, from the addition law (Section 14.1.1), the probability of $k$ defectives in a lot of $n$ items is

$$
P\{ x = k\}  = {C}_{k}^{n}{p}^{k}{\left( 1 - p\right) }^{n - k}, k = 0,1,2,\ldots , n
$$

This is the binomial distribution with parameters $n$ and $p$ . Its mean and variance are

$$
E\{ x\}  = {np}
$$

$$
\operatorname{var}\{ x\}  = {np}\left( {1 - p}\right)
$$

Example 14.4-1

John Doe's daily chores require making 10 round trips by car between two towns. Once through with all ten trips, Mr. Doe can take the rest of the day off, a good enough motivation to drive above the speed limit. Experience shows that there is a 40% chance of getting a speeding fine on any round trip.

(a) What is the probability that the day will end without a speeding ticket?

(b) If each speeding ticket costs \$80, what is the average daily fine?

The probability of getting a ticket on any one trip is $p = {.4}$ . Thus, the probability of not getting a ticket in any one day is

$$
P\{ x = 0\}  = {C}_{0}^{10}{\left( {.4}\right) }^{0}{\left( {.6}\right) }^{10} = {.006}
$$

This means that there is less than 1% chance of finishing the day without a fine.

The average fine per day is

$$
\text{ Average fine } = \$ {80E}\{ x\}  = \$ {80}\left( {np}\right)  = {80} \times  {10} \times  {.4} = \$ {320}
$$

Remarks. $P\{ x = 0\}$ can be computed using excelStatTables.xls. Enter 10 in F7,.4 in G7, and 0 in J7. The answer, $P\{ x = 0\}  = {.006047}$ , is given in M7.

#### 14.4.2 Poisson Distribution

Customers arrive at a bank or a grocery store in a "totally random" fashion-meaning that arrival times cannot be predicted in advance. The pdf describing the number of arrivals during a specified time period is the Poisson distribution.

Let $x$ be the number of events (e.g., arrivals) that take place during a specified time period (e.g., a minute or an hour). Given that $\lambda$ is a known constant, the Poisson pdf is defined as

$$
P\{ x = k\}  = \frac{{\lambda }^{k}{e}^{-\lambda }}{k!}, k = 0,1,2,\ldots
$$

The mean and variance of the Poisson are

$$
E\{ x\}  = \lambda
$$

$$
\operatorname{var}\{ x\}  = \lambda
$$

The formula for the mean reveals that $\lambda$ must represent the rate at which events occur.

The Poisson distribution figures prominently in the study of queues (see Chapter 18).

Example 14.4-2

Repair jobs arrive at a small-engine repair shop randomly at the rate of 10 per day.

(a) What is the average number of jobs that are received daily at the shop?

(b) What is the probability that no jobs will arrive during any 1 hour, assuming that the shop is open 8 hours a day?

The average number of jobs received per day equals $\lambda  = {10}$ jobs per day. To compute the probability of no arrivals per hour, we need to compute the arrival rate per hour - namely, ${\lambda }_{\text{ hour }} = \frac{10}{8} = {1.25}$ jobs per hour. Thus

$$
P\{ \text{ no arrivals per hour }\}  = \frac{{\left( {\lambda }_{\text{ hour }}\right) }^{0}{e}^{-{\lambda }_{\text{ hour }}}}{0!}
$$

$$
= \frac{{1.25}^{0}{e}^{-{1.25}}}{0!} = {.2865}
$$

Remarks. The probability above can be computed with excelStatTables.xls. Enter 1.25 in F16 and 0 in J16. The answer, .286505, appears in M16.

#### 14.4.3 Negative Exponential Distribution

If the number of arrivals at a service facility during a specified time period follows the Poisson distribution (Section 14.4.2), then, automatically, the distribution of the interarrival time (i.e., between successive arrivals) is the negative exponential (or, simply, exponential) distribution. Specifically, given $\lambda$ is the rate of occurrence of Poisson arrivals, then the distribution of interarrival time, $x$ , is

$$
f\left( x\right)  = \lambda {e}^{-{\lambda x}}, x > 0
$$

Figure 14.3 graphs $f\left( x\right)$ .

The mean and variance of the exponential distribution are

$$
E\{ x\}  = \frac{1}{\lambda }
$$

$$
\operatorname{var}\{ x\}  = \frac{1}{\lambda }
$$

![bo_d56m56f7aajc73800ndg_10_310_198_619_355_0.jpg](bo_d56m56f7aajc73800ndg_10_310_198_619_355_0.jpg)

FIGURE 14.3

Probability density function of the exponential distribution

The mean $E\{ x\}$ is consistent with the definition of $\lambda$ . If $\lambda$ is the rate at which events occur, then $\frac{1}{\lambda }$ is the average time interval between successive events.

## Example 14.4-3

Cars arrive randomly at a gas station. The average interarrival time is 2 minutes. Determine the probability that the interarrival time does not exceed 1 minute.

The determination of the desired probability is the same as computing the CDF of $x -$ namely,

$$
P\{ x \leq  A\}  = {\int }_{0}^{A}\lambda {e}^{-{\lambda x}}{dx}
$$

$$
=  - {\left. {e}^{-{\lambda x}}\right| }_{o}^{A}
$$

$$
= 1 - {e}^{-{\lambda A}}
$$

The arrival rate for the example is $\lambda  = \frac{1}{2}$ arrival per minute. Substituting $A = 1$ , the desired probability is

$$
P\{ x \leq  1\}  = 1 - {e}^{-\left( \frac{1}{2}\right) \left( 1\right) } = {.3934}
$$

Remarks. You can use excelStatTables.xls to compute the preceding probability. Enter .5 in F9, 1 in J9. The answer (= .393468) appears in O9.

#### 14.4.4 Normal Distribution

The normal distribution describes many random phenomena in everyday life, such as test scores and weights and heights of individuals. The pdf of the normal distribution is

$$
f\left( x\right)  = \frac{1}{\sqrt{{2\pi }{\sigma }^{2}}}{e}^{-\frac{1}{2}{\left( \frac{x - \mu }{\sigma }\right) }^{2}}, - \infty  < x < \infty
$$

The mean and variance are

$$
E\{ x\}  = \mu
$$

$$
\operatorname{var}\{ \mathrm{x}\}  = {\sigma }^{2}
$$

The notation $N\left( {\mu ,\sigma }\right)$ is usually used to represent a normal distribution with mean $\mu$ and standard deviation $\sigma$ .

![bo_d56m56f7aajc73800ndg_11_333_199_638_385_0.jpg](bo_d56m56f7aajc73800ndg_11_333_199_638_385_0.jpg)

FIGURE 14.4

Probability density function of the normal random variable

Figure 14.4 graphs the normal pdf. The function is always symmetrical around the mean $\mu$ .

An important property of the normal random variable is that it approximates the distribution of the average of a sample taken from any distribution. This remarkable result is based on the following theorem:

Central Limit Theorem. Let ${x}_{1},{x}_{2},\ldots$ , and ${x}_{n}$ be independent and identically distributed random variables, each with mean $\mu$ and standard deviation $\sigma$ , and define

$$
{s}_{n} = {x}_{1} + {x}_{2} + \cdots  + {x}_{n}
$$

The distribution of ${s}_{n}$ is asymptotically normal with mean ${n\mu }$ and variance $n{\sigma }^{2}$ , regardless of the original distribution of ${x}_{1},{x}_{2},\ldots$ , and ${x}_{n}$ .

A special case of the central limit theorem deals with the distribution of the average of a sample of size $n$ (drawn from any distribution). The average is asymptotically normal with mean $\mu$ and variance $\frac{{\sigma }^{2}}{n}$ . This result has important applications in statistical quality control.

The CDF of the normal random variable cannot be determined in a closed form. Table A. 1 in Appendix A gives the probabilities for $N\left( {0,1}\right)$ , the standard normal distribution with mean zero and standard deviation 1. A general normal random variable $x$ with mean $\mu$ and standard deviation $\sigma$ can be converted to a standard normal $z$ using the transformation

$$
z = \frac{x - \mu }{\sigma }
$$

Over 99% of the area under any normal density function is enclosed in the range $\mu  - {3\sigma } \leq  x \leq  \mu  + {3\sigma }$ , also known as the 6-sigma limits.

## Example 14.4-4

The inside diameter of a cylinder has the specification $1 \pm  {.03}\mathrm{\;{cm}}$ . The output of the machining process producing the cylinder follows a normal distribution with mean $1\mathrm{\;{cm}}$ and standard deviation ${.1}\mathrm{\;{cm}}$ . Determine the percentage of production that will meet the specifications.

Defining $x$ as the inside parameter of the cylinder, the probability that a cylinder will meet specifications is

$$
P\{ 1 - {.03} \leq  x \leq  1 + {.03}\}  = P\{ {.97} \leq  x \leq  {1.03}\}
$$

![bo_d56m56f7aajc73800ndg_12_459_196_507_411_0.jpg](bo_d56m56f7aajc73800ndg_12_459_196_507_411_0.jpg)

FIGURE 14.5

Calculation of $P\{  - {.3} \leq  z \leq  {.3}\}$ in a standard normal distribution

This probability is computed using the standard normal (Table A. 1 in Appendix A). Given $\mu  = 1$ and $\sigma  = {.1}$ , we have

$$
P\{ {.97} \leq  x \leq  {1.03}\}  = P\left\{  {\frac{{.97} - 1}{.1} \leq  z \leq  \frac{{1.03} - 1}{.1}}\right\}
$$

$$
= P\{  - {.3} \leq  z \leq  {.3}\}
$$

$$
= P\{ z \leq  {.3}\}  - P\{ z \leq   - {.3}\}
$$

$$
= P\{ z \leq  {.3}\}  - P\{ z \geq  {.3}\}
$$

$$
= P\{ z \leq  {.3}\}  - \left\lbrack  {1 - P\{ z \leq  {.3}\} }\right\rbrack
$$

$$
= {2P}\{ z \leq  {.3}\}  - 1
$$

$$
= 2 \times  {.6179} - 1
$$

$$
= {.2358}
$$

Notice that $P\{ z \leq   - {.3}\}  = 1 - P\{ z \leq  {.3}\}$ because of the symmetry of the pdf, as shown in Figure 14.5. The cumulative probability $P\{ z \leq  {.3}\} \left( { = {.6179}}\right)$ is obtained from the standard normal table (Table A. 1 in Appendix A) as the entry designated with row $z = {0.3}$ and column $z = {0.00}$ .

Remarks. $P\{ {.97} \leq  x \leq  {1.03}\}$ can be computed directly from excelStatTables.xls. Enter 1 in F15,.1 in G15,.97 in J15, and 1.03 in K15. The answer (= .235823) appears in Q15.

### 14.5 EMPIRICAL DISTRIBUTIONS

The preceding sections have dealt with the pdfs and CDFs of five common distributions - uniform, binomial, Poisson, exponential, and normal. How are these distributions recognized in practice?

The basis for identifying any pdf is the raw data we collect about the situation under study. This section shows how sampled data can be converted into a pdf.

Step 1. Summarize the raw data in the form of an appropriate frequency histogram to determine the associated empirical pdf.

Step 2. Use the goodness-of-fit test to test if the resulting empirical pdf is sampled from a known theoretical pdf.

Frequency histogram. A frequency histogram is constructed from raw data by dividing the range of the data (minimum value to maximum value) into nonoverlapping bins. The frequency in each bin is the tally of all the raw data values that fall within the bin's designated boundaries.

## Example 14.5-1

The following data represent the service time (in minutes) in a service facility for a sample of 60 customers:

<table><tr><td>.7</td><td>.4</td><td>3.4</td><td>4.8</td><td>2.0</td><td>1.0</td><td>5.5</td><td>6.2</td><td>1.2</td><td>4.4</td></tr><tr><td>1.5</td><td>2.4</td><td>3.4</td><td>6.4</td><td>3.7</td><td>4.8</td><td>2.5</td><td>5.5</td><td>.3</td><td>8.7</td></tr><tr><td>2.7</td><td>.4</td><td>2.2</td><td>2.4</td><td>.5</td><td>1.7</td><td>9.3</td><td>8.0</td><td>4.7</td><td>5.9</td></tr><tr><td>.7</td><td>1.6</td><td>5.2</td><td>.6</td><td>.9</td><td>3.9</td><td>3.3</td><td>.2</td><td>.2</td><td>4.9</td></tr><tr><td>9.6</td><td>1.9</td><td>9.1</td><td>1.3</td><td>10.6</td><td>3.0</td><td>.3</td><td>2.9</td><td>2.9</td><td>4.8</td></tr><tr><td>8.7</td><td>2.4</td><td>7.2</td><td>1.5</td><td>7.9</td><td>11.7</td><td>6.3</td><td>3.8</td><td>6.9</td><td>5.3</td></tr></table>

The minimum and maximum values of the data are .2 and 11.7, respectively. This means that the sample is covered by the range $\left( {0,{12}}\right)$ . We arbitrarily divide the range $\left( {0,{12}}\right)$ into 12 bins, each of width 1 minute. The proper selection of the bin width is crucial in revealing the shape of the empirical distribution. Although there are no hard rules for determining the optimal bin width, a general rule of thumb is to use from 10 to 20 bins. In practice, it may be necessary to try different bin widths before deciding on an acceptable histogram.

The following table summarizes the histogram information for the given sample. The relative-frequency column, ${f}_{i}$ , is computed by dividing the entries of the observed-frequency column, ${o}_{i}$ , into the total number of observations $\left( {n = {60}}\right)$ . For example, ${f}_{1} = \frac{11}{60} = {.1833}$ . The cumulative-frequency column, ${F}_{i}$ , is generated by summing the values of ${f}_{i}$ recursively. For example, ${F}_{1} = {f}_{1} =$ .1833 and ${F}_{2} = {F}_{1} + {f}_{2} = {.1833} + {.1333} = {.3166}$ .

<table><tr><td>$i$</td><td>Bin interval</td><td>Observations tally</td><td>Observed frequency, ${o}_{i}$</td><td>Relative frequency, ${f}_{i}$</td><td>Cumulative relative frequency, ${F}_{i}$</td></tr><tr><td>1</td><td>(0,1)</td><td></td><td>11</td><td>.1833</td><td>.1833</td></tr><tr><td>2</td><td>(1,2)</td><td></td><td>8</td><td>.1333</td><td>.3166</td></tr><tr><td>3</td><td>(2,3)</td><td></td><td>9</td><td>.1500</td><td>.4666</td></tr><tr><td>4</td><td>(3, 4)</td><td></td><td>7</td><td>.1167</td><td>.5833</td></tr><tr><td>5</td><td>(4,5)</td><td></td><td>6</td><td>.1000</td><td>.6833</td></tr><tr><td>6</td><td>(5,6)</td><td>州</td><td>5</td><td>.0833</td><td>.7666</td></tr><tr><td>7</td><td>(6, 7)</td><td></td><td>4</td><td>.0667</td><td>.8333</td></tr><tr><td>8</td><td>(7, 8)</td><td></td><td>2</td><td>.0333</td><td>.8666</td></tr><tr><td>9</td><td>(8, 9)</td><td></td><td>3</td><td>.0500</td><td>.9166</td></tr><tr><td>10</td><td>(9,10)</td><td></td><td>3</td><td>.0500</td><td>.9666</td></tr><tr><td>11</td><td>(10,11)</td><td></td><td>1</td><td>.0167</td><td>.9833</td></tr><tr><td>12</td><td>(11,12)</td><td></td><td>1</td><td>.0167</td><td>1.0000</td></tr><tr><td>Totals</td><td></td><td></td><td>60</td><td>1.0000</td><td></td></tr></table>

The values of ${f}_{i}$ and ${F}_{i}$ provide a "discretized" version of the pdf and the CDF for the service time. We can convert the resulting CDF into a piecewise-continuous function by joining the resulting points with linear segments. Figure 14.6 provides the empirical pdf and CDF for the example. The CDF, as given by the histogram, is defined at midpoints of the bins.

![bo_d56m56f7aajc73800ndg_14_378_200_696_590_0.jpg](bo_d56m56f7aajc73800ndg_14_378_200_696_590_0.jpg)

FIGURE 14.6

Piecewise-linear CDF of an empirical distribution

We can now estimate the mean, $\bar{t}$ , and variance, ${s}_{t}^{2}$ , of the empirical distribution. Let $N$ be the number of bins in the histogram, and define ${\bar{t}}_{i}$ as the midpoint of bin $i$ , then

$$
\bar{t} = \mathop{\sum }\limits_{{i = 1}}^{N}{f}_{i}{\bar{t}}_{i}
$$

$$
{s}_{t}^{2} = \mathop{\sum }\limits_{{i = 1}}^{N}{f}_{i}{\left( {\bar{t}}_{i} - \bar{t}\right) }^{2}
$$

Applying these formulas to the present example, we get

$$
\bar{t} = {.1833} \times  {.5} + {.133} \times  {1.5} + \cdots  + {11.5} \times  {.0167} = {3.934}\text{ minutes }
$$

$$
{s}_{t}^{2} = {.1883} \times  {\left( {.5} - {3.934}\right) }^{2} + {.1333} \times  {\left( {1.5} - {3.934}\right) }^{2} + \cdots
$$

$$
+ {.0167} \times  {\left( {11.5} - {3.934}\right) }^{2} = {8.646}{\text{ minutes }}^{2}
$$

## Excel Moment

Histograms can be constructed conveniently using Excel. Select Data Analysis $\Rightarrow$ Histogram, then enter the pertinent data in the dialogue box.

The Histogram tool in Excel does not produce the mean and standard deviation directly as part of the output. ${}^{1}$ You may use Excel template excelMeanVar.xls to calculate the sample mean, variance, maximum, and minimum. Also, Excel allows the use histogram tool.

Goodness-of-fit test. The goodness-of-fit test evaluates whether the sample used in determining the empirical distribution is drawn from a specific theoretical distribution. An initial evaluation of the data can be made by comparing the empirical CDF with the CDF of the assumed theoretical distribution. If the two CDFs do not deviate "excessively," then it is likely that the sample is drawn from the proposed theoretical distribution. This initial "hunch" can be supported further by applying the goodness-of-fit test. The following example provides the details of the proposed procedure.

---

${}^{1}$ Data Analysis in Excel does provide a separate tool called Descriptive Statistics, which can be used to compute the mean and variance (as well as volumes of other statistics you may never use!).

---

## Example 14.5-2

This example we tests the data of Example 14.5-1 for a hypothesized exponential distribution. The first task is to specify the function that defines the theoretical distribution. From Example 14.5-1, $\bar{t} = {3.934}\mathrm{\;{min}}$ . Hence, $\lambda  = \frac{1}{3.934} = {.2542}$ service per minute for the hypothesized exponential distribution (see Section 14.4.3), and the associated pdf and CDF are given as

$$
f\left( t\right)  = {.2542}{e}^{-{.2542t}}, t > 0
$$

$$
F\left( T\right)  = {\int }_{0}^{T}f\left( t\right) {dt} = 1 - {e}^{-{.2542T}}, T > 0
$$

We can use the CDF, $F\left( T\right)$ , to compute the theoretical CDF for $T = {.5},{1.5},\ldots$ , and 11.5, and then compare them graphically with empirical value ${F}_{i}, i = 1,2,\ldots ,{12}$ , as computed in Example 14.5-1 as shown in Figure 14.7. A cursory examination of the two graphs suggests tha the exponential distribution may indeed provide a reasonable fit for the observed data.

The next step is to implement a goodness-of-fit test. Two such tests exist: (1) the Kolmogrov-Smirnov test, and (2) the chi-square test. We will limit this presentation to the chi-square test.

The chi-square test is based on a measurement of the deviation between the empirical and theoretical frequencies. Specifically, for bin $i$ , the theoretical frequency ${n}_{i}$ corresponding to the observed frequency ${o}_{i}$ is computed as

$$
{n}_{i} = n{\int }_{{I}_{i - 1}}^{{I}_{i}}f\left( t\right) {dt}
$$

$$
= n\left( {F\left( {I}_{i}\right)  - F\left( {I}_{i - 1}\right) }\right)
$$

$$
= {60}\left( {{e}^{-{.2542}{I}_{i - 1}} - {e}^{-{.2542}{I}_{i}}}\right)
$$

FIGURE 14.7

Comparison of the empirical CDF and theoretical exponential CDF

![bo_d56m56f7aajc73800ndg_15_324_1535_1230_640_0.jpg](bo_d56m56f7aajc73800ndg_15_324_1535_1230_640_0.jpg)

Next, assuming $N$ bins, a measure of the deviation between the empirical and observed frequencies is computed as

$$
{\chi }^{2} = \mathop{\sum }\limits_{{i = 1}}^{N}\frac{{\left( {o}_{i} - {n}_{i}\right) }^{2}}{{n}_{i}}
$$

The measure ${\chi }^{2}$ is asymptotically a chi-square pdf with $N - k - 1$ degrees of freedom, where $k$ is the number of parameters estimated from the raw data and used for defining the theoretical distribution.

The null hypothesis for the test stating that the observed sample is drawn from the theoretical distribution $f\left( t\right)$ is accepted if

$$
\text{ H: Accept }f\left( t\right) \text{ if }{\chi }^{2} < {\chi }_{N - k - 1,1 - \alpha }^{2}
$$

The critical value ${\chi }_{N - k - 1,1 - \alpha }^{2}$ is obtained from chi-square tables (see Table A.3, Appendix A) corresponding to $N - k - 1$ degrees of freedom and a significance level $\alpha$ .

The computations of the test are shown in the following table:

<table><tr><td>$i$</td><td>Bin</td><td>Observed frequency, ${o}_{i}$</td><td>Theoretical frequency, ${n}_{i}$</td><td>${\left( {o}_{i} - {n}_{i}\right) }^{2}$ <br> ${n}_{i}$</td></tr><tr><td>1</td><td>(0,1)</td><td>11</td><td>13.448</td><td>.453</td></tr><tr><td>2</td><td>(1,2)</td><td>8</td><td>10.435</td><td>.570</td></tr><tr><td>3</td><td>(2,3)</td><td>9</td><td>8.095</td><td>.100</td></tr><tr><td>4</td><td>(3, 4)</td><td>7</td><td>6.281</td><td>.083</td></tr><tr><td>5</td><td>(4,5)</td><td>5 】11</td><td>$\left. \begin{array}{l} {4.873} \\  {3.781} \end{array}\right\}  {8.654}$</td><td>.636</td></tr><tr><td>6</td><td>(5, 6)</td><td></td><td></td><td></td></tr><tr><td>7</td><td>(6, 7)</td><td>$\left. \begin{array}{l} 4 \\  2 \\  3 \end{array}\right\}  9$</td><td></td><td></td></tr><tr><td>8</td><td>(7, 8)</td><td></td><td>$\left. \begin{array}{l} {2.933} \\  {2.276} \\  {1.766} \end{array}\right\}  {6.975}$</td><td>.588</td></tr><tr><td>9</td><td>(8, 9)</td><td></td><td></td><td></td></tr><tr><td>10</td><td>(9,10)</td><td>$\left. \begin{array}{l} 3 \\  1 \\  1 \end{array}\right\}  5$</td><td>$\left. \begin{array}{l} {1.370} \\  {1.063} \\  {3.678} \end{array}\right\}  {6.111}$</td><td></td></tr><tr><td>11</td><td>(10,11)</td><td></td><td></td><td>.202</td></tr><tr><td>12</td><td>(11, ∞)</td><td></td><td></td><td></td></tr><tr><td colspan="2">Totals</td><td>$n = {60}$</td><td>$n = {60}$</td><td>${\chi }^{2}$ -value $= {2.623}$</td></tr></table>

As a rule of thumb, the theoretical frequency count in any bin must be at least 5 . This requirement is usually resolved by combining successive bins until the rule is satisfied, as shown in the table. The resulting number of bins becomes $N = 7$ . Because we are estimating one parameter from the observed data (namely, $\lambda$ ), the degrees of freedom for the chi-square is $7 - 1 - 1 = 5$ . If we assume a significance level $\alpha  = {.05}$ , we get the critical value ${\chi }_{5,{.05}}^{2} = {11.07}$ (use Table A. 3 in Appendix A, or, in excelStatTables.xls, enter 5 in F8 and .05 in L8, and get the answer in R8). Because the ${\chi }^{2}$ -value (=2.623) is less than the critical value, we accept the hypothesis that the sample is drawn from an exponential pdf.

## Aha! Moment: Mark Twain Gives "Statistics" a Bum Wrap!

In a nutshell: statistics is all about data and how to interpret them. The goal is to predict the future, not with certainty but with a reasonable degree of confidence. It is a noble goal; so why is statistics getting a bum wrap? Mark Twain's infamous quote "There are lies, damned lies, and statistics," Darrell Huff's "How to Lie with Statistics" (in print since 1954), and, more recently, Joel Best's "More Damned Lies and Statistics," are but three popularly adopted slogans/books that tend to cast doubt about statistics and its use.

Actually, we are talking about two distinct types of "statistics": The one often criticized is used by media and politicians, and the other is used in OR studies (and other sciences) to intelligently assess the past and predict the future. In the first type, simple statistical measures, including averages, percentage, and pie/bar charts, are sometimes misused in connection with situations of public interest. For example, the proposed U.S. tax cut in 2001 claimed an average reduction in tax burden of over \$1000 per family, but did not add that 50% of all families would receive less than \$100 - left unsaid: the tax cut favored the rich! In the second type, OR and other sciences use sophisticated statistical tools to reach robust conclusions about the future behavior of a system. This is the type that interests us, and, properly utilized, it is an indispensable tool in practically all OR projects.

## BIBLIOGRAPHY

Feller, W., An Introduction to Probability Theory and Its Applications, 2nd ed., Vols. 1 and 2, Wiley, New York, 1967.

Paulos, J.A., Innumeracy: Mathematical Illiteracy and Its Consequences, Hill and Wang, New York, 1988.

Papoulis, A., Probability and Statistics, Prentice Hall, Upper Saddle River, NJ, 1990.

Ross, S., Introduction to Probability Models, 10th ed., Academic Press, New York, 2011.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>14.1</td><td>14-1 to 14-3</td><td>14.3.2</td><td>14-26 to 14-26</td></tr><tr><td>14.1.1</td><td>14-4 to 14-7</td><td>14.4.1</td><td>14-27 to 14-32</td></tr><tr><td>14.1.2</td><td>14-8 to 14-14</td><td>14.4.2</td><td>14-33 to 14-36</td></tr><tr><td>14.2</td><td>14-15 to 14-17</td><td>14.4.3</td><td>14-37 to 14-38</td></tr><tr><td>14.3</td><td>14-18 to 14-20</td><td>14.4.4</td><td>14-39 to 14-41</td></tr><tr><td>14.3.1</td><td>14-21 to 14-25</td><td>14.5</td><td>14-42 to 14-44</td></tr></table>

*14-1. In a survey conducted in the State of Arkansas high schools to study the correlation between senior year scores in mathematics and enrollment in engineering colleges, 400 out of 1000 surveyed seniors have studied mathematics. Engineering enrollment shows that, of the 1000 seniors, 150 students have studied mathematics and 29 have not. Determine the probabilities of the following events:

(a) A student who studied mathematics is (is not) enrolled in engineering.

(b) A student neither studied mathematics nor enrolled in engineering.

(c) A student is not studying engineering.

*14-2. Consider a random gathering of $n$ persons. Determine the smallest $n$ that will make it more likely that two persons or more have the same birthday. (Hint: Assume no leap years and that all days of the year are equally likely to be a person's birthday.)

*14-3. Answer Problem 14-2 assuming that in a room full of $n$ persons at least one person shares your birthday.

14-4. A fair 6-faced die is tossed twice. Letting $E$ and $F$ represent the outcomes of the two tosses, compute the following probabilities:

(a) The sum of $E$ and $F$ is 10 .

(b) The sum of $E$ and $F$ is even.

(c) The sum of $E$ and $F$ is odd and greater than 3 .

(d) $E$ is odd less than 6 and $F$ is even greater than 1 .

(e) $E$ is greater than 2 and $F$ is less than 4 .

(f) $E$ is 4 and the sum of $E$ and $F$ is even.

14-5. Two dice are rolled independently and the two numbers that turn up are recorded. Determine the following:

(a) The probability that the two numbers are odd with values less than 5.

(b) The probability that the sum of the two numbers is 10.

(c) The probability that the two numbers differ by at least 3.

*14-6. You can toss a fair coin up to 7 times. You will win \$100 if three tails appear before a head is encountered. What are your chances of winning?

*14-7. Ann, Jim, John, and Nancy are scheduled to compete in a racquetball tournament. Ann is twice as likely to beat Jim, and Jim is at the same level as John. Nancy's past winning record against John is one out of three. Determine the following:

(a) The probability that Jim will win the tournament.

(b) The probability that a woman will win the tournament.

(c) The probability that no woman will win.

14-8. In Example 14.1-2, suppose that you are told that the outcome is less than 6.

(a) Determine the probability of getting an even number.

(b) Determine the probability of getting an odd number larger than one.

14-9. The stock of WalMark Stores, Inc. trades on the New York Stock Exchange under the symbol WMS. Historically, the price of WMS goes upward with the Dow 65% of the time and goes downward with the Dow 20% of the time. There is also a 10% chance that WMS will go up when the Dow goes down and 5% that it will go down when the Dow goes up.

(a) Determine the probability that WMS will go up regardless of the Dow.

(b) Find the probability that WMS goes up given that the Dow is up.

(c) What is the probability WMS goes down given that Dow is down?

*14-10. Graduating high school seniors with an ACT score of at least 26 can seek admission in two universities, A and B. The probability of being accepted in A is .4 and in B .25. The chance of being accepted in both universities is only 15%.

(a) Determine the probability that the student is accepted in B given that A has granted admission as well.

(b) What is the probability that admission will be granted in A given that the student was accepted in B?

14-11. Prove that if the probability $P\{ A \mid  B\}  = P\{ A\}$ , then $A$ and $B$ must be independent.

14-12. Bayes’ theorem. ${}^{2}$ Given the two events $A$ and $B$ , show that

$$
P\{ A \mid  B\}  = \frac{P\{ B \mid  A\} P\{ A\} }{P\{ B\} }, P\{ B\}  > 0
$$

14-13. A retailer receives 70% of its batteries from Factory $A$ and 30% from Factory $B$ . The percentages of defectives produced by $A$ and $B$ are known to be 3% and 5%, respectively. A customer has just bought a battery randomly from the retailer.

(a) What is the probability that the battery is defective?

(b) If a battery is defective, what is the probability that it came from Factory A? (Hint: Use Bayes' theorem in Problem 14-12.)

*14-14. Statistics show that 70% of all men have some form of prostate cancer. The PSA test will show positive 90% of the time for afflicted men and 10% of the time for healthy men. What is the probability that a man who tested positive does have prostate cancer?

14-15. The number of units, $x$ , needed of an item is discrete from 1 to 6 . The probability, $p\left( x\right)$ , is directly proportional to the number of units needed. The constant of proportionality is $K$ .

(a) Determine the pdf and CDF of $x$ , and graph the resulting functions.

(b) Find the probability that $x$ is an even value.

14-16. Consider the following function:

$$
f\left( x\right)  = \frac{k}{{x}^{2}},{10} \leq  x \leq  {20}
$$

*(a) Determine the value of the constant $k$ that will render $f\left( x\right)$ a pdf.

(b) Determine the CDF, and find the probability that $x$ is (i) larger than 12 and (ii) between 13 and 15.

*14-17. The daily demand for unleaded gasoline is uniformly distributed between 750 and 1250 gallons. The 1100-gallon gasoline tank is refilled daily at midnight. What is the probability that the tank will be empty just before a refill?

14-18. In Example 14.3-1, compute the average shortage of stamps per month. (Hint: Shortage can occur if I need more than 20 stamps.)

14-19. The results of Example 14.3-1 and of Problem 14-18 show positive averages for both the surplus and shortage of stamps. Are these results inconsistent? Explain.

*14-20. The owner of a newspaper stand receives 50 copies of Al Ahram newspaper every morning. The number of copies sold, $x$ , varies randomly according to the following probability distribution:

$$
p\left( x\right)  = \left\{  \begin{array}{l} \frac{1}{45}, x = {35},{36},\ldots ,{49} \\  \frac{1}{30}, x = {50},{51},\ldots ,{59} \\  \frac{1}{33}, x = {60},{61},\ldots ,{70} \end{array}\right.
$$

(a) Determine the probability that the owner will sell out completely.

(b) Determine the expected number of unsold copies per day.

(c) A single copy costs 50 cents and sells for \$1.00. Unsold copies have no value. Determine the expected net income per day.

---

${}^{2}$ Section 15.2.2 provides more details about Bayes’ theorem.

---

*14-21. Compute the mean and variance of the random variable defined in Problem 14-15.

14-22. Compute the mean and variance of the random variable in Problem 14-16.

14-23. Show that the mean and variance of a uniform random variable $x, a \leq  x \leq  b$ , are

$$
E\{ x\}  = \frac{b + a}{2}
$$

$$
\operatorname{var}\{ x\}  = \frac{{\left( b - a\right) }^{2}}{12}
$$

14-24. For the pdf $f\left( x\right)$ , prove that

$$
\operatorname{var}\{ x\}  = E\left\{  {x}^{2}\right\}   - {\left( E\{ x\} \right) }^{2}
$$

14-25. Given the pdf $f\left( x\right)$ and $y = {cx} + d$ , where $c$ and $d$ are constants, prove that

$$
E\{ y\}  = {cE}\{ x\}  + d
$$

$$
\operatorname{var}\{ y\}  = {c}^{2}\operatorname{var}\{ x\}
$$

14-26. The joint pdf of ${x}_{1}$ and ${x}_{2}$ is

<table><tr><td></td><td>${x}_{2} = 1$</td><td>${x}_{2} = 2$</td><td>${x}_{2} = 3$</td></tr><tr><td>${x}_{1} = 1$</td><td>.2</td><td>0</td><td>.2</td></tr><tr><td>$p\left( {{x}_{1},{x}_{2}}\right)  = {x}_{1} = 2$</td><td>0</td><td>.2</td><td>0</td></tr><tr><td>${x}_{1} = 3$</td><td>.2</td><td>0</td><td>.2</td></tr></table>

*(a) Find the marginal pdfs ${p}_{1}\left( {x}_{1}\right)$ and ${p}_{2}\left( {x}_{2}\right)$ .

*(b) Are ${x}_{1}$ and ${x}_{2}$ independent?

(c) Compute $E\left\{  {{x}_{1} + {x}_{2}}\right\}$ .

(d) Compute $\operatorname{cov}\left\{  {{x}_{1},{x}_{2}}\right\}$ .

(e) Compute $\operatorname{var}\left\{  {5{x}_{1} - 6{x}_{2}}\right\}$ .

*14-27. A fair die is rolled 10 times. What is the probability that the rolled die will not show an even number?

14-28. Suppose that four fair coins are tossed independently. What is the probability that exactly one of the coins will be different from the remaining three?

*14-29. A fortune-teller claims to predict whether people will amass financial wealth in their lifetime by examining their handwriting. To verify this claim, 10 millionaires and 10 university professors were asked to provide samples of their handwriting. The samples are then paired, one millionaire and one professor, and presented to the fortune-teller. We say that the claim is true if the fortune-teller makes at least eight correct predictions. What is the probability that the claim is correct?

14-30. In a gambling casino, you play the game of selecting a number from 1 to 6 before the operator rolls three fair dice simultaneously. The casino pays you as many dollars as the number of dice that match your selection. If there is no match, you pay the casino only \$1. Determine your long-run expected payoff.

14-31. Suppose that you throw 2 fair dice simultaneously. If there is a match, you receive 50 cents. Otherwise, you pay 10 cents. Determine the expected payoff of the game.

14-32. Prove the formulas for the mean and variance of the binomial distribution.

*14-33. Customers arrive at a service facility according to a Poisson distribution at the rate of three per minute. What is the probability that at least one customer will arrive in any given 45-second interval?

14-34. The Poisson distribution with parameter $\lambda$ approximates the binomial distribution with parameters $\left( {n, p}\right)$ when $n \rightarrow  \infty , p \rightarrow  0$ , and ${np} \rightarrow  \lambda$ . Demonstrate this result for the situation where a manufactured lot is known to contain 1% defective items. If a sample of 10 items is taken from the lot, compute the probability of at most one defective item in a sample, first by using the (exact) binomial distribution and then by using the (approximate) Poisson distribution. Show that the approximation will not be acceptable if the value of $p$ is increased to, say,0.5 .

*14-35. Customers arrive randomly at a checkout counter at the average rate of 10 per hour.

(a) Determine the probability that the counter is idle.

(b) What is the probability that at least one person is in line awaiting service?

14-36. Prove the formulas for the mean and variance of the Poisson distribution.

*14-37. Customers shopping at Walmark Store are both urban and suburban. Urban customers arrive at the rate of 5 per minute, and suburban customers arrive at the rate of 10 per minute. Arrivals are totally random. Determine the probability that the interarrival time for all customers is less than 8 seconds.

14-38. Prove the formulas for the mean and variance of the exponential distribution.

14-39. The college of engineering at $\mathrm{U}$ of $\mathrm{A}$ requires a minimum $\mathrm{{ACT}}$ score of 27. The test scores among high school seniors in a given school district are normally distributed with mean 23 and standard deviation 4.

(a) Determine the percentage of high school seniors who are potential engineering recruits.

(b) If U of A does not accept any student with an ACT score less than 17, what percentage of students will not be eligible for admission at U of A?

*14-40. The weights of individuals who seek a helicopter ride in an amusement park have a mean of 180 lb and a standard deviation of 15 lb. The helicopter can carry five persons but has a maximum weight capacity of 1000 lb. What is the probability that the helicopter will not take off with five persons aboard? (Hint: Apply the central limit theorem.)

14-41. The inside diameter of a cylinder is normally distributed with a mean of $1\mathrm{\;{cm}}$ and a standard deviation of ${.01}\mathrm{\;{cm}}$ . A solid rod is assembled inside each cylinder. The diameter of the rod is also normally distributed with a mean of ${.99}\mathrm{\;{cm}}$ and a standard deviation of .01 cm. Determine the percentage of rod-cylinder pairs that will not fit in an assembly. (Hint: The difference between two normal random variables is also normal.)

14-42. The following data represent the interarrival time (in minutes) at a service facility:

<table><tr><td>4.3</td><td>3.4</td><td>.9</td><td>.7</td><td>5.8</td><td>3.4</td><td>2.7</td><td>7.8</td></tr><tr><td>4.4</td><td>.8</td><td>4.4</td><td>1.9</td><td>3.4</td><td>3.1</td><td>5.1</td><td>1.4</td></tr><tr><td>.1</td><td>4.1</td><td>4.9</td><td>4.8</td><td>15.9</td><td>6.7</td><td>2.1</td><td>2.3</td></tr><tr><td>2.5</td><td>3.3</td><td>3.8</td><td>6.1</td><td>2.8</td><td>5.9</td><td>2.1</td><td>2.8</td></tr><tr><td>3.4</td><td>3.1</td><td>.4</td><td>2.7</td><td>.9</td><td>2.9</td><td>4.5</td><td>3.8</td></tr><tr><td>6.1</td><td>3.4</td><td>1.1</td><td>4.2</td><td>2.9</td><td>4.6</td><td>7.2</td><td>5.1</td></tr><tr><td>2.6</td><td>.9</td><td>4.9</td><td>2.4</td><td>4.1</td><td>5.1</td><td>11.5</td><td>2.6</td></tr><tr><td>.1</td><td>10.3</td><td>4.3</td><td>5.1</td><td>4.3</td><td>1.1</td><td>4.1</td><td>6.7</td></tr><tr><td>2.2</td><td>2.9</td><td>5.2</td><td>8.2</td><td>1.1</td><td>3.3</td><td>2.1</td><td>7.3</td></tr><tr><td>3.5</td><td>3.1</td><td>7.9</td><td>.9</td><td>5.1</td><td>6.2</td><td>5.8</td><td>1.4</td></tr><tr><td>.5</td><td>4.5</td><td>6.4</td><td>1.2</td><td>2.1</td><td>10.7</td><td>3.2</td><td>2.3</td></tr><tr><td>3.3</td><td>3.3</td><td>7.1</td><td>6.9</td><td>3.1</td><td>1.6</td><td>2.1</td><td>1.9</td></tr></table>

(a) Use Excel to develop three histograms for the data based on bin widths of .5, 1, and 1.5 minutes, respectively.

(b) Compare graphically the cumulative distribution of the empirical CDF and that of a corresponding exponential distribution.

(c) Test the hypothesis that the given sample is drawn from an exponential distribution. Use a 95% confidence level.

(d) Which of the three histograms is "best" for the purpose of testing the null hypothesis?

14-43. The following data represent the period (in seconds) needed to transmit a message.

<table><tr><td>25.8</td><td>67.3</td><td>35.2</td><td>36.4</td><td>58.7</td></tr><tr><td>47.9</td><td>94.8</td><td>61.3</td><td>59.3</td><td>93.4</td></tr><tr><td>17.8</td><td>34.7</td><td>56.4</td><td>22.1</td><td>48.1</td></tr><tr><td>48.2</td><td>35.8</td><td>65.3</td><td>30.1</td><td>72.5</td></tr><tr><td>5.8</td><td>70.9</td><td>88.9</td><td>76.4</td><td>17.3</td></tr><tr><td>77.4</td><td>66.1</td><td>23.9</td><td>23.8</td><td>36.8</td></tr><tr><td>5.6</td><td>36.4</td><td>93.5</td><td>36.4</td><td>76.7</td></tr><tr><td>89.3</td><td>39.2</td><td>78.7</td><td>51.9</td><td>63.6</td></tr><tr><td>89.5</td><td>58.6</td><td>12.8</td><td>28.6</td><td>82.7</td></tr><tr><td>38.7</td><td>71.3</td><td>21.1</td><td>35.9</td><td>29.2</td></tr></table>

Use Excel to construct a suitable histogram. Test the hypothesis that these data are drawn from a uniform distribution at a 95% confidence level, given the following additional information about the theoretical uniform distribution:

(a) The range of the distribution is between 0 and 100.

(b) The range of the distribution is estimated from the sample data.

(c) The maximum limit on the range of the distribution is 100 , but the minimum limit must be estimated from the sample data.

14-44. An automatic device is used to count the volume of traffic at a busy intersection. The arrival time is recorded and translated into an absolute time starting from zero. The following table provides the arrival times (in minutes) for the first 60 cars. Use Excel to construct a suitable histogram. Test the hypothesis that the interarrival time is exponential using a 95% confidence level.

<table><tr><td>Arrival</td><td>Arrival time (min)</td><td>Arrival</td><td>Arrival time (min)</td><td>Arrival</td><td>Arrival time (min)</td><td>Arrival</td><td>Arrival time (min)</td></tr><tr><td>1</td><td>5.2</td><td>16</td><td>67.6</td><td>31</td><td>132.7</td><td>46</td><td>227.8</td></tr><tr><td>2</td><td>6.7</td><td>17</td><td>69.3</td><td>32</td><td>142.3</td><td>47</td><td>233.5</td></tr><tr><td>3</td><td>9.1</td><td>18</td><td>78.6</td><td>33</td><td>145.2</td><td>48</td><td>239.8</td></tr><tr><td>4</td><td>12.5</td><td>19</td><td>86.6</td><td>34</td><td>154.3</td><td>49</td><td>243.6</td></tr><tr><td>5</td><td>18.9</td><td>20</td><td>91.3</td><td>35</td><td>155.6</td><td>50</td><td>250.5</td></tr><tr><td>6</td><td>22.6</td><td>21</td><td>97.2</td><td>36</td><td>166.2</td><td>51</td><td>255.8</td></tr><tr><td>7</td><td>27.4</td><td>22</td><td>97.9</td><td>37</td><td>169.2</td><td>52</td><td>256.5</td></tr><tr><td>8</td><td>29.9</td><td>23</td><td>111.5</td><td>38</td><td>169.5</td><td>53</td><td>256.9</td></tr><tr><td>9</td><td>35.4</td><td>24</td><td>116.7</td><td>39</td><td>172.4</td><td>54</td><td>270.3</td></tr><tr><td>10</td><td>35.7</td><td>25</td><td>117.3</td><td>40</td><td>175.3</td><td>55</td><td>275.1</td></tr><tr><td>11</td><td>44.4</td><td>26</td><td>118.2</td><td>41</td><td>180.1</td><td>56</td><td>277.1</td></tr><tr><td>12</td><td>47.1</td><td>27</td><td>124.1</td><td>42</td><td>188.8</td><td>57</td><td>278.1</td></tr><tr><td>13</td><td>47.5</td><td>28</td><td>1127.4</td><td>43</td><td>201.2</td><td>58</td><td>283.6</td></tr><tr><td>14</td><td>49.7</td><td>29</td><td>127.6</td><td>44</td><td>218.4</td><td>59</td><td>299.8</td></tr><tr><td>15</td><td>67.1</td><td>30</td><td>127.8</td><td>45</td><td>219.9</td><td>60</td><td>300.0</td></tr></table>

This page intentionally left blank