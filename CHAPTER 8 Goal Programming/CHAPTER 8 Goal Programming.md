## CHAPTER 8 Goal Programming ^chapter

## Summary

- Goal programming (GP) models multiple, potentially conflicting goals and seeks a compromise by minimizing goal violations rather than optimizing a single criterion.
- Each goal constraint is converted into an equality by adding two nonnegative deviational variables: one for underachievement and one for overachievement.
- A “good” GP solution depends on the decision maker’s preference model: either weighted trade-offs (weights method) or strict priorities (preemptive method).
- GP often produces satisficing solutions; when goals are treated as hard “limits,” the best compromise may not be the true optimum for any underlying objective.
- The Mount Sinai Hospital case illustrates an integer-GP schedule that targets equitable weekly operating-room hours and highlights practical computational challenges of ILP.

```markmap
---
markmap:
  height: 643
---
# [[#^chapter|CHAPTER 8: Goal Programming]]

## [[#^application|Real-Life Application: Mount Sinai OR Time Allocation]]
### [[#^appcontext|Health-care funding context and why OR time is scarce]]
### [[#^appequity|Objective: an equitable daily schedule for available ORs]]

## [[#^formulation|8.1 Goal Programming Formulation]]
### [[#^taxplanning|Example 8.1-1: Fairville Tax Planning]]
#### [[#^fairvilledata|Data and decision variables (tax rates and gasoline tax)]]
#### [[#^fairvillegoals|Four policy goals (revenue, shares, and a per-gallon cap)]]
#### [[#^simplify|Simplify the original goal inequalities to linear form]]
#### [[#^flexgoals|Make each goal “flexible” using deviational variables]]
#### [[#^deviation|Interpret s_i^- and s_i^+ as under/over deviations]]
#### [[#^violations|Identify which deviations represent goal violations]]
#### [[#^multiobjective|Convert multiple goals to one objective: weights vs preemptive]]

## [[#^algorithms|8.2 Goal Programming Algorithms]]
### [[#^weights|Weights Method]]
#### [[#^weightedobjective|Single objective: weighted sum of goal measures]]
#### [[#^weightschoice|Weights represent preferences; choosing them is subjective]]
#### [[#^topad|Example 8.2-1: TopAd media mix]]
##### [[#^topadtable|Reach/cost/labor data table]]
##### [[#^topadformulation|GP model: exposure shortfall and budget overrun]]
##### [[#^topadsolution|Solution reading: which goals are met vs violated]]
#### [[#^satisficing|Aha! Satisficing versus maximizing (Herbert Simon)]]
##### [[#^satisficingexample|Why GP can “satisfice” instead of optimize]]

### [[#^preemptive|Preemptive (Lexicographic) Method]]
#### [[#^rho|Priorities defined via a deviational component ρ_i]]
#### [[#^nondegradation|Solve goals sequentially without degrading higher priorities]]
#### [[#^columndropping|Column-dropping rule (special simplex idea)]]
#### [[#^stepprocedure|Equivalent stepwise LP: add ρ_i = ρ_i* constraints]]
#### [[#^remarks|Implementation notes: substitution and bounded-simplex variant]]
#### [[#^examplepreemptive|Example 8.2-2: preemptive solution for TopAd]]
##### [[#^preemptiveinsight|Savings: if a later goal is already optimal, skip it]]

### [[#^examplecolumndrop|Example 8.2-3: optimize objectives + column dropping]]
#### [[#^restated|Restate priorities as objectives (maximize exposure, minimize cost)]]
#### [[#^twostage|Two-stage solve: same exposure, lower cost]]
#### [[#^tableauone|LP1 tableau (carry passive lower-priority objective row)]]
#### [[#^tableautwo|LP2 tableau (after dropping a column that could degrade LP1)]]

## [[#^ampl|AMPL Moment]]
## [[#^bibliography|Bibliography]]

## [[#^casestudy|Case Study: Mount Sinai Hospital OR Allocation]]
### [[#^casecontext|Situation and resources (rooms, types, departments, weekdays)]]
### [[#^tableavailability|Table 8.1: room availability by weekday and type]]
### [[#^tabledemand|Table 8.2: weekly target hours and underallocation limits]]
### [[#^caseequity|Goal: equitable schedule that meets weekly targets as much as possible]]
### [[#^model|Mathematical model (integer goal program)]]
#### [[#^modelvars|Indices and variables (x_ijk, d_ik, a_ik, h_j, u_j^-) ]]
#### [[#^modelconstraints|Objective and constraints (1)–(5)]]
#### [[#^modellogic|Interpretation: minimize relative underallocation; cap denial limits]]
### [[#^modelresults|Model results: z = 0 for given data; overallocations allowed]]
### [[#^experience|Computational experience: sensitivity and ILP difficulty]]
### [[#^mitigation|Mitigation ideas: tighter bounds or heuristics]]
### [[#^departmentsummary|Figure 8.1: departmental summary (allocated vs targets)]]

## [[#^problems|Problems (8-1–8-25)]]
### [[#^problemstable|Assigned problems by section]]
```

## Real-Life Application—Allocation of Operating Room Time in Mount Sinai Hospital ^application

The situation takes place in Canada, where health-care insurance is mandatory and universal. Funding, which is based on a combination of premiums and taxes, is controlled by the individual provinces. Under this system, hospitals are advanced a fixed annual budget, and each province pays physicians retrospectively using a fee-for-service funding mechanism. This funding arrangement limits the availability of hospital facilities (e.g., operating rooms), which in turn curbs physicians' tendency to boost personal gain through overservice to patients. ^appcontext

The objective of the study is to determine an equitable daily schedule for the use of available operating rooms. The problem is modeled using a combination of goal and integer programming. The case at the end of the chapter provides the details of the study. ^appequity

### 8.1 A GOAL PROGRAMMING FORMULATION ^formulation

The idea of goal programming (GP) is illustrated by Example 8.1-1.

## Example 8.1-1 (Tax Planning) ^taxplanning

Fairville is a small city with a population of about 20,000 residents. The annual taxation base for real estate property is \$550 million. The annual taxation bases for food and drugs and for general sales are \$35 million and \$55 million, respectively. Annual local gasoline consumption is estimated at 7.5 million gallons. The city council wants to develop the tax rates based on four main goals: ^fairvilledata

1. Tax revenues must be at least \$16 million to meet the city's financial commitments.

2. Food and drug taxes cannot exceed 10% of all taxes collected.

---

${}^{1}$ This example is based on Chissman and Associates,1989.

---

3. General sales taxes cannot exceed 20% of all taxes collected.

4. Gasoline tax cannot exceed 2 cents per gallon. ^fairvillegoals

