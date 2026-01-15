## CHAPTER 9 Integer Linear Programming

## Real-Life Application-Optimizing Trailer Payloads at PFG Building Glass

PFG uses specially equipped (fifth-wheel) trailers to deliver packs of sheets of flat glass to customers. The packs vary in both size and weight, and a single trailer load may include different packs, depending on received orders. Government regulations set maximum limits on axle weights, and the actual positioning of the packs on the trailer is crucial in determining these weights. The problem deals with determining the optimal loading of the packs on the trailer bed to satisfy axle-weight limits. The problem is solved as an integer program. Case 7 in Chapter 26 on the website provides the details of the study. ${}^{1}$

### 9.1 ILLUSTRATIVE APPLICATIONS

Integer linear program (ILP) applications generally fall into two categories: direct and transformed. In the direct category, the nature of the situation precludes assigning fractional values to the variables of the model. For example, the problem may involve determining whether or not a project is undertaken (binary variable) or finding the optimal number of machines needed to perform a task (general integer variable). In the transformed category, auxiliary integer variables are used to convert analytically intractable situations into models that can be solved by available optimization algorithms. For example, in sequencing two jobs, $A$ and $B$ , on a single machine, job $A$ may precede job $B$ or vice versa. The or-constraints make the problem analytically intractable because all mathematical programming algorithms deal with and-constraints only. Section 9.1.4 shows how auxiliary binary variables are used to transform the or-constraints into and-constraints without altering the nature of the model.

---

${}^{1}$ Cases at the end of Chapters 7 and 8 use ILP. Also, case 17 in Chapter 26 on the website combines integer programming and queueing theory.

---

For convenience, a problem is defined as a pure integer program when all the variables are integer. Else, it is a mixed integer program involving a mixture of integer and continuous variables.

#### 9.1.1 Capital Budgeting

Decisions about whether or not to undertake a project is usually made under limited-budget considerations and preset priorities. The next example deals with one of these situations.

## Example 9.1-1 (Project Selection)

Five projects are being evaluated over a 3-year planning horizon. The following table gives the expected returns for each project and the associated yearly expenditures:

<table><tr><td rowspan="2">Project</td><td colspan="3">Expenditures (\$ million)/year</td><td rowspan="2">Returns (\$ million)</td></tr><tr><td>1</td><td>2</td><td>3</td></tr><tr><td>1</td><td>5</td><td>1</td><td>8</td><td>20</td></tr><tr><td>2</td><td>4</td><td>7</td><td>10</td><td>40</td></tr><tr><td>3</td><td>3</td><td>9</td><td>2</td><td>20</td></tr><tr><td>4</td><td>7</td><td>4</td><td>1</td><td>15</td></tr><tr><td>5</td><td>8</td><td>6</td><td>10</td><td>30</td></tr><tr><td>Available funds (\$ million)</td><td>25</td><td>25</td><td>25</td><td></td></tr></table>

Which projects should be selected over the 3-year horizon?

The problem reduces to a "yes-no" decision for each project. Define the binary variable ${x}_{j}$ as

$$
{x}_{j} = \left\{  \begin{array}{l} 1,\text{ if project }j\text{ is selected } \\  0,\text{ if project }j\text{ is not selected } \end{array}\right.
$$

The ILP model is

$$
\text{ Maximize }z = {20}{x}_{1} + {40}{x}_{2} + {20}{x}_{3} + {15}{x}_{4} + {30}{x}_{5}
$$

subject to

$$
5{x}_{1} + 4{x}_{2} + 3{x}_{3} + 7{x}_{4} + 8{x}_{5} \leq  {25}
$$

$$
{x}_{1} + 7{x}_{2} + 9{x}_{3} + 4{x}_{4} + 6{x}_{5} \leq  {25}
$$

$$
8{x}_{1} + {10}{x}_{2} + 2{x}_{3} + {x}_{4} + {10}{x}_{5} \leq  {25}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} = \left( {0,1}\right)
$$

The optimum integer solution (obtained by AMPL, Solver, or TORA) ${}^{2}$ is ${x}_{1} = {x}_{2} = \; {x}_{3} = {x}_{4} = 1,{x}_{5} = 0$ , with $z = {95}$ (\$ million). The solution excludes project 5 from the product mix.

---

${}^{2}$ To use TORA, select Integer Programming from Main Menu. After entering the problem data, go to output screen, and select Automated B&B to obtain the optimum solution. Solver use is the same as in LP except that the targeted variables must be declared integer. The integer option (int or bin) is available in the Solver Parameters dialogue box when you add a new constraint. AMPL implementation for integer programming is the same as in linear programming, except that some or all the variables are declared integers by adding the key word integer (or binary) in the definition statement of the targeted variables. For example, the statement var $x\{ J\}  >  = 0$ , integer; declares ${x}_{j}$ as nonnegative integer for all ${j\varepsilon J}$ . If ${x}_{j}$ is binary, the statement is changed to var x\{J\} binary;.For execution, the statement option solver cplex; must precede solve;.

---

Remarks. It is interesting to compare the continuous LP solution with the ILP solution. The LP optimum, obtained by replacing ${x}_{j} = \left( {0,1}\right)$ with $0 \leq  {x}_{j} \leq  1$ for all $j$ , yields ${x}_{1} = {.5789}$ , ${x}_{2} = {x}_{3} = {x}_{4} = 1,{x}_{5} = {.7368}$ , and $z = {108.68}$ (\$ million). The solution is meaningless because binary ${x}_{1}$ and ${x}_{5}$ assume fractional values. We may round the solution to the closest integer, which yields ${x}_{1} = {x}_{5} = 1$ . However, the resulting solution violates the constraints. Moreover, the concept of rounding is meaningless here because ${x}_{j}$ represents a "yes-no" decision.

#### 9.1.2 Set-Covering Problem

In this class of problems, overlapping services are offered by a number of installations to a number of facilities. The objective is to determine the minimum number of installations that will cover (i.e., satisfy the service needs of)-each facility. For example, water treatment plants can be constructed at various locations, with each plant serving specific communities. The overlapping occurs when more than one plant can serve a given community.

## Example 9.1-2 (Installing Security Telephones)

To promote on-campus safety, the U of A Public Safety Department is in the process of installing emergency telephones at selected locations. The department wants to install the minimum number of telephones that serve each of the campus main streets. Figure 9.1 maps the campus principal streets.

It is logical to maximize the utility of the telephones by placing them at street intersections. In this manner, a single unit can serve at least two streets.

Define

