```markmap
---
markmap:
  height: 650
---
# [[#^Chapter|CHAPTER 4: Duality and Post-Optimal Analysis]]
## [[#^DualDefinition|Dual Problem Definition]]
### [[#^DualMotivation|Why the dual matters]]
### [[#^DualEquationForm|Equation-form primal as the baseline]]
### [[#^DualConstruction|How to construct the dual]]
#### [[#^DualMapping|Constraints ↔ variables correspondence]]
#### [[#^DualRhsToObjective|Primal RHS becomes dual objective coefficients]]
#### [[#^DualTranspose|Transpose a primal column into a dual constraint]]
#### [[#^DualRulesTable|Sense / inequality direction / variable sign rules]]
### [[#^DualSpecialCases|Special correspondence rules]]
#### [[#^UnrestrictedPrimalVar|Unrestricted primal variable ↔ equality dual constraint]]
#### [[#^PrimalEquation|Primal equation ↔ unrestricted dual variable]]
### [[#^DualExamples|Worked constructions (Examples 4.1-1 to 4.1-3)]]
## [[#^RelationshipsSection|Primal–Dual Relationships]]
### [[#^WhyRelationships|Why relationships matter (tableau recomputation)]]
### [[#^MatrixSection|Matrix tools for simplex computations]]
#### [[#^MatrixDefs|Matrix / row-vector / column-vector definitions]]
#### [[#^MatrixOps|Three basic operations used by the tableau]]
### [[#^TableauLayout|Simplex tableau layout and the inverse matrix]]
#### [[#^InverseMatrixRole|Inverse matrix as the computational core]]
### [[#^DualSolutionSection|Recovering the optimal dual solution]]
#### [[#^DualMethodOne|Method 1: z-row coefficient + original objective coefficient]]
#### [[#^DualMethodTwo|Method 2: c_B^T × (optimal inverse)]]
#### [[#^ExampleDualValues|Example 4.2-1: dual values from an optimal tableau]]
### [[#^ObjectiveValueRelation|Objective value relation (z ≤ w; at optimum z = w)]]
### [[#^TableauComputations|Recomputing any tableau iteration]]
#### [[#^FormulaConstraintColumns|Formula 1: compute any constraint/RHS column]]
#### [[#^FormulaObjectiveRow|Formula 2: compute reduced costs from the dual]]
#### [[#^RoundoffRemark|Why this motivates the revised simplex method]]
## [[#^EconomicInterpretation|Economic Interpretation of Duality]]
### [[#^ResourceAllocationView|Primal as activities vs resources]]
### [[#^ShadowPrices|Dual variables as shadow prices (worth per unit)]]
### [[#^ImputedCost|Dual constraints as imputed costs; reduced cost meaning]]
### [[#^ReddyMikksExample|Example 4.3-1: interpreting shadow prices]]
### [[#^ToycoExample|Example 4.3-2: reduced cost and profitability]]
## [[#^AdditionalAlgorithms|Additional Simplex Algorithms]]
### [[#^DualSimplex|Dual simplex algorithm]]
#### [[#^DualFeasibilityRule|Feasibility rule (leaving variable)]]
#### [[#^DualOptimalityRule|Optimality rule (entering variable ratio test)]]
#### [[#^DualSimplexStartRequirements|How to set up the starting tableau]]
#### [[#^DualSimplexExample|Example 4.4-1: dual simplex iterations]]
### [[#^GeneralizedSimplex|Generalized simplex algorithm]]
#### [[#^GeneralizedIdea|Tandem use of dual and primal simplex]]
#### [[#^GeneralizedExample|Example 4.4-2: start infeasible and nonoptimal]]
## [[#^PostOptimalAnalysis|Post-Optimal Analysis]]
### [[#^PostOptimalMotivation|Goal: update the optimum efficiently]]
### [[#^PostOptimalCasesTable|Case table: what changes → which algorithm]]
### [[#^FeasibilityChanges|Changes affecting feasibility]]
#### [[#^RhsChange|Right-hand-side changes (inverse × new RHS)]]
#### [[#^NewConstraint|Adding a new constraint (redundant vs binding)]]
### [[#^OptimalityChanges|Changes affecting optimality]]
#### [[#^ObjectiveCoeffChanges|Changing objective coefficients (recompute y and reduced costs)]]
#### [[#^NewActivity|Adding a new activity (variable): check reduced cost]]
#### [[#^FireEngineExample|Example 4.5-4: add a profitable new product]]
### [[#^PostOptimalLimitations|Key limitation: changing basic columns breaks the inverse]]
## [[#^Bibliography|Bibliography]]
## [[#^ProblemsSection|Problems]]
```


## CHAPTER 4 Duality and Post-Optimal Analysis ^Chapter

### 4.1 DEFINITION OF THE DUAL PROBLEM ^DualDefinition

The dual problem is defined systematically from the primal (or original) LP model. The two problems are closely related, in the sense that the optimal solution of one problem automatically provides the optimal solution to the other. As such, it may be advantageous computationally in some cases to determine the primal solution by solving the dual. But that computational advantage may be minor when compared with what the rich primal-dual theory offers, as we will demonstrate throughout the book. ^DualMotivation

In all textbooks this author is familiar with, the dual is defined for various forms of the primal depending on the sense of optimization (maximization or minimization), types of constraints $\left( { \leq  , \geq  ,\text{ or } = }\right)$ , and sign of the variables (nonnegative or unrestricted). Not only are there too many combinations to memorize, but their use may require a degree of reconciling with the simplex algorithm results, primarily because the primal from which the dual is constructed is not in the standard format used by the simplex algorithm (e.g., the primal from which the dual is constructed may have negative right-hand sides in the constraints).

This book offers a single definition that automatically subsumes all forms of the primal. Our definition of the dual problem requires expressing the primal problem in the equation form presented in Section 3.1, a format consistent with the simplex starting tableau (all the constraints are equations with nonnegative right-hand sides, and all the variables are nonnegative). Hence, any results obtained from the primal optimal solution apply unambiguously to the associated dual problem. ^DualEquationForm

The following is a summary of how the dual is constructed from the (equation-form) primal: ^DualConstruction

1. A dual variable is assigned to each primal (equation) constraint and a dual constraint is assigned to each primal variable. ^DualMapping

2. The right-hand sides of the primal constraints provide the coefficients of the dual objective function. ^DualRhsToObjective

TABLE 4.1 Rules for Constructing the Dual Problem ^DualRulesTable

| Primal problem objective ${}^{a}$ | Dual problem objective | Dual constraints type ${}^{\mathrm{b}}$ | Dual variables sign |
| --- | --- | --- | --- |
| Maximization | Minimization | $\ge$ | Unrestricted |
| Minimization | Maximization | $\le$ | Unrestricted |

${}^{a}$ All primal constraints are equations with nonnegative right-hand sides, and all the variables are nonnegative. ${}^{b}$ A convenient way to remember the constraint type $\left( { \geq  \text{ or } \leq  }\right)$ in the dual is that if the dual objective is a "pointing-down" minimization, then all the constraints are "pointing-up" $\left(  \geq  \right)$ -inequalities. The opposite applies when the dual objective is maximization.

3. The dual constraint corresponding to a primal variable is constructed by transposing the primal variable column into a row with (i) the primal objective coefficient becoming the dual right-hand side and (ii) the remaining constraint coefficients comprising the dual left-hand side coefficients. ^DualTranspose

4. The sense of optimization, direction of inequalities, and the signs of the variables in the dual are governed by the rules in Table 4.1

The following examples demonstrate the use of the rules in Table 4.1. The examples also show that our definition incorporates all forms of the primal automatically. ^DualExamples

Example 4.1-1

| Primal | Primal in equation form | Dual variables |
| --- | --- | --- |
| Maximize $z = 5{x}_{1} + 12{x}_{2} + 4{x}_{3}$ subject to | Maximize $z = 5{x}_{1} + 12{x}_{2} + 4{x}_{3} + 0{x}_{4}$ subject to |  |
| ${x}_{1} + 2{x}_{2} + {x}_{3} \le 10$ | ${x}_{1} + 2{x}_{2} + {x}_{3} + {x}_{4} = 10$ | ${y}_{1}$ |
| $2{x}_{1} - {x}_{2} + 3{x}_{3} = 8$ | $2{x}_{1} - {x}_{2} + 3{x}_{3} + 0{x}_{4} = 8$ | ${y}_{2}$ |
| ${x}_{1},{x}_{2},{x}_{3} \ge 0$ | ${x}_{1},{x}_{2},{x}_{3},{x}_{4} \ge 0$ |  |

Dual Problem

$$
\text{ Minimize }w = {10}{y}_{1} + 8{y}_{2}
$$

subject to

$$
{y}_{1} + 2{y}_{2} \geq  5
$$

$$
2{y}_{1} - {y}_{2} \geq  {12}
$$

$$
{y}_{1} + 3{y}_{2} \geq  4
$$

$$
\left. \begin{array}{r} {y}_{1} + 0{y}_{2} \geq  0 \\  {y}_{1},{y}_{2}\text{ unrestricted } \end{array}\right\}   \Rightarrow  \left( {{y}_{1} \geq  0,{y}_{2}\text{ unrestricted }}\right)
$$

Example 4.1-2

| Primal | Primal in equation form | Dual variables |
| --- | --- | --- |
| Minimize $z = 15{x}_{1} + 12{x}_{2}$<br>subject to | Minimize $z = 15{x}_{1} + 12{x}_{2} + 0{x}_{3} + 0{x}_{4}$<br>subject to |  |
| ${x}_{1} + 2{x}_{2} \ge 3$ | ${x}_{1} + 2{x}_{2} - {x}_{3} + 0{x}_{4} = 3$ | ${y}_{1}$ |
| $2{x}_{1} - 4{x}_{2} \le 5$ | $2{x}_{1} - 4{x}_{2} + 0{x}_{3} + {x}_{4} = 5$ | ${y}_{2}$ |
| ${x}_{1},{x}_{2} \ge 0$ | ${x}_{1},{x}_{2},{x}_{3},{x}_{4} \ge 0$ |  |

Dual Problem

$$
\text{ Maximize }w = 3{y}_{1} + 5{y}_{2}
$$

subject to

$$
{y}_{1} + 2{y}_{2} \leq  {15}
$$

$$
2{y}_{1} - 4{y}_{2} \leq  {12}
$$

$$
\left. \begin{aligned}  - {y}_{1} &  \leq  0 \\  {y}_{2} &  \leq  0 \\  {y}_{1},{y}_{2} & \text{ unrestrricted } \end{aligned}\right\}   \Rightarrow  \left( {{y}_{1} \geq  0,{y}_{2} \leq  0}\right)
$$

Example 4.1-3

| Primal | Primal in equation form | Dual variables |
| --- | --- | --- |
| Maximize $z = 5{x}_{1} + 6{x}_{2}$ subject to | Substitute ${x}_{1} = {x}_{1}^{-} - {x}_{1}^{+}$.<br>Maximize $z = 5{x}_{1}^{-} - 5{x}_{1}^{+} + 6{x}_{2}$<br>subject to |  |
| ${x}_{1} + 2{x}_{2} = 5$ | ${x}_{1}^{-} - {x}_{1}^{+} + 2{x}_{2}$ | ${y}_{1}$ |
| $- {x}_{1} + 5{x}_{2} \ge 3$ | $- {x}_{1}^{-} + {x}_{1}^{+} + 5{x}_{2} - {x}_{3} = 3$ | ${y}_{2}$ |
| $4{x}_{1} + 7{x}_{2} \le 8$ | $4{x}_{1}^{-} - 4{x}_{1}^{+} + 7{x}_{2} + {x}_{4} = 8$ | ${y}_{3}$ |
| ${x}_{1}$ unrestricted, ${x}_{2} \ge 0$ | ${x}_{1}^{-},{x}_{1}^{+},{x}_{2},{x}_{3},{x}_{4} \ge 0$ |  |

Dual Problem

$$
\text{ Minimize }z = 5{y}_{1} + 3{y}_{2} + 8{y}_{3}
$$

subject to

$$
\left. \begin{array}{r} {y}_{1} - {y}_{2} + 4{y}_{3} \geq  5 \\   - {y}_{1} + {y}_{2} - 4{y}_{3} \geq   - 5 \end{array}\right\}   \Rightarrow  \left. \begin{array}{r} {y}_{1} - {y}_{2} + 4{y}_{3} \geq  5 \\  {y}_{1} - {y}_{2} + 4{y}_{3} \leq  5 \end{array}\right\}   \Rightarrow  {y}_{1} - {y}_{2} + 4{y}_{3} = 5
$$

$$
2{y}_{1} + 5{y}_{2} + 7{y}_{3} \geq  6
$$

$$
\left. \begin{array}{r}  - {y}_{2} \geq  0 \\  {y}_{3} \geq  0 \\  {y}_{1},{y}_{2},{y}_{3}\text{ unrestricted } \end{array}\right\}   \Rightarrow  \left( {{y}_{1}\text{ unrestricted },{y}_{2} \leq  0,{y}_{3} \geq  0}\right)
$$

The first and second constraints are replaced by an equation. ^DualSpecialCases

The general rule is that an unrestricted primal variable always corresponds to an equality dual constraint. ^UnrestrictedPrimalVar

Conversely, a primal equation produces an unrestricted dual variable, as the first primal constraint demonstrates. ^PrimalEquation

TABLE 4.2 Rules for Constructing the Dual Problem

| Maximization problem |  | Minimization problem |
| --- | --- | --- |
| Constraints |  | Variables |
| $\ge$ | $\Leftrightarrow$ | $\le 0$ |
| $\le$ | $\Leftrightarrow$ | $\ge 0$ |
| $=$ |  | Unrestricted |
| Variables |  | Constraints |
| $\ge 0$ |  | $\ge$ |
| $\le 0$ | $\Leftrightarrow$ | $\le$ |
| Unrestricted | $\Leftrightarrow$ | $=$ |