Let the variables ${x}_{p},{x}_{f}$ , and ${x}_{s}$ represent the tax rates (expressed as proportions of taxation bases) for property, food and drug, and general sales and define the variable ${x}_{g}$ as the gasoline tax in cents per gallon. The goals of the city council are then expressed as

$$
{550}{x}_{p} + {35}{x}_{f} + {55}{x}_{s} + {.075}{x}_{g} \geq  {16}\;\text{ (Tax revenue) }
$$

$$
{35}{x}_{f} \leq  {.1}\left( {{550}{x}_{p} + {35}{x}_{f} + {55}{x}_{3} + {.075}{x}_{g}}\right)
$$

$$
{55}{x}_{s} \leq  {.2}\left( {{550}{x}_{p} + {35}{x}_{f} + {55}{x}_{s} + {.075}{x}_{g}}\right)
$$

$$
{x}_{g} \leq  2
$$

$$
{x}_{p},{x}_{f},{x}_{s},{x}_{g} \geq  0
$$

These constraints are then simplified as ^simplify

$$
{550}{x}_{p} + {35}{x}_{f} + {55}{x}_{s} + {.075}{x}_{g} \geq  {16}
$$

$$
{55}{x}_{p} - {31.5}{x}_{f} + {5.5}{x}_{s} + {.0075}{x}_{g} \geq  0
$$

$$
{110}{x}_{p} + 7{x}_{f} - {44}{x}_{s} + {.015}{x}_{g} \geq  0
$$

$$
{x}_{g} \leq  2
$$

$$
{x}_{p},{x}_{f},{x}_{s},{x}_{g} \geq  0
$$

Each of the inequalities of the model represents a goal that the city council aspires to satisfy. Most likely, however, the best that can be done is a compromise solution involving these conflicting goals.

The manner in which GP finds a compromise solution is to convert each inequality into a flexible goal in which the corresponding constraint may be violated, if necessary. In terms of the Fairville model, the flexible goals are expressed as follows: ^flexgoals

$$
{550}{x}_{p} + {35}{x}_{f} + {55}{x}_{s} + {.075}{x}_{g} + {\mathbf{s}}_{1}^{ - } - {s}_{1}^{ + } = {16}
$$

$$
{55}{x}_{p} - {31.5}{x}_{f} + {5.5}{x}_{s} + {.0075}{x}_{g} + {\mathbf{s}}_{2}^{ - } - {s}_{2}^{ + } = 0
$$

$$
{110}{x}_{p} + 7{x}_{f} - {44}{x}_{s} + {.015}{x}_{g} + {\mathbf{s}}_{3}^{ - } - {\mathbf{s}}_{3}^{ + } = 0
$$

$$
{x}_{g} + {s}_{4}^{ - } - {\mathbf{s}}_{4}^{ + } = 2
$$

$$
{x}_{p},{x}_{f},{x}_{s},{x}_{g} \geq  0
$$

$$
{s}_{i}^{ - },{s}_{i}^{ + } \geq  0, i = 1,2,3,4
$$

The nonnegative variables ${s}_{i}^{ - }$ and ${s}_{i}^{ + }, i = 1,2,3,4$ , are deviational variables representing the deviations below and above the right-hand side of constraint $i$ . ^deviation

The deviational variables ${s}_{i}^{ - }$ and ${s}_{i}^{ + }$ are by definition dependent, and hence cannot be basic variables simultaneously (per the theory of the simplex method). This means that in any simplex iteration, at most one of the two deviational variables can assume a positive value. If the original $i$ th inequality is of the type $\leq$ and its ${s}_{i}^{ - } \geq  0$ , then the $i$ th goal is satisfied; otherwise, goal $i$ is not satisfied. In essence, the definition of ${s}_{i}^{ - }$ and ${s}_{i}^{ + }$ allows meeting or violating the $i$ th goal at will. This is the type of flexibility that characterizes GP when it seeks a compromise solution. Logically, a good compromise solution seeks to minimize the amount by which each goal is violated. ^violations

In the Fairville model, given that the first three constraints are of the type $\geq$ and the fourth constraint is of the type $\leq$ , the deviational variables ${s}_{1}^{ - },{s}_{2}^{ - },{s}_{3}^{ - }$ , and ${s}_{4}^{ + }$ (shown in the model in bold) represent the amounts by which the respective goals are violated. Thus, the compromise solution seeks to satisfy the following four objectives as much as possible:

$$
\text{ Minimize }{G}_{1} = {s}_{1}^{ - }
$$

$$
\text{ Minimize }{G}_{2} = {s}_{2}^{ - }
$$

$$
\text{ Minimize }{G}_{3} = {s}_{3}^{ - }
$$

$$
\text{ Minimize }{G}_{4} = {s}_{4}^{ + }
$$

These functions are minimized subject to the constraint equations of the model.

How can we optimize a multiobjective model with conflicting goals? Two methods have been developed for this purpose: (1) the weights method and (2) the preemptive method. Both methods are based on converting the multiple objectives into a single function. Section 8.2 provides the details. ^multiobjective

### 8.2 GOAL PROGRAMMING ALGORITHMS ^algorithms

This section presents two algorithms for solving GP. Both methods are based on representing the multiple goals by a single objective function. In the weights method, the single objective function is the weighted sum of the functions representing the goals of the problem. The preemptive method starts by prioritizing the goals in order of importance. The model then optimizes the goals one at a time in order of priority and in a manner that does not degrade a higher-priority solution.

The proposed two methods do not generally produce the same solution. Neither method, however, is superior to the other, because the two techniques entail distinct decision-making preferences.

#### 8.2.1 The Weights Method ^weights

Suppose that the GP model has $n$ goals and that the $i$ th goal is given as

$$
\text{ Minimize }{G}_{i}, i = 1,2,\ldots , n
$$

The combined objective function used in the weights method is then defined as ^weightedobjective

$$
\text{ Minimize }z = {w}_{1}{G}_{1} + {w}_{2}{G}_{2} + \cdots  + {w}_{n}{G}_{n}
$$

The parameters ${w}_{i}, i = 1,2,\ldots , n$ , are positive weights that reflect the decision maker's preferences regarding the relative importance of each goal. For example, ${w}_{i} = 1$ , for all $i$ , signifies that all goals are of equal importance. The determination of the specific values of these weights is subjective. Indeed, the apparently sophisticated analytic procedures developed in the literature (see, e.g., Cohon, 1978) are still rooted in subjective assessments. ^weightschoice

## Example 8.2-1 ^topad

TopAd, a new advertising agency with 10 employees, has received a contract to promote a new product. The agency can advertise by radio and television. The following table gives the number of people reached daily by each type of advertisement and the cost and labor requirements. ^topadtable