$$
{x}_{j} = \left\{  \begin{array}{l} 1,\text{ at telephone is installed at intersection }j, j = 1,2,\ldots ,8 \\  0,\text{ otherwise } \end{array}\right.
$$

FIGURE 9.1

Street map of the U of A campus

![bo_d56m4mf7aajc73800na0_2_481_1549_998_652_0.jpg](bo_d56m4mf7aajc73800na0_2_481_1549_998_652_0.jpg)

The constraints of the problem require installing at least one telephone on each of the 11 streets $\left( {A\text{ to }K}\right)$ . Thus, the model is

$$
\text{ Minimize }z = {x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5} + {x}_{6} + {x}_{7} + {x}_{8}
$$

subject to

$$
{x}_{1} + {x}_{2}\; \geq  1\;\left( {\text{ Street }A}\right)
$$

$$
{x}_{2} + {x}_{3} \geq  1\;\left( {\text{ Street }B}\right)
$$

$$
{x}_{4} + {x}_{5}\; \geq  1\;\left( {\text{ Street }C}\right)
$$

$$
{x}_{7} + {x}_{8} \geq  1\;\left( {\text{ Street }D}\right)
$$

$$
{x}_{6} + {x}_{7}\; \geq  1\;\left( {\text{ Street }E}\right)
$$

${x}_{2}\; + {x}_{6}\; \geq  1\;\left( {\text{ Street }F}\right) \; {x}_{1}\; + {x}_{6}\; \geq  1\;$ (Street $G$ ) ${x}_{4}\; + {x}_{7}\; \geq  1\;\left( {\text{ Street }H}\right) \; {x}_{2}\; + {x}_{4}\; \geq  1\;\left( {\text{ Street }I}\right)$

$$
{x}_{5}\; + {x}_{8} \geq  1\;\left( {\text{ Street }J}\right)
$$

$$
{x}_{3}\; + {x}_{5}\; \geq  1\;\text{ (Street }K\text{ ) }
$$

$$
{x}_{j} = \left( {0,1}\right) , j = 1,2,\ldots ,8
$$

The optimum solution of the problem requires installing four telephones at intersections 1, 2, 5, and 7.

Remarks. In the strict sense, set-covering problems are characterized by the following criteria: (1) The variables ${x}_{j}, j = 1,2,\ldots , n$ , are binary,(2) the left-hand-side coefficients of the constraints are 0 or 1,(3) the right-hand side of each constraint is of the form $\left( { \geq  1}\right)$ , and (4) the objective function minimizes ${c}_{1}{x}_{1} + {c}_{2}{x}_{2} + \ldots  + {c}_{n}{x}_{n}$ , where ${c}_{j} > 0$ for all $j = 1,2,\ldots , n$ . In the present example, ${c}_{j} = 1$ for all $j$ . If ${c}_{j}$ represents the installation cost in intersection $j$ , then these coefficients may assume values other than 1. Variations of the set-covering problem include additional side conditions, as described by some of the situations in Problems 9-19 to 9-27.

## AMPL Moment

File amplEx9.1-2.txt provides a general AMPL model for any set-covering problem. The formulation is detailed in Section C.9 on the website.

#### 9.1.3 Fixed-Charge Problem

The fixed-charge problem deals with situations in which the economic activity incurs two types of costs: a fixed cost needed to initiate the activity and a variable cost proportional to the level of the activity. For example, the initial tooling of a machine prior to starting production incurs a fixed setup cost regardless of how many units are manufactured. Once the setup is done, the cost of labor and material is proportional to the amount produced. Given that $F$ is the fixed charge, $c$ is the variable unit cost, and $x$ is the level of production, the cost function is expressed as

$$
C\left( x\right)  = \left\{  \begin{array}{ll} F + {cx}, & \text{ if }x > 0 \\  0, & \text{ otherwise } \end{array}\right.
$$

The function $C\left( x\right)$ is intractable analytically because it involves a discontinuity at $x = 0$ . The next example shows how auxiliary binary variables are used to render the model analytically tractable.

## Example 9.1-3 (Choosing a Telephone Company)

I have been approached by three telephone companies to subscribe to their long-distance service in the United States. MaBell will charge a flat \$16 per month plus \$.25 a minute. PaBell will charge \$25 a month but will reduce the per-minute cost to \$.21. As for BabyBell, the flat monthly charge is \$18, and the cost per min is \$.22. I usually make an average of 200 minutes of long-distance calls a month. Assuming that I do not pay the flat monthly fee unless I make calls and that I can apportion my calls among all three companies as I please, how should I use the three companies to minimize my monthly telephone bill?

This problem can be solved readily without ILP. Nevertheless, it is instructive to formulate it as an integer program.

Define

$$
{x}_{1} = \text{ MaBell long-distance minutes per month }
$$

$$
{x}_{2} = \text{ PaBell long-distance minutes per month }
$$

$$
{x}_{3} = \text{ BabyBell long-distance minutes per month }
$$

$$
{y}_{1} = 1\text{ if }{x}_{1} > 0\text{ and 0 if }{x}_{1} = 0
$$

$$
{y}_{2} = 1\text{ if }{x}_{2} > 0\text{ and 0 if }{x}_{2} = 0
$$

$$
{y}_{3} = 1\text{ if }{x}_{3} > 0\text{ and 0 if }{x}_{3} = 0
$$

We can ensure that ${y}_{j}$ equals 1 when ${x}_{j}$ is positive by using the constraint

$$
{x}_{j} \leq  M{y}_{j}, j = 1,2,3
$$

The value of $M$ should be selected sufficiently large so as not to restrict the variable ${x}_{j}$ artificially. Because I make about 200 minutes of calls a month, then ${x}_{j} \leq  {200}$ for all $j$ , and it is safe to select $M = {200}$ .

The complete model is

$$
\text{ Minimize }z = {.25}{x}_{1} + {.21}{x}_{2} + {.22}{x}_{3} + {16}{y}_{1} + {25}{y}_{2} + {18}{y}_{3}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} = {200}
$$

$$
{x}_{1} \leq  {200}{y}_{1}
$$

$$
{x}_{2} \leq  {200}{y}_{2}
$$

$$
{x}_{3} \leq  {200}{y}_{3}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

$$
{y}_{1},{y}_{2},{y}_{3} = \left( {0,1}\right)
$$

The formulation shows that the $j$ th monthly flat fee will be part of the objective function $z$ only if ${y}_{j} = 1$ , which can happen only if ${x}_{j} > 0$ (per the last three constraints of the model). If ${x}_{i} = 0$ at the optimum, then the minimization of $z$ , together with the fact that the objective coefficient of ${y}_{j}$ is positive, forces ${y}_{j}$ to equal zero, as desired. ${}^{3}$

The optimum solution yields ${x}_{3} = {200},{y}_{3} = 1$ , and all the remaining variables equal to zero, which shows that BabyBell should be selected as my long-distance carrier. Remember that the information conveyed by ${y}_{3} = 1$ is redundant because the same result is implied by ${x}_{3} > 0\left( { = {200}}\right)$ . Actually, the main reason for using ${y}_{1},{y}_{2}$ , and ${y}_{3}$ is to account for the monthly flat fee. In effect, the three binary variables convert an ill-behaved (nonlinear) model into an analytically tractable formulation. This conversion has resulted in introducing the integer (binary) variables in an otherwise continuous problem.

#### 9.1.4 Either-Or and If-Then Constraints

In the fixed-charge problem (Section 9.1.3), auxiliary binary variables are used to handle the discontinuity in the objective cost function. This section deals with models in which constraints are not satisfied simultaneously (either-or) or are dependent (if-then), again using auxiliary binary variables. The transformation uses a mathematical trick to present the special constraint as and-constraints.

## Example 9.1-4 (Job Sequencing Model)

Jobco uses a single machine to process three jobs. Both the processing time and the due date (in days) for each job are given in the following table. The due dates are measured from zero, the assumed start time of the first job.

<table><tr><td>Job</td><td>Processing time (day)</td><td>Due date (day)</td><td>Late penalty (\$/day)</td></tr><tr><td>1</td><td>5</td><td>25</td><td>19</td></tr><tr><td>2</td><td>20</td><td>22</td><td>12</td></tr><tr><td>3</td><td>15</td><td>35</td><td>34</td></tr></table>

The objective of the problem is to determine the job sequence that minimizes the late penalty for processing all three jobs.

Define

$$
{x}_{j} = \text{ Start date in days for job }j\text{ (measured from time zero) }
$$

$$
{y}_{ij} = \left\{  \begin{array}{l} 1,\text{ if }i\text{ precedes }j \\  0,\text{ if }j\text{ precedes }i \end{array}\right.
$$

The problem has two types of constraints: the noninterference constraints (guaranteeing that no two jobs are processed concurrently) and the due-date constraints. Consider the noninterference constraints first.

---

${}^{3}$ For generalization, the condition ${y}_{i} = 0$ if ${x}_{i} = 0$ can be replaced with the compound condition ${y}_{i} = 1$ if ${x}_{i} > 0$ and 0 if ${x}_{i} = 0$ to make it independent of the sense of optimization (maximization or minimization). The result is achieved by replacing the constraint ${x}_{i} \leq  M{y}_{i}$ with $\frac{{x}_{i}}{M} \leq  {y}_{i} \leq  {x}_{i}$ .

---

Two jobs $i$ and $j$ with processing time ${p}_{i}$ and ${p}_{j}$ will not be processed concurrently if (depending on whether which job is processed first)

$$
{x}_{i} \geq  {x}_{j} + {p}_{j}\text{ or }{x}_{j} \geq  {x}_{i} + {p}_{i}
$$

For $M$ sufficiently large, the or-constraints are converted to and-constraints by using

$$
M{y}_{ij} + \left( {{x}_{i} - {x}_{j}}\right)  \geq  {p}_{j}\text{ and }M\left( {1 - {y}_{ij}}\right)  + \left( {{x}_{j} - {x}_{i}}\right)  \geq  {p}_{i}
$$

The conversion guarantees that only one of the two constraints can be active at any one time. If ${y}_{ij} = 0$ , the first constraint is active, and the second is redundant (because its left-hand side will include $M$ , which is much larger than ${p}_{i}$ ). If ${y}_{ij} = 1$ , the first constraint is redundant, and the second is active.

Next, given that ${d}_{j}$ is the due date for job $j$ , the job is late if ${x}_{j} + {p}_{j} > {d}_{j}$ . We can use two nonnegative variables, ${s}_{j}^{ - }$ and ${s}_{j}^{ + }$ , to determine the status of a completed job $j$ with regard to its due date - namely, the due date constraint can be written as

$$
{x}_{j} + {p}_{j} + {s}_{j}^{ - } - {s}_{j}^{ + } = {d}_{j}
$$

Job $j$ is ahead of schedule if ${s}_{j}^{ - } > 0$ , and late if ${s}_{j}^{ + } > 0$ . The late-penalty cost is thus proportional to ${s}_{j}^{ + }$ .

The model for the given problem is

$$
\text{ Minimize }z = {19}{s}_{1}^{ + } + {12}{s}_{2}^{ + } + {34}{s}_{3}^{ + }
$$

subject to

$$
{x}_{1} - {x}_{2}\; + M{y}_{12}
$$

$$
\geq  {20}
$$

$$
- {x}_{1} + {x}_{2}\; - M{y}_{12}
$$

$$
\geq  5 - M
$$

$$
{x}_{1}\; - {x}_{3}\; + M{y}_{13}
$$

$$
\geq  {15}
$$

$$
\begin{array}{l}  - {x}_{1}\; + {x}_{3}\; - M{y}_{13} \\  \end{array}
$$

$$
\geq  5 - M
$$

${x}_{2} - {x}_{3}$

$$
\geq  {15}
$$

$- {x}_{2} + {x}_{3}$

$$
\geq  {20} - M
$$

${x}_{1} \; + {s}_{1}^{ - } - {s}_{1}^{ + }$

${x}_{2}$

$$
+ {s}_{2}^{ - } - {s}_{2}^{ + }\; = {22} - {20}
$$

${x}_{3}$

$$
+ {s}_{3}^{ - } - {s}_{3}^{ + } = {35} - {15}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{s}_{1}^{ - },{s}_{1}^{ + },{s}_{2}^{ - },{s}_{2}^{ + },{s}_{3}^{ - },{s}_{3}^{ + } \geq  0
$$

$$
{y}_{12},{y}_{13},{y}_{23} = \left( {0,1}\right)
$$

The resulting model is a mixed ILP.

To solve the model, we choose $M = {100}$ , a value that is larger than the sum of the processing times for all three activities. The optimal solution is ${x}_{1} = {20},{x}_{2}, = 0$ , and ${x}_{3} = {25}$ , This means that job 2 starts at time 0 , job 1 starts at time 20 , and job 3 starts at time 25 , thus yielding the optimal processing sequence $2 \rightarrow  1 \rightarrow  3$ . The solution calls for completing job 2 at time $0 + {20} = {20}$ , job 1 at time $= {20} + 5 = {25}$ , and job 3 at ${25} + {15} = {40}$ days. Job 3 is delayed by ${40} - {35} = 5$ days past its due date at a cost of $5 \times  \$ {34} = \$ {170}$ .

## AMPL Moment

File amplEx9.1-4.txt provides the AMPL model for the problem of Example 9.1-4. The model is explained in Section C.9 on the website.

## Example 9.1-5 (Job Sequencing Model Revisited)

In Example 9.1-4, suppose that we have the following additional condition: If job $i$ precedes job $j$ , then job $k$ must precede job $m$ . Mathematically, the if-then condition is written as

$$
\text{ if }{x}_{i} + {p}_{i} \leq  {x}_{j}\text{ , then }{x}_{k} + {p}_{k} \leq  {x}_{m}
$$

Given $\varepsilon \left( { > 0}\right)$ infinitesimally small, and $M$ sufficiently large, this condition is equivalent to the following two simultaneous constraints:

$$
{x}_{j} - \left( {{x}_{i} + {p}_{i}}\right)  \leq  M\left( {1 - w}\right)  - \varepsilon
$$

$$
\left( {{x}_{k} + {p}_{k}}\right)  - {x}_{m} \leq  {Mw}
$$

$$
w = \left( {0,1}\right)
$$

If ${x}_{i} + {p}_{i} \leq  {x}_{j}$ , then ${x}_{j} - \left( {{x}_{i} + {p}_{i}}\right)  \geq  0$ , which requires $w = 0$ , and the second constraint becomes ${x}_{k} + {p}_{k} \leq  {x}_{m}$ , as desired. Else, $w$ may assume the value 0 or 1, in which case the second constraint may or may not be satisfied, depending on other conditions in the model.

### 9.2 INTEGER PROGRAMMING ALGORITHMS

The ILP algorithms are based on exploiting the tremendous computational success of LP. The strategy of these algorithms involves three steps.

Step 1. Relax the solution space of the ILP by deleting the integer restriction on all integer variables and replacing any binary variable $y$ with the continuous range $0 \leq  y \leq  1$ . The result of the relaxation is a regular LP.

Step 2. Solve the LP, and identify its continuous optimum.

Step 3. Starting from the continuous optimum point, add special constraints that iteratively modify the LP solution space in a manner that eventually renders an optimum extreme point satisfying the integer requirements.

Two general methods have been developed for generating the special constraints in step 3.

1. Branch-and-bound (B&B) method

2. Cutting-plane method

Neither method is consistently effective computationally. However, experience shows that the B&B method is far more successful than the cutting-plane method.

#### 9.2.1 Branch-and-Bound (B&B) Algorithm ${}^{4}$

The first B&B algorithm was developed in 1960 by A. Land and G. Doig for the general mixed and pure ILP problem. Later, in 1965, E. Balas developed the additive algorithm for solving ILPs with pure binary (zero or one) variables. ${}^{5}$ The additive algorithm’s computations were so simple (mainly addition and subtraction) that it was initially hailed as a possible breakthrough in the solution of general ILP. Unfortunately, it failed to produce the desired computational advantages. Moreover, the algorithm, which initially appeared unrelated to the B&B technique, was shown to be but a special case of the general Land and Doig algorithm.

This section presents the general Land-Doig B&B algorithm only. A numeric example is used to provide the details.

Example 9.2-1

$$
\text{ Maximize }z = 5{x}_{1} + 4{x}_{2}
$$

subject to

$$
{x}_{1} + {x}_{2} \leq  5
$$

$$
{10}{x}_{1} + 6{x}_{2} \leq  {45}
$$

$$
{x}_{1},{x}_{2}\text{ nonnegative integer }
$$

The lattice points (dots) in Figure 9.2 define the ILP solution space. The associated continuous LP1 problem at node 1 (shaded area) is defined from ILP by removing the integer restrictions. The optimum solution of LP1 is ${x}_{1} = {3.75},{x}_{2} = {1.25}$ , and $z = {23.75}$ .

Because the optimum LP1 solution does not satisfy the integer restrictions, the solution space is subdivided in a systematic manner that eventually locates the ILP optimum. First, B&B selects an integer variable whose optimum value at LP1 is not integer. In this example, both ${x}_{1}$ and ${x}_{2}$ qualify. Selecting ${x}_{1}\left( { = {3.75}}\right)$ arbitrarily, the region $3 < {x}_{1} < 4$ of the LP1 solution space contains no integer values of ${x}_{1}$ , and thus it can be deleted. This is equivalent to replacing the original LP1 with two new LPs:

$$
\text{ LP2 space } = \text{ LP1 space } + \left( {{x}_{1} \leq  3}\right)
$$

$$
\text{ LP3 space } = \text{ LP1 space } + \left( {{x}_{1} \geq  4}\right)
$$

Figure 9.3 depicts the LP2 and LP3 spaces. The two spaces combined contain the same feasible integer points as the original ILP-meaning that no information is lost when LP1 is replaced with LP2 and LP3. gives rise to the concept of branching in the B&B algorithm. In this case, ${x}_{1}$ is called the branching variable.

---

${}^{4}$ TORA integer programming module is equipped with a facility for generating the B&B tree interactively. To use this facility, select User-guided B&B in the output screen of the integer programming module. The resulting screen provides all the information needed to create the B&B tree.

${}^{5}$ A general ILP can be expressed in terms of binary (0-1) variables as follows. Given an integer variable $x$ with a finite upper bound $u$ (i.e., $0 \leq  x \leq  u$ ), then

$$
x = {2}^{0}{y}_{0} + {2}^{1}{y}_{1} + {2}^{2}{y}_{2} + \ldots  + {2}^{k}{y}_{k}
$$

The variables ${y}_{0},{y}_{1},\ldots$ , and ${y}_{\mathrm{k}}$ are binary, and the index $k$ is the smallest integer satisfying ${2}^{k + 1} - 1 \geq  u$ .

---

![bo_d56m4mf7aajc73800na0_9_148_195_1309_1658_0.jpg](bo_d56m4mf7aajc73800na0_9_148_195_1309_1658_0.jpg)

If we intelligently impose sequential constraints that exclude the integer-free regions (e.g., $3 < {x}_{1} < 4$ in LP1), we will be reducing the continuous solution space of LP1 into a number of LP subproblems whose optimum extreme points satisfy the integer restrictions. The best of these subproblems is the optimum solution of ILP.

The new restrictions, ${x}_{1} \leq  3$ and ${x}_{1} \geq  4$ , are mutually exclusive, so that LP2 and LP3 at nodes 2 and 3 must be dealt with as separate LPs, as Figure 9.4 shows. This dichotomization

![bo_d56m4mf7aajc73800na0_10_548_202_862_535_0.jpg](bo_d56m4mf7aajc73800na0_10_548_202_862_535_0.jpg)

FIGURE 9.4

Using branching variable ${x}_{1}$ to create LP2 and LP3 for Example 9.2-1

The optimum ILP lies in either LP2 or LP3. Hence, both subproblems must be examined. We arbitrarily examine LP2 (associated with ${x}_{1} \leq  3$ ) first:

$$
\text{ Maximize }z = 5{x}_{1} + 4{x}_{2}
$$

subject to

$$
{x}_{1} + {x}_{2} \leq  5
$$

$$
{10}{x}_{1} + 6{x}_{2} \leq  {45}
$$

$$
{x}_{1} \leq  3
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The solution of LP2 (which can be solved efficiently by the upper-bounded algorithm of Section 7.3) is ${x}_{1} = 3,{x}_{2} = 2$ , and $z = {23}$ . The LP2 solution satisfies the integer requirements for ${x}_{1}$ and ${x}_{2}$ . Hence, LP2 is said to be fathomed-meaning it cannot yield any better ILP solution and no further branching from node 2 is required.

We cannot say at this point that the integer solution obtained from LP2 is optimum for the original problem, because LP3 may yield a better integer solution. All we can say is that $z = {23}$ is a lower bound on the optimum (maximum) objective value of the original ILP. This means that any unexamined subproblem that cannot yield a better objective value than the lower bound must be discarded as nonpromising. If an unexamined subproblem produces a better integer solution, then the lower bound must be updated accordingly.

Given the lower bound $z = {23}$ , we examine LP3 (the only remaining unexamined subproblem at this point). Because optimum $z = {23.75}$ at LP1 and all the coefficients of the objective function happen to be integers, it is impossible that LP3 can produce a better integer solution (with $z > {23}$ ). As a result, we discard LP3 and conclude that it has been fathomed.

The B&B algorithm is now complete because both LP2 and LP3 have been examined and fathomed, the first for producing an integer solution and the second for failing to produce a better integer solution. We thus conclude that the optimum ILP solution is the one associated with the lower bound-namely, ${x}_{1} = 3,{x}_{2} = 2$ , and $z = {23}$ .

Two questions remain unanswered regarding the algorithm:

1. At LP1, could we have selected ${x}_{2}$ as the branching variable in place of ${x}_{1}$ ?

2. When selecting the next subproblem to be examined, could we have solved LP3 first instead of LP2?

The answer to both questions is "yes," but ensuing computations may differ dramatically. Figure 9.5 demonstrates this point. Suppose that we examine LP3 first (instead of LP2 as we did in Figure 9.4). The solution is ${x}_{1} = 4,{x}_{2} = {.83}$ , and $z = {23.33}$ (verify!). Because ${x}_{2}\left( { = {.83}}\right)$ is noninteger, LP3 is examined further by creating subproblems LP4 and LP5 using the branches ${x}_{2} \leq  0$ and ${x}_{2} \geq  1$ , respectively. This means that

$$
\text{ LP4 space } = \text{ LP3 space } + \left( {{x}_{2} \leq  0}\right)
$$

$$
= \text{ LP1 space } + \left( {{x}_{1} \geq  4}\right)  + \left( {{x}_{2} \leq  0}\right)
$$

$$
\text{ LP5 space } = \text{ LP3 space } + \left( {{x}_{2} \geq  1}\right)
$$

$$
= \mathrm{{LP}}1\text{ space } + \left( {{x}_{1} \geq  4}\right)  + \left( {{x}_{2} \geq  1}\right)
$$

FIGURE 9.5

Alternative B&B tree for Example 9.2-1

![bo_d56m4mf7aajc73800na0_11_382_940_1107_1224_0.jpg](bo_d56m4mf7aajc73800na0_11_382_940_1107_1224_0.jpg)

We now have three "dangling" subproblems to be examined: LP2, LP4, and LP5. Suppose that we arbitrarily examine LP5 first. LP5 has no feasible solution, and hence it is fathomed. Next, let us examine LP4. The optimum solution is ${x}_{1} = {4.5},{x}_{2} = 0$ , and $z = {22.5}$ . The nonin-teger value of ${x}_{1}$ leads to the two branches ${x}_{1} \leq  4$ and ${x}_{1} \geq  5$ and the creation of subproblems LP6 and LP7 from LP4.

$$
\text{ LP6 space } = \text{ LP1 space } + \left( {{x}_{1} \geq  4}\right)  + \left( {{x}_{2} \leq  0}\right)  + \left( {{x}_{1} \leq  4}\right)
$$

$$
\text{ LP7 space } = \text{ LP1 space } + \left( {{x}_{1} \geq  4}\right)  + \left( {{x}_{2} \leq  0}\right)  + \left( {{x}_{1} \geq  5}\right)
$$

Now, subproblems LP2, LP6, and LP7 remain unexamined. Selecting LP7 for examination, the problem is fathomed because it has no feasible solution. Next, we select LP6. The problem yields the first integer solution $\left( {{x}_{1} = 4,{x}_{2} = 0, z = {20}}\right)$ , and, thus provide the first lower bound $\left( { = {20}}\right)$ on the optimum ILP objective value. We are now left with subproblem LP2, and it yields a better integer solution $\left( {{x}_{1} = 3,{x}_{2} = 2, z = {23}}\right)$ . Thus, the lower bound is updated from $z = {20}$ to $z = {23}$ . At this point, all the subproblems have been fathomed (examined), and the optimum solution is the one associated with the most up-to-date lower bound-namely, ${x}_{1} = 3,{x}_{2} = 2$ , and $z = {23}$ .

The solution sequence in Figure 9.5 (LP1 $\rightarrow$ LP3 $\rightarrow$ LP5 $\rightarrow$ LP4 $\rightarrow$ LP7 $\rightarrow$ LP6 $\rightarrow$ LP2) is intentionally selected to dramatize a worst-case scenario that, nevertheless, may well occur in practice. In Figure 9.4, we were lucky to "stumble" upon a good lower bound at the very first subproblem (LP2), and that in turn allowed us to fathom LP3 without further examination. In essence, we completed the procedure by solving a total of two LPs. In Figure 9.5, the story is different; we solved seven LPs to terminate the B&B algorithm.

## AMPL Moment

AMPL can be used interactively to generate the B&B search tree. The following table shows the sequence of commands needed to generate the tree of Example 9.2-1 (Figure 9.5) starting with the continuous LP1. AMPL model (file amplEx9.2-1.txt) has two variables $\times  1$ and $\times  2$ and two constraints c0 and c1. You will find it helpful to synchronize the AMPL commands with the branches in Figure 9.5.

<table><tr><td>AMPL command</td><td>Result</td></tr><tr><td>ampl: model amplEx9.2-1.txt;solve;display x1, x2;</td><td>$\operatorname{LP1}\left( {{x}_{1} = {3.75},{x}_{2} = {1.25}}\right)$</td></tr><tr><td>ampl: c2:x1>=4;solve;display x1, x2;</td><td>$\operatorname{LP3}\left( {{x}_{1} = 4,{x}_{2} = {.83}}\right)$</td></tr><tr><td>ampl: c3:x2>=1;solve;display x1, x2;</td><td>LP5 (no solution)</td></tr><tr><td>ampl: drop c3; c4: x2<=0; solve; display x1, x2;</td><td>$\operatorname{LP4}\left( {{x}_{1} = {4.5},{x}_{2} = 0}\right)$</td></tr><tr><td>ampl: c5:x1>=5;solve;display x1, x2;</td><td>LP7 (no solution)</td></tr><tr><td>ampl: drop c5;c6:x1<=4;solve;display x1, x2;</td><td>$\operatorname{LP6}\left( {{x}_{1} = 4,{x}_{2} = 0}\right)$</td></tr><tr><td>ampl: drop c2;drop c4;drop c6;c7:x1<=3; solve; display x1, x2; LP2 $\left( {{x}_{1} = 3,{x}_{2} = 2}\right)$</td><td></td></tr></table>

## Solver Moment

Solver can be used to obtain the solution of the different subproblems by using the add/change/ delete options in the Solver Parameters dialogue box.

Remarks. Example 9.2-1 points to a principal weakness in the B&B algorithm: Given multiple choices, how do we select the next subproblem and its branching variable? In answering this question, there is but one goal in mind: Find a (good) feasible integer solution ASAP! This goal, though stated qualitatively, is of paramount importance. The reason is simple: finding a (good) feasible integer solution early on in the search tree can obviate exploring subproblems and hence speed up the termination of the search. But how can a (good) feasible solution be found? There are three possibilities:

1. Use a rounded LP optimal solution if feasibility can be ascertained.

2. Use heuristic programming to find a good feasible solution (see Chapter 10).

3. Use appropriate heuristics to select the next subpoblem and its branching variable.

The first possibility is at best iffy, particularly in large models with equality constraints. The second is plausible though costly computationally, and the third is where most of the research has been concentrated.

The overall idea of the third strategy is based on two broad options with marked trade-offs: (1) A high-echelon subproblem (closer to the start of the search tree) is more likely to produce a tighter objective bound (because it is closer-hence less additional constraints-to the continuous LP optimum), but less likely to produce a feasible integer solution (because of the smaller number of integer-branching constraints leading to the subproblem). (2) Conversely, a low-echelon subproblem is more likely to produce a feasible integer solution but less likely to generate a tight objective value bound. In essence, the first option explores the subproblems horizontally in one echelon before moving to the next echelon, whereas the second option explores the subproblems (sort of) vertically. But the two options still do not address how a branching variable is selected at each subproblem.

Although heuristics are available for the selection of both the next subproblem and its branching variable, computational experience shows that the effectiveness of these heuristics is data-dependent. In view of this difficulty, ILP software is usually not sufficiently sophisticated to be used as an input-output black box as in LP software; meaning there are cases where manual intervention is needed to "tweak" the B&B search. For example, the search may alternate periodically between horizontal and vertical selection of the next subproblem in hope of encountering a good objective value bound. Indeed all available commercial ILP packages allow this manual intervention. A typical example is demonstrated by the commands used in the AMPL moment following Example 9.2-1.

The fact remains that integer programming algorithms are not totally reliable. But perhaps their performance can be improved by tweaking the ILP model itself. One possibility is to seek a formulation with the smallest possible number of integer variable (i.e., approximating some of the integer variables with continuous ones). Another is to tighten the feasible ranges on the integer variables as much as possible. And a third is to use a different solution venue altogether (e.g., knapsack problems can be formulated as a shortest route network model). But perhaps the most plausible possibility is to settle for a near-optimum solution using heuristics. Chapter 10, on heuristic programming, provides three such heuristics.

Summary of the B&B Algorithm. Assume a maximization problem. Set an initial lower bound $z =  - \infty$ on the optimum objective value of ILP and set $i = {0.}^{6}$

Step 1. (Fathoming/bounding). Select LPi, the next subproblem to be examined. Solve LPi, and attempt to fathom it using one of three conditions:

(a) The optimal $z$ -value of LPi cannot yield a better objective value than the current lower bound.

(b) LPi yields a better feasible integer solution than the current lower bound.

(c) $\mathrm{{LP}}i$ has no feasible solution.

Two cases will arise.

(a) If $\mathrm{{LP}}i$ is fathomed and a better solution is found, update the lower bound. If all subproblems have been fathomed, stop; the lower bound gives the optimum solution (if no finite lower bound exists, the problem has no feasible solution). Else, set $i = i + 1$ , and repeat step 1 .

(b) If $\mathrm{{LP}}i$ is not fathomed, go to step 2 for branching.

Step 2. (Branching). Select one of the integer variables ${x}_{j}$ , whose optimum value ${x}_{j}^{ * }$ in the LPi solution is not integer. Create the two LP subproblems that correspond to

$$
{x}_{j} \leq  \left\lbrack  {x}_{j}^{ * }\right\rbrack  \text{ and }{x}_{j} \geq  \left\lbrack  {x}_{j}^{ * }\right\rbrack   + 1
$$

Set $i = i + 1$ , and go to step 1 .

The B&B algorithm can be extended to mixed problems (in which only some of the variables are integer), simply by never branching a continuous variable. A feasible subproblem provides a new bound on the objective value if the values of the discrete variables are integers with an improved objective value.

#### 9.2.2 Cutting-Plane Algorithm

As in the B&B algorithm, the cutting-plane algorithm also starts at the continuous optimum LP solution. Special constraints (called cuts) are added to the solution space in a manner that renders an integer optimum extreme point. In Example 9.2-2, we first demonstrate graphically how cuts are used to produce an integer solution and then implement the idea algebraically.

Example 9.2-2

Consider the following ILP:

$$
\text{ Maximize }z = 7{x}_{1} + {10}{x}_{2}
$$

subject to

$$
- {x}_{1} + 3{x}_{2} \leq  6
$$

$$
7{x}_{1} + {x}_{2} \leq  {35}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

---

${}^{6}$ For minimization problems, replace the lower bound with an initial upper bound $z =  + \infty$ .

---

![bo_d56m4mf7aajc73800na0_15_255_203_1303_372_0.jpg](bo_d56m4mf7aajc73800na0_15_255_203_1303_372_0.jpg)

FIGURE 9.6

Illustration of the use of cuts in ILP

Figure 9.6 gives an example of two such cuts. Initially, we start with the continuous LP optimum $z = {66}\frac{1}{2},{x}_{1} = 4\frac{1}{2},{x}_{2} = 3\frac{1}{2}$ . Next, we add cut I, which produces the (continuous) LP optimum solution $z = {62},{x}_{1} = {4}_{7}^{4},{x}_{2} = 3$ . Then, we add cut II, which (together with cut I and the original constraints) produces the integer LP optimum $z = {58},{x}_{1} = 4,{x}_{2} = 3$ .

The added cuts do not eliminate any of the original feasible integer points, but must pass through at least one feasible or infeasible integer point. These are basic requirements of any cut.

It is purely accidental that a 2-variable problem used exactly 2 cuts to reach the optimum integer solution. In general, the number of cuts, though finite, cannot be determined based on the size of the problem, in the sense that a smaller problem may require more cuts than a larger problem.

Next, we use the same example to show how the cuts are constructed and implemented algebraically. Given the slacks ${x}_{3}$ and ${x}_{4}$ for constraints 1 and 2, the optimum LP tableau is given as

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${x}_{3}$</td><td>${x}_{4}$</td><td>Solution</td></tr><tr><td>Z</td><td>0</td><td>0</td><td>63</td><td>$\frac{31}{22}$</td><td>${66}\frac{1}{2}$</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>$\frac{7}{22}$</td><td>$\frac{\frac{1}{22}}{\frac{3}{22}}$</td><td>$3\frac{1}{2}$</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>$- \frac{1}{22}$</td><td></td><td>$4\frac{1}{2}$</td></tr></table>

The optimum continuous solution is $z = {66}\frac{1}{2},{x}_{1} = 4\frac{1}{2},{x}_{2} = 3\frac{1}{2},{x}_{3} = 0,{x}_{4} = 0$ . The cut is developed under the assumption that all the variables, including all the slacks, are integers. Note also that because all the original objective coefficients are integers in this example, the value of $z$ also is integer.

The information in the optimum tableau can be written explicitly as

$$
z + \frac{63}{22}{x}_{3} + \frac{31}{22}{x}_{4} = {66}\frac{1}{2}\;\left( {z\text{ -equation }}\right)
$$

$$
{x}_{2} + \frac{7}{22}{x}_{3} + \frac{1}{22}{x}_{4} = 3\frac{1}{2}\;\left( {{x}_{2}\text{ -equation }}\right)
$$

$$
{x}_{1} - \frac{1}{22}{x}_{3} + \frac{3}{22}{x}_{4} = 4\frac{1}{2}\;\left( {{x}_{1}\text{ -equation }}\right)
$$

A constraint equation can be used as a source row for generating a cut, provided its right-hand side is fractional. Also, the $z$ -equation can be used as a source row in this example because $z$ happens to be defined by an integer expression. We will demonstrate how a cut is generated from each of these source rows, starting with the $z$ -equation.

First, we factor out all the noninteger coefficients of the equation into an integer value and a positive fractional component. For example,

$$
\frac{5}{2} = \left( {2 + \frac{1}{2}}\right)
$$

$$
- \frac{7}{3} = \left( {-3 + \frac{2}{3}}\right)
$$

The factoring of the $z$ -equation yields

$$
z + \left( {2 + \frac{19}{22}}\right) {x}_{3} + \left( {1 + \frac{9}{22}}\right) {x}_{4} = \left( {{66} + \frac{1}{2}}\right)
$$

Moving all the integer components to the left-hand side and all the fractional components to the right-hand side, we get

$$
z + 2{x}_{3} + 1{x}_{4} - {66} =  - \frac{19}{22}{x}_{3} - \frac{9}{22}{x}_{4} + \frac{1}{2} \tag{1}
$$

Because ${x}_{3}$ and ${x}_{4}$ are nonnegative (and all the fractions are positive by construction), the righthand side must satisfy the following inequality:

$$
- \frac{19}{22}{x}_{3} - \frac{9}{22}{x}_{4} + \frac{1}{2} \leq  \frac{1}{2} \tag{2}
$$

Now, because the left-hand side in Equation (1), $z + 2{x}_{3} + 1{x}_{4} - {66}$ , is an integer expression by construction, the right-hand side, $- \frac{19}{22}{x}_{3} - \frac{19}{22}{x}_{4} + \frac{1}{2}$ , must also be integer. It then follows that (2) can be replaced with the inequality:

$$
- \frac{19}{22}{x}_{3} - \frac{9}{22}{x}_{4} + \frac{1}{2} \leq  0
$$

This result is justified because an integer value less than a positive fraction must necessarily be $\leq  0$ .

The last inequality is the desired cut, and it represents a necessary (but not sufficient) condition for obtaining an integer solution. It is also referred to as the fractional cut because all its coefficients are fractions.

Because ${x}_{3} = {x}_{4} = 0$ in the optimum continuous LP tableau given above, the current continuous solution violates the cut (because it yields $\frac{1}{2} \leq  0$ ). Thus, if we add this cut to the optimum tableau, the resulting optimum extreme point moves the solution toward satisfying the integer restrictions.

Before showing how a cut is implemented in the optimal tableau, we will demonstrate how cuts can also be constructed from the constraint equations. Consider the ${x}_{1}$ -row:

$$
{x}_{1} - \frac{1}{22}{x}_{3} + \frac{3}{22}{x}_{4} = 4\frac{1}{2}
$$

Factoring out the equation, we get

$$
{x}_{1} + \left( {-1 + \frac{21}{22}}\right) {x}_{3} + \left( {0 + \frac{3}{22}}\right) {x}_{4} = \left( {4 + \frac{1}{2}}\right)
$$

The associated cut is

$$
- \frac{21}{22}{x}_{3} - \frac{3}{22}{x}_{4} + \frac{1}{2} \leq  0
$$

Similarly, the ${x}_{2}$ -equation

$$
{x}_{2} + \frac{7}{22}{x}_{3} + \frac{1}{22}{x}_{4} = 3\frac{1}{2}
$$

is factored as

$$
{x}_{2} + \left( {0 + \frac{7}{22}}\right) {x}_{3} + \left( {0 + \frac{1}{22}}\right) {x}_{4} = 3 + \frac{1}{2}
$$

Hence, the associated cut is

$$
- \frac{7}{22}{x}_{3} - \frac{1}{22}{x}_{4} + \frac{1}{2} \leq  0
$$

Any one of three cuts given above can be used in the first iteration of the cutting-plane algorithm. It is not necessary to generate all three cuts before selecting one.

Arbitrarily selecting the cut generated from the ${x}_{2}$ -row, we can write it in equation form as

$$
- \frac{7}{22}{x}_{3} - \frac{1}{22}{x}_{4} + {s}_{1} =  - \frac{1}{2},{s}_{1} \geq  0
$$

(Cut I)

This constraint is added to the LP optimum tableau as follows:

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${x}_{3}$</td><td>${x}_{4}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$z$</td><td>0</td><td>0</td><td>63</td><td>$\frac{31}{22}$</td><td>0</td><td>${66}\frac{1}{2}$</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>$\frac{7}{22}$</td><td>$\frac{1}{22}$</td><td>0</td><td>$3\frac{1}{2}$</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>$- \frac{1}{22}$</td><td>$\frac{3}{22}$</td><td>0</td><td>$4\frac{1}{2}$</td></tr><tr><td>${s}_{1}$</td><td>0</td><td>0</td><td>$- \frac{7}{22}$</td><td>$- \frac{1}{22}$</td><td>1</td><td>$- \frac{1}{2}$</td></tr></table>

The tableau is optimal but infeasible. We apply the dual simplex method (Section 4.4.1) to recover feasibility, which yields

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${x}_{3}$</td><td>${x}_{4}$</td><td>${s}_{1}$</td><td>Solution</td></tr><tr><td>$z$</td><td>0</td><td>0</td><td>0</td><td>1</td><td>9</td><td>62</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>3</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>0</td><td>1 7</td><td>$- \frac{1}{7}$</td><td>$4\frac{4}{7}$</td></tr><tr><td>${x}_{3}$</td><td>0</td><td>0</td><td>1</td><td>1 7</td><td>$- \frac{22}{7}$</td><td>1</td></tr></table>

The last solution is still noninteger in ${x}_{1}$ and ${x}_{3}$ (recall that all variables, including slack and surplus, must be integer), and we arbitrarily select ${x}_{1}$ as the next source row - that is,

$$
{x}_{1} + \left( {0 + \frac{1}{7}}\right) {x}_{4} + \left( {-1 + \frac{6}{7}}\right) {s}_{1} = 4 + \frac{4}{7}
$$

The associated cut is

$$
- \frac{1}{7}{x}_{4} - \frac{6}{7}{s}_{1} + {s}_{2} =  - \frac{4}{7},{s}_{2} \geq  0
$$

(Cut II)

Adding cut II to the previous optimal tableau, we get

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${x}_{3}$</td><td>${x}_{4}$</td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>Solution</td></tr><tr><td>$z$</td><td>0</td><td>0</td><td>0</td><td>1</td><td>9</td><td>0</td><td>62</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>3</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>0</td><td>1 7</td><td>$- \frac{1}{7}$</td><td>0</td><td>$4\frac{4}{7}$</td></tr><tr><td>${x}_{3}$</td><td>0</td><td>0</td><td>1</td><td>有</td><td>$- \frac{22}{7}$</td><td>0</td><td>$1\frac{4}{7}$</td></tr><tr><td>${s}_{2}$</td><td>0</td><td>0</td><td>0</td><td>$- \frac{1}{7}$</td><td>$- \frac{6}{7}$</td><td>1</td><td>$- \frac{4}{7}$</td></tr></table>

The dual simplex method yields the following tableau:

<table><tr><td>Basic</td><td>${x}_{1}$</td><td>${x}_{2}$</td><td>${x}_{3}$</td><td>${x}_{4}$</td><td>${s}_{1}$</td><td>${s}_{2}$</td><td>Solution</td></tr><tr><td>$z$</td><td>0</td><td>0</td><td>0</td><td>0</td><td>3</td><td>7</td><td>58</td></tr><tr><td>${x}_{2}$</td><td>0</td><td>1</td><td>0</td><td>0</td><td>1</td><td>0</td><td>3</td></tr><tr><td>${x}_{1}$</td><td>1</td><td>0</td><td>0</td><td>0</td><td>-1</td><td>1</td><td>4</td></tr><tr><td>${x}_{3}$</td><td>0</td><td>0</td><td>1</td><td>0</td><td>-4</td><td>1</td><td>1</td></tr><tr><td>${x}_{4}$</td><td>0</td><td>0</td><td>0</td><td>1</td><td>6</td><td>-7</td><td>4</td></tr></table>

The optimum solution $\left( {{x}_{1} = 4,{x}_{2} = 3, z = {58}}\right)$ is all integer. It is not accidental that all the coefficients of the last tableau are integers also, a consequence of using the fractional cuts.

Remarks. It is important to point out that the fractional cut assumes that all the variables, including slack and surplus, are integer. This means that the cut deals with pure integer problems only. The importance of this assumption is illustrated by an example.

Consider the constraint

$$
{x}_{1} + \frac{1}{3}{x}_{2} \leq  \frac{13}{2}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

From the standpoint of solving the associated ILP, the constraint is treated as an equation by using the nonnegative slack ${s}_{1}$ -that is,

$$
{x}_{1} + \frac{1}{3}{x}_{2} + {s}_{1} = \frac{13}{2}
$$

The application of the fractional cut assumes that the constraint has a feasible integer solution in all ${x}_{1},{x}_{2}$ , and ${s}_{1}$ . However, the given equation will have a feasible integer solution in ${x}_{1}$ and ${x}_{2}$ only if ${s}_{1}$ is noninteger. This means that the cutting-plane algorithm will conclude, through the applications of the dual simplex, that the problem has no feasible (integer) solution, even though the variables of concern, ${x}_{1}$ and ${x}_{2}$ , can assume feasible integer values.

There are two ways to "remedy" this situation.

1. Multiply the entire constraint by a proper constant to remove all the fractions. For example, multiplying the constraint above by 6 , we get

$$
6{x}_{1} + 2{x}_{2} \leq  {39}
$$

Any integer solution of ${x}_{1}$ and ${x}_{2}$ automatically yields integer slack. However, this type of conversion may produce excessively large integer coefficients in some cases, and this in turn may lead to computational roundoff errors on the computer.

2. Use a special cut, called the mixed cut, which allows only a subset of variables to assume integer values, with all the other variables (including slack and surplus) remaining continuous. The details of this cut will not be presented in this chapter (see Taha, 1975, pp. 198-202).

An unavoidable flaw in floating-point arithmetic on the computer is the roundoff error. Fractions such as 1/3 is approximated as .33333, and no matter how many trailing threes one carries, the representation remains an approximation. And herein lies one of the most serious challenges to the use of the fractional cut whose construction, ironically, rests squarely on the use of fractions. Though attempts were made to avoid the use of fractions by using the so-called all-integer cuts that require an all-integer starting tableau

(an unreasonable condition to boot!), the resulting algorithm is extremely slow because in seeking accuracy it forgoes speed. Another disadvantage of the cutting plane algorithms is their dual infeasibility; meaning that no feasible solution is available before the natural termination of the algorithm. Thus, unlike the B&B algorithm, there will be no solution to show if computations are stopped prematurely. The conclusion is that, from the practical standpoint, an ILP algorithm rooted only in the use of cuts is not recommended and for this reason branch-and-bound is the algorithm of choice in all solvers (in fact, Ralph Gomory, the developer of the fractional cut, was himself skeptical about the practicality of an all fractional-cut-based ILP algorithm because of the ensuing numerical instability).

Yet, cuts can play a role in enhancing the efficiency and efficacy of the branch-and-bound algorithm by periodically applying them to the optimum tableau of a subproblem where massive degeneracy at its optimum extreme point may make it difficult to determine the associated branches (of the type $x \leq  a$ and $x \geq  a + 1$ ). ${}^{7}$

## Aha! Moment: Seminal Development of Dantzig-Fulkerson-Johnson Cut. ${}^{8}$

The branch and cut algorithm developed in 1954 by Dantzig, Fulkeson, and Johnson for solving the traveling salesman problem (see Chapter 11) is seminal in that it ushered the start of the idea of imposing secondary constraints (cuts) on the optimum (continuous) LP solution to produce an integer optimum solution. Their work laid the foundation for the development of the branch and cut algorithm for the general mixed ILP. Additionally, the authors' idea of using cuts motivated the development of the Gomory's fractional cut in 1958 (see Section 9.2.2).

## BIBLIOGRAPHY

Barnett, A., "Misapplication Review: High Road to Glory," Interfaces, Vol. 17, No. 5, pp. 51-54, 1987.

Chen, D.-S., R. Batson, and Y. Dang, Applied Integer Programming: Modeling and Solutions, Wiley, New York, 2010.

Eiselt, H., and C. Sandblom, Integer Programming and Network Models, Springer, New York, 2000.

Gavirneni, S., C. Clark, and G. Pataki, "Schlumberger Optimizes Receiver Location for Automated Meter Reading," Interfaces, Vol. 34, No. 3, pp. 208-214, 2004.

Graves, R., L. Schrage, and J. Sankaran, "An Auction Method for Course Registration," Interfaces, Vol. 23, No. 5, pp. 81-97, 1993.

Guéret, C., C. Prins, and M. Sevaux, Applications of Optimization with Xpress-MP, Dash Optimization, London, 2002.

Lee, J., A First Course in Combinatorial Optimization, Cambridge University Press, 2004.

Nemhauser, G., and L. Wolsey, Integer and Combinatorial Optimization, Wiley, New York, 1988.

Pochet, Y. and L. Wolsey, Production Planning by Mixed Integer Programming, Springer, New York, 2010.

Schrijver, A. Theory of Linear and Integer Programming, Wiley, New York, 1998.

---

${}^{7}$ Cornuejols, G. "Revival of the Gomory Cuts in the 1990s," Annals of Operations Research, Vol. 149, pp. 63-66, 2007.

${}^{8}$ Dantzig, G. B., D. R. Fulkerson, and S. Johnson,"Solution of a Large Scale Traveling Salesman Problem," Operations Research, Vol. 2, pp. 393-410, 1954.

---

Taha, H., Integer Programming: Theory, Applications, and Computations, Academic Press, Orlando, FL, 1975.

Weber, G., "Puzzle Contests in MS/OR Education," Interfaces, Vol. 20, No. 2, pp. 72-76, 1990.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>9.1.1</td><td>9-1 to 9-18</td></tr><tr><td>9.1.2</td><td>9-19 to 9-27</td></tr><tr><td>9.1.3</td><td>9-28 to 9-37</td></tr><tr><td>9.1.4</td><td>9-38 to 9-54</td></tr><tr><td>9.2.1</td><td>9-55 to 9-64</td></tr><tr><td>9.2.2</td><td>9-65 to 9-70</td></tr></table>

9-1. Modify and solve the capital budgeting model of Example 9.1-1 to account for the following additional restrictions:

(a) Project 4 must be selected if either project 1 or project 3 is selected.

(b) Projects 2 and 4 are mutually exclusive.

9-2. Five items are to be loaded in a vessel. The weight ${w}_{i}$ , volume ${v}_{i}$ , and value ${r}_{i}$ for item $i$ are tabulated below.

<table><tr><td>Item $i$</td><td>Unit weight, ${w}_{i}$ (tons)</td><td>Unit volume, ${v}_{i}\left( {\mathrm{{yd}}}^{3}\right)$</td><td>Unit worth, ${r}_{i}\left( {\$ {100}}\right)$</td></tr><tr><td>1</td><td>5</td><td>1</td><td>4</td></tr><tr><td>2</td><td>8</td><td>8</td><td>7</td></tr><tr><td>3</td><td>3</td><td>6</td><td>6</td></tr><tr><td>4</td><td>2</td><td>5</td><td>5</td></tr><tr><td>5</td><td>7</td><td>4</td><td>4</td></tr></table>

The maximum allowable cargo weight and volume are 210 tons and ${198}{\mathrm{{yd}}}^{3}$ , respectively. Formulate the ILP model, and find the most valuable cargo.

*9-3. Suppose that you have 7 full wine bottles, 7 half-full, and 7 empty. You would like to divide the 21 bottles among three individuals so that each will receive exactly 7. Additionally, each individual must receive the same quantity of wine. Express the problem as ILP constraints, and find a solution. (Hint: Use a dummy objective function with all zero coefficients.) ${}^{9}$

9-4. An eccentric sheikh left a will to distribute a herd of camels among his three children: Tarek receives at least one-half of the herd, Sharif gets at least one third, and Maisa gets at least one-seventh. The remainder goes to charity. The will does not specify the size of the herd except to say that it is an odd number of camels and that the named charity receives exactly one camel. Use ILP to determine how many camels the sheikh left in the estate and how many each child got.

9-5. The three children of a farm couple are sent to the market to sell 90 apples. Karen, the oldest, carries 50 apples; Bill, the middle one, carries 30; and John, the youngest, carries only 10 . The parents have stipulated five rules: (a) The selling price is either \$1 for

---

${}^{9}$ Problems 9-3 to 9-6 are adapted from Malba Tahan, El Hombre que Calculaba, Editorial Limusa, Mexico City, pp. 39-182, 1994. Problems 9-13 to 9-16 are adapted from puzzles compiled in http://www.chlond.demon.co.uk/puzzles/puzzles1.html.

---

7 apples or \$3 for 1 apple, or a combination of the two prices. (b) Each child may exercise one or both options of the selling price. (c) Each of the three children must return with exactly the same amount of money. (d) Each child's income must be in whole dollars (no cents allowed). (e) The amount received by each child must be the largest possible under the stipulated conditions. Given that the three kids are able to sell all they have, use ILP to show how they can satisfy the parents' conditions.

*9-6. Once upon a time, there was a captain of a merchant ship who wanted to reward three crew members for their valiant effort in saving the ship's cargo during an unexpected storm in the high seas. The captain put aside a certain sum of money in the purser's office and instructed the first officer to distribute it equally among the three mariners after the ship had reached shore. One night, one of the sailors, unbeknown to the others, went to the purser's office and decided to claim (an equitable) one-third of the money in advance. After he had divided the money into three equal shares, an extra coin remained, which the mariner decided to keep (in addition to one-third of the money). The next night, the second mariner got the same idea and, repeating the same three-way division with what was left, ended up keeping an extra coin as well. The third night, the third mariner also took a third of what was left, plus an extra coin that could not be divided. When the ship reached shore, the first officer divided what was left of the money equally among the three mariners, again to be left with an extra coin. To simplify things, the first officer put the extra coin aside and gave the three mariners their allotted equal shares. How much money was in the safe to start with? Formulate the problem as an ILP, and find the solution. (Hint: The problem has a countably infinite number of integer solutions. For convenience, assume that we are interested in determining the smallest sum of money that satisfies the problem conditions. Then, boosting the resulting sum by 1, add it as a lower bound and obtain the next smallest sum. Continuing in this manner, a general solution pattern will emerge.)

9-7. Weber (1990). You have the following three-letter words: AFT, FAR, TVA, ADV, JOE, FIN, OSF, and KEN. Suppose that we assign numeric values to the alphabet starting with $A = 1$ and ending with $Z = {26}$ . Each word is scored by adding numeric codes of its three letters. For example, AFT has a score of $1 + 6 + {20} = {27}$ . You are to select five of the given eight words that yield the maximum total score. Simultaneously, the selected five words must satisfy the following conditions:

$$
\left( \begin{matrix} \text{ sum of letter }1 \\  \text{ scores } \end{matrix}\right)  < \left( \begin{matrix} \text{ sum of letter }2 \\  \text{ scores } \end{matrix}\right)  < \left( \begin{matrix} \text{ sum of letter }3 \\  \text{ scores } \end{matrix}\right)
$$

Formulate the problem as an ILP, and find the optimum solution.

9-8. Solve Problem 9-7 given that, in addition to the total sum being the largest, the sum of column 1 and the sum of column 2 will be the largest as well. Find the optimum solution.

9-9. Weber (1990). Consider the following two groups of words: letters such that the difference between the total scores of the two groups will be as small as possible. (Note: The score for a word is the sum of the numeric values assigned to its individual letters.)

<table><tr><td>Group 1</td><td>Group 2</td></tr><tr><td>AREA</td><td>ERST</td></tr><tr><td>FORT</td><td>FOOT</td></tr><tr><td>HOPE</td><td>HEAT</td></tr><tr><td>SPAR</td><td>PAST</td></tr><tr><td>THAT</td><td>PROF</td></tr><tr><td>TREE</td><td>STOP</td></tr></table>

All the words in groups 1 and 2 can be formed from the nine letters A, E, F, H, O, P, R, S, and T. Develop a model to assign a unique numeric value from 1 through 9 to these

*9-10. The Record-a-Song Company has contracted with a rising star to record eight songs. The sizes in MB of the different songs are8,10,8,7,9,6,7, and 12, respectively. Record-a-Song uses two CDs for the recording. Each CD has a capacity of 40 MB. The company would like to distribute the songs between the two CDs such that the used space on each CDs is about the same. Formulate the problem as an ILP, and find the optimum solution.

9-11. In Problem 9-10, suppose that the nature of the melodies dictates that songs 3 and 4 cannot be recorded on the same CD. Formulate the problem as an ILP. Would it be possible to use a 30 MB CDs to record the eight songs? If not, use ILP to determine the minimum CD capacity needed to make the recording.

*9-12. Graves and Associates (1993). Ulern University uses a mathematical model that optimizes student preferences taking into account the limitation of classroom and faculty resources. To demonstrate the application of the model, consider the simplified case of 10 students who are required to select two courses out of six offered electives. The table below gives scores that represent each student's preference for individual courses, with a score of 100 being the highest. For simplicity, it is assumed that the preference score for a two-course selection is the sum of the individual score. Course capacity is the maximum number of students allowed to take the class.

<table><tr><td rowspan="2">Student</td><td colspan="6">Preference score for course</td></tr><tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td></tr><tr><td>1</td><td>20</td><td>40</td><td>50</td><td>30</td><td>90</td><td>100</td></tr><tr><td>2</td><td>90</td><td>100</td><td>80</td><td>70</td><td>10</td><td>40</td></tr><tr><td>3</td><td>25</td><td>40</td><td>30</td><td>80</td><td>95</td><td>90</td></tr><tr><td>4</td><td>80</td><td>50</td><td>60</td><td>80</td><td>30</td><td>40</td></tr><tr><td>5</td><td>75</td><td>60</td><td>90</td><td>100</td><td>50</td><td>40</td></tr><tr><td>6</td><td>60</td><td>40</td><td>90</td><td>10</td><td>80</td><td>80</td></tr><tr><td>7</td><td>45</td><td>40</td><td>70</td><td>60</td><td>55</td><td>60</td></tr><tr><td>8</td><td>30</td><td>100</td><td>40</td><td>70</td><td>90</td><td>55</td></tr><tr><td>9</td><td>80</td><td>60</td><td>100</td><td>70</td><td>65</td><td>80</td></tr><tr><td>10</td><td>40</td><td>60</td><td>80</td><td>100</td><td>90</td><td>10</td></tr><tr><td>Course capacity</td><td>6</td><td>8</td><td>5</td><td>5</td><td>6</td><td>5</td></tr></table>

Formulate the problem as an ILP and find the optimum solution.

9-13. You have three currency denominations with 11 coins each. The total worth (of all 11 coins) is 12 bits for denomination 1,14 bits for denomination 2, and 20 bits for denomination 3. You need to buy one 30-bit item. Use ILP to determine the smallest number of coins of the three denominations needed to make the purchase. ${}^{10}$

9-14. You have a $4 \times  4$ grid and a total of 10 tokens. Use ILP to place the tokens on the grid such that each row and each column will have an even number of tokens.

9-15. A street vendor selling electronic gadgets was robbed of all his possessions. When reporting the matter to the police, the vendor did not know the number of gadgets he had but stated that when dividing the total in lots of size2,3,4,5, or 6 , there was always one gadget left over. On the other hand, there was no remainder when the total was divided into lots of size 7 . Use ILP to determine the total number of gadgets the vendor had.

---

${}^{10}$ Problems 9-13 to 9-16 are adapted from puzzles compiled in http://www.chlond.demon.co.uk/puzzles/ puzzles1.html.

---

9-16. Given $i = 1,2,\ldots , n$ , formulate a general ILP model (for any $n$ ) to determine the smallest number $y$ that, when divided by the integer amount $2 + i$ , will always produce a remainder equal to $i$ ; that is, $y{\;\operatorname{mod}\;\left( {2 + i}\right) } = i$ .

9-17. A widely circulated puzzle requires assigning a single distinct digit (0 through 9) to each letter in the equation SEND + MORE = MONEY. Formulate the problem as an integer program, and find the solution. (Hint: This is an assignment model with side conditions.)

9-18. The world-renowned logic puzzle, Sudoku, deals with a $9 \times  9$ grid subdivided into 9 nonoverlapping $3 \times  3$ subgrids. The puzzle calls for assigning the numerical digits 1 through 9 to the cells of the grid such that each row, each column, and each subgrid contain distinct digits. Some of the cells may be fixed in advance.

Formulate the problem as an integer program, and find the solution for the instance given below.

<table><tr><td></td><td>6</td><td></td><td>1</td><td></td><td>4</td><td></td><td>5</td><td></td></tr><tr><td></td><td></td><td>8</td><td>3</td><td></td><td>5</td><td>6</td><td></td><td></td></tr><tr><td>2</td><td></td><td></td><td></td><td></td><td></td><td>7</td><td></td><td></td></tr><tr><td>8</td><td></td><td></td><td>4</td><td></td><td>7</td><td></td><td></td><td>6</td></tr><tr><td></td><td></td><td>6</td><td></td><td></td><td></td><td>3</td><td></td><td></td></tr><tr><td>7</td><td></td><td></td><td>9</td><td></td><td>1</td><td></td><td></td><td>4</td></tr><tr><td>5</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>2</td></tr><tr><td></td><td></td><td>7</td><td>2</td><td></td><td>6</td><td>9</td><td></td><td></td></tr><tr><td></td><td>4</td><td></td><td>5</td><td></td><td>8</td><td></td><td>7</td><td></td></tr></table>

[Hint: Let ${x}_{ijk} = 1$ if digit $k$ is placed in cell $\left( {i, j}\right) , i, j, k = 1,2,\ldots , n, n = 9$ . If you use AMPL, keep in mind that for $n = 9$ , the resulting number of variables will exceed the capacity of student AMPL. If you do not have access to the full AMPL version, you can develop a general model for $n = 4$ or 9, and then solve it for the simpler (almost trivial) case of a $4 \times  4$ grid with a $2 \times  2$ subgrid.]

*9-19. ABC is an LTL (less-than-truckload) trucking company that delivers loads on a daily basis to five customers. The following list provides the customers associated with each route:

<table><tr><td>Route</td><td>Customers served on the route</td></tr><tr><td>1</td><td>3,2</td></tr><tr><td>2</td><td>5, 3, 4</td></tr><tr><td>3</td><td>2, 5, 1, 3</td></tr><tr><td>4</td><td>2, 3, 5</td></tr><tr><td>5</td><td>1, 4, 2</td></tr><tr><td>6</td><td>1,3,5</td></tr></table>

The segments of each route are dictated by the capacity of the truck delivering the loads. For example, on route 1, the capacity of the truck is sufficient to deliver the loads to customers 3 and 2 only. The following table lists distances (in miles) among the truck terminal (ABC) and the customers.

<table><tr><td colspan="7">Miles from $i$ to $j$</td></tr><tr><td>$j$ <br> $i$</td><td>ABC</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td></tr><tr><td>ABC</td><td>0</td><td>10</td><td>12</td><td>16</td><td>9</td><td>8</td></tr><tr><td>1</td><td>10</td><td>0</td><td>32</td><td>8</td><td>17</td><td>10</td></tr><tr><td>2</td><td>12</td><td>32</td><td>0</td><td>14</td><td>21</td><td>20</td></tr><tr><td>3</td><td>16</td><td>8</td><td>14</td><td>0</td><td>15</td><td>18</td></tr><tr><td>4</td><td>9</td><td>17</td><td>21</td><td>15</td><td>0</td><td>11</td></tr><tr><td>5</td><td>8</td><td>10</td><td>20</td><td>18</td><td>11</td><td>0</td></tr></table>

The objective is to determine the least distance needed to make the daily deliveries to all five customers. Though the solution may result in a customer being served by more than one route, an approximation in the implementation phase assumes that only one such route is used. Formulate the problem as an ILP, and find the optimum solution.

*9-20. The U of A is in the process of forming a committee to handle students' grievances. The administration wants the committee to include at least one female, one male, one student, one administrator, and one faculty member. Ten individuals (identified, for simplicity, by the letters $a$ to $j$ ) have been nominated. The mix of these individuals in the different categories is given as follows:

<table><tr><td>Category</td><td>Individuals</td></tr><tr><td>Females</td><td>$a, b, c, d, e$</td></tr><tr><td>Males</td><td>$f, g, h, i, j$</td></tr><tr><td>Students</td><td>$a, b, c, j$</td></tr><tr><td>Administrators</td><td>$e, f$</td></tr><tr><td>Faculty</td><td>$d, g, h, i$</td></tr></table>

The U of A wants to form the smallest committee with representation from each of the five categories. Formulate the problem as an ILP, and find the optimum solution.

9-21. Washington County includes six towns that need emergency ambulance service. Because of the proximity of some of the towns, a single station may serve more than one community. The stipulation is that the station must be within 18 minutes of driving time from the towns it serves. The table below gives the driving times in minutes among the six towns.

<table><tr><td colspan="7">Time in minutes from $i$ to $j$</td></tr><tr><td>$j$ <br> $i$</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td></tr><tr><td>1</td><td>0</td><td>19</td><td>23</td><td>18</td><td>20</td><td>25</td></tr><tr><td>2</td><td>19</td><td>0</td><td>22</td><td>13</td><td>22</td><td>11</td></tr><tr><td>3</td><td>23</td><td>22</td><td>0</td><td>60</td><td>17</td><td>20</td></tr><tr><td>4</td><td>18</td><td>13</td><td>60</td><td>0</td><td>55</td><td>17</td></tr><tr><td>5</td><td>20</td><td>22</td><td>17</td><td>55</td><td>0</td><td>12</td></tr><tr><td>6</td><td>25</td><td>11</td><td>20</td><td>17</td><td>12</td><td>0</td></tr></table>

![bo_d56m4mf7aajc73800na0_25_705_199_552_438_0.jpg](bo_d56m4mf7aajc73800na0_25_705_199_552_438_0.jpg)

FIGURE 9.7

Museum Layout for Problem 9-22

Formulate an ILP whose solution will produce the smallest number of stations and their locations. Find the optimum solution.

9-22. The great treasures of King Tut are on display in the Giza Museum in Cairo. The layout of the museum is shown in Figure 9.7, with the different rooms joined by open doors. A guard standing at a door can watch two adjoining rooms. The museum's security policy requires guard presence in every room. Formulate the problem as an ILP to determine the smallest number of guards.

9-23. Bill has just completed his exams for the academic year and wants to celebrate by seeing every movie showing in theaters in his town and in six other neighboring cities. If he travels to another town, he will stay there until he has seen all the movies he wants. The following table provides the information about the movie offerings and the round-trip distance to the neighboring town:

<table><tr><td>Theater location</td><td>Movie offerings</td><td>Round-trip miles</td><td>Cost per show (\$)</td></tr><tr><td>In-town</td><td>1,3</td><td>0</td><td>7.95</td></tr><tr><td>City A</td><td>1, 6, 8</td><td>25</td><td>5.50</td></tr><tr><td>City B</td><td>2, 5, 7</td><td>30</td><td>5.00</td></tr><tr><td>City C</td><td>1, 8, 9</td><td>28</td><td>7.00</td></tr><tr><td>City D</td><td>2, 4, 7</td><td>40</td><td>4.95</td></tr><tr><td>City E</td><td>1,3,5,10</td><td>35</td><td>5.25</td></tr><tr><td>City F</td><td>4,5,6,9</td><td>32</td><td>6.75</td></tr></table>

The cost of driving is 75 cents per mile. Bill wishes to determine the towns he needs to visit to see all the movies while minimizing his total cost.

9-24. Walmark Stores is in the process of expansion in the western United States. During next year, Walmark is planning to construct new stores that will serve 10 geographically dispersed communities. Past experience indicates that a community must be within 25 miles of a store to attract customers. In addition, the population of a community plays an important role in where a store is located, in the sense that bigger communities generate more participating customers. The following table provides the populations as well as the distances (in miles) between the communities:

<table><tr><td colspan="11">Miles from community $i$ to community $j$</td><td rowspan="2">Population</td></tr><tr><td>$j$ <br> $i$</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>1</td><td></td><td>20</td><td>40</td><td>35</td><td>17</td><td>24</td><td>50</td><td>58</td><td>33</td><td>12</td><td>10,000</td></tr><tr><td>2</td><td>20</td><td></td><td>23</td><td>68</td><td>40</td><td>30</td><td>20</td><td>19</td><td>70</td><td>40</td><td>15,000</td></tr><tr><td>3</td><td>40</td><td>23</td><td></td><td>36</td><td>70</td><td>22</td><td>45</td><td>30</td><td>21</td><td>80</td><td>28,000</td></tr><tr><td>4</td><td>35</td><td>68</td><td>36</td><td></td><td>70</td><td>80</td><td>24</td><td>20</td><td>40</td><td>10</td><td>30,000</td></tr><tr><td>5</td><td>17</td><td>40</td><td>70</td><td>70</td><td></td><td>23</td><td>70</td><td>40</td><td>13</td><td>40</td><td>40,000</td></tr><tr><td>6</td><td>24</td><td>30</td><td>22</td><td>80</td><td>23</td><td></td><td>12</td><td>14</td><td>50</td><td>50</td><td>30,000</td></tr><tr><td>7</td><td>50</td><td>20</td><td>45</td><td>24</td><td>70</td><td>12</td><td></td><td>26</td><td>40</td><td>30</td><td>20,000</td></tr><tr><td>8</td><td>58</td><td>19</td><td>30</td><td>20</td><td>40</td><td>14</td><td>26</td><td></td><td>20</td><td>50</td><td>15,000</td></tr><tr><td>9</td><td>33</td><td>70</td><td>21</td><td>40</td><td>13</td><td>50</td><td>40</td><td>20</td><td></td><td>22</td><td>60,000</td></tr><tr><td>10</td><td>12</td><td>40</td><td>80</td><td>10</td><td>40</td><td>50</td><td>30</td><td>50</td><td>22</td><td></td><td>12,000</td></tr></table>

The idea is to construct the least number of stores, taking into account the distance restriction and the concentration of populations.

Specify the communities where the stores should be located.

*9-25. Guéret and Associates (2002), Section 12.6. MobileCo is budgeting \$15 million to construct as many as 7 transmitters to cover as much population as possible in 15 contiguous geographical communities. The communities covered by each transmitter and the budgeted construction costs are given below.

<table><tr><td>Transmitter</td><td>Covered communities</td><td>Cost (million \$)</td></tr><tr><td>1</td><td>1,2</td><td>3.60</td></tr><tr><td>2</td><td>2, 3, 5</td><td>2.30</td></tr><tr><td>3</td><td>1, 7, 9, 10</td><td>4.10</td></tr><tr><td>4</td><td>4, 6, 8, 9</td><td>3.15</td></tr><tr><td>5</td><td>6, 7, 9, 11</td><td>2.80</td></tr><tr><td>6</td><td>5, 7, 10, 12, 14</td><td>2.65</td></tr><tr><td>7</td><td>12, 13, 14, 15</td><td>3.10</td></tr></table>

The following table provides the populations of the different communities:

<table><tr><td>Community</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>Population (in 1000s)</td><td>10</td><td>15</td><td>28</td><td>30</td><td>40</td><td>30</td><td>20</td><td>15</td><td>60</td><td>12</td></tr></table>

Which of the proposed transmitters should be constructed?

9-26. Gavernini and Associates (2004). Modern electric networks use automated electric utility meter reading in place of the more costly manual meter reading. In the automated system, meters from several customers are linked wirelessly to a single receiver. The meter sends monthly signals to a designated receiver to report the customer's consumption of electricity. The data are then channeled to a central computer to generate the utility bills. The objective is to determine the smallest number of receivers needed to serve a given number of meters. In real life, the problem encompasses thousands of meters and receivers. This problem deals with 10 meters and 8 possible locations for receivers, with the following configurations:

<table><tr><td>Receiver</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr><tr><td>Meters</td><td>1, 2, 3</td><td>2, 3, 9</td><td>5, 6, 7</td><td>7, 9, 10</td><td>3, 6, 8</td><td>1, 4, 7, 9</td><td>4, 5, 9</td><td>1, 4, 8</td></tr></table>

9-27. Solve Problem 9-26 if, additionally, each receiver can handle at most 4 meters and receiver 8 can handle meters 1, 4, 8, and 10.

9-28. Leatherco is contracted to manufacture batches of pants, vests and jackets. Each product requires a special setup of the machines needed in the manufacturing processes. The following table provides the pertinent data regarding the use of raw material (leather) and labor time together with cost and revenue estimates. Current supply of leather is estimated at ${3800}{\mathrm{{ft}}}^{2}$ and available labor time is limited to 2850 hours.

<table><tr><td></td><td>Pants</td><td>Vests</td><td>Jackets</td></tr><tr><td>Leather material per unit $\left( {\mathrm{{ft}}}^{2}\right)$</td><td>5.5</td><td>3.5</td><td>7.5</td></tr><tr><td>Labor time per unit (hrs)</td><td>4.5</td><td>3.5</td><td>5.5</td></tr><tr><td>Production cost per unit (\$)</td><td>30</td><td>20</td><td>80</td></tr><tr><td>Equipment setup cost per batch (\$)</td><td>110</td><td>90</td><td>140</td></tr><tr><td>Price per unit (\$)</td><td>60</td><td>40</td><td>120</td></tr><tr><td>Minimum number of units needed</td><td>100</td><td>150</td><td>200</td></tr></table>

Determine the optimum number of units that Leatherco must manufacture of each product.

*9-29. Jobco is planning to produce at least 2000 widgets on three machines. The minimum lot size on any machine is 600 widgets. The following table gives the pertinent data of the situation.

<table><tr><td>Machine</td><td>Setup cost (\$)</td><td>Production cost/unit (\$)</td><td>Capacity (units)</td></tr><tr><td>1</td><td>300</td><td>2</td><td>650</td></tr><tr><td>2</td><td>100</td><td>10</td><td>850</td></tr><tr><td>3</td><td>200</td><td>5</td><td>1250</td></tr></table>

Formulate the problem as an ILP, and find the optimum solution.

*9-30. Oilco is considering two potential drilling sites for reaching four targets (possible oil wells). The following table provides the preparation costs at each of the two sites and the cost of drilling from site $i$ to target $j\left( {i = 1,2;j = 1,2,3,4}\right)$ :

<table><tr><td rowspan="2">Site</td><td colspan="4">Drilling cost (\$ million) to target</td><td rowspan="2">Preparation cost (\$ million)</td></tr><tr><td>1</td><td>2</td><td>3</td><td>4</td></tr><tr><td>1</td><td>2</td><td>1</td><td>8</td><td>5</td><td>5</td></tr><tr><td>2</td><td>4</td><td>6</td><td>3</td><td>1</td><td>6</td></tr></table>

Formulate the problem as an ILP, and find the optimum solution.

9-31. Three industrial sites are considered for locating manufacturing plants. The plants send their supplies to three customers. The supply at the plants, the demand at the customers, and the unit transportation cost from the plants to the customers are given in the following table:

<table><tr><td colspan="5">Unit transportations cost (\$)</td></tr><tr><td>Customer <br> Plant</td><td>1</td><td>2</td><td>3</td><td>Supply</td></tr><tr><td>1</td><td>10</td><td>15</td><td>12</td><td>1800</td></tr><tr><td>2</td><td>17</td><td>14</td><td>20</td><td>1400</td></tr><tr><td>3</td><td>15</td><td>10</td><td>11</td><td>1300</td></tr><tr><td>Demand</td><td>1200</td><td>1700</td><td>1600</td><td></td></tr></table>

In addition to the transportation costs, fixed costs are incurred at the rate of \$12,000, \$11,000, and \$12,000 for plants 1, 2, and 3, respectively. Formulate the problem as an ILP, and find the optimum solution.

9-32. Repeat Problem 9-31 assuming that the demands at each of customers 2 and 3 are changed to 800 .

9-33. Liberatore and Miller (1985). A manufacturing facility uses two production lines to produce three products over the next 6 months. Backlogged demand is not allowed. However, a product may be overstocked to meet demand in later months. The following table provides the data associated with the demand, production, and storage of the three products:

<table><tr><td rowspan="2">Product</td><td colspan="6">Demand in period</td><td rowspan="2">Unit holding cost (\$)/month</td><td rowspan="2">Initial inventory</td></tr><tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td></tr><tr><td>1</td><td>50</td><td>30</td><td>40</td><td>60</td><td>20</td><td>45</td><td>.50</td><td>55</td></tr><tr><td>2</td><td>40</td><td>60</td><td>50</td><td>30</td><td>30</td><td>55</td><td>.35</td><td>75</td></tr><tr><td>3</td><td>30</td><td>40</td><td>20</td><td>70</td><td>40</td><td>30</td><td>.45</td><td>60</td></tr></table>

There is a fixed cost for switching a line from one product to another. The following tables give the switching cost, the production rates, and the unit production cost for each line:

<table><tr><td rowspan="2"></td><td colspan="3">Line switching cost (\$)</td></tr><tr><td>Product 1</td><td>Product 2</td><td>Product 3</td></tr><tr><td>Line 1</td><td>200</td><td>180</td><td>300</td></tr><tr><td>Line 2</td><td>250</td><td>200</td><td>174</td></tr></table>

<table><tr><td rowspan="2"></td><td colspan="3">Production rate (units/month)</td><td colspan="3">Unit production cost (\$)</td></tr><tr><td>Product 1</td><td>Product 2</td><td>Product 3</td><td>Product 1</td><td>Product 2</td><td>Product 3</td></tr><tr><td>Line 1</td><td>40</td><td>60</td><td>80</td><td>10</td><td>8</td><td>15</td></tr><tr><td>Line 2</td><td>90</td><td>70</td><td>60</td><td>12</td><td>6</td><td>10</td></tr></table>

Develop a model for determining the optimal production schedule.

9-34. Jarvis and Associates (1978). Seven cities are being considered as potential locations for the construction of at most four wastewater treatment plants. The following table provides the data for the situation. Missing links indicate that a pipeline cannot be constructed.

<table><tr><td colspan="8">Cost (\$) of pipeline construction between cities per 1000 gal/hr capacity</td></tr><tr><td>To <br> From</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td></tr><tr><td>1</td><td></td><td>100</td><td></td><td>200</td><td></td><td>50</td><td></td></tr><tr><td>2</td><td></td><td></td><td></td><td>120</td><td></td><td>150</td><td></td></tr><tr><td>3</td><td>400</td><td></td><td></td><td></td><td>120</td><td></td><td>90</td></tr><tr><td>4</td><td></td><td></td><td>120</td><td></td><td>120</td><td></td><td></td></tr><tr><td>5</td><td></td><td>200</td><td></td><td></td><td></td><td>100</td><td>200</td></tr><tr><td>6</td><td></td><td></td><td>110</td><td>180</td><td></td><td></td><td>70</td></tr><tr><td>7</td><td>200</td><td></td><td></td><td>150</td><td></td><td></td><td></td></tr><tr><td>Cost (\$ million) of</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>plant construction</td><td>1.00</td><td>1.20</td><td>2.00</td><td>1.60</td><td>1.80</td><td>.90</td><td>1.40</td></tr><tr><td>Population (1000s)</td><td>50</td><td>100</td><td>45</td><td>90</td><td>75</td><td>60</td><td>30</td></tr></table>

The capacity of a pipeline (in gallons per hour) is a direct function of the amount of wastewater generated, which is a function of the populations. Approximately 500 gallons per 1000 residents are discharged in the sewer system per hour. The maximum plant capacity is 100,000 gal/hr. Determine the optimal location and capacity of the plants.

9-35. A company uses four special tank trucks to deliver four different gasoline products to customers. Each tank has five compartments with different capacities: 500, 750, 1200, 1500, and 1750 gallons. The daily demands for the four products are estimated at 10, 15, 12, and 8 thousand gallons. Any quantities that cannot be delivered by the company's four trucks must be subcontracted at the additional costs of5,12,8, and 10 cents per gallon for products 1, 2, 3, and 4, respectively. Develop the optimal daily loading schedule for the four trucks that will minimize the additional cost of subcontracting.

9-36. A household uses at least 3000 minutes of long-distance telephone calls monthly and can choose to use the services of any of three companies: A, B, and C. Company A charges a fixed monthly fee of \$10 and 5 cents per minute for the first 1000 minutes and 4 cents per minute for all additional minutes. Company B's monthly fee is \$20 with a flat 4 cents per minute. Company C's monthly charge is \$25 with 5 cents per minute for the first 1000 minutes and 3.5 cents per minute beyond that limit. Which company should be selected to minimize the total monthly charge?

*9-37. Barnett (1987). Professor Yataha needs to schedule eight round-trips between Boston and Washington, D.C. The route is served by three airlines, Eastern, US Air, and Continental, and there is no penalty for the purchase of one-way tickets. Each airline offers bonus miles for frequent fliers. Eastern gives 1500 miles per (one-way) ticket plus 5000 extra miles if the number of tickets in a month reaches 3 and another 5000 miles if the number exceeds 5. US Air gives 1800 miles per ticket plus 12,000 extra for each 6 tickets. Continental gives 2000 miles per ticket plus 7500 extra for each 5 tickets. Professor Ya-taha wishes to allocate the 16 one-way tickets among the three airlines to maximize the total number of bonus miles earned.

*9-38. A game board has $3 \times  3$ equal squares. You are required to fill each square with a number between 1 and 9 such that the sum of the numbers in each row, each column, and each diagonal equals 15. Additionally, the numbers in all the squares must be distinct. Use ILP to determine the assignment of numbers to squares.

9-39. A machine is used to produce two interchangeable products. The daily capacity of the machine can produce at most 20 units of product 1 and 40 units of product 2. Alternatively, the machine can be adjusted to produce at most 45 units of product 1 and 25 units of product 2 daily. Market analysis shows that the maximum daily demand for the two products combined is 50 units. Given that the unit profits for the two respective products are \$10 and \$12, which of the two machine settings should be selected? Formulate the problem as an ILP and find the optimum. [Note: This two-dimensional problem can be solved by inspecting the graphical solution space. This is not the case for the $n$ -dimensional problem.]

*9-40. Gapco manufactures three products, whose daily labor and raw material requirements are given in the following table.

<table><tr><td>Product</td><td>Required daily labor (hr/unit)</td><td>Required daily raw material (lb/unit)</td></tr><tr><td>1</td><td>3</td><td>4</td></tr><tr><td>2</td><td>4</td><td>3</td></tr><tr><td>3</td><td>5</td><td>6</td></tr></table>

The profits per unit of the three products are \$20, \$25, and \$18, respectively. Gapco has two options for locating its plant. The two locations differ primarily in the availability of labor and raw material, as shown in the following table:

<table><tr><td>Location</td><td>Available daily labor (hr)</td><td>Available daily raw material (lb)</td></tr><tr><td>1</td><td>150</td><td>150</td></tr><tr><td>2</td><td>135</td><td>180</td></tr></table>

Formulate the problem as an ILP, and determine the optimum location of the plant.

9-41. Jobco Shop has 10 outstanding jobs to be processed on a single machine. The following table provides processing times and due dates. All times are in days, and due time is measured from time 0 :

<table><tr><td>Job</td><td>Processing time (day)</td><td>Due time (day)</td></tr><tr><td>1</td><td>10</td><td>20</td></tr><tr><td>2</td><td>3</td><td>98</td></tr><tr><td>3</td><td>13</td><td>100</td></tr><tr><td>4</td><td>15</td><td>34</td></tr><tr><td>5</td><td>9</td><td>50</td></tr><tr><td>6</td><td>22</td><td>44</td></tr><tr><td>7</td><td>17</td><td>32</td></tr><tr><td>8</td><td>30</td><td>60</td></tr><tr><td>9</td><td>12</td><td>80</td></tr><tr><td>10</td><td>16</td><td>150</td></tr></table>

If job 4 precedes job 3, then job 9 must precede job 7. The objective is to process all 10 jobs in the shortest possible time. Formulate the model as an ILP, and determine the optimum solution by modifying the AMPL file amplEx9.1-4.txt.

9-42. In Problem 9-41, suppose that job 4 cannot be processed until job 3 has been completed. Also, machine settings for jobs 7 and 8 necessitate processing them one right after the other (i.e., job 7 immediately succeeds or precedes job 8). Jobco's objective is to process all ten jobs with the smallest sum of due-time violations. Formulate the model mathematically, and determine the optimum solution.

9-43. Jaco owns a plant in which three products are manufactured. The labor and raw material requirements for the three products are given in the following table.

<table><tr><td>Product</td><td>Required daily labor (hr/unit)</td><td>Required daily raw material (lb/unit)</td></tr><tr><td>1</td><td>3</td><td>4</td></tr><tr><td>2</td><td>4</td><td>3</td></tr><tr><td>3</td><td>5</td><td>6</td></tr><tr><td>Daily availability</td><td>100</td><td>100</td></tr></table>

The profit per unit for the three products are \$25, \$30, and \$45, respectively. If product 2 is to be manufactured at all, then its production level must be at least 12 units daily. Formulate the problem as a mixed ILP, and find the optimal mix.

9-44. UPak is a subsidiary of an LTL transportation company. Customers bring their shipments to the UPak terminal to be loaded on the trailer and can rent space up to 36 ft. The customer pays for the exact linear space (in foot increments) the shipment occupies. No partial shipment is allowed, in the sense that a shipment requiring no more than ${36}\mathrm{{ft}}$ must be loaded on one trailer. A movable barrier, called bulkhead, is installed to separate shipments. The per-foot fee UPak collects depends on the destination of the shipment. The following table provides the outstanding orders UPak needs to process:

<table><tr><td>Order</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>Size (ft)</td><td>5</td><td>11</td><td>22</td><td>15</td><td>7</td><td>9</td><td>18</td><td>14</td><td>10</td><td>12</td></tr><tr><td>Rate (\$)</td><td>120</td><td>93</td><td>70</td><td>85</td><td>125</td><td>104</td><td>98</td><td>130</td><td>140</td><td>65</td></tr></table>

The terminal currently has two trailers ready to be loaded. Determine the priority orders that will maximize the total income from the two trailers. (Hint: A formulation using binary ${x}_{ij}$ to represent load $i$ on trailer $j$ is straightforward. However, you are challenged to define ${x}_{ij}$ as feet assigned to load $i$ in trailer $j$ . Then use if-then constraint to prevent partial load shipping.)

9-45. N queens problem. In the game of chess, queens attack by moving horizontally, vertically, or diagonally. It is desired to place $N$ queens on an $\left( {N \times  N}\right)$ -grid so that no queen can "take" any other queen. Formulate the problem as an integer program, and solve with AMPL (or any other software) for $N = 4,5,6$ , and 8. [Hint: Formulations 1: Let ${x}_{ij} = 1$ if a queen is placed in square $\left( {i, j}\right)$ , and zero otherwise. The constraints of the problem are of the type "if ${x}_{ij} > 0$ , then no other queen can be placed in row $i$ , column $j$ , or diagonal(s) from square $\left( {i, j}\right)$ ." Formulations 2: Let ${R}_{i} =$ row associated with column $i$ in which queen $i$ is placed on the grid. The constraints prevent diagonal placements of queens.]

9-46. A manufacturing process uses four interchangeable raw materials. The raw materials differ in properties, which leads to different output units per unit of raw material. They also differ in cost and lot sizes. The following table summarizes the data of the situation:

<table><tr><td></td><td>Material 1</td><td>Material 2</td><td>Material 3</td><td>Material 4</td><td>Material 5</td></tr><tr><td>Lot size (units)</td><td>100</td><td>160</td><td>80</td><td>310</td><td>50</td></tr><tr><td>Product units per unit of raw material</td><td>3</td><td>2</td><td>5</td><td>1</td><td>4</td></tr><tr><td>Cost per unit of raw material (\$)</td><td>30</td><td>80</td><td>200</td><td>10</td><td>120</td></tr></table>

A raw material, if used, must be in the indicated lots only (e.g., Material 1 can be bought either as a lot of size 100 units or none at all). The number of output units must be at least 950. Formulate a model to determine the raw materials that should be used at minimum cost.

9-47. Show how the nonconvex shaded solution spaces in Figure 9.8 can be represented by a set of simultaneous constraints. Find the optimum solution that maximizes $z = 2{x}_{1} + 3{x}_{2}$ subject to the solution space given in (a).

9-48. Given the binary variables ${x}_{1},{x}_{2},{x}_{3},{x}_{4}$ , and ${x}_{5}$ , if ${x}_{1} = 1$ and ${x}_{2} = 0$ , then ${x}_{3} = 1,{x}_{4} = 1$ , and ${x}_{5} = 1$ . Formulate the condition as simultaneous constraints.

*9-49. Suppose that product ${zw}$ occurs in a constraint, where $z$ and $w$ are binary variables. Show how this term can be linearized.

9-50. Consider the binary variable ${y}_{i}, i = 1,2,\ldots , n$ . Express the following condition as a set of simultaneous ILP constraints: If $i = k$ , then ${y}_{k} = 1$ , and all the remaining variables equal zero.

9-51. Suppose that it is required that any $k$ out of the following $m$ constraints must be active:

$$
{g}_{i}\left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)  \leq  {b}_{i},\;i = 1,2,\ldots , m
$$

Show how this condition may be represented.

9-52. In the following constraint, the right-hand side may assume one of values, ${b}_{1},{b}_{2},\ldots$ , and ${b}_{m}$ .

$$
g\left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)  \leq  \left( {{b}_{1},{b}_{2},\ldots ,\text{ or }{b}_{m}}\right)
$$