Summary of the rules for constructing the dual. Table 4.2 summarizes the primal-dual rules as they are usually presented in the literature. It is a good exercise to verify that these explicit rules are subsumed by the two rules in Table 4.1.

Note that the column headings in the table do not use the designation primal and dual. What matters here is the sense of optimization. If the primal is maximization, then the dual is minimization, and vice versa. Note also that no provision is made for including artificial variables in the primal because artificial variables would not change the definition of the dual (see Problem 4-5).

### 4.2 PRIMAL-DUAL RELATIONSHIPS ^RelationshipsSection

Changes made in the data of an LP model can affect the optimality and/or the feasibility of the current optimum solution. This section introduces a number of primal-dual relationships that can be used to recompute the elements of the optimal simplex tableau. These relationships form the basis for the economic interpretation of the LP model and for post-optimality analysis. ^WhyRelationships

The section starts with a brief review of matrices, a convenient tool for carrying out the simplex tableau computations. A more detailed review of matrices is given in Appendix D on the website.

#### 4.2.1 Review of Simple Matrix Operations ^MatrixSection

The simplex tableau can be generated by three elementary matrix operations: (row vector) $\times  \left( \text{ matrix }\right) ,\left( \text{ matrix }\right)  \times  \left( \text{ column vector }\right)$ , and (scalar) $\times  \left( \text{ matrix }\right)$ . ^MatrixOps

These operations are summarized here for convenience. First, we introduce some matrix definitions: ^MatrixDefs

1. A matrix, $\mathbf{A}$ , of size $\left( {m \times  n}\right)$ is a rectangular array of elements with $m$ rows and $n$ columns.

2. A row vector, $\mathbf{V}$ , of size $m$ is a $\left( {1 \times  m}\right)$ matrix.

3. A column vector, $\mathbf{P}$ , of size $n$ is an $\left( {n \times  1}\right)$ matrix.

These definitions can be represented mathematically as

$$
\mathbf{V} = \left( {{v}_{1},{v}_{2},\ldots ,{v}_{m}}\right) ,\mathbf{A} = \left( \begin{matrix} {a}_{11} & {a}_{12} & \cdots & {a}_{1n} \\  {a}_{21} & {a}_{22} & \cdots & {a}_{2n} \\  \cdots & \cdots & \cdots & \cdots \\  {a}_{m1} & {a}_{m2} & \cdots & {a}_{mn} \end{matrix}\right) ,\mathbf{P} = \left( \begin{matrix} {p}_{1} \\  {p}_{2} \\  \cdots \\  {p}_{n} \end{matrix}\right)
$$

1. (Row vector $\times$ matrix, VA). The operation is valid only if the size of the row vector $\mathbf{V}$ and the number of rows of $\mathbf{A}$ are equal. For example,

$$
\left( {{11},{22},{33}}\right) \left( \begin{array}{ll} 1 & 2 \\  3 & 4 \\  5 & 6 \end{array}\right)  = \left( {1 \times  {11} + 3 \times  {22} + 5 \times  {33},2 \times  {11} + 4 \times  {22} + 6 \times  {33}}\right)
$$

$$
= \left( {{242},{308}}\right)
$$

2. (Matrix $\times$ column vector, AP). The operation is valid only if the number of columns of $\mathbf{A}$ and the size of column vector $\mathbf{P}$ are equal. For example,

$$
\left( \begin{array}{lll} 1 & 3 & 5 \\  2 & 4 & 6 \end{array}\right) \left( \begin{array}{l} {11} \\  {22} \\  {33} \end{array}\right)  = \left( \begin{array}{l} 1 \times  {11} + 3 \times  {22} + 5 \times  {33} \\  2 \times  {11} + 4 \times  {22} + 6 \times  {33} \end{array}\right)  = \left( \begin{array}{l} {242} \\  {308} \end{array}\right)
$$

3. (Scalar $\times$ matrix, $\mathbf{{\alpha A}}$ ). Given the scalar (or constant) quantity $\alpha$ , the multiplication operation $\alpha \mathbf{A}$ results in a matrix of the same size as matrix $\mathbf{A}$ . For example, given $\alpha  = {10}$ ,

$$
\left( {10}\right) \left( \begin{array}{lll} 1 & 2 & 3 \\  4 & 5 & 6 \end{array}\right)  = \left( \begin{array}{lll} {10} & {20} & {30} \\  {40} & {50} & {60} \end{array}\right)
$$

#### 4.2.2 Simplex Tableau Layout ^TableauLayout

The simplex tableau in Chapter 3 is the basis for the presentation in this chapter. Figure 4.1 represents the starting and general simplex tableaus schematically. In the starting tableau, the constraint coefficients under the starting variables form an identity matrix (all main-diagonal elements are 1, and all off-diagonal elements are zero). With this arrangement, subsequent iterations of the simplex tableau generated by the Gauss-Jordan row operations (see Chapter 3) modify the elements of the identity matrix to produce what is known as the inverse matrix. As we will see in the remainder of this chapter, the inverse matrix is key to computing all the elements of the associated simplex tableau. ^InverseMatrixRole

Remarks. The inverse matrix in the general tableau has its roots in the starting tableau constraint columns. That means that the inverse at any iteration can be computed (from scratch) using the original constraint columns of the LP problem (as will be demonstrated in the remarks following Example 4.2-1). This is an important relationship that has been exploited to control round-off errors in the simplex algorithm computations.

![bo_d56m4aref24c73bhe5pg_5_363_196_1148_903_0.jpg](bo_d56m4aref24c73bhe5pg_5_363_196_1148_903_0.jpg)

FIGURE 4.1

Schematic representation of the starting and general simplex tableaus

#### 4.2.3 Optimal Dual Solution ^DualSolutionSection

The primal and dual solutions are closely related, in the sense that the optimal solution of either problem directly yields the optimal solution to the other, as is explained subsequently. Thus, in an LP model in which the number of variables is considerably smaller than the number of constraints, computational savings may be realized by solving the dual because the amount of computations associated with determining the inverse matrix primarily increases with the number of constraints. Notice that the rule addresses only the amount of computations in each iteration but says nothing about the total number of iterations needed to solve each problem.

This section provides two methods for determining the dual values.

Method 1. ^DualMethodOne

$$
\left( \begin{matrix} \text{ Optimal value of } \\  \text{ dual variable }{y}_{i} \end{matrix}\right)  = \left( \begin{matrix} \text{ Optimal primal }z\text{ -coefficient of starting basic variable }{x}_{i} \\   + \\  \text{ Original objective coefficient of }{x}_{i} \end{matrix}\right)
$$

Method 2. ^DualMethodTwo

$$
\left( \begin{array}{l} \text{ Optimal values } \\  \text{ of dual variables } \end{array}\right)  = \left( \begin{matrix} \text{ Row vector of } \\  \text{ original objective coefficients } \\  \text{ of optimal primal basic variables } \end{matrix}\right)  \times  \left( \begin{matrix} \text{ Optimal primal } \\  \text{ inverse } \end{matrix}\right)
$$

The elements of the row vector must appear in the same order the basic variables are listed in the Basic-column of the simplex tableau.

Example 4.2-1 ^ExampleDualValues

Consider the following LP:

$$
\text{ Maximize }z = 5{x}_{1} + {12}{x}_{2} + 4{x}_{3}
$$

Subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} \leq  {10}
$$

$$
2{x}_{1} - {x}_{2} + 3{x}_{3} = 8
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

To prepare the problem for solution by the simplex method, we add a slack ${x}_{4}$ in the first constraint and an artificial $R$ in the second. The resulting primal and the associated dual problems are thus defined as follows:

| **Primal**                                                                                                                                                            | **Dual**                                                                                                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Maximize $z = 5x_{1} + 12x_{2} + 4x_{3} - MR$ <br> subject to <br> $x_{1}+2x_{2}+x_{3}+x_{4}=10$ <br> $2x_{1}-x_{2}+3x_{3}+R=8$ <br> $x_{1},x_{2},x_{3},x_{4},R\ge 0$ | Minimize $w = 10y_{1}+8y_{2}$ <br> subject to <br> $y_{1}+2y_{2}\ge 5$ <br> $2y_{1}-y_{2}\ge 12$ <br> $y_{1}+3y_{2}\ge 4$ <br> $y_{1}\ge 0$ <br> $y_{2}\ge -M\;(\Rightarrow y_{2}\text{ unrestricted})$ |

Table 4.3 provides the optimal primal tableau.

We now show how the optimal dual values are determined using the two methods described at the start of this section.

Method 1. In Table 4.3, the starting primal variables ${x}_{4}$ and $R$ uniquely correspond to the dual variables ${y}_{1}$ and ${y}_{2}$ , respectively. Thus, we determine the optimum dual solution as follows:

|  | ${x}_{4}$ | $R$ |
| --- | --- | --- |
| Starting primal basic variables | ${x}_{4}$ | $R$ |
| $z$-equation coefficients | $\frac{29}{5}$ | $-\frac{2}{5} + M$ |
| Original objective coefficient | 0 | $-M$ |
| Dual variables | ${y}_{1}$ | ${y}_{2}$ |
| Optimal dual values | $\frac{29}{5}$ | $-\frac{2}{5}$ |

Method 2. The optimal inverse matrix, highlighted in Table 4.3 under the starting variables ${x}_{4}$ and $R$ , is

$$
\text{ Optimal inverse } = \left( \begin{matrix} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{matrix}\right)
$$

TABLE 4.3 Optimal Tableau of the Primal of Example 4.2-1

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | $R$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | $\frac{3}{5}$ | $\frac{29}{5}$ | $-\frac{2}{5} + M$ | $54\frac{4}{5}$ |
| ${x}_{2}$ | 0 | 1 | $-\frac{1}{5}$ | $\frac{2}{5}$ | $-\frac{1}{5}$ | $\frac{12}{5}$ |
| ${x}_{1}$ | 1 | 0 | 7 | 1 | $\frac{2}{5}$ | $\frac{26}{5}$ |

The order of the optimal primal basic variables in the Basic-column is ${x}_{2}$ followed by ${x}_{1}$ . The elements of the original objective coefficients for the two variables must appear in the same order-namely,

$$
\text{ (Original objective coefficients) } = \left( {\text{ Coefficient of }{x}_{2}\text{ , coefficient of }{x}_{1}}\right)
$$

$$
= \left( {{12},5}\right)
$$

The optimal dual values are

$$
\left( {{y}_{1},{y}_{2}}\right)  = \left( \begin{matrix} \text{ Original objective } \\  \text{ coefficients of }{x}_{2},{x}_{1} \end{matrix}\right)  \times  \left( \text{ Optimal inverse }\right)
$$

$$
= \left( {{12},5}\right) \left( \begin{matrix} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{matrix}\right)
$$

$$
= \left( {\frac{29}{5}, - \frac{2}{5}}\right)
$$

Remarks. We pause here to demonstrate the important relationship between the inverse matrix in a simplex tableau and the associated basic matrix obtained from original constraint columns in the starting tableau. For example, in the optimal tableau, the basic variables, taken in order, are $\left( {{x}_{2},{x}_{1}}\right)$ . Hence, the associated (optimal) basic matrix is obtained from the original problem as

$$
\left( \begin{matrix} \text{ Optimal } \\  \text{ basic } \\  \text{ matrix } \end{matrix}\right)  = \left( \begin{matrix} \text{ Constraint } & \text{ Constraint } \\  \text{ column of } & \text{ column of } \\  {x}_{2} & {x}_{1} \end{matrix}\right)  = \left( \begin{array}{rr} 2 & 1 \\   - 1 & 2 \end{array}\right)
$$

When this basic matrix is inverted (using one of the methods in Appendix D on the website), it will yield the inverse in the optimum tableau. We can verify that this is true because matrix theory tells us that the product of the basic matrix and its inverse must be an identity matrix; namely,

$$
\left( \begin{array}{rr} 2 & 1 \\   - 1 & 2 \end{array}\right)  \times  \left( \begin{array}{rr} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{array}\right)  = \left( \begin{array}{ll} 1 & 0 \\  0 & 1 \end{array}\right)
$$

The relationship holds true for any simplex iteration. Note importantly that the columns of the basic matrix must coincide with the order of the basic variables in the tableau.

![bo_d56m4aref24c73bhe5pg_8_548_197_861_225_0.jpg](bo_d56m4aref24c73bhe5pg_8_548_197_861_225_0.jpg)

FIGURE 4.2

Relationship between maximum $z$ and minimum $w$

Primal-dual objective values. For any pair of feasible primal and dual solutions, ^ObjectiveValueRelation

$$
\left( \begin{array}{l} \text{ Objective value in the } \\  \text{ maximization problem } \end{array}\right)  \leq  \left( \begin{array}{l} \text{ Objective value in the } \\  \text{ minimization problem } \end{array}\right)
$$

At the optimum, the relationship holds as a strict equation, meaning that the two objective values are equal. Note that the relationship does not specify which problem is primal and which is dual. Only the sense of optimization (maximization or minimization) is important in this case.

The optimum cannot occur with $z$ strictly less than $w$ (i.e., $z < w$ ) because, no matter how close the two values are, there is always room for improvement, which contradicts optimality as Figure 4.2 demonstrates.

## Example 4.2-2

In Example 4.2-1, $\left( {{x}_{1} = 0,{x}_{2} = 0,{x}_{3} = \frac{8}{3}}\right)$ and $\left( {{y}_{1} = 6,{y}_{2} = 0}\right)$ are (arbitrary) feasible primal and dual solutions. The associated values of the objective functions are

Maximization (primal): $z = 5{x}_{1} + {12}{x}_{2} + 4{x}_{3} = 5\left( 0\right)  + {12}\left( 0\right)  + 4\left( \frac{8}{3}\right)  = {10}\frac{2}{3}$

