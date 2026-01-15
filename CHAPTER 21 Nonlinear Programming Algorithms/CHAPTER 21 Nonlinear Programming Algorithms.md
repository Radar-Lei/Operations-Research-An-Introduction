## CHAPTER 21 Nonlinear Programming Algorithms

### 21.1 UNCONSTRAINED ALGORITHMS

This section presents two types of algorithms for the unconstrained problem: direct search and gradient.

#### 21.1.1 Direct Search Method

Direct search methods apply primarily to strictly unimodal single-variable functions. Although the case may appear trivial, Section 21.1.2 shows that optimization of single-variable functions is key in the development of the more general multivariable algorithm.

The idea of direct search methods is to identify the interval of uncertainty known to include the optimum solution point. The procedure locates the optimum by iteratively narrowing the interval of uncertainty to a desired level of accuracy.

Two closely related search algorithms are presented in this section: dichotomous and golden section. Both algorithms seek the maximization of a unimodal function $f\left( x\right)$ over the interval $a \leq  x \leq  b$ that includes the optimum point $x$ *. The two methods start with the initial interval of uncertainty ${I}_{0} = \left( {a, b}\right)$ .

General step $i$ . Let ${I}_{i - 1} = \left( {{x}_{L},{x}_{R}}\right)$ be the current interval of uncertainty (at iteration $\left. {0,{x}_{L} = a\text{ and }{x}_{R} = b}\right)$ . The following table shows how ${x}_{1}$ and ${x}_{2}$ are determined:

<table><tr><td>Dichotomous method</td><td>Golden section method</td></tr><tr><td>${x}_{1} = \frac{1}{2}\left( {{x}_{R} + {x}_{L} - \Delta }\right)$</td><td>${x}_{1} = {x}_{R} - \left( \frac{\sqrt{5} - 1}{2}\right) \left( {{x}_{R} - {x}_{L}}\right)$</td></tr><tr><td>${x}_{2} = \frac{1}{2}\left( {{x}_{R} + {x}_{L} + \Delta }\right)$</td><td>${x}_{2} = {x}_{L} + \left( \frac{\sqrt{5} - 1}{2}\right) \left( {{x}_{R} - {x}_{L}}\right)$</td></tr></table>

The selection of ${x}_{1}$ and ${x}_{2}$ guarantees that ${x}_{L} < {x}_{1} < {x}_{2} < {x}_{R}$ .

![bo_d56m5qn7aajc73800nj0_1_356_199_1155_845_0.jpg](bo_d56m5qn7aajc73800nj0_1_356_199_1155_845_0.jpg)

FIGURE 21.1

Illustration of the general step of the dichotomous/golden section search method

The next interval of uncertainty, ${I}_{i}$ , is determined in the following manner:

1. If $f\left( {x}_{1}\right)  > f\left( {x}_{2}\right)$ , then ${x}_{L} < {x}^{ * } < {x}_{2}$ . Let ${x}_{R} = {x}_{2}$ and set ${I}_{i} = \left( {{x}_{L},{x}_{2}}\right)$ [see Figure 21.1(a)].

2. If $f\left( {x}_{1}\right)  < f\left( {x}_{2}\right)$ , then ${x}_{1} < {x}^{ * } < {x}_{R}$ . Let ${x}_{L} = {x}_{1}$ and set ${I}_{i} = \left( {{x}_{1},{x}_{R}}\right)$ [see Figure 21.1(b)].

3. If $f\left( {x}_{1}\right)  = f\left( {x}_{2}\right)$ , then ${x}_{1} < {x}^{ * } < {x}_{2}$ . Let ${x}_{L} = {x}_{1}$ and ${x}_{R} = {x}_{2}$ ; set ${I}_{i} = \left( {{x}_{1},{x}_{2}}\right)$ .

The manner in which ${x}_{1}$ and ${x}_{2}$ are determined guarantees that ${I}_{i + 1} < {I}_{i}$ , as will be shown shortly. The algorithm terminates at iteration $k$ if ${I}_{k} \leq  \Delta$ , where $\Delta$ is a user-specified level of accuracy.

In the dichotomous method, the values ${x}_{1}$ and ${x}_{2}$ sit symmetrically around the midpoint of the current interval of uncertainty. This means that

$$
{I}_{i + 1} = {.5}\left( {{I}_{i} + \Delta }\right)
$$

Repeated application of the algorithm guarantees that the length of the interval of uncertainty will approach the desired accuracy, $\Delta$ .

In the golden section method, the idea is more involved. We notice that each iteration of the dichotomous method requires calculating the two values $f\left( {x}_{1}\right)$ and $f\left( {x}_{2}\right)$ , but ends up discarding one of them. What the golden section method proposes is to save computations by reusing the discarded value in the immediately succeeding iteration.

Define

$$
\left. \begin{array}{l} {x}_{1} = {x}_{R} - \alpha \left( {{x}_{R} - {x}_{L}}\right) \\  {x}_{2} = {x}_{L} + \alpha \left( {{x}_{R} - {x}_{L}}\right)  \end{array}\right\}  0 < \alpha  < 1
$$

Then the interval of uncertainty ${I}_{i}$ at iteration $i$ equals $\left( {{x}_{L},{x}_{2}}\right)$ or $\left( {{x}_{1},{x}_{R}}\right)$ . Consider the case ${I}_{i} = \left( {{x}_{L},{x}_{2}}\right)$ , which means that ${x}_{1}$ is included in ${I}_{i}$ . In iteration $i + 1$ , we select ${x}_{2}$ equal to ${x}_{1}$ in iteration $i$ , which leads to the following equation:

$$
{x}_{2}\left( {\text{ iteration }i + 1}\right)  = {x}_{1}\left( {\text{ iteration }i}\right)
$$

Substitution yields

$$
{x}_{L} + \alpha \left\lbrack  {{x}_{2}\left( {\text{ iteration }i}\right)  - {x}_{L}}\right\rbrack   = {x}_{R} - \alpha \left( {{x}_{R} - {x}_{L}}\right)
$$

or

$$
{x}_{L} + \alpha \left\lbrack  {{x}_{L} + \alpha \left( {{x}_{R} - {x}_{L}}\right)  - {x}_{L}}\right\rbrack   = {x}_{R} - \alpha \left( {{x}_{R} - {x}_{L}}\right)
$$

which simplifies to

$$
{\alpha }^{2} + \alpha  - 1 = 0
$$

This equation yields $\alpha  = \frac{-1 \pm  \sqrt{5}}{2}$ . The positive root $\alpha  = \frac{-1 + \sqrt{5}}{2} \approx  {.681}$ is selected because $0 < \alpha  < 1$ .

The design of the golden section computations guarantees an $\alpha$ -reduction in the successive intervals of uncertainty - that is

$$
{I}_{i + 1} = \alpha {I}_{i}
$$

The golden section method converges more rapidly than the dichotomous method because, in the dichotomous method, the narrowing of the interval of uncertainty slows down appreciably as $I \rightarrow  \Delta$ . In addition, the golden section method requires half the computations because it recycles one set of computations from the immediately preceding iteration.

Example 21.1-1