Show how this condition is represented.

9-53. Consider the following objective function

$$
\text{ Minimize }z = \min \left\{  {2{x}_{1} + {x}_{2},4{x}_{1} - 3{x}_{2} \mid  {x}_{1} \geq  1,{x}_{2} \geq  0}\right\}
$$

Use auxiliary binary variables to convert the objective function $z$ into an analytically manageable format that eliminates the min function.

9-54. Give the binary variables ${y}_{1},{y}_{2},\ldots ,{y}_{n}$ , such that if ${x}_{i} = 1$ , then ${x}_{i - 1}$ or ${x}_{i + 1}$ must equal 1, $i = 1,2,\ldots , n$ , where ${y}_{0}$ and ${y}_{n + 1}$ define the variable ${y}_{n}$ .

9-55. Solve the ILP of Example 9.2-1 by the B&B algorithm starting with ${x}_{2}$ as the branching variable. Start the procedure by solving the subproblem associated with ${x}_{2} \leq  \left\lbrack  {x}_{2}^{ * }\right\rbrack   \cdot  {}^{11}$

FIGURE 9.8

Solution Spaces for Problem 9-47

![bo_d56m4mf7aajc73800na0_32_475_1631_999_387_0.jpg](bo_d56m4mf7aajc73800na0_32_475_1631_999_387_0.jpg)