Minimization (dual): $w = {10}{y}_{1} + 8{y}_{2} = {10}\left( 6\right)  + 8\left( 0\right)  = {60}$

Since $z < w$ , the solutions are not optimal. The optimum value of $z\left( { = {54}\frac{4}{5}}\right)$ falls within the range $\left( {{10}^{\frac{2}{3}},{60}}\right)$ .

#### 4.2.4 Simplex Tableau Computations ^TableauComputations

This section shows how any iteration of the simplex tableau can be generated from the original data of the problem, the inverse associated with the iteration, and the dual problem. Using the layout of the simplex tableau in Figure 4.1, we can divide the computations into two types:

1. Constraint columns (left-hand and right-hand sides).

2. Objective $z$ -row.

Formula 1: Constraint column computations. In any simplex iteration, a left-hand or a right-hand side column is computed as follows: ^FormulaConstraintColumns

$$
\left( \begin{matrix} \text{ Constraint column } \\  \text{ in iteration }i \end{matrix}\right)  = \left( \begin{matrix} \text{ Inverse in } \\  \text{ iteration }i \end{matrix}\right)  \times  \left( \begin{matrix} \text{ Original } \\  \text{ constraint column } \end{matrix}\right)
$$

Formula 2: Objective $z$ -row computations. In any simplex iteration, the objective equation coefficient (reduced cost) of ${x}_{j}$ is computed as follows: ^FormulaObjectiveRow

$$
\left( \begin{matrix} \text{ Primal z-equation } \\  \text{ coefficient of variable }{x}_{j} \end{matrix}\right)  = \left( \begin{matrix} \text{ Left-hand side of } \\  j\text{ th dual constraint } \end{matrix}\right)  - \left( \begin{matrix} \text{ Right-hand side of } \\  j\text{ th dual constraint } \end{matrix}\right)
$$

Example 4.2-3

We use the LP in Example 4.2-1 to illustrate the application of Formulas 1 and 2. From the optimal tableau in Table 4.3, we have

$$
\text{ Optimal inverse } = \left( \begin{array}{rr} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{array}\right)
$$

$$
\left( \begin{matrix} {x}_{1}\text{ -column in } \\  \text{ optimal iteration } \end{matrix}\right)  = \left( \begin{matrix} \text{ Inverse in } \\  \text{ optimal iteration } \end{matrix}\right)  \times  \left( \begin{matrix} \text{ original } \\  {x}_{1}\text{ -column } \end{matrix}\right)
$$

$$
= \left( \begin{array}{rr} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{array}\right)  \times  \left( \begin{array}{l} 1 \\  2 \end{array}\right)  = \left( \begin{array}{l} 0 \\  1 \end{array}\right)
$$

Similar computations generate the optimal columns for ${x}_{2},{x}_{3},{x}_{4}, R$ , and the right-hand side (verify!).

Next, we demonstrate how the objective row computations are carried out with Formula 2. The optimal values of the dual variables, $\left( {{y}_{1},{y}_{2}}\right)  = \left( {\frac{29}{5}, - \frac{2}{5}}\right)$ , are computed in Example 4.2-1. These values are used in Formula 2 to compute all the $z$ -coefficients, as illustrated here for ${x}_{1}$ and $R$ .

$$
z\text{ -cofficient of }{x}_{1} = {y}_{1} + 2{y}_{2} - 5 = \frac{29}{5} + 2 \times   - \frac{2}{5} - 5 = 0
$$

$$
z\text{ -cofficient of }R = {y}_{2} - \left( {-M}\right)  =  - \frac{2}{5} - \left( {-M}\right) \; =  - \frac{2}{5} + M
$$

Similar computations can be used to determine the $z$ -coefficients of ${x}_{2},{x}_{3}$ , and ${x}_{4}$ (verify!).

Remarks. The simplex tableau format in Chapter 3 which generates the current tableau from the immediately preceding one is a sure recipe for propagating the roundoff error, greatly distorting the quality of the optimum solution. Fortunately there is a way out! You will notice from the discussion in Sections 4.2.2 and 4.2.3 that the inverse matrix of an iteration plays the key role in determining all the elements of the associated simplex tableau (by using this inverse and the original data of the problem). Indeed, the inverse itself can be determined from the original data once the basic solution is known, as demonstrated in the remarks following Example 4.2-1. This essentially means that at any iteration, all the elements of a tableau (inverse matrix included) can be determined from the original data of the model. This is a powerful result that has been used to keep computational round-off error in check. And this is precisely the overriding reason for the development of the revised simplex method presented in Chapter 7. ^RoundoffRemark

### 4.3 ECONOMIC INTERPRETATION OF DUALITY ^EconomicInterpretation

The LP problem can be viewed as a resource allocation model that seeks to maximize revenue under limited resources. Looking at the problem from this standpoint, the associated dual problem offers interesting economic interpretations. ^ResourceAllocationView

To formalize the discussion, consider the following representation of the general primal and dual problems:

| Primal | Dual |
| --- | --- |
| Maximize $z = \sum_{j=1}^{n} {c}_{j}{x}_{j}$<br>subject to<br>$\sum_{j=1}^{n} {a}_{ij}{x}_{j} \le {b}_{i},\ i=1,2,\ldots,m$<br>${x}_{j} \ge 0,\ j=1,2,\ldots,n$ | Minimize $w = \sum_{i=1}^{m} {b}_{i}{y}_{i}$<br>subject to<br>$\sum_{i=1}^{m} {a}_{ij}{y}_{i} \ge {c}_{j},\ j=1,2,\ldots,n$<br>${y}_{i} \ge 0,\ i=1,2,\ldots,m$ |

Viewed as a resource allocation model, the primal problem has $n$ economic activities and $m$ resources. The coefficient ${c}_{j}$ in the primal represents the revenue per unit of activity $j$ and resource $i$ with availability ${b}_{i}$ is consumed at the rate ${a}_{ij}$ units per unit of activity $j$ .

#### 4.3.1 Economic Interpretation of Dual Variables ^ShadowPrices

Section 4.2.3 states that for any two primal and dual feasible solutions, the values of the objective functions, when finite, must satisfy the following inequality:

$$
z = \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j} \leq  \mathop{\sum }\limits_{{i = 1}}^{m}{b}_{i}{y}_{i} = w
$$

At the optimum, the two objective values are equal-that is, $z = w$ .

In terms of the resource allocation model, $z$ represents $\$$ revenue, and ${b}_{i}$ represents available units of resource $i$ . Thus, dimensionally, $z = w$ implies

$$
\text{ \$revenue } = \mathop{\sum }\limits_{{i = 1}}^{m}{b}_{i}{y}_{i} = \mathop{\sum }\limits_{{i = 1}}^{m}\left( {\text{ units of resource }i}\right)  \times  \left( {\$ \text{ per unit of resource }i}\right)
$$

This means that the dual variable, ${y}_{i}$ , represents the worth per unit of resource $i$ (cf. the graphical definition of unit worth of a resource in Section 3.6.1)

As stated in Section 3.6.1, the standard name dual (or shadow) price of resource $i$ replaces the suggestive name worth per unit used in all LP literature and software packages, and hence the standard name is adopted in this book as well.

Using the same dimensional analysis, we can interpret the inequality $z < w$ (for any two feasible primal and dual solution) as

$$
\text{ (Revenue) } < \text{ (Worth of resources) }
$$

This relationship says that so long as the total revenue from all the activities is less than the worth of the resources, the corresponding primal and dual solutions are not optimal. Optimality is reached only when the resources have been exploited completely. This can happen only when the input (worth of the resources) equals the output (revenue dollars).

Example 4.3-1 ^ReddyMikksExample

The Reddy Mikks model (Example 2.1-1) and its dual are given as follows:

| Reddy Mikks primal | Reddy Mikks dual |
| --- | --- |
| Maximize $z = 5{x}_{1} + 4{x}_{2}$<br>subject to<br>$6{x}_{1} + 4{x}_{2} \le 24$ (resource 1, ${M1}$)<br>${x}_{1} + 2{x}_{2} \le 6$ (resource 2, ${M2}$)<br>$- {x}_{1} + {x}_{2} \le 1$ (resource 3, market)<br>${x}_{2} \le 2$ (resource 4, demand)<br>${x}_{1},{x}_{2} \ge 0$<br>Optimum solution: ${x}_{1}=3,{x}_{2}=1.5,\ z=21$ | Minimize $w = 24{y}_{1} + 6{y}_{2} + {y}_{3} + 2{y}_{4}$<br>subject to<br>$6{y}_{1} + {y}_{2} - {y}_{3} \ge 5$<br>$4{y}_{1} + 2{y}_{2} + {y}_{3} + {y}_{4} \ge 4$<br>${y}_{1},{y}_{2},{y}_{3},{y}_{4} \ge 0$<br>Optimum solution: ${y}_{1}=0.75,{y}_{2}=0.5,{y}_{3}={y}_{4}=0,\ w=21$ |

The Reddy Mikks model deals with the production of two types of paint (interior and exterior) using two raw materials ${M1}$ and ${M2}$ (resources 1 and 2) and subject to market and demand limits represented by the third and fourth constraints. The model determines the amounts (in tons/day) of exterior and interior paints that maximize the daily revenue (expressed in thousands of dollars).

The optimal dual solution shows that the dual price (worth per unit) of raw material ${M1}$ (resource 1) is ${y}_{1} = {.75}$ (or $\$ {750}$ per ton) and that of raw material ${M2}$ (resource 2) is ${y}_{2} = {.5}$ (or \$500 per ton). These results hold true for specific feasibility ranges as was shown in Section 3.6. For resources 3 and 4, representing the market and demand limits, the dual prices are both zero, which indicates that their associated resources are abundant (i.e., they are not critical in determining the optimum and, hence, their worth per unit, or dual price, is zero).

#### 4.3.2 Economic Interpretation of Dual Constraints ^ImputedCost

The economic meaning of the dual constraints can be achieved by using Formula 2 in Section 4.2.4, which states that at any primal iteration,

$$
\text{ Objective coefficient of }{x}_{j} = \left( \begin{matrix} \text{ Left -hand side of } \\  \text{ dual constraint }j \end{matrix}\right)  - \left( \begin{matrix} \text{ Right-hand side of } \\  \text{ dual constraint }j \end{matrix}\right)
$$

$$
= \mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i} - {c}_{j}
$$

We use dimensional analysis once again to interpret this equation. The revenue per unit, ${c}_{j}$ , of activity $j$ is in dollars per unit. Hence, for consistency, the quantity $\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i}$ must also be in dollars per unit. Next, because ${c}_{j}$ represents revenue, the quantity $\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i}$ , with opposite sign, must represent cost. Thus we have

$$
\$ \operatorname{cost} = \mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i} = \mathop{\sum }\limits_{{i = 1}}^{m}\left( \begin{array}{l} \text{ Usage of resource }i \\  \text{ per unit of activity }j \end{array}\right)  \times  \left( \begin{array}{l} \text{ Cost per unit } \\  \text{ of resource }i \end{array}\right)
$$

The conclusion is that the dual variable ${y}_{i}$ represents what is known in the LP literature as the imputed cost per unit of resource $i$ , and we can think of the quantity $\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i}$ as the imputed cost of all the resources needed to produce one unit of activity $j$ . As stated in Section 3.6, the quantity $\mathop{\sum }\limits_{{i = 1}}^{m}{a}_{ij}{y}_{i} - {c}_{j}\left( \right.  =$ imputed cost of activity $\left. {j - {c}_{j}}\right)$ is known by the standard name reduced cost of activity $j$ .The maximization optimality condition of the simplex method says that an increase in the level of an unused (nonbasic) activity $j$ can improve revenue only if its reduced cost is negative. In terms of the preceding interpretation, this condition states that

$$
\left( \begin{matrix} \text{ Imputed cost of } \\  \text{ resources used by } \\  \text{ one unit of activity }j \end{matrix}\right)  < \left( \begin{matrix} \text{ Revenue per unit } \\  \text{ of activity }j \end{matrix}\right)
$$

Thus, the maximization optimality condition says that it is economically advantageous to increase the level of an activity if its unit revenue exceeds its unit imputed cost.

## Example 4.3-2 ^ToycoExample

TOYCO assembles three types of toys-trains, trucks, and cars-using three operations. Available assembly times for the three operations are 430, 460, and 420 minutes per day, respectively, and the revenues per toy train, truck, and car are \$3, \$2, and \$5, respectively. The assembly times per train for the three operations are 1, 3, and 1 minutes, respectively. The corresponding times per truck and per car are $\left( {2,0,4}\right)$ and $\left( {1,2,0}\right)$ minutes (a zero time indicates that the operation is not used).

Letting ${x}_{1},{x}_{2}$ , and ${x}_{3}$ represent the daily number of units assembled of trains, trucks, and cars, the associated LP model and its dual are given as follows:

| TOYCO primal | TOYCO dual |
| --- | --- |
| Maximize $z = 3{x}_{1} + 2{x}_{2} + 5{x}_{3}$<br>subject to<br>${x}_{1} + 2{x}_{2} + {x}_{3} \le 430$ (Operation 1)<br>$3{x}_{1} + 2{x}_{3} \le 460$ (Operation 2)<br>${x}_{1} + 4{x}_{2} \le 420$ (Operation 3)<br>${x}_{1},{x}_{2},{x}_{3} \ge 0$<br>Optimal solution: ${x}_{1}=0,{x}_{2}=100,{x}_{3}=230,\ z=\$1350$ | Minimize $w = 430{y}_{1} + 460{y}_{2} + 420{y}_{3}$<br>subject to<br>${y}_{1} + 3{y}_{2} + {y}_{3} \ge 3$<br>$2{y}_{1} + 4{y}_{3} \ge 2$<br>${y}_{1} + 2{y}_{2} \ge 5$<br>${y}_{1},{y}_{2},{y}_{3} \ge 0$<br>Optimal solution: ${y}_{1}=1,{y}_{2}=2,{y}_{3}=0,\ w=\$1350$ |

