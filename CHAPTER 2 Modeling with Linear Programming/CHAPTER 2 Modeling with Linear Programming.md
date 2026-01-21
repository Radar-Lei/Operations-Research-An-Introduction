## CHAPTER 2 Modeling with Linear Programming ^chapter

```markmap
---
markmap:
  height: 643
---
# [[#^chapter|CHAPTER 2: Modeling with Linear Programming]]

## [[#^frontier|Real-Life Application: Frontier Airlines]]

## [[#^twovar|2.1 Two-Variable LP Model]]
### [[#^reddy|Example: Reddy Mikks]]
#### [[#^components|Model Components]]
##### [[#^variables|Decision Variables]]
##### [[#^objective|Objective Function]]
##### [[#^constraints|Constraints]]
###### [[#^nonnegativity|Non-negativity]]
#### [[#^model|Complete LP Formulation]]
##### [[#^feasiblesol|Feasible vs Infeasible Solutions]]
##### [[#^optimumsol|Optimum Solution]]
##### [[#^properties|Linearity & Certainty]]

## [[#^graphical|2.2 Graphical LP Solution]]
### [[#^maximization|Maximization Case]]
#### [[#^feasible|Feasible Region]]
#### [[#^optimum|Optimum Solution (Iso-Profit)]]
#### [[#^corner|Corner Point Optimality]]
### [[#^minimization|Minimization Case]]
#### [[#^diet|Diet Problem Example]]
#### [[#^weakineq|Significance of Inequalities]]

## [[#^computer|2.3 Computer Solution]]
### [[#^solver|Excel Solver]]
### [[#^ampl|AMPL]]
#### [[#^longhand|Rudimentary Model]]
#### [[#^modeldata|Algebraic Model (Data Separation)]]

## [[#^applications|2.4 LP Applications]]
### [[#^investment|Investment]]
#### [[#^bankloan|Bank Loan Model]]
##### [[#^bankobj|Objective: Net Return]]
##### [[#^bankconst|Constraints: Policy & Ratios]]
### [[#^production|Production & Inventory]]
#### [[#^singleperiod|Single-Period Model]]
##### [[#^singleobj|Objective: Minimize Penalty]]
#### [[#^multiperiod|Multi-Period Model]]
##### [[#^inventorybal|Inventory Balance Equation]]
#### [[#^smoothing|Production Smoothing]]
##### [[#^hiringfiring|Hiring & Firing Costs]]
##### [[#^substitution|Variable Substitution]]
### [[#^workforce|Workforce Planning]]
#### [[#^qantas|Qantas Application]]
#### [[#^busscheduling|Bus Scheduling (Overlapping Shifts)]]
##### [[#^overlapping|Shift Definition]]
### [[#^urban|Urban Development]]
#### [[#^urbanrenewal|Urban Renewal Model]]
### [[#^blending|Blending & Refining]]
#### [[#^crudeoil|Crude Oil Refining]]
##### [[#^octanecalc|Octane Number Calculation]]
### [[#^additional|Additional Applications]]

## [[#^bibliography|Bibliography]]

## [[#^problems|Problems]]
```

## Real-Life Application—Frontier Airlines Purchases Fuel Economically ^frontier

The fueling of an aircraft can take place at any of the stopovers along a flight route. Fuel price varies among the stopovers, and potential savings can be realized by tankering (loading) extra fuel at a cheaper location for use on subsequent flight legs. The disadvantage is that the extra weight of tankered fuel will result in higher burn of gasoline. Linear programming (LP) and heuristics are used to determine the optimum amount of tanker-ing that balances the cost of excess burn against the savings in fuel cost. The study, carried out in 1981, resulted in net savings of about $350,000 per year. With the significant rise in the cost of fuel, many airlines are using LP-based tankering software to purchase fuel. Details of the study are given in Case 1, Chapter 26 on the website.

### 2.1 TWO-VARIABLE LP MODEL ^twovar

This section deals with the graphical solution of a two-variable LP. Though two-variable problems hardly exist in practice, the treatment provides concrete foundations for the development of the general simplex algorithm presented in Chapter 3.

## Example 2.1-1 (The Reddy Mikks Company) ^reddy

Reddy Mikks produces both interior and exterior paints from two raw materials, ${M1}$ and ${M2}$ . The following table provides the basic data of the problem:

|                        | Exterior paint | Interior paint | Maximum daily availability (tons) |
| ---------------------- | -------------- | -------------- | --------------------------------- |
| Raw material, M1       | 6              | 4              | 24                                |
| Raw material, M2       | 1              | 2              | 6                                 |
| Profit per ton ($1000) | 5              | 4              |                                   |

The daily demand for interior paint cannot exceed that for exterior paint by more than 1 ton. Also, the maximum daily demand for interior paint is 2 tons.

Reddy Mikks wants to determine the optimum (best) product mix of interior and exterior paints that maximizes the total daily profit.

All OR models, LP included, consist of three basic components: ^components

1. Decision variables that we seek to determine.

2. Objective (goal) that we need to optimize (maximize or minimize).

3. Constraints that the solution must satisfy.

The proper definition of the decision variables is an essential first step in the development of the model. Once done, the task of constructing the objective function and the constraints becomes more straightforward.

For the Reddy Mikks problem, we need to determine the daily amounts of exterior and interior paints to be produced. Thus the variables of the model are defined as: ^variables

$$
{x}_{1} = \text{ Tons produced daily of exterior paint }
$$

$$
{x}_{2} = \text{ Tons produced daily of interior paint }
$$

The goal of Reddy Mikks is to maximize (i.e., increase as much as possible) the total daily profit of both paints. The two components of the total daily profit are expressed in terms of the variables ${x}_{1}$ and ${x}_{2}$ as:

$$
\text{ Profit from exterior paint } = 5{x}_{1}\text{ (thousand) dollars }
$$

$$
\text{ Profit from interior paint } = 4{x}_{2}\text{ (thousand) dollars }
$$

Letting $z$ represent the total daily profit (in thousands of dollars), the objective (or goal) of Reddy Mikks is expressed as ^objective

$$
\text{ Maximize }z = 5{x}_{1} + 4{x}_{2}
$$

Next, we construct the constraints that restrict raw material usage and product demand. The raw material restrictions are expressed verbally as ^constraints

$$
\left( \begin{matrix} \text{ Usage of a raw material } \\  \text{ by both paints } \end{matrix}\right)  \leq  \left( \begin{matrix} \text{ Maximum raw material } \\  \text{ availability } \end{matrix}\right)
$$

The daily usage of raw material ${M1}$ is 6 tons per ton of exterior paint and 4 tons per ton of interior paint. Thus,

Usage of raw material ${M1}$ by both paints $= 6{x}_{1} + 4{x}_{2}$ tons/day

In a similar manner,

$$
\text{ Usage of raw material }{M2}\text{ by both paints } = 1{x}_{1} + 2{x}_{2}\text{ tons/day }
$$

The maximum daily availabilities of raw materials ${M1}$ and ${M2}$ are 24 and 6 tons, respectively. Thus, the raw material constraints are:

$$
6{x}_{1} + 4{x}_{2} \leq  {24}\;\text{ (Raw material }{M1}\text{ ) }
$$

$$
{x}_{1} + 2{x}_{2} \leq  6\text{ (Raw material }{M2}\text{ ) }
$$

The first restriction on product demand stipulates that the daily production of interior paint cannot exceed that of exterior paint by more than 1 ton, which translates to:

$$
{x}_{2} - {x}_{1} \leq  1\;\text{ (Market limit) }
$$

The second restriction limits the daily demand of interior paint to 2 tons-that is,

$$
{x}_{2} \leq  2\text{ (Demand limit) }
$$

An implicit (or "understood-to-be") restriction requires (all) the variables, ${x}_{1}$ and ${x}_{2}$ , to assume zero or positive values only. The restrictions, expressed as ${x}_{1} \geq  0$ and ${x}_{2} \geq  0$ , are referred to as nonnegativity constraints. ^nonnegativity

The complete Reddy Mikks model is ^model

$$
\text{ Maximize }z = 5{x}_{1} + 4{x}_{2}
$$

subject to

$$
6{x}_{1} + 4{x}_{2} \leq  {24}\left( 1\right)
$$

$$
{x}_{1} + 2{x}_{2} \leq  6\left( 2\right)
$$

$$
- {x}_{1} + {x}_{2} \leq  1\left( 3\right)
$$

$$
{x}_{2} \leq  2\left( 4\right)
$$

$$
{x}_{1},{x}_{2} \geq  0\left( 5\right)
$$

Any values of ${x}_{1}$ and ${x}_{2}$ that satisfy all five constraints constitute a feasible solution. Otherwise, the solution is infeasible. For example, the solution ${x}_{1} = 3$ tons per day and ${x}_{2} = 1$ ton per day is feasible because it does not violate any of the five constraints;a result that is confirmed by using substituting $\left( {{x}_{1} = 3,{x}_{2} = 1}\right)$ in the left-hand side of each constraint. In constraint (1), we have $6{x}_{1} + 4{x}_{2} = \left( {6 \times  3}\right)  + \left( {4 \times  1}\right)  = {22}$ , which is less than the right-hand side of the constraint $\left( { = {24}}\right)$ . Constraints 2 to 5 are checked in a similar manner (verify!). On the other hand, the solution ${x}_{1} = 4$ and ${x}_{2} = 1$ is infeasible because it does not satisfy at least one constraint. For example, in constraint $\left( 1\right) ,\left( {6 \times  4}\right)  + \left( {4 \times  1}\right)  = {28}$ , which is larger than the right-hand side $\left( { = {24}}\right)$ . ^feasiblesol

The goal of the problem is to find the optimum, the best feasible solution that maximizes the total profit $z$ . First, we need to show that the Reddy Mikks problem has an infinite number of feasible solutions, a property that is shared by all nontrivial LPs. Hence the problem cannot be solved by enumeration. The graphical method in Section 2.2 and its algebraic generalization in Chapter 3 show how the optimum can be determined in a finite number of steps. ^optimumsol

Remarks. The objective and the constraint function in all LPs must be linear. Additionally, all the parameters (coefficients of the objective and constraint functions) of the model are known with certainty. ^properties

### 2.2 GRAPHICAL LP SOLUTION ^graphical

The graphical solution includes two steps:

1. Determination of the feasible solution space.

2. Determination of the optimum solution from among all the points in the solution space.

The presentation uses two examples to show how maximization and minimization objective functions are handled.

#### 2.2.1 Solution of a Maximization Model ^maximization

Example 2.2-1

This example solves the Reddy Mikks model of Example 2.1-1.

## Step 1. Determination of the Feasible Solution Space: ^feasible

First, consider the nonnegativity constraints ${x}_{1} \geq  0$ and ${x}_{2} \geq  0$ . In Figure 2.1, the horizontal axis ${x}_{1}$ and the vertical axis ${x}_{2}$ represent the exterior- and interior-paint variables, respectively. Thus, the nonnegativity constraints restrict the variables to the first quadrant (above the ${x}_{1}$ -axis and to the right of the ${x}_{2}$ -axis).

To account for the remaining four constraints, first replace each inequality with an equation, and then graph the resulting straight line by locating two distinct points. For example, after replacing $6{x}_{1} + 4{x}_{2} \leq  {24}$ with the straight line $6{x}_{1} + 4{x}_{2} = {24}$ , two distinct points are determined by setting ${x}_{1} = 0$ to obtain ${x}_{2} = \frac{24}{4} = 6$ and then by setting ${x}_{2} = 0$ to obtain ${x}_{1} = \frac{24}{6} = 4$ . Thus the line $6{x}_{1} + 4{x}_{2} = {24}$ passes through $\left( {0,6}\right)$ and $\left( {4,0}\right)$ , as shown by line (1) in Figure 2.1.

Next, consider the direction $\left( { > \text{ or } < }\right)$ of the inequality. It divides the $\left( {{x}_{1},{x}_{2}}\right)$ plane into two half-spaces, one on each side of the graphed line. Only one of these two halves satisfies the inequality. To determine the correct side, designate any point not lying on the straight line as a reference point. If the chosen reference point satisfies the inequality, then its side is feasible; otherwise, the opposite side becomes the feasible half-space.

The origin $\left( {0,0}\right)$ is a convenient reference point and should always be used so long as it does not lie on the line representing the constraint. This happens to be true for all the constraints of this example. Starting with the constraint $6{x}_{1} + 4{x}_{2} \leq  {24}$ , substitution of $\left( {{x}_{1},{x}_{2}}\right)  = \left( {0,0}\right)$ automatically yields zero for the left-hand side. Since it is less than 24, the half-space containing $\left( {0,0}\right)$ is feasible for inequality (1), as the direction of the arrow in Figure 2.1 shows. A similar application of the reference-point procedure to the remaining constraints produces the feasible solution space ${ABCDEF}$ in which all the constraints are satisfied (verify!). All points outside the boundary of the area ${ABCDEF}$ are infeasible.

FIGURE 2.1

Feasible space of the Reddy Mikks model

![bo_d56m43v7aajc73800n2g_3_470_1309_924_864_0.jpg](bo_d56m43v7aajc73800n2g_3_470_1309_924_864_0.jpg)

## Step 2. Determination of the Optimum Solution: ^optimum

The number of solution points in the feasible space ${ABCDEF}$ in Figure 2.1 is infinite, clearly precluding the use of exhaustive enumeration. A systematic procedure is thus needed to determine the optimum solution.

First, the direction in which the profit function $z = 5{x}_{1} + 4{x}_{2}$ increases (recall that we are maximizing $z$ ) is determined by assigning arbitrary increasing values to $z$ . In Figure 2.2, the two lines $5{x}_{1} + 4{x}_{2} = {10}$ and $5{x}_{1} + 4{x}_{2} = {15}$ corresponding to (arbitrary) $z = {10}$ and $z = {15}$ depict the direction in which $z$ increases. Moving in that direction, the optimum solution occurs at $C$ because it is the feasible point in the solution space beyond which any further increase will render an infeasible solution.

The values of ${x}_{1}$ and ${x}_{2}$ associated with the optimum point $C$ are determined by solving the equations associated with lines (1) and (2):

$$
6{x}_{1} + 4{x}_{2} = {24}
$$

$$
{x}_{1} + 2{x}_{2} = 6
$$

FIGURE 2.2

Optimum solution of the Reddy Mikks model

![bo_d56m43v7aajc73800n2g_4_432_1333_1084_837_0.jpg](bo_d56m43v7aajc73800n2g_4_432_1333_1084_837_0.jpg)

The solution is ${x}_{1} = 3$ and ${x}_{2} = {1.5}$ with $z = \left( {5 \times  3}\right)  + \left( {4 \times  {1.5}}\right)  = {21}$ . This calls for a daily product mix of 3 tons of exterior paint and 1.5 tons of interior paint. The associated daily profit is \$21,000.

Remarks. In practice, a typical LP may include hundreds or even thousands of variables and constraints. Of what good then is the study of a two-variable LP? The answer is that the graphical solution provides a key result: The optimum solution of an LP, when it exists, is always associated with a corner point of the solution space, thus limiting the search for the optimum from an infinite number of feasible points to a finite number of corner points. This powerful result is the basis for the development of the general algebraic simplex method presented in Chapter 3.1 ^corner

#### 2.2.2 Solution of a Minimization Model ^minimization

## Example 2.2-2 (Diet Problem) ^diet

Ozark Farms uses at least 800 lb of special feed daily. The special feed is a mixture of corn and soybean meal with the following compositions:


| Feedstuff | lb per lb of feedstuff - Protein | Fiber | Cost (\$/lb) |
| --- | --- | --- | --- |
| Corn | .09 | .02 | .30 |
| Soybean meal | .60 | .06 | .90 |


The dietary requirements of the special feed are at least 30% protein and at most 5% fiber. The goal is to determine the daily minimum-cost feed mix.

The decision variables of the model are:

$$
{x}_{1} = \mathrm{{lb}}\text{ of corn in the daily mix }
$$

$$
{x}_{2} = \mathrm{{lb}}\text{ of soybean meal in the daily mix }
$$

The objective is to minimize the total daily cost (in dollars) of the feed mix-that is,

$$
\text{ Minimize }z = {.3}{x}_{1} + {.9}{x}_{2}
$$

---

${}^{1}$ To reinforce this key result, use TORA to verify that the optimum of the following objective functions of the Reddy Mikks model (Example 2.1-1) will yield the associated corner points as defined in Figure 2.2 (click View/Modify Input Data to modify the objective coefficients and re-solve the problem graphically):

(a) $z = 5{x}_{1} + {x}_{2}$ (optimum: point $B$ in Figure 2.2)

(b) $z = 5{x}_{1} + 4{x}_{2}$ (optimum: point $C$ )

(c) $z = {x}_{1} + 3{x}_{2}$ (optimum: point $D$ )

(d) $z = {x}_{2}$ (optimum: point $D$ or $E$ , or any point inbetween-see Section 3.5.2)

(e) $z =  - 2{x}_{1} + {x}_{2}$ (optimum: point $F$ )

(f) $z =  - {x}_{1} - {x}_{2}$ (optimum: point $A$ )

---

The constraints represent the daily amount of the mix and the dietary requirements. Ozark Farms needs at least 800 lb of feed a day-that is,

$$
{x}_{1} + {x}_{2} \geq  {800}
$$

The amount of protein included in ${x}_{1}$ lb of corn and ${x}_{2}$ lb of soybean meal is $\left( {{.09}{x}_{1} + {.6}{x}_{2}}\right)$ lb. This quantity should equal at least ${30}\%$ of the total feed mix $\left( {{x}_{1} + {x}_{2}}\right)$ lb-that is,

$$
{.09}{x}_{1} + {.6}{x}_{2} \geq  {.3}\left( {{x}_{1} + {x}_{2}}\right)
$$

In a similar manner, the fiber requirement of at most 5% is represented as

$$
{.02}{x}_{1} + {.06}{x}_{2} \leq  {.05}\left( {{x}_{1} + {x}_{2}}\right)
$$

The constraints are simplified by moving the terms in ${x}_{1}$ and ${x}_{2}$ to the left-hand side of each inequality, leaving only a constant on the right-hand side. The complete model is

$$
\text{ Minimize }z = {.3}{x}_{1} + {.9}{x}_{2}
$$

subject to

$$
{x}_{1} + \;{x}_{2} \geq  {800}
$$

$$
{.21}{x}_{1} - {.30}{x}_{2} \leq  0
$$

$$
{.03}{x}_{1} - {.01}{x}_{2} \geq  0
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

