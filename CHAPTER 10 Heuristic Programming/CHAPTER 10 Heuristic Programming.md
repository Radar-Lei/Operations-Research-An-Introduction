```markmap
---
markmap:
  height: 650
---
# [[#^chapterten|CHAPTER 10 Heuristic Programming]]
## [[#^fedexcase|Real-Life Application: FedEx Bid Lines via Simulated Annealing]]
### [[#^fedexsetting|Problem Setting]]
### [[#^fedexobjective|Objective: Minimize Required Bid Lines]]
### [[#^fedexsa|Why Simulated Annealing]]
## [[#^tenone|10.1 Introduction]]
### [[#^heuristicsintro|What Is a Heuristic]]
### [[#^greedylocal|Greedy Local Search and Local Optima]]
### [[#^metaintro|Metaheuristics: Escaping Local Traps]]
### [[#^chapterroadmap|Chapter Roadmap]]
## [[#^franklin|Aha Moment: Franklin Rule]]
### [[#^franklincontext|Franklin as Early OR Thinker]]
### [[#^franklinprocon|Pro–Con List and Pairwise Elimination]]
### [[#^franklinalgebra|Moral or Prudential Algebra]]
## [[#^greedysection|10.2 Greedy (Local Search) Heuristics]]
### [[#^greedyproblem|Single-Variable Problem Template]]
### [[#^greedyprocess|Iterative Neighborhood Improvement]]
### [[#^neighborhood|Neighborhood Design Tradeoff]]
### [[#^discretesection|10.2.1 Discrete Variable Heuristic]]
#### [[#^greedyexamplea|Example: Immediate Neighborhood Gets Local Minimum]]
#### [[#^tablegreedya|Table: Immediate-Neighborhood Iterations]]
#### [[#^greedyimprove|Improving Solution Quality]]
#### [[#^randomwalkexample|Example: Random-Walk with Expanded Neighborhood]]
#### [[#^tablerandomwalk|Table: Random-Walk Iterations]]
### [[#^continuoussection|10.2.2 Continuous Variable Heuristic]]
#### [[#^uniformdisp|Uniform Displacement Rule]]
#### [[#^normaldisp|Normal Displacement Rule]]
#### [[#^continuousexample|Example: Polynomial Minimization on [0,4]]]
#### [[#^tableuniform|Table: Uniform-Sampling Iterations]]
#### [[#^tablenormal|Table: Normal-Sampling Iterations]]
#### [[#^multivariable|Extension to Multiple Variables]]
#### [[#^excelcontinuous|Excel Moment: Continuous Random-Walk Heuristic]]
## [[#^metasection|10.3 Metaheuristic]]
### [[#^metatermination|Common Termination Benchmarks]]
### [[#^tabusection|10.3.1 Tabu Search]]
#### [[#^tabuexamplea|Example: Single-Variable Tabu Search Basics]]
#### [[#^tabletabua|Table: Tabu Search Iterations]]
#### [[#^tabuexampleb|Example: Job Sequencing with Tabu Tenure]]
#### [[#^tablejobsdataa|Table: Job Sequencing Data]]
#### [[#^tablecostcalc|Cost Computation for a Sequence]]
#### [[#^tabletabujobs|Table: Tabu Search Iterations for Sequencing]]
#### [[#^tabufinetune|Fine-Tuning: Aspiration and Search Control]]
#### [[#^tabusummary|Summary of Tabu Search Algorithm]]
### [[#^sasection|10.3.2 Simulated Annealing]]
#### [[#^satemperature|Temperature Schedule]]
#### [[#^saaccept|Acceptance Probability for Inferior Moves]]
#### [[#^tablesaexample|Table: SA Iterations on Single Variable]]
#### [[#^saexamplea|Example: Walkthrough of SA Computations]]
#### [[#^saexampleb|Example: Job Sequencing with SA]]
#### [[#^tablejobsdatab|Table: Job Sequencing Data]]
#### [[#^tablesajobs|Table: SA Iterations for Sequencing]]
#### [[#^sasummary|Summary of Simulated Annealing Algorithm]]
### [[#^gasection|10.3.3 Genetic Algorithm]]
#### [[#^gageneral|Encoding, Population, and Fitness]]
#### [[#^gaexamplea|Example: GA on Single-Variable Domain]]
#### [[#^tablesampling|Table: Sampling Distribution]]
#### [[#^tablepopulation|Table: Starting Population]]
#### [[#^gacrossover|Crossover Rules]]
#### [[#^gamutation|Mutation and Feasibility Handling]]
#### [[#^gacontinuous|Handling Continuous Variables with Binary Strings]]
#### [[#^gaexampleb|Example: Job Sequencing Chromosome as Sequence]]
#### [[#^tablejobsdatac|Table: 5-Job Data]]
#### [[#^gajobencoding|One-Point Crossover Example for Sequences]]
#### [[#^gasummary|Summary of Genetic Algorithm]]
#### [[#^tablegajobs|Table: GA Iterations for Sequencing]]
## [[#^ilpsection|10.4 Metaheuristics for Integer Linear Programs]]
### [[#^ilpmodel|General ILP Form]]
### [[#^ilpstart|Starting Solution via Rounded LP Optimum]]
### [[#^ilpneighborhood|Neighborhood: Change One Variable by ±1]]
### [[#^ilpinfeasibility|Infeasibility Measure]]
### [[#^ilptabu|10.4.1 ILP Tabu Algorithm]]
#### [[#^ilpexamplea|Example: ILP Tabu Search Walkthrough]]
#### [[#^tableilptabu|Table: ILP Tabu Iterations]]
### [[#^ilpsa|10.4.2 ILP Simulated Annealing Algorithm]]
#### [[#^ilpsaaccept|Acceptance Rule for Inferior Feasible Moves]]
#### [[#^ilpexampleb|Example: ILP SA Iterations]]
#### [[#^tableilpsa|Table: ILP SA Iterations]]
### [[#^ilpga|10.4.3 ILP Genetic Algorithm]]
#### [[#^tablebinary|Table: Binary Coding Example]]
#### [[#^tableranges|Table: Random Initial Population Ranges]]
#### [[#^ilpexamplec|Example: ILP GA with Crossover and Mutation]]
#### [[#^tableilpga|Table: ILP GA Starting Population]]
## [[#^cpsection|10.5 Introduction to Constraint Programming]]
### [[#^cppropagation|Constraint Propagation and Domain Tightening]]
### [[#^cptree|Search Tree Strategy]]
### [[#^oplcode|ILOG OPL Model Sketch]]
## [[#^bibliography|Bibliography]]
## [[#^problems|Problems]]
### [[#^tableproblems|Problems by Section Table]]
```

## CHAPTER 10 Heuristic Programming ^chapterten

## Real-Life Application: FedEx Generates Bid Lines Using Simulated Annealing ^fedexcase

FedEx delivers millions of items throughout the world daily using a fleet of more than 500 aircraft and more than 3000 pilots. Bid lines (roundtrips), starting and ending at one of nine crew domiciles (or hubs), must satisfy numerous Federal Aviation Administration and FedEx regulations and, to the extent possible, personal preferences based on pilots' seniority. ^fedexsetting

The main objective is to minimize the required number of bid lines (i.e., required manning). ^fedexobjective

The complexity of the constraints precludes the implementation of an integer programming model. Instead, a simulated annealing heuristic is used to solve the problem. ${}^{1}$ ^fedexsa

### 10.1 INTRODUCTION ^tenone

Heuristics are designed to find good, approximate solutions to difficult combinatorial problems that otherwise cannot be solved by available optimization algorithms. A heuristic is a direct search technique that uses favorable rules of thumb to locate improved solutions. The advantage of heuristics is that they usually find (good) solutions quickly. The disadvantage is that the quality of the solution (relative to the optimum) is generally unknown. ^heuristicsintro

Early generations of heuristics are based on the greedy search rule that mandates making improvement in the value of the objective function with each search move. The search ends at a local optimum where no further improvements are possible. ^greedylocal

In the 1980s, a new generation of metaheuristics sought to improve the quality of the heuristic solutions by allowing the search to escape entrapment at local optima. The realized advantage comes at the expense of increased computations. ^metaintro

---

${}^{1}$ Details of the study can be found in Camplell, K., B. Durfee, and G. Hines,"FedEx Bid Lines Using Simulated Annealing," Interfaces, Vol. 27, No. 2, pp. 1-16, 1997.

---

Section 10.2 deals with the greedy heuristic. Section 10.3 presents three prominent metaheuristics: tabu, simulated annealing, and genetic. Section 10.4 applies metaheuris-tics to the general integer programming problem. The chapter concludes in Section 10.5 with a brief discussion of the related constrained-based search known as constraint programming. ^chapterroadmap

## Aha! Moment: Earliest Decision-Making Heuristic-The Franklin Rule ^franklin

Some argue that Benjamin Franklin (1705-1790) is the first ever operations researcher, and he might well have been, at least in the Americas. He was a person of diverse superior talents, but his association with OR (at best informal) originates from a letter ${}^{2}$ he wrote in 1772 to the famed English natural philosopher and scientist Joseph Priestley (discoverer of oxygen), in which he outlined a first-ever publicized description of a decision-making heuristic using the pro and con list. He described the heuristic, now dubbed the Franklin Rule, in the following manner: ^franklincontext

In the Affair of so much Importance to you, wherein you ask my Advice, I cannot for want of sufficient Premises, advise you what to determine, but if you please I will tell you how.

When these difficult Cases occur, they are difficult chiefly because while we have them under Consideration all the Reasons pro and con are not present to the Mind at the same time; but sometimes one Set present themselves, and at other times another, the first being out of Sight. Hence the various Purposes or Inclinations that alternately prevail, and the Uncertainty that perplexes us.

To get over this, my Way is, to divide half a Sheet of Paper by a Line into two Columns, writing over the one Pro, and over the other Con. Then during three or four Days Consideration I put down under the different Heads short Hints of the different Motives that at different Times occur to me for or against the Measure. When I have thus got them all together in one View, I endeavour to estimate their respective Weights; and where I find two, one on each side, that seem equal, I strike them both out: If I find a Reason pro equal to some two Reasons con, I strike out the three. If I judge some two Reasons con equal to some three Reasons pro, I strike out the five; and thus proceeding I find at length where the Ballance lies; and if after a Day or two of farther Consideration nothing new that is of Importance occurs on either side, I come to a Determination accordingly. ^franklinprocon

And tho' the Weight of Reasons cannot be taken with the Precision of Algebraic Quantities, yet when each is thus considered separately and comparatively, and the whole lies before me, I think I can judge better, and am less likely to take a rash Step; and in fact I have found great Advantage from this kind of Equation, in what may be called Moral or Prudential Algebra. ^franklinalgebra

### 10.2 GREEDY (LOCAL SEARCH) HEURISTICS ^greedysection

The main ideas of the greedy heuristic are explained via a single-variable problem. These ideas are subsequently extended to cover multiple variables.

Define the optimization problem with a solution space $S$ as ^greedyproblem

$$
\text{ Minimize }z = F\left( x\right) , x \in  S
$$

---

${}^{2}$ W. Bell Jr., ed. "Benjamin Franklin’s 1772 letter to Joseph Priestley," Mr. Franklin: A Selection from His Personal Letters. New Haven, CT: Yale University Press, 1956.

---

The iterative process of a greedy heuristic starts from a (random) feasible point and then attempts to move to a better solution point in the neighborhood of the current solution point. Specifically, at iteration $k$ , given the solution point ${x}_{k}$ , the heuristic examines all the feasible points in the neighborhood $N\left( {x}_{k}\right)$ in search of a better solution. The search ends when no further improvements are possible. ^greedyprocess

The definition of $N\left( {x}_{k}\right)$ is important in the design of the heuristic. For example, for integer $x, N\left( {x}_{k}\right)  = \left\{  {{x}_{k} - 1,{x}_{k} + 1}\right\}$ defines the immediate neighborhood of ${x}_{k}$ . Alternatively, an expanded neighborhood can include additional neighboring solution points. The first definition involves less local search computations but could impair the quality of the final solution. The second definition (expanded neighborhood) requires more local search computations, but could lead to improvement in the quality of the solution. ^neighborhood

Sections 10.2.1 and 10.2.2 apply the greedy heuristic to discrete and continuous single variables. Extension of the heuristic to multiple variables is discussed at the end of Section 10.2.2.

#### 10.2.1 Discrete Variable Heuristic ^discretesection

This section presents two examples that use the greedy heuristic for estimating the optimum of a single discrete-variable function. The first example uses the immediate neighborhood and the second one expands the domain to include more solution points.

Example 10.2-1 ^greedyexamplea

Consider the function $F\left( x\right)$ given in Figure 10.1 and define the optimization problem as

$$
\text{ Minimize }F\left( x\right) , x \in  S = \{ 1,2,\ldots ,8\}
$$

The function has a local minimum at $x = 3\left( B\right)$ and a global minimum at $x = 7\left( D\right)$ .

![bo_d56m4pn7aajc73800nbg_2_309_1451_665_722_0.jpg](bo_d56m4pn7aajc73800nbg_2_309_1451_665_722_0.jpg)

FIGURE 10.1

Function $F\left( x\right) , x \in  S = \{ 1,2,\ldots ,8\}$ , with local minimum at $x = 3$ and global minimum at $x = 7$

TABLE 10.1 Greedy Heuristic Applied to $F\left( x\right)$ in Figure 10.1 Starting at ${x}_{0} = 1$ with $N\left( {x}_{k}\right)  = \left\{  {{x}_{k} - 1,{x}_{k} + 1}\right\}$ ^tablegreedya

| Iteration $k$ | ${x}_{k}$ | $N\left( {x}_{k}\right)$ | $F\left( {{x}_{k} - 1}\right)$ | $F\left( {{x}_{k} + 1}\right)$ | Action |
|---|---:|---|---:|---:|---|
| (Start) 0 | 1 |  |  |  | Set ${x}^{ * } = 1, F\left( {x}^{ * }\right)  = {90}$ , and ${x}_{k + 1} = 1$ |
| 1 | 1 | $\{  - ,2\}$ | - | 60 | $F\left( {{x}_{k} + 1}\right)  < F\left( {x}^{ * }\right)$ : Set ${x}^{ * } = 2, F\left( {x}^{ * }\right)  = {60},{x}_{k + 1} = 2$ |
| 2 | 2 | $\{1,3\}$ | 90 | 50 | $F\left( {{x}_{k} + 1}\right)  < F\left( {x}^{ * }\right)$ : Set ${x}^{ * } = 3, F\left( {x}^{ * }\right)  = {50},{x}_{k + 1} = 3$ |
| (End) 3 | 3 | $\{2,4\}$ | 60 | 80 | $F\left( {{x}_{k} - 1}\right)$ and $F\left( {{x}_{k} + 1}\right)  > F\left( {x}^{ * }\right)$ : Local minimum reached, stop |

Search result: ${x}^{ * } = 3, F\left( {x}^{ * }\right)  = {50}$ , occurs at iteration 2.

Table 10.1 provides the iterations of the heuristic using immediate neighborhood, $N\left( {x}_{k}\right)  = \left\{  {{x}_{k} - 1,{x}_{k} + 1}\right\}$ . The random number $R = {.1002}$ selects the starting point $x = 1$ from among all the feasible points $x = 1,2,\ldots$ , and 8 . At iteration $1, N\left( 1\right)  = \{ 2\}$ because $x = 0$ is infeasible. The search ends at iteration 3 because $F\left( x\right)  > F\left( {{x}^{ * } = 3}\right)$ for all $x \in  N\left( 3\right)$ . This means that the search stops at the local minimum ${x}^{ * } = 3$ with $F\left( {x}^{ * }\right)  = {50}$ .

Table 10.1 shows that the greedy search stops at a local minimum $(x = 3$ in Figure 10.1). We can improve the quality of the solution in two ways: ^greedyimprove

1. Repeat the heuristic using random starting points.

2. Expand the size of the neighborhood to allow reaching more feasible solution points.

The application of the first idea is straightforward and requires no further explanation.

Expanded neighborhood search can be based on evaluating all the neighborhood points, a strategy that increases the computational burden. Alternatively, we can determine the next search move by random selection from the neighborhood. Specifically, at iteration $k$ , the next move, ${x}_{k + 1}$ , is selected from $N\left( {x}_{k}\right)$ with probability $1/m$ , where $m$ is the number of elements in the neighborhood set. Sampling from the same neighborhood is repeated, if necessary, until an improved solution is found or until a specified number of iterations has been reached The random selection rule describes what is known as a random-walk heuristic.

## Example 10.2-2 (Random-Walk Heuristic) ^randomwalkexample

This example applies once again to $F\left( x\right)$ in Figure 10.1. We arbitrarily define the expanded neighborhood set $N\left( {x}_{k}\right)$ as $\left\{  {1,2,\ldots ,{x}_{k} - 1,{x}_{k} + 1,\ldots ,8}\right\}$ . The search starts at ${x}_{0} = 1$ and can continue for any number of iterations (the longer the more likely it is to find a better solution). In this example, the search is limited to 5 iterations to conserve space. Denote ${x}_{k}^{\prime }$ [selected from $N\left( {x}_{k}\right)$ ] as a possible next move. It is accepted as the new search move only if it improves the solution. If it does not, a new random selection from $N\left( {x}_{k}\right)$ is attempted.