|  | Radio | Television |
|---|---:|---:|
| Exposure (in millions of persons)/min | 4 | 8 |
| Cost (in thousands of dollars)/min | 8 | 24 |
| Assigned employees/min | 1 | 2 |

The contract prohibits TopAd from using more than 6 minutes of radio advertisement. Additionally, radio and television advertisements need to reach at least 45 million people. TopAd has a budget goal of \$100,000 for the project. How many minutes of radio and television advertisement should TopAd use?

Let ${x}_{1}$ and ${x}_{2}$ be the minutes allocated to radio and television advertisements. The GP formulation for the problem is given as ^topadformulation

$$
\text{ Minimize }{G}_{1} = {s}_{1}^{ - }\text{ (Satisfy exposure goal) }
$$

$$
\text{ Minimize }{G}_{2} = {s}_{2}^{ + }\text{ (Satisfy budget goal) }
$$

subject to

$$
4{x}_{1} + 8{x}_{2} + {s}_{1}^{ - } - {s}_{1}^{ + }\; = {45}\text{ (Exposure goal) }
$$

$$
8{x}_{1} + {24}{x}_{2}\; + {s}_{2}^{ - } - {s}_{2}^{ + } = {100}\text{ (Budget goal) }
$$

$$
{x}_{1} + 2{x}_{2}\; \leq  {10}\text{ (Personnel limit) }
$$

$$
{x}_{1}\; \leq  \;6\text{ (Radio limit) }
$$

$$
{x}_{1},{x}_{2},{s}_{1}^{ - },{s}_{1}^{ + },{s}_{2}^{ - },{s}_{2}^{ + } \geq  0
$$

TopAd's management estimates that the exposure goal is twice as important as the budget goal. The combined objective function thus becomes

$$
\text{ Minimize }z = 2{G}_{1} + {G}_{2} = 2{s}_{1}^{ - } + {s}_{2}^{ + }
$$

The optimum solution is $z = {10},{x}_{1} = 5\mathrm{\;{min}},{x}_{2} = {2.5}\mathrm{\;{min}},{s}_{1}^{ - } = 5$ million persons, ${s}_{1}^{ - } = 0$ , and ${s}_{2}^{ - } = 0$ .

The fact that the optimum value of $z$ is not zero indicates that at least one of the goals is not met. Specifically, ${s}_{1}^{ - } = 5$ means that the exposure goal (of at least 45 million persons) is missed by 5 million individuals. Conversely, the budget goal (of not exceeding \$100,000) is not violated, because ${s}_{2}^{ + } = 0$ . ^topadsolution

## Aha! Moment: Satisficing versus Maximizing, or How Long to Age Wine! ^satisficing

In his book Science of the Artificial, American Nobel Laureate Herbert A. Simon (1916-2001) coined the verb satisfice (a combination of satisfy and suffice) as an alternative goal to maximize in decision making. The difference is explained by the dilemma of an immortal (presumably expecting eternal life) in possession of a bottle of fine wine. The wine gets tastier with age and the immortal must decide when to consume it. The satisficer would choose a reasonable future time to open the bottle but the maximizer would say never!

Though GP is presented in the context of optimized linear programs, its end result seeks a satisficing rather than an optimum solution. This conclusion can be demonstrated by Example 8.2-1, where the "optimum" GP solution yields ${x}_{1} = 5\mathrm{\;{min}}$ and ${x}_{2} = {2.5}\mathrm{\;{min}}$ with exposure of 40 million persons and a cost $\$ {100},{000}$ . By contrast, the feasible solution ${x}_{1} = 6\mathrm{\;{min}}$ and ${x}_{2} = 2\mathrm{\;{min}}$ yields the same exposure ( $4 \times  6 + 8 \times  2 = {40}$ million persons) but costs less $\left( {8 \times  6 + {24} \times  2 = \$ {96},{000}}\right)$ . In essence, what GP does is to find a satisficing rather than an optimum solution. The failure to find the best solution raises doubts about the viability of GP as an optimization technique (see Example 8.2-3 for further discussion). ^satisficingexample

#### 8.2.2 The Preemptive Method ^preemptive

In the preemptive method, the decision maker ranks the goals of the problem in order of importance. Given an $n$ -goal situation, the objectives of the problem are written as

$$
\text{ Minimize }{G}_{1} = {\rho }_{1}\text{ (Highest priority) }
$$

$$
\vdots
$$

$$
\text{ Minimize }{G}_{n} = {\rho }_{n}\text{ (Lowest priority) }
$$

The variable ${\rho }_{i}$ is the component of the deviational variables, ${s}_{i}^{ - }$ or ${s}_{i}^{ + }$ , representing goal i. For example, in the TopAd model (Example 8.2-1), ${\rho }_{1} = {s}_{1}^{ - }$ and ${\rho }_{2} = {s}_{2}^{ + }$ . ^rho

The solution procedure starts with optimizing the highest priority, ${G}_{1}$ , and terminates with optimizing the lowest, ${G}_{n}$ . The preemptive method is designed such that $a$ lower-priority solution never degrades a higher-priority solution. ^nondegradation

The literature on GP presents a "special" simplex method that guarantees the nondegradation of higher-priority solutions. The method uses the column-dropping rule that calls for eliminating a nonbasic variable ${x}_{j}$ with nonzero reduced cost $\left( {{z}_{j} - {c}_{j} \neq  0}\right)$ from the optimal tableau of goal ${G}_{k}$ prior to solving the problem of goal ${G}_{k + 1}$ . The rule recognizes that such nonbasic variables, if elevated above zero level in the optimization of succeeding goals, may degrade (but never improve) the quality of a higher-priority goal. The procedure requires including the objective functions of all the goals in the simplex tableau of the model. ^columndropping

The proposed column-dropping modification needlessly complicates GP. In this presentation, we show that the same results can be achieved in a more straightforward manner using the following steps: ^stepprocedure

Step 0. Identify the goals of the model and rank them in order of priority:

$$
{G}_{1} = {\rho }_{1} > {G}_{2} = {\rho }_{2} > \cdots  > {G}_{n} = {\rho }_{n}
$$

Set $i = 1$ .

General Step. Solve ${\mathrm{{LP}}}_{i}$ that minimizes ${G}_{i}$ , and let ${\rho }_{i} = {\rho }_{i}^{ * }$ define the corresponding optimum value of the deviational variable ${\rho }_{i}$ . If $i = n$ , stop; ${\mathrm{{LP}}}_{n}$ solves the $n$ -goal program. Otherwise, add the constraint ${\rho }_{i} = {\rho }_{i}^{ * }$ to the constraints of the ${G}_{i}$ -problem to ensure that the value of ${\rho }_{i}$ is not degraded in future problems. Set $i = i + 1$ , and repeat step $i$ .

