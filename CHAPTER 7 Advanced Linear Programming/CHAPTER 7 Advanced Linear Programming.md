## CHAPTER 7 Advanced Linear Programming ^Chapter

```markmap
---
markmap:
  height: 643
---
# [[#^Chapter|CHAPTER 7: Advanced Linear Programming]]
## [[#^Application|Real-Life Application: Optimal Ship Routing and Personnel Assignment]]
## [[#^SimplexFundamentals|7.1 Simplex Method Fundamentals]]
### [[#^Convexity|Convex Sets and Extreme Points]]
### [[#^ConvexCombo|Optimum at Extreme Points and Convex Combinations]]
### [[#^SimplexCrux|Why Simplex Works: Finite Extreme Points Define the Space]]
### [[#^ExampleConvex|Example: Showing a Set Is Convex]]
### [[#^ExtremeToBasic|From Extreme Points to Basic Solutions]]
#### [[#^ExtremeBasicEquivalence|Extreme Points and Basic Solutions Are Equivalent]]
#### [[#^ExampleBasicSolutions|Example: Listing Basic Feasible and Infeasible Solutions]]
### [[#^TableauMatrix|Generalized Simplex Tableau in Matrix Form]]
#### [[#^TableauDerivation|Computing z and XB from the Basis Inverse]]
#### [[#^TableauColumn|Tableau Column for a Variable xj]]
#### [[#^InverseTradeoff|Inverse Updates: Accuracy vs Speed]]
#### [[#^ExampleTableau|Example: Generating a Simplex Tableau]]
## [[#^RevisedSimplex|7.2 Revised Simplex Method]]
### [[#^RevisedOverview|Matrix Computations vs Row Operations]]
### [[#^OptimalityFeasibility|Optimality and Feasibility Conditions]]
#### [[#^ReducedCost|Reduced Cost Formula]]
#### [[#^OptimalityRule|Optimality Condition (Entering Variable)]]
#### [[#^FeasibilityRule|Feasibility Condition (Leaving Variable)]]
#### [[#^RatioTest|Ratio Test]]
### [[#^RevisedAlgorithm|Revised Simplex Algorithm]]
#### [[#^AlgorithmSteps|Algorithm Steps]]
#### [[#^ExampleRevised|Example: Reddy Mikks via Revised Simplex]]
### [[#^ComputationalIssues|Computational Issues]]
#### [[#^AccuracySpeed|Accuracy vs Speed and Why Solvers Avoid Explicit Inversion]]
#### [[#^ProductForm|Product Form Update of the Inverse]]
#### [[#^LUDecomposition|LU Decomposition]]
#### [[#^RefreshInverse|Reinversion (Refreshing) Strategy]]
#### [[#^RoundoffError|Roundoff Error Diagnostics]]
#### [[#^AhaHistory|Aha Moment: Early Simplex Implementations]]
## [[#^BoundedVariables|7.3 Bounded-Variables Algorithm]]
### [[#^LowerBounds|Handling Lower Bounds by Substitution]]
### [[#^UpperBounds|Why Upper-Bound Substitution Needs Care]]
### [[#^BoundedModel|Upper-Bounded LP Model Form]]
### [[#^ModifiedFeasibility|Modified Feasibility Condition with Bounds]]
### [[#^ThetaRules|How θ1, θ2, and uj Determine the Next Move]]
## [[#^Duality|7.4 Duality]]
### [[#^DualMatrix|Matrix Definition of the Dual Problem]]
### [[#^WeakDuality|Weak Duality and Equality at Optimality]]
### [[#^UnboundedInfeasible|Unboundedness and Infeasibility Relationships]]
### [[#^OptimalDualSolution|Optimal Dual Solution from the Optimal Primal Basis]]
### [[#^ShadowPrices|Shadow Prices (Dual Variables)]]
### [[#^DualSimplexMotivation|Motivation for the Dual Simplex Algorithm]]
### [[#^ExampleDual|Example: Writing the Dual and Solving from the Primal Basis]]
## [[#^ParametricLP|7.5 Parametric Linear Programming]]
### [[#^ParametricIdea|C(t), b(t), and the Parametric View]]
### [[#^CriticalValues|Critical Values and Piecewise-Constant Bases]]
### [[#^ParametricC|Parametric Changes in C]]
#### [[#^OptimalityInequalities|Optimality Inequalities Determine the Next Breakpoint]]
#### [[#^ExampleParametricC|Example: Tracking Optimality as t Changes]]
#### [[#^ParametricSummaryC|Summary of the Optimal Solution over t]]
### [[#^Parametricb|Parametric Changes in b]]
#### [[#^FeasibilityInequalities|Feasibility Inequalities Determine the Next Breakpoint]]
#### [[#^ExampleParametricb|Example: Tracking Feasibility as t Changes]]
#### [[#^ParametricSummaryb|Summary of the Optimal Solution over t]]
## [[#^MoreTopics|7.6 More Linear Programming Topics]]
### [[#^MinCostFlow|Minimum-Cost Capacitated Flow and Network Simplex]]
### [[#^DantzigWolfe|Dantzig-Wolfe Decomposition]]
### [[#^Karmarkar|Karmarkar Interior-Point Algorithm]]
## [[#^Bibliography|Bibliography]]
## [[#^Problems|Problems]]
### [[#^AssignedProblems|Assigned Problems Table]]
```

## Chapter Summary ^Summary

- The feasible region of an LP is convex; optimum solutions occur at feasible extreme (corner) points.
- Any feasible point in a convex polyhedron can be expressed as a convex combination of its extreme points.
- Extreme points correspond exactly to basic solutions of $\mathbf{AX}=\mathbf{b}$; feasibility adds $\mathbf{X}\ge \mathbf{0}$.
- The matrix simplex tableau highlights that $\mathbf{B}^{-1}$ drives the iteration; revised simplex improves numerical behavior.
- Revised simplex pivots by reduced costs (optimality) and the ratio test (feasibility), rather than full row operations.
- Practical solvers balance accuracy and speed via product-form or LU updates and periodic reinversion.
- With variable bounds, feasibility must consider both lower/upper limits; the bounded-variables method modifies the ratio logic.
- Duality provides bounds and certificates: weak duality, $\mathbf{Y}=\mathbf{C}_B\mathbf{B}^{-1}$ at optimum, and shadow-price interpretation.
- Parametric LP traces how optimal bases change across critical values as $\mathbf{C}(t)$ or $\mathbf{b}(t)$ varies.
- Additional advanced topics include capacitated network simplex, Dantzig-Wolfe decomposition, and interior-point methods.

## Real-Life Application—Optimal Ship Routing and Personnel Assignment for Naval Recruitment in Thailand ^Application

Thailand Navy recruits are drafted four times a year. A draftee reports to 1 of 34 local centers and is then transported by bus to one of four navy branch bases. From there, recruits are transported to the main naval base by ship. The docking facilities at the branch bases may restrict the type of ship that can visit each base. Branch bases have limited capacities but, as a whole, the four bases have sufficient capacity to accommodate all the draftees. During the summer of 1983, a total of 2929 draftees were transported from the drafting centers to the four branch bases and eventually to the main base. The problem deals with determining the optimal schedule for transporting the draftees, first from the drafting centers to the branch bases and then from the branch bases to the main base. The study uses a combination of linear and integer programming. Details of the study are presented in Case 5, Chapter 26 on the website.

### 7.1 SIMPLEX METHOD FUNDAMENTALS ^SimplexFundamentals

In linear programming, the feasible solution space forms a convex set if the line segment joining any two distinct feasible points also falls in the set. An extreme point of the convex set is a feasible point that cannot lie on a line segment joining any two distinct feasible points in the set. Actually, extreme points are the same as corner points, as used in Chapters 2, 3, and 4. ^Convexity

Figure 7.1 illustrates two sets. Set (a) is convex (with six extreme points), and set (b) is not.

The graphical LP solution given in Section 2.3 demonstrates that the optimum solution is always associated with a feasible extreme (corner) point of the solution space. This result makes sense intuitively, because every feasible point in the LP solution space can be determined as a function of its feasible extreme points. For example, in convex set (a) of Figure 7.1, a convex combination of the extreme points, ${\mathbf{X}}_{1},{\mathbf{X}}_{2},{\mathbf{X}}_{3},{\mathbf{X}}_{4}$ , ${\mathbf{X}}_{5}$ , and ${\mathbf{X}}_{6}$ , identifies any feasible point $\mathbf{X}$ as ^ConvexCombo

$$
\mathbf{X} = {\alpha }_{1}{\mathbf{X}}_{1} + {\alpha }_{2}{\mathbf{X}}_{2} + {\alpha }_{3}{\mathbf{X}}_{3} + {\alpha }_{4}{\mathbf{X}}_{4} + {\alpha }_{5}{\mathbf{X}}_{5} + {\alpha }_{6}{\mathbf{X}}_{6}
$$

$$
{\alpha }_{1} + {\alpha }_{2} + {\alpha }_{3} + {\alpha }_{4} + {\alpha }_{5} + {\alpha }_{6} = 1
$$

$$
{\alpha }_{\mathrm{i}} \geq  0, i = 1,2,\ldots ,6
$$

![bo_d56m4hbef24c73bhe5s0_1_405_200_496_276_0.jpg](bo_d56m4hbef24c73bhe5s0_1_405_200_496_276_0.jpg)

FIGURE 7.1

Examples of a convex and a nonconvex set

This observation shows that a finite number of extreme points completely define the infinite number of points in the solution space. This result is the crux of the simplex method. ^SimplexCrux

## Example 7.1-1 ^ExampleConvex

Show that the following set is convex:

$$
C = \left\{  {\left( {{x}_{1},{x}_{2}}\right)  \mid  {x}_{1} \leq  2,{x}_{2} \leq  3,{x}_{1} \geq  0,{x}_{2} \geq  0}\right\}
$$

Let ${\mathbf{X}}_{1} = \left\{  {{x}_{1}^{\prime },{x}_{2}^{\prime }}\right\}$ and ${\mathbf{X}}_{2} = \left\{  {{x}_{1}^{\prime \prime },{x}_{2}^{\prime \prime }}\right\}$ be any two distinct points in $C$ . If $C$ is convex, then $\mathbf{X} = \left( {{x}_{1},{x}_{2}}\right)  = {\alpha }_{1}{\mathbf{X}}_{1} + {\alpha }_{2}{\mathbf{X}}_{2},{\alpha }_{1} + {\alpha }_{2} = 1,{\alpha }_{1},{\alpha }_{2} \geq  0$ , must also be in $C$ . To show that this is true, we need to show that all the constraints of $C$ are satisfied by the line segment $\mathbf{X}$ -that is,

$$
\left. \begin{array}{l} {x}_{1} = {\alpha }_{1}{x}_{1}^{\prime } + {\alpha }_{2}{x}_{1}^{\prime \prime } \leq  {\alpha }_{1}\left( 2\right)  + {\alpha }_{2}\left( 2\right)  = 2 \\  {x}_{2} = {\alpha }_{1}{x}_{2}^{\prime } + {\alpha }_{2}{x}_{2}^{\prime \prime } \leq  {\alpha }_{1}\left( 3\right)  + {\alpha }_{2}\left( 3\right)  = 3 \end{array}\right\}   \Rightarrow  {x}_{1} \leq  2,{x}_{2} \leq  3
$$

Additionally, the nonnegativity conditions are satisfied because ${\alpha }_{1}$ and ${\alpha }_{2}$ are nonnegative.

#### 7.1.1 From Extreme Points to Basic Solutions ^ExtremeToBasic

It is convenient to express the general LP problem in equation form (see Section 3.1) using matrix notation. ${}^{1}$ Define $\mathbf{X}$ as an $n$ -vector representing the variables, $\mathbf{A}$ as an $\left( {m \times  n}\right)$ -matrix representing the constraint coefficients, $\mathbf{b}$ as a column vector representing the right-hand side, and $\mathbf{C}$ as an $n$ -vector representing the objective-function coefficients. The LP is then written as

$$
\text{ Maximize or minimize }z = \mathbf{{CX}}
$$

---

${}^{1}$ A review of matrix algebra is given in Appendix D on the website.

---

subject to

$$
\mathbf{{AX}} = \mathbf{b}
$$

$$
\mathbf{X} \geq  \mathbf{0}
$$

Using the format of Chapter 3, the rightmost $m$ elements of $\mathbf{X}$ represent the starting basic variables. Hence, the rightmost $m$ columns of $\mathbf{A}$ always form an identity matrix $\mathbf{I}$ .

A basic solution of $\mathbf{{AX}} = \mathbf{b}$ is determined by setting $n - m$ variables equal to zero, and then solving the resulting $m$ equations in the remaining $m$ unknowns, provided that the resulting solution is unique. Given this definition, the theory of linear programming establishes the following result between the geometric definition of extreme points and the algebraic definition of basic solutions:

$$
\text{ Extreme points of }\{ \mathbf{X} \mid  \mathbf{{AX}} = \mathbf{b}\}  \Leftrightarrow  \text{ Basic solutions of }\mathbf{{AX}} = \mathbf{b}
$$

The relationship means that the extreme points of the LP solution space are defined by the basic solutions of $\mathbf{{AX}} = \mathbf{b}$ , and vice versa. Thus, the basic solutions of $\mathbf{{AX}} = \mathbf{b}$ provide all the information needed to determine the optimum solution of the LP problem. Furthermore, the nonnegativity restriction, $\mathbf{X} \geq  \mathbf{0}$ , limits the search for the optimum to the feasible basic solutions only. ^ExtremeBasicEquivalence

To formalize the definition of a basic solution, the system $\mathbf{{AX}} = \mathbf{b}$ is written in vector form as

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{\mathbf{P}}_{j}{x}_{j} = \mathbf{b}
$$

The vector ${\mathbf{P}}_{j}$ is the $j$ th column of $\mathbf{A}$ . A subset of $m$ vectors forms a basis, $\mathbf{B}$ , if, and only if, the selected $m$ vectors are linearly independent. In this case, the matrix $\mathbf{B}$ is nonsingular. Defining ${\mathbf{X}}_{B}$ as an $m$ -vector of the basic variables, then

$$
\mathbf{B}{\mathbf{X}}_{B} = \mathbf{b}
$$

Using the inverse ${\mathbf{B}}^{-1}$ , the associated basic solution is

$$
{\mathbf{X}}_{B} = {\mathbf{B}}^{-1}\mathbf{b}
$$

If ${\mathbf{B}}^{-1}\mathbf{b} \geq  \mathbf{0}$ , then ${\mathbf{X}}_{B}$ is feasible. The remaining $n - m$ variables are nonbasic at zero level.

The previous result shows that in a system of $m$ equations and $n$ unknowns, the maximum number of (feasible and infeasible) basic solutions is $\left( \begin{array}{l} n \\  m \end{array}\right)  = \frac{n!}{m!\left( {n - m}\right) !}$ .

## Example 7.1-2 ^ExampleBasicSolutions

Determine all the basic feasible and infeasible solutions of the following system of equations:

$$
\left( \begin{array}{rrr} 1 & 3 &  - 1 \\  2 &  - 2 &  - 2 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \\  {x}_{3} \end{array}\right)  = \left( \begin{array}{l} 4 \\  2 \end{array}\right)
$$

The following table summarizes the results. The inverse of $\mathbf{B}$ is determined by one of the methods in Section D.2.7 on the website.

| B | $\mathbf{B}{\mathbf{X}}_{B} = \mathbf{b}$ | Solution | Type |
| --- | --- | --- | --- |
| $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$ | $\left( \begin{array}{rr} 1 & 3 \\  2 &  - 2 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 4 \\  2 \end{array}\right)$ | $\left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \frac{\frac{1}{4}}{\frac{1}{4}}\right. \; \left. \begin{array}{r} \frac{3}{8} \\   - \frac{1}{8} \end{array}\right) \left( \begin{array}{l} 4 \\  2 \end{array}\right)  = \left( \begin{array}{l} \frac{7}{4} \\  \frac{3}{4} \end{array}\right)$ | Feasible |
| $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3}}\right)$ | (Not a basis because ${\mathbf{P}}_{1}$ and ${\mathbf{P}}_{3}$ are dependent) |  |  |
| $\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ | $\left( \begin{array}{rr} 3 &  - 1 \\   - 2 &  - 2 \end{array}\right) \left( \begin{array}{l} {x}_{2} \\  {x}_{3} \end{array}\right)  = \left( \begin{array}{l} 4 \\  2 \end{array}\right)$ | $\left( \begin{array}{l} {x}_{2} \\  {x}_{3} \end{array}\right)  = \left( \begin{matrix} \frac{1}{4} \\   - \frac{1}{4} \end{matrix}\right. \; \left. {-\frac{1}{8}}\right) \left( \begin{array}{l} 4 \\  2 \end{array}\right)  = \left( \begin{array}{r} \frac{3}{4} \\   - \frac{7}{4} \end{array}\right)$ | Infeasible |