Table 10.2 details the application of the random-walk heuristic. In contrast with immediate-neighborhood heuristic in Example 10.2-1, the random-walk heuristic produces the solution $x = 7$ and $F\left( x\right)  = {40}$ at iteration 4, which accidentally happens to be better than the one obtained in Example 10.2-1.

TABLE 10.2 Random-Walk Heuristic Applied to $F\left( x\right)$ in Figure 10.1 Starting at ${x}_{0} = 1$ ^tablerandomwalk

| Iteration $k$ | ${x}_{k}$ | $F\left( {x}_{k}\right)$ | $N\left( {x}_{k}\right)$ | ${R}_{k}$ | ${x}_{k}^{\prime }$ | $F\left( {x}_{k}^{\prime }\right)$ | Action |
|---|---:|---:|---|---:|---:|---:|---|
| (Start) 0 | 1 | 90 |  |  |  |  | ${x}^{ * } = 1, F\left( {x}^{ * }\right)  = {90}$ |
| 1 | 1 | 90 | $\{ 2,3,4,5,6,7,8\}$ | .4128 | 4 | 80 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)$ : Set ${x}^{ * } = 4, F\left( {x}^{ * }\right)  = {80},{x}_{k + 1} = 4$ |
| 2 | 4 | 80 | $\{ 1,2,3,5,6,7,8\}$ | .2039 | 2 | 60 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)$ : Set ${x}^{ * } = 2, F\left( {x}^{ * }\right)  = {60},{x}_{k + 1} = 2$ |
| 3 | 2 | 60 | $\{ 1,3,4,5,6,7,8\}$ | .0861 | 1 | 100 | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample from $N\left( {x}_{k}\right)$ |
| 4 | 2 | 60 | $\{ 1,3,4,5,6,7,8\}$ | .5839 | 6 | 40 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)$ : Set ${x}^{ * } = 6, F\left( {x}^{ * }\right)  = {40},{x}_{k + 1} = 6$ |
| (End) 5 | 6 | 40 | $\{ 1,2,3,4,5,7,8\}$ | .5712 | 4 | 80 | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample from $N\left( {x}_{k}\right)$ |

Best solution: $x = 6, F\left( x\right)  = {40}$ , occurs at iteration 4 .

Note the behavior of the heuristic. At iteration 3, the possible random move ${x}_{k}^{\prime } = 1$ from $N\left( {{x}_{3} = 2}\right)  = \{ 1,3,4,5,6,7,8\}$ does not improve the solution. Hence, at iteration 4 another random move is attempted from the same neighborhood. This time the move produces the superior solution ${x}^{ * } = 6$ .

#### 10.2.2 Continuous Variable Heuristic ^continuoussection

The optimization problem is defined as

$$
\text{ Minimize }F\left( x\right) , L \leq  x \leq  U
$$

The continuous random-walk heuristic differs from that of the discrete case (Example 10.2-2) in the definition of the (continuous) neighborhood and the selection of the next move from the neighborhood. The domain $L \leq  x \leq  U$ defines the continuous neighborhood of ${x}_{k}$ at any iteration $k$ (a subset of this domain is also acceptable).

The next move, ${x}_{k + 1}$ , is computed as a random (positive or negative) displacement above or below ${x}_{k}$ . There are two ways to achieve this result:

1. The displacement is based on a uniform distribution in the range $\left( {-\frac{U - L}{2},\frac{U - L}{2}}\right)$ . Given $R$ is a $\left( {0,1}\right)$ random number, then ^uniformdisp

$$
{x}_{k + 1} = {x}_{k} + \left( {-\left( \frac{U - L}{2}\right)  + R\left( {U - L}\right) }\right)
$$

$$
= {x}_{k} + \left( {R - {.5}}\right) \left( {U - L}\right)
$$

2. The displacement is based on a normal distribution with mean ${x}_{k}$ and standard deviation $\frac{U - L}{6}$ (the estimate of the standard deviation is based on the assumption that $U - L$ approximates the 6-sigma spread of the normal distribution). Thus, ^normaldisp

$$
{x}_{k + 1} = {x}_{k} + \left( \frac{U - L}{6}\right) N\left( {0,1}\right)
$$

The standard $N\left( {0,1}\right)$ deviate is determined from the normal tables in Appendix A, or by using ExcelStatTables.xls. Excel function NORMSINV $\left( R\right)$ may also be used.

In the two formulas given above, it may be necessary to recompute ${x}_{k + 1}$ more than once, using the same ${x}_{k}$ , until ${x}_{k + 1}$ falls within the feasible range $\left( {L, U}\right)$ . Moreover, if $F\left( {x}_{k + 1}\right)$ is not an improved solution relative to $F\left( {x}^{ * }\right)$ , the random selection is repeated for a specified number of iterations or until an improvement is realized, whichever occurs first.

## Example 10.2-3 ^continuousexample

Consider the following problem

$$
\text{ Minimize }F\left( x\right)  = {x}^{5} - {10}{x}^{4} + {35}{x}^{3} - {50}{x}^{2} + {24x},0 \leq  x \leq  4
$$

Starting with $x = {.5}$ , the example details how the random-walk heuristic is used to approximate the minimum solution.

Tables 10.3 and 10.4 provide 5 iterations each using uniform and normal sampling. An increase in the number of iterations usually produces better-quality solutions (relative to the true optimum). Although normal sampling produces a better-quality solution in this example, the result may not be true in general.

The two sampling procedures can be combined into a hybrid heuristic: First, we implement the uniform sampling heuristic. Then the resulting solution is used to start the normal sampling heuristic. The idea is that the normal sampling heuristic may "fine-tune" the solution obtained by the uniform sampling heuristic (see next Excel moment). This idea is implemented later using Excel.

TABLE 10.3 Minimization of $F\left( x\right)  = {x}^{5} - {10}{x}^{4} + {35}{x}^{3} - {50}{x}^{2} + {24x},0 \leq  x \leq  4$ Using Uniform Random-Walk Heuristic with ${x}_{0} = {.5}$ and ${x}_{k}^{\prime } = {x}_{k} + 4\left( {R - {.5}}\right)$ ^tableuniform

| Iteration $k$ | ${x}_{k}$ | $F\left( {x}_{k}\right)$ | ${R}_{k}$ | ${x}_{k}^{\prime }$ | $F\left( {x}_{k}^{\prime }\right)$ | Action |
|---|---:|---:|---:|---:|---:|---|
| (Start) 0 | .5 | 3.281 |  |  |  | Set ${x}^{ * } = {.5}, F\left( {x}^{ * }\right)  = {3.281},{x}_{k + 1} = {.5}$ |
| 1 | .5 | 3.281 | .4128 | .151 | 2.602 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)  : {x}^{ * } = {.1512}, F\left( {x}^{ * }\right)  = {2.602},{x}_{k + 1} = {.151}$ |
| 2 | .1512 | 2.602 | .2039 | -1.033 |  | Out of range: Resample using ${x}_{k + 1} = {x}_{k}$ |
| 3 | .1512 | 2.602 | .9124 | 1.801 | -.757 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)  : {x}^{ * } = {1.801}, F\left( {x}^{ * }\right)  =  - {.757},{x}_{k + 1} = {1.801}$ |
| 4 | 1.801 | -.757 | .5712 | 2.086 | .339 | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample using ${x}_{k + 1} = {x}_{k}$ |
| (End) 5 | 1.801 | -.757 | .8718 | 3.288 | -1.987 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)  : {x}^{ * } = {3.288}, F\left( {x}^{ * }\right)  =  - {1.987},{x}_{k + 1} = {3.288}$ |

Search result: $x = {1.801}, F\left( x\right)  =  - {.757}$ occurs at iteration 3 [exact global minimum: ${x}^{ * } = {3.64438}, F\left( {x}^{ * }\right)  =  - {3.631}$ ].

TABLE 10.4 Minimization of $F\left( x\right)  = {x}^{5} - {10}{x}^{4} + {35}{x}^{3} - {50}{x}^{2} + {24x},0 \leq  x \leq  4$ Using Normal Random-Walk Heuristic with ${x}_{0} = {.5}$ and ${x}_{k}^{\prime } = {x}_{k} + \left( {4/6}\right) N\left( {0,1}\right)$ . ^tablenormal

| Iteration $k$ | ${x}_{k}$ | $F\left( {x}_{k}\right)$ | ${R}_{k}$ | $N\left( {0,1}\right)$ | ${x}_{k}^{\prime }$ | $F\left( {x}_{k}^{\prime }\right)$ | Action |
|---|---:|---:|---:|---:|---:|---:|---|
| (Start) 0 / 1 | .5 / .5 | 3.281 / 3.281 | .4128 | -.2203 | .353 | 3.631 | Set ${x}^{ * } = {.5}, F\left( {x}^{ * }\right)  = {3.281},{x}_{k + 1} = {.5}$ |
| 2 | .5 | 3.281 | .2039 | -.8278 | -.0519 |  | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample using ${x}_{k + 1} = {x}_{k}$ ; Out of range: Resample using ${x}_{k + 1} = {x}_{k}$ |
| 3 | .5 | 3.281 | .9124 | 1.3557 | 1.404 | -1.401 | $F\left( {x}_{k}^{\prime }\right)  < F\left( {x}^{ * }\right)  : {x}^{ * } = {1.404}, F\left( {x}^{ * }\right)  =  - {1.401}$ , ${x}_{k + 1} = {1.404}$ |
| 4 | 1.404 | -1.401 | .5712 | .1794 | 1.523 | -1.390 | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample using ${x}_{k + 1} = {x}_{k}$ |
| (End) 5 | 1.404 | -1.401 | .8718 | 1.1349 | 2.160 | .6219 | $F\left( {x}_{k}^{\prime }\right)  > F\left( {x}^{ * }\right)$ : Resample using ${x}_{k + 1} = {x}_{k}$ |

Search result: $x = {1.404}, F\left( x\right)  =  - {1.401}$ , occurs at iteration 3 [exact global minimum: ${x}^{ * } = {3.64438}, F\left( {x}^{ * }\right)  =  - {3.631}$ ].

Extension of the greedy search multiple variables. Given $\mathbf{X} = \left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)$ and a solution space $S$ , the optimization problem is defined as ^multivariable

$$
\text{ Minimize }z = F\left( \mathbf{X}\right) ,\mathbf{X}{\varepsilon S}
$$

The greedy search algorithm is extended to the multivariable case by targeting the variables one at a time in each iteration, where a target variable is selected randomly from the set $\left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)$ . The single-variable discrete and continuous heuristics given in Sections 10.2.1 and 10.2.2 are then applied to the selected variable.

## Excel Moment ^excelcontinuous

Figure 10.2 is a snapshot of the Excel spreadsheet application of the continuous random-walk heuristic (file excelContSingleVarHeuristic.xls). Using Excel syntax, the function $F\left( x\right)$ is entered in cell D2, with cell D5 assuming the role of the variable $x$ . The sense of optimization (max or min) is specified in cell C2. The search range is entered in cells D3 and D4. The drop-down menu in cell D5 allows the use of uniform or random sampling.

A hybrid heuristic using uniform and normal sampling in tandem can be carried out in the following manner:

1. Assign a starting point in cell H3 and the number of iterations in cell H4.

2. Select uniform sampling in cell D5, and execute the heuristic by pressing the command button in step 6.

3. Use the solution from uniform sampling (cell D6) as a new starting point in cell H3.

4. Select normal sampling in cell D5 and re-execute the heuristic.

FIGURE 10.2

Excel random-walk heuristic for finding the optimum (maximum or minimum) of a single-variable continuous function (file excelContSingleVarHeuristic.xls)

| Cell | Content |
|---|---|
| D2 ${f}_{\mathrm{c}}$ | =D5^5-10*D5^4+35*D5^3-50*D5^2+24*D5 |