The successive addition of the special constraints ${\rho }_{i} = {\rho }_{i}^{ * }$ may not be as "elegant" theoretically as the column-dropping rule. Nevertheless, it achieves the exact same result. More importantly, it is easier to implement and to understand.

Remarks. Some may argue that the column-dropping rule offers computational advantage because the rule makes the problem successively smaller by removing variables, whereas our procedure makes the problem larger by adding new constraints. Considering the nature of the additional constraints $\left( {{\rho }_{i} = {\rho }_{i}^{ * }}\right)$ , we can modify the simplex algorithm to implement the additional constraint implicitly by substituting out ${\rho }_{i} = {\rho }_{i}^{ * }$ . The substitution (affecting only the constraint in which ${\rho }_{i}$ appears) reduces the number of variables as the algorithm moves from one goal to the next. Alternatively, we can use the bounded simplex method of Section 7.4.2 by replacing ${\rho }_{i} = {\rho }_{i}^{ * }$ with ${\rho }_{i} \leq  {\rho }_{i}^{ * }$ , in which case the additional constraints are accounted for implicitly. In this regard, the column-dropping rule, theoretical appeal aside, does not appear to offer a particular computational advantage. ^remarks

For the sake of completeness, Example 8.2-3 will illustrate how the column-dropping rule works.

## Example 8.2-2 ^examplepreemptive

---

The problem of Example 8.2-1 is solved by the preemptive method. Assume that the exposure

goal has a higher priority.

Step 0. ${G}_{1} \succ  {G}_{2}$

$$
{G}_{1}\text{ : Minimize }{s}_{1}^{ - }\text{ (Satisfy exposure goal) }
$$

$$
{G}_{2}\text{ : Minimize }{s}_{2}^{ + }\text{ (Satisfy budget goal) }
$$

Step 1. Solve ${\mathrm{{LP}}}_{1}$ .

$$
\text{ Minimize }{G}_{1} = {s}_{1}^{ - }
$$

		subject to

$$
4{x}_{1} + 8{x}_{2} + {s}_{1}^{ - } - {s}_{1}^{ + }\; = {45}\text{ (Exposure goal) }
$$

$$
8{x}_{1} + {24}{x}_{2}\; + {s}_{2}^{ - } - {s}_{2}^{ + } = {100}\text{ (Budget goal) }
$$

$$
{x}_{1} + 2{x}_{2}\; \leq  {10}\text{ (Personnel limit) }
$$

$$
{x}_{1}\; \leq  \;6\text{ (Radio limit) }
$$

$$
{x}_{1},{x}_{2},{s}_{1}^{ - },{s}_{1}^{ + },{s}_{2}^{ - },{s}_{2}^{ + } \geq  0
$$

---

The optimum solution (determined by TORA) is ${x}_{1} = 5\min ,{x}_{2} = {2.5}\min ,{s}_{1}^{ - } = 5$ million people, with the remaining variables equal to zero. The solution shows that the exposure goal, ${G}_{1}$ , is violated by 5 million persons. The additional constraint to be added to the ${G}_{2}$ -problem is ${s}_{1}^{ - } = 5$ (or, equivalently, ${s}_{1}^{ - } \leq  5$ ).

Step 2. The objective function of ${\mathrm{{LP}}}_{2}$ is

$$
\text{ Minimize }{G}_{2} = {s}_{2}^{ + }
$$