Figure 2.3 provides the graphical solution of the model. The second and third constraints pass through the origin. Thus, unlike the Reddy Mikks model of Example 2.2-1, the determination of

FIGURE 2.3

Graphical solution of the diet model the feasible half-spaces of these two constraints requires using a reference point other than $\left( {0,0}\right)$ e.g., $\left( {{100},0}\right)$ or $\left( {0,{100}}\right) \rbrack$.

![bo_d56m43v7aajc73800n2g_6_459_1259_1040_933_0.jpg](bo_d56m43v7aajc73800n2g_6_459_1259_1040_933_0.jpg)

## Solution:

The model minimizes the value of the objective function by reducing $z$ in the direction shown in Figure 2.3. The optimum solution is the intersection of the two lines ${x}_{1} + {x}_{2} = {800}$ and ${.21}{x}_{1} - {.3}{x}_{2} = 0$ , which yields ${x}_{1} = {470.6}\mathrm{{lb}}$ and ${x}_{2} = {329.4}\mathrm{{lb}}$ . The minimum cost of the feed mix is $z = {.3} \times  {470.6} + {.9} \times  {329.4} = \$ {437.64}$ per day.

Remarks. One may wonder why the constraint ${x}_{1} + {x}_{2} \geq  {800}$ cannot be replaced with ${x}_{1} + {x}_{2} = {800}$ because it would not be optimum to produce more than the minimum quantity. Although the solution of the present model did satisfy the equation, a more complex model may impose additional restrictions that would require mixing more than the minimum amount. More importantly, the weak inequality (≥), by definition, implies the equality case, so that the equation $\left(  = \right)$ is permitted if optimality requires it. The conclusion is that one should not "preguess" the solution by imposing the additional equality restriction. ^weakineq

### 2.3 COMPUTER SOLUTION WITH SOLVER AND AMPL ^computer

In practice, where typical LP models may involve thousands of variables and constraints, the computer is the only viable venue for solving LP problems. This section presents two commonly used software systems: Excel Solver and AMPL. Solver is particularly appealing to spreadsheet users. AMPL is an algebraic modeling language that, like all higher-order programming languages, requires more expertise. Nevertheless, AMPL, and similar languages, ${}^{2}$ offers great modeling flexibility. Although the presentation in this section concentrates on LPs, both AMPL and Solver can handle integer and nonlinear problems, as will be shown in later chapters.

#### 2.3.1 LP Solution with Excel Solver ^solver

In Excel Solver, the spreadsheet is the input and output medium for the LP. Figure 2.4 shows the layout of the data for the Reddy Mikks model (file solverRM1.xls). The top of the figure includes four types of information: (1) input data cells (B5:C9 and F6:F9), (2) cells representing the variables and the objective function (B13:D13), (3) algebraic definitions of the objective function and the left-hand side of the constraints (cells D5:D9), and (4) cells that provide (optional) explanatory names or symbols. Solver requires the first three types only. The fourth type enhances readability but serves no other purpose. The relative positioning of the four types of information on the spreadsheet (as suggested in Figure 2.4) is convenient for proper cell cross-referencing in Solver, and its use is recommended.

---

${}^{2}$ Other known commercial packages include AIMMS, GAMS, LINGO, MPL, OPL Studio, and Xpress-Mosel.

---

![bo_d56m43v7aajc73800n2g_8_329_202_1307_1592_0.jpg](bo_d56m43v7aajc73800n2g_8_329_202_1307_1592_0.jpg)

FIGURE 2.4

Defining the Reddy Mikks model with Excel Solver (file solverRM1.xls)

How does Solver link to the spreadsheet data? First, we provide "algebraic" definitions of the objective function and the left-hand side of the constraints using the

input data (cells B5:C9 and F6:F9) and the objective function and variables (cells B13:D13). Next, we place the resulting formulas appropriately in cells D5:D9, as the following table shows:


|                | Algebraic expression  | Spreadsheet formula    | Entered in cell |
| -------------- | --------------------- | ---------------------- | --------------- |
| Objective, $z$ | $5{x}_{1} + 4{x}_{2}$ | =B5*\$B\$13+C5*\$C\$13 | D5              |
| Constraint 1   | $6{x}_{1} + 4{x}_{2}$ | =B6*\$B\$13+C6*\$C\$13 | D6              |
| Constraint 2   | ${x}_{1} + 2{x}_{2}$  | =B7*\$B\$13+C7*\$C\$13 | D7              |
| Constraint 3   | $- {x}_{1} + {x}_{2}$ | =B8*\$B\$13+C8*\$C\$13 | D8              |
| Constraint 4   | $0{x}_{1} + {x}_{2}$  | =B9*\$B\$13+C9*\$C\$13 | D9              |


Actually, you only need to enter the formula for cell D5 and then copy it into cells D6:D9. To do so correctly, it is necessary to use fixed referencing of the cells representing ${x}_{1}$ and ${x}_{2}$ (i.e., $\$ \mathrm{B}\$ {13}$ and $\$ \mathrm{C}\$ {13}$ , respectively).

The explicit formulas just described are impractical for large LPs. Instead, the formula in cell D5 can be written compactly as

$$
\text{ = SUMPRODUCT(B5:C5,\$B\$13:\$C\$13) }
$$

The new formula can then be copied into cells D6:D9.

All the elements of the LP model are now in place. To execute the model, click Solver from the spreadsheet menu bar ${}^{3}$ to access Solver Parameters dialogue box (shown in the middle of Figure 2.4). Next, update the dialogue box as follows:

Set Target Cell: \$D\$5

Equal To: $\odot$ Max

By Changing Cells: \$B\$13:\$C\$13

This information tells Solver that the LP variables (cells \$B\$13 and \$C\$13) are determined by maximizing the objective function in cell \$D\$5.

To set up the constraints, click Add in the dialogue box to display the Add Constraint box (bottom of Figure 2.4) and then enter the left-hand side, inequality type, and right-hand side of the constraints ${\mathrm{{as}}}^{4}$

$$
\text{ \$D\$6:\$D\$9 <= \$F\$6:\$F\$9 }
$$

For the nonnegativity restrictions, click Add once again and enter

$$
\text{ \$B\$13:\$C\$13 >= 0 }
$$

Another way to enter the nonnegative constraints is to click Options in the Solver Parameters box to access Solver Options (see Figure 2.5) and then check J Assume Non-Negative . Also, while in the same box, check J Assume Linear Model .

---

${}^{3}$ If Solver does not appear under Data menu (on Excel menu bar), click Excel Office Button $\rightarrow$ Excel Options $\rightarrow$ Add Ins $\rightarrow$ Solver Add-in $\rightarrow$ OK; then close and restart Excel.

${}^{4}$ In the Add Constraint box in Figure 2.4, the two additional options, int and bin, which stand for integer and binary, are used with integer programs to restrict variables to integer or binary values (see Chapter 9).

---

![bo_d56m43v7aajc73800n2g_10_400_199_783_673_0.jpg](bo_d56m43v7aajc73800n2g_10_400_199_783_673_0.jpg)

FIGURE 2.5

Solver options dialogue box

In general, the remaining default settings in Solver Options need not be changed. However, the default precision of .000001 may be too "high" for some problems, and Solver may incorrectly return the message "Solver could not find a feasible solution". In such cases, less precision (i.e., larger value) needs to be specified. If the message persists, then the problem may be infeasible.

Descriptive Excel range names can be used to enhance readability. A range is created by highlighting the desired cells, typing the range name in the top left box of the sheet, and then pressing Return. Figure 2.6 (file solverRM2.xls) provides the details with a summary of the range names used in the model. The model should be contrasted with the file solverRM1.xls to see how ranges are used in the formulas.

To solve the problem, click Solve on Solver Parameters. A new dialogue box, Solver Results, then gives the status of the solution. If the model setup is correct, the optimum value of $z$ will appear in cell D5 and the values of ${x}_{1}$ and ${x}_{2}$ will go to cells B13 and C13, respectively. For convenience, cell D13 exhibits the optimum value of $z$ by entering the formula $= \mathrm{D}5$ in cell D13, thus displaying the entire optimum solution in contiguous cells.

If a problem has no feasible solution, Solver will issue the explicit message "Solver could not find a feasible solution". If the optimal objective value is unbounded (not finite), Solver will issue the somewhat ambiguous message "The Set Cell values do not converge". In either case, the message indicates that there is something wrong with the formulation of the model, as will be discussed in Section 3.5.

The Solver Results dialogue box provides the opportunity to request further details about the solution, including the sensitivity analysis report. We will discuss these additional results in Section 3.6.4.

The solution of the Reddy Mikks by Solver is straightforward. Other models may require a "bit of ingenuity" before they can be set up. A class of LP models that falls in this category deals with network optimization, as will be demonstrated in Chapter 6.

![bo_d56m43v7aajc73800n2g_11_463_200_952_982_0.jpg](bo_d56m43v7aajc73800n2g_11_463_200_952_982_0.jpg)

FIGURE 2.6

Use of range names in Excel Solver (file solverRM2.xls)

#### 2.3.2 LP Solution with AMPL ${}^{5}$ ^ampl

This section provides a brief introduction to AMPL. The material in Appendix C on the website details AMPL syntax. It will be cross-referenced with the presentation in this section and with other AMPL presentations in the book. The two examples presented here deal with the basics of AMPL.

Reddy Mikks Problem-A Rudimentary Model. AMPL provides a facility for modeling an LP in a rudimentary longhand format. Figure 2.7 gives the self-explanatory code for the Reddy Mikks model (file amplRM1.txt). All reserved keywords are in bold. All other names are user generated. The objective function and each of the constraints must have distinct (user-generated) names followed by a colon. Each statement closes with a semicolon. ^longhand

The longhand format is problem-specific, in the sense that a new code is needed whenever the input data are changed. For practical problems (with complex structure and a large number of variables and constraints), the longhand format is at best cumbersome. AMPL alleviates this difficulty by devising a code that divides the problem into two components: (1) a general algebraic model for a specific class of problems ^modeldata

---

${}^{5}$ For convenience, the AMPL student version is on the website. Future updates may be downloaded from www.ampl.com. AMPL uses line commands and does not operate in Windows environment.

---

---

maximize z: 5*x1+4*x2; 												FIGURE 2.7

subject to 											Rudimentary AMPL model for

	c1: 6*x1+4*x2<=24; 											the Reddy Mikks problem (file

	c2: x1+2*x2<=6; 											amplRM1.txt)

	c3: -x1+x2<=1;

	c4: x2<=2;

solve;

display z, x1, x2;

---

applicable to any number of variables and constraints, and (2) data for driving the algebraic model. The implementation of these two points is addressed in the following section using the Reddy Mikks problem.

Reddy Mikks Problem-An Algebraic Model. Figure 2.8 lists the statements of the model (file amplRM2.txt). The file must be strictly text (ASCII). The symbol # designates the start of explanatory comments. Comments may appear either on a separate line or following the semicolon at the end of a statement. The language is case sensitive, and all of its keywords, with few exceptions, are in lower case. (Section C.2 provides more details.)

The algebraic model in AMPL views the general LP problem with $n$ variables and $m$ constraints in the following generic format (restr is a user-generated name):

$$
\text{ Maximize }z : \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j}
$$

$$
\text{ subject to rest }{r}_{i} : \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  {b}_{i}, i = 1,2,\ldots , m
$$

$$
{x}_{j} \geq  0, j = 1,2,\ldots , n
$$

It gives the objective function and constraint $i$ the (user-specified) names $z$ and restr ${i}_{i}$ .

The model starts with the param statements that declare $m, n, c, b$ , and ${a}_{ij}$ as parameters (or constants) whose specific values are given in the input data section of the model. It translates ${c}_{j}\left( {j = 1,2,\ldots , n}\right)$ as $c\{ 1\ldots \mathrm{n}\} ,{b}_{i}\left( {i = 1,2,\ldots , m}\right)$ as b\{1..m\}, and ${a}_{ij}\left( {i = 1,2,\ldots , m, j = 1,2,\ldots , n}\right)$ as a\{1..m,1..n\}. Next, the variables ${x}_{j}\left( {j = 1,2,\ldots , n}\right)$ together with the nonnegativity restriction are defined by the var statement

---

var x\{1..n\}>=0;

---

A variable is considered unrestricted if $>  = 0$ is removed from its definition. The notation in \{\} represents the set of subscripts over which a param or a var is defined.

The model is developed in terms of the parameters and the variables in the following manner. The objective function and constraints carry distinct names followed by a colon (:). The objective statement is a direct translation of maximize $z = \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j}$ :

---

maximize $z$ : sum\{j in 1..n\}c[j]*x[j];

---

Constraint $i$ is given the (arbitrary) root name restr indexed over the set $\{ 1$ . . . . $\}$ :

58 Chapter 2 Modeling with Linear Programming

algebraic model

---

param m;

param n;

param c\{1..n\};

param b\{1..m\};

param a\{1..m,1..n\};

var x\{1..n\}==0;

maximize z: sum\{j in 1..n\}c[j]*x[j];

subject to restr\{i in 1..m\}:

			sum\{j in 1..n\}a[i, j]*x[j]<=b[i];

#----------------------------------------------------specify model data

data;

param n:=2;

param m:=4;

param c:=1 5 2 4;

param b:=1 24 2 6 3 1 4 2;

param a: 1 2 :=

		1 6 4

		2 1 2

		3 -1 1

		4 0 1 ;

												-solve the problem

solve;

display z, x;

FIGURE 2.8

AMPL model of the Reddy Mikks problem using hard-coded input data (file amplRM2.txt)

---

The statement is a direct translation of rest ${r}_{i}\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} \leq  {b}_{i}$ .

The algebraic model may now be used with any set of applicable data that can be entered following the statement data;. For the Reddy Mikks model, the data tells AMPL that the problem has two variables (param n:=2; ) and four constraints (param m:=4;). The compound operator := must be used, and the statement must start with the keyword param. For the single-subscripted parameters, $c$ and $b$ , each element is represented by its index followed by its value and separated by at least one blank space. Thus, ${c}_{1} = 5$ and ${c}_{2} = 4$ are entered as

---

param c:= 1 5 2 4;

---

The data for param $b$ is entered in a similar manner.

For the double-subscripted parameter ${a}_{ij}$ , that data set reads as a two-dimensional matrix with its rows designating $i$ and its columns designating $j$ . The top line defines the subscript $j$ , and the subscript $i$ is entered at the start of each row as

---

param a: $1\;2 \mathrel{\text{ := }}$

	1 6 4

	2 1 2

	3 -1 1

	4 0 1 ;

---

The data set must terminate with a semicolon. Note the mandatory location of the separator : and the compound operator := after param a.

The model and its data are now ready. The command solve; invokes the solution algorithm and the command display $z, x;$ provides the solution.

To execute the model, first invoke AMPL (by clicking ampl.exe in the AMPL directory). At the ampl : prompt, enter the following model command, and then press Return:

---

model amplRM2.txt;

---

The output of the system will then appear on the screen as follows:

---

MINOS 5.5: Optimal solution found.

2 iterations, objective = 21

z = 21

x[*]:=

	1 = 3

	2 = 1.5

---

The bottom four lines are the result of executing display z, x;. Actually, AMPL has formatting capabilities that enhance the readability of the output results (see Section C.5.2).

AMPL allows separating the algebraic model and the data into two independent files. This arrangement is more convenient because only the data file needs to be changed once the model has been developed. See the end of Section C.2 for details.

AMPL offers a wide range of programming capabilities. For example, the input/ output data can be secured from/sent to external files, spreadsheets, and databases, and the model can be executed interactively for a wide variety of options. The details are given in Appendix C on the website.

### 2.4 LINEAR PROGRAMMING APPLICATIONS ^applications

This section presents realistic LP models in which the definition of the variables and the construction of the objective function and the constraints are not as straightforward as in the case of the two-variable model. The areas covered by these applications include the following:

1. Investment.

2. Production planning and inventory control.

3. Workforce planning.

4. Urban development planning.

5. Oil refining and blending.

Each model is detailed, and its optimum solution is interpreted.

#### 2.4.1 Investment ^investment

Multitudes of investment opportunities are available to today's investor. Examples of investment problems are capital budgeting for projects, bond investment strategy, stock portfolio selection, and establishment of bank loan policy. In many of these situations, LP can be used to select the optimal mix of opportunities that will maximize return while meeting requirements set by the investor and the market.

## Example 2.4-1 (Bank Loan Model) ^bankloan

Bank One is in the process of devising a loan policy that involves a maximum of \$12 million. The following table provides the pertinent data about available loans.


| Type of loan | Interest rate | Bad-debt ratio |
| --- | --- | --- |
| Personal | .140 | .10 |
| Car | .130 | .07 |
| Home | .120 | .03 |
| Farm | .125 | .05 |
| Commercial | .100 | .02 |


Bad debts are unrecoverable and produce no interest revenue.

Competition with other financial institutions dictates the allocation of at least 40% of the funds to farm and commercial loans. To assist the housing industry in the region, home loans must equal at least 50% of the personal, car, and home loans. The bank limits the overall ratio of bad debts on all loans to at most 4%.

Mathematical Model: The situation deals with determining the amount of loan in each category, thus leading to the following definitions of the variables:

$$
{x}_{1} = \text{ personal loans (in millions of dollars) }
$$

$$
{x}_{2} = \text{ car loans }
$$

$$
{x}_{3} = \text{ home loans }
$$

$$
{x}_{4} = \text{ farm loans }
$$

$$
{x}_{5} = \text{ commercial loans }
$$

The objective of the Bank One is to maximize net return, the difference between interest revenue and lost bad debts. Interest revenue is accrued on loans in good standing. For example, when 10% of personal loans are lost to bad debt, the bank will receive interest on 90% of the loan-that

is, it will receive ${14}\%$ interest on ${.9}{x}_{1}$ of the original loan ${x}_{1}$ . The same reasoning applies to the remaining four types of loans. Thus,

$$
\text{ Total interest } = {.14}\left( {{.9}{x}_{1}}\right)  + {.13}\left( {{.93}{x}_{2}}\right)  + {.12}\left( {{.97}{x}_{3}}\right)  + {.125}\left( {{.95}{x}_{4}}\right)  + {.1}\left( {{.98}{x}_{5}}\right)
$$

$$
= {.126}{x}_{1} + {.1209}{x}_{2} + {.1164}{x}_{3} + {.11875}{x}_{4} + {.098}{x}_{5}
$$

We also have

$$
\text{ Bad debt } = {.1}{x}_{1} + {.07}{x}_{2} + {.03}{x}_{3} + {.05}{x}_{4} + {.02}{x}_{5}
$$