| Row | A | B | C | D | E | F | G | H | 1 |
|---:|---|---|---|---|---|---|---|---|---|
|  | A | B | C | D | E | F | G | H | 1 |
| 1 | Random-Walk Heuristic for Continuous Single Variable functions |  |  |  |  |  |  |  |  |
| 2 | Step 1: |  | Enter F(D5) O Max O Mn | 2.325007 |  |  |  |  |  |
| 3 | Step 2a: | Enter lower bound |  | 0 | Step 4: | Enter starting point, x0 |  | 0.5 |  |
| 4 | Step 2b: | Enter upper bound |  | 4 | Step 5: | Enter nbr of iterations, N |  | 5 |  |
| 5 | Step 3: | Select sampling method |  | Uniform | Step 6: | Execute Heuristic |  |  |  |
| 6 | Solution summary: |  | Best solution: | x* = 1.455886 | F(x*) = -1.418696 |  |  |  |  |
| 7 | Iteration, k | xk | F(xk) | R | Uniform | ${\mathrm{x}}^{\prime }$ | F(x') | ${x}^{ * }$ | F(x*) |
| 8 | start | 0.5 | 3.28125 |  |  |  |  | 0.5 | 3.28125 |
| 9 | 1 | 0.5 | 3.28125 | 0.705547512 | 0.82219 | 1.322190046 | -1.2972882 | 1.32219 | -1.297288 |
| 10 | 2 | 1.32219005 | -1.297288179 | 0.53342402 | 0.1336961 | 1.455886126 | -1.4186964 | 1.4558861 | -1.418696 |
| 11 | 3 | 1.45588613 | -1.418696404 | 0.579518616 | 0.3180745 | 1.77396059 | -0.8470017 |  |  |
| 12 | 4 | 1.45588613 | -1.418696404 | 0.289562464 | -0.84175 | 0.614135981 | 2.65298409 |  |  |
| 13 | 5 | 1.45588613 | -1.418696404 | 0.301948011 | -0.792208 | 0.663678169 | 2.32500697 |  |  |

### 10.3 METAHEURISTIC ^metasection

The greedy heuristics presented in Section 10.2 share a common strategy: At iteration $k$ , the search moves to a new point ${\mathbf{X}}_{k + 1} \in  N\left( {\mathbf{X}}_{k}\right)$ only if the new point improves the value of the objective function $F\left( \mathbf{X}\right)$ . If no better ${\mathbf{X}}_{k + 1}$ can be found in $N\left( {\mathbf{X}}_{k}\right)$ or if a user-specified number of iterations is reached, the solution is entrapped at a local optimum and the search ends.

Metaheuristics are primarily designed to escape entrapment at local optima by permitting inferior moves, if necessary. The hope is that the added search flexibility will lead to a better solution.

Unlike the greedy heuristic, which always terminates when a local optimum is reached, termination of a metaheuristic search can be based on one of the following benchmarks: ^metatermination

1. The number of search iterations exceeds a specified number.

2. The number of iterations since the last best solution exceeds a specified number.

3. The neighborhood associated with the current search point is either empty or cannot lead to a new viable search move.

4. The quality of the current best solution is acceptable.

This section presents three prominent search metaheuristics: tabu, simulated annealing, and genetic. These algorithms differ primarily in the manner in which the search escapes a local optimum. Each metaheuristic is illustrated by two examples: The first, dealing with a single-variable function $F\left( x\right)$ , is designed to explain the basics of the metaheuristics. The second, dealing with the more complex job-shop scheduling problem, reveals additional intricacies in the implementation of the metaheuristics. In Chapter 11, the three metaheuristics are applied to the traveling salesperson problem.

#### 10.3.1 Tabu Search Algorithm ^tabusection

When search is trapped at a local optimum, tabu search (TS) selects the next (possibly inferior) search move in a manner that temporarily prohibits reexamining previous solutions. The main instrument for achieving this result is a tabu list that "remembers" previous search moves and disallows them during a specified tenure period. When a tabu move completes its tenure, it is removed from the tabu list and becomes available for future moves.

## Example 10.3-1 (Minimization of a Single-Variable Function) ^tabuexamplea

---

This example details the application of TS to the minimization of the function $F\left( x\right)$ in Figure 10.1.

For iteration $k$ , let

	${x}_{k} =$ Current trial solution

	$N\left( {x}_{k}\right)  =$ Neighborhood of ${x}_{k}$

	${L}_{k} =$ Tabu list of inadmissible values of $x$ at iteration $k$

	$\tau  =$ Tabu tenure period expressed in number of successive iterations

	${x}^{ * } =$ Best solution encountered during the search

---

TABLE 10.5 TS Minimization of $F\left( x\right)$ in Figure 10.1 with Tabu Tenure Period $\tau  = 3$ and $N\left( {x}_{k}\right)  = \left\{  {{x}_{k} - 4,\ldots ,{x}_{k} - 1,{x}_{k} + 1,\ldots ,{x}_{k} + 4}\right\}   - {L}_{k}$ ^tabletabua

| Iteration $k$ | ${R}_{k}$ | ${x}_{k}$ | $F\left( {x}_{k}\right)$ | ${L}_{k}$ | $N\left( {x}_{k}\right)$ |
|---|---:|---:|---:|---|---|
| (Start) 0 | .0935 | 1 | 90 |  | $\{ 2,3,4,5\}$ |
| 1 | .4128 | 3 | 50 | $\{1\}$ | $\{ 2,4,5,6,7\}$ |
| 2 | .2039 | 4 | 80 | $\{ 1,3\}$ | $\{ 2,5,6,7,8\}$ |
| 3 | .0861 | 2 | 60 | $\{ 1,3,4\}$ | $\{ 5,6\}$ |
| 4 | .5839 | 5 | 100 | $\{ 3,4,2\}$ | $\{ 1,6,7,8\}$ |
| (End) 5 | .5712 | 7 | 20 | $\{ 4,2,5\}$ | $\{ 3,6,8\}$ |

Best heuristic solution: $x = 7, F\left( x\right)  = {20}$ , at iteration 5 (also happens to be the optimum).

In terms of the function $F\left( x\right)$ in Figure 10.1, the feasible values of $x$ are $1,2,\ldots$ , and 8. At iteration $k$ , the neighborhood set of ${x}_{k}$ can be defined as $N\left( {x}_{k}\right)  = \left\{  {{x}_{k} - q,\ldots ,{x}_{k} - 1}\right.$ , $\left. {{x}_{k} + 1,\ldots ,{x}_{k} + q}\right\}   - {L}_{k}$ , where $q$ is an integer constant. The definition implicitly excludes infeasible solution points. ${}^{3}$ For example, for the case where ${x}_{k} = 3, q = 4$ , and ${L}_{k} = \{ 6\} , N\left( {x}_{k}\right)  = \{  - \mathbb{1},\varnothing ,1,2,4,5,6,7\}  - \{ 6\}  = \{ 1,2,4,5,7\}$ . The crossed-out elements are infeasible.

As explained in Section 10.2, the next search move ${x}_{k + 1}$ can be selected as the best among all the solutions in $N\left( {x}_{k}\right)$ , or as a random element of $N\left( {x}_{k}\right)$ (random-walk selection). This example uses random selection.

Table 10.5 provides 5 iterations of the TS algorithm. The search starts at ${x}_{0} = 1$ (selected randomly from $\{ 1,2,\ldots ,8\}$ using $R = {.0935}$ ). Define the neighborhood using $q = 4$ and assume a fixed tenure period $\tau  = 3$ iterations (the tenure period can be random as Problem 10-11 demonstrates).

To illustrate the computations, $N\left( {{x}_{0} = 1}\right)  = \{ 2,3,4,5\}$ . At iteration $1,{L}_{1} = \{ 1\}$ and ${R}_{1} = {.4128}$ selects ${x}_{1} = 3$ from $N\left( {x}_{0}\right)$ , which yields $N\left( {x}_{1}\right)  = \{ 1,2,4,5,6,7\}  - \{ 1\}  = \; \{ 2,4,5,6,7\}$ and updates the tabu list at iteration 2 to ${L}_{2} = \{ 1,3\}$ .

An element is dropped from the tabu list on first-in-first-out basis after a tenure period of $\tau  = 3$ successive iterations. For example, element $\{ 1\}$ stays on the tabu list during iterations 1,2, and 3 until it is dropped at iteration 4.

## Example 10.3-2 (Job Sequencing) ^tabuexampleb

Consider the case of sequencing $n$ jobs on a single machine. The processing time for job $j$ is ${t}_{j}$ and its due date is ${d}_{j}$ (measured from zero). Completing job $j$ ahead of its due date incurs a holding (storage) cost ${h}_{j}$ per unit time. A tardy job $j$ results in a penalty cost ${p}_{j}$ per unit time. Table 10.6 provides the data for a 4-job problem.

Define

${j}_{ik} =$ Job $j$ occupies sequence position $i$ during iteration $k$

$$
{s}_{k} = \text{ Job sequence used in iteration }k
$$

$$
N\left( {s}_{k}\right)  = \text{ Neighborhood sequences of }{s}_{k}
$$

---

${}^{3}$ Actually, a tabu element can define a next search move if it satisfies the so-called Aspiration Level Criterion, as will be explained following Example 10.3-2.

---

TABLE 10.6 Data of the Job Sequencing Problem for Example 10.3-2 ^tablejobsdataa

| Job, $j$ | Processing time in days, ${T}_{j}$ | Due date, ${d}_{j}$ | Holding cost, ${h}_{j}$ (\$/day) | Penalty cost, ${p}_{i}$ (\$/day) |
|---:|---:|---:|---:|---:|
| 1 | 10 | 15 | 3 | 10 |
| 2 | 8 | 20 | 2 | 22 |
| 3 | 6 | 10 | 5 | 10 |
| 4 | 7 | 30 | 4 | 8 |

${L}_{k} =$ Tabu list at iteration $k$

$\tau  =$ Tenure period expressed in number of successive iterations

${z}_{k} =$ Total cost (holding + penalty) of sequence ${s}_{k}$

${s}^{ * } =$ Best sequence available during the search

${z}^{ * } =$ Total cost associated with ${s}^{ * }$

Possible options for determining the neighborhood, $N\left( {s}_{k}\right)$ , from ${s}_{k}$ include:

1. Exchange the positions of successive pairs of jobs.

2. Exchange the positions of pairs comprised of every other job.

3. Exchange the position of a job with another selected randomly from the remaining jobs.

The first definition is used in this example. To demonstrate its use, consider ${s}_{0} =$ (1-2-3-4). The neighborhood set is $N\left( {s}_{0}\right)  = \{$ (2-1-3-4),(1-3-2-4),(1-2-4-3) $\}$ , which corresponds to swapping the positions (in ${s}_{0}$ ) of jobs 1 and 2, jobs 2 and 3, and jobs 3 and 4, respectively. The selection of the next move ${s}_{1}$ from $N\left( {s}_{0}\right)$ can be made either randomly or based on the least-cost criterion. This example employs random selection.

Table 10.7 summarizes 5 iterations assuming a tenure period $\tau  = 2$ iterations. The sequence (3-1-2-4) in iteration 2 provides the best solution with ${z}^{ * } = {126}$ . To demonstrate cost computations in the table, the value of $z$ for the sequence ${s}_{2} =$ (3-1-2-4) of iteration 2 is determined in the following order: ${}^{4}$ ^tablecostcalc

|  | 3 | 1 | 2 | 4 |
|---|---:|---:|---:|---:|
| Processing time | 6 | 10 | 8 | 7 |
| Due date | 10 | 15 | 20 | 30 |
| Completion date | 6 | 16 | 24 | 31 |
| Holding time | 4 | 0 | 0 | 0 |
| Delay time | 0 | 1 | 4 | 1 |
| Holding cost | 20 | 0 | 0 | 0 |
| Late penalty cost | 0 | 10 | 88 | 8 |

Thus, $z =$ Holding cost + Penalty cost $= {20} + \left( {{10} + {88} + 8}\right)  = \$ {126}$ .

The heuristic operates in the following manner: At iteration $1, R = {.5124}$ selects the sequence ${s}_{1} = \left( {1 - 3 - 2 - 4}\right)$ randomly from $N\left( {s}_{0}\right)$ . The associated tabu list becomes ${L}_{1} = \{ 3 - 2\}$ , which means that the positions of jobs 2 and 3 cannot be swapped during the tenure period (i.e., during two successive iterations). This is the reason the sequence (1-2-3-4) in $N\left( {s}_{1}\right)$ is excluded. The same reasoning applies to the crossed-out sequences in subsequent iterations. Note that the calculations in Table 10.7 apply $R$ to admissible (uncrossed-out) neighborhood elements only.

---

${}^{4}$ For convenience, cost calculations are automated using the spreadsheet excelJobSequencing.xls for situations involving four and five jobs. You can modify the spreadsheet to account for other situations.

---

TABLE 10.7 TS Applied to the Job Sequencing Problem with Tenure Period $\tau  = 2$ Iterations ^tabletabujobs

| Iteration, $k$ | Sequence, ${s}_{k}$ | Total cost (holding) + (penalty)                                                                              | ${z}^{ * }$ | Tabu list, $L\left( {s}_{k}\right)$ |   $R$ | Neighborhood, $N{\left( {s}_{k}\right) }^{ * }$ |
| -------------- | ------------------- | ------------------------------------------------------------------------------------------------------------- | ----------: | ----------------------------------- | ----: | ----------------------------------------------- |
| (Start) 0      | (1-2-3-4)           | $\left( {5 \times  3 + 2 \times  2}\right)  + \left( {{14} \times  {10} + 1 \times  8}\right)  = {167}$       |         167 |                                     | .5124 | (2-1-3-4) (1-3-2-4)✓ (1-2-4-3)                  |
| 1              | (1-3-2-4)           | $\left( {5 \times  3}\right)  + \left( {6 \times  {10} + 4 \times  {22} + 1 \times  8}\right)  = {171}$       |             | $\{3-2\}$                           | .3241 | (3-1-2-4)✓ (1-2-3-4) (1-3-4-2)                  |
| 2              | (3-1-2-4)           | $\left( {4 \times  5}\right)  + \left( {1 \times  {10} + 4 \times  {22} + 1 \times  8}\right)  = {126}$       |         126 | $\{3-2, 3-1\}$                      | .2952 | (1-3-2-4) (3-2-1-4)✓ (3-1-4-2)                  |
| 3              | (3-2-1-4)           | $\left( {4 \times  5 + 6 \times  2}\right)  + \left( {9 \times  {10} + 1 \times  8}\right)  = {130}$          |             | $\{3-1, 2-1\}$                      | .4241 | (2-3-1-4)✓ (3-1-2-4) (3-2-4-1)                  |
| 4              | (2-3-1-4)           | $\left( {{12} \times  2}\right)  + \left( {4 \times  {10} + 9 \times  {10} + 1 \times  8}\right)  = {162}$    |             | $\{2-1, 2-3\}$                      | .8912 | (3-2-1-4) (2-1-3-4) (2-3-4-1)✓                  |
| (End) 5        | (2-3-4-1)           | $\left( {{12} \times  2 + 9 \times  4}\right)  + \left( {4 \times  {10} + {16} \times  {10}}\right)  = {260}$ |             | $\{2-3, 4-1\}$                      | .0992 | (3-2-4-1)✓ (2-4-3-1) (2-3-1-4)                  |

Best search sequence: (3-1-2-4) with cost $= {126}$ at iteration 2.

*Check mark $\checkmark$ designates the non-tabu element selected randomly from $N\left( {s}_{k}\right)$ using $R$ .

"Fine-Tuning" TS. The following refinements can prove effective in improving the quality of the final solution: ^tabufinetune

1. Aspiration Criterion. The design of TS search disallows moves that are on the tabu list. An exception occurs when a disallowed move leads to an improved solution. For example, in Table 10.7 (Example 10.3-2 ), the crossed-out tabu sequences in iterations 1, 2, 3, and 4 should be examined for the possibility of producing better search moves. If they do, they should be accepted as search moves.

2. Intensification and Diversification. Two additional strategies, called intensification and diversification, are usually applied when a string of successive iterations fails to produce improvement. Intensification calls for a more thorough examination of nearby solution points and diversification attempts to move the search to unexplored solution regions. One way to implement these strategies is by controlling the size of the tabu list. A shorter tabu list increases the size of the allowable neighborhood set and hence intensifies the search to points that lie close to the best solution. A longer tabu list does the opposite in that it permits escape from a local optimum point by allowing the exploration of "remote" regions.

## Summary of Tabu Search Algorithm ^tabusummary

Step 0: Select a starting solution ${s}_{0} \in  S$ . Initialize the tabu list ${L}_{0} = \varnothing$ , and choose a schedule for specifying the size of the tabu list. Set $k = 0$ .

Step 1: Determine the feasible neighborhood $N\left( {s}_{k}\right)$ that excludes (inferior) members of the tabu list ${L}_{k}$ .

Step 2: Select the next move ${s}_{k + 1}$ from $N\left( {s}_{k}\right)$ (or from ${L}_{k}$ if it provides a better solution), and update the tabu list ${L}_{k + 1}$ .

Step 3: If a termination condition is reached, stop. Otherwise, set $k = k + 1$ and go to step 1.

#### 10.3.2 Simulated Annealing Algorithm ^sasection

Simulated annealing (SA) escapes entrapment at a local optimum by using a probability condition that accepts or rejects an inferior move (a no-worse move is always accepted). The idea of determining the acceptance probability of the next search move is explained in the following manner: Suppose the optimization problem is given as

$$
\text{ Maximize or minimize }z = F\left( s\right) ,{s\varepsilon S}
$$

As the number of iterations increases, SA seeks a more selective determination of solution strategies by using an adjustable parameter $T$ , called temperature, that is made progressively smaller according to a temperature schedule. ${}^{5}$ Typically, a schedule of $I$ elements for $T$ is defined as $\left\{  {T = {T}_{i}, i = 0,1,\ldots , I}\right\}$ . Each ${T}_{i}$ applies for a specified number of consecutive accept-iterations, $t \cdot  {}^{6}$ Given ${s}_{0}$ is the starting strategy of the search, ${T}_{i}$ is typically computed as ^satemperature

$$
{T}_{0} = {r}_{0}F\left( {s}_{0}\right) ,0 < {r}_{0} < 1
$$

$$
{T}_{i} = {r}_{i}{T}_{i - 1},0 < {r}_{i} < 1, i = 1,2,\ldots , I
$$

Define ${s}_{a}$ as the last accepted solution strategy. At iteration $k$ , the probability of accepting a neighborhood strategy as the next search move, ${s}_{k + 1}$ , is computed as ^saaccept

$$
P\left\{  {\text{ accept }{s}_{k + 1} \mid  {s}_{k + 1} \in  N\left( {s}_{k}\right) }\right\}   = \left\{  \begin{array}{l} 1,\text{ if }F\left( {s}_{k + 1}\right) \text{ is not worse than } \\  {e}^{\frac{-\left| {F\left( {s}_{a}\right)  - F\left( {s}_{k + 1}\right) }\right| }{T}},\text{ if otherwise } \end{array}\right.
$$

The formula says that the next search move, ${s}_{k + 1}$ , is accepted if $F\left( {s}_{k + 1}\right)$ is not worse than $F\left( {s}_{a}\right)$ . Otherwise, $F\left( {s}_{k + 1}\right)$ is an inferior solution, and ${s}_{k + 1}$ is accepted only if ${R}_{k} \leq  {e}^{\frac{-\left| {F\left( {s}_{a}\right)  - F\left( {s}_{k + 1}\right) }\right| }{T}}$ , where ${R}_{k}$ is a $\left( {0,1}\right)$ random number. If ${s}_{k + 1}$ is rejected, a different solution strategy, chosen from $N\left( {s}_{a}\right)$ , is attempted. Notice that the temperature schedule decreases the probability of acceptance as the number of iterations increases by making ${T}_{i}$ progressively smaller.

---

${}^{5}\mathrm{{SA}}$ is inspired by the annealing process in metallurgy, which involves heating and controlled cooling of a material, hence the use of the term temperature. The use of metallurgical jargon in the description of SA is purely traditional, with no technical bearing on the development of the heuristic, save the general idea imbedded in the annealing process.

${}^{6}$ Basing change in temperature on the number of accept-iterations is an arbitrary rule and can be replaced by others, such as making the change based on the total number of intervening (accept or reject) iterations.

---

TABLE 10.8 Minimization of $F\left( x\right)$ in Figure 10.1 Using SA Heuristic with Schedule ${T}_{0} = {.5F}\left( {x}_{0}\right) ,{T}_{i} = {.5}{T}_{i - 1}$ , $i = 1,2,3,\ldots$ and $t = 3$ Accept-Iterations ^tablesaexample

| Iteration $k$ | ${R}_{1k}$ | ${x}_{k}$ | $F\left( {x}_{k}\right)$ | $a$ | $T$ | $\Delta  = \left| {\text{ Change in }F}\right|$ | ${e}^{-\Delta /T}$ | ${R}_{2k}$ | Decision | $N\left( {x}_{k}\right)$ |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---|
| (Start) 0 |  | 1 | 90 | 0 | 45.0 |  |  |  |  | $\{ 2,3,4,5,6,7,8\}$ |
| 1 | 0.4128 | 4 | 80 | 1 | 45.0 |  |  |  | Accept: $F\left( {x}_{1}\right)  < F\left( {x}_{0}\right)$ | $\{ 1,2,3,5,6,7,8\}$ |
| 2 | 0.2039 | 2 | 60 | 2 | 45.0 |  |  |  | Accept: $F\left( {x}_{2}\right)  < F\left( {x}_{1}\right)$ | $\{ 1,3,4,5,6,7,8\}$ |
| 3 | 0.0861 | 1 | 90 | 2 | 45.0 | $\left| {{60} - {90}}\right|  = {30}$ | .5134 | .5462 | Reject: ${R}_{2k} > {e}^{-\Delta /T}$ | Same as $N\left( {x}_{2}\right)$ |
| 4 | 0.5839 | 6 | 40 |  | 45.0 |  |  |  | Accept: $F\left( {x}_{4}\right)  < F\left( {x}_{2}\right)$ | $\{ 1,2,3,4,5,7,8\}$ |
| (End) 5 | 0.5712 | 5 | 100 |  | 22.5 | $\left| {{40} - {100}}\right|  = {60}$ | .0695 | .0197 | Accept: ${R}_{2k} < {e}^{-\Delta /T}$ | $\{ 1,2,3,4,6,7,8\}$ |

Search best solution: $x = 6$ with $F\left( 6\right)  = {40}$ .

## Example 10.3-3 (Minimization of a Single-Variable Function) ^saexamplea

This example applies SA to find the minimum of the single-variable function in Figure 10.1.

Table 10.8 provides five iterations. The solution arbitrarily defines the neighborhood at any iteration $k$ as $N\left( {x}_{k}\right)  = \{ 1,2,\ldots ,8\}  - \left\{  {x}_{a}\right\}$ , where ${x}_{a}$ is the solution associated with the most recent accept-iteration.

To illustrate the computations, the search arbitrarily selects ${x}_{0} = 1$ with $t = 3$ accept-iterations and sets ${r}_{i} = {.5}$ for all $i \geq  0$ . Thus, $N\left( {x}_{0}\right)  = \{ 2,3,4,5,6,7,8\} , F\left( 1\right)  = {90}$ , and ${T}_{0} = {.5F}\left( 1\right)  = {45}$ . For $k = 1$ , the random number ${R}_{11} = {.4128}$ selects the (possible) next-solution point ${x}_{1} = 4$ from $N\left( {x}_{0}\right)$ with $F\left( 4\right)  = {80}$ . Because $F\left( {x}_{1}\right)$ is better than $F\left( {x}_{0}\right)$ , we accept the move. At iteration 2, we set $a = 1$ with $F\left( {x}_{a}\right)  = {80}$ . The next move ${x}_{2} = 2$ is selected from $N\left( {x}_{1}\right)  = \{ 1,2,3,5,6,7,8\}$ using ${R}_{12} = {.2039}$ . The move is again accepted because it improves the solution from $F\left( {x}_{1}\right)  = {80}$ to $F\left( {x}_{2}\right)  = {60}$ . This sets $a = 2$ with $F\left( {x}_{a}\right)  = {60}$ . At iteration $3,{R}_{13} = {.0861}$ selects ${x}_{3} = 1$ from $N\left( {x}_{2}\right)  = \{ 1,3,4,5,6,7,8\}$ with $F\left( {x}_{3}\right)  = {90}$ . The new solution is inferior to $F\left( {x}_{a}\right)  = {60}$ . Thus, $\Delta  = \left| {{60} - {90}}\right|  = {30}$ , and ${e}^{-\Delta /T} = {.5134}$ . Given ${R}_{23} = {.5462}$ , the solution ${x}_{3} = 1$ is rejected, which requires re-sampling from the last accept-neighborhood $N\left( {x}_{2}\right)$ . At iteration $4,{x}_{4} = 6$ is accepted because it yields an improved solution (relative to that of iteration 2). At this point, the condition $t = 3$ is satisfied, which changes the temperature to ${T}_{1} = {.5},{T}_{0} = {22.5}$ at the next iteration. At iteration 5, given ${x}_{5} = 5,{R}_{25}\left( { = {.0197}}\right)  < {e}^{-\Delta /\mathrm{T}}\left( { = {.0695}}\right)$ accepts the move even though it is an inferior solution $\left\lbrack  {F\left( 5\right)  = {100}}\right\rbrack$ .

## Example 10.3-4 (Job Sequencing) ^saexampleb

---

This problem is solved in Example 10.3-2 using TS. The problem statement is repeated here for

convenience. Jobs are sequenced on a single machine. Each job $j$ has a processing time ${t}_{j}$ and a

due date ${d}_{j}$ . If $j$ is completed earlier than its due date, a holding cost ${h}_{j}$ per unit time is incurred.

A tardy job $j$ results in a penalty cost ${p}_{j}$ per unit time. Table 10.9 provides the data for a 4-job

scheduling problem.

	Define

	${s}_{k} =$ Job sequence used in iteration $k$

	$N\left( {s}_{k}\right)  =$ Neighborhood sequences of ${s}_{k}$

	${T}_{i} =$ Temperature schedule, $i = {12}\ldots , I$

	${c}_{k} =$ Total cost (holding + penalty) of sequence ${s}_{k}$

---

TABLE 10.9 Data for the Job Sequencing Problem of Example 10.3-4 ^tablejobsdatab

| Job, $j$ | Processing time in days, ${D}_{j}$ | Due date, ${d}_{j}$ | Holding cost, ${h}_{j}$ (\$/day) | Penalty cost, ${p}_{i}$ (\$/day) |
|---:|---:|---:|---:|---:|
| 1 | 10 | 15 | 3 | 10 |
| 2 | 8 | 20 | 2 | 22 |
| 3 | 6 | 10 | 5 | 10 |
| 4 | 7 | 30 | 4 | 8 |

Table 10.10 provides five SA iterations. Iteration 3 gives the best sequence. Note that when a sequence is rejected at iteration $k$ , we reuse the neighborhood of the last accept-iteration to randomly select the sequence for iteration $k + 1$ . This occurs at iteration 2, where the neighborhood remains the same as at iteration 1 . Note also that the $t = 3$ is satisfied at iteration 4, causing temperature change from 83.5 to 41.75 at iteration 5.

## Summary of Simulated Annealing Algorithm ^sasummary

Step 0: Select a starting solution ${s}_{0}{\varepsilon S}$ . Set $k = 0, p = 0$ , and $i = 0$ .

Step 1: Generate the neighborhood $N\left( {s}_{k}\right)$ , and set temperature $T = {T}_{i}$ .

Step 2: Determine the solution ${s}_{k + 1}$ randomly from $N\left( {s}_{k}\right)$ . If ${s}_{k + 1}$ is not worse than the last accepted solution or if $R < P\left\{  \right.$ accept $\left. {s}_{k + 1}\right\}$ , then accept ${s}_{k + 1}$ , set $p = p + 1$ , and go to step 3. Else, reject ${s}_{k + 1}$ , and set $N\left( {s}_{k + 1}\right)  = N\left( {s}_{k}\right)$ . Set $k = k + 1$ , and go to step 1 .

Step 3: If a termination condition is reached, stop. Otherwise, set $k = k + 1$ . If $p = t$ , then set $i = i + 1$ . Go to step 1 .

TABLE 10.10 SA Applied to the Job Sequencing Problem with Schedule ${T}_{0} = {.5}{c}_{0},{T}_{i} = {.5}{T}_{i - 1}$ , $i = 1,2,3,\ldots$ and $t = 3$ Accept-Iterations ^tablesajobs

| Iteration $k$ | Sequence ${s}_{k}$ | Total cost ${c}_{k} =$ (holding) + (penalty) | ${T}_{k}$ | $z = \frac{\left| \text{ Change in cost }\right| }{{T}_{k}}$ | ${e}^{-z}$ | ${R}_{1k}$ | Decision | ${R}_{2k}$ | Neighborhood, $N{\left( {s}_{k}\right) }^{ * }$ |
|---|---|---|---:|---:|---:|---:|---|---:|---|
| (Start) 0 | (1-2-3-4) | $\left( {5 \times  3 + 2 \times  2}\right)  + ({14} \times  {10} \; + 1 \times  8) = {167}$ | 83.5 |  |  |  |  | .5462 | (2-1-3-4) (1-3-2-4)✓ (1-2-4-3) |
| 1 | (1-3-2-4) | $\left( {5 \times  3}\right)  + (6 \times  {10} + 4 \; \times  {22} + 1 \times  8) = {171}$ | 83.5 | .0479 | .9532 | .5683 | Accept: ${R}_{11} < {e}^{-z}$ | .7431 | (3-1-2-4) (1-2-3-4) (1-3-4-2)✓ |
| 2 | (1-3-4-2) | $\left( {5 \times  3 + 7 \times  4}\right)  + (6 \times  {10} \; + {11} \times  {22}) = {345}$ | 83.5 | 2.083 | .1244 | .3459 | Reject: ${R}_{12} > {e}^{-z}$ | .1932 | (3-1-2-4)✓ (1-2-3-4) (1-3-4-2) |
| 3 | (3-1-2-4) | $\left( {4 \times  5}\right)  + (1 \times  {10} + 4 \; \times  {22} + 1 \times  8) = {126}$ | 83.5 |  |  |  | Accept: ${c}_{3} < {c}_{1}$ | .6125 | (1-3-2-4) (3-2-1-4)✓ (3-1-4-2) |
| 4 | (3-2-1-4) | $\left( {4 \times  5 + 6 \times  3}\right)  + (9 \times  {10} \; + 1 \times  8) = {130}$ | 83.5 | .0479 | .9532 | .6412 | Accept: ${R}_{14} < {e}^{-z}$ | .2234 | (2-3-1-4)✓ (3-1-2-4) (3-2-4-1) |
| (End) 5 | (2-3-1-4) | $\left( {{12} \times  2}\right)  + (4 \times  {10} + 9 \; \times  {10} + 1 \times  8) = {162}$ | 41.75 | .766 | .4647 | .5347 | Reject: ${R}_{15} > {e}^{-z}$ | .8127 | (2-3-1-4) (3-1-2-4) (3-2-4-1)✓ |

Best search solution: (3-1-2-4) with cost 126 at iteration 3.

*Check mark $\checkmark$ indicates the sequence selected using random number ${R}_{2k}$ .

#### 10.3.3 Genetic Algorithm ^gasection

The genetic algorithm (GA) mimics the biological evolution process of "survival of the fittest." Each feasible solution of a problem is regarded as a chromosome encoded by a set of genes. The most common gene codes are binary $\left( {0,1}\right)$ and numeric $\left( {0,1,2,\ldots }\right)$ . For example, the chromosomes of a single variable whose feasible values are $0,1,\ldots$ , and 8 can be represented by the binary codes $\left( {{0000},{1000},{0100},{1100},{0010},{1010},{0110},{1110},}\right)$ and 0001). The chromosomes for a two-variable problem $\left( {{x}_{1},{x}_{2}}\right)$ with ${x}_{1} = \{ 0,1\}$ and ${x}_{2} = \{ 0,1,2,3\}$ can be represented by the numeric codes $\left( {0,0}\right) ,\left( {0,1}\right) ,\left( {0,2}\right) ,\left( {0,3}\right) ,\left( {1,0}\right)$ , $\left( {1,1}\right) ,\left( {1,2}\right)$ , and $\left( {1,3}\right)$ . The multivariable numeric codes may also be represented as binary codes. For example, the binary code of $\left( {{x}_{1},{x}_{2}}\right)  = \left( {0,3}\right)$ is $\left( {{000},{110}}\right)$ . There are other coding schemes, including node code for network models (see Beasley and Associates, 1993, Part 2). ^gageneral

A set of $N$ feasible solutions is referred to as a population with $N$ chromosomes. The fitness of a chromosome is measured in terms of an appropriate objective function. A more fit chromosome yields a better value of the objective function.

The overall idea of GA is to select two parents from a population. The genes of the two parents are then crossed over and (possibly) mutated (as will be explained in Example 10.3-5) to produce two children. The offspring replace the two weakest (least-fit) chromosomes in the population, and the process of selecting new parents is repeated.

The actual implementation of GA requires additional problem-specific details. Also, the rules for selecting parents and creating children may vary. For example, the parents may be selected totally randomly from a population, or they may consist of the two fittest chromosomes. Some of these details will be provided later.

## Example 10.3-5 (Minimization of a Single-Variable Function) ^gaexamplea

The GA is applied to the single-variable discrete problem in Figure 10.1 with the feasible domain $X = \{ 1,2,3,4,5,6,7,8\}$ . We will arbitrarily specify a population of size $N = 4$ parents whose chromosomes are determined from $X$ using uniform random sampling.

The random number $R$ is applied to the uniform distribution in Table 10.11 to generate the four members $\left( {N = 4}\right)$ of the initial population and their fitness, as shown in Table 10.12. The solution for $i = 4$ is a repeat of the solution for $i = 3\left( {{x}_{3} = {x}_{4}}\right)$ , hence the solution for $i = 4$ is discarded. The initial population is ${X}_{0} = \{ 8,3,5,1\}$ , and the associated best solution is ${x}^{ * } = 3$ with $F\left( {x}^{ * }\right)  = {50}$ .

Two parents can be selected from the initial population ${X}_{0} = \{ 8,3,5,1\}$ in a number of ways: (1) Select the two fittest members. (2) Select the fittest member and then a random one from the remaining members. (3) Select two parents randomly from ${X}_{0}$ . In this presentation, we use the third option. Specifically, the two random numbers ${R}_{1} = {.2869}$ and ${R}_{2} = {.0281}$ yield $x = 3$ with $F\left( 3\right)  = {50}$ and $x = 8$ with $F\left( 8\right)  = {70}$ .

The two children are created from the two selected parents by using genes crossover. There are several methods for implementing the crossover. ^gacrossover

TABLE 10.11 Uniform Random Sampling from the Domain $X = \{ x = 1,2,3,4,5,6,7,8\}$ ^tablesampling

| $x$ | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Cumulative probability, $P\left( x\right)$ | .125 | .250 | .375 | .500 | .625 | .750 | .875 | 1. |

TABLE 10.12 Generation of the Starting Population with $N = 4$ ^tablepopulation

| $i$ | ${R}_{i}$ | ${x}_{i}$ | Binary-coded ${x}_{i}$ | $F\left( {x}_{i}\right)$ |
|---:|---:|---:|---|---:|
| 1 | .3025 | 3 | 1100 | 50 |
| 2 | .9842 | 8 | 0001 | 70 |
| 3 | .5839 | 5 | 1010 | 100 |
| 4 | .5712 | 5 | Discard |  |
| 5 | .0926 | 1 | 1000 | 90 |

1. Uniform crossover. In this rule, parents' common genes apply to both children. The remaining genes for one child are determined randomly, with the other child getting the complement gene.

2. One-point crossover. The genes of parents P1 and P2 are split randomly at the same point and then swapped; that is, $\mathrm{P}1 = \left( {\mathrm{P}{11},\underline{\mathrm{P}{12}}}\right)$ and $\mathrm{P}2 = \left( {\mathrm{P}{21},\mathbf{P}{22}}\right)$ yield the children chromosomes as $\mathrm{C}1 = \{ \mathrm{P}{11},\mathbf{P}{22}\}$ and $\mathrm{C}2 = \{ \mathrm{P}{21},\underline{\mathrm{P}{12}}\}$ .

3. Multipoint crossover. This rule extends the one-point crossover to multiple random points. For example, in a 2-point crossover, $\mathrm{P}1 = \left( {\mathrm{P}{11},\mathrm{\;P}{12},\mathrm{\;P}{13}}\right)$ and $\mathrm{P}2 = \left( {\mathrm{P}{21},\mathrm{\;P}{22},\mathrm{\;P}{23}}\right)$ yield $\mathrm{C}1 = \left( {\mathrm{P}{11},\mathbf{P}{22},\mathrm{\;P}{13}}\right)$ and $\mathrm{C}2 = \left( {\mathrm{P}{21},\underline{\mathrm{P}{12}},\mathrm{P}{23}}\right)$ .

This example uses the uniform crossover rule. The one-point crossover rule will be used in Example 10.3-6.

For the two parents $\left( {{x}_{1} = 3,{x}_{2} = 8}\right)$ generated in Table 10.12, we have

$$
\text{ P1 } = \left( {{11}\underline{0}0}\right)
$$

$$
\text{ P2 } = \left( {{00}\underline{0}1}\right)
$$

In uniform crossover, the common (underlined) third gene in P1 and P2 carries over to both children. The remaining three genes are determined randomly as follows: For child 1, the gene is 1 if $0 \leq  R < {.5}$ and 0 if ${.5} \leq  R \leq  1$ . The corresponding genes for child 2 are the complements of those assigned to child 1. For example, the three random numbers .2307, .7346, and .6220 show that genes 1, 2, and 4 for child 1 are 1, 0 , and 0 , respectively, which automatically assigns the complement genes 0,1 , and 1 to child 2 . Thus

$$
\mathrm{C}1 = \left( \begin{array}{llll} 1 & 0 & 0 & 0 \end{array}\right) \left( {\text{ or }x = 1}\right)
$$

$$
\mathrm{C}2 = \left( \begin{array}{llll} 0 & 1 & 0 & 1 \end{array}\right) \left( {\text{ or }x = {10}}\right)
$$

Child 2 corresponds to an infeasible solution (recall that the feasible range is $x = 1,2,\ldots ,8$ ). However, before discarding a child infeasible solution, we first apply random mutation (replacing one gene with another) and then check the mutated offspring for feasibility. If infeasibility persists, totally new offspring must be created (from the same parents). The process can be repeated as necessary until feasibility is achieved. ^gamutation

The probability of mutation is usually about .1, meaning a gene is mutated if $0 \leq  R < {.1}$ . For child 1, the random number sequence .6901, .7698, .0871, .9534 shows that the third gene only is mutated from 0 to 1, yielding $\mathrm{C}1 = \left( \begin{array}{llll} 1 & 0 & 1 & 0 \end{array}\right)$ [or $x = 5$ with $\left. {F\left( 5\right)  = {100}}\right\rbrack$ . For Child 2, the sequence.5954,.2632,.6731,.0983mutates gene 4 and yields $\mathrm{C}2 = \left( \begin{array}{llll} 0 & 1 & 0 & \mathbf{0} \end{array}\right)$ [or $x = 2$ with $F\left( 2\right)  = {60}\rbrack$ . Both child chromosomes are feasible, but neither yields a better solution. Hence, the solution ${x}^{ * } = 3$ of the initial population continues to be the best so far.

The least-fit parents in ${X}_{0}\left( {x = 5\text{ and }x = 1}\right)$ are now replaced with the two offspring solutions $\left( {x = 5\text{ and }x = 2}\right)$ . This, in effect, says that the next population is ${X}_{1} = \left( {8,3,5,2}\right)$ . We now use ${X}_{1}$ to start a new iteration.

Dealing with continuous variables. The genetic coding in Example 10.3-5 assumes that the variable $x$ is integer. The coding can be modified to include continuous variables in the following manner: Specify a finite (preferably tight) feasible range of the form $l \leq  x \leq  u$ , where $l$ and $u$ are constants. Let $v$ represent the numeric value of a binary string $s$ of length $n$ bits. The string $s$ is then translated to a real (continuous) value by using ^gacontinuous

$$
x = l + \left( {u - l}\right) \left( \frac{v}{{2}^{n} - 1}\right)
$$

The logic of the formula is that the maximum value of an $n$ -bit binary string is ${2}^{0} + {2}^{1} + {2}^{2} + \cdots  + {2}^{n - 1} = {2}^{n} - 1$ , and $\left( \frac{v}{{2}^{n} - 1}\right)$ is the proportion of the quantity $\left( {u - l}\right)$ , which when added to the lower bound $l$ will produce the corresponding value of $x$ in the range $\left( {l, u}\right)$ . For example, given $- 1 \leq  x \leq  3$ and arbitrarily choosing $n = 5$ , the binary string $\left( \begin{array}{lllll} 0 & 0 & 1 & 0 & 1 \end{array}\right)$ has $v = {2}^{2} + {2}^{4} = {20}$ , and the associated value of $x$ is

$$
x =  - 1 + \left\lbrack  {3 - \left( {-1}\right) }\right\rbrack  \left( \frac{20}{{2}^{5} - 1}\right)  = {1.580645}
$$

The design of the code indicates that larger values of $n$ yield better accuracy.

The $n$ -bit strings representing $v$ are used in the same manner as given in Example 10.3-5. This means that children are created through crossover and mutation of the parents' genes. Indeed, a multivariable situation is handled in a similar manner with each variable represented by an independent $n$ -bit string.

## Example 10.3-6 (Job Sequencing) ^gaexampleb

This problem was solved in Example 10.3-2 using TS and in Example 10.3-4 using SA. We repeat the problem statement here for convenience (a fifth job is added to render the example more viable). Jobs are sequenced on a single machine. Each job $j$ has a processing time ${t}_{j}$ and a due date ${d}_{j}$ . If job $j$ is completed earlier than its due date, a holding cost ${h}_{j}$ per unit time is incurred. A tardy job $j$ results in a penalty cost ${p}_{j}$ per unit time. Table 10.13 provides the data for a 5-job scheduling problem.

Define

${s}_{k} =$ Job sequence used in iteration $k$

$N\left( {s}_{k}\right)  =$ Neighborhood sequences of ${s}_{k}$

${z}_{k} =$ Total cost (holding + penalty) of sequence ${s}_{k}$

TABLE 10.13 Data for a Single-Machine 5-Job Sequencing Problem ^tablejobsdatac

| Job, $j$ | Processing time in days, ${T}_{i}$ | Due date, ${d}_{j}$ | Holding cost, ${h}_{j}\left( {\$ /\text{ day }}\right)$ | Penalty cost, ${p}_{j}\left( {\$ /\text{ day }}\right)$ |
|---:|---:|---:|---:|---:|
| 1 | 10 | 15 | 3 | 10 |
| 2 | 8 | 20 | 2 | 22 |
| 3 | 6 | 10 | 5 | 10 |
| 4 | 7 | 30 | 4 | 8 |
| 5 | 4 | 12 | 6 | 15 |

${s}^{ * } =$ Best sequence available during the search

${z}^{ * } =$ Total cost associated with ${s}^{ * }$

The first task is to develop the genetic code of the chromosomes. Although binary coding can be used in the job sequencing problem (see, e.g., Yamada and Nakano, 1997), the resulting algorithm is complex because the crossover and mutation operations may result in infeasible schedules that must be "repaired." Thus, instead of using a binary code, the nature of the problem allows representing a chromosome as a job sequence (e.g., 1-2-5-3-4).

To show how children are created, consider parents chromosomes $\mathrm{P}1 = 1 - 3 - 5 - 2 - 4$ and P2 = 5-4-2-3-1. Suppose that a random 1-point crossover occurs at gene 3. The first two genes of C1(C2) are constructed by swapping the first two genes of P1(P2). The last three genes are the ones remaining from P1(P2) after excluding the first two genes - that is, ^gajobencoding

First 2 genes of $\mathrm{C}1 = \{ 5,4\}$

First 2 genes of $\mathrm{C}2 = \{ 1,3\}$

Last 3 genes of $\mathrm{C}1 = \{ 1,3,5,2,4\}  - \{ 5,4\}  = \{ 1,3,2\}$

Last 3 genes of C2 $= \{ 5,4,2,3,1\}  - \{ 1,3\}  = \{ 5,4,2\}$

Thus, C1 = 5-4-1-3-2 and C2 = 1-3-5-4-2.

Next, mutations of C1 and C2 are carried out in the following manner: If random number $R < {.1}$ , a child chromosome is subject to mutation. Mutation is then implemented for the child by swapping two randomly selected genes (jobs). For example, the random numbers $R = {.8452}\left( { > {.1}}\right)$ and $R = {.0342}\left( { < {.1}}\right)$ applied to C1 and C2, respectively, indicate that only C2 is mutated. Using $R = {.1924}$ and $R = {.8239}$ to determine swapped genes in C2, the first random number selects position 1 (job 1), and the second random number selects position 5 (job 2). Thus, C2 is mutated from 1-3-5-4-2 to 2-3-5-4-1.

Table 10.14 summarizes the calculations for iterations 0 to 3. For convenience, the cost calculations (values of $z$ ) are automated using the spreadsheet excelJobSequencing.xls. The best sequence is associated with P4 in iteration 3.

## Summary of Genetic Algorithm ^gasummary

## Step 0:

(a) Generate a random population $X$ of $N$ feasible chromosomes.

(b) For each chromosome $s$ in the selected population, evaluate its associated fitness. Record ${s}^{ * }$ as the best solution so far available.

(c) Encode each chromosome using binary or numeric representation.

## Step 1:

(a) Select two parent chromosomes from population $X$ .

(b) Crossover the parents genes to create two children.

(c) Mutate the children genes randomly.

(d) If resulting solutions are infeasible, repeat step 1 until feasibility is achieved. Else, replace the weakest two parents with the new children to form a new population $X$ and update ${s}^{ * }$ . Go to step 2

Step 2: If a termination condition has been reached, stop; ${s}^{ * }$ is the best available solution. Else, repeat step 1.

TABLE 10.14 GA Iterations Applied to the Job Sequencing Problem of Example 10.3-6 ^tablegajobs

| Iteration | Chromosome | Sequence, $s$ | $z$ | Explanation |
|---:|---|---|---:|---|
| 0 | P1 | 1-2-3-4-5 | 512 | Initial random population (P1, P2, P3, P4). |
| 0 | P2 | 2-3-4-1-5 | 605 | Chosen parents are P4 (best $z$ ) and P3 (random). |
| 0 | P3 | 4-1-5-2-3 | 695 | Crossover P3 and P4 starting at position 3. |
| 0 | P4 | 3-2-1-4-5 | 475 |  |
| 0 | C1 | 3-2-4-1-5 | 573 | Mutate C1 by exchanging positions 2 and 5. |
| 0 | C2 | 4-1-3-2-5 | 829 | Mutate C2 by exchanging positions 1 and 5. |
| 0 | mC1 | 3-5-4-1-2 | 534 |  |
| 0 | mC2 | 5-1-3-2-4 | 367 |  |
| 1 | P1 | 1-2-3-4-5 | 512 | Worst parents P2 and P3 in iteration 0 are replaced |
| 1 | P2 | 3-5-4-1-2 | 534 | with their mC1 and mC2. |
| 1 | P3 | 5-1-3-2-4 | 367 | Chosen parents are P3 (best $z$ ) and P1 (random). |
| 1 | P4 | 3-2-1-4-5 | 475 | Crossover P1 and P3 starting at position 4. |
| 1 | C1 | 5-1-3-2-4 | 367 | Mutate C1 by exchanging positions 2 and 3. |
| 1 | C2 | 1-2-3-5-4 | 439 | Mutate C2 by exchanging positions 2 and 4. |
| 1 | mC1 | 5-3-1-2-4 | 314 |  |
| 1 | mC2 | 1-5-3-2-4 | 361 |  |
| 2 | P1 | 5-3-1-2-4 | 314 | Worst parents P1 and P2 in iteration 1 are replaced |
| 2 | P2 | 1-5-3-2-4 | 361 | with their mC1 and mC2. |
| 2 | P3 | 5-1-3-2-4 | 367 | Chosen parents are P1 (best $z$ ) and P4 (random). |
| 2 | P4 | 3-2-1-4-5 | 475 | Crossover P1 and P4 starting at position 3. |
| 2 | C1 | 3-2-5-1-4 | 292 | Mutate C1 by exchanging positions 1 and 2. |
| 2 | C2 | 5-3-2-1-4 | 222 | No mutation in C2. |
| 2 | mC1 | 2-3-5-1-4 | 324 |  |
| 2 | mC2 | 5-3-2-1-4 | 222 |  |
| 3 | P1 | 5-3-1-2-4 | 314 | Worst parents P3 and P4 in iteration 2 are replaced |
| 3 | P2 | 1-5-3-2-4 | 361 | with their mC1 and mC2. |
| 3 | P3 | 2-3-5-1-4 | 324 | Chosen parents are P4 (best $z$ ) and P2 (random). |
| 3 | P4 | 5-3-2-1-4 | 222 | Crossover P2 and P4 starting at position 3. |
| 3 | C1 | 5-3-1-2-4 | 314 | No mutation. |
| 3 | C2 | 1-5-3-2-4 | 361 | No mutation. |

### 10.4 APPLICATION OF METAHEURISTICS TO INTEGER LINEAR PROGRAMS ^ilpsection

This section shows how the metaheuristics developed in Section 10.3 are applied to the following general integer linear programs (ILPs): ^ilpmodel

$$
\text{ Maximize }z = \mathop{\sum }\limits_{{j = 1}}^{n}{c}_{j}{x}_{j}
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j}\left( { \leq  , \geq  ,\text{ or } = }\right) {b}_{i}, i = 1,2,\ldots , m
$$

$$
{L}_{j} \leq  {x}_{j} \leq  {U}_{j}, j = 1,2,\ldots , n
$$

$$
{x}_{j}\text{ integer, }j = 1,2,\ldots , n
$$

The basic elements of an ILP metaheuristic include selection of the starting solution, definition of the neighborhood, and determination of the next search move.

1. Selection of starting solution. The metaheuristics use the rounded continuous optimum solution as the starting solution. In this chapter, the (arbitrary) rule for rounding is: Round up if the fractional value is greater than or equal to .5; else, round down. ^ilpstart

2. Definition of neighborhood. It is more manageable computationally to search the variables one at a time by defining the neighborhood for variable ${x}_{j}$ as ^ilpneighborhood

$$
N\left( {x}_{j}\right)  = \left\{  {\left( {{x}_{1},\ldots {x}_{j} - 1,\ldots ,{x}_{n}}\right) ,\left( {{x}_{1},\ldots ,{x}_{j} + 1,\ldots ,{x}_{n}}\right) }\right\}
$$

For example, suppose that the current solution in a 5-variable problem is $(8,6,4$ , $0,2)$ , and assume that ${x}_{3}$ is targeted for change. Then

$$
N\left( {x}_{3}\right)  = \{ \left( {8,6,3,0,2}\right) ,\left( {8,6,5,0,2}\right) \}
$$

Infeasible solutions that violate lower or upper bounds are excluded from the neighborhood. For example, if ${x}_{4}$ is designated for change and $0 \leq  {x}_{4} \leq  \infty$ , then $N\left( {x}_{4}\right)  = \{ \left( {8,6,4, - \mathbf{1},2}\right) ,\left( {8,6,4,\mathbf{1},2}\right) \}  = \{ \left( {8,6,4,\mathbf{1},2}\right) \}$ , because ${x}_{4} =  - 1$ is infeasible.

3. Determination of the next search move. The next search move is determined from a neighborhood as the solution $\mathbf{X} = \left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)$ with the least infeasibility. ${}^{7}$ The infeasibility measure is computed as ^ilpinfeasibility

$$
{I}_{\mathbf{X}} = \mathop{\sum }\limits_{\left(  \leq  \right) }\max \left\{  {0,\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - {b}_{i}}\right\}   + \mathop{\sum }\limits_{\left(  \geq  \right) }\max \left\{  {0,{b}_{i} - \mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j}}\right\}
$$