We can also investigate the problem by expressing it in vector form as follows:

$$
\left( \begin{array}{l} 1 \\  2 \end{array}\right) {x}_{1} + \left( \begin{array}{r} 3 \\   - 2 \end{array}\right) {x}_{2} + \left( \begin{array}{l}  - 1 \\   - 2 \end{array}\right) {x}_{3} = \left( \begin{array}{l} 4 \\  2 \end{array}\right)
$$

The two-dimensional vectors ${\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3}$ , and $\mathbf{b}$ can be represented generically as ${\left( {a}_{1},{a}_{2}\right) }^{T}$ . Figure 7.2 graphs these vectors on the $\left( {{a}_{1},{a}_{2}}\right)$ -plane. For example, for $\mathbf{b} = {\left( 4,2\right) }^{T},{a}_{1} = 4$ , and ${a}_{2} = 2$ .

Because we are dealing with two equations $\left( {m = 2}\right)$ , a basis includes exactly two vectors, selected from among ${\mathbf{P}}_{1},{\mathbf{P}}_{2}$ , and ${\mathbf{P}}_{3}$ . From Figure 7.2, the matrices $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$ and $\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ form bases because their associated vectors are independent. On the other hand, the vectors of the matrix $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3}}\right)$ are dependent, and hence the matrix is not a basis.

Algebraically, a (square) matrix forms a basis if its determinant is not zero (see Section D.2.5 on the website). The following computations show that the combinations $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$ and $\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ are bases, and the combination $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3}}\right)$ is not.

$$
\det \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)  = \det \left( \begin{array}{rr} 1 & 3 \\  2 &  - 2 \end{array}\right)  = \left( {1 \times   - 2}\right)  - \left( {3 \times  2}\right)  =  - 8 \neq  0
$$

$$
\det \left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)  = \det \left( \begin{array}{rr} 3 &  - 1 \\   - 2 &  - 2 \end{array}\right)  = \left( {3 \times   - 2}\right)  - \left( {-1 \times   - 2}\right)  =  - 8 \neq  0
$$

$$
\det \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3}}\right)  = \det \left( \begin{matrix} 1 &  - 1 \\  2 &  - 2 \end{matrix}\right)  = \left( {1 \times   - 2}\right)  - \left( {-1 \times  2}\right)  = 0
$$

![bo_d56m4hbef24c73bhe5s0_3_332_1552_619_621_0.jpg](bo_d56m4hbef24c73bhe5s0_3_332_1552_619_621_0.jpg)

Vector representation of LP solution space

#### 7.1.2 Generalized Simplex Tableau in Matrix Form ^TableauMatrix

This section develops the general simplex tableau in matrix form. This representation is the basis for subsequent developments in the chapter. ^TableauDerivation

Consider the LP in equation form:

$$
\text{ Maximize }z = \mathbf{{CX}}\text{ , subject to }\mathbf{{AX}} = \mathbf{b},\mathbf{X} \geq  \mathbf{0}
$$

Equivalently, the problem can be written as

$$
\left( \begin{matrix} 1 &  - \mathbf{C} \\  \mathbf{0} & \mathbf{A} \end{matrix}\right) \left( \begin{array}{l} z \\  \mathbf{X} \end{array}\right)  = \left( \begin{array}{l} 0 \\  \mathbf{b} \end{array}\right)
$$

Suppose that $\mathbf{B}$ is a feasible basis of the system $\mathbf{{AX}} = \mathbf{b},\mathbf{X} \geq  \mathbf{0}$ , and let ${\mathbf{X}}_{B}$ be the corresponding vector of basic variables and ${\mathbf{C}}_{B}$ its associated objective vector. Given all the nonbasic variables are zero, the solution is then computed as

$$
\left( \begin{matrix} z \\  {\mathbf{X}}_{B} \end{matrix}\right)  = {\left( \begin{matrix} 1 &  - {\mathbf{C}}_{B} \\  \mathbf{0} & \mathbf{B} \end{matrix}\right) }^{-1}\left( \begin{array}{l} 0 \\  \mathbf{b} \end{array}\right)  = \left( \begin{matrix} 1 & {\mathbf{C}}_{B}{\mathbf{B}}^{-1} \\  \mathbf{0} & {\mathbf{B}}^{-1} \end{matrix}\right) \left( \begin{array}{l} 0 \\  \mathbf{b} \end{array}\right)  = \left( \begin{matrix} {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b} \\  {\mathbf{B}}^{-1}\mathbf{b} \end{matrix}\right)
$$

(Inversion of partitioned matrices is given in Section D.2.7. on the website.)

The complete simplex tableau in matrix form can be derived from the original equations as

$$
\left( \begin{matrix} 1 & {\mathbf{C}}_{B}{\mathbf{B}}^{-1} \\  \mathbf{0} & {\mathbf{B}}^{-1} \end{matrix}\right) \left( \begin{matrix} 1 &  - \mathbf{C} \\  \mathbf{0} & \mathbf{A} \end{matrix}\right) \left( \begin{matrix} z \\  \mathbf{X} \end{matrix}\right)  = \left( \begin{matrix} 1 & {\mathbf{C}}_{B}{\mathbf{B}}^{-1} \\  \mathbf{0} & {\mathbf{B}}^{-1} \end{matrix}\right) \left( \begin{array}{l} 0 \\  \mathbf{b} \end{array}\right)
$$

Matrix manipulations then yield the following equations:

$$
\left( \begin{matrix} 1 & {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{A} - \mathbf{C} \\  \mathbf{0} & {\mathbf{B}}^{-1}\mathbf{A} \end{matrix}\right) \left( \begin{matrix} z \\  \mathbf{X} \end{matrix}\right)  = \left( \begin{matrix} {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b} \\  {\mathbf{B}}^{-1}\mathbf{b} \end{matrix}\right)
$$

Given the $j$ th vector ${\mathbf{P}}_{j}$ of $\mathbf{A}$ , the simplex tableau column associated with variable ${x}_{j}$ can be written as ^TableauColumn

| Basic | ${x}_{j}$ | Solution |
| --- | --- | --- |
| $z$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{P}}_{j} - {c}_{j}$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b}$ |
| ${\mathbf{X}}_{B}$ | ${\mathbf{B}}^{-1}{\mathbf{P}}_{j}$ | ${\mathbf{B}}^{-1}\mathbf{b}$ |

In fact, the tableau above is the same one used in Chapter 3 (see Problem 7-13). It also includes all the primal-dual relationships developed in Section 4.2.4.

Remarks. Look at the matrix form of the simplex tableau just given. You will notice that the inverse, ${\mathbf{B}}^{-1}$ , is the only element that changes from one iteration to the next-in the sense that all the other elements can be plucked directly from the original data. That means that the entire tableau can be generated from the original data once the associated inverse ${\mathbf{B}}^{-1}$ is known. But the matrix-format tableau reveals a deeper root for determining ${\mathbf{B}}^{-1}$ , namely,

$$
\left( \begin{matrix} \text{ Basic solution } \\  {\mathbf{X}}_{B} \\  \text{ at iteration }i \end{matrix}\right)  \rightarrow  \left( \begin{matrix} \text{ Original } \\  \text{ constraint columns } \\  \text{ of }{\mathbf{X}}_{B} \end{matrix}\right)  \rightarrow  \left( \begin{matrix} \text{ Basis }\mathbf{B}\text{ for } \\  \text{ iteration }i \end{matrix}\right)  \rightarrow  \left( \begin{matrix} \text{ Inverse }{\mathbf{B}}^{-1}\text{ for } \\  \text{ iteration }i \end{matrix}\right)
$$

That means that, once ${\mathbf{X}}_{B}$ is known, all the elements of the tableau can be determined directly from the original data of the model. Unlike the tableau method in Chapter 3 that propagates roundoff error when the next tableau is generated from the immediately preceding one, roundoff error in an iteration can be kept in check by computing ${\mathbf{B}}^{-1}$ from the original constraint columns. This result is one of the main reasons for the development of the revised simplex method in Section 7.2. Nonetheless, the golden rule in matrix algebra is to avoid inverting a matrix when possible because calculating ${\mathbf{B}}^{-1}$ anew from original data is very costly computationally. As will be explained in Section 7.2.3, it is essential to strike a balance between accuracy and computational speed by modulating the frequency of computing the inverse during the course of the simplex iterations ^InverseTradeoff

## Example 7.1-3 ^ExampleTableau

---

Consider the following LP:

$$
\text{ Maximize }z = {x}_{1} + 4{x}_{2} + 7{x}_{3} + 5{x}_{4}
$$

subject to

$$
2{x}_{1} + {x}_{2} + 2{x}_{3} + 4{x}_{4} = {10}
$$

$$
3{x}_{1} - {x}_{2} - 2{x}_{3} + 6{x}_{4} = 5
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

Generate the simplex tableau associated with the basis $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$ .

		Given $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$ , then ${\mathbf{X}}_{B} = {\left( {x}_{1},{x}_{2}\right) }^{T}$ and ${\mathbf{C}}_{B} = \left( {1,4}\right)$ . Thus,

$$
{\mathbf{B}}^{-1} = {\left( \begin{array}{rr} 2 & 1 \\  3 &  - 1 \end{array}\right) }^{-1} = \left( \begin{array}{rr} \frac{1}{5} & \frac{1}{5} \\  \frac{3}{5} &  - \frac{2}{5} \end{array}\right)
$$

We then get

$$
{\mathbf{X}}_{B} = \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = {\mathbf{B}}^{-1}\mathbf{b} = \left( \begin{array}{rr} \frac{1}{5} & \frac{1}{5} \\  \frac{3}{5} &  - \frac{2}{5} \end{array}\right) \left( \begin{array}{l} {10} \\  5 \end{array}\right)  = \left( \begin{array}{l} 3 \\  4 \end{array}\right)
$$

			To compute the constraint columns in the body of the tableau, we have

$$
{\mathbf{B}}^{-1}\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)  = \left( \begin{array}{rr} \frac{1}{5} & \frac{1}{5} \\  \frac{3}{5} &  - \frac{2}{5} \end{array}\right) \left( \begin{array}{rrrr} 2 & 1 & 2 & 4 \\  3 &  - 1 &  - 2 & 6 \end{array}\right)  = \left( \begin{array}{llll} 1 & 0 & 0 & 2 \\  0 & 1 & 2 & 0 \end{array}\right)
$$

Next, we compute the objective row as

$$
{\mathbf{C}}_{B}\left( {{\mathbf{B}}^{-1}\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{2},{\mathbf{P}}_{4}}\right) }\right)  - \mathbf{C} = \left( {1,4}\right) \left( \begin{array}{llll} 1 & 0 & 0 & 2 \\  0 & 1 & 2 & 0 \end{array}\right)  - \left( {1,4,7,5}\right)  = \left( {0,0,1, - 3}\right)
$$

---

Finally, we compute the value of the objective function as

$$
z = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b} = {\mathbf{C}}_{B}{\mathbf{X}}_{B} = \left( {1,4}\right) \left( \begin{array}{l} 3 \\  4 \end{array}\right)  = {19}
$$

Thus, the entire tableau can be summarized as follows.

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | Solution |
| --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | 1 | -3 | 19 |
| ${x}_{1}$ | 1 | 0 | 0 | 2 | 3 |
| ${x}_{2}$ | 0 | 1 | 2 | 0 | 4 |

### 7.2 REVISED SIMPLEX METHOD ^RevisedSimplex

Section 7.1.1 shows that the optimum solution of a linear program is always associated with a basic (feasible) solution. The simplex method search moves from a feasible basis, $\mathbf{B}$ , to a better (actually, no-worse) basis, ${\mathbf{B}}_{\text{ next }}$ , until the optimum basis is reached.

The iterative steps of the revised simplex method are exactly the same as in the tableau simplex method presented in Chapter 3. The main difference is that the computations in the revised method are based on matrix manipulations rather than on row operations. As such, the entire simplex tableau can be computed from the original data and the current inverse (see Section 7.1.2), thus improving the accuracy of computing ${\mathbf{B}}^{-1}$ and ameliorating the machine roundoff error problem. In the tableau simplex method of Chapter 3, generating a new tableau from the immediately preceding one propagates roundoff error rather rapidly. ^RevisedOverview

#### 7.2.1 Development of the Optimality and Feasibility Conditions ^OptimalityFeasibility

The general LP problem can be written as

$$
\text{ Maximize or minimize }z = \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j}\text{ subject to }\mathop{\sum }\limits_{{j = 1}}^{n}{\mathbf{P}}_{j}{x}_{j} = \mathbf{b},{x}_{j} \geq  0, j = 1,2,\ldots , n
$$

Given the basic vector ${\mathbf{X}}_{B}$ , its basis $\mathbf{B}$ , and its objective vector ${\mathbf{C}}_{B}$ , the general simplex tableau developed in Section 7.1.2 shows that any simplex iteration can be represented by the following equations:

$$
z + \mathop{\sum }\limits_{{j = 1}}^{n}\left( {{z}_{j} - {c}_{j}}\right) {x}_{j} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b}
$$

$$
{\left( {\mathbf{X}}_{B}\right) }_{i} + \mathop{\sum }\limits_{{j = 1}}^{n}{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}{x}_{j} = {\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i}
$$

The reduced cost of ${x}_{j}$ , as defined in Section 4.3.2, is computed as ^ReducedCost

$$
{z}_{j} - {c}_{j} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{P}}_{j} - {c}_{j}
$$

The notation ${\left( \mathbf{V}\right) }_{i}$ represents element $i$ of the vector $\mathbf{V}$ .

Optimality Condition. The $z$ -equation shows that, in the case of maximization, an increase in nonbasic ${x}_{j}$ above its current zero value can improve the value of $z$ (relative to its current value, ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b}$ ) only if ${z}_{j} - {c}_{j} < 0$ . For minimization, the condition is ${z}_{j} - {c}_{j} > 0$ . Thus, the entering vector is selected as the nonbasic vector with the most negative (most positive) ${z}_{j} - {c}_{j}$ in case of maximization (minimization). ^OptimalityRule

Feasibility Condition. Given the entering vector ${\mathbf{P}}_{j}$ as determined by the optimality condition, the constraint equations reduce to ^FeasibilityRule

$$
{\left( {\mathbf{X}}_{B}\right) }_{i} = {\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i} - {\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}{x}_{j}
$$

(Recall that the remaining $n - 1$ nonbasic variables are zero.) The idea is to (attempt to) increase ${x}_{j}$ above zero level, replacing one of the current basic variables. The extent to which ${x}_{j}$ is increased is dictated by the requirement that all ${\left( {\mathbf{X}}_{B}\right) }_{i}$ remain nonnegative - namely,

$$
{\left( {\mathbf{X}}_{B}\right) }_{i} = {\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i} - {\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}{x}_{j} \geq  \mathbf{0}
$$

If ${\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i} > 0$ for at least one $i$ , the nonnegativity condition, ${\left( {\mathbf{X}}_{B}\right) }_{i} \geq  \mathbf{0}$ for all $i$ , sets the limit on the maximum increase in the value of the entering variable ${x}_{j}$ - namely,

$$
{x}_{j} = \mathop{\min }\limits_{i}\left\{  {\left. \frac{{\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i}}{{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}}\right| \;{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i} > 0}\right\}
$$

Suppose that ${\left( {\mathbf{X}}_{B}\right) }_{k}$ is the basic variable that corresponds to the minimum ratio. It then follows that ${\mathbf{P}}_{k}$ must be the leaving vector, and its associated (basic) variable must become nonbasic (at zero level) in the next simplex iteration. ^RatioTest

#### 7.2.2 Revised Simplex Algorithm ^RevisedAlgorithm

Step 0. Construct a starting basic feasible solution, and let $\mathbf{B}$ and ${\mathbf{C}}_{B}$ be its associated basis and objective coefficients vector, respectively. ^AlgorithmSteps