$$
\text{ Maximize }f\left( x\right)  = \left\{  \begin{array}{ll} {3x}, & 0 \leq  x \leq  2 \\  \frac{1}{3}\left( {-x + {20}}\right) , & 2 \leq  x \leq  3 \end{array}\right.
$$

The maximum value of $f\left( x\right)$ occurs at $x = 2$ . The following table demonstrates the calculations for iterations 1 and 2 using the dichotomous and the golden section methods, with $\Delta  = {.1}$ .

766 Chapter 21 Nonlinear Programming Algorithms

<table><tr><td>Dichotomous method</td><td>Golden section method</td></tr><tr><td>Iteration 1 <br> ${I}_{0} = \left( {0,3}\right)  \equiv  \left( {{x}_{L},{x}_{R}}\right)$ <br> ${x}_{1} = 0 + {.5}\left( {3 - 0 - {.1}}\right)  = {1.45}, f\left( {x}_{1}\right)  = {4.35}$ <br> ${x}_{2} = 0 + {.5}\left( {3 - 0 + {.1}}\right)  = {1.55}, f\left( {x}_{2}\right)  = {4.65}$ <br> $f\left( {x}_{2}\right)  > f\left( {x}_{1}\right)  \Rightarrow  {x}_{L} = {1.45},{I}_{1} = \left( {{1.45},3}\right)$</td><td>Iteration 1 <br> ${I}_{0} = \left( {0,3}\right)  \equiv  \left( {{x}_{L},{x}_{R}}\right)$ <br> ${x}_{1} = 3 - {.618}\left( {3 - 0}\right)  = {1.146}, f\left( {x}_{1}\right)  = {3.438}$ <br> ${x}_{2} = 0 + {.618}\left( {3 - 0}\right)  = {1.854}, f\left( {x}_{2}\right)  = {5.562}$ <br> $f\left( {x}_{2}\right)  > f\left( {x}_{1}\right)  \Rightarrow  {x}_{L} = {1.146},{I}_{1} = \left( {{1.146},3}\right)$</td></tr><tr><td>Iteration 2 <br> ${I}_{1} = \left( {{1.45},3}\right)  \equiv  \left( {{x}_{L},{x}_{R}}\right)$ <br> ${x}_{1} = {1.45} + {.5}\left( {3 - {1.45} - {.1}}\right)  = {2.175}, f\left( {x}_{1}\right)  = {5.942}$ <br> ${x}_{2} = \frac{3 + {1.45} + {.1}}{2} = {2.275}, f\left( {x}_{2}\right)  = {5.908}$ <br> $f\left( {x}_{1}\right)  > f\left( {x}_{2}\right)  \Rightarrow  {x}_{R} = {2.275},{I}_{2} = \left( {{1.45},{2.275}}\right)$</td><td>Iteration 2 <br> ${I}_{1} = \left( {{1.146},3}\right)  \equiv  \left( {{x}_{L},{x}_{R}}\right)$ <br> ${x}_{1} = {x}_{2}$ in iteratoin $0 = {1.854}, f\left( {x}_{1}\right)  = {5.562}$ <br> ${x}_{2} = {1.146} + {.618}\left( {3 - {1.146}}\right)  = {2.292}, f\left( {x}_{2}\right)  = {5.903}$ <br> $f\left( {x}_{2}\right)  > f\left( {x}_{1}\right)  \Rightarrow  {x}_{L} = {1.854},{I}_{2} = \left( {{1.854},3}\right)$</td></tr></table>

Continuing in the same manner, the interval of uncertainty will eventually narrow down to the desired $\Delta$ -tolerance.

## Excel Moment

Excel template excelDiGold.xls handles both methods by entering the letter X in either D5 (dichotomous) or F5 (golden section). The input data include $f\left( x\right) , a, b$ , and $\Delta$ . The function $f\left( x\right)$ is entered in cell E3 as

$$
= \operatorname{IF}\left( {\mathrm{C}3 <  = 2,3 * \mathrm{C}3,\left( {-\mathrm{C}3 + {20}}\right) /3}\right)
$$

Cell C3 plays the role of $x$ in $f\left( x\right)$ .

Figure 21.2 compares the two methods. The golden section method requires less than half the iterations of the dichotomous method, in addition to half the calculations at each iteration.

#### 21.1.2 Gradient Method

This section develops a method for optimizing twice continuously differentiable functions, called the steepest ascent method. The idea is to generate successive points in the direction of the gradient of the function. ${}^{1}$ Termination of the gradient method occurs at the point where the gradient vector becomes null. This is only a necessary condition for optimality.

Suppose that $f\left( \mathbf{X}\right)$ is maximized. Let ${\mathbf{X}}_{0}$ be the initial point from which the procedure starts, and define $\nabla f\left( {\mathbf{X}}_{k}\right)$ as the gradient of $f$ at point ${\mathbf{X}}_{k}$ . The idea is to determine a particular path $p$ along which $\frac{\partial f}{\partial p}$ is maximized at a given point. This result is achieved if successive points ${\mathbf{X}}_{k}$ and ${\mathbf{X}}_{k + 1}$ are selected such that

$$
{\mathbf{X}}_{k + 1} = {\mathbf{X}}_{k} + {r}_{k}\nabla f\left( {\mathbf{X}}_{k}\right)
$$

where ${r}_{k}$ is the optimal step size at ${\mathbf{X}}_{k}$ .

---

${}^{1}$ The Newton-Raphson method in Section 20.1.2 is also a gradient method that locates the optimum indirectly by solving the necessary conditions equations.

---

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td></tr><tr><td>1</td><td colspan="6">Dichotomous/Golden Section Search</td></tr><tr><td>2</td><td colspan="6">Input data: Type f(C3) in E3, where C3 represents x in f(x)</td></tr><tr><td>3</td><td>$\Delta  =$</td><td>0.1</td><td>C3</td><td></td><td>#VALUE!</td><td rowspan="2">Clear Calculations</td></tr><tr><td>4</td><td>Minimum x =</td><td>0</td><td>Maximum x =</td><td>3</td><td></td></tr><tr><td>5</td><td>Solution:</td><td>Enter x to select></td><td>Dichotomous:</td><td>X</td><td>GoldenSection:</td><td></td></tr><tr><td>6</td><td>${x}^{ * } =$</td><td>2.04001</td><td>$f\left( {x}^{ * }\right)  =$</td><td>5.97002</td><td colspan="2"></td></tr><tr><td>7</td><td colspan="4">Clalculations:</td><td colspan="2">Perform calculation</td></tr><tr><td>8</td><td>xL</td><td>xR</td><td>x1</td><td>x2</td><td>f(x1)</td><td>f(x2)</td></tr><tr><td>9</td><td>0.000000</td><td>3.000000</td><td>1.450000</td><td>1.550000</td><td>4.350000</td><td>4.650000</td></tr><tr><td>10</td><td>1.450000</td><td>3.000000</td><td>2.175000</td><td>2.275000</td><td>5.941667</td><td>5.908333</td></tr><tr><td>11</td><td>1.450000</td><td>2.275000</td><td>1.812500</td><td>1.912500</td><td>5.437500</td><td>5.737500</td></tr><tr><td>12</td><td>1.812500</td><td>2.275000</td><td>1.993750</td><td>2.093750</td><td>5.981250</td><td>5.968750</td></tr><tr><td>13</td><td>1.812500</td><td>2.093750</td><td>1.903125</td><td>2.003125</td><td>5.709375</td><td>5.998958</td></tr><tr><td>14</td><td>1.903125</td><td>2.093750</td><td>1.948438</td><td>2.048438</td><td>5.845313</td><td>5.983854</td></tr><tr><td>15</td><td>1.948438</td><td>2.093750</td><td>1.971094</td><td>2.071094</td><td>5.913281</td><td>5.976302</td></tr><tr><td>16</td><td>1.971094</td><td>2.093750</td><td>1.982422</td><td>2.082422</td><td>5.947266</td><td>5.972526</td></tr><tr><td>17</td><td>1.982422</td><td>2.093750</td><td>1.988086</td><td>2.088086</td><td>5.964258</td><td>5.970638</td></tr><tr><td>18</td><td>1.988086</td><td>2.093750</td><td>1.990918</td><td>2.090918</td><td>5.972754</td><td>5.969694</td></tr><tr><td>19</td><td>1.988086</td><td>2.090918</td><td>1.989502</td><td>2.089502</td><td>5.968506</td><td>5.970166</td></tr><tr><td>20</td><td>1.989502</td><td>2.090918</td><td>1.990210</td><td>2.090210</td><td>5.970630</td><td>5.969930</td></tr><tr><td>21</td><td>1.989502</td><td>2.090210</td><td>1.989856</td><td>2.089856</td><td>5.969568</td><td>5.970048</td></tr><tr><td>22</td><td>1.989856</td><td>2.090210</td><td>1.990033</td><td>2.090033</td><td>5.970099</td><td>5.969989</td></tr><tr><td>23</td><td>1.989856</td><td>2.090033</td><td>1.989944</td><td>2.089944</td><td>5.969833</td><td>5.970019</td></tr><tr><td>24</td><td>1.989944</td><td>2.090033</td><td>1.989989</td><td>2.089989</td><td>5.969966</td><td>5.970004</td></tr><tr><td>25</td><td>1.989989</td><td>2.090031</td><td>1.990011</td><td>2.090011</td><td>5.970033</td><td>5.969996</td></tr><tr><td>26</td><td>1.989989</td><td>2.090011</td><td>1.990000</td><td>2.090000</td><td>5.969999</td><td>5.970000</td></tr><tr><td>27</td><td>1.990000</td><td>2.090011</td><td>1.990005</td><td>2.090005</td><td>5.970016</td><td>5.969998</td></tr><tr><td>28</td><td>1.990000</td><td>2.090005</td><td>1.990003</td><td>2.090003</td><td>5.970008</td><td>5.969999</td></tr><tr><td>5</td><td>Solution:</td><td>Enter x to select></td><td>Dichotomous:</td><td></td><td>GoldenSection:</td><td>X</td></tr><tr><td>6</td><td>x* =</td><td>2.00909</td><td>f(x*) =</td><td>5.99290</td><td colspan="2"></td></tr><tr><td>7</td><td colspan="6">Clalculations: Perform calculation</td></tr><tr><td>8</td><td>xL</td><td>xR</td><td>x1</td><td>x2</td><td>f(x1)</td><td>f(x2)</td></tr><tr><td>9</td><td>0.000000</td><td>3.000000</td><td>1.145898</td><td>1.854102</td><td>3.437694</td><td>5.562306</td></tr><tr><td>10</td><td>1.145898</td><td>3.000000</td><td>1.854102</td><td>2.291796</td><td>5.562306</td><td>5.902735</td></tr><tr><td>11</td><td>1.854102</td><td>3.000000</td><td>2.291796</td><td>2.562306</td><td>5.902735</td><td>5.812565</td></tr><tr><td>12</td><td>1.854102</td><td>2.562306</td><td>2.124612</td><td>2.291796</td><td>5.958463</td><td>5.902735</td></tr><tr><td>13</td><td>1.854102</td><td>2.291796</td><td>2.021286</td><td>2.124612</td><td>5.992905</td><td>5.958463</td></tr><tr><td>14</td><td>1.854102</td><td>2.124612</td><td>1.957428</td><td>2.021286</td><td>5.872283</td><td>5.992905</td></tr><tr><td>15</td><td>1.957428</td><td>2.124612</td><td>2.021286</td><td>2.060753</td><td>5.992905</td><td>5.979749</td></tr><tr><td>16</td><td>1.957428</td><td>2.060753</td><td>1.996894</td><td>2.021286</td><td>5.990683</td><td>5.992905</td></tr><tr><td>17</td><td>1.996894</td><td>2.060753</td><td>2.021286</td><td>2.036361</td><td>5.992905</td><td>5.987880</td></tr></table>

FIGURE 21.2

Excel output of the dichotomous and golden section methods applied to Example 21.1-1 (file excelDiGold.xls)

The step size ${r}_{k}$ is determined such that the next point, ${\mathbf{X}}_{k + 1}$ , leads to the largest improvement in $f$ . This is equivalent to determining $r = {r}_{k}$ that maximizes the function

$$
h\left( r\right)  = f\left\lbrack  {{\mathbf{X}}_{k} + r\nabla f\left( {\mathbf{X}}_{k}\right) }\right\rbrack
$$

Because $h\left( r\right)$ is a single-variable function, the search method in Section 21.1.1 may be used to find the optimum, provided that $h\left( r\right)$ is unimodal.

The proposed procedure terminates when two successive trial points ${\mathbf{X}}_{k}$ and ${\mathbf{X}}_{k + 1}$ are approximately equal. This is equivalent to having ${r}_{k}\nabla f\left( {\mathbf{X}}_{k}\right)  \approx  \mathbf{0}$ , or, equivalently, $\nabla f\left( {\mathbf{X}}_{k}\right)  \approx  \mathbf{0}.$

## Example 21.1-2

Consider the following problem:

$$
\text{ Maximize }f\left( {{x}_{1},{x}_{2}}\right)  = 4{x}_{1} + 6{x}_{2} - 2{x}_{1}^{2} - 2{x}_{1}{x}_{2} - 2{x}_{2}^{2}
$$

The exact optimum occurs at $\left( {{x}_{1}^{ * },{x}_{2}^{ * }}\right)  = \left( {\frac{1}{3},\frac{4}{3}}\right)$ .

The gradient of $f$ is

$$
\nabla f\left( \mathbf{X}\right)  = \left( {4 - 4{x}_{1} - 2{x}_{2},6 - 2{x}_{1} - 4{x}_{2}}\right)
$$

The quadratic nature of the function indicates that the gradients at two successive points are orthogonal (perpendicular to one another).

Suppose that we start at the initial point ${\mathbf{X}}_{0} = \left( {1,1}\right)$ . Figure 21.3 shows the successive solution points.

Iteration 1

$$
\nabla f\left( {\mathbf{X}}_{0}\right)  = \left( {-2,0}\right)
$$

The next point ${\mathbf{X}}_{1}$ is obtained by considering

$$
\mathbf{X} = \left( {1,1}\right)  + r\left( {-2,0}\right)  = \left( {1 - {2r},1}\right)
$$

Thus,

$$
h\left( r\right)  = f\left( {1 - {2r},1}\right)  =  - 2{\left( 1 - 2r\right) }^{2} + 2\left( {1 - {2r}}\right)  + 4
$$

FIGURE 21.3

Maximization of $f\left( {{x}_{1},{x}_{2}}\right)  = 4{x}_{1} + 6{x}_{2} - 2{x}_{1}^{2} - 2{x}_{1}{x}_{2} - 2{x}_{2}^{2}$ by the steepest-ascent method

![bo_d56m5qn7aajc73800nj0_5_516_1323_834_840_0.jpg](bo_d56m5qn7aajc73800nj0_5_516_1323_834_840_0.jpg)

The optimal step size is obtained using the classical necessary conditions in Chapter 20 (you may also use the search algorithms in Section 21.1.1 to determine the optimum). The maximum value of $h\left( r\right)$ is ${r}_{1} = \frac{1}{4}$ , which yields the next solution point ${\mathbf{X}}_{1} = \left( {\frac{1}{2},1}\right)$ .

Iteration 2

$$
\nabla f\left( {\mathbf{X}}_{1}\right)  = \left( {0,1}\right)
$$

$$
\mathbf{X} = \left( {\frac{1}{2},1}\right)  + r\left( {0,1}\right)  = \left( {\frac{1}{2},1 + r}\right)
$$

$$
h\left( r\right)  =  - 2{\left( 1 + r\right) }^{2} + 5\left( {1 + r}\right)  + \frac{3}{2}
$$

Thus, ${r}_{2} = \frac{1}{4}$ and ${\mathbf{X}}_{2} = \left( {\frac{1}{2},\frac{5}{4}}\right)$ .

Iteration 3

$$
\nabla f\left( {\mathbf{X}}_{2}\right)  = \left( {-\frac{1}{2},0}\right)
$$

$$
\mathbf{X} = \left( {\frac{1}{2},\frac{5}{4}}\right)  + r\left( {-\frac{1}{2},0}\right)  = \left( {\frac{1 - r}{2},\frac{5}{4}}\right)
$$

$$
h\left( r\right)  =  - \frac{1}{2}{\left( 1 - r\right) }^{2} + \frac{3}{4}\left( {1 - r}\right)  + \frac{35}{8}
$$

Hence, ${r}_{3} = \frac{1}{4}$ and ${\mathbf{X}}_{3} = \left( {\frac{3}{8},\frac{5}{4}}\right)$ .

Iteration 4

$$
\nabla f\left( {\mathbf{X}}_{3}\right)  = \left( {0,\frac{1}{4}}\right)
$$

$$
\mathbf{X} = \left( {\frac{3}{8},\frac{5}{4}}\right)  + r\left( {0,\frac{1}{4}}\right)  = \left( {\frac{3}{8},\frac{5 + r}{4}}\right)
$$

$$
h\left( r\right)  =  - \frac{1}{8}{\left( 5 + r\right) }^{2} + \frac{21}{16}\left( {5 + r}\right)  + \frac{39}{32}
$$

Thus, ${r}_{4} = \frac{1}{4}$ and ${\mathbf{X}}_{4} = \left( {\frac{3}{8},\frac{21}{16}}\right)$ .

Iteration 5

$$
\nabla f\left( {\mathbf{X}}_{4}\right)  = \left( {-\frac{1}{8},0}\right)
$$

$$
\mathbf{X} = \left( {\frac{3}{8},\frac{21}{16}}\right)  + r\left( {-\frac{1}{8},0}\right)  = \left( {\frac{3 - r}{8},\frac{21}{16}}\right)
$$

$$
h\left( r\right)  =  - \frac{1}{32}{\left( 3 - r\right) }^{2} + \frac{11}{64}\left( {3 - r}\right)  + \frac{567}{128}
$$

This gives ${r}_{5} = \frac{1}{4}$ and ${\mathbf{X}}_{5} = \left( {\frac{11}{32},\frac{21}{16}}\right)$ .

Iteration 6

$$
\nabla f\left( {\mathbf{X}}_{5}\right)  = \left( {0,\frac{1}{16}}\right)
$$

The process can be terminated at this point because $\nabla f\left( {\mathbf{X}}_{5}\right)  \approx  \mathbf{0}$ . The approximate maximum point is given by ${\mathbf{X}}_{5} = \left( {{.3438},{1.3125}}\right)$ . The exact optimum is ${\mathbf{X}}^{ * } = \left( {{.3333},{1.3333}}\right)$ .

### 21.2 CONSTRAINED ALGORITHMS

The general constrained nonlinear programming problem is defined as

$$
\text{ Maximize (or minimize) }z = f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}
$$