$$
+ \mathop{\sum }\limits_{\left(  = \right) }\max \left\{  {0,\left| {\mathop{\sum }\limits_{{j = 1}}^{n}{a}_{ij}{x}_{j} - {b}_{i}}\right| }\right\}   + \mathop{\sum }\limits_{{j = 1}}^{n}\left( {\max \left\{  {0,{L}_{j} - {x}_{j}}\right\}   + \max \left\{  {0,{x}_{j} - {U}_{j}}\right\}  }\right)
$$

If ${I}_{\mathbf{X}} = 0$ , then the next search move is feasible.

The remainder of the section details the development of TS, SA, and GA ILP. ${}^{8}$ The ideas can be applied to any ILP and, indeed, can be extended to nonlinear programs.

#### 10.4.1 ILP Tabu Algorithm ^ilptabu

The TS algorithm for an $n$ -variable ILP uses the following definitions:

$$
\mathbf{X} = \left( {{x}_{1},\ldots ,{x}_{j},\ldots ,{x}_{n}}\right)
$$

$$
{L}_{j} = \text{ Lower bound on }{x}_{j}\text{ (default } = 0\text{ ) }
$$

$$
{U}_{j} = \text{ Upper bound on }{x}_{j}\text{ (default } = \infty \text{ ) }
$$