Step 1. Compute the inverse ${\mathbf{B}}^{-1}$ of the basis $\mathbf{B}$ by using an appropriate inversion method. ${}^{2}$

Step 2. For each nonbasic vector ${\mathbf{P}}_{j}$ , compute

$$
{z}_{j} - {c}_{j} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{P}}_{j} - {c}_{j}
$$

If ${z}_{j} - {c}_{j} \geq  0$ in maximization ( $\leq  0$ in minimization) for all nonbasic vectors, stop; the optimal solution is ${\mathbf{X}}_{B} = {\mathbf{B}}^{-1}\mathbf{b}, z = {\mathbf{C}}_{B}{\mathbf{X}}_{B}$ .

---

${}^{2}$ In most LP presentations, including the first six editions of this book, the product form method for inverting a basis (see Section D.2.7 on the website) is integrated in the revised simplex algorithm because the product form lends itself readily to the revised simplex computations - namely, successive bases differ in exactly one column. This detail has been removed from this presentation because it makes the algorithm appear more complex than it really is. Moreover, the product form is rarely used in the development of commercial LP codes. Instead (variants of) the more efficient ${LU}$ decomposition method is used. We will elaborate on the use of the product form and LU decomposition later in Section 7.2.3; specifically, see the Aha! Moment at the end of Section 7.2.3. (Incidentally, TORA matrix inversion is based on LU decomposition.)

---

Else, determine the entering vector ${\mathbf{P}}_{j}$ having the most negative (positive) ${z}_{j} - {c}_{j}$ in case of maximization (minimization) among all nonbasic vectors.

Step 3. Compute ${\mathbf{B}}^{-1}{\mathbf{P}}_{j}$ . If all the elements of ${\mathbf{B}}^{-1}{\mathbf{P}}_{j}$ are negative or zero, stop; the solution is unbounded. Else, use the ratio test to determine the leaving vector ${\mathbf{P}}_{i}$ .

Step 4. Form the next basis by replacing the leaving vector ${\mathbf{P}}_{i}$ with the entering vector ${\mathbf{P}}_{j}$ in the current basis $\mathbf{B}$ . Go to step 1 to start a new iteration.

## Example 7.2-1 ^ExampleRevised

The Reddy Mikks model (Section 2.1) is solved by the revised simplex algorithm. The same model was solved by the tableau method in Section 3.3.2. A comparison shows that the two methods are one and the same.

The equation form of the Reddy Mikks model can be expressed in matrix form as

$$
\text{ maximize }z = \left( {5,4,0,0,0,0}\right) {\left( {x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5},{x}_{6}\right) }^{T}
$$

subject to

$$
\left( \begin{array}{rrrrrr} 6 & 4 & 1 & 0 & 0 & 0 \\  1 & 2 & 0 & 1 & 0 & 0 \\   - 1 & 1 & 0 & 0 & 1 & 0 \\  0 & 1 & 0 & 0 & 0 & 1 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \\  {x}_{3} \\  {x}_{4} \\  {x}_{5} \\  {x}_{6} \end{array}\right)  = \left( \begin{array}{r} {24} \\  6 \\  1 \\  2 \end{array}\right)
$$

$$
{x}_{1},{x}_{2},\ldots ,{x}_{6} \geq  0
$$

The notation $\mathbf{C} = \left( {{c}_{1},{c}_{2},\ldots ,{c}_{6}}\right)$ represents the objective-function coefficients, and $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},\ldots }\right.$ , and ${\mathbf{P}}_{6}$ ) represent the columns vectors of the constraint equations. The right-hand side of the constraints is the vector $\mathbf{b}$ .

In the following computations, we will give the algebraic formula for each step and its final numeric answer, without detailing the calculations. You will find it instructive to fill in the gaps in each step.

Iteration 0

$$
{\mathbf{X}}_{{B}_{0}} = \left( {{x}_{3},{x}_{4},{x}_{5},{x}_{6}}\right) ,{\mathbf{C}}_{{B}_{0}} = \left( {0,0,0,0}\right)
$$

$$
{\mathbf{B}}_{0} = \left( {{\mathbf{P}}_{3},{\mathbf{P}}_{4},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)  = \mathbf{I},{\mathbf{B}}_{0}^{-1} = \mathbf{I}
$$

Thus,

$$
{\mathbf{X}}_{{B}_{0}} = {\mathbf{B}}_{0}^{-1}\mathbf{b} = {\left( {24},6,1,2\right) }^{T}, z = {\mathbf{C}}_{{B}_{0}}{\mathbf{X}}_{{B}_{0}} = 0
$$

## Optimality computations:

$$
{\mathbf{C}}_{{B}_{0}}{\mathbf{B}}_{0}^{-1} = \left( {0,0,0,0}\right)
$$

$$
{\left\{  {z}_{j} - {c}_{j}\right\}  }_{j = 1,2} = {\mathbf{C}}_{{B}_{0}}{\mathbf{B}}_{0}^{-1}\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)  - \left( {{c}_{1},{c}_{2}}\right)  = \left( {-5, - 4}\right)
$$

Thus, ${\mathbf{P}}_{1}$ is the entering vector.

Feasibility computations:

$$
{\mathbf{X}}_{{B}_{0}} = {\left( {x}_{3},{x}_{4},{x}_{5},{x}_{6}\right) }^{T} = {\left( {24},6,1,2\right) }^{T}
$$

$$
{\mathbf{B}}_{0}^{-1}{\mathbf{P}}_{1} = {\left( 6,1, - 1,0\right) }^{T}
$$

Hence,

$$
{x}_{1} = \min \left\{  {\frac{24}{6},\frac{6}{1},-, - }\right\}   = \min \{ 4,6, - , - \}  = 4,
$$

and ${\mathbf{P}}_{3}$ becomes the leaving vector.

The results given above can be summarized in the familiar simplex tableau format, essentially demonstrating that the two methods are the same.

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | -5 | -4 | 0 | 0 | 0 | 0 | 0 |
| ${x}_{3}$ | 6 |  |  |  |  |  | 24 |
| ${x}_{4}$ | 1 |  |  |  |  |  | 6 |
| ${x}_{5}$ | -1 |  |  |  |  |  | 1 |
| ${x}_{6}$ | 0 |  |  |  |  |  | 2 |

Iteration 1

$$
{\mathbf{X}}_{{B}_{1}} = \left( {{x}_{1},{x}_{4},{x}_{5},{x}_{6}}\right) ,{\mathbf{C}}_{{B}_{1}} = \left( {5,0,0,0}\right)
$$

$$
{\mathbf{B}}_{1} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)
$$

$$
= \left( \begin{array}{rrrr} 6 & 0 & 0 & 0 \\  1 & 1 & 0 & 0 \\   - 1 & 0 & 1 & 0 \\  0 & 0 & 0 & 1 \end{array}\right)
$$

By using an appropriate inversion method (see Section D.2.7 on the website), then

$$
{\mathbf{B}}_{1}^{-1} = \left( \begin{array}{rrrr} \frac{1}{6} & 0 & 0 & 0 \\   - \frac{1}{6} & 1 & 0 & 0 \\  \frac{1}{6} & 0 & 1 & 0 \\  0 & 0 & 0 & 1 \end{array}\right)
$$

Thus,

$$
{\mathbf{X}}_{{B}_{1}} = {\mathbf{B}}_{1}^{-1}\mathbf{b} = {\left( 4,2,5,2\right) }^{T}, z = {\mathbf{C}}_{{B}_{1}}{\mathbf{X}}_{{B}_{1}} = {20}
$$

Optimality computations:

$$
{\mathbf{C}}_{{B}_{1}}{\mathbf{B}}_{1}^{-1} = \left( {\frac{5}{6},0,0,0}\right)
$$

$$
{\left\{  {z}_{j} - {c}_{j}\right\}  }_{j = 2,3} = {\mathbf{C}}_{{B}_{1}}{\mathbf{B}}_{1}^{-1}\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)  - \left( {{c}_{2},{c}_{3}}\right)  = \left( {-\frac{2}{3},\frac{5}{6}}\right)
$$

Thus, ${\mathbf{P}}_{2}$ is the entering vector.

## Feasibility computations:

$$
{\mathbf{X}}_{{B}_{1}} = {\left( {x}_{1},{x}_{4},{x}_{5},{x}_{6}\right) }^{T} = {\left( 4,2,5,2\right) }^{T}
$$

$$
{\mathbf{B}}_{1}^{-1}{\mathbf{P}}_{2} = {\left( \frac{2}{3},\frac{4}{3},\frac{5}{3},1\right) }^{T}
$$

Hence,

$$
{x}_{2} = \min \left\{  {\frac{4}{\frac{2}{3}},\frac{2}{\frac{4}{3}},\frac{5}{\frac{5}{3}},\frac{2}{1}}\right\}   = \min \{ 6,\frac{3}{2},3,2\}  = \frac{3}{2}
$$

The vector ${\mathbf{P}}_{4}$ leaves the basis. (You will find it helpful to summarize these results in the simplex tableau format as we did in iteration 0.)

Iteration 2

$$
{\mathbf{X}}_{{B}_{2}} = {\left( {x}_{1},{x}_{2},{x}_{5},{x}_{6}\right) }^{T},{\mathbf{C}}_{{B}_{2}} = \left( {5,4,0,0}\right)
$$

$$
{\mathbf{B}}_{2} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)
$$

$$
= \left( \begin{array}{rrrr} 6 & 4 & 0 & 0 \\  1 & 2 & 0 & 0 \\   - 1 & 1 & 1 & 0 \\  0 & 1 & 0 & 1 \end{array}\right)
$$

Hence,

$$
{\mathbf{B}}_{2}^{-1} = \left( \begin{array}{rrrr} \frac{1}{4} &  - \frac{1}{2} & 0 & 0 \\   - \frac{1}{8} & \frac{3}{4} & 0 & 0 \\  \frac{3}{8} &  - \frac{5}{4} & 1 & 0 \\  \frac{1}{8} &  - \frac{3}{4} & 0 & 1 \end{array}\right)
$$

Thus,

$$
{\mathbf{X}}_{{B}_{2}} = {\mathbf{B}}_{2}^{-1}\mathbf{b} = {\left( 3,\frac{3}{2},\frac{5}{2},\frac{1}{2}\right) }^{T}, z = {\mathbf{C}}_{{B}_{2}}{\mathbf{X}}_{{B}_{2}} = {21}
$$

Optimality computations:

$$
{\mathbf{C}}_{{B}_{2}}{\mathbf{B}}_{2}^{-1} = \left( {\frac{3}{4},\frac{1}{2},0,0}\right)
$$