The nonnegativity conditions, $\mathbf{X} \geq  \mathbf{0}$ , are part of the constraints. Also, at least one of the functions $f\left( \mathbf{X}\right)$ and $\mathbf{g}\left( \mathbf{X}\right)$ is nonlinear, and all the functions are continuously differentiable.

The erratic behavior of the nonlinear functions precludes the development of a single algorithm for the general nonlinear model. Perhaps the most general result applicable to the problem is the KKT conditions (Section 20.2.2). Table 20.2 shows that the KKT conditions are only necessary, unless $f\left( \mathbf{X}\right)$ and $\mathbf{g}\left( \mathbf{X}\right)$ are well-behaved functions.

This section presents a number of algorithms that may be classified generally as indirect and direct methods. Indirect methods solve the nonlinear problem by dealing with one or more linear programs derived from the original program. Direct methods deal with the original problem.

The indirect algorithms presented in this section include separable, quadratic, and chance-constrained programming. The direct algorithms include the method of linear combinations and a brief discussion of SUMT (sequential unconstrained maximization technique). Other important nonlinear techniques can be found in the list of references at the end of the chapter.

#### 21.2.1 Separable Programming

A function $f\left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)$ is separable if it can be expressed as the sum of $n$ single-variable functions ${f}_{1}\left( {x}_{1}\right) ,{f}_{2}\left( {x}_{2}\right) ,\ldots ,{f}_{n}\left( {x}_{n}\right)$ -that is,

$$
f\left( {{x}_{1},{x}_{1,}\ldots ,{x}_{n}}\right)  = {f}_{1}\left( {x}_{1}\right)  + {f}_{2}\left( {x}_{2}\right)  + \cdots  + {f}_{n}\left( {x}_{n}\right)
$$

For example, any linear function is separable. On the other hand, the function

$$
h\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = {x}_{1}^{2} + {x}_{1}\sin \left( {{x}_{2} + {x}_{3}}\right)  + {x}_{2}{e}^{x3}
$$

is not separable.

Some (convoluted) nonlinear functions can be made separable using appropriate substitutions. Consider, for example, the case of maximizing $z = {x}_{1}{x}_{2}$ . Let $y = {x}_{1}{x}_{2}$ , then $\ln y = \ln {x}_{1} + \ln {x}_{2}$ , and the equivalent separable problem is

$$
\text{ Maximize }z = y
$$

subject to

$$
\ln y = \ln {x}_{1} + \ln {x}_{2}
$$

The substitution assumes that ${x}_{1}$ and ${x}_{2}$ are positive variables because the logarithmic function is undefined for nonpositive values. We can account for the case where ${x}_{1}$ and ${x}_{2}$ can assume zero values by employing the approximations

$$
{w}_{1} = {x}_{1} + {\delta }_{1} > 0
$$

$$
{w}_{2} = {x}_{2} + {\delta }_{2} > 0
$$

The constants ${\delta }_{1}$ and ${\delta }_{2}$ are very small positive values.

This section shows how an approximate solution can be obtained for any separable problem by using linear approximation and the simplex method of linear programming. The single-variable function $f\left( x\right)$ can be approximated by a piecewise-linear function using mixed integer programming (Chapter 9). Suppose that $f\left( x\right)$ is approximated over an interval $\left\lbrack  {a, b}\right\rbrack$ , and define ${a}_{k}, k = 1,2,\ldots , K$ , as the $k$ th breakpoint on the $x$ -axis such that ${a}_{1} < {a}_{2} < \ldots  < {a}_{K}$ . The points ${a}_{1}$ and ${a}_{K}$ coincide with end points $a$ and $b$ of the designated interval. Thus, $f\left( x\right)$ is approximated as

$$
f\left( x\right)  \approx  \mathop{\sum }\limits_{{k = 1}}^{K}f\left( {a}_{k}\right) {w}_{k}
$$

$$
x = \mathop{\sum }\limits_{{k = 1}}^{K}{a}_{k}{w}_{k}
$$

The nonnegative weights ${w}_{k}$ must satisfy the condition

$$
\mathop{\sum }\limits_{{k = 1}}^{K}{w}_{k} = 1,{w}_{k} \geq  0, k = 1,2,\ldots , K
$$

Mixed integer programming ensures the validity of the approximation by imposing two additional conditions:

1. At most two ${w}_{k}$ are positive.

2. If ${w}_{k}$ is positive, then only an adjacent ${w}_{k + 1}$ or ${w}_{k - 1}$ can assume a positive value.

To show how these conditions are satisfied, consider the separable problem

$$
\text{ Maximize (or minimize) }z = \mathop{\sum }\limits_{{j = 1}}^{n}{f}_{j}\left( {x}_{j}\right)
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{g}_{ij}\left( {x}_{j}\right)  \leq  {b}_{i}, i = 1,2,\ldots , m
$$

This problem can be approximated by a mixed integer program as follows. Let ${}^{2}$

$$
\left. \begin{array}{l} {a}_{jk} = \text{ breakpoint }k\text{ for variable }{x}_{j} \\  {w}_{jk} = \text{ weight with breakpoint }k\text{ of variable }{x}_{j} \end{array}\right\}  k = 1,2,\ldots ,{K}_{j}, j = 1,2,\ldots , n
$$

Then the equivalent mixed problem is

$$
\text{ Maximize (or minimize) }z = \mathop{\sum }\limits_{{j = 1}}^{n}\mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{f}_{j}\left( {a}_{jk}\right) {w}_{jk}
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}\mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{g}_{jk}\left( {a}_{jk}\right) {w}_{jk} \leq  {b}_{i},\;i = 1,2,\ldots , m
$$

$$
0 \leq  {w}_{j1} \leq  {y}_{j1},\;j = 1,2,\ldots , n
$$

$$
0 \leq  {w}_{jk} \leq  {y}_{j, k - 1} + {y}_{jk},\;k = 2,3,\ldots ,{K}_{j} - 1, j = 1,2,\ldots , n
$$

$$
0 \leq  {w}_{j{K}_{j}} \leq  {y}_{j,{K}_{j} - 1},\;j = 1,2,\ldots , n
$$

$$
\mathop{\sum }\limits_{{k = 1}}^{{{K}_{j} - 1}}{y}_{jk} = 1,\;j = 1,2,\ldots , n
$$

$$
\mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{w}_{jk} = 1,\;j = 1,2,\ldots , n
$$

$$
{y}_{jk} = \left( {0,1}\right) ,\;k = 1,2,\ldots ,{K}_{j}, j = 1,2,\ldots , n
$$

---

${}^{2}$ It is more accurate to replace the index $k$ with ${k}_{j}$ to correspond uniquely to variable $j$ . In this instant, we will forsake mathematical accuracy for a simpler notation.

---

The variables in the approximation problem are ${w}_{jk}$ and ${y}_{jk}$ .

The formulation shows how any separable problem can be solved, in principle, by mixed integer programming. The difficulty is that the number of constraints increases rather rapidly with the number of breakpoints. In particular, the computational feasibility of the procedure is questionable because there are no consistently reliable computer codes for solving large mixed integer programming problems.

Another method for solving the approximation model is the regular simplex method (Chapter 3) using restricted basis. In this case, the additional constraints involving ${y}_{jk}$ are dropped. The restricted basis modifies the simplex method optimality condition by selecting the entering variable ${w}_{j}$ with the best $\left( {{z}_{jk} - {c}_{jk}}\right)$ that does not violate the adjacency requirement of the $w$ -variables with positive values. The process is repeated until the optimality condition is satisfied or until it is impossible to satisfy the restricted basis condition, whichever occurs first.

The mixed integer programming method yields a global optimum to the approximate problem, whereas the restricted basis method can only guarantee a local optimum. Additionally, in the two methods, the approximate solution may not be feasible for the original problem, in which case it may be necessary to refine the approximation by increasing the number of breakpoints.

## Example 21.2-1

---

Consider the problem

$$
\text{ Maximize }z = {x}_{1} + {x}_{2}^{4}
$$

subject to

$$
3{x}_{1} + 2{x}_{2}^{2} \leq  9
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

---

The exact optimum solution to this problem, obtained by AMPL or Solver, is ${x}_{1} = 0$ , ${x}_{2} = {2.12132}$ , and ${z}^{ * } = {20.25}$ . To show how the approximating method is used, consider the separable functions

$$
{f}_{1}\left( {x}_{1}\right)  = {x}_{1}
$$

$$
{f}_{2}\left( {x}_{2}\right)  = {x}_{2}^{4}
$$

$$
{g}_{1}\left( {x}_{1}\right)  = 3{x}_{1}
$$

$$
{g}_{2}\left( {x}_{2}\right)  = 2{x}_{2}^{2}
$$

The variable ${x}_{1}$ is not approximated because the functions ${f}_{1}\left( {x}_{1}\right)$ and ${g}_{1}\left( {x}_{1}\right)$ are already linear. Considering ${f}_{2}\left( {x}_{2}\right)$ and ${g}_{2}\left( {x}_{2}\right)$ , we assume four breakpoints: ${a}_{2k} = 0,1,2$ , and 3 for $k = 1,2,3$ , and 4, respectively. Given ${x}_{2} \leq  3$ , it follows that

<table><tr><td>$k$</td><td>${a}_{2k}$</td><td>${f}_{2}\left( {a}_{2k}\right)  = {a}_{2k}^{4}$</td><td>${g}_{2}\left( {a}_{2k}\right)  = 2{a}_{2k}^{2}$</td></tr><tr><td>1</td><td>0</td><td>0</td><td>0</td></tr><tr><td>2</td><td>1</td><td>1</td><td>2</td></tr><tr><td>3</td><td>2</td><td>16</td><td>8</td></tr><tr><td>4</td><td>3</td><td>81</td><td>18</td></tr></table>