The objective function combines interest revenue and bad debt as:

$$
\text{ Maximize }z = \text{ Total interest } - \text{ Bad debt } ^bankobj
$$

$$
= \left( {{.126}{x}_{1} + {.1209}{x}_{2} + {.1164}{x}_{3} + {.11875}{x}_{4} + {.098}{x}_{5}}\right)
$$

$$
- \left( {{.1}{x}_{1} + {.07}{x}_{2} + {.03}{x}_{3} + {.05}{x}_{4} + {.02}{x}_{5}}\right)
$$

$$
= {.026}{x}_{1} + {.0509}{x}_{2} + {.0864}{x}_{3} + {.06875}{x}_{4} + {.078}{x}_{5}
$$

The problem has five constraints: ^bankconst

1. Total funds should not exceed \$12 (million):

$$
{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5} \leq  {12}
$$

2. Farm and commercial loans equal at least 40% of all loans:

$$
{x}_{4} + {x}_{5} \geq  {.4}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5}}\right)
$$

or

$$
{.4}{x}_{1} + {.4}{x}_{2} + {.4}{x}_{3} - {.6}{x}_{4} - {.6}{x}_{5} \leq  0
$$

3. Home loans should equal at least 50% of personal, car, and home loans:

$$
{x}_{3} \geq  {.5}\left( {{x}_{1} + {x}_{2} + {x}_{3}}\right)
$$

or

$$
{.5}{x}_{1} + {.5}{x}_{2} - {.5}{x}_{3} \leq  0
$$

4. Bad debts should not exceed 4% of all loans:

$$
{.1}{x}_{1} + {.07}{x}_{2} + {.03}{x}_{3} + {.05}{x}_{4} + {.02}{x}_{5} \leq  {.04}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5}}\right)
$$

or

$$
{.06}{x}_{1} + {.03}{x}_{2} - {.01}{x}_{3} + {.01}{x}_{4} - {.02}{x}_{5} \leq  0
$$

5. Nonnegativity:

$$
{x}_{1} \geq  0,{x}_{2} \geq  0,{x}_{3} \geq  0,{x}_{4} \geq  0,{x}_{5} \geq  0
$$

A subtle assumption in the preceding formulation is that all loans are issued at approximately the same time. This allows us to ignore differences in the time value of the funds allocated to the different loans.

## Solution:

The optimal solution is computed using AMPL (file amplEx2.4-1.txt):

$$
z = {.99648},{x}_{1} = 0,{x}_{2} = 0,{x}_{3} = {7.2},{x}_{4} = 0,{x}_{5} = {4.8}
$$

## Remarks.

1. You may be wondering why we did not define the right-hand side of the second constraint as ${.4} \times  {12}$ instead of ${.4}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5}}\right)$ . After all, it appears plausible that the bank would want to loan out all \$12 million. The answer is that the usage given in the formulation does not disallow this possibility. But there are two more reasons why you should not use ${.4} \times  {12}$ : (1) If other constraints in the model are such that all \$12 million cannot be used (e.g., the bank may set caps on the different loans), then the choice .4 × 12 could lead to an infeasible or incorrect solution. (2) If you want to experiment with the effect of changing available funds (say from \$12 to \$13 million) on the optimum solution, there is a real chance that you may forget to change ${.4} \times  {12}$ to ${.4} \times  {13}$ , in which case the solution will not be correct. A similar reasoning applies to the left-hand side of the fourth constraint.

2. The optimal solution calls for allocating all \$12 million: \$7.2 million to home loans and \$4.8 million to commercial loans. The remaining categories receive none. The return on the investment is

$$
\text{ Rate of return } = \frac{z}{12} = \frac{.99648}{12} = {.08034}
$$

This shows that the combined annual rate of return is 8.034%, which is less than the best net interest rate (= 8.64% for home loans), and one wonders why the model does not take full advantage of this opportunity. The answer is that the stipulation that farm and commercial loans must account for at least 40% of all loans (constraint 2) forces the solution to allocate $\$ {4.8}$ million to commercial loans at the lower net rate of ${7.8}\%$ , hence lowering the overall interest rate to ${100}\left( \frac{{.0864} \times  {7.2} + {.078} \times  {4.8}}{12}\right)  = {8.034}\%$ . In fact, if we remove constraint 2, the optimum will allocate all the funds to home loans at the higher 8.64% rate (try it using the AMPL model!).

#### 2.4.2 Production Planning and Inventory Control ^production

There is a wealth of LP applications in the area of production planning and inventory control. This section presents three examples. The first deals with production scheduling to meet a single-period demand. The second deals with the use of inventory in a multiperiod production system to meet future demand, and the third deals with the use of inventory and worker hiring/firing to "smooth" production over a multiperiod planning horizon.

## Example 2.4-2 (Single-Period Production Model) ^singleperiod

In preparation for the winter season, a clothing company is manufacturing parka and goose overcoats, insulated pants, and gloves. All products are manufactured in four different departments: cutting, insulating, sewing, and packaging. The company has received firm orders for its products. The contract stipulates a penalty for undelivered items. Devise an optimal production plan for the company based on the following data:


| Department | Time per unit (hr) - Parka | Goose | Pants | Gloves | Capacity (hr) |
| --- | --- | --- | --- | --- | --- |
| Cutting | .30 | .30 | .25 | .15 | 1000 |
| Insulating | .25 | .35 | .30 | .10 | 1000 |
| Sewing | .45 | .50 | .40 | .22 | 1000 |
| Packaging | .15 | .15 | .1 | .05 | 1000 |
| Demand | 800 | 750 | 600 | 500 |  |
| Unit profit | \$30 | \$40 | \$20 | \$10 |  |
| Unit penalty | \$15 | \$20 | \$10 | \$8 |  |


Mathematical Model: The variables of the problem are as follows:

$$
{x}_{1} = \text{ number of parka jackets }
$$

$$
{x}_{2} = \text{ number of goose jackets }
$$

$$
{x}_{3} = \text{ number of pairs of pants }
$$

$$
{x}_{4} = \text{ number of pairs of gloves }
$$

The company is penalized for not meeting demand. The objective then is to maximize net profit, defined as

$$
\text{ Net profit } = \text{ Total profit - Total penalty } ^singleobj
$$

The total profit is ${30}{x}_{1} + {40}{x}_{2} + {20}{x}_{3} + {10}{x}_{4}$ . To compute the total penalty, the demand constraints can be written as

$$
{x}_{1} + {s}_{1} = {800},{x}_{2} + {s}_{2} = {750},{x}_{3} + {s}_{3} = {600},{x}_{4} + {s}_{4} = {500},
$$

$$
{x}_{j} \geq  0,{s}_{j} \geq  0, j = 1,2,3,4
$$

The new variable ${s}_{j}$ represents the shortage in demand for product $j$ , and the total penalty can be computed as ${15}{s}_{1} + {20}{s}_{2} + {10}{s}_{3} + 8{s}_{4}$ . The complete model thus becomes

$$
\text{ Maximize }z = {30}{x}_{1} + {40}{x}_{2} + {20}{x}_{3} + {10}{x}_{4} - \left( {{15}{s}_{1} + {20}{s}_{2} + {10}{s}_{3} + 8{s}_{4}}\right)
$$

subject to

$$
{.30}{x}_{1} + {.30}{x}_{2} + {.25}{x}_{3} + {.15}{x}_{4} \leq  {1000}
$$

$$
{.25}{x}_{1} + {.35}{x}_{2} + {.30}{x}_{3} + {.10}{x}_{4} \leq  {1000}
$$

$$
{.45}{x}_{1} + {.50}{x}_{2} + {.40}{x}_{3} + {.22}{x}_{4} \leq  {1000}
$$

$$
{.15}{x}_{1} + {.15}{x}_{2} + {.10}{x}_{3} + {.05}{x}_{4} \leq  {1000}
$$

$$
{x}_{1} + {s}_{1} = {800},{x}_{2} + {s}_{2} = {750},{x}_{3} + {s}_{3} = {600},{x}_{4} + {s}_{4} = {500}
$$

$$
{x}_{j} \geq  0,{s}_{j} \geq  0, j = 1,2,3,4
$$

## Solution:

The optimum solution (obtained using file amplEx2.4-2.txt) is $z = \$ {64},{625},{x}_{1} = {800},{x}_{2} = {750}$ , ${x}_{3} = {387.5},{x}_{4} = {500},{s}_{1} = {s}_{2} = {s}_{4} = 0,{s}_{3} = {212.5}$ . The solution satisfies all the demand for both types of jackets and the gloves. A shortage of 213 (rounded up from 212.5) pairs of pants will result in a penalty cost of ${213} \times  \$ {10} = \$ {2130}$ .

## Example 2.4-3 (Multiple Period Production-Inventory Model) ^multiperiod

Acme Manufacturing Company has a contract to deliver 100, 250, 190, 140, 220, and 110 home windows over the next 6 months. Production cost (labor, material, and utilities) per window varies by period and is estimated to be \$50, \$45, \$55, \$48, \$52, and \$50 over the next 6 months. To take advantage of the fluctuations in manufacturing cost, Acme can produce more windows than needed in a given month and hold the extra units for delivery in later months. This will incur a storage cost at the rate of $\$ 8$ per window per month, assessed on end-of-month inventory. Develop a linear program to determine the optimum production schedule.

Mathematical Model: The variables of the problem include the monthly production amount and the end-of-month inventory. For $i = 1,2,\ldots ,6$ , let

$$
{x}_{i} = \text{ Number of units produced in month }i
$$

$$
{I}_{i} = \text{ Inventory units left at the end of month }i
$$

The relationship between these variables and the monthly demand over the 6-month horizon is represented schematically in Figure 2.9. The system starts empty $\left( {{I}_{0} = 0}\right)$ .

The objective is to minimize the total cost of production and end-of-month inventory.

$$
\text{ Total production cost } = {50}{x}_{1} + {45}{x}_{2} + {55}{x}_{3} + {48}{x}_{4} + {52}{x}_{5} + {50}{x}_{6}
$$

$$
\text{ Total inventory (storage) cost } = 8\left( {{I}_{1} + {I}_{2} + {I}_{3} + {I}_{4} + {I}_{5} + {I}_{6}}\right)
$$

Thus the objective function is

$$
\text{ Minimize }z = {50}{x}_{1} + {45}{x}_{2} + {55}{x}_{3} + {48}{x}_{4} + {52}{x}_{5} + {50}{x}_{6} + 8\left( {{I}_{1} + {I}_{2} + {I}_{3} + {I}_{4} + {I}_{5} + {I}_{6}}\right)
$$

The constraints of the problem can be determined directly from the representation in Figure 2.9. For each period we have the following balance equation:

Beginning inventory + Production amount - Ending inventory = Demand ^inventorybal

This is translated mathematically for the individual months as

$$
{x}_{1} - {I}_{1} = {100}\;\left( {\text{ Month }1}\right)
$$

$$
{I}_{1} + {x}_{2} - {I}_{2} = {250}\;\left( {\text{ Month }2}\right)
$$

$$
{I}_{2} + {x}_{3} - {I}_{3} = {190}\;\text{ (Month 3) }
$$

$$
{I}_{3} + {x}_{4} - {I}_{4} = {140}\;\text{ (Month 4) }
$$

$$
{I}_{4} + {x}_{5} - {I}_{5} = {220}\text{ (Month 5) }
$$

$$
{I}_{5} + {x}_{6} = {110}\text{ (Month 6) }
$$

$$
{x}_{i}, i = 1,2,\ldots ,6,{I}_{i} \geq  0, i = 1,2,\ldots ,5
$$

FIGURE 2.9

Schematic representation of the production-inventory system

![bo_d56m43v7aajc73800n2g_19_335_1940_1200_264_0.jpg](bo_d56m43v7aajc73800n2g_19_335_1940_1200_264_0.jpg)

![bo_d56m43v7aajc73800n2g_20_381_196_1191_274_0.jpg](bo_d56m43v7aajc73800n2g_20_381_196_1191_274_0.jpg)

FIGURE 2.10

Optimum solution of the production-inventory problem

Note that the initial inventory, ${I}_{0}$ , is zero. Also, in any optimal solution, the ending inventory ${I}_{6}$ will be zero because it is not economical to incur unnecessary additional storage cost.

## Solution:

The optimum solution (obtained using file amplEx2.4-3.txt) is summarized in Figure 2.10. It shows that each month's demand is satisfied from the same month's production, except for month 2, where the production quantity (=440units) covers the demand for both months 2 and 3 . The total associated cost is $z = \$ {49},{980}$ .

## Example 2.4-4 (Multiperiod Production Smoothing Model) ^smoothing

A company is planning the manufacture of a product for March, April, May, and June of next year. The demand quantities are 520, 720, 520, and 620 units, respectively. The company has a steady workforce of 10 employees but can meet fluctuating production needs by hiring and firing temporary workers. The extra costs of hiring and firing a temp in any month are \$200 and \$400, respectively. A permanent worker produces 12 units per month, and a temporary worker, lacking equal experience, produces 10 units per month. The company can produce more than needed in any month and carry the surplus over to a succeeding month at a holding cost of \$50 per unit per month. Develop an optimal hiring/firing policy over the 4-month planning horizon.

Mathematical Model: This model is similar to that of Example 2.4-3 in the sense that each month has its production, demand, and ending inventory. The only exception deals with handling a permanent versus temporary workforce.

The permanent workers (10 in all) can be accounted for by subtracting the units they produce from the respective monthly demand. The remaining demand is then satisfied through the hiring and firing of temps. Thus,

Remaining demand for March $= {520} - {12} \times  {10} = {400}$ units

Remaining demand for April $= {720} - {12} \times  {10} = {600}$ units

Remaining demand for May $= {520} - {12} \times  {10} = {400}$ units

Remaining demand for June $= {620} - {12} \times  {10} = {500}$ units

The variables of the model for month $i$ can be defined as

${x}_{i} =$ Net number of temps at the start of month $i$ after any hiring or firing

${S}_{i} =$ Number of temps hired or fired at the start of month $i$

${I}_{i} =$ Units of ending inventory for month $i$

By definition, ${x}_{i}$ and ${I}_{i}$ are nonnegative, whereas ${S}_{i}$ is unrestricted in sign because it equals the number of hired or fired workers in month $i$ . This is the first instance in this chapter of using an unrestricted variable. As we will see shortly, special substitution is needed to allow the implementation of hiring and firing in the model.

In this model, the development of the objective function requires constructing the constraints first. The number of units produced in month $i$ by ${x}_{i}$ temps is ${10}{x}_{i}$ . Thus, we have the following inventory constraints:

$$
{10}{x}_{1} = {400} + {I}_{1}\;\left( \text{ March }\right)
$$

$$
{I}_{1} + {10}{x}_{2} = {600} + {I}_{2}\;\text{ (April) }
$$

$$
{I}_{2} + {10}{x}_{3} = {400} + {I}_{3}\;\text{ (May) }
$$

$$
{I}_{3} + {10}{x}_{4} = {500}\;\text{ (June) }
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0,{I}_{1},{I}_{2},{I}_{3} \geq  0
$$

For hiring and firing, the temp workforce starts with ${x}_{1}$ workers at the beginning of March. At the start of April, ${x}_{1}$ will be adjusted (up or down) by ${S}_{2}$ temps to generate ${x}_{2}$ . The same idea applies to ${x}_{3}$ and ${x}_{4}$ , thus leading to the following constraint equations:

$$
{x}_{1} = {S}_{1}
$$

$$
{x}_{2} = {x}_{1} + {S}_{2}
$$

$$
{x}_{3} = {x}_{2} + {S}_{3}
$$

$$
{x}_{4} = {x}_{3} + {S}_{4}
$$

$$
{S}_{1},{S}_{2},{S}_{3},{S}_{4}\text{ unrestricted in sign }
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

Next, we develop the objective function. The goal is to minimize the inventory cost plus the cost of hiring and firing. As in Example 2.4-3,

$$
\text{ Inventory holding cost } = {50}\left( {{I}_{1} + {I}_{2} + {I}_{3}}\right)
$$

Modeling the cost of hiring and firing is a bit involved. Given the costs of hiring and firing a temp are \$200 and \$400, respectively, we have ^hiringfiring

$$
\left( \begin{matrix} \text{ Cost of hiring } \\  \text{ and firing } \end{matrix}\right)  = {200}\left( \begin{matrix} \text{ Number of hired temps } \\  \text{ at the start of each month } \end{matrix}\right)  + {400}\left( \begin{matrix} \text{ Number of fired temps } \\  \text{ at the start of each month } \end{matrix}\right)
$$

If the variable ${S}_{i}$ is positive, hiring takes place in month $i$ . If it is negative, then firing occurs. This "qualitative" assessment can be translated mathematically by using the substitution ^substitution

$$
{S}_{i} = {S}_{i}^{ - } - {S}_{i}^{ + }\text{ , where }{S}_{i}^{ - },{S}_{i}^{ + } \geq  0
$$

The unrestricted variable ${S}_{i}$ is now the difference between the two nonnegative variables ${S}_{i}^{ - }$ and ${S}_{i}^{ + }$ . We can think of ${S}_{i}^{ - }$ as the number of temps hired and ${S}_{i}^{ + }$ as the number fired. For example, if ${S}_{i}^{ - } = 5$ and ${S}_{i}^{ + } = 0$ , then ${S}_{i} = 5 - 0 =  + 5$ , which represents hiring. If ${S}_{i}^{ - } = 0$ and ${S}_{i}^{ + } = 7$ , then ${S}_{i} = 0 - 7 =  - 7$ , which represents firing. In the first case, the corresponding cost of hiring is ${200}{S}_{i}^{ - } = {200} \times  5 = \$ {1000}$ , and in the second case, the corresponding cost of firing is ${400}{S}_{i}^{ + } = {400} \times  7 = \$ {2800}$ .

The substitution ${S}_{i} = {S}_{i}^{ - } - {S}_{i}^{ + }$ is the basis for the development of cost of hiring and firing. First we need to address a possible question: What if both ${S}_{i}^{ - }$ and ${S}_{i}^{ + }$ are positive? The answer is that this cannot happen because it implies both hiring and firing in the same month. Interestingly, the theory of LP (see Chapter 7) tells us that ${S}_{i}^{ - }$ and ${S}_{i}^{ + }$ cannot be positive simultaneously, a mathematical result that confirms intuition.

We can now write the total cost of hiring and firing as

$$
\text{ Cost of hiring } = {200}\left( {{S}_{1}^{ - } + {S}_{2}^{ - } + {S}_{3}^{ - } + {S}_{4}^{ - }}\right)
$$