$$
{\left\{  {z}_{j} - {c}_{j}\right\}  }_{j = 3,4} = {\mathbf{C}}_{{B}_{2}}{\mathbf{B}}_{2}^{-1}\left( {{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)  - \left( {{c}_{3},{c}_{4}}\right)  = \left( {\frac{3}{4},\frac{1}{2}}\right)
$$

Thus, ${\mathbf{X}}_{{B}_{2}}$ is optimal, and the computations end.

## Summary of optimal solution:

$$
{x}_{1} = 3,{x}_{2} = {1.5}, z = {21}
$$

#### 7.2.3 Computational Issues in the Revised Simplex Method ^ComputationalIssues

There are two overriding issues regarding the revised simplex algorithm: (1) computational accuracy (also known as numerical stability), and (2) computational speed. Computing the inverse ${\mathbf{B}}^{-1}$ from the original data will increase computational accuracy but it will slow down the execution of the revised simplex algorithm. In fact, the golden rule in numerical analysis is never to invert a matrix unless absolutely necessary. Available LP solvers follow this rule. ^AccuracySpeed

The revised simplex method utilizes two distinct methods for dealing with the inverse ${\mathbf{B}}^{-1}$ :

1. The product form ^ProductForm

2. The LU decomposition ${}^{3}$ ^LUDecomposition

The product form is detailed in Section D.2.7 in Appendix D on the website.

The idea of product form is to construct an elementary matrix, $\mathbf{E}$ , using current inverse, ${\mathbf{B}}^{-1}$ , and the constraint column, ${\mathbf{P}}_{j}$ , of the entering vector, $j$ . The new inverse is then computed as

$$
{\mathbf{B}}_{\text{ next }}^{-1} = \mathbf{E}{\mathbf{B}}_{\text{ current }}^{-1}
$$

Since the initial basis, ${\mathbf{B}}_{0}$ , is always an identity matrix, the inverse basis at iteration $k$ effectively can be computed as

$$
{\mathbf{B}}_{k}^{-1} = {\mathbf{E}}_{1}{\mathbf{E}}_{2}\ldots {\mathbf{E}}_{k}
$$

The LU decomposition calls for decomposing the basis, B, into lower and upper triangular matrices, $\mathbf{L}$ and $\mathbf{U}$ , respectively, such that,

$$
\mathbf{B} = \mathbf{{LU}}
$$

Hence

$$
{\mathbf{B}}^{-1} = {\mathbf{U}}^{-1}{\mathbf{L}}^{-1}
$$

The matrix $\mathbf{L}$ has all-zero above-diagonal elements and the matrix $\mathbf{U}$ has all-zero below-diagonal elements. Matrix $\mathbf{U}$ is determined by applying appropriate row operations to basis $\mathbf{B}$ , and the same process automatically yields the below-diagonal elements of $\mathbf{L}$ . As in the product form method, ${\mathbf{B}}_{\text{ next }}^{-1}$ is determined by modifying ${\mathbf{L}}_{\text{ current }}^{-1}$ and ${\mathbf{U}}_{\text{ current }}^{-1}$ appropriately using information from the current entering vector ${\mathbf{P}}_{j}$ .

To avoid inverting $\mathbf{B}$ anew in each iteration (which is very costly computationally), the strategy in both methods is to keep on generating ${\mathbf{B}}_{\text{ next }}^{-1}$ from the immediately preceding inverse so long as computational accuracy is not impaired to the point of distorting the original model. When this happens, ${\mathbf{B}}_{\text{ current }}^{-1}$ loses its accuracy, and it is time to replace it with a more accurate one by constructing ${\mathbf{B}}_{\text{ next }}$ associated with ${\mathbf{X}}_{B\left( \text{ next }\right) }$ from the original column vectors ${\mathbf{P}}_{j}$ . The newly constructed basis ${\mathbf{B}}_{\text{ next }}$ is then inverted and its inverse is used as a "refreshed" start in successive simplex iterations until it again loses its accuracy. And so continues the process until the simplex method terminates. ${}^{4}$ ^RefreshInverse

How is ${\mathbf{B}}_{\text{ current }}^{-1}$ judged to be no longer accurate during the course of the simplex iterations (thus signaling the need to start a new cycle with a refreshed new inverse)?

---

${}^{3}$ See J. Bunch and J. Hopcroft,"Triangular Factorization and Inversion by Fast Matrix Multiplication," Mathematics of Computation, Vol. 28, pp. 231-236, 1974.

${}^{4}$ See E. Hellerman and D. Rarick,"Reinversion with the Preassigned Pivot Procedure," Mathematical Programming, Vol. 1, pp. 195-216, 1971.

---

Roundoff error manifests itself adversely in elements of the simplex tableau that are known to be zero; namely, in any iteration, LP theory dictates: ^RoundoffError

1. The objective coefficients for all basic variables ${\mathbf{X}}_{B}$ must be zero, that is, ${\begin{Vmatrix}{z}_{j} - {c}_{j}\end{Vmatrix}}_{{\mathbf{X}}_{B}} = \mathbf{0}$ . (Incidentally, ${\begin{Vmatrix}{z}_{j} - {c}_{j}\end{Vmatrix}}_{{\mathbf{X}}_{B}} = \mathbf{0}$ represents the dual constraints associated with the basic variables.)

2. The difference between the left- and right-hand sides of (primal) LP constraints must be zero, that is, $\parallel \mathbf{A}\mathbf{X} - \mathbf{b}\parallel  = \mathbf{0}$ .

If these values exceed a specified threshold $\varepsilon$ , the roundoff error poses problems and the inverse must be refreshed.

The common thread between the product form and the LU decomposition methods is the cyclical need to refresh the inverse basis. It turned out, from reported computational experiences, that the LU method boasts approximately four times the cycle length between reinversions as the product form. For this reason, practically all current-day LP solvers use (a variant of) the LU method.

## Aha! Moment: Early-On Implementations of the Simplex Algorithm, or How the Use of the Product Form of the Inverse Came About ${}^{5}$ ^AhaHistory

The first reported nontrivial application of Dantzig's simplex method was a 21-constraint by 74-variable instance of the diet problem (see Example 2.2-2), and it took only about 120 person-days to calculate the optimal solution. But that was the era when hand computations were the norm. Then in the early 1950s, conglomerations of wired panels, punched cards, "spaghetti" wires, and vacuum tubes ushered the birth of computers. But with computers in such a "primitive" state, the execution of the simplex algorithm was extremely slow particularly because each iteration required an explicit calculation of the basis inverse (very costly computationally, even with present-day computers). Discouraged by the results, Dantzig thought that the computational future of his simplex algorithm was doomed. Then his colleague W. Orchard-Hay suggested that he use the product form method (instead of Gauss-Jordan row operations) to generate the successive inverses. The use of the product form led to a more successful implementation of the simplex algorithm (it took only about 8 hrs to solve the 26-constraint by 74-variable instance of the diet problem-nothing to cheer about, but it was, to say the least, an in-leaps-and-bounds improvement over the hand solution of the same instance in 120 person-days!). And for over two decades, the product form remained the driving engine for computing the inverse in the simplex algorithm, until it was supplanted by the more efficient LU decomposition method.

### 7.3 BOUNDED-VARIABLES ALGORITHM ^BoundedVariables

In LP models, variables may have explicit upper and lower bounds. For example, in production facilities, lower and upper bounds can represent the minimum and maximum demands for certain products. Bounded variables also arise prominently in solving integer programs by the branch-and-bound algorithm (see Section 9.3.1).

---

${}^{5}$ Robert E. Bixby,"A Brief History of Linear and Mixed-Integer Programming Computation," Documenta Mathematica, Extra Vol. ISMP, pp. 107-121, 2012.

---

The bounded algorithm is efficient computationally because it accounts implicitly for the bounds. We consider the lower bounds first because their treatment is simple. Given $\mathbf{X} \geq  \mathbf{L}$ , substitute $\mathbf{X} = \mathbf{L} + {\mathbf{X}}^{\prime },{\mathbf{X}}^{\prime } \geq  \mathbf{0}$ throughout, and solve the problem in terms of ${\mathbf{X}}^{\prime }$ (whose lower bound now equals zero). The original $\mathbf{X}$ is then determined by back-substitution, $\mathbf{X} = {\mathbf{X}}^{\prime } + \mathbf{L} \geq  0$ . ^LowerBounds

Next, consider the upper-bounding constraints, $\mathbf{X} \leq  \mathbf{U}$ . The idea of direct substitution (i.e., $\mathbf{X} = \mathbf{U} - {\mathbf{X}}^{\prime \prime },{\mathbf{X}}^{\prime \prime } \geq  \mathbf{0}$ ) is not correct because back-substitution, $\mathbf{X} = \mathbf{U} - {\mathbf{X}}^{\prime \prime }$ , does not ensure that $\mathbf{X}$ will remain nonnegative. A different procedure is thus needed. ^UpperBounds

Define the upper-bounded LP model as ^BoundedModel

$$
\text{ Maximize }z = \{ \mathbf{{CX}} \mid  \left( {\mathbf{A},\mathbf{I}}\right) \mathbf{X} = \mathbf{b},\mathbf{0} \leq  \mathbf{X} \leq  \mathbf{U}\}
$$

The bounded algorithm uses only the main constraints $\left( {\mathbf{A},\mathbf{I}}\right) \mathbf{X} = \mathbf{b},\mathbf{X} \geq  \mathbf{0}$ . It accounts for the upper bounds, $\mathbf{X} \leq  \mathbf{U}$ , implicitly by modifying the feasibility condition. ^ModifiedFeasibility

Let ${\mathbf{X}}_{B} = {\mathbf{B}}^{-1}\mathbf{b}$ be a current basic feasible solution of $\left( {\mathbf{A},\mathbf{I}}\right) \mathbf{X} = \mathbf{b},\mathbf{X} \geq  \mathbf{0}$ , and assume that ${\mathbf{P}}_{j}$ is the entering vector (as determined by the regular optimality condition). Then, given that all the nonbasic variables are zero, the constraint equation of the $i$ th basic variable is

$$
{\left( {\mathbf{X}}_{B}\right) }_{i} = {\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i} - {\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}{x}_{j}
$$

When the entering variable ${x}_{j}$ increases above zero level, ${\left( {\mathbf{X}}_{\mathbf{B}}\right) }_{i}$ will increase or decrease depending on whether ${\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}$ is negative or positive, respectively. Thus, in determining the value of the entering vector ${\mathbf{P}}_{j}$ , three conditions must be satisfied: ^ThetaRules

1. The basic variable remains nonnegative - that is, ${\left( {\mathbf{X}}_{\mathbf{B}}\right) }_{i} \geq  0$ .

2. The basic variable ${\left( {\mathbf{X}}_{B}\right) }_{i}$ does not exceed its upper bound - that is, ${\left( {\mathbf{X}}_{B}\right) }_{i} \leq  {\left( {\mathbf{U}}_{B}\right) }_{i}$ , where ${\mathbf{U}}_{B}$ comprises the elements of $\mathbf{U}$ corresponding to ${\mathbf{X}}_{B}$ .

3. The entering variable ${x}_{j}$ cannot assume a value larger than its upper bound - that is, ${x}_{j} \leq  {\mathrm{u}}_{j}$ , where ${u}_{j}$ is the $j$ th element of $\mathbf{U}$ .

The first condition ${\left( {\mathbf{X}}_{\mathbf{B}}\right) }_{i} \geq  0$ is the same as in the regular simplex method. It yields

$$
{x}_{j} \leq  {\theta }_{1} = \mathop{\min }\limits_{i}\left\{  {\left. \frac{{\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i}}{{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}}\right| \;{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i} > 0}\right\}
$$

The second condition ${\left( {\mathbf{X}}_{\mathbf{B}}\right) }_{i} \leq  {\left( {\mathbf{U}}_{\mathbf{B}}\right) }_{i}$ specifies that

$$
{\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i} - {\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}{x}_{j} \leq  {\left( {\mathbf{U}}_{B}\right) }_{i}
$$

It is satisfied if

$$
{x}_{j} \leq  {\theta }_{2} = \mathop{\min }\limits_{i}\left\{  {\left. \frac{{\left( {\mathbf{B}}^{-1}\mathbf{b}\right) }_{i} - {\left( {\mathbf{U}}_{B}\right) }_{i}}{{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i}}\right| \;{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{i} < 0}\right\}
$$

Combining the three restrictions, ${x}_{j}$ enters the solution at the level that satisfies all three conditions - that is,

$$
{x}_{j} = \min \left\{  {{\theta }_{1},{\theta }_{2},{u}_{j}}\right\}
$$

The change of basis for the next iteration depends on whether ${x}_{j}$ enters the solution at level ${\theta }_{1},{\theta }_{2}$ , or ${u}_{j}$ . Assuming that ${\left( {\mathbf{X}}_{B}\right) }_{r}$ is the leaving variable, then we have the following rules:

1. ${x}_{j} = {\theta }_{1} : {\left( {\mathbf{X}}_{B}\right) }_{r}$ leaves the basic solution (becomes nonbasic) at level zero. The new iteration is generated using the regular simplex method with ${x}_{j}$ and ${\left( {\mathbf{X}}_{B}\right) }_{r}$ as the entering and the leaving variables, respectively.

2. ${x}_{j} = {\theta }_{2} : {\left( {\mathbf{X}}_{B}\right) }_{r}$ becomes nonbasic at its upper bound. The new iteration is generated as in the case of ${x}_{j} = {\theta }_{1}$ , with one modification that accounts for the fact that ${\left( {\mathbf{X}}_{B}\right) }_{r}$ will be nonbasic at upper bound. Because the values of ${\theta }_{1}$ and ${\theta }_{2}$ require all nonbasic variables to be at zero level (convince yourself that this is the case!), the new nonbasic ${\left( {\mathbf{X}}_{B}\right) }_{r}$ at upper bound is converted to a nonbasic variable at zero level. This is achieved by using the substitution ${\left( {\mathbf{X}}_{B}\right) }_{r} = {\left( {\mathbf{U}}_{B}\right) }_{r} - {\left( {\mathbf{X}}_{B}^{\prime }\right) }_{r}$ , where ${\left( {\mathbf{X}}_{B}^{\prime }\right) }_{r} \geq  0$ . It is immaterial whether the substitution is made before or after the new basis is computed.

3. ${x}_{j} = {u}_{j}$ : The basic vector ${\mathbf{X}}_{B}$ remains unchanged because ${x}_{j} = {u}_{j}$ stops short of forcing any of the current basic variables to reach its lower $\left( { = 0}\right)$ or upper bound. This means that ${x}_{j}$ will remain nonbasic but at upper bound. The only change needed in the tableau is to use the substitution ${x}_{j} = {u}_{j} - {x}_{j}^{\prime }$ to ensure that all nonbasic variables are at zero level.

A tie among ${\theta }_{1},{\theta }_{2}$ , and ${u}_{j}$ may be broken arbitrarily. However, it is preferable, where possible, to implement the rule for ${x}_{j} = {u}_{j}$ because it entails less computation.

The substitution ${x}_{j} = {u}_{j} - {x}_{j}^{\prime }$ will change the original ${\mathrm{c}}_{j},{\mathbf{P}}_{j}$ , and $\mathbf{b}$ to ${c}_{j}^{\prime } =  - {c}_{j}$ , ${\mathbf{P}}_{j}^{\prime } =  - {\mathbf{P}}_{j}$ , and $\mathbf{b}$ to ${\mathbf{b}}^{\prime } = \mathbf{b} - {u}_{j}{\mathbf{P}}_{j}$ . This means that if the revised simplex method is used, all the computations (e.g., ${\mathbf{B}}^{-1},{\mathbf{X}}_{B}$ , and ${z}_{j} - {c}_{j}$ ) should be based on the changed values of $\mathbf{C},\mathbf{A}$ , and $\mathbf{b}$ at each iteration (see Problem 7-36, for further details).

## Example 7.3-1

Solve the following LP model by the upper-bounding algorithm. ${}^{6}$

$$
\text{ Maximize }z = 3{x}_{1} + {5y} + 2{x}_{3}
$$

subject to

$$
{x}_{1} + y + 2{x}_{3} \leq  {14}
$$

$$
2{x}_{1} + {4y} + 3{x}_{3} \leq  {43}
$$

$$
0 \leq  {x}_{1} \leq  4,7 \leq  y \leq  {10},0 \leq  {x}_{3} \leq  3
$$

The lower bound on $y$ is accounted for using the substitution $y = {x}_{2} + 7$ , where $0 \leq  {x}_{2} \leq  {10} - 7 = 3.$

---

${}^{6}$ You can use TORA’s Linear Programming $\Rightarrow$ Solve problem $\Rightarrow$ Algebraic $\Rightarrow$ Iterations $\Rightarrow$ Bounded simplex to produce the associated simplex iterations (file toraEx7.3-1.txt).

---

To avoid being "sidetracked" by the computational details, we will not use the revised simplex method to carry out the computations. Instead, we will use the compact tableau form. Problems 7-36, 7-37, and 7-38, address the revised version of the algorithm.

Iteration 0

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | -3 | -5 | -2 | 0 | 0 | 35 |
| ${x}_{4}$ | 1 | 1 | 2 | 1 | 0 | 7 |
| ${x}_{5}$ | 2 | 4 | 3 | 0 | 1 | 15 |

We have $\mathbf{B} = {\mathbf{B}}^{-1} = \mathbf{I}$ and ${\mathbf{X}}_{B} = {\left( {x}_{4},{x}_{5}\right) }^{T} = {\mathbf{B}}^{-1}\mathbf{b} = {\left( 7,{15}\right) }^{T}$ . Given that ${x}_{2}$ is the entering variable $\left( {{z}_{2} - {c}_{2} =  - 5}\right)$ , we get ${\mathbf{B}}^{-1}{\mathbf{P}}_{2} = {\left( 1,4\right) }^{T}$ , which yields

$$
{\theta }_{1} = \min \left\{  {\frac{7}{1},\frac{15}{4}}\right\}   = {3.75}\text{ , corresponding to }{x}_{5}
$$

$$
{\theta }_{2} = \infty \text{ (because all the elements of }{\mathbf{B}}^{-1}{\mathbf{P}}_{2} > \mathbf{0}\text{ ) }
$$

Next, given the upper bound on the entering variable, ${x}_{2} \leq  3$ , it follows that

$$
{x}_{2} = \min \{ {3.75},\infty ,3\}  = 3
$$

Because ${x}_{2} = {u}_{2},{\mathbf{X}}_{B}$ remains unchanged, and ${x}_{2}$ becomes nonbasic at its upper bound. The substitution ${x}_{2} = 3 - {x}_{2}^{\prime }$ yields the following new tableau:

| Basic | ${x}_{1}$ | ${x}_{2}^{\prime }$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | -3 | 5 | -2 | 0 | 0 | 50 |
| ${x}_{4}$ | 1 | -1 | 2 | 1 | 0 | 4 |
| ${x}_{5}$ | 2 | -4 | 3 | 0 | 1 | 3 |

The substitution changes the original right-hand side vector from $\mathbf{b} = {\left( 7,{15}\right) }^{T}$ to ${\mathbf{b}}^{\prime } = {\left( 4,3\right) }^{T}$ . Thus, ${\mathbf{b}}^{\prime }$ replaces $\mathbf{b}$ in future iterations.

## Iteration 1

The entering variable is ${x}_{1}$ . The basic vector ${\mathbf{X}}_{B}$ and ${\mathbf{B}}^{-1}\left( { = \mathbf{I}}\right)$ are the same as in iteration 0 . Next, given ${\mathbf{B}}^{-1}{\mathbf{P}}_{1} = {\left( 1,2\right) }^{T}$ ,

$$
{\theta }_{1} = \min \left\{  {\frac{4}{1},\frac{3}{2}}\right\}   = {1.5}\text{ , corresponding to basic }{x}_{5}
$$

$$
{\theta }_{2} = \infty \text{ (because }{\mathbf{B}}^{-1}{\mathbf{P}}_{1} > \mathbf{0}\text{ ) }
$$

Thus,

$$
{x}_{1} = \min \{ {1.5},\infty ,4\}  = {1.5}
$$

Because ${x}_{1} = {\theta }_{1}$ , the entering variable ${x}_{1}$ becomes basic, and the leaving variable ${x}_{5}$ becomes nonbasic at zero level, which yields

| Basic | ${x}_{1}$ | ${x}_{2}^{\prime }$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | -1 | $\frac{5}{2}$ | 0 | $\frac{3}{2}$ | 109 |
| ${x}_{4}$ | 0 | 1 | $\frac{1}{2}$ | 1 | $- \frac{1}{2}$ | 5 |
| ${x}_{1}$ | 1 | -2 | $\frac{3}{2}$ | 0 | $\frac{1}{2}$ | $\frac{3}{2}$ |

Iteration 2

The new inverse is

$$
{\mathbf{B}}^{-1} = \left( \begin{array}{rr} 1 &  - \frac{1}{2} \\  0 & \frac{1}{2} \end{array}\right)
$$

Now, ${\mathbf{X}}_{B} = {\left( {x}_{4},{x}_{1}\right) }^{T} = {\mathbf{B}}^{-1}{\mathbf{b}}^{\prime } = {\left( \frac{5}{2},\frac{3}{2}\right) }^{T}$ , where ${\mathbf{b}}^{\prime } = {\left( 4,3\right) }^{T}$ as computed at the end of iteration 0 . We select ${x}_{2}^{\prime }$ as the entering variable, and, noting that ${\mathbf{P}}_{2}^{\prime } =  - {\mathbf{P}}_{2}$ , we get

$$
{\mathbf{B}}^{-1}{\mathbf{P}}_{2}^{\prime } = {\left( 1, - 2\right) }^{T}
$$

Thus,

$$
{\theta }_{1} = \min \left\{  {\frac{\frac{5}{2}}{1}, - }\right\}   = {2.5}\text{ , corresponding to basic }{x}_{4}
$$

$$
{\theta }_{2} = \min \left\{  {-,\frac{\frac{3}{2} - 4}{-2}}\right\}   = {1.25}\text{ , corresponding to basic }{x}_{1}
$$

We then have

$$
{x}_{2}^{\prime } = \min \{ {2.5},{1.25},3\}  = {1.25}
$$

Because ${x}_{2}^{\prime } = {\theta }_{1},{x}_{1}$ becomes nonbasic at upper bound resulting in the substitution ${x}_{1} = 4 - {x}_{1}^{\prime }$ . The new tableau is

| Basic | ${x}_{1}^{\prime }$ | ${x}_{2}^{\prime }$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | -1 | $\frac{5}{2}$ | 0 | $\frac{3}{2}$ | 199 |
| ${x}_{4}$ | 0 | 1 | $\frac{1}{2}$ | 1 | $- \frac{1}{2}$ | 5 |
| ${x}_{1}^{\prime }$ | -1 | -2 | $\frac{3}{2}$ | 0 | $\frac{1}{2}$ | $- \frac{5}{2}$ |

Next, the entering variable ${x}_{2}^{\prime }$ becomes basic and the leaving variable ${x}_{1}^{\prime }$ becomes nonbasic, which yields

| Basic | ${x}_{1}^{\prime }$ | ${x}_{2}^{\prime }$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| 乙 | $\frac{1}{2}$ | 0 | 7 | 0 | 5 | 223 4 |
| ${x}_{4}$ | $- \frac{1}{2}$ | 0 | 5 | 1 | $- \frac{1}{4}$ | 5 4 |
| ${x}_{2}^{\prime }$ | $\frac{1}{2}$ | 1 | $- \frac{3}{4}$ | 0 | $- \frac{1}{4}$ | 5 4 |

The last tableau is feasible and optimal. Note that the last two steps could have been reversed-meaning that we could first make ${x}_{2}^{\prime }$ basic and then apply the substitution ${x}_{1} = 4 - {x}_{1}^{\prime }$ (try it!). The sequence presented here involves less computation, however.

The optimal values of ${x}_{1},{x}_{2}$ , and ${x}_{3}$ are obtained by back-substitution as ${x}_{1} = {u}_{1} - {x}_{1}^{\prime } = \; 4 - 0 = 4,{x}_{2} = {u}_{2} - {x}_{2}^{\prime } = 3 - \frac{5}{4} = \frac{7}{4}$ , and ${x}_{3} = 0$ . Finally, we get $y = {l}_{2} + {x}_{2} = 7 + \frac{7}{4} = \frac{35}{4}$ . The associated optimal value of the objective function is $\frac{223}{4}$ .

### 7.4 DUALITY ^Duality

This section presents a rigorous treatment of duality. The presentation also lays the foundation for the development of parametric programming.

#### 7.4.1 Matrix Definition of the Dual Problem ^DualMatrix

Suppose that the primal problem in equation form with $m$ constraints and $n$ variables is defined as

$$
\text{ Maximize }z = \mathbf{{CX}}
$$

subject to

$$
\mathbf{{AX}} = \mathbf{b}
$$

$$
\mathbf{X} \geq  \mathbf{0}
$$

Let the vector $\mathbf{Y} = \left( {{y}_{1},{y}_{2},\ldots ,{y}_{m}}\right)$ define the dual variables. The rules in Section 4.1 (Chapter 4) define the dual problem as:

$$
\text{ Minimize }w = \mathbf{{Yb}}
$$

subject to

$$
\mathbf{{YA}} \geq  \mathbf{C}
$$

$\mathbf{Y}$ unrestricted

Some of the constraints in $\mathbf{{YA}} \geq  \mathbf{C}$ may override unrestricted $\mathbf{Y}$ , as explained in the examples of Section 4.1, Chapter 4.

#### 7.4.2 Optimal Dual Solution ^OptimalDualSolution

This section establishes relationships between the primal and dual problems and shows how the optimal dual solution can be determined from the optimal primal solution. Let B be the current optimal primal basis, and define ${\mathbf{C}}_{B}$ as the objective-function coefficients associated with the optimal vector ${\mathbf{X}}_{B}$ .

Theorem 7.4-1 (Weak duality theory). For any pair of feasible primal and dual solutions, $\left( {\mathbf{X},\mathbf{Y}}\right)$ , the value of the objective function in the minimization problem sets an upper bound on the value of the objective function in the maximization problem. For the optimal pair $\left( {{\mathbf{X}}^{ * },{\mathbf{Y}}^{ * }}\right)$ , the two objective values are equal. ^WeakDuality

Proof. The feasible pair $\left( {\mathbf{X},\mathbf{Y}}\right)$ satisfies all the restrictions of the two problems. Premultiplying both sides of the constraints of the maximization problem with (unrestricted) $\mathbf{Y}$ , we get

$$
\mathbf{{YAX}} = \mathbf{{Yb}} = w \tag{1}
$$

Also, for the minimization problem, postmultiplying both sides of each of the first two sets of constraints by $\mathbf{X}\left( { \geq  0}\right)$ , we get

$$
\mathbf{{YAX}} \geq  \mathbf{{CX}} = z \tag{2}
$$

Thus, from (1) and (2), $z \leq  w$ for any feasible pair $\left( {\mathbf{X},\mathbf{Y}}\right)$ .

Note that the feasibility requirement of $\mathbf{X}$ and $\mathbf{Y}$ is implied by $\mathbf{{AX}} = \mathbf{b}$ in (1), and $\mathbf{X} \geq  \mathbf{0}$ and $\mathbf{{YA}} \geq  \mathbf{C}$ in (2). Also, labeling the problems as primal or dual is immaterial. What is important is the sense of optimization in each problem-meaning that, for any pair of feasible solutions, the objective value in the maximization problem does not exceed the objective value in the minimization problem.

The implication of the theorem is that, given $z \leq  w$ for any pair of feasible solutions, the maximum of $z$ and the minimum of $w$ are achieved when the two objective values are equal. A consequence of this result is that the "goodness" of any feasible primal and dual solutions relative to the optimum can be checked by comparing the difference $\left( {w - z}\right)$ to $\frac{z + w}{2}$ . The smaller the ratio $\frac{2\left( {w - z}\right) }{z + w}$ , the closer the two solutions are to being optimal. The given rule of thumb does not suggest that the optimal objective value is $\frac{z + w}{2}$ .

Unboundedness and infeasibility. If the objective value of one of the two problems is unbounded, then the other problem must be infeasible. For if it is not, then both problems have feasible solutions, and the relationship $z \leq  w$ must hold - an impossible result because unbounded objective value means $z =  + \infty$ or $w =  - \infty$ . ^UnboundedInfeasible

If one problem is infeasible, then the other problem can be infeasible also, as the following example demonstrates (verify graphically!):

$$
\text{ Primal. Maximize }z = \left\{  {{x}_{1} + {x}_{2} \mid  {x}_{1} - {x}_{2} \leq   - 1, - {x}_{1} + {x}_{2} \leq   - 1,{x}_{1},{x}_{2} \geq  0}\right\}
$$

$$
\text{ Dual. Minimize }w = \left\{  {-{y}_{1} - {y}_{2} \mid  {y}_{1} - {y}_{2} \geq  1, - {y}_{1} + {y}_{2} \geq  1,{y}_{1},{y}_{2} \geq  0}\right\}
$$

Theorem 7.4-2 Given the optimal primal basis $\mathbf{B}$ and its associated objective coefficient vector ${\mathbf{C}}_{B}$ , the optimal solution of the dual problem is

$$
\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}
$$

Proof. The proof rests on showing that $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ is a feasible dual solution and that, per Theorem 7.4-1, $z = w$ .

The feasibility of $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ is guaranteed by the optimality of the primal, ${z}_{j} - {c}_{j} \geq  0$ for all $j$ -that is,

$$
{\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{A} - \mathbf{C} \geq  \mathbf{0}
$$

(See Section 7.2.1.) Thus, $\mathbf{{YA}} - \mathbf{C} \geq  \mathbf{0}$ , which shows that $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ satisfies the dual constraints $\mathbf{{YA}} \geq  \mathbf{C}$ .

Next, we show that $w = z$ by noting that

$$
w = \mathbf{{Yb}} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b} \tag{1}
$$

Similarly, given the primal solution ${\mathbf{X}}_{B} = {\mathbf{B}}^{-1}\mathbf{b}$ , we get

$$
z = {\mathbf{C}}_{B}{\mathbf{X}}_{B} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b} \tag{2}
$$

The dual variables $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ are referred to by the standard names dual or shadow prices (see Section 4.3.1). ^ShadowPrices

Motivation for the dual simplex algorithm. Given that ${\mathbf{P}}_{j}$ is the $j$ th column of $\mathbf{A}$ , we note from Theorem 7.4-2 that ${z}_{j} - {c}_{j} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{P}}_{j} - {c}_{j} = {\mathbf{{YP}}}_{j} - {c}_{j}$ represents the difference between the left- and right-hand sides of the dual constraints. The maximization primal problem starts with ${z}_{j} - {c}_{j} < 0$ for at least one $j$ , which means that the corresponding dual constraint, $\mathbf{Y}{\mathbf{P}}_{j} \geq  {c}_{j}$ , is not satisfied. When the primal optimal is reached, we get ${z}_{j} - {c}_{j} \geq  0$ , for all $j$ , rendering the dual solution $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ feasible. Thus, as the primal problem seeks optimality, the dual problem seeks feasibility. This point is the basis for the development of the dual simplex method (Section 4.4.1), in which the iterations start (better than) optimal and infeasible and remain so until feasibility is attained at the last iteration. This is in contrast with the (primal) simplex method (Chapter 3), which remains worse than optimal but feasible until the optimal iteration is reached. ^DualSimplexMotivation