Thus

$$
{f}_{2}\left( {x}_{2}\right)  \approx  {w}_{21}{f}_{2}\left( {a}_{21}\right)  + {w}_{22}{f}_{2}\left( {a}_{22}\right)  + {w}_{23}{f}_{2}\left( {a}_{23}\right)  + {w}_{24}{f}_{2}\left( {a}_{24}\right)
$$

$$
\approx  0{w}_{21} + 1{w}_{22} + {16}{w}_{23} + {81}{w}_{24} = {w}_{22} + {16}{w}_{23} + {81}{w}_{24}
$$

Similarly,

$$
{g}_{2}\left( {x}_{2}\right)  \approx  2{w}_{22} + 8{w}_{23} + {18}{w}_{24}
$$

The approximation problem thus becomes

$$
\text{ Maximize }z = {x}_{1} + {w}_{22} + {16}{w}_{23} + {81}{w}_{24}
$$

subject to

$$
3{x}_{1} + 2{w}_{22} + 8{w}_{23} + {18}{w}_{24} \leq  9
$$

$$
{w}_{21} + {w}_{22} + {w}_{23} + {w}_{24} = 1
$$

$$
{x}_{1} \geq  0,{w}_{2k} \geq  0, k = 1,2,3,4
$$

The values of ${w}_{2k}, k = 1,2,3,4$ , must satisfy the restricted basis condition.

The initial simplex tableau (with rearranged columns to provide a starting solution) is given by

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${w}_{22}$</td><td>${w}_{23}$</td><td>${w}_{24}$</td><td>${s}_{1}$</td><td>${w}_{21}$</td><td>Solution</td></tr><tr><td>$z$</td><td>-1</td><td>-1</td><td>-16</td><td>-81</td><td>0</td><td>0</td><td>0</td></tr><tr><td>${s}_{1}$</td><td>3</td><td>2</td><td>8</td><td>18</td><td>1</td><td>0</td><td>9</td></tr><tr><td>${w}_{21}$</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td></tr></table>

The variable ${s}_{1}\left( { \geq  0}\right)$ is a slack. (This problem happened to have an obvious starting solution. In general, one can use artificial variables, as presented in Section 3.4.)

From the $z$ -row, ${w}_{24}$ is the entering variable. Because ${w}_{21}$ is currently basic and positive, the restricted basis condition dictates that it must leave before ${w}_{24}$ can enter the solution. However, by the feasibility condition, ${s}_{1}$ must be the leaving variable, which means that ${w}_{24}$ cannot enter the solution. The next-best entering variable, ${w}_{23}$ , requires ${w}_{21}$ to leave the basic solution, a condition that happens to be satisfied by the feasibility condition. The new tableau thus becomes

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${w}_{22}$</td><td>${w}_{23}$</td><td>${w}_{24}$</td><td>${s}_{1}$</td><td>${w}_{21}$</td><td>Solution</td></tr><tr><td>$z$</td><td>-1</td><td>15</td><td>0</td><td>-65</td><td>0</td><td>16</td><td>16</td></tr><tr><td>${s}_{1}$</td><td>3</td><td>-6</td><td>0</td><td>10</td><td>1</td><td>-8</td><td>1</td></tr><tr><td>${w}_{23}$</td><td>0</td><td>1</td><td>1</td><td>1</td><td>0</td><td>1</td><td>1</td></tr></table>

Next, ${w}_{24}$ is the entering variable, which is admissible because ${w}_{23}$ is positive. The simplex method shows that ${s}_{1}$ will leave. Thus,

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${w}_{22}$</td><td>${w}_{23}$</td><td>${w}_{24}$</td><td>${s}_{1}$</td><td>${w}_{21}$</td><td>Solution</td></tr><tr><td>$z$</td><td>$\frac{37}{2}$</td><td>-24</td><td>0</td><td>0</td><td>$\frac{13}{2}$</td><td>-36</td><td>${22}\frac{1}{2}$</td></tr><tr><td>${w}_{24}$</td><td>$\frac{3}{10}$</td><td>$- \frac{6}{10}$</td><td>0</td><td>1</td><td>$\frac{1}{10}$</td><td>$- \frac{8}{10}$</td><td>$\frac{1}{10}$</td></tr><tr><td>${w}_{23}$</td><td>$- \frac{3}{10}$</td><td>$\frac{16}{10}$</td><td>1</td><td>0</td><td>$- \frac{1}{10}$</td><td>$\frac{18}{10}$</td><td>$\frac{9}{10}$</td></tr></table>

The tableau shows that ${w}_{21}$ and ${w}_{22}$ are candidates for the entering variable. The variable ${w}_{21}$ is not adjacent to basic ${w}_{23}$ or ${w}_{24}$ , hence it cannot become basic. Similarly, ${w}_{22}$ cannot enter because ${w}_{24}$ cannot leave. Thus, the last tableau is the best restricted-basis solution for the approximate problem.

The optimum solution to the original problem is

$$
{x}_{1} = 0
$$

$$
{x}_{2} \approx  2{w}_{23} + 3{w}_{24} = 2\left( \frac{9}{10}\right)  + 3\left( \frac{1}{10}\right)  = {2.1}
$$

$$
z = 0 + {2.1}^{4} = {19.45}
$$

The value ${x}_{2} = {2.1}$ approximately equals the true optimum value $\left( { = {2.12132}}\right)$ .

Separable convex programming. A special case of separable programming occurs when ${g}_{ij}\left( {x}_{j}\right)$ is convex for all $i$ and $j$ , which ensures a convex solution space. Additionally, if ${f}_{j}\left( {x}_{j}\right)$ is convex (minimization) or concave (maximization) for all $j$ , then the problem has a global optimum (see Table 20.2, Section 20.2.2). Under such conditions, the following simplified approximation can be used.

Consider a minimization problem, and let ${f}_{j}\left( {x}_{j}\right)$ be as shown in Figure 21.4. The breakpoints of the function ${f}_{j}\left( {x}_{j}\right)$ are ${x}_{j} = {a}_{jk}, k = 0,1,\ldots ,{K}_{j}$ . Let ${x}_{jk}$ define the increment of the variable ${x}_{j}$ in the range $\left( {{a}_{j, k - 1},{a}_{jk}}\right) , k = 1,2,\ldots ,{K}_{j}$ , and let ${r}_{jk}$ be the corresponding rate of change (slope of the line segment) in the same range. Then

$$
{f}_{j}\left( {x}_{j}\right)  \approx  \mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{r}_{jk}{x}_{jk} + {f}_{j}\left( {a}_{j0}\right)
$$

$$
{x}_{j} = \mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{x}_{jk}
$$

$$
0 \leq  {x}_{jk} \leq  {a}_{jk} - {a}_{j, k - 1}, k = 1,2,\ldots ,{K}_{j}
$$

![bo_d56m5qn7aajc73800nj0_12_360_200_651_391_0.jpg](bo_d56m5qn7aajc73800nj0_12_360_200_651_391_0.jpg)

FIGURE 21.4

Piecewise-linear approximation of a convex function

The fact that ${f}_{j}\left( {x}_{j}\right)$ is convex ensures that ${r}_{j1} < {r}_{j2} < \cdots  < {r}_{j{K}_{i}}$ . This means that in the minimization problem the variable ${x}_{jp}$ is more attractive than ${x}_{jq}$ for $p < q$ . Consequently, ${x}_{jp}$ will always reach its maximum limit before ${x}_{jq}$ can assume a positive value.

The convex constraint functions ${g}_{ij}\left( {x}_{j}\right)$ are approximated in essentially the same way. Let ${r}_{ijk}$ be the slope of the $k$ th line segment corresponding to ${g}_{ij}\left( {x}_{j}\right)$ . It follows that

$$
{g}_{ij}\left( {x}_{j}\right)  \approx  \mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{r}_{ijk}{x}_{jk} + {g}_{ij}\left( {a}_{j0}\right)
$$

The complete problem is thus given by

$$
\text{ Minimize }z = \mathop{\sum }\limits_{{j = 1}}^{n}\left( {\mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{r}_{jk}{x}_{jk} + {f}_{j}\left( {a}_{j0}\right) }\right)
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}\left( {\mathop{\sum }\limits_{{k = 1}}^{{K}_{j}}{r}_{ijk}{x}_{jk} + {g}_{ij}\left( {a}_{j0}\right) }\right)  \leq  {b}_{i}, i = 1,2,\ldots , m
$$

$$
0 \leq  {x}_{jk} \leq  {a}_{jk} - {a}_{j, k - 1}, k = 1,2,\ldots ,{K}_{j},\;j = 1,2,\ldots , n
$$

where

$$
{r}_{jk} = \frac{{f}_{j}\left( {a}_{jk}\right)  - {f}_{j}\left( {a}_{j, k - 1}\right) }{{a}_{jk} - {a}_{j, k - 1}}
$$

$$
{r}_{ijk} = \frac{{g}_{ij}\left( {a}_{jk}\right)  - {g}_{ij}\left( {a}_{j, k - 1}\right) }{{a}_{jk} - {a}_{j, k - 1}}
$$

The maximization problem is treated in essentially the same way. In this case, ${r}_{j1} > {r}_{j2} > \cdots  > {r}_{j{K}_{j}}$ , which means that, for $p < q$ , the variable ${x}_{jp}$ will always reach its maximum value before ${x}_{jq}$ is allowed to assume a positive value (see Problem 21-11, for proof).

The new problem can be solved by the simplex method with upper-bounded variables (Section 7.3). The restricted basis concept is not needed because the convexity (concavity) of the functions guarantees correct selection of basic variables.

Example 21.2-2

Consider the problem

$$
\text{ Maximize }z = {x}_{1} - {x}_{2}
$$

subject to

$$
3{x}_{1}^{4} + {x}_{2} \leq  {243}
$$

$$
{x}_{1} + 2{x}_{2}^{2} \leq  {32}
$$

$$
{x}_{1} \geq  {2.1}
$$

$$
{x}_{2} \geq  {3.5}
$$

The separable functions of this problem are

$$
{f}_{1}\left( {x}_{1}\right)  = {x}_{1},\;{f}_{2}\left( {x}_{2}\right)  =  - {x}_{2}
$$

$$
{g}_{11}\left( {x}_{1}\right)  = 3{x}_{1}^{4},\;{g}_{12}\left( {x}_{2}\right)  = {x}_{2}
$$

$$
{g}_{21}\left( {x}_{1}\right)  = {x}_{1},\;{g}_{22}\left( {x}_{2}\right)  = 2{x}_{2}^{2}
$$

These functions satisfy the convexity condition required for the minimization problems. The functions ${f}_{1}\left( {x}_{1}\right) ,{f}_{2}\left( {x}_{2}\right) ,{g}_{12}\left( {x}_{2}\right)$ , and ${g}_{21}\left( {x}_{1}\right)$ are already linear.

The ranges of the variables ${x}_{1}$ and ${x}_{2}$ (estimated from the constraints) are $0 \leq  {x}_{1} \leq  3$ and $0 \leq  {x}_{2} \leq  4$ . Let ${K}_{1} = 3$ and ${K}_{2} = 4$ . The slopes corresponding to the separable functions are determined as follows.

For $j = 1$ ,

<table><tr><td>$k$</td><td>${a}_{1k}$</td><td>${g}_{11}\left( {a}_{1k}\right)  = 3{a}_{1k}^{4}$</td><td>${r}_{11k}$</td><td>${x}_{1k}$</td></tr><tr><td>0</td><td>0</td><td>0</td><td>-</td><td>-</td></tr><tr><td>1</td><td>1</td><td>3</td><td>3</td><td>${x}_{11}$</td></tr><tr><td>2</td><td>2</td><td>48</td><td>45</td><td>${x}_{12}$</td></tr><tr><td>3</td><td>3</td><td>243</td><td>195</td><td>${x}_{13}$</td></tr></table>