---

${}^{11}$ In Problems 9-55 to 9-64, you may solve the subproblems interactively with AMPL or Solver or by using TORA's MODIFY option for the upper and lower bounds.

---

---

9-56. Develop the B&B tree for each of the following problems. For convenience, always select

		${x}_{1}$ as the branching variable at node 0 .

		*(a) Maximize $z = 3{x}_{1} + 2{x}_{2}$

				subject to

$$
2{x}_{1} + 5{x}_{2} \leq  {18}
$$

$$
4{x}_{1} + 2{x}_{2} \leq  {18}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

		(b) Maximize $z = 2{x}_{1} + 3{x}_{2}$

				subject to

$$
7{x}_{1} + 5{x}_{2} \leq  {36}
$$

$$
4{x}_{1} + 9{x}_{2} \leq  {35}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

		(c) Maximize $z = 2{x}_{1} + 2{x}_{2}$

				subject to

$$
2{x}_{1} + 5{x}_{2} \leq  {27}
$$

$$
6{x}_{1} + 5{x}_{2} \leq  {16}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

		*(d) Minimize $z = 5{x}_{1} + 4{x}_{2}$

				subject to

$$
3{x}_{1} + 2{x}_{2} \geq  5
$$

$$
2{x}_{1} + 3{x}_{2} \geq  7
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

		(e) Maximize $z = 5{x}_{1} + 7{x}_{2}$

				subject to