## Example 7.4-1 ^ExampleDual

---

The optimal basis for the following LP is $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4}}\right)$ . Write the dual, and find its optimum

solution using the optimal primal basis.

$$
\text{ Maximize }z = 3{x}_{1} + 5{x}_{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3}\; = 5
$$

$$
- {x}_{1} + 3{x}_{2}\; + {x}_{4} = 2
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

The dual problem is

$$
\text{ Minimize }w = 5{y}_{1} + 2{y}_{2}
$$

subject to

$$
{y}_{1} - {y}_{2} \geq  3
$$

$$
2{y}_{1} + 3{y}_{2} \geq  5
$$

$$
{y}_{1},{y}_{2} \geq  0
$$

			We have ${\mathbf{X}}_{B} = {\left( {x}_{1},{x}_{4}\right) }^{T}$ and ${\mathbf{C}}_{B} = \left( {3,0}\right)$ . The optimal basis and its inverse are

$$
\mathbf{B} = \left( \begin{array}{rr} 1 & 0 \\   - 1 & 1 \end{array}\right) ,{\mathbf{B}}^{-1} = \left( \begin{array}{ll} 1 & 0 \\  1 & 1 \end{array}\right)
$$

---

---

The associated primal and dual values are

$$
{\left( {x}_{1},{x}_{4}\right) }^{T} = {\mathbf{B}}^{-1}\mathbf{b} = {\left( 5,7\right) }^{T}
$$

$$
\left( {{y}_{1},{y}_{2}}\right)  = {\mathbf{C}}_{B}{\mathbf{B}}^{-1} = \left( {3,0}\right)
$$

Both solutions are feasible, and $z = w = {15}$ (verify!). Thus, the two solutions are optimal.

---

### 7.5 PARAMETRIC LINEAR PROGRAMMING ^ParametricLP

Parametric linear programming is an extension of the post-optimal analysis presented in Section 4.5. It investigates the effect of predetermined continuous variations in the objective-function coefficients and the right-hand side of the constraints on the optimum solution.

Let $\mathbf{X} = \left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)$ and define the LP as

$$
\text{ Maximize }z = \left\{  {\mathbf{{CX}}\left| {\;\mathop{\sum }\limits_{{j = 1}}^{n}{\mathbf{P}}_{j}{x}_{j} = \mathbf{b}}\right. ,\mathbf{X} \geq  \mathbf{0}}\right\}
$$

In parametric analysis, the objective function and right-hand side vectors, $\mathbf{C}$ and $\mathbf{b}$ , are replaced with the parameterized functions $\mathbf{C}\left( t\right)$ and $\mathbf{b}\left( t\right)$ , where $t$ is the parameter of variation. Mathematically, $t$ can assume any positive or negative value. In this presentation, we will assume that $t \geq  0$ . ^ParametricIdea

The general idea of parametric analysis is to start with the optimal solution at $t = 0$ . Then, using the optimality and feasibility conditions of the simplex method, we determine the range $0 \leq  t \leq  {t}_{1}$ for which the solution at $t = 0$ remains optimal and feasible. In this case, ${t}_{1}$ is referred to as a critical value. The process continues by determining successive critical values and their corresponding optimal feasible solutions. Termination of post-optimal analysis occurs when, regardless of $t$ , the last solution remains unchanged or there is indication that no feasible solution exists. ^CriticalValues

#### 7.5.1 Parametric Changes in C ^ParametricC

Let ${\mathbf{X}}_{{B}_{i}},{\mathbf{B}}_{i},{\mathbf{C}}_{{B}_{i}}\left( t\right)$ be the elements that define the optimal solution associated with critical ${t}_{i}$ (the computations start at ${t}_{0} = 0$ with ${\mathbf{B}}_{0}$ as its optimal basis). Next, the critical value ${t}_{i + 1}$ and its optimal basis, if one exists, are determined. Because changes in $\mathbf{C}$ can affect only the optimality of the problem, the current solution ${\mathbf{X}}_{{B}_{i}} = {\mathbf{B}}_{i}^{-1}\mathbf{b}$ will remain optimal for some $t \geq  {t}_{i}$ so long as the reduced cost, ${z}_{j}\left( t\right)  - {c}_{j}\left( t\right)$ , satisfies the following optimality condition: ^OptimalityInequalities

$$
{z}_{j}\left( t\right)  - {c}_{j}\left( t\right)  = {\mathbf{C}}_{{B}_{i}}\left( t\right) {\mathbf{B}}_{i}^{-1}{\mathbf{P}}_{j} - {c}_{j}\left( t\right)  \geq  0\text{ , for all }j
$$

The value of ${t}_{i + 1}$ equals the largest $t > {t}_{i}$ that satisfies all the optimality conditions.

Note that nothing in the inequalities requires $\mathbf{C}\left( t\right)$ to be linear in $t$ . Any function $\mathbf{C}\left( t\right)$ , linear or nonlinear, is acceptable. However, with nonlinearity the numerical manipulation of the resulting inequalities can be cumbersome. (See Problem 7-53, for an illustration of the nonlinear case.)

Example 7.5-1 ^ExampleParametricC

$$
\text{ Maximize }z = \left( {3 - {6t}}\right) {x}_{1} + \left( {2 - {2t}}\right) {x}_{2} + \left( {5 + {5t}}\right) {x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} \leq  {40}
$$

$$
3{x}_{1}\; + 2{x}_{3} \leq  {60}
$$

$$
{x}_{1} + 4{x}_{2}\; \leq  {30}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

We have

$$
\mathbf{C}\left( t\right)  = \left( {3 - {6t},2 - {2t},5 + {5t}}\right) , t \geq  0
$$

The variables ${x}_{4},{x}_{5}$ , and ${x}_{6}$ will be used as the slack variables associated with the three constraints.

Optimal Solution at $t = {t}_{0} = 0$

$$
{\mathbf{X}}_{{B}_{0}} = {\left( {x}_{2},{x}_{3}{x}_{6}\right) }^{T} = {\left( 5,{30},{10}\right) }^{T}
$$

$$
{\mathbf{C}}_{{B}_{0}}\left( t\right)  = \left( {2 - {2t},5 + {5t},0}\right)
$$

$$
{\mathbf{B}}_{0}^{-1} = \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right)
$$

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 4 | 0 | 0 | 1 | 2 | 0 | 160 |
| ${x}_{2}$ | $- \frac{1}{4}$ | 1 | 0 | $\frac{1}{2}$ | $- \frac{1}{4}$ | 0 | 5 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | 1 | 0 | 30 |
| ${x}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | 10 |

The optimality conditions for the current nonbasic vectors, ${\mathbf{P}}_{1},{\mathbf{P}}_{4}$ , and ${\mathbf{P}}_{5}$ , are