For $j = 2$ ,

<table><tr><td>$k$</td><td>${a}_{2k}$</td><td>${g}_{22}\left( {a}_{2k}\right)  = 2{a}_{2k}^{2}$</td><td>${r}_{22k}$</td><td>${x}_{2k}$</td></tr><tr><td>0</td><td>0</td><td>0</td><td>-</td><td>-</td></tr><tr><td>1</td><td>1</td><td>2</td><td>2</td><td>${x}_{21}$</td></tr><tr><td>2</td><td>2</td><td>8</td><td>6</td><td>${x}_{22}$</td></tr><tr><td>3</td><td>3</td><td>18</td><td>10</td><td>${x}_{23}$</td></tr><tr><td>4</td><td>4</td><td>32</td><td>14</td><td>${x}_{24}$</td></tr></table>

The complete problem then becomes

$$
\text{ Maximize }z = {x}_{1} - {x}_{2}
$$

subject to

$$
3{x}_{11} + {45}{x}_{12} + {195}{x}_{13} + \;{x}_{2}\; \leq  {243} \tag{1}
$$

$$
{x}_{1} + 2{x}_{21} + 6{x}_{22} + {10}{x}_{23} + {14}{x}_{24} \leq  {32} \tag{2}
$$

$$
{x}_{1} \geq  {2.1} \tag{3}
$$

$$
{x}_{2} \geq  {3.5} \tag{4}
$$

$$
{x}_{11} + {x}_{12} + {x}_{13} - {x}_{1}\; = 0 \tag{5}
$$

$$
{x}_{21} + {x}_{22} + {x}_{23} + {x}_{24} - {x}_{2}\; = 0 \tag{6}
$$

$$
0 \leq  {x}_{1k} \leq  1,\;k = 1,2,3 \tag{7}
$$

$$
0 \leq  {x}_{2k} \leq  1,\;k = 1,2,3,4 \tag{8}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

Constraints 5 and 6 are needed to maintain the relationship between the original and new variables. The optimum solution is

$$
z =  - {.52},{x}_{1} = {2.98},{x}_{2} = {3.5},{x}_{11} = {x}_{12} = 1,{x}_{13} = {.98},{x}_{21} = {x}_{22} = {x}_{23} = 1,{x}_{24} = {.5}
$$

## AMPL Moment

AMPL modeling of the original nonlinear problem of Example 21.2-2 is very much the same as in linear problems. Obtaining the solution is an entirely different matter because of the "unpredictable" behavior of the nonlinear functions. File amplEx21.2-2.txt provides the model. An explanation of the model is given in Appendix C on the website (see Figure C.17).

#### 21.2.2 Quadratic Programming

A quadratic programming model is defined as

$$
\text{ Maximize }z = \mathbf{{CX}} + {\mathbf{X}}^{T}\mathbf{{DX}}
$$

subject to

$$
\mathbf{{AX}} \leq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}
$$

where

$$
\mathbf{X} = {\left( {x}_{1},{x}_{2},\ldots ,{x}_{n}\right) }^{T}
$$

$$
\mathbf{C} = \left( {{c}_{1},{\mathrm{c}}_{2},\ldots ,{\mathrm{c}}_{n}}\right)
$$

$$
\mathbf{b} = {\left( {b}_{1},{\mathrm{\;b}}_{2},\ldots ,{\mathrm{b}}_{m}\right) }^{T}
$$

$$
\mathbf{A} = \left( \begin{matrix} {a}_{11} & \ldots & {a}_{1n} \\  \vdots & \vdots & \vdots \\  {a}_{m1} & \ldots & {a}_{mn} \end{matrix}\right)
$$

$$
\mathbf{D} = \left( \begin{matrix} {d}_{11} & \ldots & {d}_{1n} \\  \vdots & \vdots & \vdots \\  {d}_{n1} & \ldots & {d}_{nn} \end{matrix}\right)
$$

The function ${\mathbf{X}}^{\mathbf{T}}\mathbf{{DX}}$ defines a quadratic form (see Section D.3 on the website). The matrix $\mathbf{D}$ is assumed symmetric and negative definite-meaning that $z$ is strictly concave. The constraints are linear, which guarantees a convex solution space.

The solution to this problem is based on the KKT necessary conditions. These conditions (as shown in Table 20.2, Section 20.2.2) are also sufficient because $z$ is concave and the solution space is a convex set.

The quadratic programming problem will be treated for the maximization case. Conversion to minimization is straightforward. The problem may be written as

$$
\text{ Maximize }z = \mathbf{{CX}} + {\mathbf{X}}^{T}\mathbf{{DX}}
$$

subject to

$$
\mathbf{G}\left( \mathbf{X}\right)  = \left( \begin{matrix} \mathbf{A} \\   - \mathbf{I} \end{matrix}\right) \mathbf{X} - \left( \begin{array}{l} \mathbf{b} \\  \mathbf{0} \end{array}\right)  \leq  \mathbf{0}
$$

Let

$$
\mathbf{\lambda } = {\left( {\lambda }_{1},{\lambda }_{2},\ldots ,{\lambda }_{m}\right) }^{T}
$$

$$
\mathbf{U} = {\left( {\mu }_{1},{\mu }_{2},\ldots ,{\mu }_{n}\right) }^{T}
$$

be the Lagrange multipliers corresponding to constraints $\mathbf{{AX}} - \mathbf{b} \leq  \mathbf{0}$ and $- \mathbf{X} \leq  \mathbf{0}$ , respectively. Application of the KKT conditions yields

$$
\mathbf{\lambda } \geq  \mathbf{0},\mathbf{U} \geq  \mathbf{0}
$$

$$
\nabla z - \left( {{\mathbf{\lambda }}^{T},{\mathbf{U}}^{T}}\right) \nabla \mathbf{G}\left( \mathbf{X}\right)  = \mathbf{0}
$$

$$
{\lambda }_{i}\left( {{b}_{i} - \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j}}\right)  = 0, i = 1,2,\ldots , m
$$

$$
{\mu }_{j}{x}_{j} = 0,\;j = 1,2,\ldots , n
$$

$$
\mathbf{{AX}} \leq  \mathbf{b}
$$

$$
- \mathbf{X} \leq  \mathbf{0}
$$

Now

$$
\nabla z = \mathbf{C} + {\mathbf{{2X}}}^{T}\mathbf{D}
$$

$$
\nabla \mathbf{G}\left( \mathbf{X}\right)  = \left( \begin{matrix} \mathbf{A} \\   - \mathbf{I} \end{matrix}\right)
$$

Let $\mathbf{S} = \mathbf{b} - \mathbf{{AX}} \geq  \mathbf{0}$ be the slack variables of the constraints. The conditions reduce to

$$
- 2{\mathbf{X}}^{T}\mathbf{D} + {\mathbf{\lambda }}^{T}\mathbf{A} - {\mathbf{U}}^{T} = \mathbf{C}
$$

$$
\mathbf{{AX}} + \mathbf{S} = \mathbf{b}
$$

$$
{\mu }_{j}{x}_{j} = 0 = {\lambda }_{i}{S}_{i}\text{ for all }i\text{ and }j
$$

$$
\mathbf{\lambda },\mathbf{U},\mathbf{X},\mathbf{S} \geq  \mathbf{0}
$$

Because ${\mathbf{D}}^{T} = \mathbf{D}$ , the transpose of the first set of equations can be written as

$$
- 2\mathbf{{DX}} + {\mathbf{A}}^{T}\mathbf{\lambda } - \mathbf{U} = {\mathbf{C}}^{T}
$$

Hence, the necessary conditions may be combined as

$$
\left( \begin{matrix}  - 2\mathbf{D} & {\mathbf{A}}^{T} &  - \mathbf{I} & \mathbf{0} \\  \mathbf{A} & \mathbf{0} & \mathbf{0} & \mathbf{I} \end{matrix}\right) \left( \begin{array}{l} \mathbf{X} \\  \mathbf{\lambda } \\  \mathbf{U} \\  \mathbf{S} \end{array}\right)  = \left( \begin{matrix} {\mathbf{C}}^{T} \\  \mathbf{b} \end{matrix}\right)
$$

$$
{\mu }_{j}{x}_{j} = 0 = {\lambda }_{i}{S}_{i}\text{ , for all }i\text{ and }j
$$

$$
\mathbf{\lambda },\mathbf{U},\mathbf{X},\mathbf{S} \geq  \mathbf{0}
$$

Except for the conditions ${\mu }_{j}{x}_{j} = 0 = {\lambda }_{i}{S}_{i}$ , the remaining equations are linear in $\mathbf{X},\mathbf{\lambda }$ , $\mathbf{U}$ , and $\mathbf{S}$ . Thus, the problem is equivalent to solving a set of linear equations with the additional conditions ${\mu }_{j}{x}_{j} = 0 = {\lambda }_{i}{S}_{i}$ .

The solution of the system is obtained by using phase I of the two-phase method (Section 3.4.2), with the added restrictions ${\lambda }_{i}{S}_{i} = 0$ and ${\mu }_{j}{x}_{j} = 0$ . This means that ${\lambda }_{i}$ and ${s}_{i}$ cannot be positive simultaneously, and neither can ${\mu }_{j}$ and ${x}_{j}$ . This is the same idea of the restricted basis used in Section 21.2.1.

Phase I will render all the artificial variables equal to zero provided the problem has a feasible solution space.

## Example 21.2-3

Consider the problem