$$
2{x}_{1} + {x}_{2} \leq  {13}
$$

$$
5{x}_{1} + 9{x}_{2} \leq  {41}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

*9-57. Repeat Problem 9-56, assuming that ${x}_{1}$ is continuous.

9-58. Show graphically that the following ILP has no feasible solution, and then verify the

		result using B&B.

$$
\text{ Maximize }z = 2{x}_{1} + {x}_{2}
$$

		subject to

$$
{10}{x}_{1} + 9{x}_{2} \leq  8
$$

$$
8{x}_{1} + 6{x}_{2} \geq  1
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

---

9-59. Solve the following problems by B&B:

$$
\text{ Maximize }z = {18}{x}_{1} + {14}{x}_{2} + 8{x}_{3} + 4{x}_{4}
$$

subject to

$$
{15}{x}_{1} + {12}{x}_{2} + 7{x}_{3} + 4{x}_{4} + {x}_{5} \leq  {37}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} = \left( {0,1}\right)
$$

9-60. Convert the following problem into a mixed ILP, and find the optimum solution:

$$
\text{ Maximize }z = {x}_{1} + 2{x}_{2} + 5{x}_{3}
$$

subject to

$$
\left| {-{x}_{1} + {10}{x}_{2} - 3{x}_{3}}\right|  \geq  {15}
$$

