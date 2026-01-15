## CHAPTER 15 Decision Analysis and Games

## Real-Life Application—Layout Planning of a Computer Integrated Manufacturing (CIM) Facility

The engineering college in an academic institution wants to establish a computer integrated manufacturing (CIM) laboratory in a vacated building. The new lab will serve as a teaching and research facility and as industry center of technical excellence. Recommendations regarding the ideal and absolute minimum square footage for each unit are solicited and compiled from the faculty. The study uses both AHP (analytic hierarchy process) and goal programming to reach a satisfactory compromise solution that meets the goals for teaching, research, and service to industry. The details of the study are given in Case 10 in Chapter 26 on the website.

### 15.1 DECISION MAKING UNDER CERTAINTY—ANALYTIC HIERARCHY PROCESS (AHP)

The LP models presented in Chapters 2 through 9 are examples of decision making under certainty (all the data are known with certainty). AHP is designed for situations in which ideas, feelings, and emotions affecting the decision process are quantified to provide a numeric scale for prioritizing the alternatives.

## Example 15.1-1 (Overall Idea of AHP)

Martin Hans, a bright high school senior, has received full academic scholarships from three institutions: U of A, U of B, and U of C. Martin bases his choice on two criteria: location and academic reputation. To him, academic reputation is five times as important as location, and he assigns a weight of approximately 83% to reputation and 17% to location. He then uses a systematic process (which will be detailed later) to rank the three universities from the standpoint of location and reputation, as the following table shows:

![bo_d56m58jef24c73bhe65g_1_282_198_1301_678_0.jpg](bo_d56m58jef24c73bhe65g_1_282_198_1301_678_0.jpg)

FIGURE 15.1

Summary of AHP calculations for Example 15.1-1

<table><tr><td rowspan="2">Criterion</td><td colspan="3">Percent weight estimates for</td></tr><tr><td>U of A</td><td>U of B</td><td>U of C</td></tr><tr><td>Location</td><td>12.9</td><td>27.7</td><td>59.4</td></tr><tr><td>Reputation</td><td>54.5</td><td>27.3</td><td>18.2</td></tr></table>

The structure of the decision problem is summarized in Figure 15.1. The problem involves a single hierarchy (level) with two criteria (location and reputation) and three decision alternatives (U of A, U of B, and U of C).

The ranking of each university is based on the following composite weights:

$$
\text{ U of A } = {.17} \times  {.129} + {.83} \times  {.545} = {.4743}
$$

$$
\text{ U of B } = {.17} \times  {.277} + {.83} \times  {.273} = {.2737}
$$

$$
\mathrm{U}\text{ of }\mathrm{C} = {.17} \times  {.594} + {.83} \times  {.182} = {.2520}
$$

Based on these calculations, Martin chooses U of A because it has the highest composite weight.

Remarks. The general structure of AHP may include several hierarchies of criteria. Suppose in Example 15.1-1 that Martin's twin sister, Jane, was also accepted with full scholarship to the three universities. The parents insist that the two siblings attend the same university. Figure 15.2 summarizes the decision problem, which now involves two hierarchies. The values $p$ and $q$ at the first hierarchy are the relative weights representing Martin's and Jane's opinions (presumably equal). The weights $\left( {{p}_{1},{p}_{2}}\right)$ and $\left( {{q}_{1},{q}_{2}}\right)$ at the second hierarchy, respectively, represent Martin’s and

![bo_d56m58jef24c73bhe65g_2_329_199_1298_949_0.jpg](bo_d56m58jef24c73bhe65g_2_329_199_1298_949_0.jpg)

FIGURE 15.2

Embellishment of the decision problem of Example 15.1-1

Jane's preferences regarding location and reputation of each university. The remainder of the decision-making chart can be interpreted similarly. Note that $p + q = 1$ , ${p}_{1} + {p}_{2} = 1,{q}_{1} + {q}_{2} = 1,{p}_{11} + {p}_{12} + {p}_{13} = 1,{p}_{21} + {p}_{22} + {p}_{23} = 1,{q}_{11} + {q}_{12} + {q}_{13} = 1$ , and ${q}_{21} + {q}_{22} + {q}_{23} = 1$ . The bottom of Figure 15.2 demonstrates how the U of A composite weight is computed.

Determination of the weights. The crux of AHP is the determination of the relative weights (such as those used in Example 15.1-1) to rank the alternatives. Assuming that we are dealing with $n$ criteria at a given hierarchy, AHP establishes a pairwise $n \times  n$ comparison matrix, $\mathbf{A}$ , that quantifies the decision maker’s judgment of the relative importance of the criteria. The pairwise comparison is made such that the criterion in row $i\left( {i = 1,2,\ldots , n}\right)$ is ranked relative to every other criterion. Letting ${a}_{ij}$ define the element $\left( {i, j}\right)$ of $\mathbf{A},$ AHP uses a numeric scale from 1 to 9 in which ${a}_{ij} = 1$ signifies that $i$ and $j$ are of equal importance, ${a}_{ij} = 5$ indicates that $i$ is strongly more important than $j$ , and ${a}_{ij} = 9$ indicates that $i$ is extremely more important than $j$ . Other intermediate values between 1 and 9 are interpreted correspondingly. Consistency in judgment means that if ${a}_{ij} = k$ , then ${a}_{ji} = \frac{1}{k}$ . Also, all the diagonal elements ${a}_{ii}$ of $\mathbf{A}$ equal 1, because these elements rank each criterion against itself.

## Example 15.1-2

To show how the comparison matrix $\mathbf{A}$ is determined for Martin’s decision problem of Example 15.1-1, we start with the top hierarchy dealing with the criteria of location $\left( L\right)$ and reputation $\left( R\right)$ . In Martin’s judgment, $R$ is strongly more important than $L$ , and hence ${a}_{21} = 5$ and, automatically, ${a}_{12} = \frac{1}{5}$ , thus yielding the following comparison matrix:

$$
\mathbf{A} = \frac{L}{R}\left( \begin{array}{ll} 1 & \frac{1}{5} \\  5 & 1 \end{array}\right)
$$

The relative weights of $R$ and $L$ can be determined by normalizing $\mathbf{A}$ to create a new matrix N. The process requires dividing the individual elements of each column by the column sum. Thus, we divide the elements of columns 1 by $6\left( {1 + 5}\right)$ and those of column 2 by ${1.2}\left( { = \frac{1}{5} + 1}\right)$ . The desired relative weights, ${w}_{R}$ and ${w}_{L}$ , are then computed as row averages:

$$
\mathbf{N} = \frac{L}{R}\left( \begin{array}{ll} {.17} & {.17} \\  {.83} & {.83} \end{array}\right) \;\begin{array}{l} {w}_{L} = \frac{{.17} + {.17}}{2} = {.17} \\  {w}_{R} = \frac{{.83} + {.83}}{2} = {.83} \end{array}
$$

The computations yield ${w}_{L} = {.17}$ and ${w}_{R} = {.83}$ , the weights we used in Figure 15.1. The columns of $\mathbf{N}$ are equal, an indication that the decision maker is exhibiting consistent judgment in specifying the entries of the comparison matrix $\mathbf{A}$ . Consistency is always guaranteed in $2 \times  2$ comparison matrices but not in higher-order matrices (as we explain shortly).

Martin's preferences regarding the relative importance of the three universities from the standpoint of the two criteria $L$ and $R$ are summarized in the following comparison matrices:

$$
{\mathbf{A}}_{L} = B\left( \begin{matrix} A & B & C & A & B & C \\  1 & \frac{1}{2} & \frac{1}{5} & A & A & C \\  2 & 1 & \frac{1}{2} & \frac{1}{2} & C & C \\  5 & 2 & 1 & C & C & \frac{1}{3} \end{matrix}\right) ,\;{\mathbf{A}}_{R} = B\left( \begin{matrix} 1 & 2 & 3 \\  \frac{1}{2} & 1 & \frac{3}{2} \\  \frac{1}{3} & \frac{2}{3} & 1 \end{matrix}\right)
$$

Next, we have

$$
{\mathbf{A}}_{L}\text{ -column sum } = \left( {8,{3.5},{1.7}}\right)
$$

$$
{\mathbf{A}}_{R}\text{ -column sum } = \left( {{1.83},{3.67},{5.5}}\right)
$$

The normalized matrices are determined by dividing each column-entry by its respective column-sum-namely,

$$
\begin{array}{l} {\mathbf{N}}_{L} = B\left( {-{125},{143},{118}}\right) \;{w}_{LA} = \frac{{.125} + {.143} + {.118}}{-{.125} + {.133} + {.118}} = {.129} \\  {\mathbf{N}}_{L} = B\left( {{.250},{.286},{294}}\right) \;{w}_{LB} = \frac{{.250} + {.286} + {.294}}{3} = {.277} \\  C\left( {{.625},{.571},{.588}}\right) \;{w}_{LC} = \frac{{.625} + {.571} + {.588}}{3} = {.594} \\  \end{array}
$$

$$
{\mathbf{N}}_{R} = \begin{array}{llll} A & B & C & \text{ Rowaverages } \\  A & \left( {{.545}\;{.545}}\right) & {.545} & {w}_{LA} = \frac{{.545}\; + \;{.545}}{3} + {.545} = {.545} \\  C & {.273} & {.273} & {w}_{LB} = \frac{{.273}\; + \;{.273}}{3} + {.273} = {.273} \\  C & {.182} & {.182} & {.182} \end{array}
$$

The values of $\left( {{w}_{LA},{w}_{LB}\text{ , and }{w}_{LC}}\right) \left( { = {.129},{.277}\text{ , and .594 }}\right)$ provide the respective location weights for $\mathrm{U}$ of $\mathrm{A},\mathrm{U}$ of $\mathrm{B}$ , and $\mathrm{U}$ of $\mathrm{C}$ , respectively. Similarly, the values of $\left( {{w}_{RA},{w}_{RB}}\right.$ , and ${w}_{RC})\left( { = {.545},{.273},{.182}}\right)$ give the relative weights regarding academic reputation of the three universities. These are the values used in Figure 15.1.

Consistency of the comparison matrix. In Example 15.1-2, all the columns of the normalized matrices $\mathbf{N}$ and ${\mathbf{N}}_{R}$ are identical, and those of ${\mathbf{N}}_{L}$ are not. This means that $\mathbf{A}$ and ${\mathbf{A}}_{R}$ are consistent and ${\mathbf{A}}_{L}$ is not.

Consistency implies rational judgment on the part of the decision maker. Mathematically, we say that a comparison matrix $\mathbf{A}$ is consistent if

$$
{a}_{ij}{a}_{jk} = {a}_{ik}\text{ , for all }i, j\text{ , and }k
$$

For example, in matrix ${\mathbf{A}}_{R}$ of Example 15.1-2, ${a}_{13} = 3$ and ${a}_{12}{a}_{23} = 2 \times  \frac{3}{2} = 3$ . This property requires all the columns (and rows) of ${\mathbf{A}}_{R}$ to be linearly dependent. In particular, the columns of any $2 \times  2$ comparison matrix, such as $\mathbf{A}$ , are by definition dependent, and hence a $2 \times  2$ matrix is always consistent.

It is unusual for higher-order comparison matrices to be always consistent, and a degree of inconsistency is expected. To decide what level of inconsistency is "tolerable," we need to develop a quantifiable measure of consistency for the comparison matrix $\mathbf{A}$ . We have seen in Example 15.1-2 that a consistent $\mathbf{A}$ produces a normalized matrix $\mathbf{N}$ in which all the columns are identical - that is,

$$
\mathbf{N} = \left( \begin{matrix} {w}_{1} & {w}_{1} & \ldots & {w}_{1} \\  {w}_{2} & {w}_{2} & \ldots & {w}_{2} \\  \ldots & \ldots & \ldots & \ldots \\  {w}_{n} & {w}_{n} & \ldots & {w}_{n} \end{matrix}\right)
$$

The original comparison matrix $\mathbf{A}$ can be determined from $\mathbf{N}$ by a reverse process that divides the elements of column $i$ by ${w}_{i}$ -that is,

$$
\mathbf{A} = \left( \begin{matrix} 1 & \frac{{w}_{1}}{{w}_{2}} & \ldots & \frac{{w}_{1}}{{w}_{n}} \\  \frac{{w}_{2}}{{w}_{1}} & 1 & \ldots & \frac{{w}_{2}}{{w}_{n}} \\  \ldots & \ldots & \ldots & \ldots \\  \frac{{w}_{n}}{{w}_{1}} & \frac{{w}_{n}}{{w}_{2}} & \ldots & 1 \end{matrix}\right)
$$

Post-multiplying $\mathbf{A}$ by $\mathbf{w} = {\left( {w}_{1},{w}_{2},\ldots ,{w}_{n}\right) }^{T}$ , we get

$$
\left( \begin{matrix} 1 & \frac{{w}_{1}}{{w}_{2}} & \ldots & \frac{{w}_{1}}{{w}_{n}} \\  \frac{{w}_{2}}{{w}_{1}} & 1 & \ldots & \frac{{w}_{2}}{{w}_{n}} \\  \ldots & \ldots & \ldots & \ldots \\  \frac{{w}_{n}}{{w}_{1}} & \frac{{w}_{n}}{{w}_{2}} & \ldots & 1 \end{matrix}\right) \left( \begin{matrix} {w}_{1} \\  {w}_{2} \\  \ldots \\  {w}_{n} \end{matrix}\right)  = \left( \begin{matrix} n{w}_{1} \\  n{w}_{2} \\  \ldots \\  n{w}_{n} \end{matrix}\right)  = n\left( \begin{matrix} {w}_{1} \\  {w}_{2} \\  \ldots \\  {w}_{n} \end{matrix}\right)
$$

Hence, $\mathbf{A}$ is consistent if,

$$
\mathbf{{Aw}} = n\mathbf{w}
$$

For the case where $\mathbf{A}$ is not consistent, the relative weight, ${w}_{i}$ , is approximated by the average of the $n$ elements of row $i$ in the normalized matrix $\mathbf{N}$ (see Example 15.1-2). Letting $\overline{\mathbf{w}}$ be the vector of computed averages, it can be shown that

$$
\mathbf{A}\overline{\mathbf{w}} = {n}_{\max }\overline{\mathbf{w}},{n}_{\max } \geq  n
$$

In this case, the closer ${n}_{\max }$ is to $n$ , the more consistent is the comparison matrix $\mathbf{A}$ . Based on this observation, AHP computes the consistency ratio as

$$
{CR} = \frac{CI}{RI}
$$

where

$$
{CI} = \text{ Consistency index of }\mathbf{A}
$$

$$
= \frac{{n}_{\max } - n}{n - 1}
$$

$$
{RI} = \text{ Random consistency of }\mathbf{A}
$$

$$
= \frac{{1.98}\left( {n - 2}\right) }{n}
$$

The random consistency index, ${RI}$ , is determined empirically as the average ${CI}$ of a large sample of randomly generated comparison matrices, $\mathbf{A}$ .

If ${CR} \leq  {.1}$ , the level of inconsistency is acceptable. Otherwise, the inconsistency is high, and the decision maker may need to revise the estimates of the elements ${a}_{ij}$ to realize better consistency.