$$
\text{ Maximize }z = 4{x}_{1} + 6{x}_{2} - 2{x}_{1}^{2} - 2{x}_{1}{x}_{2} - 2{x}_{2}^{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  2
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

This problem can be put in the following matrix form:

$$
\text{ Maximize }z = \left( {4,6}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  + \left( {{x}_{1},{x}_{2}}\right) \left( \begin{array}{ll}  - 2 &  - 1 \\   - 1 &  - 2 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)
$$

subject to

$$
\left( {1,2}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  \leq  2
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The KKT conditions are given as

$$
\left( \begin{matrix} 4 & 2 & 1 &  - 1 & 0 & 0 \\  2 & 4 & 2 & 0 &  - 1 & 0 \\  1 & 2 & 0 & 0 & 0 & 1 \end{matrix}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \\  {\lambda }_{1} \\  {\mu }_{1} \\  {\mu }_{2} \\  {s}_{1} \end{array}\right)  = \left( \begin{array}{l} 4 \\  6 \\  2 \end{array}\right) ,{\mu }_{1}{x}_{1} = {\mu }_{1}{x}_{2} = {\lambda }_{1}{s}_{1} = 0
$$

The initial tableau for phase 1 is obtained by introducing the artificial variables ${R}_{1}$ and ${R}_{2}$ and updating the objective row.

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${\lambda }_{1}$</td><td>${\mu }_{1}$</td><td>${\mu }_{2}$</td><td>${R}_{1}$</td><td>${R}_{2}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$r$</td><td>6</td><td>6</td><td>3</td><td>-1</td><td>-1</td><td>0</td><td>0</td><td>0</td><td>10</td></tr><tr><td>${R}_{1}$</td><td>4</td><td>2</td><td>1</td><td>-1</td><td>0</td><td>1</td><td>0</td><td>0</td><td>4</td></tr><tr><td>${R}_{2}$</td><td>2</td><td>4</td><td>2</td><td>0</td><td>-1</td><td>0</td><td>1</td><td>0</td><td>6</td></tr><tr><td>${s}_{1}$</td><td>1</td><td>2</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>1</td><td>2</td></tr></table>

Iteration 1. The most promising entering variable ${x}_{1}$ can be made basic because ${\mu }_{1} = 0$ .

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${\lambda }_{1}$</td><td>${\mu }_{1}$</td><td>${\mu }_{2}$</td><td>${R}_{1}$</td><td>${R}_{2}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$R$</td><td>0</td><td>3</td><td>$\frac{3}{2}$</td><td>$\frac{1}{2}$</td><td>-1</td><td>$- \frac{3}{2}$</td><td>0</td><td>0</td><td>4</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>$\frac{1}{2}$</td><td>$\frac{1}{4}$</td><td>$- \frac{1}{4}$</td><td>0</td><td>$\frac{1}{4}$</td><td>0</td><td>0</td><td>1</td></tr><tr><td>${R}_{2}$</td><td>0</td><td>3</td><td>$\frac{3}{2}$</td><td>$\frac{1}{2}$</td><td>-1</td><td>$- \frac{1}{2}$</td><td>1</td><td>0</td><td>4</td></tr><tr><td>${s}_{1}$</td><td>0</td><td>$\frac{3}{2}$</td><td>$- \frac{1}{4}$</td><td>$\frac{1}{4}$</td><td>0</td><td>$- \frac{1}{4}$</td><td>0</td><td>1</td><td>1</td></tr></table>

Iteration 2. The most promising variable ${x}_{2}$ can be made basic because ${\mu }_{2} = 0$ .

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${\lambda }_{1}$</td><td>${\mu }_{1}$</td><td>${\mu }_{2}$</td><td>${R}_{1}$</td><td>${R}_{2}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$r$</td><td>0</td><td>0</td><td>2</td><td>0</td><td>-1</td><td>-1</td><td>0</td><td>-2</td><td>2</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>$\frac{1}{3}$</td><td>$- \frac{1}{3}$</td><td>0</td><td>$\frac{1}{3}$</td><td>0</td><td>$- \frac{1}{3}$</td><td>$\frac{2}{3}$</td></tr><tr><td>${R}_{1}$</td><td>0</td><td>0</td><td>2</td><td>0</td><td>-1</td><td>0</td><td>1</td><td>-2</td><td>2</td></tr><tr><td>${x}_{1}$</td><td>0</td><td>1</td><td>$- \frac{1}{6}$</td><td>$\frac{1}{6}$</td><td>0</td><td>$- \frac{1}{6}$</td><td>0</td><td>$\frac{2}{3}$</td><td>$\frac{2}{3}$</td></tr></table>

Iteration 3. The multiplier ${\lambda }_{1}$ can be made basic because ${s}_{1} = 0$ .

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${\lambda }_{1}$</td><td>${\mu }_{1}$</td><td>${\mu }_{2}$</td><td>${R}_{1}$</td><td>${R}_{2}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$r$</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>-1</td><td>-1</td><td>0</td><td>0</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>0</td><td>$- \frac{1}{3}$</td><td>$\frac{1}{6}$</td><td>$\frac{1}{3}$</td><td>$- \frac{1}{6}$</td><td>0</td><td>$\frac{1}{3}$</td></tr><tr><td>${\lambda }_{1}$</td><td>0</td><td>0</td><td>1</td><td>0</td><td>$- \frac{1}{2}$</td><td>0</td><td>$\frac{1}{2}$</td><td>-1</td><td>1</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>0</td><td>$\frac{1}{6}$</td><td>$- \frac{1}{12}$</td><td>$- \frac{1}{6}$</td><td>$\frac{1}{12}$</td><td>$\frac{1}{2}$</td><td>$\frac{5}{6}$</td></tr></table>

The last tableau gives the optimal feasible solution $\left( {{x}_{1}^{ * } = \frac{1}{3},{x}_{2}^{ * } = \frac{5}{6}}\right)$ . The associated optimal value of $z$ is 4.16 .

## Solver Moment

Solver template excelQP.xls solves Example 21.2-3. The data are entered in a manner similar to linear programming (see Section 2.3.1). The main difference occurs in the way the nonlinear functions are entered. Specifically, the nonlinear objective function is entered in target cell D5 as

$$
\text{ =4*B10+6*C10-2*B10} \textasciicircum \text{2-2*B10*C10-2*C10} \textasciicircum \text{2 }
$$

The changing cells are B10:C10 [≡ $\left( {{x}_{1},{x}_{2}}\right)$ ]. Notice that cells B5:C5 are not used at all in the model. For readability, we entered the symbol NL to indicate that the associated constraint is nonlinear. Also, you can specify the nonnegativity of the variables either in the Options dialogue box or by adding explicit nonnegativity constraints.

Show that $z$ is strictly convex, and then solve by the quadratic programming algorithm.

#### 21.2.3 Chance-Constrained Programming

Chance-constrained programming deals with situations in which the parameters of the constraints are random variables and the constraints are realized with a minimum probability. Mathematically, the problem is defined as

$$
\text{ Maximize }z = \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j}
$$

subject to

$$
P\left\{  {\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  {b}_{i}}\right\}   \geq  1 - {\alpha }_{i}, i = 1,2,\ldots , m,{x}_{j} \geq  0\text{ , for all }j
$$

The parameters ${a}_{ij}$ and ${b}_{i}$ are random variables, and constraint $i$ is realized with a minimum probability of $1 - {\alpha }_{i},0 < {\alpha }_{i} < 1$ .

Three cases are considered:

1. Only ${a}_{ij}$ is random for all $i$ and $j$ .

2. Only ${b}_{i}$ is random for all $i$ .

3. Both ${a}_{ij}$ and ${b}_{i}$ are random for all $i$ and $j$ .

In all three cases, it is assumed that the parameters are normally distributed with known means and variances.

Case 1. Each ${a}_{ij}$ is normally distributed with mean $E\left\{  {a}_{ij}\right\}$ , variance var $\left\{  {a}_{ij}\right\}$ , and $\operatorname{cov}\left\{  {{a}_{ij},{a}_{{i}^{\prime }{j}^{\prime }}}\right\}$ of ${a}_{ij}$ and ${a}_{{i}^{\prime }{j}^{\prime }}$ .

Consider

$$
P\left\{  {\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  {b}_{i}}\right\}   \geq  1 - {\alpha }_{i}
$$

Define

$$
{h}_{i} = \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j}
$$

The random variable ${h}_{i}$ is normally distributed with

$$
E\left\{  {h}_{i}\right\}   = \mathop{\sum }\limits_{{j = 1}}^{n}E\left\{  {a}_{ij}\right\}  {x}_{j}
$$

$$
\operatorname{var}\left\{  {h}_{i}\right\}   = {\mathbf{X}}^{T}{\mathbf{D}}_{i}\mathbf{X}
$$

where

$$
\mathbf{X} = {\left( {x}_{1},\ldots ,{x}_{n}\right) }^{T}
$$

$$
{\mathbf{D}}_{i} = i\text{ th covariance matrix }
$$

$$
= \left( \begin{matrix} \operatorname{var}\left\{  {a}_{i1}\right\}  & \ldots & \operatorname{cov}\left\{  {{a}_{i1},{a}_{in}}\right\}  \\  \vdots & \vdots & \vdots \\  \operatorname{cov}\left\{  {{a}_{in},{a}_{i1}}\right\}  & \cdots & \operatorname{var}\left\{  {a}_{in}\right\}   \end{matrix}\right)
$$

Now

$$
P\left\{  {{h}_{i} \leq  {b}_{i}}\right\}   = P\left\{  {\frac{{h}_{i} - E\left\{  {h}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {h}_{i}\right\}  }} \leq  \frac{{b}_{i} - E\left\{  {h}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {h}_{i}\right\}  }}}\right\}   \geq  1 - {\alpha }_{i}
$$

Letting $F$ be the CDF of the standard normal distribution, it follows that

$$
P\left\{  {{h}_{i} \leq  {b}_{i}}\right\}   = F\left( \frac{{b}_{i} - E\left\{  {h}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {h}_{i}\right\}  }}\right)
$$

Let ${K}_{{\alpha }_{i}}$ be the standard normal value such that

$$
F\left( {K}_{{\alpha }_{i}}\right)  = 1 - {\alpha }_{i}
$$

Then the statement $P\left\{  {{h}_{i} \leq  {b}_{i}}\right\}   \geq  1 - {\alpha }_{i}$ is realized if, and only if,

$$
\frac{{b}_{i} - E\left\{  {h}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {h}_{i}\right\}  }} \geq  {K}_{{\alpha }_{i}}
$$

This yields the following nonlinear deterministic constraint:

$$
\mathop{\sum }\limits_{{j = 1}}^{n}E\left\{  {a}_{ij}\right\}  {x}_{j} + {K}_{{\alpha }_{i}}\sqrt{{\mathbf{X}}^{T}{\mathbf{D}}_{i}\mathbf{X}} \leq  {b}_{i}
$$

For the special case where the parameters ${a}_{ij}$ are independent, $\operatorname{cov}\left\{  {{a}_{ij},{a}_{{i}^{\prime }{j}^{\prime }}}\right\}   = 0$ , and the last constraint reduces to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}E\left\{  {a}_{ij}\right\}  {x}_{j} + {K}_{{\alpha }_{i}}\sqrt{\mathop{\sum }\limits_{{j = 1}}^{n}\operatorname{var}\left\{  {a}_{ij}\right\}  {x}_{j}^{2}} \leq  {b}_{i}
$$

This constraint can be put in the separable programming form (Section 21.2.1) by using the substitution

$$
{y}_{i} = \sqrt{\mathop{\sum }\limits_{{j = 1}}^{n}\operatorname{var}\left\{  {a}_{ij}\right\}  {x}_{j}^{2}}\text{ , for all }i
$$

Thus, the original constraint is equivalent to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}E\left\{  {a}_{ij}\right\}  {x}_{j} + {K}_{{\alpha }_{i}}{y}_{i} \leq  {b}_{i}
$$

and

$$
\mathop{\sum }\limits_{{j = 1}}^{n}\operatorname{var}\left\{  {a}_{ij}\right\}  {x}_{j}^{2} - {y}_{i}^{2} = 0
$$

Case 2. Only ${b}_{i}$ is normal with mean $E\left\{  {b}_{i}\right\}$ and variance $\operatorname{var}\left\{  {b}_{i}\right\}$ .

Consider the stochastic constraint

$$
P\left\{  {{b}_{i} \geq  \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j}}\right\}   \geq  {\alpha }_{i}
$$

As in case 1,

$$
P\left\{  {\frac{{b}_{i} - E\left\{  {b}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {b}_{i}\right\}  }} \geq  \frac{\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - E\left\{  {b}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {b}_{i}\right\}  }}}\right\}   \geq  {\alpha }_{i}
$$

This can hold true only if

$$
\frac{\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - E\left\{  {b}_{i}\right\}  }{\sqrt{\operatorname{var}\left\{  {b}_{i}\right\}  }} \leq  {K}_{{\alpha }_{i}}
$$

Thus, the stochastic constraint is equivalent to the deterministic linear constraint

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  E\left\{  {b}_{i}\right\}   + {K}_{{\alpha }_{i}}\sqrt{\operatorname{var}\left\{  {b}_{i}\right\}  }
$$

Case 3. All ${a}_{ij}$ and ${b}_{i}$ are normal random variables.

Consider the constraint

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  {b}_{i}
$$

This may be written

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - {b}_{i} \leq  0
$$

Because all ${a}_{ij}$ and ${b}_{i}$ are normal, $\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - {b}_{i}$ is also normal. This shows that the chance constraint reduces to the situation in case 1 and is treated in a similar manner.

## Example 21.2-4

Consider the chance-constrained problem

$$
\text{ Maximize }z = 5{x}_{1} + 6{x}_{2} + 3{x}_{3}
$$

subject to

$$
P\left\{  {{a}_{11}{x}_{1} + {a}_{12}{x}_{2} + {a}_{13}{x}_{3} \leq  8}\right\}   \geq  {.95}
$$