$$
2{x}_{1} + {x}_{2} + {x}_{3} \leq  {10}
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

9-61. TORA/Solver/AMPL Experiment. The following problem is designed to demonstrate the bizarre behavior of the B&B algorithm even for small problems. In particular, note how many subproblems are examined before the optimum is found and how many are needed to verify optimality.

$$
\text{ Minimizey }
$$

subject to

$$
2\left( {{x}_{1} + {x}_{2} + \cdots  + {x}_{15}}\right)  + y = {15}
$$

$$
\text{ All variables are }\left( {0,1}\right)
$$

(a) Use TORA's automated option to show that although the optimum is found after only 9 subproblems, over 25,000 subproblems are examined before optimality is confirmed.

(b) Show that Solver exhibits an experience similar to TORA's. [Note: In Solver, you can watch the change in the number of generated branches (subproblems) at the bottom of the spreadsheet.]

(c) Solve the problem with AMPL, and show that the solution is obtained instantly with 0 mixed integer program (MIP) simplex iterations and 0 B&B nodes. The reason for this superior performance can only be attributed to the presolve steps performed by AMPL and/or the CPLEX solver.

9-62. TORA Experiment. Consider the following ILP:

$$
\text{ Maximize }z = {18}{x}_{1} + {14}{x}_{2} + 8{x}_{3}
$$