$$
{\left\{  {\mathbf{C}}_{{B}_{0}}\left( t\right) {\mathbf{B}}_{0}^{-1}{\mathbf{P}}_{j} - {c}_{j}\left( t\right) \right\}  }_{j = 1,4,5} = \left( {4 + {14t},1 - t,2 + {3t}}\right)  \geq  \mathbf{0}
$$

Thus, ${\mathbf{X}}_{{B}_{0}}$ remains optimal for $t \leq  {t}_{1}$ , where ${t}_{1}$ is determined from the optimality conditions as

$$
\left. \begin{array}{r} 4 + {14t} \geq  0 \\  1 - t \geq  0 \\  2 + {3t} \geq  0 \end{array}\right\}   \Rightarrow  0 \leq  t \leq  1 \Rightarrow  {t}_{1} = 1
$$

The reduced cost ${z}_{4}\left( t\right)  - {c}_{4}\left( t\right)  = 1 - t$ equals zero at $t = 1$ and becomes negative for $t > 1$ . Thus, ${\mathbf{P}}_{4}$ must enter the basis for $t > 1$ . In this case, ${\mathbf{P}}_{2}$ must leave the basis (see the optimal tableau at $t = 0$ ). The new basic solution ${\mathbf{X}}_{{B}_{1}}$ is the alternative solution obtained at $t = 1$ by letting ${\mathbf{P}}_{4}$ enter the basis-that is, ${\mathbf{X}}_{{B}_{1}} = {\left( {x}_{4},{x}_{3},{x}_{6}\right) }^{T}$ and ${\mathbf{B}}_{1} = \left( {{\mathbf{P}}_{4},{\mathbf{P}}_{3},{\mathbf{P}}_{6}}\right)$ .

Alternative Optimal Basis at $t = {t}_{1} = 1$

$$
{\mathbf{B}}_{1} = \left( \begin{array}{lll} 1 & 1 & 0 \\  0 & 2 & 0 \\  0 & 0 & 1 \end{array}\right) ,{\mathbf{B}}_{1}^{-1} = \left( \begin{array}{rrr} 1 &  - \frac{1}{2} & 0 \\  0 & \frac{1}{2} & 0 \\  0 & 0 & 1 \end{array}\right)
$$

Thus,

$$
{\mathbf{X}}_{{B}_{1}} = {\left( {x}_{4},{x}_{3},{x}_{6}\right) }^{T} = {\mathbf{B}}_{1}^{-1}\mathbf{b} = {\left( {10},{30},{30}\right) }^{T}
$$

$$
{\mathbf{C}}_{{B}_{1}}\left( t\right)  = \left( {0,5 + {5t},0}\right)
$$

The associated nonbasic vectors are ${\mathbf{P}}_{1},{\mathbf{P}}_{2}$ , and ${\mathbf{P}}_{5}$ , and we have

$$
{\left\{  {\mathbf{C}}_{{B}_{1}}\left( t\right) {\mathbf{B}}_{1}^{-1}{\mathbf{P}}_{j} - {c}_{j}\left( t\right) \right\}  }_{j = 1,2,5} = \left( {\frac{9 + {27t}}{2}, - 2 + {2t},\frac{5 + {5t}}{2}}\right)  \geq  \mathbf{0}
$$

According to these conditions, the basic solution ${\mathbf{X}}_{{B}_{1}}$ remains optimal for all $t \geq  1$ . Observe that the optimality condition, $- 2 + {2t} \geq  0$ , automatically "remembers" that ${\mathbf{X}}_{{B}_{1}}$ is optimal for a range of $t$ that starts from the last critical value ${t}_{1} = 1$ . This will always be the case in parametric programming computations.

The optimal solution for the entire range of $t$ is summarized in the following table (the value of $z$ is computed by direct substitution): ^ParametricSummaryC

| $t$ | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | $z$ |
| --- | --- | --- | --- | --- |
| $0 \leq  t \leq  1$ | 0 | 5 | 30 | ${160} + {140t}$ |
| $t \geq  1$ | 0 | 0 | 30 | ${150} + {150t}$ |

#### 7.5.2 Parametric Changes in b ^Parametricb

The parameterized right-hand side $\mathbf{b}\left( t\right)$ can affect the feasibility of the problem only. The critical values of $t$ are thus determined from the condition ^FeasibilityInequalities

$$
{\mathbf{X}}_{B}\left( t\right)  = {\mathbf{B}}^{-1}\mathbf{b}\left( t\right)  \geq  \mathbf{0}
$$

Example 7.5-2 ^ExampleParametricb

$$
\text{ Maximize }z = 3{x}_{1} + 2{x}_{2} + 5{x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} \leq  {40} - t
$$

$$
3{x}_{1}\; + 2{x}_{3} \leq  {60} + {2t}
$$

$$
{x}_{1} + 4{x}_{2}\; \leq  {30} - {7t}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

Assume that $t \geq  0$ .

At $t = {t}_{0} = 0$ , the problem is identical to that of Example 7.5-1. We thus have

$$
{\mathbf{X}}_{{B}_{0}} = {\left( {x}_{2},{x}_{3},{x}_{6}\right) }^{T} = {\left( 5,{30},{10}\right) }^{T}
$$

$$
{\mathbf{B}}_{0}^{-1} = \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right)
$$

To determine the first critical value ${t}_{1}$ , we apply the feasibility conditions ${\mathbf{X}}_{{B}_{0}}\left( t\right)  = \; {\mathbf{B}}_{0}^{-1}\mathbf{b}\left( t\right)  \geq  0$ , which yields

$$
\left( \begin{array}{l} {x}_{2} \\  {x}_{3} \\  {x}_{6} \end{array}\right)  = \left( \begin{matrix} 5 - t \\  {30} + t \\  {10} - {3t} \end{matrix}\right)  \geq  \left( \begin{array}{l} 0 \\  0 \\  0 \end{array}\right)  \Rightarrow  0 \leq  t \leq  \frac{10}{3} \Rightarrow  {t}_{1} = \frac{10}{3}
$$

The basis ${\mathbf{B}}_{0}$ remains feasible for the range $0 \leq  t \leq  \frac{10}{3}$ . However, the values of the basic variables ${x}_{2},{x}_{3}$ , and ${x}_{6}$ change with $t$ .

The value of the basic variable ${x}_{6}\left( { = {10} - {3t}}\right)$ equals zero at $t = {t}_{1} = \frac{10}{3}$ , and will become negative for $t > \frac{10}{3}$ . Thus, at $t = \frac{10}{3}$ , we can determine the alternative basis ${\mathbf{B}}_{1}$ by applying the revised dual simplex method (see Problem 7-31, for details). The leaving variable is ${x}_{6}$ .

## Alternative Basis at $t = {t}_{1} = \frac{10}{3}$

Given that ${x}_{6}$ is the leaving variable, we determine the entering variable as follows:

$$
{\mathbf{X}}_{{B}_{0}} = {\left( {x}_{2},{x}_{3},{x}_{6}\right) }^{T},{\mathbf{C}}_{{B}_{0}} = \left( {2,5,0}\right)
$$

Thus,

$$
{\left\{  {z}_{j} - {c}_{j}\right\}  }_{j = 1,4,5} = {\left\{  {\mathbf{C}}_{{B}_{0}}{\mathbf{B}}_{0}^{-1}{\mathbf{P}}_{j} - {c}_{j}\right\}  }_{j = 1,4,5} = \left( {4,1,2}\right)
$$

Next, for nonbasic ${x}_{j}, j = 1,4,5$ , we compute

$$
\text{ (Row of }{\mathbf{B}}_{0}^{-1}\text{ associated with }{x}_{6}\text{ ) }\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4},{\mathbf{P}}_{5}}\right)  = \left( {\text{ Third row of }{\mathbf{B}}_{0}^{-1}}\right) \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4},{\mathbf{P}}_{5}}\right)
$$

$$
= \left( {-2,1,1}\right) \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4},{\mathbf{P}}_{5}}\right)
$$

$$
= \left( {2, - 2,1}\right)
$$

The entering variable is thus associated with

$$
\theta  = \min \left\{  {-,\left| \frac{1}{-2}\right| , - }\right\}   = \frac{1}{2}
$$

Thus, ${\mathbf{P}}_{4}$ is the entering vector. The alternative basic solution and its ${\mathbf{B}}_{1}$ and ${\mathbf{B}}_{1}^{-1}$ are

$$
{\mathbf{X}}_{{B}_{1}} = {\left( {x}_{2},{x}_{3},{x}_{4}\right) }^{T}
$$

$$
{\mathbf{B}}_{1} = \left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)  = \left( \begin{array}{lll} 2 & 1 & 1 \\  0 & 2 & 0 \\  4 & 0 & 0 \end{array}\right) ,{\mathbf{B}}_{1}^{-1} = \left( \begin{matrix} 0 & 0 & \frac{1}{4} \\  0 & \frac{1}{2} & 0 \\  1 &  - \frac{1}{2} &  - \frac{1}{2} \end{matrix}\right)
$$

The next critical value ${t}_{2}$ is determined from the feasibility conditions, ${\mathbf{X}}_{{B}_{1}}\left( t\right)  = {\mathbf{B}}_{1}^{-1}\mathbf{b}\left( \mathrm{t}\right)  \geq  \mathbf{0}$ , which yield

$$
\left( \begin{array}{l} {x}_{2} \\  {x}_{3} \\  {x}_{4} \end{array}\right)  = \left( \begin{matrix} \frac{{30} - {7t}}{4} \\  {30} + t \\  \frac{-{10} + {3t}}{2} \end{matrix}\right) \left( \begin{array}{l} 0 \\  0 \\  0 \end{array}\right)  \Rightarrow  \frac{10}{3} \leq  t \leq  \frac{30}{7} \Rightarrow  {t}_{2} = \frac{30}{7}
$$

At $t = {t}_{2} = \frac{30}{7}$ , an alternative basis can be obtained by the revised dual simplex method. The leaving variable is ${x}_{2}$ , because it corresponds to the condition yielding the critical value ${t}_{2}$ .

## Alternative Basis at $t = {t}_{2} = \frac{30}{7}$

Given that ${x}_{2}$ is the leaving variable, we determine the entering variable as follows:

$$
{\mathbf{X}}_{{B}_{1}} = {\left( {x}_{2},{x}_{3},{x}_{4}\right) }^{T},{\mathbf{C}}_{{B}_{1}} = \left( {2,5,0}\right)
$$

Thus,

$$
{\left\{  {z}_{j} - {c}_{j}\right\}  }_{j = 1,5,6} = {\left\{  {\mathbf{C}}_{{B}_{1}}{\mathbf{B}}_{1}^{-1}{\mathbf{P}}_{j} - {c}_{j}\right\}  }_{j = 1,5,6} = \left( {5,\frac{5}{2},\frac{1}{2}}\right)
$$

Next, for nonbasic ${x}_{j}, j = 1,5$ , and 6, we compute

$$
\text{ (Row of }{\mathbf{B}}_{1}^{-1}\text{ associated with }{x}_{2}\text{ ) }\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)  = \text{ (First row of }{\mathbf{B}}_{1}^{-1}\text{ ) }\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)
$$

$$
= \left( {0,0,\frac{1}{4}}\right) \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{5},{\mathbf{P}}_{6}}\right)
$$

$$
= \left( {\frac{1}{4},0,\frac{1}{4}}\right)
$$

Because all the denominator elements, $\left( {\frac{1}{4},0,\frac{1}{4}}\right)$ , are $\geq  0$ , the problem has no feasible solution for $t > \frac{30}{7}$ , and the parametric analysis ends at $t = {t}_{2} = \frac{30}{7}$ .

The optimal solution is summarized as ^ParametricSummaryb

| $t$ | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | $z$ |
| --- | --- | --- | --- | --- |
| $0 \leq  t \leq  \frac{10}{3}$ | 0 | $5 - t$ | ${30} + t$ | ${160} + {3t}$ |
| $\frac{10}{3} \leq  t \leq  \frac{30}{7}$ | 0 | $\frac{{30} - {7t}}{4}$ | ${30} + t$ | ${165} + \frac{3}{2}t$ |
| $t > \frac{30}{7}$ | (No feasible solution exists) |  |  |  |

### 7.6 MORE LINEAR PROGRAMMING TOPICS ^MoreTopics

The following list provides additional LP topics (normally covered in specialized OR courses) that can be found in Chapter 22 on the website. The reason these topics are not included in the text is to maintain the number of printed pages at a reasonable level.

1. Minimum-cost capacitated flow problem, including LP formulation, and capacitated network simplex algorithm model. ^MinCostFlow

2. Dantzig-Wolfe decomposition algorithm. ^DantzigWolfe

3. Karmarkar interior-point algorithm. ^Karmarkar

## BIBLIOGRAPHY ^Bibliography

Bazaraa, M., J. Jarvis, and H. Sherali, Linear Programming and Network Flows, 4th ed., Wiley, New York, 2009.

Chvàtal, V., Linear Programming, Freeman, San Francisco, 1983.

Nering, E., and A. Tucker, Linear Programming and Related Problems, Academic Press, Boston, 1992.

Saigal, R. Linear Programming: A Modern Integrated Analysis, Kluwer Academic Publishers, Boston, 1995.

Vanderbei, R., Linear Programming: Foundation and Extensions, 3rd ed., Springer, New York, 2008.

## PROBLEMS ^Problems

| Section | Assigned Problems | Section | Assigned Problems |
| --- | --- | --- | --- |
| 7.1.1 | 7-1 to 7-4 | 7.3 | 7-32 to 7-39 |
| 7.1.1 | 7-5 to 7-8 | 7.4.1 | 7-40 to 7-41 |
| 7.1.2 | 7-9 to 7-13 | 7.4.2 | 7-42 to 7-48 |
| 7.2.1 | 7-14 to 7-26 | 7.5.1 | 7-49 to 7-53 |
| 7.2.2 | 7-27 to 7-31 | 7.5.2 | 7-54 to 7-57 | ^AssignedProblems

7-1. Show that the set $Q = \left\{  {{x}_{1},{x}_{2} \mid  {x}_{1} + {x}_{2} \leq  3,{x}_{1} \geq  0,{x}_{2} \geq  0}\right\}$ is convex. Is the nonnegativity condition essential for the proof?

*7-2. Show that the set $Q = \left\{  {{x}_{1},{x}_{2} \mid  {x}_{1} \geq  1\text{ or }{x}_{2} \geq  2}\right\}$ is not convex.

7-3. Determine graphically the extreme points of the following convex set:

$$
Q = \left\{  {{x}_{1},{x}_{2} \mid  {x}_{1} + {x}_{2} \leq  3,{x}_{1} \geq  0,{x}_{2} \geq  0}\right\}
$$

Show that the entire feasible solution space can be determined as a convex combination of its extreme points. Hence, conclude that any convex (bounded) solution space is totally defined once its extreme points are known.

7-4. In the solution space in Figure 7.3 (drawn to scale), express the interior point $\left( {3,1}\right)$ as a convex combination of the extreme points $A, B, C$ , and $D$ by determining the weights associated with the extreme points.

![bo_d56m4hbef24c73bhe5s0_25_384_1538_666_635_0.jpg](bo_d56m4hbef24c73bhe5s0_25_384_1538_666_635_0.jpg)

FIGURE 7.3

Solution space for Problem 7-4

7-5. In the following sets of equations, (a) and (b) have unique (basic) solutions, (c) has an infinite number of solutions, and (d) has no solution. Show how these results can be verified using graphical vector representation. From this exercise, state the general conditions for vector dependence/independence that

(a) ${x}_{1} + 3{x}_{2} = 2$ (b) $2{x}_{1} + 3{x}_{2} = 1$

$3{x}_{1} + {x}_{2} = 3 \; 2{x}_{1} - {x}_{2} = 2$

(c) $2{x}_{1} + 6{x}_{2} = 4$ (d) $2{x}_{1} - 4{x}_{2} = 2$

${x}_{1} + 3{x}_{2} = 2 \; - {x}_{1} + 2{x}_{2} = 1$

7-6. Use vectors to determine graphically the type of solution for each of the sets of equations below: unique solution, an infinite number of solutions, or no solution. For the cases of unique solutions, indicate from the vector representation (and without solving the equations algebraically) whether the values of ${x}_{1}$ and ${x}_{2}$ are positive, zero, or negative.