The optimal primal solution calls for producing no toy trains, 100 toy trucks, and 230 toy cars.

Suppose that TOYCO is interested in producing toy trains $\left( {x}_{1}\right)$ as well. How can this be achieved? Looking at the reduced cost for ${x}_{1}$ , toy trains becomes attractive economically only if its unit imputed cost is strictly less than its unit revenue. TOYCO can achieve this by increasing the unit price. It can also decrease the imputed cost of the consumed resources $\left( { = {y}_{1} + 3{y}_{2} + {y}_{3}}\right)$ .

A decrease in the unit imputed cost entails reducing the assembly times used by a unit toy train on the three operations. Let ${r}_{1},{r}_{2}$ , and ${r}_{3}$ represent the reduction ratios on operations 1,2, and 3, respectively. The goal is to determine the values of ${r}_{1},{r}_{2}$ , and ${r}_{3}$ such that the new imputed cost per toy train is less than its unit revenue - that is,

$$
1\left( {1 - {r}_{1}}\right) {y}_{1} + 3\left( {1 - {r}_{2}}\right) {y}_{2} + 1\left( {1 - {r}_{3}}\right) {y}_{3} < 3
$$

$$
0 \leq  {r}_{1} \leq  1,0 \leq  {r}_{2} \leq  1,0 \leq  {r}_{3} \leq  1
$$

For the optimal dual values, ${y}_{1} = 1,{y}_{2} = 2$ , and ${y}_{3} = 0$ , this inequality reduces to

$$
{r}_{1} + 6{r}_{2} > 4,0 \leq  {r}_{1} \leq  1,0 \leq  {r}_{2} \leq  1
$$

Any values of ${r}_{1}$ and ${r}_{2}$ that satisfy these conditions will make toy trains profitable. Note, however, that this goal may not be attainable because it requires impractically large reductions in the times of operations 1 and 2. For example, even a 50% reduction (i.e., ${r}_{1} = {r}_{2} = {.5}$ ) fails to satisfy the given condition. The logical conclusion then is that TOYCO should not produce toy trains unless the time reductions are accompanied with increase in unit revenue.

### 4.4 ADDITIONAL SIMPLEX ALGORITHMS ^AdditionalAlgorithms

Chapter 3 presents the (primal) simplex algorithm that starts feasible and continues to be feasible until the optimum is reached. This section presents two additional algorithms: The dual simplex starts infeasible (but better than optimal) and remains infeasible until feasibility is restored, and the (author's) generalized simplex combines the primal and dual simplex methods, starting both nonoptimal and infeasible. All three algorithms are used with post-optimal analysis in Section 4.5.

#### 4.4.1 Dual Simplex Algorithm ^DualSimplex

The dual simplex method starts with a better than optimal and infeasible basic solution. The optimality and feasibility conditions are designed to preserve the optimality of the basic solutions as the solution move toward feasibility.

Dual feasibility condition. The leaving variable, ${x}_{r}$ , is the basic variable having the most negative value (ties are broken arbitrarily). If all the basic variables are nonnegative, the algorithm ends. ${}^{1}$ ^DualFeasibilityRule

Dual optimality condition. Given that ${x}_{r}$ is the leaving variable, let ${\bar{c}}_{j}$ be the reduced cost of nonbasic variable ${x}_{j}$ and ${\alpha }_{rj}$ the constraint coefficient in the ${x}_{r}$ -row and ${x}_{j}$ -column of the tableau. The entering variable is the nonbasic variable with ${\alpha }_{rj} < 0$ that corresponds to ^DualOptimalityRule

$$
\mathop{\min }\limits_{{\text{ Nonbasic }{x}_{j}}}\left\{  {\left| \frac{{\bar{c}}_{j}}{{\alpha }_{rj}}\right| ,{\alpha }_{rj} < 0}\right\}
$$

(Ties are broken arbitrarily.) If ${\alpha }_{rj} \geq  0$ for all nonbasic ${x}_{j}$ , the problem has no feasible solution.

To start the LP optimal and infeasible, two requirements must be met: ^DualSimplexStartRequirements

1. The objective function must satisfy the optimality condition of the regular simplex method (Chapter 3).

2. All the constraints must be of the type $\left(  \leq  \right)$ .

Inequalities of the type $\left(  \geq  \right)$ are converted to $\left(  \leq  \right)$ by multiplying both sides of the inequality by -1 . If the LP includes $\left(  = \right)$ constraints, the equation can be replaced by two inequalities. For example, ${x}_{1} + {x}_{2} = 1$ is equivalent to ${x}_{1} + {x}_{2} \leq  1,{x}_{1} + {x}_{2} \geq  1$ or ${x}_{1} + {x}_{2} \leq  1, - {x}_{1} - {x}_{2} \leq   - 1$ . The starting solution is infeasible if at least one of the right-hand sides of the inequalities is negative.

---

${}^{1}$ As explained in Section 3.7, a different feasibility condition, called the steepest edge, has so improved the computational efficiency of the dual simplex algorithm that it is now the dominant (simplex-based) algorithm for solving LPs in all commercial codes.

---

Example 4.4-1 ^DualSimplexExample

$$
\text{ Minimize }z = 3{x}_{1} + 2{x}_{2} + {x}_{3}
$$

subject to

$$
3{x}_{1} + {x}_{2} + {x}_{3} \geq  3
$$

$$
- 3{x}_{1} + 3{x}_{2} + {x}_{3} \geq  6
$$

$$
{x}_{1} + {x}_{2} + {x}_{3} \leq  3
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

In the present example, the first two inequalities are multiplied by -1 to convert them to $\left(  \leq  \right)$ constraints. The starting tableau is thus given as follows:

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | -3 | -2 | -1 | 0 | 0 | 0 | 0 |
| ${x}_{4}$ | -3 | -1 | -1 | 1 | 0 | 0 | -3 |
| ${x}_{5}$ | 3 | -3 | -1 | 0 | 1 | 0 | -6 |
| ${x}_{6}$ | 1 | 1 | 1 | 0 | 0 | 1 | 3 |

The tableau is optimal because all the reduced costs in the $z$ -row are $\leq  0\left( {{\bar{c}}_{1} =  - 3,{\bar{c}}_{2} =  - 2}\right.$ , $\left. {\bar{c} =  - 1,{\bar{c}}_{4} = 0,{\bar{c}}_{5} = 0,{\bar{c}}_{6} = 0}\right)$ . It is also infeasible because at least one of the basic variables is negative $\left( {{x}_{4} =  - 3,{x}_{5} =  - 6,{x}_{6} = 3}\right)$ .

According to the dual feasibility condition, ${x}_{5}\left( { =  - 6}\right)$ is the leaving variable. The next table shows how the dual optimality condition is used to determine the entering variable.

|  | $j = 1$ | $j = 2$ | $j = 3$ |
| --- | --- | --- | --- |
| Nonbasic variable | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ |
| $z$-row $\left( {\bar{c}}_{j}\right)$ | -3 | -2 | -1 |
| ${x}_{5}$-row, ${\alpha }_{5j}$ | 3 | -3 | -1 |
| Ratio $\left|\frac{{\bar{c}}_{j}}{{\alpha }_{5j}}\right|$ (only if ${\alpha }_{5j}<0$) | — | 2 | 1 |

The ratios show that ${x}_{2}$ is the entering variable.

The next tableau is obtained by using the familiar row operations, which give

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | -5 | 0 | $-\frac{1}{3}$ | 0 | $-\frac{2}{3}$ | 0 | 4 |
| ${x}_{4}$ | -4 | 0 | $-\frac{2}{3}$ | 1 | $-\frac{1}{3}$ | 0 | -1 |
| ${x}_{2}$ | -1 | 1 | $\frac{1}{3}$ | 0 | $-\frac{1}{3}$ | 0 | 2 |
| ${x}_{6}$ | 2 | 0 | $\frac{2}{3}$ | 0 | $\frac{1}{3}$ | 1 | 1 |
| Ratio | $\frac{5}{4}$ | — | $\frac{1}{2}$ | — | 2 | — |  |

The preceding tableau shows that ${x}_{4}$ leaves and ${x}_{3}$ enters, thus yielding the following tableau, which is both optimal and feasible:

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | -3 | 0 | 0 | $-\frac{1}{2}$ | $-\frac{1}{2}$ | 0 | $\frac{9}{2}$ |
| ${x}_{3}$ | 6 | 0 | 1 | $-\frac{3}{2}$ | $\frac{1}{2}$ | 0 | $\frac{3}{2}$ |
| ${x}_{2}$ | -3 | 1 | 0 | $\frac{1}{2}$ | $-\frac{1}{2}$ | 0 | $\frac{3}{2}$ |
| ${x}_{6}$ | -2 | 0 | 0 | 1 | 0 | 1 | 0 |

Notice how the dual simplex works. In all the iterations, optimality is maintained (all reduced costs are $\leq  0$ ) as each new iteration moves the solution toward feasibility. At iteration 3, feasibility is restored for the first time, and the process ends with the optimal feasible solution given as ${x}_{1} = 0,{x}_{2} = \frac{3}{2},{x}_{2} = \frac{3}{2}$ , and $z = \frac{9}{2}$ .

## TORA Moment

TORA provides a tutorial module for the dual simplex method. From the SOLVE/MODIFY menu select Solve $\Rightarrow$ Algebraic $\Rightarrow$ Iterations $\Rightarrow$ Dual Simplex. Remember that you need to convert $\left(  = \right)$ constraints to inequalities. You do not need to convert $\left(  \geq  \right)$ constraints because TORA will do the conversion internally.

#### 4.4.2 Generalized Simplex Algorithm ^GeneralizedSimplex

The (primal) simplex algorithm in Chapter 3 starts feasible but nonoptimal. The dual simplex (Section 4.4.1) starts better than optimal and infeasible. What if an LP model starts both nonoptimal and infeasible? Of course we can use artificial variables and artificial constraints to secure a starting solution. But this really is not necessary because the key idea of both the primal and dual simplex methods is that the optimum feasible solution, when finite, always occurs at a corner point (or a basic solution). This suggests that a new simplex algorithm (developed by this author) can be developed based on tandem use of the dual simplex and the primal simplex methods. First, use the dual algorithm to get rid of infeasibility (without worrying about optimality). Once feasibility is restored, the primal simplex can be used to find the optimum. Alternatively, we can first apply the primal simplex to secure optimality (without worrying about feasibility) and then use the dual simplex to seek feasibility. ^GeneralizedIdea

Example 4.4-2 ^GeneralizedExample

---

Consider the maximization LP model of Problem 4-38(a), repeated here for convenience.

$$
\text{ Maximize }z = 2{x}_{3}
$$

subject to

$$
- {x}_{1} + 2{x}_{2} - 2{x}_{3} \geq  8
$$

$$
- {x}_{1} + {x}_{2} + {x}_{3} \leq  4
$$

$$
2{x}_{1} - {x}_{2} + 4{x}_{3} \leq  {10}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

---

The following tableau format of the problem shows that the starting basic solution $\left( {{x}_{4},{x}_{5},{x}_{6}}\right)$ is both nonoptimal (because of nonbasic ${x}_{3}$ ) and infeasible (because of basic ${x}_{4}$ ).

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | -2 | 0 | 0 | 0 | 0 |
| ${x}_{4}$ | 1 | -2 | 2 | 1 | 0 | 0 | -8 |
| ${x}_{5}$ | -1 | 1 | 1 | 0 | 1 | 0 | 4 |
| ${x}_{6}$ | 2 | -1 | 4 | 0 | 0 | 1 | 10 |

We can solve the problem without the use of any artificial variables or artificial constraints, first securing feasibility using the dual simplex and then seeking optimality using the primal simplex. The dual simplex selects ${x}_{4}$ as the leaving variable. The entering variable can be any nonbasic variable with a negative constraint coefficient in the ${x}_{4}$ -row (recall that if no negative constraint coefficient exists, the problem has no feasible solution). In the present example, ${x}_{2}$ has a negative coefficient in the ${x}_{4}$ -row and is selected as the entering variable. The next tableau is thus computed as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | -2 | 0 | 0 | 0 | 0 |
| ${x}_{2}$ | $-\frac{1}{2}$ | 1 | -1 | $-\frac{1}{2}$ | 0 | 0 | 4 |
| ${x}_{5}$ | $-\frac{1}{2}$ | 0 | 2 | $\frac{1}{2}$ | 1 | 0 | 0 |
| ${x}_{6}$ | $\frac{3}{2}$ | 0 | 3 | $-\frac{1}{2}$ | 0 | 1 | 14 |

The new solution is now feasible but nonoptimal, and we can use the primal simplex to determine the optimal solution. In general, had we not restored feasibility in the preceding tableau, we would repeat the procedure as necessary until feasibility is satisfied or until there is evidence that the problem has no feasible solution.

Remarks. The essence of the generalized simplex method in Example 4.4-2 is that the simplex algorithm is not rigid. The literature abounds with variations of the simplex method (e.g., the primal-dual method, the criss-cross method, and the multiplex method) that give the impression that each procedure is fundamentally different, when, in fact, they all seek corner-point (basic) solutions, with a slant toward automated computations and, perhaps, computational efficiency.

### 4.5 POST-OPTIMAL ANALYSIS ^PostOptimalAnalysis

In Section 3.6, we dealt with the sensitivity of the optimum solution by determining the ranges for the different LP parameters that would keep the optimum basic variables unchanged. In this section, we deal with making changes in the parameters of the model and finding the new optimum solution. Take, for example, a case in the poultry industry, where an LP model is commonly used to determine the optimal feed mix per broiler (see Example 2.2-2). The weekly consumption per broiler varies from .26 lb (120 g) for a 1-week-old bird to 2.1 lb (950 g) for an 8-week-old bird. Additionally, the cost of the ingredients in the mix may change periodically. These changes require periodic re-calculation of the optimum solution. Post-optimal analysis determines the new solution in an efficient way. The new computations are rooted in the use duality and the primal-dual relationships given in Section 4.2. ^PostOptimalMotivation

The following table lists the cases that can arise in post-optimal analysis and the actions needed to obtain the new solution (assuming one exists): ^PostOptimalCasesTable

| Condition after parameters change | Recommended action |
| --- | --- |
| Current solution remains optimal and feasible. | No further action is necessary. |
| Current solution becomes infeasible. | Use dual simplex to recover feasibility. |
| Current solution becomes nonoptimal. | Use primal simplex to recover optimality. |
| Current solution becomes both nonoptimal and infeasible. | Use the generalized simplex method to recover optimality and feasibility. |

The first three cases are investigated in this section. The fourth case, being a combination of cases 2 and 3, is treated in Problem 4-47.

The TOYCO model of Example 4.3-2 will be used to explain the different procedures. Recall that the problem deals with the assembly of three types of toys: trains, trucks, and cars. Three operations are involved in the assembly. The model and its dual are repeated here for convenience.

| TOYCO primal | TOYCO dual |
| --- | --- |
| Maximize $z = 3{x}_{1} + 2{x}_{2} + 5{x}_{3}$<br>subject to<br>${x}_{1} + 2{x}_{2} + {x}_{3} \le 430$ (Operation 1)<br>$3{x}_{1} + 2{x}_{3} \le 460$ (Operation 2)<br>${x}_{1} + 4{x}_{2} \le 420$ (Operation 3)<br>${x}_{1},{x}_{2},{x}_{3} \ge 0$<br>Optimal solution: ${x}_{1}=0,{x}_{2}=100,{x}_{3}=230,\ z=\$1350$ | Minimize $z = 430{y}_{1} + 460{y}_{2} + 420{y}_{3}$<br>subject to<br>${y}_{1} + 3{y}_{2} + {y}_{3} \ge 3$<br>$2{y}_{1} + 4{y}_{3} \ge 2$<br>${y}_{1} + 2{y}_{2} \ge 5$<br>${y}_{1},{y}_{2},{y}_{3} \ge 0$<br>Optimal solution: ${y}_{1}=1,{y}_{2}=2,{y}_{3}=0,\ w=\$1350$ |

The associated optimum tableau for the primal is given as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $Z$ | 4 | 0 | 0 | 1 | 2 | 0 | 1,350 |
| ${X}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | $\frac{1}{2}$ | $-\frac{1}{4}$ | 0 | 100 |
| ${X}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | 1 | 0 | 230 |
| ${X}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | 20 |

#### 4.5.1 Changes Affecting Feasibility ^FeasibilityChanges

The feasibility of the current optimum solution is affected only if the right-hand side of the constraints is changed, or a new constraint is added to the model. In both cases, infeasibility occurs when one or more of the current basic variables become negative.

Changes in the right-hand side. This change requires recomputing the right-hand side of the tableau using Formula 1 in Section 4.2.4: ^RhsChange

$$
\left( \begin{matrix} \text{ New right-hand side of } \\  \text{ tableau in iteration }i \end{matrix}\right)  = \left( \begin{matrix} \text{ Inverse in } \\  \text{ iteration }i \end{matrix}\right)  \times  \left( \begin{matrix} \text{ New right-hand } \\  \text{ side of constraints } \end{matrix}\right)
$$

Recall that the right-hand side of the tableau gives the values of the basic variables.

Example 4.5-1

Situation 1. Suppose that TOYCO is increasing the daily capacity of operations 1, 2, and 3 to 600,640, and 590 minutes, respectively. How would this change affect the total revenue?

With these increases, the only change that will take place in the optimum tableau is the righthand side of the constraints (and the optimum objective value). Thus, the new basic solution is computed as follows:

$$
\left( \begin{array}{l} {x}_{2} \\  {x}_{3} \\  {x}_{6} \end{array}\right)  = \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right) \left( \begin{array}{l} {600} \\  {640} \\  {590} \end{array}\right)  = \left( \begin{matrix} {140} \\  {320} \\  {30} \end{matrix}\right)
$$