---

${}^{7}$ More sophisticated metaheuristics include techniques for restoring feasibility or use of Lagrangean functions to penalize feasibility violations (see, e.g., Abramson and Randall, 1999).

${}^{8}$ A review of Section 10.3 is recommended before proceeding with this material.

---

$N\left( {x}_{j}\right)  = \left\{  {\left( {{x}_{1},\ldots {x}_{j} - 1,\ldots ,{x}_{n}}\right) ,\left( {{x}_{1},\ldots ,{x}_{j} + 1,\ldots ,{x}_{n}}\right) }\right\}$

${\mathbf{X}}_{j}^{t}\left( k\right)  =$ Solution $\mathbf{X}$ in which ${x}_{j}$ is replaced with ${x}_{j} + k\left( {k =  \pm  1}\right)$ at iteration $t$

${I}_{j}^{t}\left( k\right)  =$ Infeasibility measure of solution ${\mathbf{X}}_{j}^{t}\left( k\right)$

${z}_{j}^{t}\left( k\right)  =$ Objective value associated with ${\mathbf{X}}_{j}^{t}\left( k\right)$

${\mathbf{X}}^{ * } =$ Best feasible solution encountered during the search

${z}^{ * } =$ Objective value associated with ${\mathbf{X}}^{ * }$

${I}^{ * } = \min \left\{  {{I}_{j}^{t}\left( k\right) , j = 1,2,\ldots , n;k =  - 1,1}\right\}$ encountered in iteration $t$

${j}^{ * } = \operatorname{Index}j$ associated with ${I}^{ * }$

${k}^{ * } =$ Value of $k\left( { =  \pm  1}\right)$ associated with ${I}^{ * }$

$\tau  =$ Tabu tenure period, expressed in number of iterations

The tabu list is composed of the indices of tabu variables.

The algorithm starts by setting $\mathbf{X}$ equal to the rounded optimum LP solution. At iteration $t$ , a tabu variable is allowed (per the aspiration criterion, Section 10.3.1) to define the next search move if it results in an improved feasible solution. Otherwise, a tabu variable is excluded.

At iteration $t$ , the search computes the associated infeasibility measure ${I}_{j}^{t}\left( k\right)$ and the objective value ${z}_{j}^{t}\left( k\right)$ for all $j$ and $k$ . The algorithm keeps track of the candidate for the next move by updating the indices ${j}^{ * }$ and ${k}^{ * }$ . A better feasible solution automatically defines the next move. Otherwise, the non-tabu move with the least infeasibility measure is selected. If ${j}^{ * } = 0$ , all neighborhood solutions are tabu and the tabu list is emptied to allow the search to continue.

## Example 10.4-1 ^ilpexamplea

The TS is applied to the following ILP:

$$
\text{ Maximize }z = 2{x}_{1} + {x}_{2} + 3{x}_{3} + 2{x}_{4}
$$

Subject to

$$
{x}_{1} + 2{x}_{2} - 3{x}_{3} - {x}_{4} \leq  {10}
$$

$$
3{x}_{1} - 2{x}_{2} + {x}_{3} - {x}_{4} \leq  {14}
$$

$$
2{x}_{1} + {x}_{2} - 2{x}_{3} + 2{x}_{4} \leq  9
$$

$$
- {x}_{1} + {x}_{2} + {x}_{3} \leq  {10}
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4}\text{ nonnegative integers }
$$

The optimum continuous solution is ${x}_{1} = {4.625},{x}_{2} = 0,{x}_{3} = {14.625},{x}_{4} = {14.5}$ with $z = {82.125}$ . Its optimum integer solution (obtained by TORA) is ${x}_{1} = 5,{x}_{2} = 1,{x}_{3} = {14},{x}_{4} = {13}$ with $z = {79}$ . The rounded solution is $\mathbf{X} = \left( {5,0,{15},{15}}\right)$ . The associated infeasibility measures are ${I}_{\mathbf{X}} = 2$ with ${z}_{\mathbf{X}} = {85}$ . (Verify!)