$$
\text{ Cost of firing } = {400}\left( {{S}_{1}^{ + } + {S}_{2}^{ + } + {S}_{3}^{ + } + {S}_{4}^{ + }}\right)
$$

It may appear necessary to add to $z$ the amount ${400}{x}_{4}$ representing the cost of end-of-horizon-firing of ${x}_{4}$ temps. From the standpoint of optimization, this factor is accounted for by the presence of ${S}_{4}^{ + }$ in the objective function. Hence the optimum will not change, except for inflating optimum $z$ by ${400}{x}_{4}$ (try it!).

The complete model is as follows:

$$
\text{ Minimize }z = {50}\left( {{I}_{1} + {I}_{2} + {I}_{3}}\right)  + {200}\left( {{S}_{1}^{ - } + {S}_{2}^{ - } + {S}_{3}^{ - } + {S}_{4}^{ - }}\right)  + {400}\left( {{S}_{1}^{ + } + {S}_{2}^{ + } + {S}_{3}^{ + } + {S}_{4}^{ + }}\right)
$$

subject to

$$
{10}{x}_{1} = {400} + {I}_{1}
$$

$$
{I}_{1} + {10}{x}_{2} = {600} + {I}_{2}
$$

$$
{I}_{2} + {10}{x}_{3} = {400} + {I}_{3}
$$

$$
{I}_{3} + {10}{x}_{4} = {500}
$$

$$
{x}_{1} = {S}_{1}^{ - } - {S}_{1}^{ + }
$$

$$
{x}_{2} = {x}_{1} + {S}_{2}^{ - } - {S}_{2}^{ + }
$$

$$
{x}_{3} = {x}_{2} + {S}_{3}^{ - } - {S}_{3}^{ + }
$$

$$
{x}_{4} = {x}_{3} + {S}_{4}^{ - } - {S}_{4}^{ + }
$$

$$
{S}_{1}^{ - },{S}_{1}^{ + }{S}_{2}^{ - },{S}_{2}^{ + },{S}_{3}^{ - },{S}_{3}^{ + },{S}_{4}^{ - },{S}_{4}^{ + } \geq  0
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

$$
{I}_{1},{I}_{2},{I}_{3} \geq  0
$$

## Solution:

The optimum solution (obtained using file amplEx2.4-4.txt) is $z = \$ {19},{500},{x}_{1} = {50},{x}_{2} = {50}$ , ${x}_{2} = {50},{x}_{3} = {45},{x}_{4} = {45},{S}_{1}^{ - } = {50},{S}_{3}^{ + } = 5,{I}_{1} = {100},{I}_{3} = {50}$ . All the remaining variables are zero. The solution calls for hiring 50 temps in March $\left( {{S}_{1}^{ - } = {50}}\right)$ and holding the workforce steady till May when five temps are fired $\left( {{S}_{3}^{ + } = 5}\right)$ . No further hiring or firing is recommended until the end of June, when, presumably, all temps are terminated. This solution requires 100 units of inventory to be carried into May and 50 units to be carried into June.

#### 2.4.3 Workforce Planning ^workforce

## Real-Life Application-Telephone Sales Workforce Planning at Qantas Airways ^qantas

Australian airline Qantas operates its main reservation offices from 7:00 till 22:00 using six shifts that start at different times of the day. Qantas used LP (with imbedded queuing analysis) to staff its main telephone sales reservation office efficiently while providing convenient service to its customers. The study, carried out in the late 1970s, resulted in annual savings of over 200,000 Australian dollars per year. The study is detailed in Case 15, Chapter 26, on the website.

Fluctuations in a labor force to meet variable demand over time can be achieved through the process of hiring and firing, as demonstrated in Example 2.4-4. There are situations in which the effect of fluctuations in demand can be "absorbed" by adjusting the start and end times of a work shift. For example, instead of following the traditional three 8-hr-shift start times at 8:00 A.M., 3:00 P.M., and 11:00 P.M., we can use overlapping 8-hr shifts in which the start time of each is made in response to increase or decrease in demand.

The idea of redefining the start of a shift to accommodate fluctuation in demand can be extended to other operating environments as well. Example 2.4-5 deals with the determination of the minimum number of buses needed to meet rush-hour and off-hour transportation needs.

## Example 2.4-5 (Bus Scheduling Model) ^busscheduling

Progress City is studying the feasibility of introducing a mass-transit bus system to reduce in-city driving. The study seeks the minimum number of buses that can handle the transportation needs. After gathering necessary information, the city engineer noticed that the minimum number of buses needed fluctuated with time of the day, and that the required number of buses could be approximated by constant values over successive 4-hr intervals. Figure 2.11 summarizes the engineer's findings. To carry out the required daily maintenance, each bus can operate only 8 successive hours a day.

Mathematical Model: The variables of the model are the number of buses needed in each shift, and the constraints deal with satisfying demand. The objective is to minimize the number of buses in operation.

The stated definition of the variables is somewhat "vague." We know that each bus will run for 8 consecutive hours, but we do not know when a shift should start. If we follow a normal three-shift schedule (8:01 a.m. to 4:00 p.m., 4:01 p.m. to 12:00 midnight, and 12:01 a.m. to 8:00 a.m.) and assume that ${x}_{1},{x}_{2}$ , and ${x}_{3}$ are the number of buses starting in the first, second, and third shifts, we can see in Figure 2.11 that ${x}_{1} \geq  {10},{x}_{2} \geq  {12}$ , and ${x}_{3} \geq  8$ . The corresponding minimum number of daily buses is ${x}_{1} + {x}_{2} + {x}_{3} = {10} + {12} + 8 = {30}$ .

The given solution is acceptable only if the shifts must coincide with the normal three-shift schedule. However, it may be advantageous to allow the optimization process to choose the "best" starting time for a shift. A reasonable way to accomplish this goal is to allow a shift to start every $4\mathrm{{hr}}$ . The bottom of Figure 2.11 illustrates this idea with overlapping 8-hr shifts starting at 12:01 a.m., 4:01 a.m., 8:01 a.m., 12:01 p.m., 4:01 p.m., and 8:01 p.m. Thus, the variables are defined as ^overlapping

$$
{x}_{1} = \text{ number of buses starting at 12:01 A.M. }
$$

$$
{x}_{2} = \text{ number of buses starting at 4:01 A.M. }
$$

$$
{x}_{3} = \text{ number of buses starting at 8:01 A.M. }
$$

$$
{x}_{4} = \text{ number of buses starting at 12:01 P.M. }
$$

$$
{x}_{5} = \text{ number of buses starting at 4:01 P.M. }
$$

$$
{x}_{6} = \text{ number of buses starting at 8:01 P.M. }
$$

![bo_d56m43v7aajc73800n2g_24_429_197_1101_896_0.jpg](bo_d56m43v7aajc73800n2g_24_429_197_1101_896_0.jpg)

FIGURE 2.11

Number of buses as a function of the time of the day

We can see from Figure 2.11 that because of the overlapping of the shifts, the number of buses for the successive 4-hr periods can be computed as follows:


| Time period | Number of buses in operation |
| --- | --- |
| 12:01 A.M. to 4:00 A.M. | ${x}_{1} + {x}_{6}$ |
| 4:01 A.M. to 8:00 A.M. | ${x}_{1} + {x}_{2}$ |
| 8:01 A.M. to 12:00 noon | ${x}_{2} + {x}_{3}$ |
| 12:01 P.M. to 4:00 P.M. | ${x}_{3} + {x}_{4}$ |
| 4:01 P.M. to 8:00 P.M. | ${x}_{4} + {x}_{5}$ |
| 8:01 A.M. to 12:00 A.M. | ${x}_{5} + {x}_{6}$ |


The complete model thus becomes

$$
\text{ Minimize }z = {x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5} + {x}_{6}
$$

subject to

$$
{x}_{1}\; + {x}_{6} \cong  4\left( {{12} : {01}\text{ A.M. } - 4 : {00}\text{ A.M. }}\right)
$$

$$
{x}_{1} + {x}_{2}\; \geq  \;8\left( {4 : {01}\text{ A.M. } - 8 : {00}\text{ A.M. }}\right)
$$

$$
{x}_{2} + {x}_{3}\; \geq  {10}\left( {8 : {01}\text{ A.M. } - {12} : {00}\text{ noon }}\right)
$$

$$
{x}_{3} + {x}_{4}\; \geq  \;7\left( {{12} : {01}\text{ P.M. } - 4 : {00}\text{ P.M. }}\right)
$$

$$
{x}_{4} + {x}_{5}\; \geq  {12}\left( {4 : {01}\text{ P.M. } - 8 : {00}\text{ P.M. }}\right)
$$

$$
{x}_{5} + {x}_{6} \geq  4\left( {8 : {01}\text{ P.M. } - {12} : {00}\text{ P.M. }}\right)
$$

$$
{x}_{j} \geq  0, j = 1,2,\ldots ,6
$$

## Solution:

The optimal solution (obtained using file amplEx2.4-5.txt, solverEx2.4-5.xls, or toraEx2.4-5.txt) calls for scheduling 26 buses (compared with 30 buses when the three traditional shifts are used). The schedule calls for ${x}_{1} = 4$ buses to start at 12:01 A.M., ${x}_{2} = {10}$ at 4:01 A.M., ${x}_{4} = 8$ at 12:01 P.M., and ${x}_{5} = 4$ at 4:01 P.M. (Note: File solverEx2.4-5.xls yields the alternative optimum ${x}_{1} = 2,{x}_{2} = 6,{x}_{3} = 4,{x}_{4} = 6,{x}_{5} = 6$ , and ${x}_{6} = 2$ , with $z = {26}$ .)

#### 2.4.4 Urban Development Planning ${}^{6}$ ^urban

Urban planning deals with three general areas: (1) building new housing developments, (2) upgrading inner-city deteriorating housing and recreational areas, and (3) planning public facilities (such as schools and airports). The constraints associated with these projects are both economic (land, construction, and financing) and social (schools, parks, and income level). The objectives in urban planning vary. In new housing developments, profit is usually the motive for undertaking the project. In the remaining two categories, the goals involve social, political, economic, and cultural considerations. Indeed, in a publicized case in 2004, the mayor of a city in Ohio wanted to condemn an old area of the city to make way for a luxury housing development. The motive was to increase tax collection to help alleviate budget shortages. The example presented in this section is fashioned after the Ohio case.

## Example 2.4-6 (Urban Renewal Model) ^urbanrenewal

The city of Erstville is faced with a severe budget shortage. Seeking a long-term solution, the city council votes to improve the tax base by condemning an inner-city housing area and replacing it with a modern development.

The project involves two phases: (1) demolishing substandard houses to provide land for the new development and (2) building the new development. The following is a summary of the situation.

1. As many as 300 substandard houses can be demolished. Each house occupies a .25-acre lot. The cost of demolishing a condemned house is \$2000.

2. Lot sizes for new single-, double-, triple-, and quadruple-family homes (units) are .18, .28, .4, and .5 acre, respectively. Streets, open space, and utility easements account for 15% of available acreage.

---

${}^{6}$ This section is based on Laidlaw (1972).

---

3. In the new development, the triple and quadruple units account for at least 25% of the total. Single units must be at least 20% of all units, and double units at least 10%.

4. The tax levied per unit for single, double, triple, and quadruple units is \$1000, \$1900, \$2700, and \$3400, respectively.

5. The construction cost per unit for single-, double-, triple-, and quadruple-family homes is \$50,000, \$70,000, \$130,000, and \$160,000, respectively.

6. Financing through a local bank is limited to \$15 million.

How many units of each type should be constructed to maximize tax collection?

Mathematical Model: Besides determining the number of units of each type of housing to be constructed, we also need to decide how many houses must be demolished to make room for the new development. Thus, the variables of the problem can be defined as follows:

$$
{x}_{1} = \text{ Number of units of single-family homes }
$$

$$
{x}_{2} = \text{ Number of units of double-family homes }
$$

$$
{x}_{3} = \text{ Number of units of triple-family homes }
$$

$$
{x}_{4} = \text{ Number of units of quadruple-family homes }
$$

$$
{x}_{5} = \text{ Number of condemned homes to be demolished }
$$

The objective is to maximize total tax collection from all four types of homes-that is,

$$
\text{ Maximize }z = {1000}{x}_{1} + {1900}{x}_{2} + {2700}{x}_{3} + {3400}{x}_{4}
$$

The first constraint of the problem deals with land availability.

$$
\left( \begin{matrix} \text{ Acreage used for new } \\  \text{ homes construction } \end{matrix}\right)  \leq  \left( \begin{matrix} \text{ Net available } \\  \text{ acreage } \end{matrix}\right)
$$

From the data of the problem, we have

$$
\text{ Acreage needed for new homes } = {.18}{x}_{1} + {.28}{x}_{2} + {.4}{x}_{3} + {.5}{x}_{4}
$$

To determine the available acreage, each demolished home occupies a .25-acre lot, thus netting ${.25}{x}_{5}$ acres. Allowing for 15% open space, streets, and easements, the net acreage available is ${.85}\left( {{.25}{x}_{5}}\right)  = {.2125}{x}_{5}$ . The resulting constraint is

$$
{.18}{x}_{1} + {.28}{x}_{2} + {.4}{x}_{3} + {.5}{x}_{4} \leq  {.2125}{x}_{5}
$$

or

$$
{.18}{x}_{1} + {.28}{x}_{2} + {.4}{x}_{3} + {.5}{x}_{4} - {.2125}{x}_{5} \leq  0
$$

The number of demolished homes cannot exceed 300 , which translates to

$$
{x}_{5} \leq  {300}
$$

Next, we add the constraints limiting the number of units of each home type.

$$
\text{ (Number of single units) } \geq  \left( {{20}\% \text{ of all units }}\right)
$$

$$
\text{ (Number of double units) } \geq  ({10}\% \text{ of all units) }
$$

(Number of triple and quadruple units) $\geq  ({25}\%$ of all units)

These constraints translate mathematically to

$$
{x}_{1} \geq  {.2}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4}}\right)
$$

$$
{x}_{2} \geq  {.1}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4}}\right)
$$

$$
{x}_{3} + {x}_{4} \geq  {.25}\left( {{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4}}\right)
$$

The only remaining constraint deals with keeping the demolition/construction cost within the allowable budget-that is,

$$
\text{ (Construction and demolition cost) } \leq  \text{ (Available budget) }
$$

Expressing all the costs in thousands of dollars, we get

$$
\left( {{50}{x}_{1} + {70}{x}_{2} + {130}{x}_{3} + {160}{x}_{4}}\right)  + 2{x}_{5} \leq  {15000}
$$

The complete model thus becomes

$$
\text{ Maximize }z = {1000}{x}_{1} + {1900}{x}_{2} + {2700}{x}_{3} + {3400}{x}_{4}
$$

subject to

$$
{.18}{x}_{1} + {.28}{x}_{2} + {.4}{x}_{3} + {.5}{x}_{4} - {.2125}{x}_{5} \leq  0
$$

$$
{x}_{5} \leq  {300}
$$

$$
- {.8}{x}_{1} + {.2}{x}_{2} + {.2}{x}_{3} + {.2}{x}_{4}
$$

$$
{.1}{x}_{1} - {.9}{x}_{2} + {.1}{x}_{3} + {.1}{x}_{4}
$$

$$
{.25}{x}_{1} + {.25}{x}_{2} - {.75}{x}_{3} - {.75}{x}_{4}
$$

$$
{50}{x}_{1} + {70}{x}_{2} + {130}{x}_{3} + {160}{x}_{4} +
$$

$$
2{x}_{5} \leq  {15000}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} \geq  0
$$

Solution:

The optimum solution (obtained using file amplEX2.4-6.txt or solverEx2.4-6.xls) is

Total tax collection $= z = \$ {343},{965}$

Number of single homes $= {x}_{1} = {35.83} \approx  {36}$ units

Number of double homes $= {x}_{2} = {98.53} \simeq  {99}$ units

Number of triple homes $= {x}_{3} = {44.79} \simeq  {45}$ units

Number of quadruple homes $= {x}_{4} = 0$ units

Number of homes demolished $= {x}_{5} = {244.49} \simeq  {245}$ units

Remarks. Linear programming does not automatically guarantee an integer solution, and this is the reason for rounding the continuous values to the closest integer. The rounded solution calls for constructing ${180}\left( { = {36} + {99} + {45}}\right)$ units and demolishing 245 old homes, which yields \$345,600 in taxes. Keep in mind, however, that, in general, the rounded solution may not be feasible. In fact, the current rounded solution violates the budget constraint by \$70,000 (verify!). Interestingly, the true optimum integer solution (using the algorithms in Chapter 9) is ${x}_{1} = {36},{x}_{2} = {98},{x}_{3} = {45},{x}_{4} = 0$ , and ${x}_{5} = {245}$ with $z = \$ {343},{700}$ . Carefully note that the rounded solution yields a better objective value, which appears contradictory. The reason is that the rounded solution calls for producing an extra double home, which is feasible only if the budget is increased by \$70,000.

#### 2.4.5 Blending and Refining ^blending

A number of LP applications deal with blending different input materials to manufacture products that meet certain specifications while minimizing cost or maximizing profit. The input materials could be ores, metal scraps, chemicals, or crude oils, and the output products could be metal ingots, paints, or gasoline of various grades. This section presents a (simplified) model for oil refining. The process starts with distilling crude oil to produce intermediate gasoline stocks, and then blending these stocks to produce final gasoline products. The final products must satisfy certain quality specifications (such as octane rating). In addition, distillation capacities and demand limits can directly affect the level of production of the different grades of gasoline. One goal of the model is to determine the optimal mix of final products that will maximize an appropriate profit function. In some cases, the goal may be to minimize a cost function.

## Example 2.4-7 (Crude Oil Refining and Gasoline Blending) ^crudeoil

Shale Oil, located on the island of Aruba, has a capacity of 1,500,000 bbl of crude oil per day. The final products from the refinery include three types of unleaded gasoline with different octane numbers (ON): regular with ON = 87, premium with ON = 89, and super with ON = 92 . The refining process encompasses three stages: (1) a distillation tower that produces feedstock (ON = 82) at the rate of .2 bbl per bbl of crude oil, (2) a cracker unit that produces gasoline stock (ON = 98) by using a portion of the feedstock produced from the distillation tower at the rate of ${.5}\mathrm{\;b}\mathrm{{bl}}$ per bbl of feedstock, and (3) a blender unit that blends the gasoline stock from the cracker unit and the feedstock from the distillation tower. The company estimates the net profit per barrel of the three types of gasoline to be \$6.70, \$7.20, and \$8.10, respectively. The input capacity of the cracker unit is 200,000 bbl of feedstock a day. The demand limits for regular, premium, and super gasoline are 50,000, 30,000, and 40,000 bbl, respectively, per day. Develop a model for determining the optimum production schedule for the refinery.