Thus, the current basic variables, ${x}_{2},{x}_{3}$ , and ${x}_{6}$ , remain feasible at the new values 140,320, and 30 units, respectively. The associated optimum revenue is \$1880.

Situation 2. Although the new solution is appealing from the standpoint of increased revenue, TOYCO recognizes that its implementation may take time. Another proposal shifts the slack capacity of operation $3\left( {{x}_{6} = {20}}\right.$ minutes $)$ to the capacity of operation 1 . How would this change impact the optimum solution?

The capacity mix of the three operations changes to 450, 460, and 400 minutes, respectively. The resulting solution is

$$
\left( \begin{array}{l} {x}_{2} \\  {x}_{3} \\  {x}_{6} \end{array}\right)  = \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right) \left( \begin{array}{l} {450} \\  {460} \\  {400} \end{array}\right)  = \left( \begin{array}{l} {110} \\  {230} \\   - {40} \end{array}\right)
$$

The resulting solution is infeasible because ${x}_{6} =  - {40}$ , which requires applying the dual simplex method to recover feasibility. First, we modify the right-hand side of the tableau as shown by the shaded column. Notice that the associated value of $z = 3 \times  0 + 2 \times  {110} + 5 \times  {230} = \$ {1370}$ .

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 4 | 0 | 0 | 1 | 2 | 0 | 1370 |
| ${x}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | $\frac{1}{2}$ | $-\frac{1}{4}$ | 0 | 110 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | $\frac{1}{2}$ | 0 | 230 |
| ${x}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | -40 |

Using the dual simplex, ${x}_{6}$ leaves and ${x}_{4}$ enters, which yields the following optimal feasible tableau (in general, the dual simplex may take more than one iteration to recover feasibility).

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 5 | 0 | 0 | 0 | $\frac{5}{2}$ | $\frac{1}{2}$ | 1350 |
| ${x}_{2}$ | $\frac{1}{4}$ | 1 | 0 | 0 | 0 | $\frac{1}{4}$ | 100 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | $\frac{1}{2}$ | 0 | 230 |
| ${x}_{4}$ | -1 | 0 | 0 | 1 | $-\frac{1}{2}$ | $-\frac{1}{2}$ | 20 |

The optimum solution (in terms of ${x}_{1},{x}_{2}$ , and ${x}_{3}$ ) remains the same as in the original model. This means that the proposed shift in capacity allocation is not advantageous because it simply shifts the surplus capacity from operation 3 to a surplus capacity in operation 1. The conclusion then is that operation 2 is the bottleneck, and it may be advantageous to shift the surplus to operation 2 instead (see Problem 4-42).

Addition of a new constraint. The addition of a new constraint can never improve the current optimum objective value. If the new constraint is redundant, it will have no effect on the current solution. Otherwise, the current solution does not satisfy the new constraint, and a new solution is determined by the dual simplex method. ^NewConstraint

Example 4.5-2

Situation 1. Suppose that TOYCO is changing the design of its toys and that the change will require the addition of a fourth assembly operation. The daily capacity of the new operation is 500 minutes and the times per unit for the three products on this operation are 3,1, and 1 minutes, respectively.

The new constraint for operation 4 is

$$
3{x}_{1} + {x}_{2} + {x}_{3} \leq  {500}
$$

This constraint is redundant because it is satisfied by the current optimum solution ${x}_{1} = 0$ , ${x}_{2} = {100}$ , and ${x}_{3} = {230}$ . Hence, the current optimum solution remains unchanged.

Situation 2. Suppose, instead, that TOYCO unit times on the fourth operation are changed to 3, 3, and 1 minutes, respectively. All the remaining data of the model remain the same.

The new constraint for operation 4 is

$$
3{x}_{1} + 3{x}_{2} + {x}_{3} \leq  {500}
$$

This constraint is not satisfied by the current optimum solution; namely, for ${x}_{1} = 0,{x}_{2} = {100}$ , and ${x}_{3} = {230}$ ,

$$
{x}_{7} = {500} - \left( {3 \times  0 + 3 \times  {100} + 1 \times  {230}}\right)  =  - {30}
$$

This means that the new constraint is not redundant. Off hand, this is not good news because it indicates that the additional constraint will worsen the optimum objective value (remember the intuitive argument that additional constraints can never improve the optimum objective value). Nonetheless, to obtain the new solution without having to solve the problem completely anew, the constraint is added to the current optimum tableau as follows ( ${x}_{7}$ is a slack variable):

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | ${x}_{7}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 4 | 0 | 0 | 1 | 2 | 0 | 0 | 1350 |
| ${x}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | $\frac{1}{2}$ | $-\frac{1}{4}$ | 0 | 0 | 100 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | $\frac{1}{2}$ | 0 | 0 | 230 |
| ${x}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | 0 | 20 |
| ${x}_{7}$ | 3 | 3 | 1 | 0 | 0 | 0 | 1 | 500 |

This means that that ${x}_{7} = {500}$ is not consistent with the values of ${x}_{1},{x}_{2}$ and ${x}_{3}$ in the rest of the tableau. To effect consistency, the ${x}_{7}$ -row must be "conditioned" by performing the following row operations:

$$
\text{ New }{x}_{7}\text{ -row } = \text{ Old }{x}_{7}\text{ -row } - \left\lbrack  {\mathbf{3} \times  \left( {{x}_{2}\text{ -row }}\right)  + \mathbf{1} \times  \left( {{x}_{3}\text{ -row }}\right) }\right\rbrack
$$

These operations are the same as the ones used in the $M$ -method (Section 3.4.1) to zero out the coefficients of the artificial variables in the objective function and are exactly equivalent to using the substitutions

$$
{x}_{2} = {100} - \left( {-\frac{1}{4}{x}_{1} + \frac{1}{2}{x}_{4} - \frac{1}{4}{x}_{5}}\right)
$$

$$
{x}_{3} = {230} - \left( {\frac{3}{2}{x}_{1} + \frac{1}{2}{x}_{5}}\right)
$$

The new (consistent) tableau is thus given as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | ${x}_{7}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 4 | 0 | 0 | 1 | 2 | 0 | 0 | 1350 |
| ${x}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | $\frac{1}{2}$ | $-\frac{1}{4}$ | 0 | 0 | 100 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | $\frac{1}{2}$ | 0 | 0 | 230 |
| ${x}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | 0 | 20 |
| ${x}_{7}$ | 9 | 0 | 0 | $-\frac{3}{2}$ | $\frac{1}{4}$ | 0 | 1 | -30 |

Application of the dual simplex method will produce the new optimum solution ${x}_{1} = 0$ , ${x}_{2} = {90},{x}_{3} = {230}$ , and $z = \$ {1330}$ (verify!). The solution shows that the addition of the non-redundant constraint of operation 4 is not recommended because, as expected, it lowers the revenues from \$1350 to \$1330.

#### 4.5.2 Changes Affecting Optimality ^OptimalityChanges

This section considers making changes in the objective coefficients and the addition of a new economic activity (variable).

Changes in the objective function coefficients. These changes affect only the optimality of the solution and require recomputing the $z$ -row coefficients (reduced costs) according to the following procedure: ^ObjectiveCoeffChanges

1. Compute the dual values using Method 2, Section 4.2.3.

2. Substitute the new dual values in Formula 2, Section 4.2.4, to determine the new reduced costs ( $z$ -row coefficients).

If the new $z$ -row satisfies the optimality condition, the solution remains unchanged (the optimum objective value may change, however). If it is not, the primal simplex is used to recover optimality.

## Example 4.5-3

Situation 1. In the TOYCO model, suppose that the company is instituting a revised pricing policy to meet the competition. The new unit revenues are \$2, \$3, and \$4 for train, truck, and car toys, respectively.

The new objective function is

$$
\text{ Maximize }z = 2{x}_{1} + 3{x}_{2} + 4{x}_{3}
$$

Thus,

(New objective coefficients of basic ${x}_{2},{x}_{3}$ , and ${x}_{6}) = \left( {3,4,0}\right)$

Using Method 2, Section 4.2.3, the new dual variables are computed as

$$
\left( {{y}_{1},{y}_{2},{y}_{3}}\right)  = \left( {3,4,0}\right) \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right)  = \left( {\frac{3}{2},\frac{5}{4},0}\right)
$$

The $z$ -row coefficients are determined as the difference between the left- and right-hand sides of the dual constraints (Formula 2, Section 4.2.4). It is not necessary to recompute the objective-row coefficients of the basic variables $\left( {{x}_{2},{x}_{3}\text{ , and }{x}_{6}}\right)$ because they are always zero regardless of any changes made in the objective coefficients (verify!).

$$
\text{ (Reduced cost of }{x}_{1}\text{ ) } = {y}_{1} + 3{y}_{2} + {y}_{3} - \mathbf{2} = \frac{3}{2} + 3\left( \frac{5}{4}\right)  + 0 - \mathbf{2} = \frac{13}{4}
$$

$$
\text{ (Reduced cost of }{x}_{4}\text{ ) } = {y}_{1} - 0 = \frac{3}{2}
$$

$$
\text{ (Reduced cost of }{x}_{5}\text{ ) } = {y}_{2} - 0 = \frac{5}{4}
$$

Note that the right-hand side of the first dual constraint is 2 , the new coefficient in the modified objective function.

The computations show that the current solution, ${x}_{1} = 0$ train, ${x}_{2} = {100}$ trucks, and ${x}_{3} = {230}$ cars, remains optimal. The corresponding new revenue is computed as $2 \times  0 + 3 \times \; {100} + 4 \times  {230} = \$ {1220}$ . The new pricing policy is not recommended because it lowers revenue.