Table 10.15 gives five iterations using a tabu tenure period $\tau  = 4$ iterations. An underlined index identifies a tabu variable. For example, ${x}_{1}\left( { = 4}\right)$ enters the tabu list at iteration 1, hence it is underlined. At iteration 5, the underline is removed because the tabu tenure period is $\tau  = 4$ .

TABLE 10.15 Tabu Search of ILP Example with Tenure Period $\tau  = 4$ ^tableilptabu

| Iteration | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${I}^{ * }$ | $z$ | ${j}^{ * }$ | ${k}^{ * }$ |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| LP optimum | 4.625 | 0 | 14.625 | 14.5 |  | 82.125 |  |  |
| Search start | 5 | 0 | 15 | 15 | 2 | 85 |  |  |
| 1 | 4 | 0 | 15 | 15 | 1 | 83 | 1 | -1 |
| 2 | 4 | 0 | 15 | 14 | 1 | 81 | 4 | -1 |
| (Best) 3 | 4 | 0 | 14 | 14 | 0 | 78 | 3 | -1 |
| (All-tabu list) 4 | 4 | 1 | 14 | 14 | 1 | 79 | 2 | 1 |
| (Empty tabu list) 4a | 4 | 1 | 14 | 14 |  |  |  |  |
| (Repeat of iteration 3) 5 | 4 | 0 | 14 | 14 | 0 | 78 | 2 | -1 |
| (Restart, iteration 4) 5a | 4 | 1 | 14 | 14 |  |  |  |  |

The search encounters the first feasible solution at iteration 3 (which happens to be the best solution in all 5 iterations). At iteration 4, all the variables are tabu, and no neighborhood solution leads to a better solution. Thus, the tabu list is emptied, releasing all four variables and yielding the solution $\left( {4,1,{14},{14}}\right)$ as the start of future search. At iteration 5 the neighborhood ${x}_{2} = 0$ yields $I = 0$ and hence is selected (and underlined). However, the resulting solution $\left( {4,\underline{0},{14},{14}}\right)$ is a repeat of iteration 3 solution. Hence the next iteration will restart with iteration 4 solution $\left( {4,\underline{1},{14},{14}}\right)$ with ${x}_{2}$ tabooed to allow a different search move. In this case, iteration 6 will produce the new (minimum-infeasibility) solution $\left( {4,\underline{1},{14},\underline{13}}\right)$ with $z = {77}$ . (Try it!)

## Excel Moment

File excelTabu-IP-Heuristic.xls allows experimentation with small-size problems (up to 10 variables). The spreadsheet presentation is basically a learning tool designed to reinforce your understanding of the details of TS. Commercial TS algorithms include additional rules for solving very large problems.

#### 10.4.2 ILP Simulated Annealing Algorithm ^ilpsa

In Section 10.4.1 dealing with TS, all the variables are examined before selecting the next search move. The same strategy can be used with SA. However, for the sake of variation, we will adopt a new strategy that calls for examining one randomly selected variable in each iteration.

The following definitions are used in detailing the steps of the SA algorithm:

$\mathbf{X} = \left( {{x}_{1},\ldots ,{x}_{j},\ldots ,{x}_{n}}\right)$

${L}_{j} =$ Lower bound on ${x}_{j}\left( {\text{ default } = 0}\right)$

${U}_{j} =$ Upper bound on ${x}_{j}\left( {\text{ default } = \infty }\right)$

$N\left( {x}_{j}\right)  = \left\{  {\left( {{x}_{1},\ldots {x}_{j} - 1,\ldots ,{x}_{n}}\right) ,\left( {{x}_{1},\ldots ,{x}_{j} + 1,\ldots ,{x}_{n}}\right) }\right\}$

${\mathbf{X}}_{j}^{t}\left( k\right)  =$ Solution $\mathbf{X}$ in which ${x}_{j}$ is replaced with ${x}_{j} + k\left( {k =  \pm  1}\right)$ at iteration $t$

${I}_{j}^{t}\left( k\right)  =$ Infeasibility measure of solution ${\mathbf{X}}_{j}^{t}\left( k\right)$

${z}_{j}^{t}\left( k\right)  =$ Objective value associated with ${\mathbf{X}}_{j}^{t}\left( k\right)$

${\mathbf{X}}^{ * } =$ Best feasible solution encountered during the search

${z}^{ * } =$ Objective value associated with ${\mathbf{X}}^{ * }$

${I}^{ * } = \min \left\{  {{I}_{j}^{t}\left( k\right) , k =  - 1,1;j = 1,2,\ldots , n}\right\}$ encountered in iteration $t$

${j}^{ * } =$ Index $j$ associated with ${I}^{ * }$

${k}^{ * } =$ Index $k$ associated with ${I}^{ * }$

${T}_{0} =$ Initial temperature

$r =$ Temperature reduction ratio applied every $t$ accept-iterations

${T}_{i} =$ Temperature at level $i$

$= r{T}_{i - 1},0 < r < 1$

$a =$ Counter of number of accept-iteration since last temperature reduction

${a}^{ * } =$ Number of accept-iterations needed to trigger temperature reduction

${z}_{\text{ last }} =$ Objective value of the last accepted solution

$R = \left( {0,1}\right)$ random number

At the start of the algorithm, $\mathbf{X}$ is set equal to the rounded LP solution. In each iteration, an index $j = {j}^{ * }$ is selected randomly from the variables set $\{ 1,2,\ldots , n\}$ , and the feasibility measure ${I}_{j}^{t}\left( k\right)$ is determined for the neighborhood solutions. Feasibility includes checking the upper and lower bounds ${U}_{j}$ and ${L}_{j}$ .

1. If solution ${\mathbf{X}}_{{j}^{ * }}^{t}\left( {k}^{ * }\right)$ has been encountered previously (i.e., redundant), reject it and start a new iteration.

2. If ${\mathbf{X}}_{{j}^{ * }}^{t}\left( {k}^{ * }\right)$ is infeasible, allow it as the next move.

3. If ${\mathbf{X}}_{{j}^{ * }}^{t}\left( {k}^{ * }\right)$ is a no-worse feasible solution, allow it as the next move.

4. If ${\mathbf{X}}_{{j}^{ * }}^{t}\left( {k}^{ * }\right)$ is an inferior feasible solution, accept it as the next move if ^ilpsaaccept

$$
R \leq  \exp \left( \frac{-\left| {{z}_{\text{ last }} - {z}_{{j}^{ * }}^{t}\left( {k}^{ * }\right) }\right| }{T}\right) \text{ . Otherwise, reject it. }
$$

Prior to the start of a new iteration, the temperature $T$ is reduced if $a = {a}^{ * }$ .

## Example 10.4-2 ^ilpexampleb

We use the ILP defined in Example 10.4-1 starting with the rounded solution $\left( {{x}_{1} = 5,{x}_{2} = 0}\right.$ , ${x}_{3} = {15},{x}_{4} = {15})$ and the initial temperature ${T}_{0} = {.75} \times$ (LP optimum objective value) $= \; {.75}\left( {82.125}\right)  \approx  {62}$ . Temperature reduction is triggered every ${a}^{ * } = 2$ accept-iterations using a reduction ratio $r = {.5}$ . Table 10.16 summarizes 10 iterations. At each iteration, the randomly selected variable is labeled with an underline. For example, ${x}_{1}$ is the random selection at iteration 1 and ${x}_{4}$ at iteration 2. According to the rules of the algorithm, an infeasible nonredundant solution is allowed as a move toward achieving feasibility. This occurs at iterations 1, 2, and 4. Also, a move is always generated from the most recent allowed/accepted move. For example, the move at iteration 6 is generated from the allowed move at iteration 4 because the move at iteration 5 is rejected.

TABLE 10.16 Simulated Annealing Applied to ILP of Example 10.4-1 with ${T}_{0} = {.75}$ (LP Objective Value), $r = {.5}$ , and ${a}^{ * } = 2$ ^tableilpsa

| Iteration $t$ | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | ${I}^{ * }$ | ${z}_{{j}^{ * }}^{t}\left( {k}^{ * }\right)$ | ${z}_{\text{ last }}$ | Temp $T$ | $\exp \left( \frac{-\left| {{z}_{\text{ last }} - {z}_{{j}^{ * }}^{t}\left( {k}^{ * }\right) }\right| }{T}\right)$ | $R$ | Explanation |
|---|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|---|
| Search start | 5 | 0 | 15 | 15 | 2 | 85 | $- \infty$ | 62 |  |  | Infeasible first trial solution |
| 1 | 4 | 0 | 15 | 15 | 3 | 83 | $- \infty$ | 62 |  |  | Infeasible move: Allow |
| 2 | 4 | 0 | 15 | 14 | 1 | 81 | $- \infty$ | 62 |  |  | Infeasible move: Allow |
| (Best) 3 | 4 | 0 | 14 | 14 | 0 | 78 | $- \infty$ | 62 |  |  | First feasible move: Accept |
| 4 | 4 | 0 | 13 | 14 | 1 | 75 | 78 | 62 |  |  | Infeasible move: Allow |
| 5 | 4 | 0 | 14 | 14 | 0 | 78 | 78 | 62 |  |  | Redundant: Reject |
| 6 | 4 | 0 | 13 | 13 | 0 | 73 | 78 | 62 | 0.92 | 0.11 | $R < \mathrm{P}\{$ accept $\}$ : Accept |
| 7 | 4 | 1 | 13 | 13 | 0 | 74 | 73 | 31 |  |  | ${z}_{{i}^{ * }{k}^{ * }}^{t} > {z}_{\text{ last }}$ : Accept |
| 8 | 4 | 1 | 13 | 12 | 0 | 72 | 74 | 31 | 0.94 | 0.93 | $R < \mathrm{P}\{$ accept $\}$ : Accept |
| 9 | 4 | 1 | 12 | 12 | 0 | 69 | 72 | 15.5 | 0.82 | 0.96 | $R > \mathrm{P}\{$ accept $\}$ : Reject |
| 10 | 4 | 0 | 13 | 12 | 0 | 71 | 72 | 15.5 | 0.94 | 0.38 | $R < \mathrm{P}\{$ accept $\}  :$ Accept |

Best solution occurs at iteration 3.

The move at iteration 3 is accepted because it is the first feasible solution encountered in the search. This sets ${z}^{ * } = {78}$ and ${\mathbf{X}}^{ * } = \left( {4,0,{14},{14}}\right)$ . At iteration 6, the inferior feasible solution is accepted because it satisfies the condition $R < P\{$ accept $\}$ . At iteration7, the feasible move is accepted because it is an improvement over last accept-solution $\left( {z}_{\text{ last }}\right)$ in iteration 6 . Note that the temperature $T$ is adjusted every 2 accept-iterations at iterations 7 and 9 .

## Excel Moment

As in TS, file excelSA-IP-Heuristic.xls allows experimentation with small-size problems (number of variables $\leq  {10}$ ). The user can study the impact of changing the data in steps 2 and 3 on the efficacy of the algorithm. One of the immediate observations about the behavior of the algorithm is that the "frequency" of rejecting feasible solutions increases with the number of iterations, a typical behavior of SA.

#### 10.4.3 ILP Genetic Algorithm ^ilpga

In Section 10.2.3, binary coding is used in the development of the GA. The same idea can be applied to ILP. For example, in a 3-variable problem, the solution $\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = \left( {{100},{24},{60}}\right)$ can be represented by the binary code in Table 10.17. In general, the number of binary bits is adjusted to represent the maximum value of any of the variables.

A convenient way to represent the ILP variables is to use numeric coding. In this case, the rounded LP solution in an $n$ -variable problem is represented as $\overline{\mathbf{X}} = \left( {{\bar{x}}_{1},{\bar{x}}_{2},\ldots ,{\bar{x}}_{n}}\right)$ . The initial population chromosomes can be generated randomly from the range $\left( {{\bar{x}}_{j} - q{\bar{x}}_{j},{\bar{x}}_{j} + q{\bar{x}}_{j}}\right) ,0 < q < 1$ . The resulting limits of the range are adjusted if the bounds ${L}_{j} \leq  {x}_{j} \leq  {U}_{j}, j = 1,2,\ldots , n$ are tighter. A convenient way to determine the genes is to sample from the continuous search range and then approximate the result to an integer value.

TABLE 10.17 Binary Coding of $\left( {{x}_{\mathbf{1}},{x}_{\mathbf{2}},{x}_{\mathbf{3}}}\right)  = \left( {{100},{24},{60}}\right)$ ^tablebinary

| ${x}_{1} = {100}$ | ${x}_{2} = {24}$ | ${x}_{3} = {60}$ |
|---|---|---|
| 0010011 | 0001100 | 0011110 |

Table 10.18 demonstrates the idea of generating a population of three parent chromosomes starting with the solution $\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = \left( {{100},1,{60}}\right)$ with bounds $0 \leq  {x}_{1} \leq  {99},0 \leq  {x}_{2} \leq  \infty ,{50} \leq  {x}_{3} \leq  \infty$ , and using $q = {.2}$ . The genes of each parent are determined randomly from the respective (adjusted) ranges.

Suppose that parents 1 and 2 in Table 10.18 are selected to create the two children based on a one-point crossover at ${x}_{3}$ . This means that gene 3 is swapped between parents 1 and 2 to provide the child chromosomes as

$$
\text{ Child1: }\left( {{92},7,{70}}\right)
$$

$$
\text{ Child2: }\left( {{81},9,\underline{58}}\right)
$$

(It is immaterial which chromosome is designated as child 1 or child 2.)

Mutation is applied according to a specified (small) probability. Suppose that gene 1 of child 1 is mutated from the original value of 92 to the new random value of 89 selected from the search range $\left( {{80},{99}}\right)$ . The mutated chromosome of child 1 thus becomes $\left( {{89},7,{70}}\right)$ .

The GA algorithm uses the following definitions:

$\mathbf{X} = \left( {{\underline{x}}_{1},\ldots ,{\underline{x}}_{j},\ldots ,{\underline{x}}_{n}}\right)$

$q =$ Neighborhood search ratio $\left( { < 1}\right)$

${\mathbf{X}}^{ * } =$ Best feasible solution encountered during the search

${z}^{ * } =$ Objective value associated with ${\mathbf{X}}^{ * }$

${I}_{i} =$ Infeasibility associated with chromosome $i$

${I}^{ * } =$ Smallest infeasibility associated with the current population

${i}^{ * } =$ Chromosome with the best objective value or the smallest infeasibility in the current population

${i}^{* * } =$ Chromosome with the worst infeasibility in the current population

TABLE 10.18 Random Generation of Initial Population of 3 Parents Starting with Solution $\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = \left( {{100},1,{60}}\right)$ ^tableranges

|  | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ |
|---|---|---|---|
| Starting value | 100 | 8 | 60 |
| ${L}_{j} \leq  {x}_{j} \leq  {U}_{j}$ | $0 \leq  {x}_{1} \leq  {99}$ | $0 \leq  {x}_{2} \leq  \infty$ | ${50} \leq  {x}_{3} \leq  \infty$ |
| $\left( {{x}_{j} - q{x}_{j},{x}_{j} + q{x}_{j}}\right) , q = {.2}$ | (80, 120) | (6.4, 9.6) | (48,72) |
| Adjusted search ranges | (80, 99) | (6, 10) | (50,72) |
| Parent 1 | 92 | 7 | 58 |
| Parent 2 | 81 | 9 | 70 |
| Parent 3 | 90 | 8 | 62 |

${i}^{* *  * } =$ Chromosome with the next-worst infeasibility relative to ${i}^{* * }$

$P =$ Population size

$c =$ Number of crossovers

$p =$ Mutation probability

The GA metaheuristic starts with a population of $P$ chromosomes. The population is then examined for the best feasible solution. Such a solution, if it exists, identifies parent 1. If no feasible solution exists, the chromosome with the smallest infeasibility is used instead to identify parent 1. Parent 2 is then determined randomly from the remaining chromosomes (after excluding that of parent 1). Child 1 and child 2 are created from parent 1 and parent 2 (using crossovers or some other method) with random mutation. Next, child 1 and child 2 replace chromosomes ${i}^{* * }$ and ${i}^{* *  * }$ having the two worst infeasibilities.

## Example 10.4-3 ^ilpexamplec

For the ILP in Example 10.4-1, Table 10.19 provides a starting population of 10 chromosomes generated randomly from the rounded LP solution $\left( {5,0,{15},{15}}\right)$ .

The search ranges, based on $q = {.2}$ , are given at the bottom of the table. All ten chromosomes happen to be infeasible. Chromosome 5 is chosen as parent 1 because it has the smallest infeasibility. Chromosome 2 is selected randomly from the remaining chromosomes to represent parent 2. Thus,

$$
\text{ Parent 1: }\left( {4,0,{15},{16}}\right)
$$

$$
\text{ Parent 2: }\left( {5,0,{15},{17}}\right)
$$

With a single crossover $\left( {c = 1}\right)$ , the partition (selected randomly) occurs at variable 4 . Thus, the children are created by exchanging gene 4 (shown in bold) as

$$
\text{ Child1: }\left( {4,0,{15},\mathbf{{17}}}\right)
$$

$$
\text{ Child2: }\left( {5,0,{15},\mathbf{{16}}}\right)
$$

Next, we apply mutation to each child. The probability of mutation of .1 calls for mutating a gene (to a new value in the search range) if $R < {.1}$ . As shown in the table, only (underlined) gene 4 of child 1 is mutated from 17 to 14 .