Mathematical Model: Figure 2.12 summarizes the elements of the model. The variables can be defined in terms of two input streams to the blender (feedstock and cracker gasoline) and the three final products. Let

${x}_{ij} = \mathrm{{bbl}}/\mathrm{{day}}$ of input stream $i$ used to blend final product $j, i = 1,2;j = 1,2,3$

FIGURE 2.12

Product flow in the refinery problem

![bo_d56m43v7aajc73800n2g_28_331_1698_1305_508_0.jpg](bo_d56m43v7aajc73800n2g_28_331_1698_1305_508_0.jpg)

Using this definition, we have

Daily production of regular gasoline $= {x}_{11} + {x}_{21}$ bbl/day

Daily production of premium gasoline $= {x}_{12} + {x}_{22}$ bbl/day

Daily production of super gasoline $= {x}_{13} + {x}_{23}$ bbl/day

$$
\left( \begin{array}{l} \text{ Daily output } \\  \text{ of blender unit } \end{array}\right)  = \left( \begin{matrix} \text{ Daily regular } \\  \text{ production } \end{matrix}\right)  + \left( \begin{matrix} \text{ Daily premium } \\  \text{ production } \end{matrix}\right)  + \left( \begin{array}{l} \text{ Daily super } \\  \text{ production } \end{array}\right)
$$

$$
= \left( {{x}_{11} + {x}_{21}}\right)  + \left( {{x}_{12} + {x}_{22}}\right)  + \left( {{x}_{13} + {x}_{23}}\right) \mathrm{{bbl}}/\mathrm{{day}}
$$

$$
\left( \begin{matrix} \text{ Daily feedstock } \\  \text{ to blender } \end{matrix}\right)  = {x}_{11} + {x}_{12} + {x}_{13}\text{ bbl/day }
$$

$$
\left( \begin{matrix} \text{ Daily cracker unit } \\  \text{ feed to blender } \end{matrix}\right)  = {x}_{21} + {x}_{22} + {x}_{23}\text{ bbl/day }
$$

$$
\left( \begin{matrix} \text{ Daily feedstock } \\  \text{ to cracker } \end{matrix}\right)  = 2\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right) \text{ bbl/day }
$$

$$
\left( \begin{matrix} \text{ Daily crude oil used } \\  \text{ in the refinery } \end{matrix}\right)  = 5\left( {{x}_{11} + {x}_{12} + {x}_{13}}\right)  + {10}\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right) \text{ bbl/day }
$$

The objective of the model is to maximize the total profit resulting from the sale of all three grades of gasoline. From the definitions given earlier, we get

$$
\text{ Maximize }z = {6.70}\left( {{x}_{11} + {x}_{21}}\right)  + {7.20}\left( {{x}_{12} + {x}_{22}}\right)  + {8.10}\left( {{x}_{13} + {x}_{23}}\right)
$$

The constraints of the problem are developed as follows:

1. Daily crude oil supply does not exceed 1,500,000 bbl/day:

$$
5\left( {{x}_{11} + {x}_{12} + {x}_{13}}\right)  + {10}\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right)  \leq  1,{500},{000}
$$

2. Cracker unit input capacity does not exceed 200,000 bbl/day:

$$
2\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right)  \leq  {200},{000}
$$

3. Daily demand for regular does not exceed 50,000 bbl:

$$
{x}_{11} + {x}_{21} \leq  {50},{000}
$$

4. Daily demand for premium does not exceed 30,000 bbl:

$$
{x}_{12} + {x}_{22} \leq  {30},{000}
$$

5. Daily demand for super does not exceed 40,000 bbl:

$$
{x}_{13} + {x}_{23} \leq  {40},{000}
$$

6. Octane number (ON) for regular is at least 87:

The octane number of a gasoline product is the weighted average of the octane numbers of the input streams used in the blending process and can be computed as

$\left( \begin{array}{l} \text{ Average ON of } \\  \text{ regular gasoline } \end{array}\right)  =$ ^octanecalc

Feedstock ON $\times$ feedstock bbl/day + Cracker unit ON $\times$ Cracker unit bbl/day

Total bbl/day of regular gasoline

$$
= \frac{{82}{x}_{11} + {98}{x}_{21}}{{x}_{11} + {x}_{21}}
$$

Thus, octane number constraint for regular gasoline becomes

$$
\frac{{82}{x}_{11} + {98}{x}_{21}}{{x}_{11} + {x}_{21}} \geq  {87}
$$

The constraint is linearized as

$$
{82}{x}_{11} + {98}{x}_{21} \geq  {87}\left( {{x}_{11} + {x}_{21}}\right)
$$

7. Octane number for premium is at least 89:

$$
\frac{{82}{x}_{12} + {98}{x}_{22}}{{x}_{12} + {x}_{22}} \geq  {89}
$$

which is linearized as

$$
{82}{x}_{12} + {98}{x}_{22} \geq  {89}\left( {{x}_{12} + {x}_{22}}\right)
$$

8. Octane number for super is at least 92:

$$
\frac{{82}{x}_{13} + {98}{x}_{23}}{{x}_{13} + {x}_{23}} \geq  {92}
$$

or

$$
{82}{x}_{13} + {98}{x}_{23} \geq  {92}\left( {{x}_{13} + {x}_{23}}\right)
$$

The complete model is thus summarized as

$$
\text{ Maximize }z = {6.70}\left( {{x}_{11} + {x}_{21}}\right)  + {7.20}\left( {{x}_{12} + {x}_{22}}\right)  + {8.10}\left( {{x}_{13} + {x}_{23}}\right)
$$

subject to

$$
5\left( {{x}_{11} + {x}_{12} + {x}_{13}}\right)  + {10}\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right)  \leq  1,{500},{000}
$$

$$
2\left( {{x}_{21} + {x}_{22} + {x}_{23}}\right)  \leq  {200},{000}
$$

$$
{x}_{11} + {x}_{21} \leq  {50},{000}
$$

$$
{x}_{12} + {x}_{22} \leq  {30},{000}
$$

$$
{x}_{13} + {x}_{23} \leq  {40},{000}
$$

$$
{82}{x}_{11} + {98}{x}_{21} \geq  {87}\left( {{x}_{11} + {x}_{21}}\right)
$$

$$
{82}{x}_{12} + {98}{x}_{22} \geq  {89}\left( {{x}_{12} + {x}_{22}}\right)
$$

$$
{82}{x}_{13} + {98}{x}_{23} \geq  {92}\left( {{x}_{13} + {x}_{23}}\right)
$$

$$
{x}_{11},{x}_{12},{x}_{13},{x}_{21},{x}_{22},{x}_{23} \geq  0
$$

The last three constraints can be simplified to produce a constant right-hand side.

## Solution:

The optimum solution (obtained using file toraEx2.4-7.txt or amplEx2.4-7.txt) is $z = {875},{000}$ , ${x}_{11} = {34},{375},{x}_{21} = {15},{625},{x}_{12} = {16},{875},{x}_{22} = {13},{125},{x}_{13} = {15},{000},{x}_{23} = {25},{000}$ . This translates to

Daily profit $= \$ {875},{000}$

Daily amount of regular gasoline $= {x}_{11} + {x}_{21} = {34},{375} + {13},{125} = {30},{000}\mathrm{{bbl}}/\mathrm{{day}}$

Daily amount of premium gasoline $= {x}_{12} + {x}_{22} = {16},{875} + {13},{125} = {30},{000}\mathrm{{bbl}}/$ day

Daily amount of super gasoline $= {x}_{13} + {x}_{23} = {15},{000} + {25},{000} = {40},{000}\mathrm{{bbl}}/$ day

The solution shows that regular gasoline production is 20,000 bbl/day short of satisfying the maximum demand. The demand for the remaining two grades is satisfied.

#### 2.4.6 Additional LP Applications ^additional

The preceding sections have demonstrated representative LP applications in five areas. Problems 2-77 to 2-87 provide additional areas of application, ranging from agriculture to military.

## BIBLIOGRAPHY ^bibliography

Dantzig, G. and M. Thapa, Linear Programming 1: Introduction, Springer, New York, 1997.

Fourer, R., D. Gay, and B. Kernighan, AMPL, A Modeling Language for Mathematical Programming, 2nd ed., Brooks/Cole-Thomson, Pacific Grove, CA, 2003.

Laidlaw, C. Linear Programming for Urban Development Plan Evaluation, Praegers, London, 1972.

Lewis, T., "Personal Operations Research: Practicing OR on Ourselves," Interfaces, Vol. 26, No. 5, pp. 34-41, 1996.

Shepard, R., D. Hartley, P. Hasman, L. Thorpe, and M. Bathe, Applied Operations Research, Plenum Press, New York, 1988.

Stark, R., and R. Nicholes, Mathematical Programming Foundations for Design: Civil Engineering Systems, McGraw-Hill, New York, 1972.

## PROBLEMS ^problems


| Section | Assigned Problems | Section | Assigned Problems |
| --- | --- | --- | --- |
| 2.1 | 2-1 to 2-4 | 2.4.2 | 2-47 to 2-54 |
| 2.2.1 | 2-5 to 2-27 | 2.4.3 | 2-55 to 2-60 |
| 2.2.2 | 2-28 to 2-35 | 2.4.4 | 2-61 to 2-66 |
| 2.3.1 | 2-36 to 2-37 | 2.4.5 | 2-67 to 2-76 |
| 2.3.2 | 2-38 to 2-39 | 2.4.6 | 2-77 to 2-87 |
| 2.4.1 | 2-40 to 2-46 |  |  |


2-1. For the Reddy Mikks model, construct each of the following constraints, and express it with a linear left-hand side and a constant right-hand side:

*(a) The daily demand for interior paint exceeds that of exterior paint by at least 1 ton.

(b) The daily usage of raw material ${M1}$ in tons is at most 8 and at least 5 .

*(c) The demand for exterior paint cannot be less than the demand for interior paint.

(d) The maximum quantity that should be produced of both the interior and the exterior paint is 15 tons.

*(e) The proportion of exterior paint to the total production of both interior and exterior paints must not exceed .5.

2-2. Determine the best feasible solution among the following (feasible and infeasible) solutions of the Reddy Mikks model:

(a) ${x}_{1} = 1,{x}_{2} = 2$ .

(b) ${x}_{1} = 3,{x}_{2} = 1$ .

(c) ${x}_{1} = 3,{x}_{2} = {1.5}$ .

(d) ${x}_{1} = 2,{x}_{2} = 1$ .

(e) ${x}_{1} = 2,{x}_{2} =  - 1$ .

*2-3. For the feasible solution ${x}_{1} = 1,{x}_{2} = 2$ of the Reddy Mikks model, determine the unused amounts of raw materials ${M1}$ and ${M2}$ .

2-4. Suppose that Reddy Mikks sells its exterior paint to a single wholesaler at a quantity discount. The profit per ton is \$5000 if the contractor buys no more than 5 tons daily and \$4300 otherwise. Express the objective function mathematically. Is the resulting function linear?

2-5. Determine the feasible space for each of the following independent constraints, given that ${x}_{1},{x}_{2} \geq  0$ .

*(a) $- 3{x}_{1} + {x}_{2} \leq  6$ .

(b) ${x}_{1} - 2{x}_{2} \geq  5$ .

(c) $2{x}_{1} - 3{x}_{2} \leq  {12}$ .

(d) ${x}_{1} - {x}_{2} \leq  0$ .

*(e) $- {x}_{1} + {x}_{2} \geq  0$ .

2-6. Identify the direction of increase in $z$ in each of the following cases:

*(a) Maximize $z = {x}_{1} - {x}_{2}$ .

(b) Maximize $z =  - 8{x}_{1} - 3{x}_{2}$ .

(c) Maximize $z =  - {x}_{1} + 3{x}_{2}$ .

*(d) Maximize $z =  - 3{x}_{1} + {x}_{2}$ .

2-7. Determine the solution space and the optimum solution of the Reddy Mikks model for each of the following independent changes:

(a) The maximum daily demand for interior paint is 1.9 tons and that for exterior paint is at most 2.5 tons.

(b) The daily demand for interior paint is at least 2.5 tons.

(c) The daily demand for interior paint is exactly 1 ton higher than that for exterior paint.

(d) The daily availability of raw material ${M1}$ is at least 24 tons.

(e) The daily availability of raw material ${M1}$ is at least 24 tons, and the daily demand for interior paint exceeds that for exterior paint by at least 1 ton.

2-8. A company that operates 10 hrs a day manufactures two products on three sequential processes. The following table summarizes the data of the problem:


| Product | Minutes per unit - Process 1 | Process 2 | Process 3 | Unit profit |
| --- | --- | --- | --- | --- |
| 1 | 10 | 6 | 8 | \$20 |
| 2 | 5 | 20 | 10 | \$30 |


Determine the optimal mix of the two products.

*2-9. A company produces two products, $A$ and $B$ . The sales volume for $A$ is at least 80% of the total sales of both $A$ and $B$ . However, the company cannot sell more than 110 units of $A$ per day. Both products use one raw material, of which the maximum daily availability is 300 lb. The usage rates of the raw material are 2 lb per unit of $A$ , and 4 lb per unit of $B$ . The profit units for $A$ and $B$ are \$40 and \$90, respectively. Determine the optimal product mix for the company.

2-10. Alumco manufactures aluminum sheets and aluminum bars. The maximum production capacity is estimated at either 800 sheets or 600 bars per day. The maximum daily demand is 550 sheets and 560 bars. The profit per ton is \$40 per sheet and \$35 per bar. Determine the optimal daily production mix.

*2-11. An individual wishes to invest \$5000 over the next year in two types of investment: Investment $A$ yields 5%, and investment $B$ yields 8%. Market research recommends an allocation of at least ${25}\%$ in $A$ and at most ${50}\%$ in $B$ . Moreover, investment in $A$ should be at least half the investment in $B$ . How should the fund be allocated to the two investments?

2-12. The Continuing Education Division at the Ozark Community College offers a total of 30 courses each semester. The courses offered are usually of two types: practical and humanistic. To satisfy the demands of the community, at least 10 courses of each type must be offered each semester. The division estimates that the revenues of offering practical and humanistic courses are approximately \$1500 and \$1000 per course, respectively.

(a) Devise an optimal course offering for the college.

(b) Show that the worth per additional course is \$1500, which is the same as the revenue per practical course. What does this result mean in terms of offering additional courses?

2-13. ChemLabs uses raw materials $I$ and ${II}$ to produce two domestic cleaning solutions, $A$ and $B$ . The daily availabilities of raw materials $I$ and ${II}$ are 150 and 145 units, respectively. One unit of solution $A$ consumes .5 unit of raw material $I$ and .6 unit of raw material ${II}$ . One unit of solution $B$ uses .5 unit of raw material $I$ and .4 unit of raw material ${II}$ . The profits per unit of solutions $A$ and $B$ are $\$ 8$ and $\$ {10}$ , respectively. The daily demand for solution $A$ lies between 30 and 150 units, and that for solution $B$ between 40 and 200 units. Find the optimal production amounts of $A$ and $B$ .

2-14. In the Ma-and-Pa grocery store, shelf space is limited and must be used effectively to increase profit. Two cereal items, Grano and Wheatie, compete for a total shelf space of ${60}{\mathrm{{ft}}}^{2}$ . A box of Grano occupies ${.2}{\mathrm{{ft}}}^{2}$ and a box of Wheatie needs ${.4}{\mathrm{{ft}}}^{2}$ . The maximum daily demands of Grano and Wheatie are 200 and 120 boxes, respectively. A box of Grano nets \$1.00 in profit and a box of Wheatie \$1.35. Ma-and-Pa thinks that because the unit profit of Wheatie is 35% higher than that of Grano, Wheatie should be allocated 35% more space than Grano, which amounts to allocating about 57% to Wheatie and 43% to Grano. What do you think?

2-15. Jack is an aspiring freshman at Ulern University. He realizes that "all work and no play make Jack a dull boy." Jack wants to apportion his available time of about ${10}\mathrm{{hr}}$ s a day between work and play. He estimates that play is twice as much fun as work. He also wants to study at least as much as he plays. However, Jack realizes that if he is going to get all his homework assignments done, he cannot play more than 4 hrs a day. How should Jack allocate his time to maximize his pleasure from both work and play?

2-16. Wild West produces two types of cowboy hats. A Type 1 hat requires twice as much labor time as a Type 2. If all the available labor time is dedicated to Type 2 alone, the company can produce a total of 400 Type 2 hats a day. The respective market limits for Type 1 and Type 2 are 150 and 200 hats per day, respectively. The profit is \$8 per Type 1 hat and \$5 per Type 2 hat. Determine the number of hats of each type that maximizes profit.

2-17. Show & Sell can advertise its products on local radio and television (TV). The advertising budget is limited to \$10,000 a month. Each minute of radio advertising costs \$15, and each minute of TV commercials \$300. Show & Sell likes to advertise on radio at least twice as much as on TV. In the meantime, it is not practical to use more than 400 minutes of radio advertising a month. From past experience, advertising on TV is estimated to be 25 times as effective as on radio. Determine the optimum allocation of the budget to radio and TV advertising.

*2-18. Wyoming Electric Coop owns a steam-turbine power-generating plant. Because Wyoming is rich in coal deposits, the plant generates its steam from coal. This, however, may result in emission that does not meet the Environmental Protection Agency (EPA) standards. EPA regulations limit sulfur dioxide discharge to 2000 parts per million per ton of coal burned and smoke discharge from the plant stacks to 20 lb per hour. The Coop receives two grades of pulverized coal, ${C1}$ and ${C2}$ , for use in the steam plant. The two grades are usually mixed together before burning. For simplicity, it can be assumed that the amount of sulfur pollutant discharged (in parts per million) is a weighted average of the proportion of each grade used in the mixture. The following data is based on the consumption of 1 ton per hr of each of the two coal grades.


| Coal grade | Sulfur discharge in parts per million | Smoke discharge in lb per hour | Steam generated in lb per hour |
| --- | --- | --- | --- |
| ${C1}$ | 1800 | 2.1 | 12,000 |
| ${C2}$ | 2100 | .9 | 9,000 |


(a) Determine the optimal ratio for mixing the two coal grades.

(b) Determine the effect of relaxing the smoke discharge limit by 1 lb on the amount of generated steam per hour.