$$
P\left\{  {5{x}_{1} + {x}_{2} + 6{x}_{3} \leq  {b}_{2}}\right\}   \geq  {.10}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

Assume that the parameters ${a}_{1jj}, j = 1,2,3$ , are independent and normally distributed random variables with the following means and variances:

$$
E\left\{  {a}_{11}\right\}   = 1, E\left\{  {a}_{12}\right\}   = 3, E\left\{  {a}_{13}\right\}   = 9
$$

$$
\operatorname{var}\left\{  {a}_{11}\right\}   = {25},\operatorname{var}\left\{  {a}_{12}\right\}   = {16},\operatorname{var}\left\{  {a}_{13}\right\}   = 4
$$

The parameter ${b}_{2}$ is normally distributed with mean 7 and variance 9 .

From standard normal tables in Appendix A (or excelStatTables.xls),

$$
{K}_{{\alpha }_{1}} = {K}_{.05} \approx  {1.645},\;{K}_{{\alpha }_{2}} = {K}_{.10} \approx  {1.285}
$$

For the first constraint, the equivalent deterministic constraint is

$$
{x}_{1} + 3{x}_{2} + 9{x}_{3} + {1.645}\sqrt{{25}{x}_{1}^{2} + {16}{x}_{2}^{2} + 4{x}_{3}^{2}} \leq  8
$$

and for the second constraint

$$
5{x}_{1} + {x}_{2} + 6{x}_{3} \leq  7 + {1.285}\left( 3\right)  = {10.855}
$$

The resulting problem can be solved as a nonlinear program (using AMPL or Solver), or it can be converted to a separable program as follows:

$$
{y}^{2} = {25}{x}_{1}^{2} + {16}{x}_{2}^{2} + 4{x}_{3}^{2}
$$

The problem becomes

$$
\text{ Maximize }z = 5{x}_{1} + 6{x}_{2} + 3{x}_{3}
$$

subject to

$$
{x}_{1} + 3{x}_{2} + 9{x}_{3} + {1.645y} \leq  8
$$

$$
{25}{x}_{1}^{2} + {16}{x}_{2}^{2} + 4{x}_{3}^{2} - {y}^{2} = 0
$$

$$
5{x}_{1} + {x}_{2} + 6{x}_{3} \leq  {10.855}
$$

$$
{x}_{1},{x}_{2},{x}_{3}, y \geq  0
$$

The problem can be solved by separable programming. Also, Excel file excelCCP.xls can be used to solve the nonlinear problem directly.

#### 21.2.4 Linear Combinations Method

This method deals with the following problem in which all constraints are linear:

$$
\text{ Maximize }z = f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{{AX}} \leq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}
$$

The procedure is based on the steepest-ascent (gradient) method (Section 21.1.2). However, the direction specified by the gradient vector may not yield a feasible solution for the constrained problem. Also, the gradient vector will not necessarily be null at the optimum (constrained) point. The steepest ascent method thus must be modified to handle the constrained case.

Let ${\mathbf{X}}_{k}$ be the feasible trial point at iteration $k$ . The objective function $f\left( \mathbf{X}\right)$ can be expanded in the neighborhood of ${\mathbf{X}}_{k}$ using Taylor’s series. This gives

$$
f\left( \mathbf{X}\right)  \approx  f\left( {\mathbf{X}}_{k}\right)  + \nabla f\left( {\mathbf{X}}_{k}\right) \left( {\mathbf{X} - {\mathbf{X}}_{k}}\right)  = \left( {f\left( {\mathbf{X}}_{k}\right)  - \nabla f\left( {\mathbf{X}}_{k}\right) {\mathbf{X}}_{k}}\right)  + \nabla f\left( {\mathbf{X}}_{k}\right) \mathbf{X}
$$

The procedure calls for determining a feasible point $\mathbf{X} = {\mathbf{X}}^{ * }$ such that $f\left( \mathbf{X}\right)$ is maximized subject to the (linear) constraints of the problem. Because $f\left( {\mathbf{X}}_{k}\right)  - \nabla f\left( {\mathbf{X}}_{k}\right) {\mathbf{X}}_{k}$ is a constant, the problem for determining ${\mathbf{X}}^{ * }$ reduces to solving the following linear program:

$$
\text{ Maximize }{w}_{k}\left( \mathbf{X}\right)  = \nabla f\left( {\mathbf{X}}_{k}\right) \mathbf{X}
$$

subject to

$$
\mathbf{{AX}} \leq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}
$$

Given that ${w}_{k}$ is constructed from the gradient of $f\left( \mathbf{X}\right)$ at ${\mathbf{X}}_{k}$ , an improved solution point can be secured if and only if ${w}_{k}\left( {\mathbf{X}}^{ * }\right)  > {w}_{k}\left( {\mathbf{X}}_{k}\right)$ . From Taylor’s expansion, the condition does not guarantee that $f\left( {\mathbf{X}}^{ * }\right)  > f\left( {\mathbf{X}}_{k}\right)$ unless ${\mathbf{X}}^{ * }$ is in the neighborhood of ${\mathbf{X}}_{k}$ . However, given ${w}_{k}\left( {\mathbf{X}}^{ * }\right)  > {w}_{k}\left( {\mathbf{X}}_{k}\right)$ , there must exist a point ${\mathbf{X}}_{k + 1}$ on the line segment $\left( {{\mathbf{X}}_{k},{\mathbf{X}}^{ * }}\right)$ such that $f\left( {\mathbf{X}}_{k + 1}\right)  > f\left( {\mathbf{X}}_{k}\right)$ . The objective is to determine ${\mathbf{X}}_{k + 1}$ . Define

$$
{\mathbf{X}}_{k + 1} = \left( {1 - r}\right) {\mathbf{X}}_{k} + r{\mathbf{X}}^{ * } = {\mathbf{X}}^{k} + r\left( {{\mathbf{X}}^{ * } - {\mathbf{X}}_{k}}\right) ,0 < r \leq  1
$$

This means that ${\mathbf{X}}_{k + 1}$ is a linear combination of ${\mathbf{X}}_{k}$ and ${\mathbf{X}}^{ * }$ . Because ${\mathbf{X}}_{k}$ and ${\mathbf{X}}^{ * }$ are two feasible points in a convex solution space, ${\mathbf{X}}_{k + 1}$ is also feasible. In terms of the steepest-ascent method (Section 21.1.2), the parameter $r$ represents step size.

The point ${\mathbf{X}}_{k + 1}$ is determined such that $f\left( \mathbf{X}\right)$ is maximized. Because ${\mathbf{X}}_{k + 1}$ is a function of $r$ only, ${\mathbf{X}}_{k + 1}$ is determined by maximizing

$$
h\left( r\right)  = f\left( {{\mathbf{X}}_{k} + r\left( {{\mathbf{X}}^{ * } - {\mathbf{X}}_{k}}\right) }\right)
$$

The procedure is repeated until, at the $k$ th iteration, ${w}_{k}\left( {\mathbf{X}}^{ * }\right)  \leq  {w}_{k}\left( {\mathbf{X}}_{k}\right)$ . At this point, no further improvements are possible, and the process terminates with ${\mathbf{X}}_{\mathbf{k}}$ as the best solution point.

The linear programming problems generated at the successive iterations differ only in the coefficients of the objective function. Post-optimal analysis procedures presented in Section 4.5 thus may be used to carry out calculations efficiently.

## Example 21.2-5

Consider the quadratic programming of Example 21.2-3.