TABLE 10.19 Starting Population of Size $p = {10}$ Generated from the Rounded LP Solution $\left( {5,0,{15},{15}}\right)$ with $q = {.2}, c = 1$ Crossover, and Mutation Probability .1 ^tableilpga

| Chromosome | ${x}_{1}$ | ${x}_{2}$ | ${x}_{3}$ | ${x}_{4}$ | $I$ | $z$ |
|---|---:|---:|---:|---:|---:|---:|
| 1 | 4 | 1 | 16 | 15 | 3 | 87 |
| (Parent 2) 2 | 5 | 0 | 15 | 17 | 5 | 89 |
| 3 | 6 | 1 | 17 | 12 | 9 | 88 |
| 4 | 4 | 0 | 12 | 14 | 3 | 72 |
| (Parent 1) 5 | 4 | 0 | 15 | 16 | 2 | 85 |
| 6 | 5 | 1 | 12 | 13 | 4 | 73 |
| 7 | 6 | 0 | 14 | 13 | 6 | 80 |
| 8 | 6 | 1 | 15 | 12 | 5 | 82 |
| 9 | 6 | 0 | 15 | 15 | 7 | 87 |
| 10 | 4 | 0 | 12 | 16 | 7 | 76 |
| Child 1 | 4 | 0 | 15 | 14 | 1 | 81 |
| Child 2 | 5 | 0 | 15 | 16 | 3 | 87 |
| Search ranges | (4,6) | (0,1) | (12, 18) | (12,18) |  |  |

In the next iteration, child 1 and child 2 replace two parents in the current population. Parent 3 has the highest infeasibility $\left( { = 9}\right)$ , hence ${i}^{* * } = 3$ . There is a tie between parents 9 and 10 for the next-worst infeasibility. The tie is broken in favor of the chromosome with worse objective value (87 for parent 9 versus 76 for parent 10), which yields ${i}^{* * } = {10}$ . Hence, parent 3 and parent 10 are replaced by child 1 and child 2, respectively. The new population is now ready for a new iteration.

## Excel Moment

With the Excel implementation of GA file excelGA-IP-Heuristic.xls, you can step through the iterations one at a time or execute all the iterations automatically. In the former case, FIRST Iteration button initializes the computations. Each additional click of NEXT Iteration button generates a new iteration. This iterative design uses color codes to show how a child chromosome replaces a parent chromosome in the next iteration.

If the number of crossovers, $c$ , in cell H4 is set equal to zero, the genes of the two children are given by the arithmetic and geometric means of the parents.

### 10.5 INTRODUCTION TO CONSTRAINT PROGRAMMING (CP) ^cpsection

Suppose that we want to determine the values of the variables $x, y$ , and $z$ that satisfy the following requirements:

$$
{x\varepsilon }\{ 1,2,\ldots ,8\}
$$

$$
{y\varepsilon }\{ 1,2,\ldots ,{10}\}
$$

$$
{z\varepsilon }\{ 1,2,\ldots ,{10}\}
$$

$$
x \neq  7, y \neq  2, x - y = {3z}
$$

One way to solve the problem is to enumerate all 800 combinations, which is computationally inefficient.

Constraint programming solves the problem by producing tighter domains for the variables. ^cppropagation

It then applies an "intelligent" search tree to find the feasible solutions. ^cptree

The constraints $x \neq  7$ and $y \neq  2$ reduce the domains of $x$ and $y$ to

$$
\text{ Domain of }x : {x\varepsilon }\{ 1,2,3,4,5,6,8\}
$$

$$
\text{ Domain of }y : {y\varepsilon }\{ 1,3,4,5,6,7,8,9,{10}\}
$$

Next, the constraint $x - y = {3z}$ requires the minimum value of $x$ to be 4, which occurs when $y = z = 1$ . The maximum value of $y$ is 5, which occurs when $x = 8$ and $z = 1$ . Next, max $\left( {x - y}\right)  = 7$ , which occurs when $x = 8$ and $y = 1$ and produces max $\left( z\right)  = 2$ . This so-called constraint propagation results in the following feasible, but tight, domains:

$$
{x\varepsilon }\{ 4,5,6,8\}
$$

$$
{y\varepsilon }\{ 1,3,4,5\}
$$

$$
{z\varepsilon }\{ 1,2\}
$$

The use of constraint propagation reduces the number of combinations from 800 to 32. Although the new problem is more manageable computationally, we can do better by using the search tree in Figure 10.3. We will select $z$ to initiate the search because it has the smallest domain, giving rise to the two branches only: $z = 1$ and $z = 2$ . Branch $z = 1$ implies that $x - y = 3$ , which is satisfied for $\left( {x = 4, y = 1}\right) ,\left( {x = 6, y = 3}\right)$ , and $\left( {x = 8, y = 5}\right)$ , resulting in three solutions in Figure 10.3. For $z = 2$ , the resulting condition $x - y = 6$ is impossible to satisfy for the given domains. This completes the search tree. The computational advantage here is that we only need to investigate 4 out the possible 32 combinations.

The example above provides the gist of what CP does. It is basically an efficient search process that is based on describing the problem in terms of the domains for the variables and a set of constraints. To facilitate the search, special computer languages have been developed that allow restricting the values of the variables within their domains to satisfy the constraints. As an illustration, Figure 10.4 codes the problem in ILOG OPL. The code directly describes the problem in terms of variable domains and constraints. All domain reductions are carried out automatically by the language processor using intelligent procedures.

As the example demonstrates, CP is not an optimization technique in the sense used in mathematical programming. However, the fact that CP can be used to determine feasible solutions can enhance the efficiency of mathematical programming algorithms. In particular, CP can be imbedded within the B&B algorithm for the MIP problem.

FIGURE 10.3

Construction of search tree for CP example

![bo_d56m4pn7aajc73800nbg_27_501_1634_876_443_0.jpg](bo_d56m4pn7aajc73800nbg_27_501_1634_876_443_0.jpg)

---

	1 var int x in 1.8; FIGURE 10.4

2 var int y in 1..10; ILOG OPL code for the CP example ^oplcode

3 var int z in 1..10;

4 solve\{

5 x<>7;

	6 y<>2;

		7 x-y=3*z;

		8 \};

---

## BIBLIOGRAPHY ^bibliography

Abramson, D., and M. Randall, "A Simulated Annealing Code for General Integer Linear Program," Annals of Operations Research, Vol. 86, pp. 3-21, 1999.

Glover, F., "Tabu Search - Part I," ORSA Journal on Computing, Vol. 1, pp. 190-206, 1989.

Glover, F., "Tabu Search - Part II," ORSA Journal on Computing, Vol. 2, pp. 4-32, 1990.

Hertz, A., and D. de Werra, "The Tabu Search Metaheuristic: How We Used It," Annals of Mathematics and Artificial Intelligence, Vol. 1, pp. 111-121, 1991.

Kirkpatrick, S., C. D. Gelatt Jr., and M. P. Vecchi, "Optimization by Simulated Annealing," Science, Vol. 220, pp. 671-680, 1983.

Michalewicz, Z., and D. B. Fogel, How to Solve It: Modern Heuristics. Springer-Verlag, 2000.

Yamada, T., and R. Nakano, "Genetic Algorithm for Job-Shop Scheduling Problems," Proceeding of Modern Heuristic for Decision Support, UNICOM Seminar (March 18-19), London, pp. 67-81, 1997.

Yamamoto, M., G. Câmara, and L. Lorena, "Tabu Search Heuristic for Point-Feature Cartographic Label Placement," GeoInformatica, Vol. 6, No. 1, pp. 77-90, 2002.

## PROBLEMS ^problems

Assigned Problems by Section ^tableproblems

| Section | Assigned Problems | Section | Assigned Problems |
|---|---|---|---|
| 10.3.1 | 10-9 to 10-16 | 10.4.2 | 10-33 to 10-35 |
| 10.3.2 | 10-17 to 10-23 | 10.4.3 | 10-36 to 10-38 |
| 10.3.3 | 10-24 to 10-29 | 10.5 | 10-39 to 10-40 |
| 10.4.1 | 10-30 to 10-32 |  |  |

10-1. Re-solve the problem of Example 10.2-1 to estimate the maximum value of $F\left( x\right)$ . Repeat the calculations using $x = 7$ as a starting solution.

10-2. Re-solve the problem of Example 10.2-2 to estimate the maximum value of $F\left( x\right)$ .

10-3. Re-solve the problem of Example 10.2-3 to estimate the maximum value of $F\left( x\right)$ using uniform sampling. Next, use the solution from uniform sampling as a starting solution for the application of normal sampling.

10-4. Excel experiment. Consider the following function:

$$
f\left( x\right)  = {.01172}{x}^{6} - {.3185}{x}^{5} + {3.2044}{x}^{4} - {14.6906}{x}^{3} + {29.75625}{x}^{2} - {19.10625x}
$$

The function has multiple maxima and minima in the range $0 \leq  x \leq  {10}$ . Use excelContVarHeuristic.xls to estimate the maximum and minimum of the function using uniform sampling starting at ${x}_{0} = 5$ and then refine the solution using normal sampling in which the starting point is the solution obtained from uniform sampling.

10-5. Consider the problem of forming a maximum-area rectangle out of a piece of wire of length 100 inches.

(a) Excel experiment. Use excelContVarHeuristic.xls with uniform sampling to generate 5 iterations of the continuous variable heuristic to estimate the dimensions of the rectangle. Start with a base of rectangle equal to 5 inches.

(b) Excel experiment. Use excelContVarHeuristic.xls with normal sampling to refine the solution obtained in (a). Carry out 5 iterations.

*10-6. Taxation can be used as an instrument to curb the demand for cigarettes. Suppose that, for a tax rate $t$ , the average daily consumption per smoker follows the linear function ${53} - {100}\left( {t/{100}}\right) ,{10} \leq  t \leq  {60}$ . If the tax rate is set high, demand will drop, and the tax revenue will drop as well. The goal is to determine the tax rate that maximizes the tax revenue. For the purpose of taxation, the base price per cigarette is 15 cents. Formulate the problem as a mathematical model, and use a heuristic to determine the tax rate.

10-7. Apply the uniform sampling heuristic to estimate the minimum solution of the following two-variable function: $f\left( x\right)  = 3{x}^{2} + 2{y}^{2} - {4xy} - {2x} - {3y},0 \leq  x \leq  5,0 \leq  y \leq  5$ .

10-8. The height of a cylindrical water tank must be at least twice as much as its base diameter. Neither the diameter nor the height can exceed ${10}\mathrm{{ft}}$ . The volume of the tank must be at least ${300}{\mathrm{{ft}}}^{3}$ . The cost of the elevated structure on which the tank is installed is proportional to the area of the base. The sheet metal cost is $\$ 8/{\mathrm{{ft}}}^{2}$ , and the cost of the supporting structure is $\$ {15}/{\mathrm{{ft}}}^{2}$ . Formulate the problem as a mathematical model, and develop a random-walk heuristic to estimate the diameter and height of the tank.

10-9. Solve Example 10.2-1 to estimate the maximum solution point. Use ${x}_{0} = 8$ and $\tau  = 2$ .

10-10. Consider the following function:

$$
f\left( x\right)  = {.01172}{x}^{6} - {.3185}{x}^{5} + {3.2044}{x}^{4} - {14.6906}{x}^{3} + {29.75625}{x}^{2} - {19.10625x}
$$

The function has multiple maxima and minima in the range $x = 1,2,\ldots ,{10}$ . Apply 10 TS iterations to estimate the maximum and minimum. Use ${x}_{0} = 5$ and tabu tenure period $\tau  = 2$ iterations.

10-11. Apply TS with $\tau  = 3$ iterations to solve the 5-job sequencing problem using the data in Table 10.20. (Hint: You may find it convenient to use file excelJobSequencing.xls to compute the cost functions.)

TABLE 10.20 Data for Problem 10-11

| Job, $j$ | Processing time in days, ${T}_{j}$ | Due date, ${d}_{j}$ | Holding cost, ${h}_{i}$ (\$/day) | Penalty cost ${p}_{i}$ (\$/day) |
|---:|---:|---:|---:|---:|
| 1 | 10 | 12 | 3 | 10 |
| 2 | 12 | 30 | 1 | 20 |
| 3 | 5 | 9 | 5 | 12 |
| 4 | 7 | 25 | 2 | 8 |
| 5 | 9 | 40 | 4 | 15 |

10-12. Consider 10 Boolean variables, $\mathrm{B}i, i = 1,2,\ldots ,{10}$ . Each variable assumes the value $T$ (true) or $F$ (false). Next, consider the following six expressions (the notation $\underline{\mathrm{B}}i$ defines not Bi):

(B1 and B3 and B8) or (B4 and B10) and B6

B2 and B7

(B2 or B5) and (B1 or B4 or B6)

(B1 and B3 or B4) or (B5)

(B4 and B6) or B9

B2 or B5 or B6 or (B1 and B3)

Use TS to assign a solution to each Boolean variable that maximizes the number of true logical expressions. Carry out five TS iterations starting with solution ${S}_{0} = \left( {T, F, T, F, T, F, T, F, T, F}\right)$ and a tabu tenure period of two iterations. (Hint: For convenience, file exelSAT.xls automates the evaluation of the Boolean expressions.)

10-13. Repeat Problem 10-12 for the following Boolean expressions:

(B1 and B5) or (B3 and B9) and (B2 or B10)

B3 or B6 and (B7 or B9 and B10)

B4 and B7 and B8

B2 or B3 and B4 and B5 or B8 and (B1 or B6)

(B3 and B4 and B10) or (B5 and B7) or (B9 and B10)

B1 or (B4 and B7) or B8

(B3 and B5 or B6) or (B1 or B8 and B9 or B10)

10-14. Warehouse allocation. Consider the case of 4 warehouses and 5 stores. The fixed cost of opening a warehouse is20(\$ thousand). The transportation cost, ${c}_{ij}$ , of shipments between the warehouses and the stores is summarized in Table 10.21.

(a) Formulate the problem as an ILP, and find the optimum solution (using AMPL or Solver).

(b) Solve the problem using TS with a tabu tenure period of two iterations.

TABLE 10.21 Data for Problem 10-14

| $j$ / $i$ | 1 | 2 | 3 | 4 | 5 |
|---:|---:|---:|---:|---:|---:|
| 1 | 10 | 15 | 20 | 9 | 40 |
| 2 | 12 | 17 | 15 | 20 | 10 |
| 3 | 18 | 14 | 10 | 35 | 16 |
| 4 | 9 | 12 | 33 | 28 | 19 |

10-15. Constrained Minimal Spanning Tree, Glover (1990). Section 6.2 presents an optimum algorithm for finding the minimal spanning tree that links all the nodes of a network (by definition, a tree contains no cycles). In a practical setting, it may be necessary to impose interdependence restrictions on the arcs (branches) of the minimal spanning tree (e.g., only one of a subset of arcs can be in the spanning tree). TS can be used to account for the additional restrictions.

Consider the 6-arc network $\left( {a, b, c, d, e, f, g, h}\right)$ in Figure 10.5 with the following additional restrictions:

1. Only one of the two arcs, $a$ and $c$ , can be in the tree.

2. If $\operatorname{arc}b$ is in the tree then arc $d$ must also be in the tree.

The application of TS to determine the constrained minimal spanning tree is achieved as follows: The unconstrained minimal spanning tree $\left( {b, c, f, g, h}\right)$ of length $\left( {2 + 3 + 1 + 6 + 4}\right)  = {16}$ is used as a starting solution. The remaining arcs, $a, d$ , and $e$ , are designated as free. A neighborhood spanning tree (solution) can be generated by adding a free arc to the current spanning tree and deleting an existing one to prevent cycles. For example, arc $b$ or $c$ must be deleted if free arc $a$ is admitted in spanning tree $\left( {b, c, f, g, h}\right)$ to prevent the formation of cycle $a, b, c$ . The swapping produces two alternatives: add $a$ and delete $b$ , or add $a$ and delete $c$ . Similar alternatives can be generated when the remaining free variables, $d$ and $e$ , are considered. The collection of all these alternatives defines the neighborhood.

The fitness of an alternative includes the length of the spanning tree plus a penalty for the violation of the additional constraints given earlier. For example, given the tree $\left( {b, c, f, g, h}\right)$ , the alternative "add $a$ and delete $b$ " produces the tree $\left( {a, c, f, g, h}\right)$ whose fitness is $\left\lbrack  {\left( {5 + 3 + 1 + 6 + 4}\right)  + \left( \text{ penalty for violating the first constraint }\right) }\right\rbrack$ . Similarly, the alternative "add arc $a$ and delete arc $c$ " produces the tree $\left( {a, b, f, g, h}\right)$ whose fitness is $\left\lbrack  {\left( {5 + 2 + 1 + 6 + 4}\right)  + \left( \text{ penalty of violating the second constraint }\right) }\right\rbrack$ . The penalty must be sufficiently large (e.g., a multiple of the sum of the lengths of all the arcs in the network). In the present situation, the total length of the network is 37, and a penalty of 200 is appropriate. The alternative with the smallest fitness provides the next trial solution. The corresponding free variable is then augmented to the tabu list to prevent it from leaving the tree during its tenure period.

Apply five iterations to the network in Figure 10.5.