2-19. Top Toys is planning a new radio and TV advertising campaign. A radio commercial costs \$300 and a TV ad costs \$2000. A total budget of \$20,000 is allocated to the campaign. However, to ensure that each medium will have at least one radio commercial and one TV ad, the most that can be allocated to either medium cannot exceed 80% of the total budget. It is estimated that the first radio commercial will reach 5000 people, with each additional commercial reaching only 2000 new ones. For TV, the first ad will reach 4500 people, and each additional ad an additional 3000. How should the budgeted amount be allocated between radio and TV?

2-20. The Burroughs Garment Company manufactures men's shirts and women's blouses for Walmark Discount Stores. Walmark will accept all the production supplied by Burroughs. The production process includes cutting, sewing, and packaging. Burroughs employs 25 workers in the cutting department, 35 in the sewing department, and 5 in the packaging department. The factory works one 8-hr shift, 5 days a week. The following table gives the time requirements and profits per unit for the two garments.


| Garment | Minutes per unit - Cutting | Sewing | Packaging | Unit profit (\$) |
| --- | --- | --- | --- | --- |
| Shirts | 20 | 70 | 12 | 8 |
| Blouses | 60 | 60 | 4 | 12 |


Determine the optimal weekly production schedule for Burroughs.

2-21. A furniture company manufactures desks and chairs. The sawing department cuts the lumber for both products, which is then sent to separate assembly departments. Assembled items are sent to the painting department for finishing. The daily capacity of the sawing department is 200 chairs or 80 desks. The chair assembly department can produce 120 chairs daily, and the desk assembly department 60 desks daily. The paint department has a daily capacity of either 150 chairs or 110 desks. Given that the profit per chair is \$50 and that of a desk is \$100, determine the optimal production mix for the company.

*2-22. An assembly line consisting of three consecutive stations produces two radio models: HiFi-1 and HiFi-2. The following table provides the assembly times for the three workstations.


| Workstation | Minutes per unit - HiFi-1 | HiFi-2 |
| --- | --- | --- |
| 1 | 6 | 4 |
| 2 | 5 | 5 |
| 3 | 4 | 6 |


The daily maintenance for stations 1, 2, and 3 consumes 10%, 14%, and 12%, respectively, of the maximum 480 minutes available for each station each day. Determine the optimal product mix that will minimize the idle (or unused) times in the three workstations.

2-23. Determination of the Optimum LP Solution by Enumerating All Feasible Corner Points. The remarkable observation gleaned from the graphical LP solution is that the optimum, when finite, is always associated with a corner point of the feasible solution space. Show how this idea is applied to the Reddy Mikks model by evaluating all of its feasible corner points $A, B, C, D, E$ , and $F$ .

2-24. TORA Experiment. Enter the following LP into TORA, and select the graphic solution mode to reveal the LP graphic screen.

$$
\text{ Minimize }z = 3{x}_{1} + 8{x}_{2}
$$

subject to

$$
{x}_{1} + {x}_{2} \geq  8
$$

$$
2{x}_{1} - 3{x}_{2} \leq  0
$$

$$
{x}_{1} + 2{x}_{2} \leq  {30}
$$

$$
3{x}_{1} - {x}_{2} \geq  0
$$

$$
{x}_{1} \leq  {10}
$$

$$
{x}_{2} \geq  9
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

Next, on a sheet of paper, graph and scale the ${x}_{1}$ - and ${x}_{2}$ -axes for the problem (you may also click Print Graph on the top of the right window to obtain a ready-to-use scaled sheet). Now, graph a constraint manually on the prepared sheet, and then click on the left window of the screen to check your answer. Repeat the same for each constraint, and then terminate the procedure with a graph of the objective function. The suggested process is designed to test and reinforce your understanding of the graphical LP solution through immediate feedback from TORA.

2-25. TORA Experiment. Consider the following LP model:

$$
\text{ Maximize }z = 5{x}_{1} + 4{x}_{2}
$$

$$
6{x}_{1} + 4{x}_{2} \leq  {24}
$$

$$
6{x}_{1} + 3{x}_{2} \leq  {22.5}
$$

$$
{x}_{1} + {x}_{2} \leq  5
$$

$$
{x}_{1} + 2{x}_{2} \leq  6
$$

$$
- {x}_{1} + {x}_{2} \leq  1
$$

$$
{x}_{2} \leq  2
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

---

subject to

---

In LP, a constraint is said to be redundant if its removal from the model leaves the feasible solution space unchanged. Use the graphical facility of TORA to identify the redundant constraints, and then show that their removal (simply by not graphing them) does not affect the solution space or the optimal solution.

2-26. TORA Experiment. In the Reddy Mikks model, use TORA to show that the removal of the raw material constraints (constraints 1 and 2) would result in an unbounded solution space. What can be said in this case about the optimal solution of the model?

2-27. TORA Experiment. In the Reddy Mikks model, suppose that the following constraint is added to the problem:

$$
{x}_{2} \geq  3
$$

Use TORA to show that the resulting model has conflicting constraints that cannot be satisfied simultaneously, and hence it has no feasible solution.

2-28. Identify the direction of decrease in $z$ in each of the following cases:

*(a) Minimize $z = 4{x}_{1} - 2{x}_{2}$ .

(b) Minimize $z =  - 6{x}_{1} + 2{x}_{2}$ .

(c) Minimize $z =  - 3{x}_{1} - 6{x}_{2}$ .

2-29. For the diet model, suppose that the daily availability of corn is limited to 400 lb. Identify the new solution space, and determine the new optimum solution.

2-30. For the diet model, determine the optimum solution given the feed mix does not exceed 500 lb a day? Does the solution make sense?

2-31. John must work at least 20 hours a week to supplement his income while attending school. He has the opportunity to work in two retail stores. In store 1, he can work between 4.5 and 12 hours a week, and in store 2, he is allowed between 5.5 and 10 hours. Both stores pay the same hourly wage. In deciding how many hours to work in each store, John wants to base his decision on work stress. Based on interviews with present employees, John estimates that, on an ascending scale of 1 to 10, the stress factors are 8 and 6 at stores 1 and 2, respectively. Because stress mounts by the hour, he assumes that the total stress for each store at the end of the week is proportional to the number of hours he works in the store. How many hours should John work in each store?

*2-32. OilCo is building a refinery to produce four products: diesel, gasoline, lubricants, and jet fuel. The minimum demand (in bbl/day) for each of these products is 14,000,30,000, 10,000, and 8000, respectively. Iraq and Dubai are under contract to ship crude to OilCo. Because of the production quotas specified by OPEC (Organization of Petroleum Exporting Countries), the new refinery can receive at least 40% of its crude from Iraq and the remaining amount from Dubai. OilCo predicts that the demand and crude oil quotas will remain steady over the next 10 years.

The specifications of the two crude oils lead to different product mixes. One barrel of Iraq crude yields .2 bbl of diesel, .25 bbl of gasoline, .1 bbl of lubricant, and .15 bbl of jet fuel. The corresponding yields from Dubai crude are .1, .6, .15, and .1, respectively. OilCo needs to determine the minimum capacity of the refinery (in bbl/day).

2-33. Day Trader wants to invest a sum of money that would generate an annual yield of at least \$10,000. Two stock groups are available: blue chips and high tech, with average annual yields of 10% and 25%, respectively. Though high-tech stocks provide higher yield, they are more risky, and Trader wants to limit the amount invested in these stocks to no more than 60% of the total investment. What is the minimum amount Trader should invest in each stock group to accomplish the investment goal?

*2-34. An industrial recycling center uses two scrap aluminum metals, $A$ and $B$ , to produce a special alloy. Scrap $A$ contains 6% aluminum,3% silicon, and 4% carbon. Scrap $B$ has 3% aluminum,6% silicon, and 3% carbon. The costs per ton for scraps $A$ and $B$ are \$100 and \$80, respectively. The specifications of the special alloy require that (1) the aluminum content must be at least 3% and at most 6%, (2) the silicon content must be between 3% and 5%, and (3) the carbon content must be between 3% and 7%. Determine the optimum mix of the scraps that should be used in producing 1000 tons of the alloy.

2-35. TORA Experiment. Consider the Diet Model, and let the objective function be given as

$$
\text{ Minimize }z = {.8}{x}_{1} + {.8}{x}_{2}
$$

Use TORA to show that the optimum solution is associated with two distinct corner points, and that both points yield the same objective value. In this case, the problem is said to have alternative optima. Explain the conditions leading to this situation, and show that, in effect, the problem has an infinite number of alternative optima. Then provide a formula for determining all such solutions.

2-36. Modify the Reddy Mikks Solver model of Figure 2.4 to account for a third type of paint named "marine." Requirements per ton of raw materials 1 and 2 are .6 and .85 ton, respectively. The daily demand for the new paint lies between .6 ton and 1.9 tons. The profit per ton is \$3700.

2-37. Develop the Excel Solver model for the following problems:

(a) The diet model of Example 2.2-2.

(b) Problem 2-21.

(c) Problem 2-34.

2-38. In the Reddy Mikks model, suppose that a third type of paint, named "marine," is produced. The requirements per ton of raw materials ${M1}$ and ${M2}$ are .7 and .95 ton, respectively. The daily demand for the new paint lies between .4 ton and 2.1 tons, and the profit per ton is \$4500. Modify the Excel Solver model solverRM2.xls and the AMPL model amplRM2.txt to account for the new situation and determine the optimum solution. Compare the additional effort associated with each modification.

2-39. Develop AMPL models for the following problems:

(a) The diet problem of Example 2.2-2 and find the optimum solution.

(b) Problem 2-22.

(c) Problem 2-34.

2-40. Fox Enterprises is considering six projects for possible construction over the next four years. Fox can undertake any of the projects partially or completely. A partial undertaking of a project will prorate both the return and cash outlays proportionately. The expected (present value) returns and cash outlays for the projects are given in the following table.


| Project | Cash outlay (\$1000) - Year 1 | Year 2 | Year 3 | Year 4 | Return (\$1000) |
| --- | --- | --- | --- | --- | --- |
| 1 | 10.5 | 14.4 | 2.2 | 2.4 | 324.00 |
| 2 | 8.3 | 12.6 | 9.5 | 3.1 | 358.00 |
| 3 | 10.2 | 14.2 | 5.6 | 4.2 | 177.50 |
| 4 | 7.2 | 10.5 | 7.5 | 5.0 | 148.00 |
| 5 | 12.3 | 10.1 | 8.3 | 6.3 | 182.00 |
| 6 | 9.2 | 7.8 | 6.9 | 5.1 | 123.50 |
| Available funds (\$1000) | 60.0 | 70.0 | 35.0 | 20.0 |  |


(a) Formulate the problem as a linear program, and determine the optimal project mix that maximizes the total return using AMPL, Solver, or TORA. Ignore the time value of money.

(b) Suppose that if a portion of project 2 is undertaken, then at least an equal portion of project 6 must be undertaken. Modify the formulation of the model, and find the new optimal solution.

(c) In the original model, suppose that any funds left at the end of a year are used in the next year. Find the new optimal solution, and determine how much each year "borrows" from the preceding year. For simplicity, ignore the time value of money.

(d) Suppose in the original model the yearly funds available for any year can be exceeded, if necessary, by borrowing from other financial activities within the company. Ignoring the time value of money, reformulate the LP model, and find the optimum solution. Would the new solution require borrowing in any year? If so, what is the rate of return on borrowed money?

*2-41. Investor Doe has \$10,000 to invest in four projects. The following table gives the cash flow for the four investments.


| Project | Cash flow (\$1000) at the start of - Year 1 | Year 2 | Year 3 | Year 4 | Year 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | -1.00 | 0.50 | 0.30 | 1.80 | 1.20 |
| 2 | -1.00 | 0.60 | 0.20 | 1.50 | 1.30 |
| 3 | 0.00 | -1.00 | 0.80 | 1.90 | 0.80 |
| 4 | -1.00 | 0.40 | 0.60 | 1.80 | 0.95 |


The information in the table can be interpreted as follows: For project 1, \$1.00 invested at the start of year 1 will yield \$.50 at the start of year 2, \$.30 at the start of year 3, \$1.80 at the start of year 4, and \$1.20 at the start of year 5. The remaining entries can be interpreted similarly. The entry 0.00 indicates that no transaction is taking place. Doe has the additional option of investing in a bank account that earns 6.5% annually. All funds accumulated at the end of 1 year can be reinvested in the following year. Formulate the problem as a linear program to determine the optimal allocation of funds to investment opportunities. Solve the model using Solver or AMPL.

2-42. HiRise Construction can bid on two 1-year projects. The following table provides the quarterly cash flow (in millions of dollars) for the two projects.


| Project | Cash flow (in millions of \$) at - January 1 | April 1 | July 1 | October 1 | December 31 |
| --- | --- | --- | --- | --- | --- |
| I | -1.0 | -3.1 | -1.5 | 1.8 | 5.0 |
| II | -3.0 | -2.5 | 1.5 | 1.8 | 2.8 |


HiRise has cash funds of \$1 million at the beginning of each quarter and may borrow at most \$1 million at a 10% nominal annual interest rate. Any borrowed money must be returned at the end of the quarter. Surplus cash can earn quarterly interest at an 8% nominal annual rate. Net accumulation at the end of one quarter is invested in the next quarter.

(a) Assume that HiRise is allowed partial or full participation in the two projects. Determine the level of participation that will maximize the net cash accumulated on December 31. Solve the model using Solver or AMPL.

(b) Is it possible in any quarter to borrow money and simultaneously end up with surplus funds? Explain.

2-43. In anticipation of the immense college expenses, Joe and Jill started an annual investment program on their child's eighth birthday that will last until the eighteenth birthday. They plan to invest the following amounts at the beginning of each year:


| Year | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Amount (\$) | 2000 | 2000 | 2500 | 2500 | 3000 | 3500 | 3500 | 4000 | 4000 | 5000 |


To avoid unpleasant surprises, they want to invest the money safely in the following options: insured savings with 7.5% annual yield, 6-year government bonds that yield 7.9% and have a current market price equal to 98% of face value, and 9-year municipal bonds yielding 8.5% and having a current market price of 1.02 of face value. How should the money be invested?

*2-44. A business executive has the option to invest money in two plans: Plan A guarantees that each dollar invested will earn \$.70 a year later, and plan B guarantees that each dollar invested will earn \$2 after 2 years. In plan A, investments can be made annually, and in plan B, investments are allowed for periods that are multiples of 2 years only. How should the executive invest \$100,000 to maximize the earnings at the end of 3 years? Solve the model using Solver or AMPL.

2-45. A gambler plays a game that requires dividing bet money among four choices. The game has three outcomes. The following table gives the corresponding gain or loss per dollar for the different options of the game.


| Outcome | Return per dollar deposited in choice - 1 | 2 | 3 | 4 |
| --- | --- | --- | --- | --- |
| 1 | -3 | 4 | -7 | 15 |
| 2 | 5 | -3 | 9 | 4 |
| 3 | 3 | -9 | 10 | -8 |


The gambler has a total of \$1500, which may be played only once. The exact outcome of the game is not known a priori. Because of this uncertainty, the gambler's strategy is to maximize the minimum return produced by the three outcomes. How should the gambler allocate the \$1500 among the four choices? Solve the model using Solver or AMPL. (Hint: The gambler's net return may be positive, zero, or negative.)

2-46. Lewis (1996). Bills in a household are received monthly (e.g., utilities and home mortgage), quarterly (e.g., estimated tax payments), semiannually (e.g., insurance), or annually (e.g., subscription renewals and dues). The following table provides the monthly bills for next year.


| Month | Jan. | Feb. | Mar. | Apr. | May | June | July | Aug. | Sep. | Oct. | Nov. | Dec. | Total |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| \$ | 800 | 1200 | 400 | 700 | 600 | 900 | 1500 | 1000 | 900 | 1100 | 1300 | 1600 | 12,000 |


To account for these expenses, the family sets aside \$1000 per month, which is the average of the total divided by 12 months. If the money is deposited in a regular savings account, it can earn 4% annual interest, provided it stays in the account at least 1 month. The bank also offers 3-month and 6-month certificates of deposit that can earn 5.5% and 7% annual interest, respectively. Develop a 12-month investment schedule that will maximize the family's total return for the year. State any assumptions or requirements needed to reach a feasible solution. Solve the model using Solver or AMPL.

2-47. Toolco has contracted with AutoMate to supply their automotive discount stores with wrenches and chisels. AutoMate's weekly demand consists of at least 1570 wrenches and 1250 chisels. Toolco cannot produce all the requested units with its present one-shift capacity, and must use overtime and possibly subcontract with other tool shops. The result is an increase in the production cost per unit, as shown in the following table. Market demand restricts the ratio of chisels to wrenches to at least 2:1.


| Tool - Wrenches | Production type - Regular | Weekly production range (units) - 0-500 | Unit cost (\$) - 2.00 |
| --- | --- | --- | --- |
| Wrenches | Overtime | 501-800 | 2.80 |
| Wrenches | Subcontracting | 801-∞ | 3.00 |
| Chisel | Regular | 0-620 | 2.10 |
| Chisel | Overtime | 621-900 | 3.20 |
| Chisel | Subcontracting | 901-0 | 4.20 |


(a) Formulate the problem as a linear program, and determine the optimum production schedule for each tool.

(b) Explain why the validity of the model is dependent on the fact that the unit production cost is an increasing function of the production quantity.

(c) Solve the model using AMPL, Solver, or TORA.

2-48. Four products are processed sequentially on three machines. The following table gives the pertinent data of the problem.


| Machine | Cost per hr (\$) | Manufacturing time (hr) per unit - Product 1 | Product 2 | Product 3 | Product 4 | Capacity (hr) |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 10 | 2 | 3 | 4 | 2 | 500 |
| 2 | 5 | 3 | 2 | 1 | 2 | 380 |
| 3 | 4 | 7 | 3 | 2 | 1 | 450 |
| Unit selling / price (\$) |  | 75 | 70 | 55 | 45 |  |


Formulate the problem as an LP model and find the optimum solution using AMPL, Solver, or TORA.

*2-49. A manufacturer produces three models, I, II, and III, of a certain product using raw materials $A$ and $B$ . The following table gives the data for the problem.


| Raw material | Requirements per unit - $I$ | II | III | Availability |
| --- | --- | --- | --- | --- |
| $A$ | 2 | 3 | 5 | 4000 |
| $B$ | 4 | 2 | 7 | 6000 |
| Minimum demand / Price per unit (\$) | 200 | 200 | 150 |  |
| Minimum demand / Price per unit (\$) | 30 | 20 | 50 |  |