(a) $\left( \begin{array}{rr} 5 & 4 \\  1 &  - 3 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 2 \\  2 \end{array}\right)$ *(b) $\left( \begin{array}{rr} 2 &  - 2 \\  1 & 3 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 1 \\  3 \end{array}\right)$

(c) $\left( \begin{array}{ll} 2 & 4 \\  1 & 3 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l}  - 4 \\   - 2 \end{array}\right)$ *(d) $\left( \begin{array}{ll} 2 & 4 \\  1 & 2 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 6 \\  3 \end{array}\right)$

(e) $\left( \begin{array}{rr}  - 2 & 4 \\  1 &  - 2 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 4 \\  2 \end{array}\right)$ *(f) $\left( \begin{array}{rr} 1 &  - 2 \\  0 & 0 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \end{array}\right)  = \left( \begin{array}{l} 1 \\  1 \end{array}\right)$

7-7. Consider the following system of equations:

$$
\left( \begin{array}{l} 1 \\  2 \\  3 \end{array}\right) {x}_{1} + \left( \begin{array}{l} 0 \\  2 \\  1 \end{array}\right) {x}_{2} + \left( \begin{array}{l} 1 \\  4 \\  2 \end{array}\right) {x}_{3} + \left( \begin{array}{l} 2 \\  0 \\  0 \end{array}\right) {x}_{4} = \left( \begin{array}{l} 3 \\  4 \\  2 \end{array}\right)
$$

Determine if any of the following combinations forms a basis:

*(a) $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$

(b) $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)$

(c) $\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)$

*(d) $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)$

7-8. True or False?

(a) The system $\mathbf{{BX}} = \mathbf{b}$ has a unique solution if $\mathbf{B}$ is singular.

(b) The system $\mathbf{{BX}} = \mathbf{b}$ has no solution if $\mathbf{B}$ is singular and $\mathbf{b}$ is independent of $\mathbf{B}$ .

(c) The system $\mathbf{{BX}} = \mathbf{b}$ has an infinity of solutions if $\mathbf{B}$ is singular and $\mathbf{b}$ is dependent.

*7-9. In Example 7.1-3, consider $\mathbf{B} = \left( {{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)$ . Show that the corresponding basic solution is feasible, and then generate the corresponding simplex tableau.

7-10. Consider the following LP:

$$
\text{ Maximize }z = 5{x}_{1} + {12}{x}_{2} + 4{x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} + {x}_{4} = {10}
$$

$$
2{x}_{1} - 2{x}_{2} - {x}_{3}\; = 2
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

Check if each of the following matrices forms a (feasible or infeasible) basis: $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{3}}\right)$ , $\left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4}}\right) ,\left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right) ,\left( {{\mathbf{P}}_{3},{\mathbf{P}}_{4}}\right)$ .

7-11. In the following LP, compute the entire simplex tableau associated with ${\mathbf{X}}_{B} = {\left( {x}_{1},{x}_{2},{x}_{5}\right) }^{T}$ .

$$
\text{ Minimize }z = 2{x}_{1} + {x}_{2}
$$

subject to

$$
3{x}_{1} + {x}_{2} - {x}_{3}\; = 2
$$

$$
4{x}_{1} + 3{x}_{2}\; - {x}_{4}\; = 4
$$

$$
{x}_{1} + 2{x}_{2}\; + {x}_{5} = 2
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} \geq  0
$$

*7-12. The following is an optimal LP tableau:

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | 0 | 3 | 2 | ? |
| ${x}_{3}$ | 0 | 0 | 1 | 1 | -1 | 2 |
| ${x}_{2}$ | 0 | 1 | 0 | 1 | 0 | 6 |
| ${x}_{1}$ | 1 | 0 | 0 | -1 | 1 | 2 |

The variables ${x}_{3},{x}_{4}$ , and ${x}_{5}$ are slacks in the original problem. Use matrix manipulations to reconstruct the original LP, and then compute the optimum objective value.

7-13. In the matrix simplex tableau, suppose that $\mathbf{X} = {\left( {\mathbf{X}}_{\mathrm{I}},{\mathbf{X}}_{\mathrm{{II}}}\right) }^{T}$ , where ${\mathbf{X}}_{\mathrm{{II}}}$ corresponds to a typical starting basic solution (consisting of slack and/or artificial variables) with $\mathbf{B} = \mathbf{I}$ , and let $\mathbf{C} = \left( {{\mathbf{C}}_{\mathrm{I}},{\mathbf{C}}_{\mathrm{{II}}}}\right)$ and $\mathbf{A} = \left( {\mathbf{D},\mathbf{I}}\right)$ be the corresponding partitions of $\mathbf{C}$ and $\mathbf{A}$ , respectively. Show that the matrix simplex tableau reduces to the same form used in Chapter 3 - namely,

| Basic | ${\mathbf{X}}_{\mathrm{I}}$ | ${\mathbf{X}}_{\text{ II }}$ | Solution |
| --- | --- | --- | --- |
| $z$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{D} - {\mathbf{C}}_{\mathrm{I}}$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1} - {\mathbf{C}}_{\text{ II }}$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}\mathbf{b}$ |
| ${\mathbf{X}}_{B}$ | ${\mathbf{B}}^{-1}\mathbf{D}$ | ${\mathbf{B}}^{-1}$ | ${\mathbf{B}}^{-1}\mathbf{b}$ |

*7-14. Consider the following LP:

$$
\text{ Maximize }z = {c}_{1}{x}_{1} + {c}_{2}{x}_{2} + {c}_{3}{x}_{3} + {c}_{4}{x}_{4}
$$

subject to

$$
{\mathbf{P}}_{1}{x}_{1} + {\mathbf{P}}_{2}{x}_{2} + {\mathbf{P}}_{3}{x}_{3} + {\mathbf{P}}_{4}{x}_{4} = \mathbf{b}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

The vectors ${\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3}$ , and ${\mathbf{P}}_{4}$ are shown in Figure 7.4. Assume that the basis $\mathbf{B}$ of the current iteration is comprised of ${\mathbf{P}}_{1}$ and ${\mathbf{P}}_{2}$ .

(a) If the vector ${\mathbf{P}}_{1}$ enters the basis, which of the current two basic vectors must leave in order for the resulting basic solution to be feasible?

(b) Can the vector ${\mathbf{P}}_{4}$ be part of a feasible basis?

![bo_d56m4hbef24c73bhe5s0_28_487_200_466_518_0.jpg](bo_d56m4hbef24c73bhe5s0_28_487_200_466_518_0.jpg)

FIGURE 7.4

Vector representation of Problem 7-14

*7-15. Prove that, in any simplex iteration, ${z}_{j} - {c}_{j} = 0$ for all the associated basic variables.

7-16. Prove that if ${z}_{j} - {c}_{j} > 0\left( { < 0}\right)$ for all the nonbasic variables ${x}_{j}$ of a maximization (minimization) LP problem, then the optimum is unique. Else, if ${z}_{j} - {c}_{j}$ equals zero for a nonbasic ${x}_{j}$ , then the problem has an alternative optimum solution.

7-17. In an all-slack starting basic solution, show using the matrix form of the tableau that the mechanical procedure used in Section 3.3 in which the objective equation is set as $z - \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j} = 0$ automatically computes the proper ${z}_{j} - {c}_{j}$ for all the variables in the starting tableau.

7-18. Using the matrix form of the simplex tableau, show that in an all-artificial starting basic solution, the procedure in Section 3.4.1 that substitutes out the artificial variables in the objective function (using the constraint equations) actually computes the ${z}_{j} - {c}_{j}$ for all the variables in the starting tableau.

7-19. Consider an LP in which the variable ${x}_{k}$ is unrestricted in sign. Prove that by substituting ${x}_{k} = {x}_{k}^{ - } - {x}_{k}^{ + }$ , where ${x}_{k}^{ - }$ and ${x}_{k}^{ + }$ are nonnegative, it is impossible that the two variables replace one another in an alternative optimum solution.

7-20. Consider the implementation of the feasibility condition of the simplex method. Specify the mathematical conditions for encountering a degenerate solution (at least one basic variable $= 0$ ) for the first time, for continuing to obtain a degenerate solution in the next iteration, and for removing degeneracy in the next iteration.

*7-21. Consider the general LP in equation form with $m$ equations and $n$ unknowns. Determine the maximum number of adjacent extreme points that can be reached from a nondegenerate extreme point (all basic variable are $> 0$ ) of the solution space.

7-22. In applying the feasibility condition of the simplex method, suppose that ${x}_{k} = 0$ is a basic variable and that ${x}_{j}$ is the entering variable with ${\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{k} \neq  0$ . Prove that the resulting basic solution remains feasible even if ${\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{k}$ is negative.

*7-23. What are the relationships between extreme points and basic solutions under degeneracy and nondegeneracy? What is the maximum number of iterations that can be performed at a given extreme point assuming no cycling?

*7-24. Consider the LP, maximize $z = \mathbf{{CX}}$ subject to $\mathbf{{AX}} \leq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}$ , where $\mathbf{b} \geq  \mathbf{0}$ . Suppose that the entering vector ${\mathbf{P}}_{j}$ is such that at least one element of ${\mathbf{B}}^{-1}{\mathbf{P}}_{j}$ is positive.

(a) If ${\mathbf{P}}_{j}$ is replaced with $\alpha {\mathbf{P}}_{j}$ , where $\alpha$ is a positive scalar, and provided ${x}_{j}$ remains the entering variable, find the relationship between the values of ${x}_{j}$ corresponding to ${\mathbf{P}}_{j}$ and $\alpha {\mathbf{P}}_{j}$ .

(b) Answer Part (a) if, additionally, $\mathbf{b}$ is replaced with $\beta \mathbf{b}$ , where $\beta$ is a positive scalar.

7-25. Consider the LP

$$
\text{ Maximize }z = \mathbf{{CX}}\text{ subject to }\mathbf{{AX}} \leq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}\text{ , where }\mathbf{b} \geq  \mathbf{0}
$$

After obtaining the optimum solution, it is suggested that a nonbasic variable ${x}_{j}$ can be made basic (profitable) by reducing the resource requirements per unit of ${x}_{j}$ to $\frac{1}{\alpha }$ of their original values, $\alpha  > 1$ . Since the requirements per unit are reduced, it is expected that the profit per unit of ${x}_{j}$ will also be reduced to $\frac{1}{\alpha }$ of its original value. Will these changes make ${x}_{j}$ a profitable variable? Explain mathematically.

7-26. Consider the LP

$$
\text{ Maximize }z = \mathbf{{CX}}\text{ subject to }\left( {\mathbf{A},\mathbf{I}}\right) \mathbf{X} = \mathbf{b},\mathbf{X} \geq  \mathbf{0}
$$

Define ${\mathbf{X}}_{B}$ as the current basic vector with $\mathbf{B}$ as its associated basis and ${\mathbf{C}}_{B}$ as its vector of objective coefficients. Show that if ${\mathbf{C}}_{B}$ is replaced with the new coefficients ${\mathbf{D}}_{B}$ , the values of ${z}_{j} - {c}_{j}$ for the basic vector ${\mathbf{X}}_{B}$ will remain equal to zero. What is the significance of this result?

7-27. In Example 7.2-1, summarize the data of iteration 1 in the tableau format of Section 3.3.

7-28. Solve the following LPs by the revised simplex method:

(a) Maximize $z = 6{x}_{1} - 2{x}_{2} + 3{x}_{3}$ subject to

$$
2{x}_{1} - {x}_{2} + 2{x}_{3} \leq  2
$$

$$
{x}_{1}\; + 4{x}_{3} \leq  4
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

*(b) Maximize $z = 2{x}_{1} + {x}_{2} + 2{x}_{3}$

subject to

$$
4{x}_{1} + 3{x}_{2} + 8{x}_{3} \leq  {12}
$$

$$
4{x}_{1} + {x}_{2} + {12}{x}_{3} \leq  8
$$

$$
4{x}_{1} - \;{x}_{2} + \;3{x}_{3} \leq  \;8
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

(c) Minimize $z = 2{x}_{1} + {x}_{2}$

subject to

$$
3{x}_{1} + {x}_{2} = 3
$$

$$
4{x}_{1} + 3{x}_{2} \geq  6
$$

$$
{x}_{1} + 2{x}_{2} \leq  3
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(d) Minimize $z = 5{x}_{1} - 4{x}_{2} + 6{x}_{3} + 8{x}_{4}$

subject to

$$
{x}_{1} + 7{x}_{2} + 3{x}_{3} + 7{x}_{4} \leq  {46}
$$

$$
3{x}_{1} - {x}_{2} + {x}_{3} + 2{x}_{4} \leq  {20}
$$

$$
2{x}_{1} + 3{x}_{2} - {x}_{3} + {x}_{4} \geq  {18}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

7-29. Solve the following LP by the revised simplex method given the starting basic feasible vector ${\mathbf{X}}_{{B}_{0}} = {\left( {x}_{2},{x}_{4},{x}_{5}\right) }^{T}$ .

$$
\text{ Minimize }z = 7{x}_{2} + {11}{x}_{3} - {10}{x}_{4} + {26}{x}_{6}
$$

subject to

$$
{x}_{2} - {x}_{3}\; + {x}_{5} + {x}_{6} = 3
$$

$$
{x}_{2} - {x}_{3} + {x}_{4}\; + 3{x}_{6} = 4
$$

$$
{x}_{1} + {x}_{2} - 3{x}_{3} + {x}_{4} + {x}_{5}\; = 6
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5},{x}_{6} \geq  0
$$

7-30. Solve the following using the two-phase revised simplex method:

(a) Problem 7-28(c).

(b) Problem 7-28(d).

(c) Problem 7-29 (ignore the given starting ${\mathbf{X}}_{{B}_{0}}$ ).

7-31. Revised Dual Simplex Method. The steps of the revised dual simplex method (using matrix manipulations) can be summarized as follows:

Step 0. Let ${\mathbf{B}}_{0} = \mathbf{I}$ be the starting basis for which at least one of the elements of ${\mathbf{X}}_{{B}_{0}}$ is negative (infeasible).

Step 1. Compute ${\mathbf{X}}_{B} = {\mathbf{B}}^{-1}\mathbf{b}$ , the current values of the basic variables. Select the leaving variable ${x}_{r}$ as the one having the most negative value. If all the elements of ${\mathbf{X}}_{B}$ are nonnegative, stop; the current solution is feasible (and optimal).

Step 2. (a) Compute ${z}_{j} - {c}_{j} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{P}}_{j} - {c}_{j}$ for all the nonbasic variables ${x}_{j}$ .