10-16. Cartographic label placement, Yamamoto and Associates (2002). Unambiguous placement of the names of cities, streets, lakes, and rivers on printed maps has long been a time-consuming manual process. With the advent of online map generation (as in Google and MapQuest), the manual process is not a viable option. A tabu heuristic can be used to automate label placement on map. This problem will deal with the case of labeling cities. The general goal is to avoid label overlapping, while accounting for label placement preferences relative to the location of the named city on the map.

![bo_d56m4pn7aajc73800nbg_31_455_1847_595_320_0.jpg](bo_d56m4pn7aajc73800nbg_31_455_1847_595_320_0.jpg)

FIGURE 10.5

Network for Problem 10-15

![bo_d56m4pn7aajc73800nbg_32_460_197_1040_557_0.jpg](bo_d56m4pn7aajc73800nbg_32_460_197_1040_557_0.jpg)

FIGURE 10.6

Label options for Problem 10-16

Figure 10.6 provides an example of placing the names of four cities, A, B, C, and D, on a map. Each city has four placement options represented by four rectangles. Priority for label placement among the four rectangles can be in any order. In Figure 10.6, we assume a counterclockwise best-to-worst order of preference for the rectangles of each city. For example, for city A, the order of labeling preference is A1-A2-A3-A4. A typical solution selects a specific rectangle for each city. For example, (A1, B2, C3, D2) is a solution for the four cities in Figure 10.6.

The "cost" of selecting a specific rectangle in a solution is the sum of two components: a numeric preference score in the range $\left( {0,1}\right)$ in which zero is best, and the number of overlaps with other rectangles. Figure 10.6 gives the preference scores for the city A $\left( {\mathrm{A}1 = 0,\mathrm{\;A}2 = {.02},\mathrm{\;A}3 = {.03}\text{ , and }\mathrm{A}4 = {.04}}\right)$ . The same scores apply to corresponding rectangles in cities B, C, and D as well. To determine the overlaps, consider the solution (A1, B2, C3, D2). Only C3 and D2 overlap.

The following matrix summarizes the scores associated with solution (A1, B2, C3, D2).

|  | A1 | B2 | C3 | D2 |
|---|---:|---:|---:|---:|
| A1 | .00 | .00 | .00 | .00 |
| B2 | .00 | .02 | .00 | .00 |
| C3 | .00 | .00 | .03 | 1.00 |
| D2 | .00 | .00 | 1.00 | .02 |

All diagonal entries equal the preference scores of the associated rectangle. An off-diagonal element equals 1 if the corresponding elements overlap. Else, it is zero. The cost associated with the solution $\left( {\mathrm{A}1,\mathrm{\;B}2,\mathrm{C}3,\mathrm{\;D}2}\right)$ is the sum of all the entries in the matrix $\left\lbrack  { = \left( {{.02} + {.03} + {.02}}\right)  + \left( {1 + 1}\right)  = {2.7}}\right\rbrack$ . The objective of the model is to find the solution that minimizes the total cost.

(a) Construct the $\left( {{16} \times  {16}}\right)$ fitness table that will account for all possible label placements.

(b) Find a solution to the problem using three TS iterations with a two-iteration tabu tenure. [Hint: The optimum solution for this trivial problem is obvious: (A1, B1, B2, B3, and B4) with zero total fitness. To demonstrate meaningful TS iterations, however, you are required to start with the solution A1, B2, C3, D2. A neighborhood solution consists of replacing one of the rectangles of a city with another, for example, replacing C3 with C1. In this case, city C is placed on the tabu list for the duration of the tenure period.]

10-17. Carry out five additional iterations in Example 10.3-3.

10-18. Solve Example 10.3-3 to estimate the maximum solution point. Use ${x}_{0} = 2$ and $t = 3$ .

10-19. Carry out four additional iterations of the job sequencing problem in Example 10.3-4.

10-20. Timetable scheduling. Consider a case of developing a timetable of teaching 5 classes (C) by 5 teachers (T). The teachers provide the following preferences for teaching classes (first of the list is most desired):

T1: C2-C3-C1-C5

T2: C2-C1-C4-C5

T3: C1-C4-C5-C3

T4: C4-C2-C5-C3

T5: C2-C5-C3-C1

The situation is simplified to developing a one-day five-period timetable that minimizes dissatisfaction among teachers. A measure of dissatisfaction is represented by how far down the preference list a course is assigned to a teacher. For example, the measure of dissatisfaction is zero if C2 is assigned to T1 and 3 if C5 is assigned to T1. A timetable is evaluated by the sum of its individual measures.

Develop a 5-iteration SA heuristic for the problem.

10-21. Map-coloring problem. The coloring problem deals with determining the least number of colors for painting the regions of a map such that no two adjacent regions will have the same color. Figure 10.7(a) provides an example of a 6-region map. The problem can be modeled as a network in which the nodes represent the regions as shown in Figure 10.7(b). An arc between two nodes signifies that the corresponding two regions are adjacent (share a common border). The map-coloring problem can represent other practical situations, as Problem 10-22 demonstrates.

FIGURE 10.7

(a) Six-region map (b) network representation for Problem 10-21

![bo_d56m4pn7aajc73800nbg_33_450_1707_970_466_0.jpg](bo_d56m4pn7aajc73800nbg_33_450_1707_970_466_0.jpg)

An SA heuristic can be applied to the coloring problem. The starting solution, ${x}_{0}$ , can be determined in one of two ways:

1. Assign a unique color to each node of the network. Thus, ${x}_{0} = \left( {1,2,\ldots ,6}\right)$ for the network in Figure 10.7(b),

2. Use a greedy algorithm that starts by assigning color 1 to node 1. Next, given that nodes $1,2,\ldots$ , and $i - 1$ use the colors $1,2,\ldots$ , and $c, c \leq  i - 1$ , assign the smallest color number in the set $\left( {1,2,\ldots , c}\right)$ to node $i$ without creating bad arcs (those whose two end nodes use the same color). If none can be found, apply a new color $c + 1$ . For the network in Figure 10.7(b), the successive steps for constructing ${x}_{0}$ are

$$
{x}_{0}^{1} = \left( 1\right)
$$

$$
{x}_{0}^{2} = \left( {1,2}\right)
$$

$$
{x}_{0}^{3} = \left( {1,2,3}\right)
$$

$$
{x}_{0}^{4} = \left( {1,2,3,1}\right)
$$

$$
{x}_{0}^{5} = \left( {1,2,3,1,4}\right)
$$

$$
{x}_{0} = {x}_{0}^{6} = \left( {1,2,3,1,4,2}\right)
$$

The greedy algorithm uses 4 color classes, ${C}_{1} = \left( {1,1}\right) ,{C}_{2} = \left( {2,2}\right) ,{C}_{3} = \left( 3\right)$ , ${C}_{4} = \left( 4\right)$ , that apply to nodes 1 and 4, nodes 2 and 6, node 3, and node 5 , respectively.

A neighborhood solution, ${x}_{i + 1}$ , is determined by changing the color of a random node in ${x}_{i}$ to a random color in the same set. For example, given ${x}_{0} = \left( {1,2,3,1,4,2}\right)$ and its associated color set ${c}_{0} = \left( {1,2,3,4}\right)$ , random selections of color 1 from ${c}_{0}$ and node (position) 5 from ${x}_{0}$ give

$$
{x}_{1} = \left( {1,2,3,1,1,2}\right)
$$

The new color classes of ${x}_{1}$ are ${C}_{1} = \left( {1,1,1}\right) ,{C}_{2} = \left( {2,2}\right)$ , and ${C}_{3} = \left( 3\right)$ corresponding to nodes $\left( {1,4,5}\right) ,\left( {2,6}\right)$ , and $\left( 3\right)$ , respectively. To generate ${x}_{2}$ from ${x}_{1}$ , randomly select a color from ${c}_{1} = \left( {1,2,3}\right)$ to replace the color of a randomly selected node in ${x}_{1}$ . If necessary, repeat the random exchange until ${x}_{2}$ becomes distinct from ${x}_{1}$ .

Next, we develop a measure of performance for solution. A simple measure calls for the minimization of the number of bad arcs (those whose two end nodes bear the same color). A more sophisticated measure can be developed in the following manner: Solution ${x}_{1}$ is better than ${x}_{0}$ from the standpoint of reducing the number of color classes (i.e., uses less colors by increasing the size of at least one color class), but simultaneously increases the chance of creating bad arcs. Specifically, ${x}_{0}$ of the greedy algorithm has no bad arcs, and ${x}_{1}$ has one bad arc,4-5 . Thus, an empirical measure of performance that balances the two conflicting situations [increasing the sizes (cardinalities) of the color classes and, simultaneously, reducing the number of bad arcs] calls for maximizing

$$
f\left( x\right)  = \mathop{\sum }\limits_{{j = 1}}^{k}{\left( \left| {C}_{j}\right| \right) }^{2} - 2\mathop{\sum }\limits_{{k = 1}}^{k}\left| {C}_{j}\right|  \cdot  \left| {A}_{j}\right|
$$

where

$k =$ Number of color classes

${A}_{j} =$ Set of bad arcs associated with color class $j$

[The notation $\left| S\right|$ represents the number of elements (cardinality) of the set $S$ .] In terms of ${x}_{0}$ and ${x}_{1}$ of the greedy algorithm, we have

$$
f\left( {x}_{0}\right)  = \left( {{2}^{2} + {2}^{2} + {1}^{2} + {1}^{2}}\right)  - 2\left( {2 \times  0 + 2 \times  0 + 1 \times  0 + 1 \times  0}\right)  = {10}
$$

$$
f\left( {x}_{1}\right)  = \left( {{3}^{2} + {2}^{2} + {1}^{2}}\right)  - 2\left( {3 \times  1 + 1 \times  0 + 2 \times  0}\right)  = 8
$$

The two values show that ${x}_{1}$ is worse than ${x}_{0}$ [recall that we are maximizing $f\left( x\right)$ ]. Hence, per SA heuristic, we accept ${x}_{1}$ if $R < {e}^{-\left| {f\left( {x}_{0}\right)  - f\left( {x}_{1}\right) }\right| /T}$ .

Note that the generation of ${x}_{i + 1}$ from ${x}_{i}$ may result in an infeasible color assignment. (This point does not arise in Examples 10.3-3 and 10.3-4 because of the nature of the associated problems.) In these cases, an infeasible move can be accepted using the probability condition of SA, but the best solution is updated only if a better feasible solution is encountered.

Apply three additional SA iterations to the coloring network in Figure 10.7(b) using the greedy algorithm to determine the starting solution and the measure of performance $f\left( x\right)$ , as explained above.

10-22. Scheduling conflicting classroom courses. A simplified version of college course scheduling calls for assigning eight courses $\left( {1,2,\ldots ,8}\right)$ in the least possible number of time periods. Table 10.22 assigns "x" to conflicting courses (those that cannot be scheduled in the same time period).

(a) Express the problem as a map-coloring network (Problem 10-21).

(b) Determine a starting solution using the greedy algorithm.

(c) Apply three SA iterations to estimate the minimum number of periods.

10-23. Consider the well-known six-hump camelback function:

$$
f\left( {x, y}\right)  = 4{x}^{2} - {2.1}{x}^{4} + {x}^{6}/3 + {xy} - 4{y}^{2} + 4{y}^{4}, - 3 \leq  x \leq  3, - 2 \leq  y \leq  2
$$

The exact global minima are ( -.08984, .71266) and (.08984, -.71266) with ${f}^{ * } =  - {1.0316}$ . Apply five SA iterations to estimate the minima of $f\left( {x, y}\right)$ . Start with $\left( {{x}_{0},{y}_{0}}\right)  = \left( {2,1}\right) ,{T}_{0} = {.5f}\left( {{x}_{0},{y}_{0}}\right) ,{T}_{i} = {.5}{T}_{i - 1}$ , and $t = 3$ accept-iterations.

10-24. Suppose that GA is used to find the maximum of $F\left( x\right) , x = 0,1,\ldots ,{275}$ . Let $x = {107}$ and $x = {254}$ represent parents $\mathrm{P}1$ and $\mathrm{P}2$ .

(a) Represent $\mathrm{P}1$ and $\mathrm{P}2$ as binary codes.

(b) Use uniform crossover to create C1 and C2.

(c) Create C1 and C2 using a 1-point crossover.

TABLE 10.22 Conflicts in Course Schedules for Problem 10-22

|  | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---:|---|---|---|---|---|---|---|---|
| 1 |  | X | X | X |  | X |  |  |
| 2 | X |  |  |  | X |  | X | X |
| 3 | X |  |  | X |  | X |  |  |
| 4 | X |  | X |  | X |  | X |  |
| 5 |  | X |  | X |  | X |  | X |
| 6 | X |  | X |  | X |  | X | X |
| 7 |  | X |  | X |  | X |  | X |
| 8 |  | X |  |  | X | X | X |  |

(d) Create C1 and C2 using a 2-point crossover.

(e) In Part (b), use random numbers to mutate C1 and C2.

10-25. Carry out two additional iterations of Example 10.3-5.

10-26. Carry out an additional iteration of Example 10.3-6.

*10-27. You have a deck of ten cards numbered 1 to10. You need to divide the ten cards into two piles such that the sum of pile 1 cards is 36 and the product of the pile 2 cards is also 36. Develop a GA for the problem using an initial population of 4 parents, 1-point crossover, and 1% mutation rate. Carry out 5 iterations.

10-28. You have a piece of wire whose length is $L = {107.1}$ inches and you would like to shape it into a rectangular frame. Use the genetic algorithm to determine the width and height that will yield the maximum area of the rectangle.

10-29. Repeat Problem 10-28 assuming that the wire is used to form a box with the maximum volume.

10-30. Consider the following problem:

Maximize $f\left( {x, y}\right)  = x\sin \left( {4x}\right)  + {1.1}\sin \left( {2y}\right) , x = 0,1,2,\ldots ,{10}, y = 0,1,2,\ldots ,{10}$

Carry out five GA iterations to estimate the optimum solution.

10-31. In the game of chess, queens move horizontally, vertically, or along a (45°) diagonal path. We need to position $N$ queens in the $\left( {N \times  N}\right)$ grid so that no queen can "take" any other queen. Design a GA for the problem starting with a random population of 4 parents and using a 1-point crossover. A reasonable measure of effectiveness is the number of queens in conflict. Carry out three iterations.

10-32. Verify the entries in iterations 1, 2, and 3 in Table 10.15.

10-33. Carry out ${10}\mathrm{\;{TS}}$ iterations for each of the following problems:

(a) Maximize $z = 4{x}_{1} + 6{x}_{2} + 2{x}_{3}$ subject to

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

(b) Maximize $z = 3{x}_{1} + {x}_{2} + 3{x}_{3}$ subject to

$$
- {x}_{1} + 2{x}_{2} + {x}_{3} \leq  4
$$

$$
4{x}_{2} - 3{x}_{3} \leq  2
$$

$$
{x}_{1} - 3{x}_{2} + 2{x}_{3} \leq  3
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0\text{ and integer }
$$

10-34. Excel experiment. Use excelTabu-IP-heuristc.xls to find a solution for the following problems:

(a) Project selection problem of Example 9.1-1.

(b) Set covering problem of Example 9.1-2.

Compare the heuristic and exact solutions.

10-35. Carry out 5 iterations of Example 10.4-2 assuming ${c}_{j} = 1$ for all $j$ .

10-36. Carry out 5 SA iterations for the following problem:

$$
\text{ Maximize }z = {99}{x}_{1} + {90}{x}_{2} + {58}{x}_{3} + {40}{x}_{4} + {79}{x}_{5}
$$

$$
+ {92}{x}_{6} + {102}{x}_{7} + {74}{x}_{8} + {67}{x}_{9} + {80}{x}_{10}
$$

subject to

$$
{30}{x}_{1} + 8{x}_{2} + 6{x}_{3} + 5{x}_{4} + {20}{x}_{5} + {12}{x}_{6} + {25}{x}_{7} + {24}{x}_{8} + {32}{x}_{9} + {29}{x}_{10} \leq  {100}
$$

All variables are binary

10-37. Excel experiment. Use file excels-IP-Heuristic.xls to find a solution for the following ILP:

$$
\text{ Minimize }z = {x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5} + {x}_{6} + {x}_{7}
$$

subject to

$$
{x}_{1}\; + {x}_{4} + {x}_{5} + {x}_{6} + {x}_{7} \geq  {20}
$$

$$
{x}_{1} + {x}_{2}\; + {x}_{5} + {x}_{6} + {x}_{7} \geq  {12}
$$

$$
{x}_{1} + {x}_{2} + {x}_{3}\; + {x}_{6} + {x}_{7} \geq  {14}
$$

$$
{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4}\; + {x}_{7} \geq  {17}
$$

$$
{x}_{1} + {x}_{2} + {x}_{3} + {x}_{4} + {x}_{5}\; \geq  {18}
$$

$$
{x}_{2} + {x}_{3} + {x}_{4} + {x}_{5} + {x}_{6}\; \geq  {19}
$$

$$
{x}_{3} + {x}_{4} + {x}_{5} + {x}_{6} + {x}_{7} \geq  {14}
$$

All variables are binary

10-38. Carry out the next iteration that follows the one given in Table 10.19.

10-39. Carry out two iterations of Problem 10-36.

10-40. Excel experiment. Apply excellPHeuristicGA.xls to Problem 10-37.

10-41. Construct the search tree in Figure 10.3 using the variable $x$ to initiate the search. Compare the resulting amount of computations with that in Figure 10.3.

10-42. Repeat Problem 10-41 using the variable $y$ .