subject to

$$
{15}{x}_{1} + {12}{x}_{2} + 7{x}_{3} \leq  {43}
$$

$$
{x}_{1},{x}_{2},{x}_{3}\text{ nonnegative integers }
$$

Use TORA's B&B user-guided option to generate the search tree with and without activating the objective-value bound. What is the impact of activating the objective-value bound on the number of generated subproblems? For consistency, always select the branching variable as the one with the lowest index and investigate all the subproblems in a current row from left to right before moving to the next row.

*9-63. TORA Experiment. Reconsider Problem 9-62. Convert the problem into an equivalent 0-1 ILP, then solve it with TORA's automated option. Compare the size of the search trees in the two problems.

9-64. AMPL Experiment. In the following 0-1 ILP, use interactive AMPL to generate the associated search tree. In each case, show how the $z$ -bound is used to fathom subproblems.

$$
\text{ Maximize }z = 3{x}_{1} + 2{x}_{2} - 5{x}_{3} - 2{x}_{4} + 3{x}_{5}
$$

subject to

$$
{x}_{1} + {x}_{2} + {x}_{3} + 2{x}_{4} + {x}_{5} \leq  4
$$

$$
\begin{array}{l} 7{x}_{1}\; + 3{x}_{3} - 4{x}_{4} + 3{x}_{5} \leq  8 \\  \end{array}
$$