Situation 2. Suppose now that the TOYCO objective function is changed to

$$
\text{ Maximize }z = 6{x}_{1} + 3{x}_{2} + 4{x}_{3}
$$

Will the optimum solution change?

We have

$$
\left( {{y}_{1},{y}_{2},{y}_{3}}\right)  = \left( {3,4,0}\right) \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right)  = \left( {\frac{3}{2},\frac{5}{4},0}\right)
$$

(Reduced cost of ${x}_{1}$ ) $= {y}_{1} + 3{y}_{2} + {y}_{3} - \mathbf{6} = \frac{3}{2} + 3\left( \frac{5}{4}\right)  + 0 - \mathbf{6} =  - \frac{3}{4}$

(Reduced cost of ${x}_{4}$ ) $= {y}_{1} - 0 = \frac{3}{2}$

(Reduced cost of ${x}_{5}$ ) $= {y}_{2} - 0 = \frac{5}{4}$

The new reduced cost of ${x}_{1}$ shows that the current solution is not optimum.

To determine the new solution, the $z$ -row is changed as highlighted in the following tableau:

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | $-\frac{3}{4}$ | 0 | 0 | $\frac{3}{2}$ | $\frac{5}{4}$ | 0 | 1220 |
| ${x}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | 1 | $-\frac{1}{4}$ | 0 | 100 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | 0 | $\frac{1}{2}$ | 0 | 230 |
| ${x}_{6}$ | 2 | 0 | 0 | -2 | 1 | 1 | 20 |

The highlighted elements are the new reduced costs and the new objective value. All the remaining elements are the same as in the original optimal tableau. The new optimum solution is then determined by letting ${x}_{1}$ enter and ${x}_{6}$ leave, which yields the solution ${x}_{1} = {10},{x}_{2} = {102.5}$ , ${x}_{3} = {215}$ , and $z = \$ {1227.50}$ (verify!). Although the new solution recommends the production of all three toys, the optimum revenue is less than that when only two toys are manufactured.

Addition of a new activity. A new activity signifies adding a new variable to the model. Intuitively, the addition of a new activity is desirable only if it is profitable. This condition can be checked by using Formula 2, Section 4.2.4, to compute the reduced cost of the new variable. The new activity is not profitable if it satisfies the optimality condition. ^NewActivity

## Example 4.5-4 ^FireEngineExample

TOYCO recognizes that toy trains are not currently in production because they are not profitable. The company wants to replace toy trains with a new product, a toy fire engine, to be assembled on the existing facilities. TOYCO estimates the revenue per toy fire engine to be \$4 and the assembly times per unit to be 1 minute on each of operations 1 and 2, and 2 minutes on operation 3.

Let ${x}_{7}$ represent the new fire engine product. Given that $\left( {{y}_{1},{y}_{2},{y}_{3}}\right)  = \left( {1,2,0}\right)$ are the optimal dual values, we get

$$
\text{ (Reduced cost of }{x}_{7}\text{ ) } = 1{y}_{1} + 1{y}_{2} + 2{y}_{3} - 4 = 1 \times  1 + 1 \times  2 + 2 \times  0 - 4 =  - 1
$$

The result shows that it is profitable to include ${x}_{7}$ in the optimal basic solution. To obtain the new optimum, we first compute its column constraint using Formula 1, Section 4.2.4, as

$$
{x}_{7}\text{ -constraint colum } = \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right) \left( \begin{array}{l} 1 \\  1 \\  2 \end{array}\right)  = \left( \begin{array}{l} \frac{1}{4} \\  \frac{1}{2} \\  1 \end{array}\right)
$$

Thus, the current simplex tableau must be modified as follows ${}^{2}$

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{7}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 4 | 0 | 0 | -1 | 1 | 2 | 0 | 1350 |
| ${x}_{2}$ | $-\frac{1}{4}$ | 1 | 0 | $\frac{1}{4}$ | $\frac{1}{2}$ | $-\frac{1}{4}$ | 0 | 100 |
| ${x}_{3}$ | $\frac{3}{2}$ | 0 | 1 | $\frac{1}{2}$ | 0 | $\frac{1}{2}$ | 0 | 230 |
| ${x}_{6}$ | 2 | 0 | 0 | 1 | -2 | 1 | 1 | 20 |

---

${}^{2}$ As a side observation, variable ${x}_{1}$ can be eliminated from the tableau altogether, thus reducing the size of the tableau and hence the associated amount of computations.

---

The new optimum is determined by letting ${x}_{7}$ enter the basic solution, in which case ${x}_{6}$ must leave. The new solution is ${x}_{1} = 0,{x}_{2} = 0,{x}_{3} = {125},{x}_{7} = {210}$ , and $z = \$ {1465}$ (verify!), which improves the revenues by \$115.

Remarks. The heart of the post-optimal computations is the inverse matrix of the optimal tableau; meaning that for the mathematics to work correctly, post-optimal sensitivity analysis cannot include changes in the data of the original problem that affect the inverse matrix (recall from Sections 4.2.2 and 4.2.3 that the inverse is computed from the basic matrix composed of constraint columns of the original problem). So, even though the post-optimal analysis in this chapter is more encompassing than the presentation in Sections 3.6.2 and 3.6.3 in that it allows simultaneous changes in both the objective function and the constraints, it still has the shortcoming of not allowing changes in the constraint columns of basic variables. And herein lies a typical problem where mathematics is not sufficiently responsive to practical needs; meaning that, in a practical sense, we cannot use the technical excuse that the changes cannot be made "because the associated variable is basic"! Instead, the changes have to be tested in a different manner and, as stated in Chapter 3, a viable alternative in this case calls for solving the proposed LP scenario totally anew. ^PostOptimalLimitations

## BIBLIOGRAPHY ^Bibliography

Bazaraa, M., J. Jarvis, and H. Sherali, Linear Programming and Network Flows, 4th ed., Wiley, New York, 2009.

Bradley, S., A. Hax, and T. Magnanti, Applied Mathematical Programming, Addison-Wesley, Reading, MA, 1977.

Diwckar, U., Introduction to Applied Optimization, Kluwer Academic Publishers, Boston, 2003.

Nering, E., and A. Tucker, Linear Programming and Related Problems, Academic Press, Boston, 1992.

Vanderbei, R., Linear Programming: Foundation and Extensions, 3rd ed., Springer, New York, 2008.

## PROBLEMS ^ProblemsSection

| Section | Assigned Problems | Section | Assigned Problems |
| --- | --- | --- | --- |
| 4.1 | 4-1 to 4-6 | 4.3.2 | 4-31 to 4-34 |
| 4.2.1 | 4-7 to 4-7 | 4.4.1 | 4-35 to 4-39 |
| 4.2.2 | 4-8 to 4-9 | 4.4.2 | 4-40 to 4-41 |
| 4.2.3 | 4-10 to 4-18 | 4.5.1 | 4-42 to 4-49 |
| 4.2.4 | 4-19 to 4-27 | 4.5.2 | 4-50 to 4-56 |
| 4.3.1 | 4-28 to 4-30 |  |  |

4-1. In Example 4.1-1, derive the associated dual problem if the sense of optimization in the primal problem is changed to minimization.

*4-2. In Example 4.1-2, derive the associated dual problem given that the primal problem is augmented with a third constraint, $3{x}_{1} + {x}_{2} = 4$ .

4-3. In Example 4.1-3, show that even if the sense of optimization in the primal is changed to minimization, an unrestricted primal variable always corresponds to an equality dual constraint.

4-4. Write the dual for each of the following primal problems:

(a) Maximize $z = {66}{x}_{1} - {22}{x}_{2}$

subject to

$$
- {x}_{1} + {x}_{2} \leq   - 2
$$

$$
2{x}_{1} + 3{x}_{2} \leq  5
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(b) Minimize $z = 6{x}_{1} + 3{x}_{2}$ subject to

$$
6{x}_{1} - 3{x}_{2} + {x}_{3} \geq  {25}
$$

$$
3{x}_{1} + 4{x}_{2} + {x}_{3} \geq  {55}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

*(c) Maximize $z = {x}_{1} + {x}_{2}$ subject to

$$
2{x}_{1} + {x}_{2} = 5
$$

$$
3{x}_{1} - {x}_{2} = 6
$$

${x}_{1},{x}_{2}$ unrestricted

*4-5. Consider Example 4.1-1. The application of the simplex method to the primal requires the use of an artificial variable in the second constraint of the standard primal to secure a starting basic solution. Show that the presence of an artificial primal in equation form variable does not affect the definition of the dual because it leads to a redundant dual constraint.

4-6. True or False?

(a) The dual of the dual problem yields the original primal.

(b) If the primal constraint is originally in equation form, the corresponding dual variable is necessarily unrestricted.

(c) If the primal constraint is of the type $\leq$ , the corresponding dual variable will be nonnegative (nonpositive) if the primal objective is maximization (minimization).

(d) If the primal constraint is of the type $\geq$ , the corresponding dual variable will be nonnegative (nonpositive) if the primal objective is minimization (maximization).

(e) An unrestricted primal variable will result in an equality dual constraint.

4-7. Consider the following matrices:

$$
\mathbf{A} = \left( \begin{array}{ll} 1 & 4 \\  2 & 5 \\  3 & 6 \end{array}\right) ,{\mathbf{P}}_{1} = \left( \begin{array}{l} {10} \\  {20} \end{array}\right) ,{\mathbf{P}}_{2} = \left( \begin{array}{l} {10} \\  {20} \\  {30} \end{array}\right)
$$

$$
{\mathbf{V}}_{1} = \left( {{11},{22}}\right) ,{\mathbf{V}}_{2} = \left( {-2, - 4, - 6}\right)
$$

In each of the following cases, indicate whether the given matrix operation is legitimate, and, if so, calculate the result.

*(a) ${\mathbf{{AV}}}_{1}$

(b) ${\mathbf{{AP}}}_{1}$

(c) ${\mathbf{{AP}}}_{2}$

(d) ${\mathbf{V}}_{1}\mathbf{A}$

*(e) ${\mathbf{V}}_{2}\mathbf{A}$

(f) ${\mathbf{P}}_{1}{\mathbf{P}}_{2}$

(g) ${\mathbf{V}}_{1}{\mathbf{P}}_{1}$

4-8. Consider the optimal tableau of Example 3.3-1.

*(a) Identify the optimal inverse matrix.

(b) Show that the right-hand side equals the inverse multiplied by the original right-hand side vector of the original constraints.

4-9. Repeat Problem 4-8 for the last tableau of Example 3.4-2.

4-10. Find the optimal value of the objective function for the following problem by inspecting only its dual. (Do not solve the dual by the simplex method.)

$$
\text{ Minimize }z = {10}{x}_{1} + 4{x}_{2} + 5{x}_{3}
$$

subject to

$$
5{x}_{1} - 7{x}_{2} + 3{x}_{3} \geq  {20}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

4-11. Solve the dual of the following problem, and then find its optimal solution from the solution of the dual. Does the solution of the dual offer computational advantages over solving the primal directly?

$$
\text{ Minimize }z = {50}{x}_{1} + {60}{x}_{2} + {30}{x}_{3}
$$

subject to

$$
5{x}_{1} + 5{x}_{2} + 3{x}_{3} \geq  {50}
$$

$$
{x}_{1} + \;{x}_{2} - \;{x}_{3} \geq  {20}
$$

$$
7{x}_{1} + 6{x}_{2} - 9{x}_{3} \geq  {30}
$$

$$
5{x}_{1} + 5{x}_{2} + 5{x}_{3} \geq  {35}
$$

$$
2{x}_{1} + 4{x}_{2} - {15}{x}_{3} \geq  {10}
$$

$$
{12}{x}_{1} + {10}{x}_{2} \geq  {90}
$$

$$
{x}_{2} - {10}{x}_{3} \geq  {20}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

*4-12. Consider the following LP:

$$
\text{ Maximize }z = 5{x}_{1} + 2{x}_{2} + 3{x}_{3}
$$

subject to

$$
{x}_{1} + 5{x}_{2} + 2{x}_{3} = {15}
$$

$$
{x}_{1} - 5{x}_{2} - 6{x}_{3} \leq  {20}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

Given that the artificial variable ${x}_{4}$ and the slack variable ${x}_{5}$ form the starting basic variables and that $M$ was set equal to 100 when solving the problem, the optimal tableau is given as:

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 23 | 7 | 105 | 0 | 75 |
| ${x}_{1}$ | 1 | 5 | 2 | 1 | 0 | 15 |
| ${x}_{5}$ | 0 | -10 | -8 | -1 | 1 | 5 |

Write the associated dual problem, and determine its optimal solution in two ways.

4-13. Consider the following LP:

$$
\text{ Minimize }z = 4{x}_{1} + {x}_{2}
$$

subject to

$$
3{x}_{1} + {x}_{2} = {30}
$$

$$
4{x}_{1} + 3{x}_{2} \geq  {60}
$$

$$
{x}_{1} + 2{x}_{2} \leq  {40}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The starting solution consists of artificial ${x}_{4}$ and ${x}_{5}$ for the first and second constraints and slack ${x}_{6}$ for the third constraint. Using $M = {100}$ for the artificial variables, the optimal tableau is given as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | ${x}_{6}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | 0 | -98.6 | -100 | -0.2 | 34 |
| ${x}_{1}$ | 1 | 0 | 0 | 0.4 | 0 | -0.2 | 4 |
| ${x}_{2}$ | 0 | 1 | 0 | 0.2 | 0 | 0.6 | 18 |
| ${x}_{3}$ | 0 | 0 | 1 | 1 | -1 | 1 | 10 |

Write the associated dual problem, and determine its optimal solution in two ways.

4-14. Consider the following LP:

$$
\text{ Maximize }z = 2{x}_{1} + 4{x}_{2} + 4{x}_{3} - 3{x}_{4}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} = 4
$$

$$
{x}_{1} + 4{x}_{2}\; + {x}_{4} = 8
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

Using ${x}_{3}$ and ${x}_{4}$ as starting variables, the optimal tableau is given as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | Solution |
| --- | --- | --- | --- | --- | --- |
| $z$ | 2 | 0 | 0 | 3 | 16 |
| ${x}_{3}$ | 0.75 | 0 | 1 | -0.25 | 2 |
| ${x}_{2}$ | 0.25 | 1 | 0 | 0.25 | 2 |

Write the associated dual problem, and determine its optimal solution in two ways.

*4-15. Consider the following LP:

$$
\text{ Maximize }z = {x}_{1} + 5{x}_{2} + 3{x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} = 3
$$

$$
2{x}_{1} - {x}_{2}\; = 4
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

The starting solution consists of ${x}_{3}$ in the first constraint and an artificial ${x}_{4}$ in the second constraint with $M = {100}$ . The optimal tableau is given as

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | Solution |
| --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 2 | 0 | 99 | 5 |
| ${x}_{3}$ | 1 | 2.5 | 1 | -0.5 | 1 |
| ${x}_{1}$ | 0 | -0.5 | 0 | 0.5 | 2 |

Write the associated dual problem, and determine its optimal solution in two ways.

4-16. Consider the following set of inequalities:

$$
2{x}_{1} + 3{x}_{2} \leq  {12}
$$

$$
- 3{x}_{1} + 2{x}_{2} \leq   - 4
$$

$$
3{x}_{1} - 5{x}_{2} \leq  2
$$

$$
{x}_{1}\text{ unrestricted }
$$

$$
{x}_{2} \geq  0
$$

A feasible solution can be found by augmenting the trivial objective function, maximize $z = {x}_{1} + {x}_{2}$ , and then solving the problem. Another way is to solve the dual, from which a solution for the set of inequalities can be found. Apply the two methods.

4-17. Estimate a range for the optimal objective value for the following LPs:

*(a) Minimize $z = 5{x}_{1} + 2{x}_{2}$

subject to

$$
{x}_{1} - {x}_{2} \geq  3
$$

$$
2{x}_{1} + 3{x}_{2} \geq  5
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(b) Maximize $z = {x}_{1} + 5{x}_{2} + 3{x}_{3}$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} = {30}
$$

$$
2{x}_{1} - {x}_{2}\; = {40}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

(c) Maximize $z = 2{x}_{1} + {x}_{2}$

subject to

$$
{x}_{1} - {x}_{2} \leq  2
$$

$$
2{x}_{1} \leq  8
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(d) Maximize $z = 3{x}_{1} + 2{x}_{2}$

subject to

$$
2{x}_{1} + {x}_{2} \leq  3
$$

$$
3{x}_{1} + 4{x}_{2} \leq  {12}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

4-18. In Problem 4-17(a), let ${y}_{1}$ and ${y}_{2}$ be the dual variables. Determine whether the following pairs of primal-dual solutions are optimal:

*(a) $\left( {{x}_{1} = 3,{x}_{2} = 1;{y}_{1} = 4,{y}_{2} = 1}\right)$

(b) $\left( {{x}_{1} = 4,{x}_{2} = 1;{y}_{1} = 1,{y}_{2} = 0}\right)$

(c) $\left( {{x}_{1} = 3,{x}_{2} = 0;{y}_{1} = 5,{y}_{2} = 0}\right)$

4-19. Generate the first simplex iteration of Example 4.2-1 (you may use TORA's Iterations $\Rightarrow  M$ -method with $M = {100}$ for convenience), then use Formulas 1 and 2 to verify all the elements of the resulting tableau.

4-20. Consider the following LP model:

$$
\text{ Maximize }z = 4{x}_{1} + {14}{x}_{2}
$$

subject to

$$
2{x}_{1} + 7{x}_{2} + {x}_{3}\; = {21}
$$

$$
7{x}_{1} + 2{x}_{2}\; + {x}_{4} = {21}
$$

$$
{x}_{1,}{x}_{2,}{x}_{3,}{x}_{4} \geq  0
$$

Check the optimality and feasibility of each of the following basic solutions:

*(a) Basic variables $= \left( {{x}_{2},{x}_{4}}\right)$ , Inverse $= \left( \begin{array}{rr} \frac{1}{7} & 0 \\   - \frac{2}{7} & 1 \end{array}\right)$

(b) Basic variables $= \left( {{x}_{2},{x}_{3}}\right)$ , Inverse $= \left( \begin{array}{rr} 0 & \frac{1}{2} \\  1 &  - \frac{7}{2} \end{array}\right)$

(c) Basic variables $= \left( {{x}_{2},{x}_{1}}\right)$ , Inverse $= \left( \begin{array}{rr} \frac{7}{45} &  - \frac{2}{45} \\   - \frac{2}{45} & \frac{7}{45} \end{array}\right)$

(d) Basic variables $= \left( {{x}_{1},{x}_{4}}\right)$ , Inverse $= \left( \begin{matrix} \frac{1}{2} & 0 \\   - \frac{7}{2} & 1 \end{matrix}\right)$

4-21. Consider the following LP model:

$$
\text{ Maximize }z = 3{x}_{1} + 2{x}_{2} + 5{x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} + {x}_{4}\; = {30}
$$

$$
3{x}_{1}\; + 2{x}_{3}\; + {x}_{5}\; = {60}
$$

$$
{x}_{1} + 4{x}_{2}\; + {x}_{6} = {20}
$$

$$
{x}_{2},{x}_{2},{x}_{3},{x}_{4},{x}_{5},{x}_{6} \geq  0
$$

Check the optimality and feasibility of the following basic solutions:

(a) Basic variables $= \left( {{x}_{4},{x}_{3},{x}_{6}}\right)$ , Inverse $= \left( \begin{matrix} 1 &  - \frac{1}{2} & 0 \\  0 & \frac{1}{2} & 0 \\  0 & 0 & 1 \end{matrix}\right)$

(b) Basic variables $= \left( {{x}_{2},{x}_{3},{x}_{1}}\right)$ , Inverse $= \left( \begin{array}{rrr} \frac{1}{4} &  - \frac{1}{8} & \frac{1}{8} \\  \frac{3}{2} &  - \frac{1}{4} &  - \frac{3}{4} \\   - 1 & \frac{1}{2} & \frac{1}{2} \end{array}\right)$

(c) Basic variables $= \left( {{x}_{2},{x}_{3},{x}_{6}}\right)$ , Inverse $= \left( \begin{array}{rrr} \frac{1}{2} &  - \frac{1}{4} & 0 \\  0 & \frac{1}{2} & 0 \\   - 2 & 1 & 1 \end{array}\right)$

*4-22. Consider the following LP model:

$$
\text{ Minimize }z = 2{x}_{1} + {x}_{2}
$$

subject to

$$
3{x}_{1} + {x}_{2} - {x}_{3}\; = 3
$$

$$
4{x}_{1} + 3{x}_{2}\; - {x}_{4}\; = 6
$$

$$
{x}_{1} + 2{x}_{2}\; + {x}_{5} = 3
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} \geq  0
$$

Compute the entire simplex tableau associated with the following basic solution, and check it for optimality and feasibility.

$$
\text{ Basic variables } = \left( {{x}_{1},{x}_{2},{x}_{5}}\right) \text{ , Inverse } = \left( \begin{array}{rrr} \frac{3}{5} &  - \frac{1}{5} & 0 \\   - \frac{4}{5} & \frac{3}{5} & 0 \\  1 &  - 1 & 1 \end{array}\right)
$$

4-23. Consider the following LP model:

$$
\text{ Maximize }z = 5{x}_{1} + {12}{x}_{2} + 4{x}_{3}
$$

subject to

$$
{x}_{1} + 2{x}_{2} + {x}_{3} + {x}_{4} = 5
$$

$$
2{x}_{1} - {x}_{2} + 3{x}_{3}\; = 1
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

(a) Identify the best solution from among the following basic feasible solutions:

(i) Basic variables $= \left( {{x}_{4},{x}_{3}}\right)$ , Inverse $= \left( \begin{array}{rr} 1 &  - \frac{1}{3} \\  0 & \frac{1}{3} \end{array}\right)$

(ii) Basic variables $= \left( {{x}_{2},{x}_{1}}\right)$ , Inverse $= \left( \begin{array}{rr} \frac{2}{5} &  - \frac{1}{5} \\  \frac{1}{5} & \frac{2}{5} \end{array}\right)$

(iii) Basic variables $= \left( {{x}_{2},{x}_{3}}\right)$ , Inverse $= \left( \begin{matrix} \frac{3}{7} &  - \frac{1}{7} \\  \frac{1}{7} & \frac{2}{7} \end{matrix}\right)$

(b) Is the solution obtained in (a) optimum for the LP model?

4-24. Consider the following LP model:

$$
\text{ Maximize }z = 5{x}_{1} + 2{x}_{2} + 3{x}_{3}
$$

subject to

$$
{x}_{1} + 5{x}_{2} + 2{x}_{3} \leq  {b}_{1}
$$

$$
{x}_{1} - 5{x}_{2} - 6{x}_{3} \leq  {b}_{2}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

The following optimal tableau corresponds to specific values of ${b}_{1}$ and ${b}_{2}$ :

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | $a$ | 7 | $d$ | $e$ | 15 |
| ${x}_{1}$ | 1 | $b$ | 2 | 1 | 0 | 3 |
| ${x}_{5}$ | 0 | $C$ | -8 | -1 | 1 | 1 |

Determine the following:

(a) The right-hand-side values, ${b}_{1}$ and ${b}_{2}$ .

(b) The optimal dual solution.

(c) The elements $a, b, c, d$ , and $e$ .

*4-25. The following is the optimal tableau for a maximization LP model with three $\left(  \leq  \right)$ constraints and all nonnegative variables. The variables ${x}_{3},{x}_{4}$ , and ${x}_{5}$ are the slacks associated with the three constraints. Determine the associated optimal objective value in two different ways by using the primal and dual objective functions.

| Basic | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${x}_{5}$ | Solution |
| --- | --- | --- | --- | --- | --- | --- |
| $z$ | 0 | 0 | 0 | 3 | 2 | ? |
| ${x}_{3}$ | 0 | 0 | 1 | 1 | -1 | 2 |
| ${x}_{2}$ | 0 | 1 | 0 | 1 | 0 | 6 |
| ${x}_{1}$ | 1 | 0 | 0 | -1 | 1 | 2 |

4-26. Consider the following LP:

$$
\text{ Maximize }z = 2{x}_{1} + 4{x}_{2} + 4{x}_{3} - 3{x}_{4}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} = 4
$$

$$
{x}_{1} + 4{x}_{2} + {x}_{4} = 8
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

Use the dual problem to show that the basic solution $\left( {{x}_{1},{x}_{2}}\right)$ is not optimal.

4-27. Show that Method 1 in Section 4.2.3 for determining the optimal dual values is actually based on the Formula 2 in Section 4.2.4.

4-28. In Example 4.3-1, compute the change in the optimal revenue in each of the following cases (use TORA output to obtain the feasibility ranges):

(a) The constraint for raw material ${M1}$ (resource 1) is $6{x}_{1} + 4{x}_{2} \leq  {20}$ .

(b) The constraint for raw material ${M2}$ (resource 2) is ${x}_{1} + 2{x}_{2} \leq  5$ .

(c) The market condition represented by resource 4 is ${x}_{2} \leq  4$ .

*4-29. NWAC Electronics manufactures four types of simple cables for a defense contractor. Each cable must go through four sequential operations: splicing, soldering, sleeving, and inspection. The following table gives the pertinent data of the situation:

| Cable | Splicing (min/unit) | Soldering (min/unit) | Sleeving (min/unit) | Inspection (min/unit) | Unit revenue (\$) |
| --- | --- | --- | --- | --- | --- |
| SC320 | 10.5 | 20.4 | 3.2 | 5.0 | 9.40 |
| SC325 | 9.3 | 24.6 | 2.5 | 5.0 | 10.80 |
| SC340 | 11.6 | 17.7 | 3.6 | 5.0 | 8.75 |
| SC370 | 8.2 | 26.5 | 5.5 | 5.0 | 7.80 |
| Daily capacity (minutes) | 4,800.0 | 9,600.0 | 4,700.0 | 4,500.0 |  |

The contractor guarantees a minimum production level of 100 units for each of the four cables.

(a) Formulate the problem as a linear programming model, and determine the optimum production schedule.

(b) Based on the dual prices, do you recommend making increases in the daily capacities of any of the four operations? Explain.

(c) Does the minimum production requirements for the four cables represent an advantage or a disadvantage for NWAC Electronics? Provide an explanation based on the dual prices.

(d) Can the present unit contribution to revenue as specified by the dual price be guaranteed if we increase the capacity of soldering by 10%?

4-30. BagCo produces leather jackets and handbags. A jacket requires $8{\mathrm{\;m}}^{2}$ of leather, and a handbag only $2{\mathrm{\;m}}^{2}$ . The labor requirements for the two products are 12 and 5 hours, respectively. The current weekly supplies of leather and labor are limited to ${600}{\mathrm{\;m}}^{2}$ and 925 hours, respectively. The company sells the jackets and handbags at \$350 and \$120, respectively. The objective is to determine the production schedule that maximizes the net revenue.

(a) Determine the optimum solution.

(b) BagCo is considering an expansion of production. What is the maximum purchase price the company should pay for additional leather? For additional labor?

4-31. In Example 4.3-2, suppose that for toy trains the per-unit time of operation 2 can be reduced from 3 minutes to at most 1.3 minutes. By how much must the per-unit time of operation 1 be reduced to make toy trains just profitable?