The labor time per unit of model I is twice that of II and three times that of III. The entire labor force of the factory can produce the equivalent of 1500 units of model I. Market requirements specify the ratios 3:2:5 for the production of the three respective models. Formulate the problem as a linear program and find the optimum solution using AMPL, Solver, or TORA.

2-50. The demand for ice cream at All-Flavors Parlor during the three summer months (June, July, and August) is estimated at 500, 600, and 400 20-gallon cartons, respectively. Two wholesalers, 1 and 2, supply All-Flavors with its ice cream. Although the flavors from the two suppliers are different, they are interchangeable. The maximum number of cartons either supplier can provide is 400 per month. Also, the price the two suppliers charge change monthly according to the following schedule:


|  | Price per carton in month - June | July | August |
| --- | --- | --- | --- |
| Supplier 1 | \$100 | \$110 | \$120 |
| Supplier 2 | \$115 | \$108 | \$125 |


To take advantage of price fluctuation, All-Flavors can purchase more than is needed for a month and store the surplus to satisfy the demand in a later month. The storage cost of an ice cream carton is \$5 per month. It is realistic in the present situation to assume that the storage cost is a function of the average number of cartons on hand during the month. Develop a model to determine the optimum schedule for buying ice cream from the two suppliers and find the optimum solution using TORA, Solver, or AMPL.

2-51. The demand for an item over the next four quarters is280,400,450, and 300 units, respectively. The price per unit starts at \$20 in the first quarter and increases by \$1 each quarter thereafter. The supplier can provide no more than 400 units in any one quarter. Although we can take advantage of lower prices in early quarters, a storage cost of \$3.80 is incurred per unit per quarter. In addition, the number of units that can be held over from one quarter to the next must be 80 or less. Develop an LP model to determine the optimum schedule for purchasing the item to meet the demand, and find the optimum solution using AMPL, Solver, or TORA.

2-52. A company has contracted to produce two products, $A$ and $B$ , over the months of June, July, and August. The total production capacity (expressed in hours) varies monthly. The following table provides the basic data of the situation:


|  | June | July | August |
| --- | --- | --- | --- |
| Demand for $A$ (units) | 500 | 5000 | 750 |
| Demand for $B$ (units) | 1000 | 1200 | 1200 |
| Capacity (hours) | 3000 | 3500 | 3000 |


The production rates in units per hour are .75 and 1 for products $A$ and $B$ , respectively. All demand must be met. However, demand for a later month may be filled from the production in an earlier one. For any carryover from one month to the next, holding costs of \$.90 and \$.75 per unit per month are charged for products $A$ and $B$ , respectively. The unit production costs for the two products are \$30 and \$28 for $A$ and $B$ , respectively. Develop an LP model to determine the optimum production schedule for the two products and find the optimum solution using AMPL, Solver, or TORA.

*2-53. The manufacturing process of a product consists of two successive operations, I and II. The following table provides the pertinent data over the months of June, July, and August:


|  | June | July | August |
| --- | --- | --- | --- |
| Finished product demand (units) | 500 | 450 | 600 |
| Capacity of operation I (hr) | 800 | 700 | 550 |
| Capacity of operation II (hr) | 1000 | 850 | 700 |


Producing a unit of the product takes ${.6}\mathrm{{hr}}$ on operation I plus ${.8}\mathrm{{hr}}$ on operation II. Overproduction of either the semifinished product (operation I) or the finished product (operation II) in any month is allowed for use in a later month. The respective holding costs for operations I and II are \$.20 and \$.40 per unit per month. The production cost varies by operation and by month. For operation 1, the unit production cost is $\$ {10},\$ {12}$ , and $\$ {11}$ for June, July, and August. For operation 2, the corresponding unit production cost is \$15, \$18, and \$16. Develop an LP model to determine the optimal production schedule for the two operations over the 3-month horizon and find the optimum solution using AMPL, Solver, or TORA.

2-54. Two products are manufactured sequentially on two machines. The time available on each machine is 8 hours per day and may be increased by up to 4 hours of overtime, if necessary, at an additional cost of \$110 per hour. The table below gives the production rate on the two machines as well as the price per unit of the two products. Develop an LP model to determine the optimum production schedule, and the recommended use of overtime, if any. Solve the problem using AMPL, Solver, or TORA.


|  | Production rate (units/hr) - Product 1 | Product 2 |
| --- | --- | --- |
| Machine 1 | 5 | 5 |
| Machine 2 | 8 | 4 |
| Price per unit (\$) | 120 | 128 |


*2-55. In the bus scheduling example suppose that buses can run either 8- or 12-hr shifts. If a bus runs for ${12}\mathrm{{hr}}$ , the driver must be paid for the extra hours at ${150}\%$ of the regular hourly pay. Do you recommend the use of 12-hr shifts? Solve the new model using AMPL, Solver, or TORA.

2-56. A hospital employs volunteers to staff the reception desk between 8:00 A.M. and 10:00 P.M. Each volunteer works three consecutive hours except for those starting at 8:00 p.m. who work for two hours only. The minimum need for volunteers is approximated by a step function over 2-hour intervals starting at 8:00 a.m. as8,6,8,6,4,6, and 5. Because most volunteers are retired individuals, they are willing to offer their services at any hour of the day (8:00 A.M. to 10:00 P.M.). However, because of the large number of charities competing for their service, the number needed must be kept as low as possible. Determine an optimal schedule (using AMPL, Solver, or TORA) for the start time of the volunteers.

2-57. In Problem 2-56, suppose that no volunteers will start at 2:00 P.M. or 7:00 P.M. to allow for lunch and dinner. Develop the LP, and determine the optimal schedule using AMPL, Solver, or TORA.

2-58. In an LTL (less-than-truckload) trucking company, terminal docks include casual workers who are hired temporarily to account for peak loads. At the Omaha, Nebraska dock, the minimum demand for casual workers during the seven days of the week (starting on Monday) is12,20,14,10,15,18, and 10 workers. Each worker is contracted to work five consecutive days. Develop the LP model, and determine an optimal weekly hiring practice of casual workers for the company using AMPL, Solver, or TORA.

*2-59. On most U.S. university campuses, students are contracted by academic departments to do errands, such as answering the phone and typing. The need for such service fluctuates during work hours (8:00 A.M. to 5:00 P.M.). In one department, the minimum number of students needed is 2 between 8:00 A.M. and 10:00 A.M., 4 between 10:01 A.M. and 11:00 A.M., 3 between 11:01 A.M. and 1:00 P.M., and 2 between 1:01 P.M. and 5:00 P.M. Each student is allotted 3 consecutive hours (except for those starting at 3:01, who work for 2 hours, and those who start at 4:01, who work for 1 hour). Because of their flexible schedule, students can usually report to work at any hour during the work day, except that no student wants to start working at lunch time (12:00 noon). Develop the LP model, and determine a time schedule specifying the time of the day and the number of students reporting to work. Use AMPL, Solver, or TORA to determine the solution.

2-60. A large department store operates 7 days a week. The manager estimates that the minimum number of salespersons required to provide prompt service is 12 for Monday, 18 for Tuesday, 20 for Wednesday, 28 for Thursday, 32 for Friday, and 40 for each of Saturday and Sunday. Each salesperson works 5 days a week, with the two consecutive off-days staggered throughout the week. For example, if 10 salespersons start on Monday, 2 can take their off-days on Tuesday and Wednesday, 5 on Wednesday and Thursday, and 3 on Saturday and Sunday. How many salespersons should be contracted, and how should their off-days be allocated? Use AMPL, Solver, or TORA to find the solution.

2-61. A realtor is developing a rental housing and retail area. The housing area consists of efficiency apartments, duplexes, and single-family homes. Maximum demand by potential renters is estimated to be 500 efficiency apartments, 300 duplexes, and 250 single-family homes, but the number of duplexes must equal at least 50% of the number of efficiency apartments and single homes. Retail space is proportionate to the number of home units at the rates of at least ${12}{\mathrm{{ft}}}^{2},{18}{\mathrm{{ft}}}^{2}$ , and ${20}{\mathrm{{ft}}}^{2}$ for efficiency, duplex, and single family units, respectively. However, land availability limits retail space to no more than 15,000 ${\mathrm{{ft}}}^{2}$ . The monthly rental income is estimated at \$650, \$800, and \$1500 for efficiency-, duplex-, and single-family units, respectively. The retail space rents for \$120/ft2. Develop an LP model to determine the optimal retail space area and the number of family residences, and find the solution using AMPL, Solver, or TORA.

2-62. The city council of Fayetteville is in the process of approving the construction of a new 180,000-ft ${}^{2}$ convention center. Two sites have been proposed, and both require exercising the "eminent domain" law to acquire the property. The following table provides data about proposed (contiguous) properties in both sites together with the acquisition cost.


| Property | Site 1 - Area (1000 ft ${}^{2}$ ) | Cost (1000 \$) | Site 2 - Area (1000 ft ${}^{2}$ ) | Cost (1000 \$) |
| --- | --- | --- | --- | --- |
| 1 | 20 | 1,000 | 80 | 2,800 |
| 2 | 50 | 2,100 | 60 | 1,900 |
| 3 | 50 | 2,350 | 50 | 2,800 |
| 4 | 30 | 1,850 | 70 | 2,500 |
| 5 | 60 | 2,950 |  |  |


Partial acquisition of property is allowed. At least 80% of property 4 must be acquired if site 1 is selected, and at least 60% of property 3 must be acquired if site 2 is selected. Although site 1 property is more expensive (on a per ${\mathrm{{ft}}}^{2}$ basis), the construction cost is less than at site 2, because the infrastructure at site 1 is in a much better shape. Construction cost is \$30 million at site 1 and \$32 million at site 2. Which site should be selected, and what properties should be acquired? Find the solution using AMPL, Solver, or TORA.

*2-63. A city will undertake five urban renewal housing projects over the next 5 years. Each project has a different starting year and a different duration. The following table provides the basic data of the situation:


| Project 1 | Year 1 - Start | Year 2 - Start | Year 3 - End | Year 4 | Year 5 | Cost (million \$) - 5.0 | Annual income (million \$) - .05 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Project 2 | Start | Start |  |  | End | 8.0 | .07 |
| Project 3 | Start | Start |  |  | End | 15.0 | .15 |
| Project 4 |  | Start | Start | End |  | 1.2 | .02 |
| Budget / (million \$) | 3.0 | 6.0 | 7.0 | 7.0 | 7.0 |  |  |


Projects 1 and 4 must be finished completely within their durations. The remaining two projects can be finished partially within budget limitations, if necessary. However, each project must be at least 25% completed within its duration. At the end of each year, the completed section of a project is immediately occupied by tenants, and a proportional amount of income is realized. For example, if 40% of project 1 is completed in year 1 and 60% in year 3, the associated income over the 5-year planning horizon is .4 × \$50,000 (for year 2) + .4 × \$50,000 (for year 3) + (.4 + .6) × \$50,000 (for year 4) $+ \left( {{.4} + {.6}}\right)  \times  \$ {50},{000}$ (for year 5) $= \left( {4 \times  {.4}}\right)  + \left( {2 \times  {.6}}\right)  \times  \$ {50},{000}$ . Develop an LP model to determine the schedule for the projects that will maximize

the total income over the 5-year horizon, and find the solution using AMPL, Solver, or TORA. For simplicity, disregard the time value of money.

2-64. The city of Fayetteville is embarking on an urban renewal project that will include lower and middle-income row housing, upper-income luxury apartments, and public housing. The project also includes a public elementary school and retail facilities. The size of the elementary school (number of classrooms) is proportional to the number of pupils, and the retail space is proportional to the number of housing units. The following table provides the pertinent data of the situation:


|  | Lower income | Middle income | Upper income | Public housing | School room | Retail unit |
| --- | --- | --- | --- | --- | --- | --- |
| Minimum number of units | 100 | 125 | 75 | 300 |  | 0 |
| Maximum number of units | 200 | 190 | 260 | 600 |  | 25 |
| Lot size per unit (acre) | .05 | .07 | .03 | .025 | .045 | .1 |
| Average number of pupils per unit | 1.3 | 1.2 | .5 | 1.4 |  |  |
| Retail demand per unit (acre) | .023 | .034 | .046 | .023 | .034 |  |
| Annual income per unit (\$) | 7,000 | 12,000 | 20,000 | 5,000 | - | 15,000 |


The new school can occupy a maximum of 2 acres. Class size is limited to 25 students per room. The operating annual cost per schoolroom is \$10,000. The project will be located on a 50-acre vacant property owned by the city. Additionally, the project can make use of an adjacent property occupied by 200 condemned slum homes. Each condemned home occupies .25 acre. The cost of buying and demolishing a slum unit is \$7000. Open space, streets, and parking lots consume 15% of total available land.

Develop a linear program to determine the optimum plan for the project, and find the solution using AMPL, Solver, or TORA.

2-65. Realco owns 900 acres of undeveloped land on a scenic lake in the heart of the Ozark Mountains. In the past, little or no regulation was imposed upon new developments around the lake. The lake shores are now dotted with vacation homes, and septic tanks are in extensive use, most of them improperly installed. Over the years, seepage from the septic tanks led to severe water pollution. To curb further degradation of the lake, county officials have approved stringent ordinances applicable to all future developments: (1) Only single-, double-, and triple-family homes can be constructed, with single-family homes accounting for at least 50% of the total. (2) To limit the number of septic tanks, minimum lot sizes of 2, 3, and 5 acres are required for single-, double-, and triple-family homes, respectively. (3) Recreation areas of 1 acre each must be established at the rate of one area per 220 families. (4) To preserve the ecology of the lake, underground water may not be pumped out for house or garden use. The president of Realco is studying the possibility of developing the 800-acre property. The new development will include single-, double-, and triple-family homes. It is estimated that 15% of the acreage will be allocated to streets and utility easements. Realco estimates the returns from the different housing units as follows:


| Housing unit | Single | Double | Triple |
| --- | --- | --- | --- |
| Net return per unit (\$) | 12,000 | 15,000 | 18,000 |


The cost of connecting water service to the area is proportionate to the number of units constructed. However, the county charges a minimum of \$120,000 for the project. Additionally, the expansion of the water system beyond its present capacity is limited to

220,000 gallons per day during peak periods. The following data summarize the water service connection cost as well as the water consumption, assuming an average size family:


| Housing unit | Single | Double | Triple | Recreation |
| --- | --- | --- | --- | --- |
| Water service connection cost per unit (\$) | 1000 | 1200 | 1400 | 800 |
| Water consumption per unit (gal/day) | 400 | 600 | 840 | 450 |


Develop an LP model to determine the optimal plan for Realco, and find the solution using AMPL, Solver, or TORA.

2-66. Consider the Realco model of Problem 2-65. Suppose that an additional 100 acres of land can be purchased for \$450,000, which will increase the total acreage to 900 acres. Is this a profitable deal for Realco?

2-67. Hi-V produces three types of canned juice drinks, $A, B$ , and $C$ , using fresh strawberries, grapes, and apples. The daily supply is limited to 200 tons of strawberries, 90 tons of grapes, and 150 tons of apples. The cost per ton of strawberries, grapes, and apples is \$210, \$110, and \$100, respectively. Each ton makes 1500 lb of strawberry juice, 1200 lb of grape juice, and 1000 lb of apple juice. Drink $A$ is a 1:1 mix of strawberry and apple juice. Drink $B$ is 1:1:2 mix of strawberry, grape, and apple juice. Drink $C$ is a 2:3 mix of grape and apple juice. All drinks are canned in 16-oz (1 lb) cans. The price per can is \$1.15, \$1.25, and \$1.20 for drinks $A, B$ , and $C$ . Develop an LP model to determine the optimal production mix of the three drinks, and find the solution using AMPL, Solver, or TORA.

*2-68. A hardware store packages handyman bags of screws, bolts, nuts, and washers. Screws come in 100-lb boxes and cost \$120 each, bolts come in 100-lb boxes and cost \$175 each, nuts come in 80-lb boxes and cost \$75 each, and washers come in 30-lb boxes and cost \$25 each. The handyman package weighs at least 1 lb and must include, by weight, at least 10% screws and 25% bolts, and at most 15% nuts and 10% washers. To balance the package, the number of bolts cannot exceed the number of nuts or the number of washers. A bolt weighs 10 times as much as a nut and 50 times as much as a washer. Develop an LP model to determine the optimal mix of the package, and find the solution using AMPL, Solver, or TORA.

2-69. All-Natural Coop makes three breakfast cereals, $A, B$ , and $C$ , from four ingredients: rolled oats, raisins, shredded coconuts, and slivered almonds. The daily availabilities of the ingredients are 5 tons, 2 tons, 1 ton, and 1 ton, respectively. The corresponding costs per ton are \$100, \$120, \$110, and \$200, respectively. Cereal $A$ is a 50:5:2 mix of oats, raisins, and almond. Cereal $B$ is a 60:2:3 mix of oats, coconut, and almond. Cereal $C$ is a 60:3:4:2 mix of oats, raisins, coconut, and almond. The cereals are produced in jumbo 5-lb sizes. All-Natural sells $A, B$ , and $C$ at $\$ {2.00},\$ {2.50}$ , and $\$ {3.00}$ per box, respectively. The minimum daily demand for cereals $A, B$ , and $C$ is 500,600, and 500 boxes, respectively. Develop an LP model to determine the optimal production mix of the cereals and the associated amounts of ingredients, and find the solution using AMPL, Solver, or TORA.

2-70. A refinery manufactures two grades of jet fuel, ${F1}$ and ${F2}$ , by blending four types of gasoline, $A, B, C$ , and $D$ . Fuel ${F1}$ uses gasolines $A, B, C$ , and $D$ in the ratio $1 : 1 : 2 : 4$ , and fuel ${F2}$ uses the ratio 2:2:1:3. The supply limits for $A, B, C$ , and $D$ are1000,1200,900, and 1500 bbl/day, respectively. The costs per bbl for gasolines $A, B, C$ , and $D$ are \$120, \$90, \$100, and \$150, respectively. Fuels F1 and F2 sell for \$200 and \$250 per bbl, respectively. The minimum demand for ${F1}$ and ${F2}$ is 200 and 400 bbl/day, respectively. Develop an LP model to determine the optimal production mix for ${F1}$ and ${F2}$ , and find the solution using AMPL, Solver, or TORA.

*2-71. An oil company distills two types of crude oil, $A$ and $B$ , to produce regular and premium gasoline and jet fuel. There are limits on the daily availability of crude oil