The constraints are the same as in step 1 plus the additional constraint ${s}_{1}^{ - } = 5$ . (TORA's MODIFY option can be used conveniently to represent the new constraint by assigning 5 to both the lower and upper bounds of ${s}_{1}^{ - }$ .)

In general, the additional constraint ${s}_{1}^{ - } = 5$ can also be accounted for by substituting out ${s}_{1}^{ - }$ in the first constraint. The result is that the right-hand side of the exposure goal constraint will be changed from 45 to 40, thus reducing ${\mathrm{{LP}}}_{2}$ to

$$
\text{ Minimize }{G}_{2} = {s}_{2}^{ + }
$$

subject to

$$
4{x}_{1} + 8{x}_{2} - {s}_{1}^{ + }\; = {40}\text{ (Exposure goal) }
$$

$$
8{x}_{1} + {24}{x}_{2}\; + {s}_{2}^{ - } - {s}_{2}^{ + } = {100}\text{ (Budget goal) }
$$

$$
{x}_{1} + 2{x}_{2}\; \leq  {10}\text{ (Personnel limit) }
$$

$$
{x}_{1}\; \leq  \;6\text{ (Radio limit) }
$$

$$
{x}_{1},{x}_{2},{s}_{1}^{ + },{s}_{2}^{ - },{s}_{2}^{ + } \geq  0
$$

The new formulation is one variable less than the one in ${\mathrm{{LP}}}_{1}$ , which is the general idea advanced by the column-dropping rule.

Actually, the optimization of ${\mathrm{{LP}}}_{2}$ is not necessary in this problem, because the optimum solution to problem ${G}_{1}$ already yields ${s}_{2}^{ + } = 0$ ; that is, it is already optimum for ${\mathrm{{LP}}}_{2}$ . Such computational-saving opportunities should be exploited during the course of implementing the preemptive method. ^preemptiveinsight

## Example 8.2-3 (Column-Dropping Rule) ^examplecolumndrop

In this example, we show that a better solution for the problem of Examples 8.2-1 and 8.2-2 can be obtained if the preemptive method is used to optimize objectives rather than to satisfice goals. Later on, the same example is solved using the column-dropping rule.

The goals of Example 8.2-1 can be restated as ^restated

$$
\text{ Priority 1: Maximize exposure }\left( {P}_{1}\right)
$$

$$
\text{ Priority 2: Minimize cost }\left( {P}_{2}\right)
$$

Mathematically, the two objectives are given as

$$
\text{ Maximize }{P}_{1} = 4{x}_{1} + 8{x}_{2}\;\text{ (Exposure) }
$$

$$
\text{ Minimize }{P}_{2} = 8{x}_{1} + {24}{x}_{2}\;\text{ (Cost) }
$$

The specific goal limits for exposure and cost (=45 and 100) in Examples 8.2-1 and 8.2-2 are removed, because we will allow the simplex method to determine these limits optimally.

The new problem can thus be stated as

$$
\text{ Maximize }{P}_{1} = 4{x}_{1} + 8{x}_{2}
$$

$$
\text{ Minimize }{P}_{2} = 8{x}_{1} + {24}{x}_{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  {10}
$$

$$
{x}_{1} \leq  6
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

We first solve the problem using the procedure introduced in Example 8.2-2.

Step 1. Solve ${\mathrm{{LP}}}_{1}$ .

$$
\text{ Maximize }{P}_{1} = 4{x}_{1} + 8{x}_{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  {10}
$$

$$
{x}_{1} \leq  6
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The optimum solution (obtained by TORA) is ${x}_{1} = 0,{x}_{2} = 5$ with ${P}_{1} = {40}$ , which shows that the most exposure we can get is 40 million persons.

Step 2. Add the constraint $4{x}_{1} + 8{x}_{2} \geq  {40}$ to ensure that goal ${G}_{1}$ is not degraded. Thus, we solve ${\mathrm{{LP}}}_{2}$ as

$$
\text{ Minimize }{P}_{2} = 8{x}_{1} + {24}{x}_{2}
$$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  {10}
$$

$$
{x}_{1} \leq  6
$$

$$
4{x}_{1} + 8{x}_{2} \geq  {40}\text{ (additional constraint) }
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The optimum solution of ${\mathrm{{LP}}}_{2}$ is ${P}_{2} = \$ {96},{000},{x}_{1} = 6\mathrm{\;{min}}$ , and ${x}_{2} = 2\mathrm{\;{min}}$ . It yields the same exposure $\left( {{P}_{1} = {40}}\right.$ million people) but at a smaller cost than the one in Example 8.2-2, where we seek to satisfy rather than optimize the goals. ^twostage

The same problem is solved now by using the column-dropping rule. The rule calls for carrying the objective rows associated with all the goals in the simplex tableau, as we will show below.

${\mathrm{{LP}}}_{1}$ (Exposure maximization). The ${\mathrm{{LP}}}_{1}$ simplex tableau carries both objective rows ${P}_{1}$ and ${P}_{2}$ . The optimality condition applies to the ${P}_{1}$ -objective row only. The ${P}_{2}$ -row plays a passive role in ${\mathrm{{LP}}}_{1}$ but must be updated (using the simplex row operations) with the rest of the simplex tableau in preparation for the optimization of ${\mathrm{{LP}}}_{2}$ .

${\mathrm{{LP}}}_{1}$ is solved in two iterations as follows: ^tableauone

| Iteration | Basic | ${x}_{1}$ | ${x}_{2}$ | ${s}_{1}$ | ${s}_{2}$ | Solution |
|---:|---|---:|---:|---:|---:|---:|
| 1 | ${P}_{1}$ | -4 | -8 | 0 | 0 | 0 |
| 1 | ${P}_{2}$ | -8 | -24 | 0 | 0 | 0 |
| 1 | ${s}_{1}$ | 1 | 2 | 1 | 0 | 10 |
| 1 | ${s}_{2}$ | 1 | 0 | 0 | 1 | 6 |
| 2 | ${P}_{1}$ | 0 | 0 | 4 | 0 | 40 |
| 2 | ${P}_{2}$ | 4 | 0 | 12 | 0 | 120 |
| 2 | ${x}_{2}$ | $\frac{1}{2}$ | 1 | $\frac{1}{2}$ | 0 | 5 |
| 2 | ${s}_{2}$ | 1 | 0 | 0 | 1 | 6 |

The last tableau yields the optimal solution ${x}_{1} = 0,{x}_{2} = 5$ , and ${P}_{1} = {40}$ .

The column-dropping rule calls for eliminating any nonbasic variable ${x}_{j}$ with ${z}_{j} - {c}_{j} \neq  0$ from the optimum tableau of ${\mathrm{{LP}}}_{1}$ before ${\mathrm{{LP}}}_{2}$ is optimized. The reason is that these variables, if left unchecked, could become positive in lower-priority optimization problems, which can degrade the quality of higher-priority solutions.

${\mathbf{{LP}}}_{2}$ (Cost minimization). The column-dropping rule eliminates ${s}_{1}$ (with ${z}_{j} - {c}_{j} = 4$ in $\left. {\mathrm{{LP}}}_{1}\right)$ . We can see from the ${P}_{2}$ -row that if ${s}_{1}$ is not eliminated, it will be the entering variable at the start of the ${P}_{2}$ -iterations and will yield the optimum solution ${x}_{1} = {x}_{2} = 0$ , which will degrade the optimum objective value of the ${P}_{1}$ -problem from ${P}_{1} = {40}$ to ${P}_{1} = 0$ . (Try it!)

The ${P}_{2}$ -problem is of the minimization type. Following the elimination of ${s}_{1}$ , the variable ${x}_{1}$ with ${z}_{j} - {c}_{j} = 4\left( { >  - 0}\right)$ can improve the value of ${P}_{2}$ . The following table shows the ${\mathrm{{LP}}}_{2}$ iterations. The ${P}_{1}$ -row has been deleted because it serves no purpose in the optimization of ${\mathrm{{LP}}}_{2}$ . ^tableautwo

| Iteration | Basic | ${x}_{1}$ | ${x}_{2}$ | ${s}_{1}$ | ${s}_{2}$ | Solution |
|---:|---|---:|---:|---:|---:|---:|
| 1 | ${P}_{1}$ |  |  |  |  | 40 |
| 1 | ${P}_{2}$ | 4 | 0 |  | 0 | 120 |
| 1 | ${x}_{2}$ | $\frac{1}{2}$ | 1 |  | 0 | 5 |
| 1 | ${s}_{2}$ | 1 | 0 |  | 1 | 6 |
| 2 | ${P}_{1}$ |  |  |  |  | 40 |
| 2 | ${P}_{2}$ | 0 | 0 |  | -4 | 96 |
| 2 | ${x}_{2}$ | 0 | 1 |  | $- \frac{1}{2}$ | 2 |
| 2 | ${x}_{1}$ | 1 | 0 |  | 1 | 6 |

The optimum solution $\left( {{x}_{1} = 6,{x}_{2} = 2}\right)$ with a total exposure of ${P}_{1} = {40}$ and a total cost of ${P}_{2} = {96}$ is the same as obtained earlier.

## AMPL Moment ^ampl

AMPL lends itself readily to applying the idea presented in Example 8.2-2, where simple constraints are added to ensure that higher-priority solutions are not degraded. File amplEx8.1-1.txt provides a generic AMPL code that allows the application of the preemptive method. The model must be implemented interactively as explained in Section C.9 on the website.

## BIBLIOGRAPHY ^bibliography

Chissman, J., T. Fey, G. Reeves, H. Lewis, and R Weinstein, "A Multiobjective Linear Programming Methodology for Public Sector Tax Planning," Interfaces, Vol. 19, No. 5, pp. 13-22, 1989.

Cohon, T. L., Multiobjective Programming and Planning, Academic Press, New York, 1978.

Ignizio, J. P., and T. M. Cavalier, Linear Programming, Prentice-Hall, Upper Saddle River, NJ, 1994.

Steuer, R. E., Multiple Criteria Optimization: Theory, Computations, and Application, Wiley, New York, 1986.

## Case Study: Allocation of Operating Room Time in Mount Sinai Hospital ${}^{2}$ ^casestudy

Tools: GP, ILP

## Area of application: Health care

## Description of the situation: ^casecontext

The situation takes place in Canada, where health-care insurance is mandatory and universal for all citizens. Funding, which is based on a combination of premiums and taxes, is controlled by the individual provinces. Under this system, hospitals are advanced a fixed annual budget and each province pays physicians retroactively using a fee-for-service funding mechanism. Local governments control the size of the health-care system by placing limits on hospital spending. The result is that the use of health resources, particularly operating rooms, is controlled effectively.

Mount Sinai Hospital has 10 staffed operating rooms serving 5 departments: surgery, gynecology, ophthalmology, otolaryngology, and oral surgery. There are 8 main surgical rooms and 2 elective outpatient surgery (EOPS) rooms. An operating room is either "short" or "long," depending on the daily number of hours the room is in use. Because of the socialized nature of health care in Canada, all surgeries are scheduled during work days only (Monday through Friday). Table 8.1 summarizes the daily availability of the different types of rooms and Table 8.2 provides the weekly demand for operating room hours. The limit on the underal-located hours in Table 8.2 is the most hours a department can be denied relative to its weekly request.

---

${}^{2}$ J. T. Blake and J. Donald,"Mount Sinai Hospital Uses Integer Programming to Allocate Operating Room Time," Interfaces, Vol. 32, No. 2, pp. 63-73, 2002.

---

TABLE 8.1 Surgery Room Availability in Mount Sinai Hospital ^tableavailability

| Weekday | Main "short" | Main "long" | EOPS "short" | EOPS "long" |
|---|---|---|---|---|
| Monday | 08:00-15:30 | 08:00-17:00 | 08:00-15:30 | 08:00-16:00 |
| Tuesday | 08:00-15:30 | 08:00-17:00 | 08:00-15:30 | 08:00-16:00 |
| Wednesday | 08:00-15:30 | 08:00-17:00 | 08:00-15:30 | 08:00-16:00 |
| Thursday | 08:00-15:30 | 08:00-17:00 | 08:00-15:30 | 08:00-16:00 |
| Friday | 09:00-15:30 | 09:00-17:00 | 09:00-15:30 | 09:00-16:00 |
| Number of rooms | 4 | 4 | 1 | 1 |

TABLE 8.2 Weekly Demand for Operating Room Hours ^tabledemand

| Department | Weekly target hours | Admissible limit of underallocated hours |
|---|---:|---:|
| Surgery | 189.0 | 10.0 |
| Gynecology | 117.4 | 10.0 |
| Ophthalmology | 39.4 | 10.0 |
| Oral surgery | 19.9 | 10.0 |
| Otolaryngology | 26.3 | 10.0 |
| Emergency | 5.4 | 3.0 |

The objective of the study is to determine a reasonably equitable daily schedule for the utilization of available operating rooms. ^caseequity

## Mathematical model: ^model

The best that can be done in this situation is to devise a daily schedule that most satisfies the weekly target hours for the different departments. In other words, we set the target hours for each department as a goal and try to satisfy it. The objective of the model is to minimize the total deviation from the weekly target hours.

Let ^modelvars

$$
{x}_{ijk} = \text{ Number of rooms of type }i\text{ assigned to department }j\text{ on day }k
$$

$$
{d}_{ik} = \text{ Duration (availability in hours) of room type }i\text{ on day }k
$$

$$
{a}_{ik} = \text{ Number of rooms of type }i\text{ available on day }k
$$

$$
{h}_{j} = \text{ Requested (ideal) target hours for department }j
$$

$$
{u}_{j}^{ - } = \text{ Maximum underallocated hours permitted in department }
$$

The given situation involves 6 departments and 4 types of rooms. Thus, $i = 1,2,3,4$ and $j = 1,2,\ldots ,6$ . For a 5-day work week, the index $k$ assumes the values 1 through 5 .

The following integer-GP model represents the Mount Sinai Hospital scheduling situation: ^modelconstraints

$$
\text{ Minimize }z = \mathop{\sum }\limits_{{j = 1}}^{6}\left( \frac{{s}_{j}^{ - }}{{h}_{j}}\right)
$$

subject to

$$
\mathop{\sum }\limits_{{i = 1}}^{4}\mathop{\sum }\limits_{{k = 1}}^{5}{d}_{ik}{x}_{ijk} + {s}_{j}^{ - } - {s}_{j}^{ + } = {h}_{j}\text{ , for all }j \tag{1}
$$

$$
\mathop{\sum }\limits_{{j = 1}}^{6}{x}_{ijk} \leq  {a}_{ik}\text{ , for all }i\text{ and }k \tag{2}
$$

$$
0 \leq  {s}_{j}^{ - } \leq  {u}_{j}^{ - }\text{ , for all }j \tag{3}
$$

$$
{x}_{ijk} \geq  0\text{ and integer for all }i, j\text{ , and }k \tag{4}
$$

$$
{s}_{j}^{ - },{s}_{j}^{ + } \geq  0\text{ , for all }j \tag{5}
$$

The logic of the model is that it may not be possible to satisfy the target hours ${h}_{j}$ for department $j, j = 1,2,\ldots ,6$ . Thus, the objective is to determine a schedule that minimizes possible "underallocation" of rooms to the different departments. To do this, the nonnegative variables ${s}_{i}^{ - }$ and ${s}_{j}^{ + }$ in constraint (1) represent the under- and overallocation of hours relative to the target ${h}_{i}$ for department $j$ . The ratio $\frac{{s}_{j}}{{h}_{j}}$ measures the relative amount of underallocation to department $j$ . Constraint (2) recognizes room availability limits. Constraint (3) is used to limit the amount by which a department is underallocated. The limits ${u}_{j}^{ - }$ are user specified. ^modellogic

## Model results ^modelresults

File amplCase6.txt gives the AMPL model of the problem. Figure 8.1 gives the solution for the data provided in the statement of the problem. It shows that all goals are met $\left( {z = 0}\right)$ , and it details the allocation of rooms (by type) to the different departments during the work week (Monday through Friday). Indeed, the departmental summary given at the bottom of the figure shows that the requests for 5 (out of 6) departments are oversatisfied. This happens to be the case because there is abundance of resources for the week and the model does not try to minimize the overal-location of hours to the different departments. Actually, it makes no sense in the present model to try to do away with overallocation of hours, because the rooms are available and might as well be apportioned to the different departments. In essence, the main concern is about underallocation when available resources do not meet the demand.

## Computational experience ^experience

In the model, the variable ${x}_{ijk}$ represents the number of allocated rooms. It must assume integer values, and here lies a familiar problem that continues to plague integer programming computations. The AMPL model executed rapidly with the set of data given in the description of the problem. However, when the data representing target hours, ${h}_{j}$ , were adjusted slightly (keeping all other data unchanged), the computational experience was totally different. First, the execution time lasted more than $1\mathrm{{hr}}$ (as opposed to a few seconds with the initial set of data) and, after exploring more than 45 million branch-and-bound nodes, failed to produce a feasible solution, let alone the optimum. This experience appears to take place when the supply exceeds the demand. Actually, the behavior of this ILP is unpredictable, because when the objective function is changed to simply minimize the unweighted sum of ${s}_{j}^{ - }$ , all previously unsolvable cases are solved instantly. On the website, the questions at the end of this case (Case 6) outline these computational experiences.

What courses of action are available for overcoming this problem? At first thought, the temptation may be to drop the integer requirement and then round the resulting linear programming solution. This option will not work in this case because, in all likelihood, it will not produce a feasible solution. Given that a specific number of hospital rooms are available, it is highly

z = 0.00

Weekly Time Allocation:

Mon:

Gynecology: 39.0 hrs

4 room(s) type Main_L

1 room(s) type Main_S

Ophthalmology: 17.0 hrs

1 room(s) type Main_S

1 room(s) type EOPS_S

Oral_surgery: 16.5 hrs

1 room(s) type Main_S

1 room(s) type EOPS_L

Otolaryngology: 9.0 hrs

1 room(s) type Main_S

Tue:

Surgery: 17.0 hrs

1 room(s) type Main_S

1 room(s) type EOPS_S

Gynecology: 39.0 hrs

4 room(s) type Main_L

1 room(s) type Main_S

Oral_surgery: 7.5 hrs

1 room(s) type EOPS_L

Otolaryngology: 18.0 hrs

2 room(s) type Main_S

Wed:

Surgery: 66.5 hrs

3 room(s) type Main_L

4 room(s) type Main_S

1 room(s) type EOPS_S

Ophthalmology: 15.0 hrs

1 room(s) type Main_L

1 room(s) type EOPS_L

Thu:

Surgery: 72.5 hrs

4 room(s) type Main_L

3 room(s) type Main_S

1 room(s) type EOPS_L

1 room(s) type EOPS_S

Ophthalmology: 9.0 hrs

1 room(s) type Main_S

Fri:

Surgery: 34.0 hrs

3 room(s) type Main_S

1 room(s) type EOPS_S

Gynecology: 39.0 hrs

4 room(s) type Main_L

1 room(s) type Main_S

Emergency: 6.5 hrs

1 room(s) type EOPS_L

Departmental summary: ^departmentsummary

| Department | Allocated hours | % of target |
|---|---:|---:|
| Surgery | 190.0 | 101% |
| Gynecology | 117.0 | 100% |
| Ophthalmology | 41.0 | 104% |
| Oral_surgery | 24.0 | 121% |
| Otolaryngology | 27.0 | 103% |
| Emergency | 6.5 | 120% |

FIGURE 8.1

Output of Mount Sinai Hospital model unlikely that a trial-and-error rounded solution will meet room availability limits. This means that there is no alternative to imposing the integer condition.

One way to improve the chances for a successful execution of the integer model is to limit the feasible ranges for the variables ${x}_{ijk}$ by taking into account the availability of other resources. For example, if the hospital has only two dental surgeons on a given day, no more than two rooms (of any type) can be assigned to that department on that day. Setting tighter bounds may be effective in securing an optimal integer solution. Short of meeting this requirement, the only remaining option is to devise a heuristic for the problem. ^mitigation

## PROBLEMS ^problems

Assigned problems by section. ^problemstable

| Section | Assigned Problems |
|---|---|
| 8.1 | 8-1 to 8-11 |
| 8.2.1 | 8-12 to 8-21 |
| 8.2.2 | 8-22 to 8-25 |

*8-1. Formulate the Fairville tax problem, assuming that the town council is specifying an additional goal, ${G}_{5}$ , that requires gasoline tax to equal at least ${20}\%$ of the total tax bill.

8-2. The NW Shopping Mall conducts special events to attract potential patrons. Among the events that seem to attract teenagers, the young/middle-aged group, and senior citizens, the two most popular are band concerts and art shows. Their costs per presentation are \$1500 and \$3000, respectively. The total (strict) annual budget allocated to the two events is \$20,000. The mall manager estimates the attendance as follows:

| Event | Teenagers | Young/middle-age | Seniors |
|---|---:|---:|---:|
| Band concert | 200 | 100 | 0 |
| Art show | 0 | 400 | 250 |

The manager has set minimum goals of 1500, 450, and 900 for the attendance of teenagers, the young/middle-aged group, and seniors, respectively. Formulate the problem as a goal programming model.

*8-3. The Ozark University admission office is processing freshman applications for the upcoming academic year. The applications fall into three categories: in-state, out-of-state, and international. The male-female ratios for in-state and out-of-state applicants are 1:1 and 3:2, respectively. For international students, the corresponding ratio is 8:1. The American College Test (ACT) score is an important factor in accepting new students. The statistics gathered by the university indicate that the average ACT scores for in-state, out-of-state, and international students are 27, 26, and 23, respectively. The committee on admissions has established the following desirable goals for the new freshman class:

(a) The incoming class is at least 1200 freshmen.

(b) The average ACT score for all incoming students is at least 25.

(c) International students constitute at least 10% of the incoming class.

(d) The female-male ratio is at least 3:4.

(e) Out-of-state students constitute at least 20% of the incoming class.

Formulate the problem as a GP model.

8-4. Circle K Farms consumes 3 tons of special feed daily. The feed - a mixture of limestone, corn, and soybean meal-must satisfy the following nutritional requirements:

Calcium. At least 0.8% but not more than 1.2%.

Protein. At least 22%.

Fiber. At most 5%.

The following table gives the nutritional content of the feed ingredients:

| Ingredient | Calcium | Protein | Fiber |
|---|---:|---:|---:|
| Limestone | .380 | .00 | .00 |
| Corn | .001 | .09 | .02 |
| Soybean meal | .002 | .50 | .08 |

Formulate the problem as a GP model, and state your opinion regarding the applicability of GP to this situation.

*8-5. Mantel produces a toy carriage, whose final assembly must include four wheels and two seats. The factory producing the parts operates three shifts a day. The following table provides the amounts produced of each part in the three shifts:

| Shift | Wheels | Seats |
|---:|---:|---:|
| 1 | 500 | 300 |
| 2 | 600 | 280 |
| 3 | 640 | 360 |

Ideally, the number of wheels produced is exactly twice that of the number of seats. However, because production rates vary from shift to shift, exact balance in production may not be possible. Mantel is interested in determining the number of production runs in each shift that minimizes the imbalance in the production of the parts. The capacity limitations restrict the number of runs to between 4 and 5 for shift 1, 10 and 20 for shift 2, and 3 and 5 for shift 3. Formulate the problem as a GP model.

8-6. Camyo Manufacturing produces four parts that require the use of a lathe and a drill press. The two machines operate 10 hours a day. The following table provides the time in minutes required by each part:

| Part | Lathe | Drill press |
|---:|---:|---:|
| 1 | 5 | 3 |
| 2 | 6 | 2 |
| 3 | 4 | 6 |
| 4 | 7 | 4 |

It is desired to balance the two machines by limiting the difference between their total operation times to at most 30 minutes. The market demand for each part is at least 10 units. Additionally, the number of units of part 1 may not exceed that of part 2. Formulate the problem as a GP model.

8-7. Two products are manufactured on two sequential machines. The following table gives the machining times in minutes per unit for the two products:

| Machine | Product 1 | Product 2 |
|---:|---:|---:|
| 1 | 5 | 3 |
| 2 | 6 | 2 |

The daily production quotas for the two products are 80 and 60 units, respectively. Each machine runs 8 hours a day. Overtime, though not desirable, may be used if necessary to meet the production quota. Formulate the problem as a GP model.

8-8. Vista City Hospital plans the short-stay assignment of surplus beds (those that are not already occupied) 4 days in advance. During the 4-day planning period, about 30, 25, and 20 patients will require 1-, 2-, or 3-day stays, respectively. Surplus beds during the same period are estimated at20,30,30, and 30, respectively. Use GP to resolve the problem of overadmission and underadmission in the hospital.

8-9. The Von Trapp family is in the process of moving to a new city where both parents have accepted new jobs. In trying to find an ideal location for their new home, the family list the following goals:

(a) It should be as close as possible to Mrs. Von Trapp's place of work (within $\frac{1}{4}$ mile).

(b) It should be as far as possible from the noise of the airport (at least 10 miles).

(c) It should be reasonably close to a shopping mall (within 1 mile).

Mr. and Mrs. Von Trapp use a landmark in the city as a reference point and locate the $\left( {x, y}\right)$ -coordinates of work, airport, and shopping mall at $\left( {1,1}\right) ,\left( {{20},{15}}\right)$ , and $\left( {4,7}\right)$ , respectively (all distances are in miles). Formulate the problem as a GP model. (Note: The resulting constraints are not linear.)

8-10. Regression analysis. In a laboratory experiment, suppose that ${y}_{i}$ is the $i$ th observed (independent) yield associated with the dependent observational measurements ${x}_{ij}, i = 1,2,\ldots , m;j = 1,2,\ldots , n$ . It is desired to determine a linear regression fit into these data points. Let ${b}_{j}, j = 0,1,\ldots , n$ , be the regression coefficients. It is desired to determine all ${b}_{j}$ such that the sum of the absolute deviations between the observed and the estimated yields is minimized. Formulate the problem as a GP model.

8-11. Chebyshev Problem. An alternative goal for the regression model in Problem 8-10 is to minimize over ${b}_{j}$ the maximum of the absolute deviations. Formulate the problem as a GP model.

*8-12. Consider Problem 8-1, dealing with the Fairville tax situation. Solve the problem, assuming that all five goals have the same weight. Does the solution satisfy all the goals?

8-13. In Problem 8-2, suppose that the goal of attracting young/middle-aged people is twice as important as for either of the other two categories (teens and seniors). Find the associated solution, and check if all the goals have been met.

8-14. In the Ozark University admission situation described in Problem 8.3, suppose that the limit on the size of the incoming freshmen class must be met, but the remaining requirements can be treated as flexible goals. Further, assume that the ACT score goal is twice as important as any of the remaining goals.

(a) Solve the problem, and specify whether or not all the goals are satisfied.

(b) If, in addition, the size of the incoming class can be treated as a flexible goal that is twice as important as the ACT goal, how would this change affect the solution?

*8-15. In the Circle K model of Problem 8-4, is it possible to satisfy all the nutritional requirements?

8-16. In Problem 8-5, determine the solution, and specify whether or not the daily production of wheels and seats can be balanced.

8-17. In Problem 8-6, suppose that the market demand goal is twice as important as that of balancing the two machines, and that no overtime is allowed. Solve the problem, and determine if the goals are met.

*8-18. In Problem 8-7, suppose that production strives to meet the quota for the two products, using overtime if necessary. Find a solution to the problem, and specify the amount of overtime, if any, needed to meet the production quota.

8-19. In the Vista City Hospital of Problem 8-8, suppose that only the bed limits represent flexible goals and that all the goals have equal weights. Can all the goals be met?

8-20. The Malco Company has compiled the following table from the files of five of its employees to study the impact on income of three factors: age, education (expressed in number of college years completed), and experience (expressed in number of years in the business).

| Age (year) | Education (year) | Experience (year) | Annual income ($) |
|---:|---:|---:|---:|
| 30 | 4 | 5 | 40,000 |
| 39 | 5 | 10 | 48,000 |
| 44 | 2 | 14 | 38,000 |
| 48 | 0 | 18 | 36,000 |
| 37 | 3 | 9 | 41,000 |

Use the GP formulation in Problem 8-10 to fit the data into the linear equation $y = {b}_{0} + {b}_{1}{x}_{1} + {b}_{2}{x}_{2} + {b}_{3}{x}_{3}.$

8-21. Solve Problem 8-20 using the Chebyshev method proposed in Problem 8-11.

8-22. In Example 8.2-2, suppose that the budget goal is increased to \$150,000. The exposure goal remains unchanged at 45 million persons. Show how the preemptive method will reach a solution. ${}^{3}$

*8-23. Solve Problem 8-1 using the following priority ordering for the goals:

$$
{G}_{1} > {G}_{2} > {G}_{3} > {G}_{4} > {G}_{5}.
$$

8-24. Consider Problem 8-2, which deals with the presentation of band concerts and art shows at the NW Mall. Suppose that the goals set for teens, the young/middle-aged group, and seniors are referred to as ${G}_{1},{G}_{2}$ , and ${G}_{3}$ , respectively. Solve the problem for each of the following priority orders:

(a) ${G}_{1} \succ  {G}_{2} \succ  {G}_{3}$

(b) ${G}_{3} \succ  {G}_{2} \succ  {G}_{1}$

Show that the satisfaction of the goals (or lack of it) can be a function of the priority order.

8-25. Solve the Ozark University model (Problem 8-3) using the preemptive method, assuming that the goals are prioritized in the same order given in the problem.