$$
{11}{x}_{1} - 6{x}_{2}\; + 3{x}_{4} - 3{x}_{5} \geq  3
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4},{x}_{5} = \left( {0,1}\right)
$$

9-65. In Example 9.2-2, show graphically whether or not each of the following constraints can form a legitimate cut:

*(a) ${x}_{1} + 2{x}_{2} \leq  {10}$

(b) $2{x}_{1} + {x}_{2} \leq  {10}$

(c) $3{x}_{2} \leq  {10}$

(d) $3{x}_{1} + {x}_{2} \leq  {15}$

9-66. In Example 9.2-2, show graphically how the following two (legitimate) cuts can lead to the optimum integer solution:

$$
{x}_{1} + 2{x}_{2} \leq  {10}\;\left( {\mathrm{{Cut}}\mathrm{I}}\right)
$$

$$
3{x}_{1} + {x}_{2} \leq  {15}\text{ (Cut II) }
$$

9-67. Express cuts I and II of Example 9.2-2 in terms of ${x}_{1}$ and ${x}_{2}$ , and show that they are the same ones used graphically in Figure 9.6.

9-68. In Example 9.2-2, derive cut II from the ${x}_{3}$ -row. Use the new cut to complete the solution of the example.

9-69. Show that, even though the following problem has a feasible integer solution in ${x}_{1}$ and ${x}_{2}$ , the fractional cut would not yield a feasible solution unless all the fractions in the constraint were eliminated.

$$
\text{ Maximize }z = {x}_{1} + 2{x}_{2}
$$

subject to

$$
{x}_{1} + \frac{1}{2}{x}_{2} \leq  \frac{13}{4}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

9-70. Solve the following problems by the fractional cut, and compare the true optimum integer solution with the solution obtained by rounding the continuous optimum.

*(a) Maximize $z = 4{x}_{1} + 6{x}_{2} + 2{x}_{3}$

subject to

$$
4{x}_{1} - 4{x}_{2}\; \leq  5
$$

$$
- {x}_{1} + 6{x}_{2}\; \leq  5
$$

$$
- {x}_{1} + {x}_{2} + {x}_{3} \leq  5
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0\text{ and integer }
$$

(b) Maximize $z = 3{x}_{1} + {x}_{2} + 3{x}_{3}$

subject to

$$
- {x}_{1} + 2{x}_{2} + {x}_{3} \leq  4
$$

$4{x}_{2} - 3{x}_{3} \leq  2 \; {x}_{1} - 3{x}_{2} + 2{x}_{3} \leq  3 \; {x}_{1},{x}_{2},{x}_{3} \geq  0$ and integer

This page intentionally left blank