*4-32. In Example 4.3-2, suppose that TOYCO is studying the possibility of introducing a fourth toy: fire trucks. The assembly does not make use of operation 1. Its unit assembly times on operations 2 and 3 are 1 and 3 minutes, respectively. The revenue per unit is \$4. Would you advise TOYCO to introduce the new product?

*4-33. JoShop uses lathes and drill presses to produce four types of machine parts, PP1, PP2, PP3, and PP4. The following table summarizes the pertinent data:

| Machine | PP1 (min/unit) | PP2 (min/unit) | PP3 (min/unit) | PP4 (min/unit) | Capacity (min) |
| --- | --- | --- | --- | --- | --- |
| Lathes | 2 | 5 | 3 | 4 | 5300 |
| Drill presses | 3 | 4 | 6 | 4 | 5300 |
| Unit revenue (\$) | 3 | 6 | 5 | 4 |  |

For the parts that are not produced by the present optimum solution, determine the rate of deterioration in the optimum revenue per unit increase of each of these products.

4-34. Consider the optimal solution of JoShop in Problem 4-33. The company estimates that for each part that is not produced (per the optimum solution), an across-the-board 20% reduction in machining time can be realized through process improvements. Would these improvements make these parts profitable? If not, what is the minimum percentage reduction needed to realize profitability?

4-35. Consider the solution space in Figure 4.3, where it is desired to find the optimum extreme point that uses the dual simplex method to minimize $z = 2{x}_{1} + {x}_{2}$ . The optimal solution occurs at point $F = \left( {{0.5},{1.5}}\right)$ on the graph.

(a) Can the dual simplex start at point A?

*(b) If the starting basic (infeasible but better than optimum) solution is given by point $G$ with the optimum given by point $F$ , would it be possible for the iterations of the dual simplex method to follow the path $G \rightarrow  E \rightarrow  F$ ? Explain.

(c) If the starting basic (infeasible) solution starts at point $L$ , identify a possible path of the dual simplex method that leads to the optimum feasible point at point $F$ .

4-36. Generate the dual simplex iterations for the following problems (using TORA for convenience), and trace the path of the algorithm on the graphical solution space.

(a) Minimize $z = 2{x}_{1} + 3{x}_{2}$ subject to

$$
2{x}_{1} + 2{x}_{2} \leq  3
$$

$$
{x}_{1} + 2{x}_{2} \geq  1
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

![bo_d56m4aref24c73bhe5pg_33_433_200_1004_730_0.jpg](bo_d56m4aref24c73bhe5pg_33_433_200_1004_730_0.jpg)

FIGURE 4.3

Solution space for Problem 4-35

---

					(b) Minimize $z = 5{x}_{1} + 6{x}_{2}$

								subject to

$$
{x}_{1} + {x}_{2} \geq  {20}
$$

$$
4{x}_{1} + {x}_{2} \geq  {40}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

					(c) Minimize $z = 4{x}_{1} + 2{x}_{2}$

								subject to

$$
{x}_{1} + {x}_{2} = {10}
$$

$$
3{x}_{1} - {x}_{2} \geq  {20}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

					(d) Minimize $z = 2{x}_{1} + 3{x}_{2}$

								subject to

$$
2{x}_{1} + {x}_{2} \geq  {30}
$$

$$
{x}_{1} + {x}_{2} = {20}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

4-37. Dual Simplex with Artificial Constraints. Consider the following problem:

$$
\text{ Maximize }z = 2{x}_{1} - {x}_{2} + {x}_{3}
$$

---

subject to

$$
2{x}_{1} + 3{x}_{2} - 5{x}_{3} \geq  4
$$

$$
- {x}_{1} + 9{x}_{2} - {x}_{3} \geq  3
$$

$$
4{x}_{1} + 6{x}_{2} + 3{x}_{3} \leq  8
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

The starting basic solution consisting of surplus variables ${x}_{4}$ and ${x}_{5}$ and slack variable ${x}_{6}$ is infeasible because ${x}_{4} =  - 4$ and ${x}_{5} =  - 3$ . However, the dual simplex is not applicable directly, because ${x}_{1}$ and ${x}_{3}$ do not satisfy the maximization optimality condition. Show that by adding the artificial constraint ${x}_{1} + {x}_{3} \leq  M$ (where $M$ is sufficiently large not to eliminate any feasible points in the original solution space), and then using the new constraint as a pivot row, the selection of ${x}_{1}$ as the entering variable (because it has the most negative objective coefficient) will render an all-optimal objective row. Next, carry out the regular dual simplex method on the modified problem.

4-38. Using the artificial constraint procedure introduced in Problem 4-37, solve the following problems by the dual simplex method. In each case, indicate whether the resulting solution is feasible, infeasible, or unbounded.

(a) Maximize $z = 2{x}_{3}$

subject to

$$
- {x}_{1} + 2{x}_{2} - 2{x}_{3} \geq  4
$$

$$
- {x}_{1} + {x}_{2} + {x}_{3} \leq  2
$$

$$
2{x}_{1} - {x}_{2} + 4{x}_{3} \leq  5
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

(b) Maximize $z = {x}_{1} - 3{x}_{2}$ subject to

$$
{x}_{1} - {x}_{2} \leq  {20}
$$

$$
{x}_{1} + {x}_{2} \geq  {40}
$$

$$
2{x}_{1} - 2{x}_{2} \geq  {30}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

*(c) Minimize $z =  - {x}_{1} + {x}_{2}$ subject to

$$
{x}_{1} - 4{x}_{2} \geq  5
$$

$$
{x}_{1} - 3{x}_{2} \leq  1
$$

$$
2{x}_{1} - 5{x}_{2} \geq  1
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(d) Maximize $z = 2{x}_{3}$

subject to

$$
- {x}_{1} + 3{x}_{2} - 7{x}_{3} \geq  {50}
$$

$$
- {x}_{1} + {x}_{2} - \;{x}_{3} \leq  {10}
$$

$$
3{x}_{1} + {x}_{2} - {10}{x}_{3} \leq  {80}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

4-39. Solve the following LP in three different ways (use TORA for convenience). Which method appears to be the most efficient computationally?

$$
\text{ Minimize }z = 6{x}_{1} + 7{x}_{2} + 3{x}_{3} + 5{x}_{4}
$$

subject to

$$
5{x}_{1} + 6{x}_{2} - 3{x}_{3} + 4{x}_{4} \geq  {12}
$$

$$
{x}_{2} - 5{x}_{3} - 6{x}_{4} \geq  {10}
$$

$$
2{x}_{1} + 5{x}_{2} + {x}_{3} + {x}_{4} \geq  8
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

4-40. The LP model of Problem 4-38(c) has no feasible solution. Show how this condition is detected by the generalized simplex procedure.

4-41. The LP model of Problem 4-38(d) has no bounded solution. Show how this condition is detected by the generalized simplex procedure.

4-42. In the TOYCO model listed at the start of Section 4.5, would it be more advantageous to assign the 20-minute excess capacity of operation 3 to operation 2 instead of operation 1?

4-43. Suppose that TOYCO wants to change the capacities of the three operations according to the following cases:

(a) $\left( \begin{array}{l} {460} \\  {500} \\  {400} \end{array}\right)$ (b) $\left( \begin{array}{l} {500} \\  {400} \\  {600} \end{array}\right)$ (c) $\left( \begin{array}{l} {300} \\  {800} \\  {200} \end{array}\right)$ (d) $\left( \begin{array}{l} {450} \\  {700} \\  {350} \end{array}\right)$

Use post-optimal analysis to determine the optimum solution in each case.

4-44. Consider the Reddy Mikks model of Example 2.1-1. Its optimal tableau is given in Example 3.3-1. If the daily availabilities of raw materials ${M1}$ and ${M2}$ are increased to 35 and 10 tons, respectively, use post-optimal analysis to determine the new optimal solution.

*4-45. The Ozark Farm has 20,000 broilers that are fed for 8 weeks before being marketed. The weekly feed per broiler varies according to the following schedule:

| Week | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| lb/broiler | 0.26 | 0.48 | 0.75 | 1.00 | 1.30 | 1.60 | 1.90 | 2.10 |

For the broiler to reach a desired weight gain in 8 weeks, the feedstuffs must satisfy specific nutritional needs. Although a typical list of feedstuffs is large, for simplicity

we will limit the model to three items only: limestone, corn, and soybean meal. The nutritional needs will also be limited to three types: calcium, protein, and fiber. The following table summarizes the nutritive content of the selected ingredients together with the cost data.

| Ingredient | Calcium (lb/lb) | Protein (lb/lb) | Fiber (lb/lb) | \$ per lb |
| --- | --- | --- | --- | --- |
| Limestone | 0.380 | 0.00 | 0.00 | 0.12 |
| Corn | 0.001 | 0.09 | 0.02 | 0.45 |
| Soybean meal | 0.002 | 0.50 | 0.08 | 1.60 |

The feed mix must contain at least .8% but not more than 1.2% calcium, at least 22% protein, and at most 5% crude fiber.

Solve the LP for week 1 and then use post-optimal analysis to develop an optimal schedule for the remaining 7 weeks.

4-46. Show that the 100% feasibility rule in Problem 3-79 (Chapter 3) is based on the condition

$$
\left( \begin{matrix} \text{ Optimum } \\  \text{ inverse } \end{matrix}\right) \left( \begin{matrix} \text{ Original right-hand } \\  \text{ side vector } \end{matrix}\right)  \geq  0
$$

4-47. Post-Optimal Analysis for Cases Affecting Both Optimality and Feasibility. Suppose that you are given the following simultaneous changes in the Reddy Mikks model: The revenue per ton of exterior and interior paints are \$2000 and \$5000, respectively, and the maximum daily availabilities of raw materials, ${M1}$ and ${M2}$ , are 35 and 10 tons, respectively.

(a) Show that the proposed changes will render the current optimal solution both non-optimal and infeasible.

(b) Use the generalized simplex algorithm (Section 4.4.2) to determine the new optimal feasible solution.

4-48. In the TOYCO model, suppose the fourth operation has the following specifications: The maximum production rate based on 480 minutes a day is 120 units of product 1,480 units of product 2, or 240 units of product 3. Determine the optimal solution, assuming that the daily capacity is limited to

*(a) 565 minutes.

(b) 548 minutes.

4-49. Secondary Constraints. Instead of solving a problem using all of its constraints, we can start by identifying the so-called secondary constraints. These are the constraints that we suspect are least restrictive in terms of the optimum solution. The model is solved using the remaining (primary) constraints. We may then add the secondary constraints one at a time. A secondary constraint is discarded if it satisfies the available optimum. The process is repeated until all the secondary constraints are accounted for.

Apply the proposed procedure to the following LP:

$$
\text{ Maximize }z = 5{x}_{1} + 6{x}_{2} + 3{x}_{2}
$$

subject to

$$
5{x}_{1} + 5{x}_{2} + 3{x}_{3} \leq  {50}
$$

$$
{x}_{1} + {x}_{2} - {x}_{3} \leq  {20}
$$

$$
7{x}_{1} + 6{x}_{2} - 9{x}_{3} \leq  {30}
$$

$$
5{x}_{1} + 5{x}_{2} + 5{x}_{3} \leq  {35}
$$

$$
{12}{x}_{1} + 6{x}_{2}\; \leq  {90}
$$

$$
{x}_{2} - 9{x}_{3} \leq  {20}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

4-50. Investigate the optimality of the TOYCO solution for each of the following objective functions. Where necessary, use post-optimal analysis to determine the new optimum. (The optimum tableau of TOYCO is given at the start of Section 4.5.)

(a) $z = 4{x}_{1} + 2{x}_{2} + 8{x}_{3}$

(b) $z = 3{x}_{1} + 6{x}_{2} + {x}_{3}$

(c) $z = {16}{x}_{1} + 6{x}_{2} + {18}{x}_{3}$

4-51. Investigate the optimality of the Reddy Mikks solution (Example 4.3-1) for each of the following objective functions. If necessary, use post-optimal analysis to determine the new optimum. (The optimal tableau of the model is given in Example 3.3-1.)

*(a) $z = 3{x}_{1} + 2{x}_{2}$

(b) $z = 8{x}_{1} + {10}{x}_{2}$

*(c) $z = 2{x}_{1} + 5{x}_{2}$

4-52. Show that the 100% optimality rule (Problem 3-88, Chapter 3) is derived from (reduced costs) $\geq  0$ for maximization problems and (reduced costs) $\leq  0$ for minimization problems.

*4-53. In the original TOYCO model, toy trains are not part of the optimal product mix. The company recognizes that market competition will not allow raising the unit price of the toy. Instead, the company wants to concentrate on improving the assembly operation itself. This entails reducing the assembly time per unit in each of the three operations by a specified percentage, $p\%$ . Determine the value of $p$ that will make toy trains just profitable. (The optimum tableau of the TOYCO model is given at the start of Section 4.5.)

4-54. In the TOYCO model, suppose that the company can reduce the unit times on operations 1, 2, and 3 for toy trains from the current levels of 1, 3, and 1 minutes to .5, 1, and .5 minutes, respectively. The revenue per unit is changed to \$4. Determine the new optimum solution.

4-55. In the TOYCO model, suppose that a new toy (fire engine) requires 3, 2, and 4 minutes, respectively, on operations 1, 2, and 3. Determine the optimal solution when the revenue per unit is given by

*(a) \$5. (b) \$10.

4-56. In the Reddy Mikks model, the company is considering the production of a cheaper brand of exterior paint whose input requirements per ton include .75 ton of each of raw materials ${M1}$ and ${M2}$ . Market conditions still dictate that the excess of interior paint over the production of both types of exterior paint be limited to 1 ton daily. The revenue per ton of the new exterior paint is \$3500. Determine the new optimal solution. (The model is explained in Example 4.5-1, and its optimum tableau is given in Example 3.3-1.)