and the minimum demand for the final products. If the production is not sufficient to cover demand, the shortage must be made up from outside sources at a penalty. Surplus production will not be sold immediately and will incur storage cost. The following table provides the data of the situation:


| Crude | Fraction yield per bbl - Regular | Premium | Jet | Price/bbl (\$) | bbl/day |
| --- | --- | --- | --- | --- | --- |
| Crude A | .20 | .1 | .25 | 30 | 2500 |
| Crude B | .25 | .3 | .10 | 40 | 3000 |
| Demand (bbl/day) | 500 | 700 | 400 |  |  |
| Revenue (\$/bbl) | 50 | 70 | 120 |  |  |
| Storage cost for surplus production (\$/bbl) | 2 | 3 | 4 |  |  |
| Penalty for unfilled demand (\$/bbl) | 10 | 15 | 20 |  |  |


Develop an LP model to determine the optimal product mix for the refinery, and find the solution using AMPL, Solver, or TORA.

2-72. In the refinery situation of Problem 2-71, suppose that the distillation unit actually produces the intermediate products naphtha and light oil. One bbl of crude $A$ produces .35 bbl of naphtha and .6 bbl of light oil, and one bbl of crude $B$ produces .45 bbl of naphtha and .5 bbl of light oil. Naphtha and light oil are blended to produce the three final gasoline products: One bbl of regular gasoline has a blend ratio of 2:1 (naphtha to light oil), one bbl of premium gasoline has a blend ratio of 1:1, and one bbl of jet fuel has a blend ratio of 1:2. Develop an LP model to determine the optimal production mix, and find the solution using AMPL, Solver, or TORA.

2-73. Hawaii Sugar Company produces brown sugar, processed (white) sugar, powdered sugar, and molasses from sugarcane syrup. The company purchases 4000 tons of syrup weekly and is contracted to deliver at least 25 tons weekly of each type of sugar. The production process starts by manufacturing brown sugar and molasses from the syrup. A ton of syrup produces .3 ton of brown sugar and .1 ton of molasses. White sugar is produced by processing brown sugar. It takes 1 ton of brown sugar to produce .8 ton of white sugar. Powdered sugar is produced from white sugar through a special grinding process that has a 95% conversion efficiency (1 ton of white sugar produces .95 ton of powdered sugar). The profits per ton for brown sugar, white sugar, powdered sugar, and molasses are \$150, \$200, \$230, and \$35, respectively. Formulate the problem as a linear program, and determine the weekly production schedule using AMPL, Solver, or TORA.

2-74. Shale Oil refinery blends two petroleum stocks, $A$ and $B$ , to produce two high-octane gasoline products, I and II. Stocks $A$ and $B$ are produced at the maximum rates of 450 and ${700}\mathrm{{bbl}}/\mathrm{{hr}}$ , respectively. The corresponding octane numbers are 98 and 89, and the vapor pressures are 10 and $8\mathrm{{lb}}/{\mathrm{{in}}}^{2}$ . Gasoline I and gasoline II must have octane numbers of at least 91 and 93, respectively. The vapor pressure associated with both products should not exceed 12 lb/in ${}^{2}$ . The profits per bbl of I and II are \$7 and \$10, respectively. Develop an LP model to determine the optimum production rate for I and II and their blend ratios from stocks $A$ and $B$ , and find the solution using AMPL, Solver, or TORA. (Hint: Vapor pressure, like the octane number, is the weighted average of the vapor pressures of the blended stocks.)

2-75. A foundry smelts steel, aluminum, and cast iron scraps to produce two types of metal ingots, I and II, with specific limits on the aluminum, graphite, and silicon contents.

Aluminum and silicon briquettes may be used in the smelting process to meet the desired specifications. The following tables set the specifications of the problem:


| Input item | Contents (%) - Aluminum | Graphite | Silicon | Cost/ton (\$) | Available (tons/day) |
| --- | --- | --- | --- | --- | --- |
| Steel scrap | 10 | 5 | 4 | 100 | 1000 |
| Aluminum scrap | 95 | 1 | 2 | 150 | 500 |
| Cast iron scrap | 0 | 15 | 8 | 75 | 2500 |
| Aluminum briquette | 100 | 0 | 0 | 900 | Any amount |
| Silicon briquette | 0 | 0 | 100 | 380 | Any amount |



| Ingredient | Ingot I (%) - Minimum | Maximum | Ingot II (%) - Minimum | Maximum |
| --- | --- | --- | --- | --- |
| Aluminum | 8.1 | 10.8 | 6.2 | 8.9 |
| Graphite | 1.5 | 3.0 | 4.1 | $\infty$ |
| Silicon | 2.5 | $\infty$ | 2.8 | 4.1 |
| Demand (tons/day) |  | 130 | 250 |  |


Develop an LP model to determine the optimal input mix the foundry should smelt, and find the solution using AMPL, Solver, or TORA.

2-76. Two alloys, $A$ and $B$ , are made from four metals, I, II, III, and IV, according to the following specifications: 100 boxes, respectively. The shelf space in square inches for the respective boxes is 15, 25, 16, 20, and 22. The total available shelf space is ${5000}{\text{ in }}^{2}$ . The profit per unit is \$1.10,\$1.30,\$1.08, \$1.25, and \$1.20, respectively. Determine the optimal space allocation for the five cereals.


| Alloy | Specifications | Selling price (\$) |
| --- | --- | --- |
| $A$ | At most 80% of I / At most 30% of II / At least 50% of IV | 200 |
| $B$ | Between 40% and 60% of II / At least 30% of III / At most 70% of IV | 300 |


The four metals are extracted from three ores according to the following data:


| Ore | Maximum quantity (tons) | Constituents (%) - I | II | III | IV | Others | Price/ton (\$) |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1000 | 20 | 10 | 30 | 30 | 10 | 30 |
| 2 | 2000 | 10 | 20 | 30 | 30 | 10 | 40 |
| 3 | 3000 | 5 | 5 | 70 | 20 | 0 | 50 |


Develop an LP model to determine how much of each type of alloy should be produced, and find the solution using AMPL, Solver, or TORA. (Hint: Let ${x}_{kj}$ be tons of ore $i$ allocated to alloy $k$ , and define ${w}_{k}$ as tons of alloy $k$ produced.)

2-77. Shelf Space Allocation. A grocery store must decide on the shelf space to be allocated to each of five types of breakfast cereals. The maximum daily demand is110,80,150,85, and

2-78. Voting on Issues. In a particular county in the State of Arkansas, four election issues are on the ballot: Build new highways, increase gun control, increase farm subsidies, and increase gasoline tax. The county includes 100,000 urban voters, 250,000 suburban voters, and 50,000 rural voters, all with varying degrees of support for and opposition to, election issues. For example, rural voters are opposed to gun control and gas tax and in favor of road building and farm subsidies. The county is planning a TV advertising campaign with a budget of \$100,000 at a cost of \$1500 per ad. The following table summarizes the impact of a single ad in terms of the number of pro and con votes as a function of the different issues:


| Issue | Expected number of pro $\left( +\right)$ and con (-) votes per ad - Urban | Suburban | Rural |
| --- | --- | --- | --- |
| New highways | -30,000 | +60,000 | +30,000 |
| Gun control | +80,000 | +30,000 | -45,000 |
| Smog control | +40,000 | +10,000 | 0 |
| Gas tax | +90,000 | 0 | -25,000 |


An issue will be adopted if it garners at least 51% of the votes. Which issues will be approved by voters, and how many ads should be allocated to these issues?

2-79. Assembly-Line Balancing. A product is assembled from three different parts. The parts are manufactured by two departments at different production rates as given in the following table:


| Department | Capacity (hr/wk) | Production rate (units/hr) - Part 1 | Part 2 | Part 3 |
| --- | --- | --- | --- | --- |
| 1 | 100 | 6 | 8 | 12 |
| 2 | 90 | 6 | 12 | 4 |


Determine the maximum number of final assembly units that can be produced weekly. (Hint: Assembly units = min \{units of part 1, units of part 2, and units of part 3\}. Maximize $z = \min \left\{  {{x}_{1},{x}_{2}}\right\}$ is equivalent to max $z$ subject to $z \leq  {x}_{1}$ and $z \leq  {x}_{2}$ .)

2-80. Pollution Control. Three types of coal, C1, C2, and C3, are pulverized and mixed together to produce 50 tons per hour needed to power a plant for generating electricity. The burning of coal emits sulfur oxide (in parts per million) which must meet the EPA specifications of no more than 2000 parts per million. The following table summarizes the data of the situation:


|  | C1 | C2 | C3 |
| --- | --- | --- | --- |
| Sulfur (parts per million) | 2500 | 1500 | 1600 |
| Pulverizer capacity (ton/hr) | 30 | 30 | 30 |
| Cost per ton | \$30 | \$35 | \$33 |


Determine the optimal mix of the coals.

*2-81. Traffic Light Control, Stark and Nicholes (1972). Automobile traffic from three highways, H1, H2, and H3, must stop and wait for a green light before exiting to a toll road. The tolls are $\$ 4,\$ 5$ , and $\$ 6$ for cars exiting from H1, H2, and H3, respectively. The flow rates from H1, H2, and H3 are 550, 650, and 450 cars per hour. The traffic light cycle may not exceed 2.2 minutes, and the green light on any highway must be at least 22 seconds. The yellow light is on for 10 seconds. The toll gate can handle a maximum of 500 cars per hour. Assuming that no cars move on yellow, determine the optimal green time interval for the three highways that will maximize toll gate revenue per traffic cycle.

2-82. Fitting a Straight Line into Empirical Data (Regression). In a 10-week typing class for beginners, the average speed per student (in words per minute) as a function of the number of weeks in class is given in the following table.


| Week, $x$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Words per minute, $y$ | 5 | 9 | 15 | 19 | 21 | 24 | 26 | 30 | 31 | 35 |


Determine the coefficients $a$ and $b$ in the straight-line relationship, $\widehat{y} = {ax} + b$ , that best fit the given data. (Hint: Minimize the sum of the absolute value of the deviations between theoretical $\widehat{y}$ and empirical $y$ . Min $\left| w\right|$ is equivalent to $\min z$ subject to $z \geq  w$ and $z \geq   - w, z \geq  0$ . Alternatively, $\min \left| w\right|$ is equivalent to $\min \left( {{z}^{ + } + {z}^{ - }}\right)$ subject to $w = {z}^{ + } - {z}^{ - }$ with ${z}^{ + },{z}^{ - } \geq  0$ .)

2-83. Leveling the Terrain for a New Highway, Stark and Nicholes (1972). The Arkansas Highway Department is planning a new 10-mile highway on uneven terrain as shown by the profile in Figure 2.13. The width of the construction terrain is approximately 50 yards. To simplify the situation, the terrain profile can be replaced by a step function as shown in the figure. Using heavy machinery, earth removed from high terrain is hauled to fill low areas. There are also two burrow pits, I and II, located at the ends of the 10-mile stretch from which additional earth can be hauled, if needed. Pit I has a capacity of 20,000 cubic yards and pit II a capacity of 15,000 cubic yards. The costs of removing earth from pits I and II are, respectively, \$1.50 and \$1.90 per cubic yard.

FIGURE 2.13

Terrain profile for Problem 2-83

![bo_d56m43v7aajc73800n2g_50_425_1533_1109_645_0.jpg](bo_d56m43v7aajc73800n2g_50_425_1533_1109_645_0.jpg)

The transportation cost per cubic yard per mile is \$.15, and the cost of using heavy machinery to load hauling trucks is \$.20 per cubic yard. This means that a cubic yard from pit I hauled 1 mile will cost a total of $\left( {{1.5} + {.20}}\right)  + 1 \times  {.15} = \$ {1.85}$ and a cubic yard hauled 1 mile from a hill to a fill area will cost ${.20} + 1 \times  {.15} = \$ {.35}$ . Develop a minimum cost plan for leveling the 10-mile stretch.

2-84. Military Planning, Shepard and Associates (1988). The Red Army (R) is trying to invade the territory defended by the Blue Army (B). Blue has three defense lines and 200 regular combat units and can draw also on a reserve pool of 200 units. Red plans to attack on two fronts, north and south. Blue has set up three east-west defense lines, I, II, and III. The purpose of defense lines 1 and 2 is to delay the Red Army attack by at least 4 days in each line and to maximize the total duration of the battle. The advance time of the Red Army is estimated by the following empirical formula:

$$
\text{ Battle duration in days } = a + b\left( \frac{\text{ Blue units }}{\text{ Red units }}\right)
$$

The constants $a$ and $b$ are a function of the defense line and the north/south front as the following table shows:


|  | $a$ - I | II | III | $b$ - I | II | III |
| --- | --- | --- | --- | --- | --- | --- |
| North front | .5 | .75 | .55 | 8.8 | 7.9 | 10.2 |
| South front | 1.1 | 1.3 | 1.5 | 10.5 | 8.1 | 9.2 |


The Blue Army reserve units can be used in defense lines II and III only. The allocation of units by the Red Army to the three defense lines is given in the following table:


|  | Number of Red Army attack units - Defense line 1 | Defense line 2 | Defense line 3 |
| --- | --- | --- | --- |
| North front | 30 | 60 | 20 |
| South front | 30 | 40 | 20 |


How should Blue allocate its resources among the three defense lines and the north/south fronts?

2-85. Water Quality Management, Stark and Nicholes (1972). Four cities discharge wastewater into the same stream. City 1 is upstream, followed downstream by city 2, then city 3, and then city 4. Measured alongside the stream, the cities are approximately 15 miles apart. A measure of the amount of pollutants in wastewater is the BOD (biochemical oxygen demand), which is the weight of oxygen required to stabilize the waste constituent in water. A higher BOD indicates worse water quality. The EPA sets a maximum allowable BOD loading, expressed in lb BOD per gallon. The removal of pollutants from wastewater takes place in two forms: (1) natural decomposition activity stimulated by the oxygen in the air, and (2) treatment plants at the points of discharge before the waste reaches the stream. The objective is to determine the most economical efficiency of each of the four plants that will reduce BOD to acceptable levels. The maximum possible plant efficiency is 99%.

To demonstrate the computations involved in the process, consider the following definitions for plant 1:

${Q}_{1} =$ Stream flow (gal/hr) on the 15-mile reach 1-2 leading to city 2

${p}_{1} =$ BOD discharge rate (in lb/hr)

$$
{x}_{1} = \text{ efficiency of plant }1\left( { \leq  {.99}}\right)
$$

${b}_{1} =$ maximum allowable BOD loading in reach 1-2 (in lb BOD/gal)

To satisfy the BOD loading requirement in reach 1-2, we must have

$$
{p}_{1}\left( {1 - {x}_{1}}\right)  \leq  {b}_{1}{Q}_{1}
$$

In a similar manner, the BOD loading constraint for reach 2-3 takes the form

$$
\left( {1 - {r}_{12}}\right) \left( \begin{matrix} \text{ BOD discharge } \\  \text{ rate in reach }1 - 2 \end{matrix}\right)  + \left( \begin{matrix} \text{ BOD discharge } \\  \text{ rate in reach }2 - 3 \end{matrix}\right)  \leq  {b}_{2}{Q}_{2}
$$

or

$$
\left( {1 - {r}_{12}}\right) {p}_{1}\left( {1 - {x}_{1}}\right)  + {p}_{2}\left( {1 - {x}_{2}}\right)  \leq  {b}_{2}{Q}_{2}
$$

The coefficient ${r}_{12}\left( { < 1}\right)$ represents the fraction of waste removed in reach 1-2 by decomposition. For reach 2-3, the constraint is

$$
\left( {1 - {r}_{23}}\right) \left\lbrack  {\left( {1 - {r}_{12}}\right) {p}_{1}\left( {1 - {x}_{1}}\right)  + {p}_{2}\left( {1 - {x}_{2}}\right) }\right\rbrack   + {p}_{3}\left( {1 - {x}_{3}}\right)  \leq  {b}_{3}{Q}_{3}
$$

Determine the most economical efficiency for the four plants using the following data (the fraction of BOD removed by decomposition is 6% for all four reaches):


|  | Reach 1-2 (i = 1) | Reach 2-3 (i = 2) | Reach 2-3 (i = 3) | Reach 3-4 (i = 4) |
| --- | --- | --- | --- | --- |
| ${Q}_{i}$ (gal/hr) | 215,000 | 220,000 | 200,000 | 210,000 |
| ${p}_{i}\left( {\mathrm{{lb}}/\mathrm{{hr}}}\right)$ | 500 | 3,000 | 6,000 | 1,000 |
| ${b}_{i}$ (lb BOD/gal) | .00085 | .0009 | .0008 | .0008 |
| Treatment cost / (\$/lb BOD removed) | .20 | .25 | .15 | .18 |


2-86. Loading Structure, Stark and Nichole (1972). The overhead crane in Figure 2.14 with two lifting yokes is used to transport mixed concrete to a yard for casting concrete barriers.

FIGURE 2.14

Overhead crane with two yokes (Problem 2-86)

![bo_d56m43v7aajc73800n2g_52_408_1653_1141_522_0.jpg](bo_d56m43v7aajc73800n2g_52_408_1653_1141_522_0.jpg)

The concrete bucket hangs at midpoint from the yoke. The crane end rails can support a maximum of 25 kip each, and the yoke cables have a 20-kip capacity each. Determine the maximum load capacity, ${W}_{1}$ and ${W}_{2}$ . (Hint: At equilibrium, the sum of moments about any point on the girder or yoke is zero.)

2-87. Allocation of Aircraft to Routes. Consider the problem of assigning aircraft to four routes according to the following data:


| Aircraft type | Capacity (passengers) | Number of aircraft | Number of daily trips on route - 1 | 2 | 3 | 4 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 50 | 5 | 3 | 2 | 2 | 1 |
| 2 | 30 | 8 | 4 | 3 | 3 | 2 |
| 3 | 20 | 10 | 5 | 5 | 4 | 2 |
| Daily number of customers |  |  | 1000 | 2000 | 900 | 1200 |


The associated costs, including the penalties for losing customers because of space unavailability, are:


| Aircraft type | Operating cost (\$) per trip on route - 1 | 2 | 3 | 4 |
| --- | --- | --- | --- | --- |
| 1 | 1000 | 1100 | 1200 | 1500 |
| 2 | 800 | 900 | 1,000 | 1000 |
| 3 | 600 | 800 | 800 | 900 |
| Penalty (\$) per lost customer | 40 | 50 | 45 | 70 |


Determine the optimum allocation of aircraft to routes, and determine the associated number of trips.