The value of ${n}_{\max }$ is computed from $\mathbf{A}\overline{\mathbf{w}} = {n}_{\max }\overline{\mathbf{w}}$ by noting that the $i$ th equation is

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{\bar{w}}_{j} = {n}_{\max }{\bar{w}}_{i}, i = 1,2,\ldots , n
$$

Given $\mathop{\sum }\limits_{{i = 1}}^{n}{\bar{w}}_{i} = 1$ , we get

$$
\mathop{\sum }\limits_{{i = 1}}^{n}\left( {\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{\bar{w}}_{j}}\right)  = {n}_{\max }\mathop{\sum }\limits_{{i = 1}}^{n}{\bar{w}}_{i} = {n}_{\max }
$$

This means that the value of ${n}_{\max }$ equals the sum of the elements of the column vector $\mathbf{A}\overline{\mathbf{w}}$ .

## Example 15.1-3

In Example 15.1-2, the matrix ${\mathbf{A}}_{L}$ is inconsistent because the columns of its ${\mathbf{N}}_{L}$ are not identical. To test the consistency of ${\mathbf{N}}_{L}$ , we start by computing ${n}_{\max }$ . From Example 15.1-2, we have

$$
{\bar{w}}_{1} = {.129},{\bar{w}}_{2} = {.277},{\bar{w}}_{3} = {.594}
$$

Thus,

$$
{\mathbf{A}}_{L}\overline{\mathbf{w}} = \left( \begin{matrix} 1 & \frac{1}{2} & \frac{1}{5} \\  2 & 1 & \frac{1}{2} \\  5 & 2 & 1 \end{matrix}\right) \left( \begin{matrix} {.129} \\  {.277} \\  {.594} \end{matrix}\right)  = \left( \begin{matrix} {0.3863} \\  {0.8320} \\  {1.7930} \end{matrix}\right)
$$

$$
{n}_{\max } = {.3863} + {.8320} + {1.7930} = {3.0113}
$$

Now, for $n = 3$ ,

$$
{CI} = \frac{{n}_{\max } - n}{n - 1} = \frac{{3.0113} - 3}{3 - 1} = {.00565}
$$

$$
{RI} = \frac{{1.98}\left( {n - 2}\right) }{n} = \frac{{1.98} \times  1}{3} = {.66}
$$

$$
{CR} = \frac{CI}{RI} = \frac{.00565}{.66} = {.00856}
$$

Because ${CR} < {.1}$ , the level of inconsistency in ${\mathbf{A}}_{L}$ is acceptable.

## Excel Moment

Template excelAHP.xls is driven by user input and can handle comparison matrices of size $8 \times  8$ or less. Figure 15.3 demonstrates the application of the model to Example 15.1-2 (columns F:I and rows 10:13 are hidden to conserve space). The comparison matrices of the problem are entered one at a time in the (top) input data section of the spreadsheet. The order in which the comparison matrices are entered is unimportant, though it makes more sense to consider them in their natural hierarchal order.

The output (bottom) section of the spreadsheet provides the associated normalized matrix and its consistency ratio, $C{R}^{1}$ The weights, $w$ , are copied from column J and pasted into the solution summary area (the right section of the spreadsheet). Remember to use Paste Special $\Rightarrow$ Values when performing this step to guarantee a permanent record. The process is repeated until all the weights for all the comparison matrices have been stored in the solution summary area starting at column K.

In Figure 15.3, the final ranking is given in cells (K18:K20). The formula in cell K18 is

$$
\text{ =\$L\$4*\$L7+\$L\$5*\$N7 }
$$

FIGURE 15.3

Excel solution of Example 15.1-2 (file excelAHP.xls)

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>J</td><td>K</td><td>L</td><td>M</td><td>N</td></tr><tr><td>1</td><td colspan="10">AHP-Analytic Hierarchy Process</td></tr><tr><td>2</td><td colspan="5">Input: Comparison matrix</td><td rowspan="11"></td><td colspan="4">Solution summary</td></tr><tr><td>3</td><td>Matrix name:</td><td>AL</td><td rowspan="2" colspan="3"><<Maximum size = 8</td><td></td><td>A</td><td></td><td></td></tr><tr><td>4</td><td>Matrix size=</td><td>3</td><td>R</td><td>0.83333</td><td></td><td></td></tr><tr><td>5</td><td>Matrix data:</td><td>UA</td><td>UB</td><td>UC</td><td></td><td>L</td><td>0.16667</td><td></td><td></td></tr><tr><td>6</td><td>UA</td><td>1</td><td>0.5</td><td>0.2</td><td></td><td></td><td>AR</td><td></td><td>AL</td></tr><tr><td>7</td><td>UB</td><td>2</td><td>1</td><td>0.5</td><td></td><td>UA</td><td>0.54545</td><td>UA</td><td>0.1285</td></tr><tr><td>8</td><td>UC</td><td>5</td><td>2</td><td>1</td><td></td><td>UB</td><td>0.27273</td><td>UB</td><td>0.27661</td></tr><tr><td>9</td><td></td><td></td><td></td><td></td><td></td><td>UC</td><td>0.18182</td><td>UC</td><td>0.59489</td></tr><tr><td>14</td><td>Col sum</td><td>8</td><td>3.5</td><td>1.7</td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>15</td><td colspan="5">Output: Normalized martix</td><td></td><td></td><td></td><td></td></tr><tr><td>16</td><td rowspan="2"></td><td>nMax=</td><td>3.00746</td><td>CR=</td><td>0.0056</td><td></td><td></td><td></td><td></td></tr><tr><td>17</td><td>UA</td><td>UB</td><td>UC</td><td></td><td>Weight</td><td colspan="4">Final ranking</td></tr><tr><td>18</td><td>UA</td><td>0.12500</td><td>0.14286</td><td>0.11765</td><td></td><td>0.12850</td><td colspan="4">UA= 0.47596</td></tr><tr><td>19</td><td>UB</td><td>0.25000</td><td>0.28571</td><td>0.29412</td><td></td><td>0.27661</td><td colspan="4">UB= 0.27337</td></tr><tr><td>20</td><td>UC</td><td>0.62500</td><td>0.57143</td><td>0.58824</td><td></td><td>0.59489</td><td colspan="4">UC= 0.25066</td></tr><tr><td>27</td><td colspan="10">Caution: Formulas in Col. J are unprotected to allow copying to Solution Summary. Keep formulas intact.</td></tr></table>

---

${}^{1}$ The more accurate results of the spreadsheet differ from those in Examples 15.1-2 and 15.1-3 because of manual roundoff approximation.

---

This formula provides the composite weight for alternative UA and is copied in cells K19 and K20 to evaluate alternatives UB and UC. Note from the formula in K18 that cell reference to the alternative UA must be column-fixed (namely, \$L7 and \$N7), whereas all other references must be row-and-column-fixed (namely, \$L\$4 and \$L\$5). The validity of the copied formulas requires stacking the (column-fixed) alternative weights of each matrix in a single column (no intervening empty cells). In Figure 15.3, the ${\mathrm{A}}_{R}$ -weights are in column $\mathrm{L}$ and the ${\mathrm{A}}_{L}$ -weights are in column $\mathrm{N}$ . There are no restrictions on the placement of the A-weights because they are row- and column-fixed in the formula.

You can embellish the formula in K18 to capture the names of the alternatives by using

$$
\text{ =\$K7\&"="\&TEXT(\$L\$4*\$L7+\$L\$5*\$N7,"\#\#\#\# 0.00000") }
$$

The procedure for evaluating alternatives can be extended to any number of hierarchy levels. Once you develop the formula correctly for the first alternative, the same formula is copied to the remaining cells. Remember that all cell references in the formula must be row-and-column-fixed, except for references to the alternatives, which must be column-fixed only. Problem 15-2, asks you to develop the formula for a 3-level problem.

### 15.2 DECISION MAKING UNDER RISK

Under conditions of risk, the payoffs associated with each decision alternative are represented by probability distributions, and decision can be based on the expected value criterion-maximization of expected profit or the minimization of expected cost. The expected value criterion is sometimes modified to account for other situations, as will be described later in this section.

## Real-Life Application—Booking Limits in Hotel Reservations

Hotel La Posada has a total of 300 guest rooms. Its clientele includes both business and leisure travelers. Room prices are discounted, mainly to leisure travelers. Business travelers, who usually are late in booking their rooms, pay full price. La Posada sets a booking limit on the number of discount rooms to take advantage of the full price paid by business customers. The case study at the end of this chapter utilizes decision tree analysis to determine the booking limits.

#### 15.2.1 Decision Tree-Based Expected Value Criterion

The expected value criterion seeks the maximization of expected (average) profit or the minimization of expected cost. The data of the problem assumes that the payoff (or cost) associated with each decision alternative is probabilistic.

Decision tree analysis. The following example considers simple decision situations with a finite number of decision alternatives and explicit payoff matrices.

## Example 15.2-1

Suppose that you want to invest \$10,000 in the stock market by buying shares in one of two companies: $A$ and $B$ . Shares in Company $A$ , though risky, could yield a 50% return during the next year. If the stock market conditions are not favorable (i.e., a "bear" market), the stock may lose 20% of its value. Company $B$ provides safe investments with a 15% return in a "bull" market and only 5% in a "bear" market. All the publications you have consulted (and there is always a flood of them at the end of the year!) are predicting a 60% chance for a "bull" market and 40% chance for a "bear" market. How should you invest your money?

![bo_d56m58jef24c73bhe65g_8_454_198_657_439_0.jpg](bo_d56m58jef24c73bhe65g_8_454_198_657_439_0.jpg)

FIGURE 15.4

Decision-tree representation of the stock market problem

The decision problem is summarized in the following table:

<table><tr><td rowspan="2">Decision alternative</td><td colspan="2">1-year return on \$10,000 investment</td></tr><tr><td>"Bull" market (\$)</td><td>"Bear" market (\$)</td></tr><tr><td>Company $A$ stock</td><td>5000</td><td>-2000</td></tr><tr><td>Company $B$ stock</td><td>1500</td><td>500</td></tr><tr><td>Probability of occurrence</td><td>.6</td><td>.4</td></tr></table>

The problem can also be represented as a decision tree as shown in Figure 15.4. Two types of nodes are used in the tree: A square ( $\square$ ) represents a decision point, and a circle ( $\text{ ○ }$ ) represents a chance event. Thus, the two branches from decision point 1 represent the two alternatives of investing in stock $A$ or stock $B$ . Next, the two branches emanating from chance events 2 and 3 represent the "bull" and the "bear" markets with their respective probabilities and payoffs.

From Figure 15.4, the expected 1-year returns are

$$
\text{ Stock }A = \$ {5000} \times  {.6} + \left( {-{2000}}\right)  \times  {.4} = \$ {2200}
$$

$$
\text{ Stock }B = \$ {1500} \times  {.6} + \$ {500} \times  {.4} = \$ {1100}
$$

Stock $A$ is chosen because it yields a higher expected return.

Remarks. In the terminology of decision theory, the probabilistic "bull" and the "bear" markets are called states of nature. In general, a decision problem may include $n$ states of nature and $m$ alternatives. If ${p}_{j}\left( { > 0}\right)$ is the probability of occurrence for state $j$ and ${a}_{ij}$ is the payoff of alternative $i$ , given state $j\left( {i = 1,2,\ldots , m;j = 1,2,\ldots , n}\right)$ , then the expected payoff for alternative $i$ is computed as

$$
E{V}_{i} = {a}_{i1}{p}_{1} + {a}_{i2}{p}_{2} + \ldots  + {a}_{in}{p}_{n}, i = 1,2,\ldots , n
$$

$$
{p}_{1} + {p}_{2} + \ldots  + {p}_{n} = 1
$$

The best alternative corresponds to $\mathop{\max }\limits_{i}\left\{  {E{V}_{i}}\right\}$ and $\mathop{\min }\limits_{i}\left\{  {E{V}_{i}}\right\}$ for the cases of profit and loss, respectively.

#### 15.2.2 Variants of the Expected Value Criterion

This section addresses two issues relating to the expected value criterion: the determination of posterior probabilities based on experimentation and the use of utility versus actual value of money.

Posterior (Bayes') probabilities. The probabilities used in the expected value criterion are usually estimated from historical data (see Section 14.5). In some cases, the accuracy of these estimates can be enhanced by using additional experimentation. The resulting probabilities are referred to as posterior (or Bayes') probabilities, as opposed to the prior probabilities determined from raw data.

## Real-Life Application-Casey's Problem: Interpreting and Evaluating a New Test

A screening test of a newborn, named Casey, reveals a C14:1 enzyme deficiency. The enzyme is required to digest a particular form of long-chain fats, and its absence could lead to severe illness or mysterious death (broadly categorized under the sudden infant death syndrome or SIDS). The test had been administered previously to approximately 13,000 newborns, and Casey was the first to test positive. Though the screening test does not in itself constitute a definitive diagnosis, the extreme rarity of the condition led her doctors to conclude that there was an 80 to ${90}\%$ chance that she was suffering from this deficiency. Given that Casey tested positive, Bayes' posterior probability is used to assess whether or not the child has the C14:1 deficiency. The situation is detailed in Case 11 in Chapter 26, on the website.

## Example 15.2-2

This example demonstrates how the expected-value criterion is modified to take advantage of posterior probabilities. In Example 15.2-1, the (prior) probabilities of .6 and .4 of a "bull" and a "bear" market are determined from available financial publications. Suppose that rather than relying solely on these publications, you have decided to conduct a more "personal" investigation by consulting a friend who has done well in the stock market. The friend quantifies a "for/ against" investment recommendation in the following manner: In a "bull" market, there is a 90% chance the recommendation is "for." It drops to 50% in a "bear" market. How does the additional information affect the decision?

The friend's statement provides conditional probabilities of the recommendations "for" and "against" given that the states of nature are "bull" and "bear" markets. Define

$$
{v}_{1} = \text{ "For" vote }
$$

$$
{v}_{2} = \text{ "Against" vote }
$$

$$
{m}_{1} = \text{ "Bull" market }
$$

$$
{m}_{2} = \text{ "Bear" market }
$$

Thus, the friend's statement may be written in the form of probability statements as

$$
P\left\{  {{v}_{1} \mid  {m}_{1}}\right\}   = {.9}, P\left\{  {{v}_{2} \mid  {m}_{1}}\right\}   = {.1}
$$

$$
P\left\{  {{v}_{1} \mid  {m}_{2}}\right\}   = {.5}, P\left\{  {{v}_{2} \mid  {m}_{2}}\right\}   = {.5}
$$

With this representation, the decision problem is summarized as:

1. If the friend’s recommendation is "for," would you invest in stock $A$ or in stock $B$ ?

2. If the friend’s recommendation is "against," would you invest in stock $A$ or in stock $B$ ?

The decision tree in Figure 15.5 represents the problem. Node 1 is a chance event representing the "for" and "against" possibilities. Nodes 2 and 3 are decision points for choosing between stocks $A$ and $B$ , given the "for" and "against" recommendations, respectively. Finally, nodes 4 to 7 are chance events representing the "bull" and "bear" markets.

To evaluate the different alternatives in Figure 15.5, it is necessary to compute the posterior probabilities $P\left\{  {{m}_{i} \mid  {v}_{j}}\right\}$ shown on the ${m}_{1}$ - and ${m}_{2}$ -branches of nodes 4,5,6, and 7 . These posterior probabilities take into account the additional information provided by the friend's "for/ against" recommendation and are computed according to the following general steps:

Step 1. Summarize the conditional probabilities $P\left\{  {{v}_{j} \mid  {m}_{i}}\right\}$ in the following tabular form:

![bo_d56m58jef24c73bhe65g_10_854_836_245_197_0.jpg](bo_d56m58jef24c73bhe65g_10_854_836_245_197_0.jpg)

FIGURE 15.5

Decision tree for the stock market problem with posterior probabilities

![bo_d56m58jef24c73bhe65g_10_532_1208_899_960_0.jpg](bo_d56m58jef24c73bhe65g_10_532_1208_899_960_0.jpg)

Step 2. Compute the joint probabilities as

$$
P\left\{  {{m}_{i},{v}_{j}}\right\}   = P\left\{  {{v}_{j} \mid  {m}_{i}}\right\}  P\left\{  {m}_{i}\right\}  \text{ , for all }i\text{ and }j
$$

Given the prior probabilities $P\left\{  {m}_{1}\right\}   = {.6}$ and $P\left\{  {m}_{2}\right\}   = {.4}$ , the joint probabilities are determined by multiplying the first and the second rows of the table in step 1 by .6 and .4, respectively - that is,

<table><tr><td rowspan="3">${m}_{1}$ <br> ${m}_{2}$</td><td>${v}_{1}$</td><td>${v}_{2}$</td></tr><tr><td>.54</td><td>.06</td></tr><tr><td>.20</td><td>.20</td></tr></table>

The sum of all the entries in the table equals 1.

Step 3. Compute the absolute probabilities as

$$
P\left\{  {v}_{j}\right\}   = \mathop{\sum }\limits_{{\text{ all }i}}P\left\{  {{m}_{i},{v}_{j}}\right\}  \text{ , for all }j
$$

These probabilities are the column sums in the table in step 2 - that is,

<table><tr><td>$P\left\{  {v}_{1}\right\}$</td><td>$P\left\{  {v}_{2}\right\}$</td></tr><tr><td>.74</td><td>.26</td></tr></table>

Step 4. Determine the desired posterior probabilities as

$$
P\left\{  {{m}_{i} \mid  {v}_{j}}\right\}   = \frac{P\left\{  {{m}_{i},{v}_{j}}\right\}  }{P\left\{  {v}_{j}\right\}  }
$$

These probabilities are computed by dividing each column in the table of step 2 by the corresponding column sum in the table of step 3, which yields

<table><tr><td></td><td>${v}_{1}$</td><td>${v}_{2}$</td></tr><tr><td>${\mathrm{m}}_{1}$</td><td>.730</td><td>.231</td></tr><tr><td>${m}_{2}$</td><td>.270</td><td>.769</td></tr></table>

These are the probabilities used in Figure 15.5 and are different from the prior probabilities $P\left\{  {m}_{1}\right\}   = {.6}$ and $P\left\{  {m}_{2}\right\}   = {.4}$ .

We are now ready to evaluate the alternatives based on the expected payoffs for nodes 4, 5, 6, and 7 - that is,

## "For" Recommendation

Stock $A$ at node $4 = {5000} \times  {.730} + \left( {-{2000}}\right)  \times  {.270} \times   = \$ {3110}$

Stock $B$ at node $5 = {1500} \times  {.730} + {500} \times  {.270} = {1230}$

Decision. Invest in stock $A$ .

"Against" Recommendation

Stock $A$ at node $6 = {5000} \times  {.231} + \left( {-{2000}}\right)  \times  {.769} =  - \$ {383}$ Stock $B$ at node $7 = {1500} \times  {.231} + {500} \times  {.769} = \$ \mathbf{{731}}$ Decision. Invest in stock B.

The given decisions are equivalent to saying that the expected payoffs at decision nodes 2 and 3 are \$3110 and \$731, respectively (see Figure 15.5). Thus, given the probabilities $P\left\{  {v}_{1}\right\}   = {.74}$ and $P\left\{  {v}_{2}\right\}   = {.26}$ as computed in step 3, we can compute the expected payoff for the entire decision tree. (See Problem 15-30.)

## Excel Moment

Excel file excelBayes.xls is designed to determine the posterior probabilities for prior probability matrices of sizes up to ${10} \times  {10}$ (some rows and columns have been hidden to conserve space). The input data include $P\{ m\}$ and $P\{ v \mid  m\}$ . The spreadsheet checks input data errors and displays appropriate error messages.

## Aha! Moment: An Eighteenth-Century Lottery that Yields Infinite Expected Payoff, or Does It?

In the early eighteenth century, Swiss mathematician Nicolas Bernoulli introduced a paradoxical theoretical lottery game with an expected payoff of infinity. The paradox arises because the game sets no limit on the amount of money a player can win. The game was published by Nicolas' brother, Daniel, in 1738 in the St. Petersburg Academy Proceedings and became known as the Petersburg Paradox. The rules of the game are simple: Toss a fair coin. If the outcome is heads (H), the game continues; otherwise, the game ends at the first occurrence of tails (T). Starting with \$2 for the first $\mathrm{H}$ , the payoff doubles with the occurrence of each successive $\mathrm{H}$ , yielding the monetary stream $\$ 2,\$ 4,\$ 8,\$ {16},\ldots$ The probability that an $\mathrm{H}$ will recur in toss $n$ is ${\left( \frac{1}{2}\right) }^{n - 1}\left( \frac{1}{2}\right)  = \left( \frac{1}{{2}^{n}}\right)$ . Thus, assuming the game is played indefinitely,

$$
\text{ Expected payoff } = \mathop{\sum }\limits_{{n = 1}}^{\infty }{2}^{n}\left( \frac{1}{{2}^{n}}\right)  = 1 + 1 + 1 + \ldots  = \infty
$$

If the infinite expected payoff is the "fair" value of the game, then, theoretically, a player should accept any price for playing the game, a paradoxical outcome particularly when a rational decision maker realizes that a low payoff is probable (e.g., there is a 50-50 chance of winning \$2) and a high payoff is unlikely [e.g., the probability of winning the (by-comparison) modest amount of $\$ {1024}\left( { = {2}^{10}}\right)$ is less than .001].

The paradox was resolved by Daniel Bernoulli ${}^{2}$ by introducing the concepts of utility functions and risk aversion to replace monetary amounts in the expected value computations, as the remainder of this section explains.

---

${}^{2}$ http://www.econ.ucsb.edu/~tedb/Courses/GraduateTheoryUCSB/Bernoulli.pdf, accessed 06-14-2015. Bernoulli acknowledged that ten years earlier his Swiss colleague Gabriel Cramer independently came very close to resolving the paradox.

---

Utility functions. In the preceding presentation, the expected value criterion is applied to situations where the payoff is real money. There are cases where the utility rather than the real value should be used in the analysis. To illustrate this point, suppose there is a 50-50 chance that a \$20,000 investment will produce a profit of \$40,000 or be lost. The associated expected profit is ${40},{000} \times  {.5} - {20},{000} \times  {.5} = \$ {10},{000}$ . Although there is a net expected profit, different individuals vary in interpreting the result. An investor who is willing to accept risk may undertake the investment for a 50% chance to make a \$40,000 profit. Conversely, a conservative investor may not be willing to risk losing \$20,000. The concept of utility function is devised to reflect these differences. The utility function then takes the place of real money in the decision-making model.

How is the subjective attitude toward risk quantified in the form of a utility function? In the preceding investment illustration, the best payoff is \$40,000, and the worst is - \$20,000. We can establish a utility scale, $U$ , from 0 to 100 that specifies $U\left( {-\$ {20},{000}}\right)  = 0$ and $U\left( {\$ {40},{000}}\right)  = {100}$ . The value of $U$ for investment return between $- \$ {20},{000}$ and $\$ {40},{000}$ can be determined in the following manner: If the decision maker is neutral (indifferent) toward risk, then $U$ can be represented by a straight line joining $\left( {0, - \$ {20},{000}}\right)$ and $\left( {{100},\$ {40},{000}}\right)$ . In this case, both real money and its utility lead to the same decisions. More generally, the function $U$ can take other forms reflecting different attitudes toward risk. Figure 15.6 illustrates the cases of individuals $X, Y$ , and $Z$ . Individual $Y$ is risk neutral, individual $X$ is risk averse (or cautious), and individual $Z$ , the opposite of $X$ , is a risk seeker. The figure demonstrates that for the risk-averse $X$ , the drop in utility ${bc}$ corresponding to a loss of \$10,000 is larger than the increase ${ab}$ associated with a gain of \$10,000 . The opposite is true for risk seeker $Z$ where ${de} > {ef}$ . In general, an individual can be both risk averse and risk seeking, in which case the associated utility curve will follow an elongated $S$ -shape.

FIGURE 15.6

Utility functions for risk averse $\left( X\right)$ , neutral $\left( Y\right)$ , and risk seeker $\left( Z\right)$ decision makers

![bo_d56m58jef24c73bhe65g_13_511_1368_847_806_0.jpg](bo_d56m58jef24c73bhe65g_13_511_1368_847_806_0.jpg)

Utility curves similar to the ones demonstrated in Figure 15.6 are determined by "quantifying" the decision maker's attitude toward risk for different levels of cash money. In our example, the desired range is $\left( {-\$ {20},{000}\text{ to }\$ {40},{000}}\right)$ with $U\left( {-\$ {20},{000}}\right)  = 0$ and $U\left( {\$ {40},{000}}\right)  = {100}$ . To specify the values of $U$ for intermediate cash values (e.g., - $\$ {10},{000},\$ 0,\$ {10},{000},\$ {20},{000}$ , and $\$ {30},{000}$ ), we establish a lottery for a cash amount $x$ whose expected utility is

$$
U\left( x\right)  = {pU}\left( {-{20},{000}}\right)  + \left( {1 - p}\right) U\left( {\$ {40},{000}}\right) ,0 \leq  p \leq  1
$$

$$
= {0p} + {100}\left( {1 - p}\right)
$$

$$
= {100} - {100p}
$$

To determine $U\left( x\right)$ , the decision maker must state a preference between a guaranteed cash amount $x$ and the chance to play a lottery for which there is a loss of - \$20,000 with probability $p$ and a profit of \$40,000 with probability $1 - p$ . The value of $p$ reflects the decision maker’s neutrality (or indifference) toward risk. For example, for $x = \$ {20},{000}$ , the decision maker may feel that a guaranteed $\$ {20},{000}$ cash and the lottery with $p = {.8}$ are equally attractive. In this case, we can compute the utility of $x = \$ {20},{000}$ as

$$
U\left( {\$ {20},{000}}\right)  = {100} - {100} \times  {.8} = {20}
$$

Note that higher values of $p$ for the same lottery reflect risk seeking (as opposed to risk aversion). For example, for $p = {.1}$ ,

$$
U\left( {\$ {20},{000}}\right)  = {100} - {100} \times  {.2} = {80}
$$

### 15.3 DECISION UNDER UNCERTAINTY

Decision making under uncertainty, as under risk, involves alternative actions whose payoffs depend on the (random) states of nature. Specifically, the payoff matrix of a decision problem with $m$ alternative actions and $n$ states of nature can be represented as

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>...</td><td>${s}_{n}$</td></tr><tr><td>${a}_{1}$</td><td>$v\left( {{a}_{1},{s}_{1}}\right)$</td><td>$v\left( {{a}_{1},{s}_{2}}\right)$</td><td>...</td><td>$v\left( {{a}_{1},{s}_{n}}\right)$</td></tr><tr><td>${a}_{2}$</td><td>$v\left( {{a}_{2},{s}_{1}}\right)$</td><td>$v\left( {{a}_{2},{s}_{2}}\right)$</td><td>...</td><td>$v\left( {{a}_{2},{s}_{n}}\right)$</td></tr><tr><td>:</td><td>:</td><td>:</td><td>$\vdots$</td><td>:</td></tr><tr><td>${a}_{m}$</td><td>$v\left( {{a}_{m},{s}_{1}}\right)$</td><td>$v\left( {{a}_{m},{s}_{2}}\right)$</td><td>...</td><td>$v\left( {{a}_{m},{s}_{n}}\right)$</td></tr></table>

The element ${a}_{i}$ represents action $i$ and the element ${s}_{j}$ represents state of nature $j$ . The payoff or outcome associated with action ${a}_{i}$ and state ${s}_{j}$ is $v\left( {{a}_{i},{s}_{j}}\right)$ .

In decision making under uncertainty, the probability distribution associated with the states ${s}_{j}, j = 1,2,\ldots , n$ , is either unknown or cannot be determined. This lack of information has led to the development of special decision criteria:

1. Laplace

2. Minimax

3. Savage

4. Hurwicz

These criteria differ in how conservative the decision maker is in the face of uncertainty.

The Laplace criterion is based on the principle of insufficient reason. Because the probability distributions are not known, there is no reason to believe that the probabilities associated with the states of nature are different. The alternatives are thus evaluated using the liberal assumption that all states are equally likely to occur-that is, $P\left\{  {s}_{1}\right\}   = P\left\{  {s}_{2}\right\}   = \ldots  = P\left\{  {s}_{n}\right\}   = \frac{1}{n}$ . Given that the payoff $v\left( {{a}_{i},{s}_{j}}\right)$ represents gain, the best alternative is the one that yields

$$
\mathop{\max }\limits_{{a}_{i}}\left\{  {\frac{1}{n}\mathop{\sum }\limits_{{j = 1}}^{n}v\left( {{a}_{i},{s}_{j}}\right) }\right\}
$$

The maximin (minimax) criterion is based on the conservative attitude of making the best of the worst-possible conditions. If $v\left( {{a}_{i},{s}_{j}}\right)$ is loss, then we select the action that corresponds to the following minimax criterion:

$$
\mathop{\min }\limits_{{a}_{i}}\left\{  {\mathop{\max }\limits_{{s}_{j}}v\left( {{a}_{i},{s}_{j}}\right) }\right\}
$$

If $v\left( {{a}_{i},{s}_{j}}\right)$ is gain, we use the maximin criterion given by

$$
\mathop{\max }\limits_{{a}_{i}}\left\{  {\mathop{\min }\limits_{{S}_{j}}v\left( {{a}_{i},{s}_{j}}\right) }\right\}
$$

The Savage regret criterion aims at "moderating" the degree of conservatism in the minimax (maximin) criterion by replacing the (gain or loss) payoff matrix $v\left( {{a}_{i},{s}_{j}}\right)$ with a loss (or regret) matrix, $r\left( {{a}_{i},{s}_{j}}\right)$ , by using the following transformation:

$$
r\left( {{a}_{i},{s}_{j}}\right)  = \left\{  \begin{array}{l} v\left( {{a}_{i},{s}_{j}}\right)  - \mathop{\min }\limits_{{a}_{k}}\left\{  {v\left( {{a}_{k},{s}_{j}}\right) }\right\}  ,\text{ if }v\text{ is loss } \\  \mathop{\max }\limits_{{a}_{k}}\left\{  {v\left( {{a}_{k},{s}_{j}}\right) }\right\}   - v\left( {{a}_{i},{s}_{j}}\right) ,\text{ if }v\text{ is gain } \end{array}\right.
$$

To show why the Savage criterion moderates the minimax (maximin) criterion, consider the following loss matrix:

<table><tr><td rowspan="3">${a}_{1}$ <br> ${a}_{2}$</td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>Row max</td><td></td></tr><tr><td>\$11,000</td><td>\$90</td><td>\$11,000</td><td></td></tr><tr><td>\$10,000</td><td>\$10,000</td><td>\$10,000</td><td>Minimax</td></tr></table>

The application of the minimax criterion shows that ${a}_{2}$ , with a definite loss of \$10,000, is the preferred alternative. However, it may be better to choose ${a}_{1}$ because there is a chance of limiting the loss to $\$ {90}$ only if ${s}_{2}$ occurs. This happens to be the case when the regret matrix is used:

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>Row max</td><td></td></tr><tr><td></td><td>\$1,000</td><td>\$0</td><td>\$1,000</td><td>Minimax</td></tr><tr><td></td><td>\$0</td><td>\$9,910</td><td>\$9,910</td><td></td></tr></table>

The last criterion, Hurwicz, is designed to represent different decision-making attitudes, ranging from the most liberal (optimistic) to the most conservative (pessimistic). Define $0 \leq  \alpha  \leq  1$ . The selected action must be associated with

$$
\mathop{\max }\limits_{{a}_{i}}\left\{  {\alpha \mathop{\max }\limits_{{s}_{j}}v\left( {{a}_{i},{s}_{j}}\right)  + \left( {1 - \alpha }\right) \mathop{\min }\limits_{{s}_{j}}v\left( {{a}_{i},{s}_{j}}\right) }\right\}  \text{ , if }v\text{ is gain }
$$

$$
\mathop{\min }\limits_{{a}_{i}}\left\{  {\alpha \mathop{\min }\limits_{{s}_{j}}v\left( {{a}_{i},{s}_{j}}\right)  + \left( {1 - \alpha }\right) \mathop{\max }\limits_{{s}_{j}}v\left( {{a}_{i},{s}_{j}}\right) }\right\}  \text{ , if }v\text{ is loss }
$$

The parameter $\alpha$ is the index of optimism. If $\alpha  = 0$ , then the criterion reduces to conservative minimax criterion, seeking the best of the worst conditions. If $\alpha  = 1$ , then the criterion is liberal because it seeks the best of the best conditions. The degree of optimism (or pessimism) can be adjusted by selecting a value of $\alpha$ between 0 and 1 . In the absence of strong feeling regarding extreme optimism and extreme pessimism, $\alpha  = {.5}$ may be a fair choice.

## Example 15.3-1

National Outdoors School (NOS) is preparing a summer campsite in the heart of Alaska to train individuals in wilderness survival. NOS estimates that attendance can fall into one of four categories: 200, 250, 300, and 350 persons. The cost of the campsite will be the smallest when its size meets the demand exactly. Deviations above or below the ideal demand levels incur additional costs resulting from constructing more capacity than needed or losing income opportunities when the demand is not met. Letting ${a}_{1}$ to ${a}_{4}$ represent the sizes of the campsites $({200},{250}$ , 300, and 350 persons) and ${s}_{1}$ to ${s}_{4}$ the level of attendance, the following table summarizes the cost matrix (in thousands of dollars) for the situation:

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>${s}_{3}$</td><td>${s}_{4}$</td></tr><tr><td>${a}_{1}$</td><td>5</td><td>10</td><td>18</td><td>25</td></tr><tr><td>${a}_{2}$</td><td>8</td><td>7</td><td>12</td><td>23</td></tr><tr><td>${a}_{3}$</td><td>21</td><td>18</td><td>12</td><td>21</td></tr><tr><td>${a}_{4}$</td><td>30</td><td>22</td><td>19</td><td>15</td></tr></table>

The problem is analyzed using all four criteria.

Laplace. Given $P\left\{  {s}_{j}\right\}   = \frac{1}{4}, j = 1$ to 4, the expected values for the different actions are computed as

$$
E\left\{  {a}_{1}\right\}   = \frac{1}{4}\left( {5 + {10} + {18} + {25}}\right)  = \$ {14},{500}
$$

$$
E\left\{  {a}_{2}\right\}   = \frac{1}{4}\left( {8 + 7 + {12} + {23}}\right)  = \$ \mathbf{{12},{500}} \leftarrow  \text{ Optimum }
$$

$$
E\left\{  {a}_{3}\right\}   = \frac{1}{4}\left( {{21} + {18} + {12} + {21}}\right)  = \$ {18},{000}
$$

$$
E\left\{  {a}_{4}\right\}   = \frac{1}{4}\left( {{30} + {22} + {19} + {15}}\right)  = \$ {21},{500}
$$

Minimax. The minimax criterion produces the following matrix:

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>${s}_{3}$</td><td>${s}_{4}$</td><td>Row max</td></tr><tr><td>${a}_{1}$</td><td>5</td><td>10</td><td>18</td><td>25</td><td>25</td></tr><tr><td>${a}_{2}$</td><td>8</td><td>7</td><td>12</td><td>23</td><td>23</td></tr><tr><td>${a}_{3}$</td><td>21</td><td>18</td><td>12</td><td>21</td><td>21 ← Minimax</td></tr><tr><td>${a}_{4}$</td><td>30</td><td>22</td><td>19</td><td>15</td><td>30</td></tr></table>

Savage. The regret matrix is determined by subtracting 5, 7, 12, and 15 from columns 1 to 4, respectively. Thus,

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>${s}_{3}$</td><td>S4</td><td>Row max</td></tr><tr><td>${a}_{1}$</td><td>0</td><td>3</td><td>6</td><td>10</td><td>10</td></tr><tr><td>${a}_{2}$</td><td>3</td><td>0</td><td>0</td><td>8</td><td>8 ← Minimax</td></tr><tr><td>${a}_{3}$</td><td>16</td><td>11</td><td>0</td><td>6</td><td>16</td></tr><tr><td>${a}_{4}$</td><td>25</td><td>15</td><td>7</td><td>0</td><td>25</td></tr></table>

Hurwicz. The following table summarizes the computations:

<table><tr><td>Alternative</td><td>Row min</td><td>Row max</td><td>$\alpha \left( \text{ Row min }\right)  + \left( {1 - \alpha }\right) \left( \text{ Row max }\right)$</td></tr><tr><td>${a}_{1}$</td><td>5</td><td>25</td><td>${25} - {20\alpha }$</td></tr><tr><td>${a}_{2}$</td><td>7</td><td>23</td><td>23-16α</td></tr><tr><td>${a}_{3}$</td><td>12</td><td>21</td><td>${21} - {9\alpha }$</td></tr><tr><td>${a}_{4}$</td><td>15</td><td>30</td><td>${30} - {15\alpha }$</td></tr></table>

Using an appropriate $\alpha$ , we can determine the optimum alternative. For example, at $\alpha  = {.5}$ , either ${a}_{1}$ or ${a}_{2}$ is the optimum, and at $\alpha  = {.25},{a}_{3}$ is the optimum.

## Excel Moment

Template excelUncertainty.xls can be used to automate the computations of Laplace, maximin, Savage, and Hurwicz criteria. The spreadsheet is based on the use of a cost matrix. To use a reward matrix, all entries must be multiplied by -1 . The maximum matrix size is $\left( {{10} \times  {10}}\right)$ .

### 15.4 GAME THEORY

Game theory deals with decision situations in which two intelligent opponents with conflicting objectives are vying to outdo one another. Typical examples include launching advertising campaigns for competing products and planning strategies for war battles.

In a conflict, each of two players (opponents) has a (finite or infinite) number of alternatives or strategies. Associated with each pair of strategies is the payoff one player receives from the other. Such a situation is known as a two-person zero-sum game, because a gain by one player is an equal loss by the other. This means that we can represent the game in terms of the payoff to one player. Designating the two players as $A$ and $B$ with $m$ and $n$ strategies, respectively, the game is usually presented in terms of the payoff matrix to player $A$ as

![bo_d56m58jef24c73bhe65g_18_795_762_388_296_0.jpg](bo_d56m58jef24c73bhe65g_18_795_762_388_296_0.jpg)

The representation indicates that if $A$ uses strategy $i$ and $B$ uses strategy $j$ , the payoff to $A$ is ${a}_{ij}$ , and the payoff to $B$ is $- {a}_{ij}$ .

## Real-Life Application—Ordering Golfers on the Final Day of Ryder Cup Matches

On the final day of a golf tournament, two teams compete for the championship. Each team captain must submit a slate (an ordered list of golfers) that determines the matches. For two competing players occupying the same order in their respective slates, it is plausible to assume that there is 50-50 chance that either golfer will win the match. The win-probability increases for a higher-order golfer when matched with a lower-order player. The goal is to develop an analytical procedure that will support or refute the idea of using slates. Case 12, Chapter 26 on the website details the study based on game theory.

#### 15.4.1 Optimal Solution of Two-Person Zero-Sum Games

Because games involve a conflict of interest, the basis for the selection of optimal strategies guarantees that neither player is tempted to seek a different strategy because a worse payoff will ensue. These solutions can be in the form of a single pure strategy or several strategies mixed randomly.

## Example 15.4-1

Two companies, $A$ and $B$ , sell two brands of flu medicine. Company $A$ advertises in radio $\left( {A}_{1}\right)$ , television $\left( {A}_{2}\right)$ , and newspapers $\left( {A}_{3}\right)$ . Company $B$ , in addition to using radio $\left( {B}_{1}\right)$ , television $\left( {B}_{2}\right)$ , and newspapers $\left( {B}_{3}\right)$ , also mails brochures $\left( {B}_{4}\right)$ . Depending on the effectiveness of each advertising campaign, one company can capture a portion of the market from the other. The following matrix summarizes the percentage of the market captured or lost by company $A$ :

![bo_d56m58jef24c73bhe65g_19_565_300_741_353_0.jpg](bo_d56m58jef24c73bhe65g_19_565_300_741_353_0.jpg)

The solution of the game is based on the principle of securing the best of the worst for each player. If Company $A$ selects strategy ${A}_{1}$ , then regardless of what $B$ does, the worst that can happen is that $A$ loses $3\%$ of the market share to $B$ . This is represented by the minimum value of the entries in row 1. Similarly, with strategy ${A}_{2}$ , the worst outcome is for $A$ to capture 5% from $B$ , and for strategy ${A}_{3}$ , the worst outcome is for $A$ to lose 9% to $B$ . These results are listed under row min. To achieve the best of the worst, Company $A$ chooses strategy ${A}_{2}$ because it corresponds to the maximin value.

Next, for Company $B$ , the given payoff matrix is for $A$ and $B$ ’s best of the worst solution is based on the minimax value. The result is that Company B will select strategy ${B}_{2}$ .

The optimal solution of the game calls for selecting strategies ${A}_{2}$ and ${B}_{2}$ , which means that both companies should use television advertising. The payoff will be in favor of company $A$ , because its market share will increase by 5%. In this case, we say that the value of the game is 5% and that $A$ and $B$ are using a pure saddle-point solution.

The saddle-point solution precludes the selection of a better strategy by either company. If $B$ moves to another strategy $\left( {{B}_{1},{B}_{3}\text{ , or }{B}_{4}}\right)$ , Company $A$ can stay with strategy ${A}_{2}$ , ensuring worse loss for $B$ (6% or 8%). By the same token, $A$ would not seek a different strategy because $B$ can change to ${B}_{3}$ to realize a 9% market gain if ${A}_{1}$ is used and 3% if ${A}_{3}$ is used.

The optimal saddle-point solution of a game need not be a pure strategy. Instead, the solution may require mixing two or more strategies randomly, as the following example illustrates.

## Example 15.4-2

Two players, $A$ and $B$ , play the coin-tossing game. Each player, unbeknownst to the other, chooses a head $\left( H\right)$ or a tail $\left( T\right)$ . Both players would reveal their choices simultaneously. If they match (HH or TT), player $A$ receives $\$ 1$ from $B$ . Otherwise, $A$ pays $B\$ 1$ .

The following payoff matrix for player $A$ gives the row-min and the column-max values corresponding to $A$ ’s and $B$ ’s strategies, respectively:

![bo_d56m58jef24c73bhe65g_19_645_1846_545_227_0.jpg](bo_d56m58jef24c73bhe65g_19_645_1846_545_227_0.jpg)

The maximin and the minimax values of the games are - \$1 and \$1, respectively, and the game does not have a pure strategy solution because the two values are not equal. Specifically,

if player $A$ selects ${A}_{H}$ , player $B$ can select ${B}_{T}$ to receive $\$ 1$ from $A$ . If this happens, $A$ can move to strategy ${A}_{T}$ to reverse the outcome by receiving $\$ 1$ from $B$ . The constant temptation to switch to another strategy shows that a pure strategy solution is not acceptable. What is needed in this case is for both players to randomly mix their respective pure strategies. The optimal value of the game will then occur somewhere between the maximin and the minimax values of the game-that is,

maximin (lower) value $\leq$ value of the game $\leq$ minimax (upper) value

In the coin-tossing example, the value of the game must lie between - \$1 and + \$1 (see Problem 15-45).

#### 15.4.2 Solution of Mixed Strategy Games

Games with mixed strategies can be solved either graphically or by linear programming. The graphical solution is suitable for games with exactly two pure strategies for one or both players. Linear programming, on the hand, can solve any two-person zero-sum game. The graphical method is interesting because it explains the idea of a saddle point pictorially.

Graphical solution of games. We start with the case of $\left( {2 \times  n}\right)$ games in which player $A$ has two strategies, ${A}_{1}$ and ${A}_{2}$ .

![bo_d56m58jef24c73bhe65g_20_700_1079_573_209_0.jpg](bo_d56m58jef24c73bhe65g_20_700_1079_573_209_0.jpg)

Player $A$ mixes strategies ${A}_{1}$ and ${A}_{2}$ with probabilities ${x}_{1}$ and $1 - {x}_{1},0 \leq  {x}_{1} \leq  1$ . Player $B$ mixes strategies ${B}_{1},{B}_{2},\ldots$ , and ${B}_{n}$ with probabilities ${y}_{1},{y}_{2},\ldots$ , and ${y}_{n},{y}_{j} \geq  0$ for $j = 1,2,\ldots , n$ , and ${y}_{1} + {y}_{2} + \ldots  + {y}_{n} = 1$ . In this case, $A$ ’s expected payoff corresponding to $B$ ’s $j$ th pure strategy is

$$
\left( {{a}_{1j} - {a}_{2j}}\right) {x}_{1} + {a}_{2j}, j = 1,2,\ldots , n
$$

Player $A$ seeks the value of ${x}_{1}$ that maximizes the minimum expected payoffs-that is,

$$
\mathop{\max }\limits_{{x}_{i}}\mathop{\min }\limits_{j}\left\{  {\left( {{a}_{1j} - {a}_{2j}}\right) {x}_{1} + {a}_{2j}}\right\}
$$

Example 15.4-3

Consider the following $2 \times  4$ game. The payoff is for player $A$ .

<table><tr><td></td><td>${B}_{1}$</td><td>${B}_{2}$</td><td>${B}_{3}$</td><td>${B}_{4}$</td></tr><tr><td>${A}_{1}$</td><td>2</td><td>2</td><td>3</td><td>-1</td></tr><tr><td>${A}_{2}$</td><td>4</td><td>3</td><td>2</td><td>6</td></tr></table>

The game has no pure strategy solution because the maximin and minimax values are not equal (verify!). A's expected payoffs corresponding to B's pure strategies are given as

<table><tr><td>$B$ ’s pure strategy</td><td>$A$ ’s expected payoff</td></tr><tr><td>1</td><td>$- 2{x}_{1} + 4$</td></tr><tr><td>2</td><td>$- {x}_{1} + 3$</td></tr><tr><td>3</td><td>${x}_{1} + 2$</td></tr><tr><td>4</td><td>$- 7{x}_{1} + 6$</td></tr></table>

Figure 15.7 provides TORA plot of the four straight lines associated with $B$ ’s pure strategies (file toraEx15.4-3.txt). ${}^{3}$ To determine the best of the worst solution, the lower envelope of the four lines (delineated by vertical stripes) represents the minimum (worst) expected payoff for $A$ regardless of $B$ ’s choices. The maximum (best) of the lower envelope corresponds to the maximin solution point at ${x}_{1}^{ * } = {.5}$ . This point is the intersection of the lines associated with strategies ${B}_{3}$ and ${B}_{4}$ .

FIGURE 15.7

TORA graphical solution of the two-person zero-sum game of Example 15.4-3 (file toraEx15.4-3.txt)

![bo_d56m58jef24c73bhe65g_21_311_845_1125_1145_0.jpg](bo_d56m58jef24c73bhe65g_21_311_845_1125_1145_0.jpg)

${}^{3}$ From Main Menu, select Zero-sum Games and enter the problem data, then select Graphical from the SOLVE/MODIFY menu.

Player $A$ ’s optimal solution thus calls for ${50} - {50}\mathrm{{mix}}$ of ${A}_{1}$ and ${A}_{2}$ . The corresponding value of the game, $v$ , is determined by substituting ${x}_{1} = {.5}$ in the function of either line 3 or line 4, which gives

$$
v = \left\{  \begin{array}{rr} \frac{1}{2} + 2 = \frac{5}{2}, & \text{ from line }3 \\   - 7\left( \frac{1}{2}\right)  + 6 = \frac{5}{2}, & \text{ from line }4 \end{array}\right.
$$

Player $B$ ’s optimal mix is determined by the two strategies that define the lower envelope of the graph. This means that $B$ can mix strategies ${B}_{3}$ and ${B}_{4}$ , in which case ${y}_{1} = {y}_{2} = 0$ and ${y}_{4} = 1 - {y}_{3}$ . As a result, $B$ ’s expected payoffs corresponding to $A$ ’s pure strategies are

<table><tr><td>$A$ ’s pure strategy</td><td>$B$ ’s expected payoff</td></tr><tr><td>1</td><td>$4{y}_{3} - 1$</td></tr><tr><td>2</td><td>$- 4{y}_{3} + 6$</td></tr></table>

The best of the worst solution for $B$ is the minimum point on the upper envelope of the given two lines (you will find it instructive to graph the two lines and identify the upper envelope). This process is equivalent to solving the equation

$$
4{y}_{3} - 1 =  - 4{y}_{3} + 6
$$

The solution gives ${y}_{3} = \frac{7}{8}$ , which yields the value of the game as $v = 4 \times  \left( \frac{7}{8}\right)  - 1 = \frac{5}{2}$ .

The solution of the game calls for player $A$ to mix ${A}_{1}$ and ${A}_{2}$ with equal probabilities and for player $B$ to mix ${B}_{3}$ and ${B}_{4}$ with probabilities $\frac{7}{8}$ and $\frac{1}{8}$ (Actually, the game has alternative solutions for $B$ , because the maximin point in Figure 15.7 is determined by more than two lines. Any nonnegative combination of these alternative solutions is also a legitimate solution.)

Remarks. Games in which player $A$ has $m$ strategies and player $B$ has only two can be treated similarly. The main difference is that we will be plotting $B$ ’s expected payoff corresponding to $A$ ’s pure strategies. As a result, we will be seeking the minimax, rather than the maximin, point of the upper envelope of the plotted lines. However, to solve the problem with TORA, it is necessary to express the payoff in terms of the player that has two strategies, multiplying the payoff matrix by -1 .

## Aha! Moment: Cooperation Should Be the Name of the Game!

In a two-person zero-sum game, the gain of one player is an equal loss to the opponent. A different noncooperative game involving $N\left( { \geq  2}\right)$ players was developed in 1951 by American mathematician John Nash. ${}^{4}$ The goal is to maximize each player’s payoff given that the strategies of the remaining $N - 1$ players are held fixed. Each player’s strategy is optimal against those of the others. An example of the noncooperative game is the well-known Prisoner's Dilemma, where two suspects are held incommunicado in prison pending trial. The maximum sentence for the crime is 5 years. Each prisoner has two possible interrogation strategies: remain silent or testify against the other prisoner. If both remain silent, they each get 1-year jail sentence for lack of evidence, If both simultaneously testify against one another, each gets 3 years, but if one remains silent and the other testifies, the silent prisoner gets the maximum sentence and the other is set free. The following matrix summarizes the game where the payoff (reward) $= 5 -$ jail sentence:

<table><tr><td colspan="2"></td><td colspan="2">Prisoner $B$ (Underlined elements give the payoffs to Prisoner $B$ .)</td></tr><tr><td colspan="2"></td><td>Be silent</td><td>Testify</td></tr><tr><td rowspan="2">Prisoner $A$</td><td>Be silent</td><td>4,4</td><td>0,5</td></tr><tr><td>Testify</td><td>5,0</td><td>2,2</td></tr></table>

The optimum strategy of the game calls for $A$ and $B$ to testify against one another (resulting in a 3-year jail sentence -2-year reward for each) because neither player is tempted to select another strategy without getting a worse deal eventually (convince yourself that this is the case by tracking changes of strategy). The pure "Testify" strategy is called Nash equilibrium and it is, in a way, the equivalent of the saddle point in the two-person zero-sum game. If the game has no optimal pure strategy, Nash equilibrium is replaced with a probability-weighted mixed strategy. Interestingly, if cooperation between the two players is allowed, both will benefit by choosing to be silent (1-year jail sentence).

The arms race between superpowers can be modeled as a prisoner's dilemma game with resulting mutual benefits if all parties choose to cooperate [as exemplified by the likes of the 1968 Nuclear Nonproliferation Treaty (NPT) principally between the United States and the former Soviet Union]. Other possible applications occur between competing manufacturers, among others.

As an end note, John Nash (1928-2015) shared the 1994 Nobel Prize in Economics for his contribution in noncooperative games. His work in mathematics and his severe bouts with schizophrenia when he was only in his 30s inspired the 2001 American film A Beautiful Mind.

Linear programming solution of games. Game theory bears a strong relationship to linear programming, in the sense that any two-person zero-sum game can be expressed as a linear program, and vice versa. In fact, G. Dantzig (1963, p. 24) states that J. von Neumann, father of game theory, when first introduced to the simplex method in 1947, immediately recognized this relationship and further pinpointed and stressed the concept of duality in linear programming. This section explains how games are solved by linear programming.

Player $A$ ’s optimal probabilities, ${x}_{1},{x}_{2},\ldots$ , and ${x}_{m}$ , can be determined by solving the following maximin problem:

$$
\mathop{\max }\limits_{{x}_{i}}\left\{  {\min \left( {\mathop{\sum }\limits_{{i = l}}^{m}{a}_{i1}{x}_{i},\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{i2}{x}_{i},\ldots ,\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{in}{x}_{i}}\right) }\right\}
$$

$$
{x}_{1} + {x}_{2} + \cdots  + {x}_{m} = 1
$$

$$
{x}_{i} \geq  0, i = 1,2,\ldots , m
$$

Let

$$
v = \min \left\{  {\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{i1}{x}_{i},\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{i2}{x}_{i},\ldots ,\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{in}{x}_{i}}\right\}
$$

The equation implies that

$$
\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{x}_{i} \geq  v, j = 1,2,\ldots , n
$$

Player $A$ ’s problem thus can be written as

$$
\text{ Maximize }z = v
$$

subject to

$$
v - \mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{x}_{i} \leq  0, j = 1,2,\ldots , n
$$

$$
{x}_{1} + {x}_{2} + \cdots  + {x}_{m} = 1
$$

$$
{x}_{i} \geq  0, i = 1,2,\ldots , m
$$

$v$ unrestricted

Note that the value of the game, $v$ , is unrestricted in sign.

Player $B$ ’s optimal strategies, ${y}_{1},{y}_{2},\ldots$ , and ${y}_{n}$ , are determined by solving the problem

$$
\mathop{\min }\limits_{{y}_{j}}\left\{  {\max \left( {\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{1j}{y}_{j},\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{2j}{y}_{j},\ldots ,\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{mj}{y}_{j}}\right) }\right\}
$$

$$
{y}_{1} + {y}_{2} + \cdots  + {y}_{n} = 1
$$

$$
{y}_{j} \geq  0, j = 1,2,\ldots , n
$$

Using a procedure similar to that of player $A, B$ ’s problem reduces to

$$
\text{ Minimize }w = v
$$

subject to

$$
v - \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{y}_{j} \geq  0, i = 1,2,\ldots , m
$$

$$
{y}_{1} + {y}_{2} + \cdots  + {y}_{n} = 1
$$

$$
{y}_{j} \geq  0, j = 1,2,\ldots , n
$$

$$
v\text{ unrestricted }
$$

The two problems optimize the same (unrestricted) variable $v$ , the value of the game. The reason is that $B$ ’s problem is the dual of $A$ ’s problem (verify this claim using the definition of duality in Chapter 4). This means that the optimal solution of one problem automatically yields the optimal solution of the other.

## Example 15.4-4

Solve the following game by linear programming. The value of the game, $v$ , lies between -2 and 2 .

![bo_d56m58jef24c73bhe65g_24_672_1912_606_292_0.jpg](bo_d56m58jef24c73bhe65g_24_672_1912_606_292_0.jpg)

Player A's linear program

$$
\text{ Maximize }z = v
$$

subject to

$$
v - 3{x}_{1} + 2{x}_{2} + 5{x}_{3} \leq  0
$$

$$
v + {x}_{1} - 4{x}_{2} + 6{x}_{3} \leq  0
$$

$$
v + 3{x}_{1} + {x}_{2} - 2{x}_{2} \leq  0
$$

$$
{x}_{1} + {x}_{2} + {x}_{3} = 1
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

$v$ unrestricted

The optimum solution ${}^{5}$ is ${x}_{1} = {.39},{x}_{2} = {.31},{x}_{3} = {.29}$ , and $v =  - {0.91}$ .

## Player B's Linear Program

$$
\text{ Minimize }z = v
$$

subject to

$$
v - 3{y}_{1} + {y}_{2} + 3{y}_{3} \geq  0
$$

$$
v + 2{y}_{1} - 4{y}_{2} + {y}_{3} \geq  0
$$

$$
v + 5{y}_{1} + 6{y}_{2} - 2{y}_{3} \geq  0
$$

$$
{y}_{1} + {y}_{2} + {y}_{3} = 1
$$

$v$ unrestricted

The solution yields ${y}_{1} = {.32},{y}_{2} = {.08},{y}_{3} = {.60}$ , and $v =  - {0.91}$ .

## BIBLIOGRAPHY

Chen, S., and C. Hwang, Fuzzy Multiple Attribute Decision Making, Springer-Verlag, Berlin, 1992.

Clemen, R. J., and T. Reilly, Making Hard Decisions with Decision Tools, Suite Update Edition, Duxbury, Pacific Grove, CA, 2004.

Cohan, D., S. Haas, D. Radloff, and R. Yancik, "Using Fire in Forest Management: Decision Making under Uncertainty," Interfaces, Vol. 14, No. 5, pp. 8-19, 1984.

Dantzig, G. B., Linear Programming and Extensions, Princeton University Press, Princeton, NJ, 1963.

Meyerson, R., Game Theory: Analysis of Conflict, Harvard University Press, Cambridge, MA, 1991.

Rapport, A. "Sensitivity Analysis in Decision Making," The Accounting Review, Vol. 42, No. 3, pp. 441-456, 1967.

Saaty, T. L., Fundamentals of Decision Making, RWS Publications, Pittsburgh, 1994.

---

${}^{5}$ TORA Zero-sum Games $\Rightarrow$ Solve $\Rightarrow$ LP-based can be used to solve any two-person zero-sum game.

---

## Case Study: Booking Limits in Hotel Reservations ${}^{6}$

Tool: Decision tree analysis

## Area of application: Hotels

## Description of the situation:

Hotel La Posada has a total of 300 guest rooms. Its clientele includes both business and leisure travelers. Rooms can be sold in advance (usually to leisure travelers) at a discount price. Business travelers, who invariably are late in booking their rooms, pay full price. La Posada must thus establish a booking limit on the number of discount rooms sold to leisure travelers to take advantage of the full-price business customers.

## Mathematical model:

Let $N$ be the number of available rooms and suppose that the current protection level of rooms sold at full price is $Q + 1,0 \leq  Q < N$ . The associated booking limit (rooms sold at a discount) is $N - Q - 1$ . Figure 15.8 summarizes the situation.

To determine if the protection level should be lowered from $Q + 1$ to $Q$ , we use the decision tree in Figure 15.9. Let $D$ be the random variable representing historical or forecast demand for full-price (business) rooms. Further, let $c$ be the full price and $d$ be the discount price $\left( {d < c}\right)$ . A decision to lower the protection level from $Q + 1$ to $Q$ signifies that room $Q + 1$ will be sold at the discount price $d$ because there will be ample opportunity to do so. Alternatively, not lowering the protection level will result in two probabilistic outcomes: If the demand for business rooms is greater than or equal to $Q + 1$ , then room $Q + 1$ will sell at full price, $c$ ; else the room will not sell at all. The associated probabilities are $P\{ D \geq  Q + 1\}$ and $P\{ D \leq  Q\}$ , respectively. It thus follows that the decision to lower the protection level to $Q$ should be adopted if

$$
d \geq  {cP}\{ D \geq  Q + 1\}  + {0P}\{ D \leq  Q\}
$$

FIGURE 15.8

![bo_d56m58jef24c73bhe65g_26_479_1402_618_626_0.jpg](bo_d56m58jef24c73bhe65g_26_479_1402_618_626_0.jpg)

Booking limit and protection level

---

${}^{6}$ Netessine, S., and R. Shumsky,"Introduction to the Theory and Practice of Yield Management," INFORMS Transactions on Education, Vol. 3, No. 1, pp. 20-28, 2002.

---

![bo_d56m58jef24c73bhe65g_27_467_201_942_573_0.jpg](bo_d56m58jef24c73bhe65g_27_467_201_942_573_0.jpg)

FIGURE 15.9

Decision tree for determining protection level $Q$

or

$$
P\{ D \leq  Q\}  \geq  \frac{c - d}{c}
$$

Given the distribution of demand $D$ , together with the unit costs $c$ and $d$ , the protection level $Q$ can be determined readily.

## Collection of data:

The most crucial piece of information needed to determine the protection level is the distribution of demand for full price rooms. We can use historical data over a specified time period for this purpose. The number of days a block of rooms $Q$ is reserved at full fare then estimates the demand probability $P\{ D = Q\}$ from which the cumulative probability can be determined. Table 15.1 provides the data for determining the distribution of demand. The first two columns include the raw data.

The use of the information in Table 15.1 can be illustrated by the following situation. Suppose that the full fare is \$159 and the discount fare is \$105. The protection limit is determined such that

$$
P\{ D \leq  Q\}  \geq  \frac{{159} - {105}}{159} = {.33962}
$$

The cumulative probability column in Table 15.1 shows the protection level to be $Q = {79}$ rooms.

## Conclusion:

The ideas presented in this study can be extended similarly to setting booking limits for airline tickets. Additionally, in place of using one booking limit, the analysis can be modified to allow setting several levels of booking limits with the discount price increasing with the nearness of the reservation date. The most important information for the model is a reliable estimate of demand data.

TABLE 15.1 Calculation of $P\{ D = x\}$ and $P\{ D \leq  x\}$

<table><tr><td>Number of rooms, $Q$</td><td>Number of days in demand</td><td>$P\{ D = Q\}$</td><td>$P\{ D \leq  Q\}$</td></tr><tr><td>0-70</td><td>12</td><td>0.09756</td><td>0.097561</td></tr><tr><td>71</td><td>3</td><td>0.02439</td><td>0.12195</td></tr><tr><td>72</td><td>3</td><td>0.02439</td><td>0.14634</td></tr><tr><td>73</td><td>2</td><td>0.01626</td><td>0.16260</td></tr><tr><td>74</td><td>0</td><td>0.00000</td><td>0.16260</td></tr><tr><td>75</td><td>4</td><td>0.03252</td><td>0.19512</td></tr><tr><td>76</td><td>4</td><td>0.03252</td><td>0.22764</td></tr><tr><td>77</td><td>5</td><td>0.04065</td><td>0.26829</td></tr><tr><td>78</td><td>2</td><td>0.01626</td><td>0.28455</td></tr><tr><td>79</td><td>7</td><td>0.05691</td><td>0.34146</td></tr><tr><td>80</td><td>4</td><td>0.03252</td><td>0.37398</td></tr><tr><td>81</td><td>10</td><td>0.08130</td><td>0.45528</td></tr><tr><td>82</td><td>13</td><td>0.10569</td><td>0.56098</td></tr><tr><td>83</td><td>12</td><td>0.09756</td><td>0.65854</td></tr><tr><td>84</td><td>4</td><td>0.03252</td><td>0.69106</td></tr><tr><td>85</td><td>9</td><td>0.07317</td><td>0.76423</td></tr><tr><td>86</td><td>10</td><td>0.08130</td><td>0.84553</td></tr><tr><td>>86</td><td>19</td><td>0.15447</td><td>1.00000</td></tr><tr><td>Total</td><td>123</td><td>1.00000</td><td></td></tr></table>

PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>15.1</td><td>15-1 to 15-8</td><td>15.3</td><td>15-38 to 15-40</td></tr><tr><td>15.2.1</td><td>15-9 to 15-27</td><td>15.4.1</td><td>15-41 to 15-45</td></tr><tr><td>15.2.2</td><td>15-28 to 15-37</td><td>15.4.2</td><td>15-46 to 15-53</td></tr></table>

*15-1. Suppose that the following weights are specified for the situation of Martin and Jane (Figure 15.2):

$$
p = {.5}, q = {.5}
$$

$$
{p}_{1} = {.4},{p}_{2} = {.6}
$$

$$
{p}_{11} = {.129},{p}_{12} = {.277},{p}_{13} = {.594}
$$

$$
{p}_{21} = {.545},{p}_{22} = {.273},{p}_{23} = {.182}
$$

$$
{q}_{1} = {.6},{q}_{2} = {.4}
$$

$$
{q}_{11} = {.2},{q}_{12} = {.3},{q}_{13} = {.5}
$$

$$
{q}_{21} = {.5},{q}_{22} = {.2},{q}_{23} = {.3}
$$

Based on this information, rank the three universities.

15-2. Consider the two-hierarchal data of Problem 15-1. Copy the weights in a logical order into the solution summary section of the spreadsheet excelAHP.xls, then develop the formula for evaluating the first alternative, UA, and copy it to evaluate the remaining two alternatives. ${}^{7}$

*15-3. The personnel department at C&H has narrowed the search for a new hire to three candidates: Steve $\left( S\right)$ , Jane $\left( J\right)$ , and Maisa $\left( M\right)$ . The final selection is based on three criteria: personal interview $\left( I\right)$ , experience $\left( E\right)$ , and references $\left( R\right)$ . The department uses matrix $\mathbf{A}$ (given below) to establish the preferences among the three criteria. After interviewing the three candidates and compiling the data regarding their experiences and references, the matrices ${\mathbf{A}}_{I},{\mathbf{A}}_{E}$ , and ${\mathbf{A}}_{R}$ are constructed. Which of the three candidates should be hired? Assess the consistency of the data.

$$
\mathbf{A} = \begin{matrix} I & E & R & S & J & M \\  I & 2 & \frac{1}{4} & \frac{1}{5} & S & I \\  R & I & \frac{1}{5} & \frac{1}{1} & M & I = I \end{matrix}\;\left( \begin{array}{lll} I & 3 & 4 \\  \frac{1}{3} & 1 & \frac{1}{5} \\  \frac{1}{4} & 5 & 1 \end{array}\right)
$$

$$
{\mathbf{A}}_{E} = J\left( \begin{matrix} S & J & M & S & J & M \\  1 & \frac{1}{3} & 2 & J & {M}_{2} & J \\  0 & 1 & \frac{1}{2} & 2 & 1 & M \end{matrix}\right) {\mathbf{A}}_{R} = J\left( \begin{matrix} 1 & \frac{1}{2} & 1 \\  2 & 1 & \frac{1}{2} \\  1 & 2 & 1 \end{matrix}\right)
$$

15-4. Kevin and June Park $\left( {K\text{ and }J}\right)$ are in the process of buying a new house. Three houses, $A, B$ , and $C$ , are available. The Parks have agreed on two criteria for the selection of the house - amount of yard work $\left( Y\right)$ and proximity to place of work $\left( W\right)$ - and have developed the following comparison matrices. Rank the three houses in order of priority, and compute the consistency ratio for each matrix.

![bo_d56m58jef24c73bhe65g_29_752_1252_251_149_0.jpg](bo_d56m58jef24c73bhe65g_29_752_1252_251_149_0.jpg)

![bo_d56m58jef24c73bhe65g_29_589_1419_564_143_0.jpg](bo_d56m58jef24c73bhe65g_29_589_1419_564_143_0.jpg)

$$
{\mathbf{A}}_{KY} = B\left( \begin{matrix} A & B & C & A & B & C \\  1 & 2 & 3 & C & A & B \\  \frac{1}{2} & \frac{1}{1} & 2 & 1 & A & C \\  \frac{1}{3} & \frac{1}{2} & \frac{1}{1} & 1 & B & C \end{matrix}\right) \;{\mathbf{A}}_{KW} = B\left( \begin{matrix} A & B & C & A & B & C \\  \frac{1}{2} & 1 & \frac{1}{3} & A & C & A \\  \frac{1}{2} & 1 & \frac{1}{3} & A & B & C \\  \frac{1}{2} & \frac{1}{3} & 1 & C & \frac{1}{2} & A \end{matrix}\right) \;{\mathbf{A}}_{JW} = B\left( \begin{matrix} A & B & C & A & B & C \\  \frac{1}{2} & 1 & 3 & 3 & C & B \\  \frac{1}{2} & 1 & 3 & 1 & C & A \\  \frac{1}{4} & \frac{1}{3} & 1 & 1 & B & C \end{matrix}\right)
$$

*15-5. A new author sets three criteria for selecting a publisher for an OR textbook: royalty percentage $\left( R\right)$ , marketing $\left( M\right)$ , and advance payment $\left( A\right)$ . Two publishers, $H$ and $P$ , have expressed interest in the book. Using the following comparison matrices, rank the two publishers and assess the consistency of the decision.

$$
\begin{array}{l} A = M\left( \begin{matrix} 1 & 1 & 1 \\  1 & 1 & \frac{1}{4} \\  1 & 1 & \frac{1}{5} \end{matrix}\right) \\  A = M\left( \begin{matrix} 1 & 1 & \frac{1}{4} \\  1 & 1 & \frac{1}{5} \\  4 & 5 & 1 \end{matrix}\right) \\  \end{array}
$$

$$
{\mathbf{A}}_{R} = H\left( \begin{array}{ll} 1 & 2 \\  1 & 2 \\  \frac{1}{2} & 1 \end{array}\right) \;{\mathbf{A}}_{M} = H\left( \begin{array}{ll} 1 & \frac{1}{2} \\  1 & \frac{1}{2} \\  2 & 1 \end{array}\right) \;{\mathbf{A}}_{A} = H\left( \begin{array}{ll} 1 & 1 \\  1 & 1 \end{array}\right)
$$

15-6. A professor of political science wants to predict the outcome of a school board election. Three candidates, Ivy (I), Bahrn (B), and Smith (S), are running for one position. There are three categories of voters: left $\left( L\right)$ , center $\left( C\right)$ , and right $\left( R\right)$ . The candidates are judged based on three factors: educational experience $\left( E\right)$ , stand on issues $\left( S\right)$ , and personal character $\left( P\right)$ . The following are the comparison matrices for the first hierarchy of left, center, and right:

$$
\mathbf{A} = \left. \begin{matrix} L & C & R & E & S & P \\  1 & 2 & \frac{1}{2} & \frac{1}{5} & {\mathbf{A}}_{L} = & S\left( \begin{array}{lll} 1 & 3 & \frac{1}{2} \\  \frac{1}{3} & 1 & \frac{1}{3} \\  2 & 5 & 1 \end{array}\right)  \end{matrix}\right.
$$

$$
{\mathbf{A}}_{c} = \left\lbrack  \begin{matrix} E & S & P & E & S & P \\  1 & 2 & 2 & 2 & E & P \\  \frac{1}{2} & 1 & 1 & 1 & 1 & 1 \end{matrix}\right\rbrack  \;{\mathbf{A}}_{R} = \left\lbrack  \begin{array}{lll} E & S & P \\  1 & 1 & 8 \\  1 & 1 & 8 \\  \frac{1}{2} & \frac{1}{8} & 1 \end{array}\right\rbrack
$$

The professor generated nine more comparison matrices for the second hierarchy representing experience $\left( E\right)$ , stand on issues $\left( S\right)$ , and personal character $\left( P\right)$ . AHP was then used to reduce these matrices to the following relative weights:

<table><tr><td rowspan="2">Candidate</td><td colspan="3">Left</td><td colspan="3">Center</td><td colspan="3">Right</td></tr><tr><td>$E$</td><td>$S$</td><td>$P$</td><td>$E$</td><td>$S$</td><td>$P$</td><td>$E$</td><td>$S$</td><td>$P$</td></tr><tr><td>Ivy</td><td>.1</td><td>.2</td><td>.3</td><td>.3</td><td>.5</td><td>.2</td><td>.7</td><td>.1</td><td>.3</td></tr><tr><td>Bahrn</td><td>.5</td><td>.4</td><td>.2</td><td>.4</td><td>.2</td><td>.4</td><td>.1</td><td>.4</td><td>.2</td></tr><tr><td>Smith</td><td>.4</td><td>.4</td><td>.5</td><td>.3</td><td>.3</td><td>.4</td><td>.2</td><td>.5</td><td>.5</td></tr></table>

Determine the winning candidate, and assess the consistency of the decision.

15-7. A school district is in dire need to reduce expenses to meet new budgetary restrictions at its elementary schools. Two options are available: delete the physical education program $\left( E\right)$ , or delete the music program $\left( M\right)$ . The superintendent has formed a committee with equal-vote representation from the school board (S) and the parent-teacher association (P) to study the situation and make a recommendation. The committee has decided to study the issue from the standpoint of budget restriction $\left( B\right)$ and students needs $\left( N\right)$ . The analysis produced the following comparison matrices:

![bo_d56m58jef24c73bhe65g_31_702_195_584_145_0.jpg](bo_d56m58jef24c73bhe65g_31_702_195_584_145_0.jpg)

![bo_d56m58jef24c73bhe65g_31_687_350_604_139_0.jpg](bo_d56m58jef24c73bhe65g_31_687_350_604_139_0.jpg)

![bo_d56m58jef24c73bhe65g_31_685_499_603_142_0.jpg](bo_d56m58jef24c73bhe65g_31_685_499_603_142_0.jpg)

Analyze the decision problem, and make a recommendation.

15-8. An individual is in the process of buying a car and has narrowed the choices to three models: ${M1},{M2}$ , and ${M3}$ . The deciding factors include purchase price (PP), maintenance cost (MC), cost of city driving (CD), and cost of rural driving (RD). The following table provides the relevant data for 3 years of operation:

<table><tr><td>Car Model</td><td>PP (\$)</td><td>MC (\$)</td><td>CD (\$)</td><td>RD (\$)</td></tr><tr><td>${M1}$</td><td>6000</td><td>1800</td><td>4500</td><td>1500</td></tr><tr><td>${M2}$</td><td>8000</td><td>1200</td><td>2250</td><td>750</td></tr><tr><td>${M3}$</td><td>10,000</td><td>600</td><td>1125</td><td>600</td></tr></table>

Use the cost data to develop the comparison matrices. Assess the consistency of the matrices, and determine the choice of model.

15-9. You have been invited to play the Fortune Wheel game on television. The wheel operates electronically with two buttons that produce hard $\left( H\right)$ or soft $\left( S\right)$ spin. The wheel itself is divided into white $\left( W\right)$ and red $\left( R\right)$ half-circle regions. You have been told that the wheel is designed to stop on white 30% of the time. The payoff of the game is

<table><tr><td></td><td>$W$</td><td>$R$</td></tr><tr><td>$H$</td><td>\$800</td><td>\$200</td></tr><tr><td>$S$</td><td>-\$2500</td><td>\$1000</td></tr></table>

Develop the associated decision tree, and determine a course of action based on the expected value criterion.

*15-10. Farmer McCoy can plant either corn or soybeans. The probabilities that the next harvest prices will go up, stay the same, or go down are .25, .30, and .45, respectively. If the prices go up, the corn crop will net \$30,000 and the soybeans will net \$10,000. If the prices remain unchanged, McCoy will (barely) break even. But if the prices go down, the corn and soybeans crops will sustain losses of \$35,000 and \$5000, respectively.

(a) Represent McCoy's problem as a decision tree.

(b) Which crop should McCoy plant?

15-11. You have the chance to invest in three mutual funds: utility, aggressive growth, and global. The value of your investment will change depending on the market conditions.

There is a 20% chance the market will go down, 45% chance it will remain moderate, and 35% chance it will perform well. The following table provides the percentage change in the investment value under the three conditions:

<table><tr><td rowspan="2">Alternative</td><td colspan="3">Percent return on investment</td></tr><tr><td>Down market (%)</td><td>Moderate market (%)</td><td>Up market (%)</td></tr><tr><td>Utility</td><td>+5</td><td>+7</td><td>+8</td></tr><tr><td>Aggressive growth</td><td>-10</td><td>+5</td><td>+30</td></tr><tr><td>Global</td><td>+2</td><td>+7</td><td>+20</td></tr></table>

(a) Represent the problem as a decision tree.

(b) Which mutual fund should you select?

15-12. You have the chance to invest your money in either a 7.5% bond that sells at face value or an aggressive growth stock that pays only 1% dividend. If inflation occurs, the interest rate will go up to 8%, in which case the principal value of the bond will go down by 10%, and the stock value will go down by 20%. If recession materializes, the interest rate will go down to 6%. In this case, the principal value of the bond is expected to go up by 5%, and the stock value will increase by 20%. If the economy remains unchanged, the stock value will go up by 8% and the bond principal value will remain the same. Economists estimate a 10% chance of inflation and 5% of recession. You are basing your investment decision on next year's economic conditions.

(a) Represent the problem as a decision tree.

(b) Would you invest in stocks or bonds?

15-13. AFC is about to launch its new Wings 'N Things fast food nationally. The research department is convinced that Wings 'N Things will be a great success and wants to introduce it immediately in all AFC outlets without advertising. The marketing department sees "things" differently and wants to unleash an intensive advertising campaign. The advertising campaign will cost \$120,000 and if successful will produce \$950,000 revenue. If the campaign is unsuccessful (and there is a 25% chance it won't be), the revenue is estimated at only \$200,000. If no advertising is used, the revenue is estimated at \$400,000 with probability .7 if customers are receptive to the new product and \$200,000 with probability .3 if they are not.

(a) Draw the associated decision tree.

(b) What course of action should AFC follow in launching the new product?

*15-14. A fair coin is flipped three successive times. You receive \$1.00 for each head $\left( H\right)$ that turns up and an additional \$.25 for each two successive heads that appear (remember that ${HHH}$ includes two sets of ${HH}$ ). However, you give back \$1.10 for each tail that shows up. You have the option to either play or not play the game.

(a) Draw the decision tree for the game.

(b) Would you favor playing this game?

15-15. You have the chance to play the following game in a gambling casino. A fair die is rolled twice, leading to four outcomes: (1) both rolls show the same even number, (2) both rolls show the same odd number, (3) the two rolls show either even followed by odd or odd followed by even, and (4) all other outcomes. You are allowed to bet your money on exactly two outcomes with equal dollar amounts. For example, you can bet equal dollars on even-match (outcome 1) and odd-match (outcome 2). The payoff for each dollar you bet is \$2.00 for the first outcome, \$1.95 for the second and the third outcomes, and \$1.50 for the fourth outcome.

(a) Draw the decision tree for the game.

(b) Which two choices would you make?

(c) Do you ever come out ahead in this game?

15-16. Acme Manufacturing produces lots of widget with .8%, 1%, 1.2%, and 1.4% defectives according to the respective probabilities .4, .3, .25, and .05. Three customers, A, B, and $C$ , are contracted to receive batches with no more than .8%,1.2%, and 1.4% defectives, respectively. If the defectives are higher than contracted, Acme is penalized \$100 for each .1% increase. Supplying higher-quality batches than required costs Acme \$50 for each .1% below specifications. Assume that the batches are not inspected before shipment.

(a) Draw the associated decision tree.

(b) Which of the three customers should have the highest priority to receive their order?

15-17. TriStar plans to open a new plant in Arkansas. The company can open a full-size plant now or a small-size plant that can be expanded 2 years later if warranted by high demand. The time horizon for the decision problem is 10 years. TriStar estimates that the probabilities for high and low demands over the next 10 years are .75 and .25, respectively. The cost of immediate construction is \$5 million for a large plant and \$1 million for a small plant. The expansion cost of a small plant 2 years from now is \$4.2 million. The income from the operation over the next 10 years is given in the following table:

<table><tr><td rowspan="2">Alternative</td><td colspan="2">Annual income estimates (in \$1,000)</td></tr><tr><td>High demand</td><td>Low demand</td></tr><tr><td>Full-size plant now</td><td>1000</td><td>300</td></tr><tr><td>Small-size plant now</td><td>250</td><td>200</td></tr><tr><td>Expanded plant in 2 years</td><td>900</td><td>200</td></tr></table>

(a) Develop the associated decision tree, given that after 2 years TriStar has the option to expand or not expand the small plant.

(b) Develop a construction strategy for TriStar over the next 10 years. (For simplicity, ignore the time value of money.)

15-18. Rework Problem 15-17, assuming that decisions are made taking into account the time value of money at an annual interest rate of 10%. [Note: You need compound interest tables to solve this problem. You can use Excel function $\operatorname{NPV}\left( {i, R}\right)$ to compute the present value of cash flows stored in range $R$ , given interest rate $i$ . NPV assumes that each cash flow occurs at the end of the year.]

15-19. Rework Problem 15-17, assuming that the demand can be high, medium, and low with probabilities .7, .2, and .1, respectively. Expansion of a small plant will occur only if demand in the first 2 years is high. The following table provides estimates of the annual income. Ignore the time value of money.

<table><tr><td rowspan="2">Alternative</td><td colspan="3">Annual income estimates (in \$1000)</td></tr><tr><td>High demand</td><td>Medium demand</td><td>Low demand</td></tr><tr><td>Full-sized plant now</td><td>1000</td><td>500</td><td>300</td></tr><tr><td>Small-sized plant now</td><td>400</td><td>280</td><td>150</td></tr><tr><td>Expanded plant in 2 years</td><td>900</td><td>600</td><td>200</td></tr></table>

*15-20. Sunray Electric Coop uses a fleet of 20 trucks to service its electric network. The company wants to develop a preventive maintenance schedule for the fleet. The probability of a breakdown in year 1 is zero. For year 2, the breakdown probability is .03, increasing annually by .01 for years 3 through 10. Beyond year 10, the breakdown probability remains constant at .13 . The cost per truck is $\$ {200}$ for a random breakdown and $\$ {75}$ for a preventive maintenance.

(a) Develop the associated decision tree.

(b) Determine the optimal period (in years) between successive preventive maintenances.

15-21. Daily demands for loaves of bread at a grocery store are specified by the following probability distribution:

<table><tr><td>$n$</td><td>100</td><td>150</td><td>200</td><td>250</td><td>300</td></tr><tr><td>${p}_{n}$</td><td>.20</td><td>.25</td><td>.30</td><td>.15</td><td>.10</td></tr></table>

The store buys a loaf for 55 cents and sells it for \$1.20 each. Any unsold loaves at the end of the day are disposed of at 25 cents each. Assume that the stock level is restricted to one of the demand levels specified for ${p}_{n}$ .

(a) Develop the associated decision tree.

(b) How many loaves should be stocked daily?

15-22. In Problem 15-21, suppose that the store wishes to extend the decision problem to a 2-day horizon. The alternatives for the second day depend on the demand in the first day. If demand on day 1 equals the amount stocked, the store will continue to order the same quantity for day 2; if it exceeds the amount stocked, the store can order any of the higher-level stocks; and if it is less than the amount stocked, the store can order any of the lower-level stocks. Develop the associated decision tree, and determine the optimal ordering strategy.

*15-23. An automatic machine produces $\alpha$ (thousands of) units of a product per day. As $\alpha$ increases, the proportion of defectives, $p$ , goes up according to the following probability density function:

$$
f\left( p\right)  = \left\{  \begin{array}{ll} \alpha {p}^{\alpha  - 1}, & 0 \leq  p \leq  1 \\  0, & \text{ otherwise } \end{array}\right.
$$

Each defective item incurs a loss of \$50. A good item yields \$5 profit.

(a) Develop a decision tree for this problem.

(b) Determine the value of $\alpha$ that maximizes the expected profit.

15-24. The outer diameter, $d$ , of a cylinder is processed on an automatic machine with upper and lower tolerance limits of $d + {t}_{U}$ and $d - {t}_{L}$ . The production process follows a normal distribution with mean $\mu$ and standard deviation $\sigma$ . Oversized cylinders are reworked at the cost of ${c}_{1}$ dollars each. Undersized cylinders are salvaged at the cost of ${c}_{2}$ dollars each. Develop the decision tree, and determine the optimal setting $d$ for the machine.

15-25. Cohan and Associates (1984). Modern forest management uses controlled fires to reduce fire hazards and to stimulate new forest growth. Management has the option to postpone or plan a burning. In a specific forest tract, if burning is postponed, a general administrative cost of \$300 is incurred. If a controlled burning is planned, there is a 50% chance that good weather will prevail and burning will cost \$3200. The results of the burning may be either successful with probability .6 or marginal with probability .4. Successful execution will result in an estimated benefit of \$6000, and marginal execution will provide only \$3000 in benefits. If the weather is poor, burning will be cancelled incurring a cost of \$1200 and no benefit.

(a) Develop a decision tree to determine whether burning should be planned or postponed.

(b) Study the sensitivity of the solution to changes in the probability of good weather.

15-26. Rapport (1967). A manufacturer has used linear programming to determine the optimum production mix of the various TV models it produces. Recent information received by the manufacturer indicates that there is a 40% chance that the supplier of a component used in one of the models may raise the price by \$35. The manufacturer thus can either continue to use the original (optimum) product mix (A1) or use a new (optimum) mix based on the higher component price (A2). Naturally, action A1 is ideal if the price is not raised, and action A2 will also be ideal if the price is raised. The following table provides the resulting total profit per month as a function of the action taken and the random outcome regarding the component price.

<table><tr><td rowspan="3">Original mix (A1) <br> New mix (A2)</td><td>Price increase (O1)</td><td>No price increase (O2)</td></tr><tr><td>\$400,000</td><td>\$295,500</td></tr><tr><td>\$372,000</td><td>\$350,000</td></tr></table>

(a) Develop the associated decision tree, and determine which action should be adopted.

(b) The manufacturer can invest \$1000 to obtain additional information about whether or not the price will increase. This information says that there is a 58% chance that the probability of price increase will be .9 and a 42% chance that the probability of price increase will be .3. Would you recommend the additional investment?

*15-27. Aspiration Level Criterion. Acme Manufacturing uses a chemical in one of its processes. The shelf life is 1 month, and any amount left is destroyed. The amount, $x$ , in gallons of the chemical used by Acme is represented by the following distribution:

$$
f\left( x\right)  = \left\{  \begin{array}{ll} \frac{200}{{x}^{2}}, & {100} \leq  x \leq  {200} \\  0, & \text{ otherwise } \end{array}\right.
$$

The actual consumption of the chemical occurs instantaneously at the start of the month. Acme wants to determine the level of the chemical that satisfies two conflicting criteria (or aspiration levels): The average excess quantity for the month does not exceed 20 gallons, and the average shortage quantity for the month does not exceed 40 gallons.

15-28. Data in a community college show that ${80}\%$ of new students who took calculus in high school do well, compared with 50% of those who did not take calculus. Admissions for the current academic year show that only 40% of the new students have completed a course in calculus. What is the probability that a new student will do well in college?

*15-29. Elektra receives 75% of its electronic components from vendor $A$ and the remaining 25% from vendor $B$ . The percentage of defectives from vendors $A$ and $B$ are 1% and 2%, respectively. When a random sample of size 5 from a received lot is inspected, only one defective unit is found. Determine the probability that the lot is received from vendor $A$ . From vendor $B$ . (Hint: The probability distribution of defective items in a sample is binomial.)

15-30. In Example 15.2-2, suppose that you have the additional option of investing the original \$10,000 in a safe certificate of deposit that yields 4% interest. The friend's advice applies to investing in the stock market only.

(a) Develop the associated decision tree.

(b) What is the optimal decision in this case? (Hint: Make use of $P\left\{  {v}_{1}\right\}$ and $P\left\{  {v}_{2}\right\}$ given in step 3 of Example 15.2-2 to determine the expected value of investing in the stock market.)

*15-31. You are the author of what promises to be a successful novel. You have the option to either publish the novel yourself or through a publisher. The publisher is offering you \$20,000 for signing the contract. If the novel is successful, it will sell 200,000 copies. Else, it will sell 10,000 copies only. The publisher pays a \$1 royalty per copy. A market survey indicates that there is a 70% chance that the novel will be successful. If you undertake publishing, you will incur an initial cost of \$90,000 for printing and marketing, but each copy sold will net you \$2.

(a) Based on the given information, would you accept the publisher's offer or publish the novel yourself?

(b) Suppose that you contract a literary agent to conduct a survey concerning the potential success of the novel. From past experience, the agent advises you that when a novel is successful, the survey will predict the wrong outcome 20% of the time. When the novel is not successful, the survey will give the correct prediction 85% of the time. How would this information affect your decision?

15-32. Consider Farmer McCoy's decision situation in Problem 15-10. The farmer has the additional option of using the land as a grazing range, in which case a payoff of \$7500 is guaranteed. The farmer has also secured additional information from a broker regarding the degree of stability of future commodity prices. The broker's assessment of "favorable" and "unfavorable" is described by the following conditional probabilities:

![bo_d56m58jef24c73bhe65g_36_836_1707_390_255_0.jpg](bo_d56m58jef24c73bhe65g_36_836_1707_390_255_0.jpg)

The symbols ${a}_{1}$ and ${a}_{2}$ represent the "favorable" and "unfavorable" assessments, and ${s}_{1},{s}_{2}$ , and ${s}_{3}$ represent the "up," "same," and "down" changes in future prices.

(a) Develop the associated decision tree.

(b) Specify the optimal decision for the problem.

15-33. In Problem 15-13, suppose that AFC management has decided to test-market its Wings 'N Things in selective locations. The outcome of the test is either "good" $\left( {a}_{1}\right)$ or "bad" $\left( {a}_{2}\right)$ . The test yields the following conditional probabilities with and without the advertising campaign:

$\mathrm{P}\left\{  {{a}_{j} \mid  {w}_{i}}\right\}   -$ No campaign

<table><tr><td></td><td>${a}_{1}$</td><td>${a}_{2}$</td></tr><tr><td>${w}_{1}$</td><td>.8</td><td>.2</td></tr><tr><td>${w}_{2}$</td><td>.4</td><td>.6</td></tr></table>

${a}_{1} \; {a}_{2}$

${v}_{1}$ .95 .05

${v}_{2}$ .3 .7

The symbols ${v}_{1}$ and ${v}_{2}$ represent "success" and "no success," and ${w}_{1}$ and ${w}_{2}$ represent "receptive" and "not receptive."

(a) Develop the associated decision tree.

(b) Determine the best course of action for AFC.

15-34. Historical data at Acme Manufacturing estimate a 5% chance that a batch of widgets will be unacceptable (bad). A bad batch has 15% defective items, and a good batch includes only 4% defective items. Letting $a = {\theta }_{1}$ and $a = {\theta }_{2}$ represent a good and a bad batch, respectively, the associated prior probabilities are given as

$$
P\left\{  {a = {\theta }_{1}}\right\}   = {.95}\text{ and }P\left\{  {a = {\theta }_{2}}\right\}   = {.05}
$$

Instead of shipping batches based solely on prior probabilities, a test sample of two items is used, giving rise to three possible outcomes: (1) both items are good $\left( {z}_{1}\right)$ , (2) one item is good $\left( {z}_{2}\right)$ , and (3) both items are defective $\left( {z}_{3}\right)$ .

(a) Determine the posterior probabilities $P\left\{  {{\theta }_{i} \mid  {z}_{j}}\right\}  , i = 1,2;j = 1,2,3$ .

*(b) Suppose that the manufacturer ships batches to two customers, $A$ and $B$ . The contracts specify that the defectives for $A$ and $B$ should not exceed 5% and 8%, respectively. A penalty of \$100 is incurred per percentage point above the maximum limit. Supplying better-quality batches than specified by the contract costs the manufacturer \$50 per percentage point. Develop the associated decision tree, and determine a priority strategy for shipping the batches.

*15-35. You are a student at the University of Arkansas and desperately want to attend the next Razorbacks basketball game. The problem is that the admission ticket costs \$10, and you have only \$5. You can bet your \$5 in a poker game, with a 50-50 chance of either doubling your money or losing all of it.

(a) Based on the real value of money, would you be tempted to participate in the poker game?

(b) Based on your ardent desire to see the game, translate the actual money into a utility function.

(c) Based on the utility function you developed in (b), would you be tempted to participate in the poker game?

*15-36. The Golden family has just moved to a location where earthquakes are not uncommon. They must decide whether to build their house according to the high-standard earthquake code. The construction cost using the earthquake code is \$850,000; otherwise, a comparable house can be constructed for only \$350,000. If an earthquake occurs (and there is a probability of .001 it might happen), a substandard home will cost \$900,000 to repair. Develop the lottery associated with this situation, assuming a utility scale from 0 to 100 .

15-37. An investment of \$10,000 in a high-risk venture has a 50-50 chance over the next year of increasing to \$14,000 or decreasing to \$8000. Thus the net return can be either \$4000 or - \$2000.

(a) Assuming a risk-neutral investor and a utility scale from 0 to 100, determine the utility of $\$ 0$ net return on investment and the associated indifference probability.

(b) Suppose that two investors $A$ and $B$ have exhibited the following indifference probabilities:

<table><tr><td rowspan="2">Net return (\$)</td><td colspan="2">Indifference probability</td></tr><tr><td>Investor A</td><td>Investor B</td></tr><tr><td>-2000</td><td>1.00</td><td>1.00</td></tr><tr><td>-1000</td><td>0.30</td><td>0.90</td></tr><tr><td>0</td><td>0.20</td><td>0.80</td></tr><tr><td>1000</td><td>0.15</td><td>0.70</td></tr><tr><td>2000</td><td>0.10</td><td>0.50</td></tr><tr><td>3000</td><td>0.05</td><td>0.40</td></tr><tr><td>4000</td><td>0.00</td><td>0.00</td></tr></table>

Graph the utility functions for investors $A$ and $B$ , and categorize each investor as either a risk-averse person or a risk seeker.

(c) Suppose that investor $A$ has the chance to invest in one of two ventures. Venture I can produce a net return of \$2000 with probability .4 or a net loss of \$1000 with probability .6. Venture II can produce a net return of \$3000 with probability .6 and no return with probability .4. Based on the utility function in (b), use the expected utility criterion to determine the venture investor $A$ should select. What is the expected monetary value associated with the selected venture? (Hint: Use linear interpolation of the utility function.)

(d) Repeat part (c) for investor $B$ .

*15-38. Hank is an intelligent student and usually makes good grades, provided that he can review the course material the night before the test. For tomorrow's test, Hank is faced with a small problem: His fraternity brothers are having an all-night party in which he would like to participate. Hank has three options:

${a}_{1} =$ Party all night

${a}_{2} =$ Divide the night equally between studying and partying

${a}_{3} =$ Study all night

Tomorrow’s exam can be easy $\left( {s}_{1}\right)$ , moderate $\left( {s}_{2}\right)$ , or tough $\left( {s}_{3}\right)$ , depending on the professor's unpredictable mood. Hank anticipates the following scores:

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>${s}_{3}$</td></tr><tr><td>${a}_{1}$</td><td>85</td><td>60</td><td>40</td></tr><tr><td>${a}_{2}$</td><td>92</td><td>85</td><td>81</td></tr><tr><td>${a}_{3}$</td><td>100</td><td>88</td><td>82</td></tr></table>

(a) Recommend a course of action for Hank (based on each of the four criteria of decisions under uncertainty).

(b) Suppose that Hank is more interested in the letter grade he will get. The dividing scores for the passing letter grades A to D are90,80,70, and 60, respectively. Would this attitude toward grades call for a change in Hank's course of action?

15-39. For the upcoming planting season, Farmer McCoy can plant corn $\left( {a}_{1}\right)$ , wheat $\left( {a}_{2}\right)$ , or soybeans $\left( {a}_{3}\right)$ or use the land for grazing $\left( {a}_{4}\right)$ . The payoffs associated with the different actions are influenced by the amount of rain: heavy rainfall $\left( {s}_{1}\right)$ , moderate rainfall $\left( {s}_{2}\right)$ , light rainfall $\left( {s}_{3}\right)$ , or drought $\left( {s}_{4}\right)$ . The payoff matrix (in thousands of dollars) is estimated as

<table><tr><td></td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>${s}_{3}$</td><td>${s}_{4}$</td></tr><tr><td>${a}_{1}$</td><td>-20</td><td>60</td><td>30</td><td>-5</td></tr><tr><td>${a}_{2}$</td><td>40</td><td>50</td><td>35</td><td>0</td></tr><tr><td>${a}_{3}$</td><td>-50</td><td>100</td><td>45</td><td>-10</td></tr><tr><td>${a}_{4}$</td><td>12</td><td>15</td><td>15</td><td>10</td></tr></table>

Develop a course of action for Farmer McCoy based on each of the four decisions under uncertainty criteria.

15-40. One of $N$ machines must be selected for manufacturing $Q$ units of a specific product. The minimum and maximum demands for the product are ${Q}^{ * }$ and ${Q}^{* * }$ , respectively. The total production cost for $Q$ items on machine $i$ involves a fixed cost ${K}_{i}$ and a variable cost per unit ${c}_{i}$ , and it is given as

$$
T{C}_{i} = {K}_{i} + {c}_{i}Q
$$

(a) Devise a solution for the problem under each of the four criteria of decisions under uncertainty.

(b) For ${1000} \leq  Q \leq  {4000}$ , solve the problem for the following set of data:

<table><tr><td>Machine $i$</td><td>${K}_{i}\left( \mathbb{s}\right)$</td><td>${C}_{i}\left( \mathbb{s}\right)$</td></tr><tr><td>1</td><td>100</td><td>5</td></tr><tr><td>2</td><td>40</td><td>12</td></tr><tr><td>3</td><td>150</td><td>3</td></tr><tr><td>4</td><td>90</td><td>8</td></tr></table>

15-41. In games (a) and (b) given below, the payoff is for player $A$ . Each game has a pure strategy solution. In each case, determine the strategies that define the saddle point and the value of the game.

<table><tr><td>(a)</td><td>${B}_{1}$</td><td>${B}_{2}$</td><td>${B}_{3}$</td><td>${B}_{4}$</td></tr><tr><td>${A}_{1}$</td><td>9</td><td>6</td><td>2</td><td>8</td></tr><tr><td>${A}_{2}$</td><td>8</td><td>9</td><td>4</td><td>5</td></tr><tr><td>${A}_{3}$</td><td>7</td><td>5</td><td>2</td><td>5</td></tr></table>

<table><tr><td></td><td>${B}_{1}$</td><td>${B}_{2}$</td><td>${B}_{3}$</td><td>${B}_{4}$</td></tr><tr><td>${A}_{1}$</td><td>5</td><td>-4</td><td>-5</td><td>6</td></tr><tr><td>${A}_{2}$</td><td>-3</td><td>-4</td><td>-8</td><td>-2</td></tr><tr><td>${A}_{3}$</td><td>6</td><td>8</td><td>-8</td><td>-9</td></tr><tr><td>${A}_{4}$</td><td>7</td><td>3</td><td>-9</td><td>6</td></tr></table>

15-42. In games (a) and (b) below, the payoff is for player $A$ . Determine the values of $p$ and $q$ that will make $\left( {{A}_{2},{B}_{2}}\right)$ a saddle point:

(a)

<table><tr><td></td><td>${B}_{1}$</td><td>${B}_{2}$</td><td>${B}_{3}$</td></tr><tr><td>${A}_{1}$</td><td>1</td><td>$q$</td><td>6</td></tr><tr><td>${A}_{2}$</td><td>$p$</td><td>5</td><td>10</td></tr><tr><td>${A}_{3}$</td><td>6</td><td>2</td><td>3</td></tr></table>

(b)

![bo_d56m58jef24c73bhe65g_40_960_298_297_257_0.jpg](bo_d56m58jef24c73bhe65g_40_960_298_297_257_0.jpg)

15-43. In the games below, the payoff is for player $A$ . Specify the range for the value of the game in each case.

![bo_d56m58jef24c73bhe65g_40_420_651_430_309_0.jpg](bo_d56m58jef24c73bhe65g_40_420_651_430_309_0.jpg)

(b) ${B}_{1}\;{B}_{2}\;{B}_{3}\;{B}_{4}$

${A}_{1}$ -1 9 6 8

${A}_{2}$ -2 10 4 6

${A}_{3}$ 5 3 0 7

${A}_{4}$ 7 -2 8 4

(c)

${B}_{1} \; {B}_{2} \; {B}_{3}$

${A}_{1}$ 3 6 1

${A}_{2}$ 5 2 3

${A}_{3}$ 4 2 -5

(d) ${B}_{1}\;{B}_{2}\;{B}_{3}\;{B}_{4}$

${A}_{1}$ 3 7 1 3

${A}_{2}$ 4 8 0 -6

${A}_{3}$ 6 -9 -2 4

15-44. Two companies promote two competing products. Currently, each product controls 50% of the market. Because of recent improvements in the two products, each company plans to launch an advertising campaign. If neither company advertises, equal market shares will continue. If either company launches a stronger campaign, the other company is certain to lose a proportional percentage of its customers. A survey of the market shows that 50% of potential customers can be reached through television, 30% through newspapers, and 20% through radio.

(a) Formulate the problem as a two-person zero-sum game, and determine the advertising media for each company.

(b) Determine a range for the value of the game. Can each company operate with a single pure strategy?

15-45. Let ${a}_{ij}$ be the $\left( {i, j}\right)$ th element of a payoff matrix with $m$ strategies for player $A$ and $n$ strategies for player $B$ . The payoff is for player $A$ . Prove that

$$
\mathop{\max }\limits_{i}\mathop{\min }\limits_{j}{a}_{ij} \leq  \mathop{\min }\limits_{i}\mathop{\max }\limits_{i}{a}_{ij}
$$

*15-46. Solve the coin-tossing game of Example 15.4-2 graphically. ${}^{8}$

*15-47. Robin travels between two cities and may use one of two routes: Route $A$ is a fast four-lane highway, and route $B$ is a long winding road. She has the habit of driving "superfast." The highway patrol has a limited police force. If the full force is allocated to the route driven by Robin, she is certain to receive a \$100 speeding fine. If the force is split 50-50 between the two routes, there is a 50% chance of getting a \$100 fine on route $A$ , and only a 30% chance of getting the same fine on route $B$ . Develop a strategy for both Robin and the police patrol.

15-48. Solve the following games graphically. The payoff is for Player $A$ .

(a)

${B}_{1} \; {B}_{2} \; {B}_{3}$ (b) ${B}_{1} \; {B}_{2}$

<table><tr><td>${A}_{1}$</td><td>5</td><td>8</td></tr><tr><td>${A}_{2}$</td><td>6</td><td>5</td></tr><tr><td>${A}_{3}$</td><td>5</td><td>7</td></tr></table>

${A}_{1}$ 2 -3 8

${A}_{2}$ 3 3 -6

15-49. Consider the following two-person, zero-sum game:

<table><tr><td></td><td>${B}_{1}$</td><td>${B}_{2}$</td><td>${B}_{3}$</td><td></td></tr><tr><td>${A}_{1}$</td><td>5</td><td>50</td><td>50</td><td></td></tr><tr><td>${A}_{2}$</td><td>1</td><td>1</td><td>.1</td><td></td></tr><tr><td>${A}_{3}$</td><td>10</td><td>1</td><td>10</td><td></td></tr></table>

(a) Verify that the strategies $\left( {\frac{1}{6},0,\frac{5}{6}}\right)$ for $A$ and $\left( {\frac{49}{54},\frac{5}{54},0}\right)$ for $B$ are optimal, and determine the value of the game.

(b) Show that the optimal value of the game equals

$$
\mathop{\sum }\limits_{{i = 1}}^{3}\mathop{\sum }\limits_{{j = 1}}^{3}{a}_{ij}{x}_{i}{y}_{j}
$$

15-50. On a picnic outing, 2 two-person teams are playing hide-and-seek. There are four hiding locations $\left( {A, B, C,\text{ and }D}\right)$ , and the two members of the hiding team can hide separately in any two of the four locations. The other team can then search any two locations. The searching team gets a bonus point if they find both members of the hiding team. If they miss both, they lose a point. Otherwise, the outcome is a draw.

*(a) Set up the problem as a two-person zero-sum game.

(b) Determine the optimal strategy and the value of the game.

15-51. UA and DU are devising their strategies for the 1994 national championship men's college basketball game. Assessing the strengths of their respective "benches," each coach comes up with four strategies for rotating the players during the game. The ability of each team to score 2-pointers, 3-pointers, and free throws is key to determining the final score of the game. The following table summarizes the net points UA will score per possession as a function of the different strategies available to each team:

<table><tr><td></td><td>${\mathrm{{DU}}}_{1}$</td><td>${\mathrm{{DU}}}_{2}$</td><td>${\mathrm{{DU}}}_{3}$</td><td>${\mathrm{{DU}}}_{4}$</td></tr><tr><td>${\mathrm{{UA}}}_{1}$</td><td>3</td><td>-2</td><td>1</td><td>4</td></tr><tr><td>${\mathrm{{UA}}}_{2}$</td><td>2</td><td>3</td><td>-5</td><td>0</td></tr><tr><td>${\mathrm{{UA}}}_{3}$</td><td>-1</td><td>2</td><td>-2</td><td>2</td></tr><tr><td>${\mathrm{{UA}}}_{4}$</td><td>-3</td><td>-5</td><td>4</td><td>1</td></tr></table>

(a) Solve the game by linear programming and determine a strategy for the championship game.

(b) Based on the given information, which of the two teams is projected to win the championship?

(c) Suppose that the entire game will have a total of 60 possessions (30 for each team). Predict the expected number of points by which the championship will be won.

15-52. Colonel Blotto's army is fighting for the control of two strategic locations. Blotto has two regiments and the enemy has three. A location will fall to the army with more regiments. Otherwise, the result of the battle is a draw.

*(a) Formulate the problem as a two-person zero-sum game, and solve by linear programming.

(b) Which army will win the battle?

15-53. In the two-player, two-finger Morra game, each player shows one or two fingers, and simultaneously guesses the number of fingers the opponent will show. The player making the correct guess wins an amount equal to the total number of fingers shown. Otherwise, the game is a draw. Set up the problem as a two-person zero-sum game, and solve by linear programming.

This page intentionally left blank