$$
\text{ Maximize }f\left( \mathbf{X}\right)  = 4{x}_{1} + 6{x}_{2} - 2{x}_{1}^{2} - 2{x}_{1}{x}_{2} - 2{x}_{2}^{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  2
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

Let the initial trial point be ${\mathbf{X}}_{0} = \left( {\frac{1}{2},\frac{1}{2}}\right)$ , which is feasible. Now

$$
\nabla f\left( \mathbf{X}\right)  = \left( {4 - 4{x}_{1} - 2{x}_{2},6 - 2{x}_{1} - 4{x}_{2}}\right)
$$

Iteration 1

$$
\nabla f\left( {\mathbf{X}}_{0}\right)  = \left( {1,3}\right)
$$

The associated linear program maximizes ${w}_{1} = {x}_{1} + 3{x}_{2}$ subject to the constraints of the original problem. This gives the optimal solution ${\mathbf{X}}^{ * } = \left( {0,1}\right)$ . The values of ${w}_{1}$ at ${\mathbf{X}}_{0}$ and ${\mathbf{X}}^{ * }$ equal 2 and 3, respectively. Hence, a new trial point is determined as

$$
{\mathbf{X}}_{1} = \left( {\frac{1}{2},\frac{1}{2}}\right)  + r\left\lbrack  {\left( {0,1}\right)  - \left( {\frac{1}{2},\frac{1}{2}}\right) }\right\rbrack   = \left( {\frac{1 - r}{2},\frac{1 + r}{2}}\right)
$$

The maximization of

$$
h\left( r\right)  = f\left( {\frac{1 - r}{2},\frac{1 + r}{2}}\right)
$$

yields ${r}_{1} = 1$ . Thus ${\mathbf{X}}_{1} = \left( {0,1}\right)$ with $f\left( {\mathbf{X}}_{1}\right)  = 4$ .

Iteration 2

$$
\nabla f\left( {\mathbf{X}}_{1}\right)  = \left( {2,2}\right)
$$

The objective function of the new linear programming problem is ${w}_{2} = 2{x}_{1} + 2{x}_{2}$ . The optimum solution to this problem yields ${\mathbf{X}}^{ * } = \left( {2,0}\right)$ . Because the values of ${w}_{2}$ at ${\mathbf{X}}_{1}$ and ${\mathbf{X}}^{ * }$ are 2 and 4, respectively, a new trial point must be determined. Thus

$$
{\mathbf{X}}_{2} = \left( {0,1}\right)  + r\left\lbrack  {\left( {2,0}\right)  - \left( {0,1}\right) }\right\rbrack   = \left( {{2r},1 - r}\right)
$$

The maximization of

$$
h\left( r\right)  = f\left( {{2r},1 - r}\right)
$$

yields ${r}_{2} = \frac{1}{6}$ . Thus ${\mathbf{X}}_{2} = \left( {\frac{1}{3},\frac{5}{6}}\right)$ with $f\left( {\mathbf{X}}_{2}\right)  \approx  {4.16}$ .

Iteration 3

$$
\nabla f\left( {\mathbf{X}}_{2}\right)  = \left( {1,2}\right)
$$

The corresponding objective function is ${w}_{3} = {x}_{1} + 2{x}_{2}$ . The optimum solution of this problem yields the alternative solutions ${\mathbf{X}}^{ * } = \left( {0,1}\right)$ and ${\mathbf{X}}^{ * } = \left( {2,0}\right)$ . The value of ${w}_{3}$ for both points equals its value at ${\mathbf{X}}_{2}$ . Consequently, no further improvements are possible. The approximate optimum solution is ${\mathbf{X}}_{2} = \left( {\frac{1}{3},\frac{5}{6}}\right)$ with $f\left( {\mathbf{X}}_{2}\right)  \approx  {4.16}$ . This happens to be the exact optimum.

#### 21.2.5 SUMT Algorithm

In this section, a more general gradient method is presented. It is assumed that the objective function $f\left( \mathbf{X}\right)$ is concave and each constraint function ${g}_{i}\left( \mathbf{X}\right)$ is convex. Moreover, the solution space must have an interior. This rules out both implicit and explicit use of equality constraints.

The SUMT (Sequential Unconstrained Maximization Technique) algorithm is based on transforming the constrained problem into an equivalent unconstrained problem. The procedure is more or less similar to the Lagrange multipliers method. The transformed problem can then be solved using the steepest-ascent method (Section 21.1.2).

To clarify the concept, consider the new function

$$
p\left( {\mathbf{X}, t}\right)  = f\left( \mathbf{X}\right)  + t\left( {\mathop{\sum }\limits_{{i = 1}}^{m}\frac{1}{{g}_{i}\left( \mathbf{X}\right) } - \mathop{\sum }\limits_{{j = 1}}^{n}\frac{1}{{x}_{j}}}\right)
$$

where $t$ is a nonnegative parameter. The second summation sign accounts for the nonnegativity constraints, which must be put in the form $- {x}_{j} \leq  0$ to be consistent with the original constraints. Because ${g}_{i}\left( \mathbf{X}\right)$ is convex, $\frac{1}{{g}_{i}\left( \mathbf{X}\right) }$ is concave. This means that $p\left( {\mathbf{X}, t}\right)$ is concave in $\mathbf{X}$ . Consequently, $p\left( {\mathbf{X}, t}\right)$ possesses a unique maximum. Optimization of the original constrained problem is equivalent to optimization of $p\left( {\mathbf{X}, t}\right)$ .

The algorithm is initiated by arbitrarily selecting an initial nonnegative value for $t$ . An initial point ${\mathbf{X}}_{0}$ is selected as the first trial solution. This point must be an interior point-that is, it must not lie on the boundaries of the solution space. Given the value of $t$ , the steepest-ascent method is used to determine the corresponding optimal solution (maximum) of $p\left( {\mathbf{X}, t}\right)$ .

The new solution point will always be an interior point, because if the solution point is close to the boundaries, at least one of the functions $\frac{1}{{g}_{i}\left( \mathbf{X}\right) }$ or $- \frac{1}{{x}_{i}}$ will acquire a very large negative value. Because the objective is to maximize $p\left( {\mathbf{X}, t}\right)$ , such solution points are automatically excluded. The main result is that successive solution points will always be interior points. Consequently, the problem can always be treated as an unconstrained case.

Once the optimum solution corresponding to a given value of $t$ is obtained, a new value of $t$ is generated, and the optimization process (using the steepest-ascent method) is repeated. If ${t}^{\prime }$ is the current value of $t$ , the next value, ${t}^{\prime \prime }$ , must be selected such that $0 < {t}^{\prime \prime } < {t}^{\prime }$ .

The SUMT algorithm ends when, for two successive values of $t$ , the corresponding optimum values of $\mathbf{X}$ obtained by maximizing $p\left( {\mathbf{X}, t}\right)$ are approximately the same. At this point, further trials will produce little improvement.

Actual implementation of SUMT involves more details than have been presented here. Specifically, the selection of an initial value of $t$ is an important factor that can affect the speed of convergence. Further, the determination of an initial interior point may require special techniques. These details can be found in Fiacco and McCormick (1968).

## BIBLIOGRAPHY

Bazaraa, M., H. Sherall, and C. Shetty, Nonlinear Programming, Theory and Algorithms, 2nd ed., Wiley, New York, 1993.

Beightler, C., D. Phillips, and D. Wilde, Foundations of Optimization, 2nd ed., Prentice Hall, Upper Saddle River, NJ, 1979.

Fletcher, R., Practical Methods of Optimization, 2nd ed., Wiley, New York, 2000.

Fiacco, A., and G. McCormick, Nonlinear Programming, Sequential Unconstrained Minimization Techniques, Wiley, New York, 1968.

Luenberger, D., Linear and Nonlinear Programming, Kluwer Academic Publishers, Boston, 2003.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>21.1.1</td><td>21-1 to 21-4</td></tr><tr><td>21.2.1</td><td>21-5 to 21-13</td></tr><tr><td>21.2.2</td><td>21-14 to 21-15</td></tr><tr><td>21.2.3</td><td>21-16 to 21-17</td></tr><tr><td>21.2.4</td><td>21-18 to 21-18</td></tr></table>

21-1. Use Excel template excelDiGold.xls to solve Example 21.1-1 assuming that $\Delta  = {.01}$ . Compare the amount of computations and the accuracy of the results with those in Figure 21.2.

21-2. Find the maximum of each of the following functions by dichotomous search. Assume that $\Delta  = {.05}$ :

(a) $f\left( x\right)  = \frac{1}{\left| {\left( x - 3\right) }^{3}\right| },\;2 \leq  x \leq  4$

(b) $f\left( x\right)  = x\cos x,\;0 \leq  x \leq  \pi$

*(c) $f\left( x\right)  = x\sin {\pi x},\;{1.5} \leq  x \leq  {2.5}$

(d) $f\left( x\right)  =  - {\left( x - 3\right) }^{2},\;2 \leq  x \leq  4$

*(e) $f\left( x\right)  = \left\{  \begin{array}{ll} {4x}, & 0 \leq  x \leq  2 \\  4 - x, & 2 \leq  x \leq  4 \end{array}\right.$

*21-3. Show that, in general, the Newton-Raphson method (Section 20.1.2) when applied to a strictly concave quadratic function will converge in exactly one step. Apply the method to the maximization of

$$
f\left( \mathbf{X}\right)  = 4{x}_{1} + 6{x}_{2} - 2{x}_{1}^{2} - 2{x}_{1}{x}_{2} - 2{x}_{2}^{2}
$$

21-4. Carry out five iterations for each of the following problems using the method of steepest ascent/descent. Assume that ${\mathbf{X}}^{0} = 0$ in each case.

(a) $\min f\left( \mathbf{X}\right)  = \min f\left( \mathbf{X}\right)  = {\left( {x}_{2} - {x}_{1}^{2}\right) }^{2} + \left( {1 - {x}_{1}}\right)$

(b) $\max f\left( \mathbf{X}\right)  = \mathbf{{cX}} + {\mathbf{X}}^{T}\mathbf{A}\mathbf{X}$

where

$$
\mathbf{c} = \left( {1,3,5}\right)
$$

$$
\mathbf{A} = \left( \begin{array}{rrr}  - 5 &  - 3 &  - \frac{1}{2} \\   - 3 &  - 2 & 0 \\   - \frac{1}{2} & 0 &  - \frac{1}{2} \end{array}\right)
$$

(c) $\min f\left( \mathbf{X}\right)  = {x}_{1} - {x}_{2} + {x}_{1}^{2} - {x}_{1}{x}_{2}$

21-5. Approximate the following problem as a mixed integer program:

$$
\text{ Maximize }z = {e}^{-{x}_{1}} + {x}_{1} + {\left( {x}_{2} + 1\right) }^{2}
$$

subject to

$$
{x}_{1}^{2} + {x}_{2} \leq  3
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

*21-6. Repeat Problem 21-5 using the restricted basis method. Then find the optimal solution.

21-7. Consider the problem

$$
\text{ Maximize }z = {x}_{1}{x}_{2}{x}_{3}
$$

subject to

$$
{x}_{1}^{2} + {x}_{2} + {x}_{3} \leq  4
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

Approximate the problem as a linear program for use with the restricted basis method.

*21-8. Show how the following problem can be made separable:

$$
\text{ Maximize }z = {x}_{1}{x}_{2} + {x}_{3} + {x}_{1}{x}_{3}
$$

subject to

$$
{x}_{1}{x}_{2} + {x}_{2} + {x}_{1}{x}_{3} \leq  {10}
$$

$$
{x}_{1},{x}_{2}{x}_{3} \geq  0
$$

21-9. Show how the following problem can be made separable:

$$
\text{ Minimize }z = {e}^{2{x}_{1} + {x}_{2}{}^{2}} + {\left( {x}_{3} - 2\right) }^{2}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} \leq  6
$$

$$
{x}_{1},{x}_{2}{x}_{3} \geq  0
$$

21-10. Show how the following problem can be made separable:

$$
\text{ Maximize }z = {e}^{{x}_{1}{x}_{2}} + {x}_{2}^{2}{x}_{3} + {x}_{4}
$$

subject to

$$
{x}_{1} + {x}_{2}{x}_{3} + {x}_{3} \leq  {10}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

$$
{x}_{4}\text{ unrestricted in sign }
$$

21-11. Show that in separable convex programming, it is never optimal to have ${x}_{ki} > 0$ when ${x}_{k - 1, i}$ is not at its upper bound.

21-12. Solve as a separable convex programming problem.

$$
\text{ Minimize }z = {x}_{1}^{4} + {x}_{2} + {x}_{3}^{2}
$$

subject to

$$
{x}_{1}^{2} + {x}_{2} + {x}_{3}^{2} \leq  4
$$

$$
\left| {{x}_{1} + {x}_{2}}\right|  \leq  3
$$

$$
{x}_{1},{x}_{3} \geq  0
$$

${x}_{2}$ unrestricted in sign

21-13. Solve the following as a separate convex programming problem:

$$
\text{ Minimize }z = {\left( {x}_{1} - 2\right) }^{2} + 4{\left( {x}_{2} - 6\right) }^{2}
$$

subject to

$$
6{x}_{1} + 3{\left( {x}_{2} + 1\right) }^{2} \leq  {12}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

*21-14. Consider the problem

$$
\text{ Maximize }z = 6{x}_{1} + 3{x}_{2} - 4{x}_{1}{x}_{2} - 2{x}_{1}^{2} - 3{x}_{2}^{2}
$$

subject to

$$
{x}_{1} + {x}_{2} \leq  1
$$

$$
2{x}_{1} + 3{x}_{2} \leq  4
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

Show that $z$ is strictly concave, and then solve the problem using the quadratic programming algorithm.

*21-15. Consider the problem:

$$
\text{ Minimize }z = 2{x}_{1}^{2} + 2{x}_{2}^{2} + 3{x}_{3}^{2} + 2{x}_{1}{x}_{2} + 2{x}_{2}{x}_{3} + {x}_{1} - 3{x}_{2} - 5{x}_{3}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} \geq  1
$$

$$
3{x}_{1} + 2{x}_{2} + {x}_{3} \leq  6
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

*21-16. Convert the following stochastic problem into an equivalent deterministic model:

$$
\text{ Maximize }z = {x}_{1} + 2{x}_{2} + 5{x}_{3}
$$

subject to

$$
P\left\{  {{a}_{1}{x}_{1} + 3{x}_{2} + {a}_{3}{x}_{3} \leq  {10}}\right\}   \geq  {0.9}
$$

$$
P\left\{  {7{x}_{1} + 5{x}_{2} + {x}_{3} \leq  {b}_{2}}\right\}   \geq  {0.1}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

Assume that ${a}_{1}$ and ${a}_{3}$ are independent and normally distributed random variables with means $E\left\{  {a}_{1}\right\}   = 2$ and $E\left\{  {a}_{3}\right\}   = 5$ and variances $\operatorname{var}\left\{  {a}_{1}\right\}   = 9$ and $\operatorname{var}\left\{  {a}_{3}\right\}   = {16}$ and that ${b}_{2}$ is normally distributed with mean 15 and variance 25 .

21-17. Consider the following stochastic programming model:

$$
\text{ Maximize }z = {x}_{1} + {x}_{2}^{2} + {x}_{3}
$$

subject to

$$
P\left\{  {{x}_{1}^{2} + {a}_{2}{x}_{2}^{3} + {a}_{3}\sqrt{{x}_{3}} \leq  {10}}\right\}   \geq  {0.9}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

The parameters ${a}_{2}$ and ${a}_{3}$ are independent and normally distributed random variables with means 5 and 2, and variance 16 and 25, respectively. Convert the problem into a (deterministic) separable programming form.

21-18. Solve the following problem by the linear combinations method:

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = {x}_{1}^{3} + {x}_{2}^{3} - 3{x}_{1}{x}_{2}
$$

subject to

$$
3{x}_{1} + {x}_{2} \leq  3
$$

$$
5{x}_{1} - 3{x}_{2} \leq  5
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

This page intentionally left blank