(b) For all the nonbasic variables ${x}_{j}$ , compute the constraint coefficients ${\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{r}$ associated with the row of the leaving variable ${x}_{r}$ .

(c) The entering variable is associated with

$$
\theta  = \mathop{\min }\limits_{i}\left\{  {\left| \frac{{z}_{j} - {c}_{j}}{{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{r}}\right| ,{\left( {\mathbf{B}}^{-1}{\mathbf{P}}_{j}\right) }_{r} < 0}\right\}
$$

If all ${\left( {\mathrm{B}}^{-1}{\mathrm{P}}_{j}\right) }_{r} \geq  0$ , no feasible solution exists.

Step 3. Obtain the new basis by interchanging the entering and leaving vectors $\left( {{\mathbf{P}}_{j}\text{ and }\left. {\mathbf{P}}_{r}\right) }\right.$ . Compute the new inverse and go to step 1.

Apply the method to the following problem:

$$
\text{ Minimize }z = 3{x}_{1} + 2{x}_{2}
$$

subject to

$$
3{x}_{1} + {x}_{2} \geq  3
$$

$$
4{x}_{1} + 3{x}_{2} \geq  6
$$

$$
{x}_{1} + 2{x}_{2} \leq  3
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

7-32. Consider the following linear program:

$$
\text{ Maximize }z = 2{x}_{1} + {x}_{2}
$$

subject to

$$
{x}_{1} + {x}_{2} \leq  3
$$

$$
0 \leq  {x}_{1} \leq  2,0 \leq  {x}_{2} \leq  2
$$

(a) Solve the problem graphically, and trace the sequence of extreme points leading to the optimal solution. (You may use TORA.)

(b) Solve the problem by the upper-bounding algorithm and show that the method produces the same sequence of extreme points as in the graphical optimal solution (you may use TORA to generate the iterations).

(c) How does the upper-bounding algorithm recognize the extreme points?

*7-33. Solve the following problem by the bounded algorithm:

$$
\text{ Maximize }z = 6{x}_{1} + 2{x}_{2} + 8{x}_{3} + 4{x}_{4} + 2{x}_{5} + {10}{x}_{6}
$$

subject to

$$
8{x}_{1} + {x}_{2} + 8{x}_{3} + 2{x}_{4} + 2{x}_{5} + 4{x}_{6} \leq  {13}
$$

$$
0 \leq  {x}_{j} \leq  1, j = 1,2,\ldots ,6
$$

7-34. Solve the following problems by the bounded algorithm:

(a) Minimize $z = 6{x}_{1} - 2{x}_{2} - 3{x}_{3}$

subject to

$$
2{x}_{1} + 4{x}_{2} + 2{x}_{3} \leq  8
$$

$$
{x}_{1} - 2{x}_{2} + 3{x}_{3} \leq  7
$$

$$
0 \leq  {x}_{1} \leq  2,0 \leq  {x}_{2} \leq  2,0 \leq  {x}_{3} \leq  1
$$

(b) Maximize $z = 3{x}_{1} + 5{x}_{2} + 2{x}_{3}$

subject to

$$
{x}_{1} + 2{x}_{2} + 2{x}_{3} \leq  {10}
$$

$$
2{x}_{1} + 4{x}_{2} + 3{x}_{3} \leq  {15}
$$

$$
0 \leq  {x}_{1} \leq  4,0 \leq  {x}_{2} \leq  3,0 \leq  {x}_{3} \leq  3
$$

7-35. In the following problems, some of the variables have positive lower bounds. Use the bounded algorithm to solve these problems.

(a) Maximize $z = 3{x}_{1} + 2{x}_{2} - 2{x}_{3}$ subject to

$$
2{x}_{1} + {x}_{2} + {x}_{3} \leq  8
$$

$$
{x}_{1} + 2{x}_{2} - {x}_{3} \geq  3
$$

$$
1 \leq  {x}_{1} \leq  3,0 \leq  {x}_{2} \leq  3,2 \leq  {x}_{3}
$$

(b) Maximize $z = {x}_{1} + 2{x}_{2}$

subject to

$$
- {x}_{1} + 2{x}_{2} \geq  0
$$

$$
3{x}_{1} + 2{x}_{2} \leq  {10}
$$

$$
- {x}_{1} + {x}_{2} \leq  1
$$

$$
1 \leq  {x}_{1} \leq  3,0 \leq  {x}_{2} \leq  1
$$

(c) Maximize $z = 4{x}_{1} + 2{x}_{2} + 6{x}_{3}$ subject to

$$
4{x}_{1} - {x}_{2}\; \leq  9
$$

$$
- {x}_{1} + {x}_{2} + 2{x}_{3} \leq  8
$$

$$
- 3{x}_{1} + {x}_{2} + 4{x}_{3} \leq  {12}
$$

$$
1 \leq  {x}_{1} \leq  3,0 \leq  {x}_{2} \leq  5,0 \leq  {x}_{3} \leq  2
$$

7-36. Consider the matrix definition of the bounded-variables problem. Suppose that the vector $\mathbf{X}$ is partitioned into $\left( {{\mathbf{X}}_{z},{\mathbf{X}}_{u}}\right)$ , where ${\mathbf{X}}_{u}$ represents the basic and nonbasic variables that will be substituted at upper bound during the course of the algorithm. The problem may thus be written as

$$
\left( \begin{array}{rrr} 1 &  - {\mathbf{C}}_{z} &  - {\mathbf{C}}_{u} \\  0 & {\mathbf{D}}_{z} & {\mathbf{D}}_{u} \end{array}\right) \left( \begin{matrix} z \\  {\mathbf{X}}_{z} \\  {\mathbf{X}}_{u} \end{matrix}\right)  = \left( \begin{array}{l} 0 \\  \mathbf{b} \end{array}\right)
$$

Using ${\mathbf{X}}_{u} = {\mathbf{U}}_{u} - {\mathbf{X}}_{u}^{\prime }$ where ${\mathbf{U}}_{u}$ is a subset of $\mathbf{U}$ representing the upper bounds for ${\mathbf{X}}_{u}$ , let $\mathbf{B}$ (and ${\mathbf{X}}_{B}$ ) be the basis of the current simplex iteration after ${\mathbf{X}}_{u}$ has been substituted out. Show that the associated general simplex tableau is given as

| Basic | ${\mathbf{X}}_{z}^{T}$ | ${\mathbf{X}}^{\prime }{}_{u}^{T}$ | Solution |
| --- | --- | --- | --- |
| $z$ | ${\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{D}}_{z} - {\mathbf{C}}_{z}$ | $- {\mathbf{C}}_{B}{\mathbf{B}}^{-1}{\mathbf{D}}_{u} + {\mathbf{C}}_{u}$ | ${\mathbf{C}}_{u}{\mathbf{B}}^{-1}{\mathbf{B}}^{-1}\left( {\mathbf{b} - {\mathbf{D}}_{u}{\mathbf{U}}_{u}}\right)  + {\mathbf{C}}_{u}{\mathbf{U}}_{u}$ |
| ${\mathbf{X}}_{B}$ | ${\mathbf{B}}^{-1}{\mathbf{D}}_{z}$ | $- {\mathbf{B}}^{-1}{\mathbf{D}}_{u}$ | ${\mathbf{B}}^{-1}\left( {\mathbf{b} - {\mathbf{D}}_{u}{\mathbf{U}}_{u}}\right)$ |

7-37. In Example 7.3-1, do the following:

(a) In Iteration 1, verify that ${\mathbf{X}}_{B} = {\left( {x}_{4},{x}_{1}\right) }^{T} = {\left( \frac{5}{2},\frac{3}{2}\right) }^{T}$ by using matrix manipulation.

(b) In Iteration 2, show how ${\mathbf{B}}^{-1}$ can be computed from the original data of the problem. Then verify the given values of basic ${x}_{4}$ and ${x}_{2}^{\prime }$ using matrix manipulation.

7-38. Solve part (a) of Problem 7-34 using the revised simplex (matrix) version for upper-bounded variables.

7-39. Bounded Dual Simplex Algorithm. The dual simplex algorithm (Section 4.4.1) can be modified to accommodate the bounded variables as follows. Given the upper-bound constraint ${x}_{j} \leq  {u}_{j}$ for all $j$ (if ${u}_{j}$ is infinite, replace it with a sufficiently large upper-bound $M)$ , the LP problem is converted to a dual feasible (i.e., primal optimal) form by using the substitution ${x}_{j} = {u}_{j} - {x}_{j}^{\prime }$ , where necessary.

Step 1. If any of the current basic variables ${\left( {\mathbf{X}}_{B}\right) }_{i}$ exceeds its upper bound, use the substitution ${\left( {\mathbf{X}}_{B}\right) }_{i} = {\left( {\mathbf{U}}_{B}\right) }_{i} - {\left( {\mathbf{X}}_{B}\right) }_{i}^{\prime }$ . Go to step 2.

Step 2. If all the basic variables are feasible, stop. Otherwise, select the leaving variable ${x}_{r}$ as the basic variable having the most negative value. Go to step 3 .

Step 3. Select the entering variable using the optimality condition of the regular dual simplex method (Section 4.4.1). Go to step 4.

Step 4. Perform a change of basis. Go to step 1. Apply the given algorithm to the following problems:

(a) Minimize $z =  - 3{x}_{1} - 2{x}_{2} + 2{x}_{3}$

subject to

$$
2{x}_{1} + {x}_{2} + {x}_{3} \leq  8
$$

$$
- {x}_{1} + 2{x}_{2} + {x}_{3} \geq  {13}
$$

$$
0 \leq  {x}_{1} \leq  2,0 \leq  {x}_{2} \leq  3,0 \leq  {x}_{3} \leq  1
$$

(b) Maximize $z = {x}_{1} + 5{x}_{2} - 2{x}_{3}$

subject to

$$
4{x}_{1} + 2{x}_{2} + 2{x}_{3} \leq  {26}
$$

$$
{x}_{1} + 3{x}_{2} + 4{x}_{3} \geq  {17}
$$

$$
0 \leq  {x}_{1} \leq  2,0 \leq  {x}_{2} \leq  3,{x}_{3} \geq  0
$$

7-40. Prove that the dual of the dual is the primal.

*7-41. Define the dual problem given the primal is $\min z = \{ \mathbf{{CX}} \mid  \mathbf{{AX}} \geq  \mathbf{b},\mathbf{X} \geq  \mathbf{0}\}$ .

7-42. Verify that the dual problem of the numeric example given at the end of Theorem 7.4-1 is correct. Then verify graphically that both the primal and dual problems have no feasible solution.

7-43. Consider the following LP:

$$
\text{ Maximize }z = {50}{x}_{1} + {30}{x}_{2} + {10}{x}_{3}
$$

subject to

$$
2{x}_{1} + {x}_{2} = 1
$$

$$
2{x}_{2}\; =  - 5
$$

$$
4{x}_{1}\; + {x}_{3} = 6
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

(a) Write the dual.

(b) Show by inspection that the primal is infeasible.

(c) Show that the dual in (a) is unbounded.

(d) From Problems 7-42 and 7-43, develop a general conclusion regarding the relationship between infeasibility and unboundedness in the primal and dual problems.

7-44. Consider the following LP:

$$
\text{ Maximize }z = 5{x}_{1} + {12}{x}_{2} + 4{x}_{3}
$$

subject to

$$
2{x}_{1} - {x}_{2} + 3{x}_{3} = 2
$$

$$
{x}_{1} + 2{x}_{2} + {x}_{3} + {x}_{4} = 5
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

(a) Write the dual.

(b) In each of the following cases, first verify that the given basis $\mathbf{B}$ is feasible for the primal. Next, using $\mathbf{Y} = {\mathbf{C}}_{B}{\mathbf{B}}^{-1}$ , compute the associated dual values and verify whether or not the primal solution is optimal.

(i) $\mathbf{B} = \left( {{\mathbf{P}}_{4},{\mathbf{P}}_{3}}\right)$ (iii) $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2}}\right)$

(ii) $\mathbf{B} = \left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ (iv) $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{4}}\right)$

7-45. Consider the following LP:

$$
\text{ Maximize }z = 2{x}_{1} + 4{x}_{2} + 4{x}_{3} - 3{x}_{4}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} = 4
$$

$$
{x}_{1} + 4{x}_{2} + \; + {x}_{4} = 8
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

(a) Write the dual problem.

(b) Verify that $\mathbf{B} = \left( {{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ is optimal by computing ${z}_{j} - {c}_{j}$ for all nonbasic ${\mathbf{P}}_{j}$ .

(c) Find the associated optimal dual solution.

*7-46. An LP model includes two variables ${x}_{1}$ and ${x}_{2}$ and three constraints of the type $\leq$ . The associated slacks are ${x}_{3},{x}_{4}$ , and ${x}_{5}$ . Suppose that the optimal basis is $\mathbf{B} = \left( {{\mathbf{P}}_{1},{\mathbf{P}}_{2},{\mathbf{P}}_{3}}\right)$ , and its inverse is

$$
{\mathbf{B}}^{-1} = \left( \begin{array}{rrr} 0 &  - 1 & 1 \\  0 & 1 & 0 \\  1 & 1 &  - 1 \end{array}\right)
$$

The optimal primal and dual solutions are

$$
{\mathbf{X}}_{B} = {\left( {x}_{1},{x}_{2},{x}_{3}\right) }^{T} = {\left( 1,3,1\right) }^{T}
$$

$$
\mathbf{Y} = \left( {{y}_{1},{y}_{2},{y}_{3}}\right)  = \left( {0,3,2}\right)
$$

Determine the optimal value of the objective function in two ways using the primal and dual problems.

*7-47. Write the dual of max $z = \{ \mathbf{{CX}} \mid  \mathbf{{AX}} = \mathbf{b},\;\mathbf{X}$ unrestricted $\}$ .

7-48. Show that the dual of $\max z = \{ \mathbf{{CX}} \mid  \mathbf{{AX}} \leq  \mathbf{b},\mathbf{0} < \mathbf{L} \leq  \mathbf{X} \leq  \mathbf{U}\}$ always possesses a feasible solution.

*7-49. In Example 7.5-1, suppose that $t$ is unrestricted in sign. Determine the range of $t$ for which ${\mathbf{X}}_{{B}_{0}}$ remains optimal.

7-50. Solve Example 7.5-1, assuming that the objective function is given as

*(a) Maximize $z = \left( {3 + {3t}}\right) {x}_{1} + 2{x}_{2} + \left( {5 - {6t}}\right) {x}_{3}$

(b) Maximize $z = \left( {3 - {2t}}\right) {x}_{1} + \left( {2 + t}\right) {x}_{2} + \left( {5 + {2t}}\right) {x}_{3}$

(c) Maximize $z = \left( {3 + t}\right) {x}_{1} + \left( {2 + {2t}}\right) {x}_{2} + \left( {5 - t}\right) {x}_{3}$

7-51. Study the variation in the optimal solution of the following parameterized LP, given $t \geq  0$ .

$$
\text{ Minimize }z = \left( {4 - t}\right) {x}_{1} + \left( {1 - {3t}}\right) {x}_{2} + \left( {2 - {2t}}\right) {x}_{3}
$$

subject to

$$
3{x}_{1} + {x}_{2} + 2{x}_{3} = 6
$$

$$
4{x}_{1} + 3{x}_{2} + 2{x}_{3} \geq  {12}
$$

$$
{x}_{1} + 2{x}_{2} + 5{x}_{3} \leq  8
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

7-52. The analysis in this section assumes that the optimal solution of the LP at $t = 0$ is obtained by the (primal) simplex method. In some problems, it may be more convenient to obtain the optimal solution by the dual simplex method (Section 4.4.1). Show how the parametric analysis can be carried out in this case, then analyze the LP of Example 4.4-1, assuming that the objective function is given as

$$
\text{ Minimize }z = \left( {3 + t}\right) {x}_{1} + \left( {2 + {4t}}\right) {x}_{2} + {x}_{3}, t \geq  0
$$

*7-53. In Example 7.5-1, suppose that the objective function is nonlinear in $t\left( {t \geq  0}\right)$ and is defined as

$$
\text{ Maximize }z = \left( {3 + 2{t}^{2}}\right) {x}_{1} + \left( {2 - 2{t}^{2}}\right) {x}_{2} + \left( {5 - t}\right) {x}_{3}
$$

Determine the first critical value ${t}_{1}$ .

7-54. In Example 7.5-2, find the first critical value, ${t}_{1}$ , and define the vectors of ${\mathbf{B}}_{1}$ in each of the following cases:

*(a) $\mathbf{b}\left( t\right)  = {\left( {40} + 2t,{60} - 3t,{30} + 6t\right) }^{T}$

(b) $\mathbf{b}\left( t\right)  = {\left( {40} - t,{60} + 2t,{30} - 5t\right) }^{T}$

*7-55. Study the variation in the optimal solution of the following parameterized LP, given $t \geq  0$ :

$$
\text{ Minimize }z = 4{x}_{1} + {x}_{2} + 2{x}_{3}
$$

subject to

$$
3{x}_{1} + {x}_{2} + 2{x}_{3} = 6 + {6t}
$$

$$
4{x}_{1} + 3{x}_{2} + 2{x}_{3} \geq  {12} + {4t}
$$

$$
{x}_{1} + 2{x}_{2} + 5{x}_{3} \leq  8 - {2t}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

7-56. The analysis in this section assumes that the optimal LP solution at $t = 0$ is obtained by the (primal) simplex method. In some problems, it may be more convenient to obtain the optimal solution by the dual simplex method (Section 4.4.1). Show how the parametric analysis can be carried out in this case, and then analyze the LP of Example 4.4-1, assuming that $t \geq  0$ and the right-hand side vector is

$$
\mathbf{b}\left( t\right)  = {\left( 3 + 2t,6 - t,3 - 4t\right) }^{T}
$$

7-57. Solve Problem 7-55 assuming that the right-hand side is changed to

$$
\mathbf{b}\left( t\right)  = {\left( 3 + 3{t}^{2},6 + 2{t}^{2},4 - {t}^{2}\right) }^{T}
$$

Further assume that $t$ can be positive, zero, or negative.
