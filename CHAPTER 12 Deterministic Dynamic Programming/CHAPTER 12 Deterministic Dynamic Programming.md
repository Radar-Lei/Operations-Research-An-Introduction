## CHAPTER 12 Deterministic Dynamic Programming

## Real-Life Application—Optimization of Crosscutting and Log Allocation at Weyerhaeuser

Mature trees are harvested and crosscut into logs to manufacture different end products (construction lumber, plywood, wafer boards, or paper). Log specifications (e.g., length and end diameters) differ depending on the mill where the logs are processed. With harvested trees measuring up to 100 ft in length, the number of crosscut combinations meeting mill requirements can be large, and the manner in which a tree is disassembled into logs can affect revenues. The objective is to determine the crosscut combinations that maximize the total revenue. The study uses dynamic programming to optimize the process. The proposed system was first implemented in 1978 with an annual increase in profit of at least \$7 million. Details of the case are presented at the end of the chapter.

### 12.1 RECURSIVE NATURE OF DYNAMIC PROGRAMMING (DP) COMPUTATIONS

The main idea of DP is to decompose the problem into (more manageable) subproblems. Computations are then carried out recursively where the optimum solution of one subproblem is used as an input to the next subproblem. The optimum solution for the entire problem is at hand when the last subproblem is solved. The manner in which the recursive computations are carried out depends on how the original problem is decomposed. In particular, the subproblems are normally linked by common constraints. The feasibility of these common constraints is maintained at all iterations.

---

## Example 12.1-1 (Shortest-Route Problem)

Suppose that we want to select the shortest highway route between two cities. The network in Figure 12.1 provides the possible routes between the starting city at node 1 and the destination city at node 7. The routes pass through intermediate cities designated by nodes 2 to 6.

---

![bo_d56m4vjef24c73bhe620_1_339_199_727_465_0.jpg](bo_d56m4vjef24c73bhe620_1_339_199_727_465_0.jpg)

FIGURE 12.1

Route network for Example 12.1-1

We can solve this problem by enumerating all the routes between nodes 1 and 7 (there are five such routes). However, exhaustive enumeration is computationally intractable in large networks.

To solve the problem by DP, first decompose it into stages as delineated by the vertical dashed lines in Figure 12.2. Next, carry out the computations for each stage separately.

The general idea for determining the shortest route is to compute the shortest (cumulative) distances to all the terminal nodes of a stage and then use these distances as input data to the immediately succeeding stage. Starting from node 1, stage 1 reaches three end nodes (2, 3, and 4), and its computations are simple.

Stage 1 Summary.

Shortest distance from node 1 to node 2 = 7 miles (from node 1)

Shortest distance from node 1 to node 3 = 8 miles (from node 1)

Shortest distance from node 1 to node 4 = 5 miles (from node 1)

FIGURE 12.2

Decomposition of the shortest-route problem into stages

![bo_d56m4vjef24c73bhe620_1_491_1541_897_626_0.jpg](bo_d56m4vjef24c73bhe620_1_491_1541_897_626_0.jpg)

Next, stage 2 has two end nodes, 5 and 6. Figure 12.2 shows that node 5 can be reached from nodes 2, 3, and 4 via routes (2, 5), (3, 5), and (4, 5). This information, together with the summary results (shortest distances) in stage 1, determines the shortest (cumulative) distance to node 5 as

$$
\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }5 \end{matrix}\right)  = \mathop{\min }\limits_{{i = 2,3,4}}\left\{  {\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }i \end{matrix}\right)  + \left( \begin{matrix} \text{ Distance from } \\  \text{ node }i\text{ to node }5 \end{matrix}\right) }\right\}
$$

$$
= \min \left\{  \begin{array}{l} 7 + {12} = {19} \\  8 + 8 = {16} \\  5 + 7 = {12} \end{array}\right\}   = {12}\text{ (from node 4) }
$$

Node 6 can be reached from nodes 3 and 4 only. Thus

$$
\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }6 \end{matrix}\right)  = \mathop{\min }\limits_{{i = 3,4}}\left\{  {\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }i \end{matrix}\right)  + \left( \begin{matrix} \text{ Distance from } \\  \text{ node }i\text{ to node }6 \end{matrix}\right) }\right\}
$$

$$
= \min \left\{  \begin{array}{l} 8 + 9 = {17} \\  5 + {13} = {18} \end{array}\right\}   = {17}\text{ (from node 3) }
$$

Stage 2 Summary.

Shortest distance from node 1 to node 5 = 12 miles (from node 4)

Shortest distance from node 1 to node 6 = 17 miles (from node 3)

The last step is to consider stage 3. The destination node 7 can be reached from either node 5 or 6. Using the summary results from stage 2 and the distances from nodes 5 and 6 to node 7, we get

$$
\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }7 \end{matrix}\right)  = \mathop{\min }\limits_{{i = 5,6}}\left\{  {\left( \begin{matrix} \text{ Shortest distance } \\  \text{ to node }i \end{matrix}\right)  + \left( \begin{matrix} \text{ Distance from } \\  \text{ node }i\text{ to node }7 \end{matrix}\right) }\right\}
$$

$$
= \min \left\{  \begin{array}{l} {12} + 9 = {21} \\  {17} + 6 = {23} \end{array}\right\}   = {21}\text{ (from node 5) }
$$

Stage 3 Summary.

Shortest distance from node 1 to node 7 = 21 miles (from node 5)

Stage 3 summary shows that the shortest distance between nodes 1 and 7 is 21 miles. To determine the optimal route, start at stage 3 summary, where node 7 links to node 5; stage 2 summary links node 4 to node 5; and stage 1 summary links node 4 to node 1. Thus, the shortest route is $1 \rightarrow  4 \rightarrow  5 \rightarrow  7$ .

The example reveals the basic properties of DP computations:

1. The computations at each stage are a function of the feasible routes of that stage, and only that stage.

2. A current stage is linked to the immediately preceding stage only (without regard to earlier stages) based on the shortest-distance summary of the immediately preceding stage.

Recursive Equation. This section shows how the recursive computations in Example 12.1-1 can be expressed mathematically. Let ${f}_{i}\left( {x}_{i}\right)$ be the shortest distance to node ${x}_{i}$ at stage $i$ , and define $d\left( {{x}_{i - 1},{x}_{i}}\right)$ as the distance from node ${x}_{i - 1}$ to node ${x}_{i}$ . The DP recursive equation is defined as

$$
{f}_{0}\left( {{x}_{0} = 1}\right)  = 0
$$

$$
{f}_{i}\left( {x}_{i}\right)  = \mathop{\min }\limits_{\substack{\text{ all feasible } \\  \left( {{x}_{i - 1},{x}_{i}}\right) \text{ routes } }}\left\{  {d\left( {{x}_{i - 1},{x}_{i}}\right)  + {f}_{i - 1}\left( {x}_{i - 1}\right) }\right\}  , i = 1,2,3
$$

All distances are measured from 0 by setting ${f}_{0}\left( {{x}_{0} = 1}\right)  = 0$ . The main recursive equation expresses the shortest distance ${f}_{i}\left( {x}_{i}\right)$ at stage $i$ as a function of the next node, ${x}_{i}$ . In DP terminology, ${x}_{i}$ is referred to as the state at stage $i$ . The state links successive stages in a manner that permits making optimal feasible decisions at a future stage independently of the decisions already made in all preceding stages.

The definition of the state leads to the following unifying framework for DP.

Principle of Optimality. Future decisions for all future stages constitute an optimal policy regardless of the policy adopted in all preceding stages.

The implementation of the principle of optimality is evident in the computations in Example 12.1-1. In stage 3, the recursive computations at node 7 use the shortest distance to nodes 5 and 6 (i.e., the states of stage 2) without concern about how nodes 5 and 6 are reached from the starting node 1.

The principle of optimality does not address the details of how a subproblem is optimized. The reason is the generic nature of the subproblem. It can be linear or nonlinear, and the number of alternative can be finite or infinite. All the principle of optimality does is "break down" the original problem into more computationally tractable subproblems.

## Aha! Moment: Solving Marriage Problem . . . with Dynamic Programming!

The German mathematician Johannes Kepler (1571-1630), arguably one of the greatest astronomers ever, was faced with a personal problem: He was seeking a compatible spouse and a stepmother for his young children after his wife died. A marriage broker presented him with 11 candidates, and over a span of two years he interviewed them one at a time. He rejected some for lack of compatibility but could not make up his mind regarding the remaining ones, who in turn, tired of waiting, withdrew their names. After much agonized vacillation, he re-wooed the fifth woman he interviewed, and the union was a happy one.

Kepler's problem, initially dubbed as the marriage problem and later as the secretary (selection) problem, generated considerable interest starting in 1960. The solved version posed additional restrictions that were not followed by Kepler himself: Given a pool of $n$ applicants seeking to fill a single position, candidates are interviewed one at a time in random order. Following each interview, an irrevocable decision is made to accept or reject the candidate. Acceptance of a candidate ends the process; otherwise the next candidate, if any, is interviewed. If all the first $n - 1$ candidates have been rejected (or if $n = 1$ ), then candidate $n$ must be accepted.

Finding the best candidate in the pool is complicated by the irrevocable accept/reject decision immediately following each interview. Short of interviewing all $n$ candidates (in which case the absolute best candidate could be determined), a proposed game strategy calls for rejecting the first $r - 1$ candidates ( $r$ is yet to be determined from the solution) and then continuing the interview process, stopping at the first applicant who is better than all the ones rejected. This strategy makes use of previous interviewing experiences in the hope of finding a better (possibly the best) future candidate, and it is more efficient because it could stop short of interviewing all $n$ candidates. One way to optimize the decision problem is to determine the cutoff $r$ that maximizes the probability that a future applicant $i$ is better than the first $\left( {r - 1}\right)$ rejected candidates.

The described problem (and its variants) was solved by dynamic programming. ${}^{1}$ Other solution models include probability theory, linear programming, and Markov chains. ${}^{2}$ The solutions show that the desired probability, defined as $P\left( {r \mid  n}\right)$ , is concave in $r$ and that

$$
P\left( {r \mid  n}\right)  \geq  \max \left\{  {\mathop{\lim }\limits_{{n \rightarrow  \infty }}P\left( {r \mid  n}\right) }\right\}   = \frac{1}{e} = \frac{1}{2.718} \approx  {.37}\text{ , for all }n > 1
$$

This remarkable simple result says that for $r \approx  {.37n} + 1$ , there is at least a notable 37% chance that a future candidate $i \geq  r$ is better than the first $r - 1$ candidates, no matter how large $n$ is.

The proposed solution was actually realized in Kepler's case when he married candidate number 5 (note that ${.37} \times  {11} = {4.07}$ ). In all likelihood, however, the outcome is purely coincidental because Kepler did not quite follow the rules of the proposed problem. Not to mention that, per published accounts, Kepler first tried to woo candidate number 4 but was unsuccessful. Nevertheless, the conjecture is a story worth telling!

### 12.2 FORWARD AND BACKWARD RECURSION

Example 12.1-1 uses forward recursion in which the computations proceed from stage 1 to stage 3. The same example can be solved by backward recursion, starting at stage 3 and ending at stage 1.

Naturally, both the forward and backward recursions yield the same optimum. Although the forward procedure appears more logical, DP literature mostly uses backward recursion. The reason for this preference is that, in general, backward recursion can be more efficient computationally.

We will demonstrate the use of backward recursion by applying it to Example 12.1-1. The demonstration will also provide the opportunity to present the DP computations in a compact tabular form.

## Example 12.2-1

The backward recursive equation for Example 12.2-1 is

$$
{f}_{4}\left( {{x}_{4} = 7}\right)  = 0
$$

$$
{f}_{i}\left( {x}_{i}\right)  = \mathop{\min }\limits_{\substack{\text{ all feasible } \\  \text{ routes }\left( {{x}_{i - 1},{x}_{i}}\right)  }}\left\{  {d\left( {{x}_{i - 1},{x}_{i}}\right)  + {f}_{i - 1}\left( {x}_{i - 1}\right) }\right\}  , i = 1,2,3
$$

The order of computations is ${f}_{3} \rightarrow  {f}_{2} \rightarrow  {f}_{1}$ .

---

${}^{1}$ Beckmann, M.,"Dynamic Programming and the Secretary Problem," Computers and Mathematics with Applications, Vol. 19, No. 11, pp. 25-28, 1990.

${}^{2}$ Thomas S. Ferguson,"Who Solved the Secretary Problem?" Statistical Science, Vol. 4, No. 3, pp. 282-289, 1989. Stable URL: http://www.jstor.org/stable/2245639 accessed 7-29-2015 9:10 P.M.

---

Stage 3. Node $7\left( {{x}_{4} = 7}\right)$ is connected to nodes 5 and 6 $\left( {{x}_{3} = 5}\right.$ and 6 $)$ with exactly one route each. The following table summarizes stage 3 computations:

<table><tr><td rowspan="2">${x}_{3}$</td><td>$d\left( {{x}_{3},{x}_{4}}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{4} = 7$</td><td>${f}_{3}\left( {x}_{3}\right)$</td><td>${x}_{4}^{ * }$</td></tr><tr><td>5</td><td>9</td><td>9</td><td>7</td></tr><tr><td>6</td><td>6</td><td>6</td><td>7</td></tr></table>

Stage 2. Route $\left( {2,6}\right)$ does not exist. Given ${f}_{3}\left( {x}_{3}\right)$ from stage 3, we can compare the feasible alternatives as the following table shows:

<table><tr><td rowspan="2">${x}_{2}$</td><td colspan="2">$d\left( {{x}_{2},{x}_{3}}\right)  + {f}_{3}\left( {x}_{3}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{3} = 5$</td><td>${x}_{3} = 6$</td><td>${f}_{2}\left( {x}_{2}\right)$</td><td>${x}_{3}^{ * }$</td></tr><tr><td>2</td><td>${12} + 9 = {21}$</td><td>-</td><td>21</td><td>5</td></tr><tr><td>3</td><td>$8 + 9 = {17}$</td><td>$9 + 6 = {15}$</td><td>15</td><td>6</td></tr><tr><td>4</td><td>$7 + 9 = {16}$</td><td>${13} + 6 = {19}$</td><td>16</td><td>5</td></tr></table>

The optimum solution of stage 2 reads as follows: For cities 2 and 4, the shortest routes pass through city 5, and for city 3, the shortest route passes through city 6.

Stage 1. From node 1, we have three alternative routes: $\left( {1,2}\right) ,\left( {1,3}\right)$ , and $\left( {1,4}\right)$ . Using ${f}_{2}\left( {x}_{2}\right)$ from stage 2, we get

<table><tr><td rowspan="2">${x}_{1}$</td><td colspan="3">$d\left( {{x}_{1},{x}_{2}}\right)  + {f}_{2}\left( {x}_{2}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{2} = 2$</td><td>${x}_{2} = 3$</td><td>${x}_{2} = 4$</td><td>${f}_{1}\left( {x}_{1}\right)$</td><td>${x}_{2}^{ * }$</td></tr><tr><td>1</td><td>$7 + {21} = {28}$</td><td>$8 + {15} = {23}$</td><td>$5 + {16} = {21}$</td><td>21</td><td>4</td></tr></table>

Stage 1 solution links city 1 to city 4. Next, stage 2 solution links city 4 to city 5. Finally, stage 3 solution connects city 5 to city 7 . The optimum route is $1 \rightarrow  4 \rightarrow  5 \rightarrow  7$ , and the associated distance is 21 miles.

### 12.3 SELECTED DP APPLICATIONS

This section presents four applications, each with a new idea in the implementation of DP. All the examples use the backward recursive equation because of its prevalence in the literature.

As you study each application, pay special attention to the three basic elements of the DP model:

1. Definition of the stages

2. Definition of the alternatives at each stage

3. Definition of the states for each stage

Of the three elements, the definition of the state is usually the most subtle. The applications presented here show that the definition of the state varies depending on the situation being modeled. Nevertheless, as you investigate each application, you will find it helpful to consider the following questions:

1. What relationships bind the stages together?

2. What information is needed to make feasible decisions at the current stage without regard to how the decisions made at the preceding stages have been reached?

You can enhance your understanding of the concept of the state by questioning the validity of the way it is defined here. Try another definition that may appear "more logical" to you, and use it in the recursive computations. You will soon discover that the definitions presented here are correct. Meanwhile, the associated mental process should give you a better understanding of the role of states in the development of DP recursive equation.

#### 12.3.1 Knapsack/Fly-Away Kit/Cargo-Loading Model

The knapsack model classically deals with determining the most valuable items a combat soldier carries in a backpack. The problem represents a general resource allocation model in which limited resources are used by a number of economic activities. The objective is to maximize the total return. ${}^{3}$

The (backward) recursive equation is developed for the general problem of allocating $n$ items to a knapsack with weight capacity $W$ . Let ${m}_{i}$ be the number of units of item $i$ in the knapsack, and define ${r}_{i}$ and ${w}_{i}$ as the unit revenue and weight of item $i$ . The general problem can be represented as

$$
\text{ Maximize }z = {r}_{1}{m}_{1} + {r}_{2}{m}_{2} + \ldots  + {r}_{n}{m}_{n}
$$

subject to

$$
{w}_{1}{m}_{1} + {w}_{2}{m}_{2} + \ldots  + {w}_{n}{m}_{n} \leq  W
$$

$$
{m}_{1},{m}_{2},\ldots ,{m}_{n}\text{ nonnegative integers }
$$

The three elements of the model are

1. Stage $i$ is represented by item $i, i = 1,2,\ldots , n$ .

2. The alternatives at stage $i$ are the number of units of item $i,{m}_{i} = 0,1,\ldots ,\left\lbrack  \frac{W}{{w}_{i}}\right\rbrack$ , where $\left\lbrack  \frac{W}{{w}_{i}}\right\rbrack$ is the largest integer less than or equal to $\frac{W}{{w}_{i}}$ . This definition allows the solution to allocate none, some, or all of the resource $W$ to any of the $m$ items. The return for ${m}_{i}$ is ${r}_{i}{m}_{i}$ .

---

${}^{3}$ The knapsack problem is also known in the literature as the fly-away kit problem (determination of the most valuable items a jet pilot takes on board) and the cargo-loading problem (determination of the most valuable items to be loaded on a navy ship). It appears that the three names were coined to ensure equal representation of three branches of the armed forces: army, air force, and navy!

---

3. The state at stage $i$ is represented by ${x}_{i,}$ the total weight assigned to stages (items) $i, i + 1,\ldots$ , and $n$ . This definition recognizes that the weight limit is the only constraint that binds all $n$ stages. ${}^{4}$

Define

$$
{f}_{i}\left( {x}_{i}\right)  = \text{ maximum return for stages }i, i + 1\text{ , and }n\text{ , given state }{x}_{i}
$$

The most convenient way to construct the recursive equation is a two-step procedure:

Step 1. Express ${f}_{i}\left( {x}_{i}\right)$ as a function of ${f}_{i}\left( {x}_{i + 1}\right)$ as follows:

$$
{f}_{n + 1}\left( {x}_{n + 1}\right)  \equiv  0
$$

$$
\begin{matrix} {f}_{i}\left( {x}_{i}\right)  = \mathop{\min }\limits_{{{m}_{i} = 0,1,\ldots \left\lbrack  \frac{W}{{w}_{i}}\right\rbrack  }}\left\{  {{r}_{i}{m}_{i} + {f}_{i + 1}\left( {x}_{i + 1}\right) }\right\}  ,\;i = 1,2,\ldots , n \\  {x}_{i} \leq  W \end{matrix}
$$

Step 2. Express ${x}_{i + 1}$ as a function of ${x}_{i}$ to ensure consistency with the left-hand side of the recursive equation. By definition, ${x}_{i} - {x}_{i + 1} = {w}_{i}{m}_{i}$ represents the weight used at stage $i$ . Thus, ${x}_{i + 1} = {x}_{i} - {w}_{i}{m}_{i}$ , and the proper recursive equation is given as

$$
{f}_{i}\left( {x}_{i}\right)  = \mathop{\max }\limits_{{{m}_{i} = 0,1,\ldots \left\lbrack  \frac{W}{{w}_{i}}\right\rbrack  }}\left\{  {{r}_{i}{m}_{i} + {f}_{i + 1}\left( {{x}_{i} - {w}_{i}{m}_{i}}\right) }\right\}  , i = 1,2,\ldots , n
$$

$$
{x}_{i} \leq  W
$$

## Example 12.3-1

A 4-ton vessel can be loaded with one or more of three items. The following table gives the unit weight, ${w}_{i}$ , in tons and the unit revenue in thousands of dollars, ${r}_{i}$ , for item $i$ . The goal is to determine the number of units of each item that will maximize the total return.

<table><tr><td>Item $i$</td><td>${w}_{i}$</td><td>${r}_{i}$</td></tr><tr><td>1</td><td>2</td><td>31</td></tr><tr><td>2</td><td>3</td><td>47</td></tr><tr><td>3</td><td>1</td><td>14</td></tr></table>

Because the unit weight ${w}_{i}$ and the maximum weight $W$ are integers, the state ${x}_{i}$ assumes integer values only.

Stage 3. The exact weight to be allocated to stage 3 (item 3) is not known in advance but can assume one of the values $0,1,\ldots$ , and 4 (because $W = 4$ tons and ${w}_{3} = 1$ ton). A value of ${m}_{3}$ is feasible only if ${w}_{3}{m}_{3} \leq  {x}_{3}$ . Thus, all the infeasible values (with ${w}_{3}{m}_{3} > {x}_{3}$ ) are excluded. The revenue for item 3 is ${14}{m}_{3}$ . Thus, the recursive equation for stage 3 is

$$
{f}_{3}\left( {x}_{3}\right)  = \mathop{\min }\limits_{{{m}_{3} = 0,1,\ldots ,4}}\left\{  {{14}{m}_{3}}\right\}
$$

---

${}^{4}$ The definition of the state can be multidimensional. For example, the volume of the knapsack may pose another restriction. In general, a multidimensional state implies more complex stage calculations. See Section 12.4.

---

The following tableau summarizes the computations for stage 3:

<table><tr><td rowspan="2">${x}_{3}$</td><td colspan="5">${14}{m}_{3}$</td><td colspan="2">Optimum solution</td></tr><tr><td>${m}_{3} = 0$</td><td>${m}_{3} = 1$</td><td>${m}_{3} = 2$</td><td>${m}_{3} = 3$</td><td>${m}_{3} = 4$</td><td>${f}_{3}\left( {x}_{3}\right)$</td><td>${m}_{3}^{ * }$</td></tr><tr><td>0</td><td>0</td><td>-</td><td>-</td><td>-</td><td>-</td><td>0</td><td>0</td></tr><tr><td>1</td><td>0</td><td>14</td><td>-</td><td>-</td><td>-</td><td>14</td><td>1</td></tr><tr><td>2</td><td>0</td><td>14</td><td>28</td><td>-</td><td>-</td><td>28</td><td>2</td></tr><tr><td>3</td><td>0</td><td>14</td><td>28</td><td>42</td><td>-</td><td>42</td><td>3</td></tr><tr><td>4</td><td>0</td><td>14</td><td>28</td><td>42</td><td>56</td><td>56</td><td>4</td></tr></table>

Stage 2. $\max \left\{  {m}_{2}\right\}   = \left\lbrack  \frac{4}{3}\right\rbrack   = 1$ , or ${m}_{3} = 0,1,{f}_{2}\left( {x}_{2}\right)  = \mathop{\max }\limits_{{m = 0,1}}\left\{  {{47}{m}_{2} + {f}_{3}\left( {{x}_{2} - 3{m}_{2}}\right) }\right\}$

<table><tr><td rowspan="2">${x}_{2}$</td><td colspan="2">${47}{m}_{2} + {f}_{3}\left( {{x}_{2} - 3{m}_{2}}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${m}_{2} = 0$</td><td>${m}_{2} = 1$</td><td>${f}_{2}\left( {x}_{2}\right)$</td><td>${m}_{2}^{ * }$</td></tr><tr><td>0</td><td>$0 + 0 = 0$</td><td>-</td><td>0</td><td>0</td></tr><tr><td>1</td><td>$0 + {14} = {14}$</td><td>-</td><td>14</td><td>0</td></tr><tr><td>2</td><td>$0 + {28} = {28}$</td><td>-</td><td>28</td><td>0</td></tr><tr><td>3</td><td>$0 + {42} = {42}$</td><td>${47} + 0 = {47}$</td><td>47</td><td>1</td></tr><tr><td>4</td><td>$0 + {56} = {56}$</td><td>${47} + {14} = {61}$</td><td>61</td><td>1</td></tr></table>

Stage 1. $\max \left\{  {m}_{1}\right\}   = \left\lbrack  \frac{4}{2}\right\rbrack   = 2$ or ${m}_{1} = 0,1,2,{f}_{1}\left( {x}_{1}\right)  = \mathop{\max }\limits_{{{m}_{3} = 0,1,2}}\left\{  {{31}{m}_{2} + {f}_{2}\left( {{x}_{1} - 2{m}_{1}}\right) }\right\}$

<table><tr><td rowspan="2">${x}_{1}$</td><td colspan="3">${31}{m}_{1} + {f}_{2}\left( {{x}_{1} - 2{m}_{1}}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${m}_{1} = 0$</td><td>${m}_{1} = 1$</td><td>${m}_{1} = 2$</td><td>${f}_{1}\left( {x}_{1}\right)$</td><td>${m}_{1}^{ * }$</td></tr><tr><td>0</td><td>$0 + 0 = 0$</td><td>-</td><td>-</td><td>0</td><td>0</td></tr><tr><td>1</td><td>$0 + {14} = {14}$</td><td>-</td><td>-</td><td>14</td><td>0</td></tr><tr><td>2</td><td>$0 + {28} = {28}$</td><td>${31} + 0 = {31}$</td><td>-</td><td>31</td><td>1</td></tr><tr><td>3</td><td>$0 + {47} = {47}$</td><td>${31} + {14} = {45}$</td><td>-</td><td>47</td><td>0</td></tr><tr><td>4</td><td>$0 + {61} = {61}$</td><td>${31} + {28} = {59}$</td><td>${62} + 0 = {62}$</td><td>62</td><td>2</td></tr></table>

The optimum solution is determined in the following manner: Given $W = 4$ tons, from stage $1,{x}_{1} = 4$ gives the optimum alternative ${m}_{1}^{ * } = 2 -$ meaning that 2 units of item 1 will be loaded on the vessel. This allocation leaves ${x}_{2} = {x}_{1} - 2{m}_{2}^{ * } = 4 - 2 \times  2 = 0$ for stages 2 and 3. From stage $2,{x}_{2} = 0$ yields ${m}_{2}^{ * } = 0$ , which leaves ${x}_{3} = {x}_{2} - 3{m}_{2} = 0 - 3 \times  0 = 0$ units for stage 3. Next, from stage $3,{x}_{3} = 0$ gives ${m}_{2}^{ * } = 0$ . Thus, the complete optimal solution is ${m}_{1}^{ * } = 2$ , ${m}_{2}^{ * } = 0$ , and ${m}_{3}^{ * } = 0$ . The associated return is ${f}_{1}\left( 4\right)  = \$ {62},{000}$ .

In the table for stage 1, we actually need to compute the row for ${x}_{1} = 4$ only, because this is the last stage to be considered. However, the computations for ${x}_{1} = 0,1,2$ , and 3 are included to allow carrying out sensitivity analysis. For example, what happens if the vessel capacity is 3 tons in place of 4 tons? The new optimum solution can be determined as

$$
\left( {{x}_{1} = 3}\right)  \rightarrow  \left( {{m}_{1}^{ * } = 0}\right)  \rightarrow  \left( {{x}_{2} = 3}\right)  \rightarrow  \left( {{m}_{2}^{ * } = 1}\right)  \rightarrow  \left( {{x}_{3} = 0}\right)  \rightarrow  \left( {{m}_{3}^{ * } = 0}\right)
$$

Thus the optimum is $\left( {{m}_{1}^{ * },{m}_{2}^{ * },{m}_{3}^{ * }}\right)  = \left( {0,1,0}\right)$ , and the optimum revenue is ${f}_{1}\left( 3\right)  = \$ {47},{000}$ .

## Excel Moment

The nature of DP computations makes it impossible to develop a general computer code that can handle all DP problems. Perhaps this explains the persistent absence of commercial DP software.

In this section, we present an Excel-based algorithm for handling a subclass of DP problems: the single-constraint knapsack problem (file excelKnapsack.xls). The algorithm is not data-specific and can handle problems in which an alternative can assume values in the range of 0 to 10.

Figure 12.3 shows the starting screen of the knapsack (backward) DP model. The screen is divided into two sections: The right section (columns Q:V) summarizes the output solution. In the left section (columns A:P), the input data for the current stage appear in rows 3, 4, and 6. Stage computations start at row 7. (Columns H:N are hidden to conserve space.) The input data symbols are self-explanatory. To fit the spreadsheet conveniently on one screen, the maximum feasible value for alternative ${m}_{i}$ at stage $i$ is 10 (cells D6:N6).

Figure 12.4 shows the stage computations generated by the algorithm for Example 12.3-1. The computations are carried out one stage at a time, and the user provides the basic data that drive each stage.

Starting with stage 3, and using the notation and data in Example 12.3-1, the input cells are updated as the following list shows:

<table><tr><td>Cell(s)</td><td>Data</td></tr><tr><td>D3</td><td>Number of stages, $N = 3$</td></tr><tr><td>G3</td><td>Resource limit, $W = 4$</td></tr><tr><td>C4</td><td>Current stage $= 3$</td></tr><tr><td>E4</td><td>${w}_{3} = 1$</td></tr><tr><td>G4</td><td>${r}_{3} = {14}$</td></tr><tr><td>D6:H6</td><td>${m}_{3} = \left( {0,1,2,3,4}\right)$</td></tr></table>

Note that the feasible values of ${m}_{3}$ are $0,1,\ldots$ , and $4\left( { = \left\lbrack  \frac{W}{{w}_{3}}\right\rbrack   = \left\lbrack  \frac{4}{1}\right\rbrack  }\right)$ , as in Example 12.3-1. The spreadsheet automatically checks the validity of the values the user enters and issues self-explanatory messages in row 5: "yes," "no," and "delete."

As stage 3 data are entered and verified, the spreadsheet "comes alive" and generates all the necessary computations of the stage (columns B through P) automatically. The value -1111111 is used to indicate that the corresponding entry is not feasible. The optimum solution $\left( {{f}_{3},{m}_{3}}\right)$ for the stage is given in columns O and P. Column A provides the values of ${f}_{4}$ , which equal 0 for all ${x}_{3}$ because the computations start at stage 3 (you can leave A9:A13 blank or enter zeros).

## FIGURE 12.3

Excel starting screen of the general DP knapsack model (file excelKnapsack.xls)

<table><tr><td>4</td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>0</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td></tr><tr><td>1</td><td colspan="15">Dynamic Programming (Backward) Knapsack Model</td></tr><tr><td>2</td><td colspan="9">Input Data and Stage Calculations</td><td colspan="6">Ouput Solution Summary</td></tr><tr><td>3</td><td colspan="3">Number of stages, N=</td><td></td><td colspan="2">Res. limit, W=</td><td></td><td colspan="2" rowspan="5">Stage Optimum Solution</td><td>X</td><td>f</td><td>m</td><td>✘</td><td>f</td><td>m</td></tr><tr><td>4</td><td colspan="2">Current stage=</td><td></td><td>w=</td><td></td><td>r=</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>5</td><td colspan="3">Are m values correct?</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>6</td><td rowspan="2"></td><td colspan="2">m=</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>7</td><td colspan="2">r*m=</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>8</td><td></td><td colspan="2">w*m=</td><td></td><td></td><td></td><td></td><td>f</td><td>m</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>9</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>10</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table>

Stage 3:

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>0</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td></tr><tr><td>1</td><td colspan="16">Dynamic Programming (Backward) Knapsack Model</td></tr><tr><td>2</td><td colspan="10">Input Data and Stage Calculations</td><td colspan="6">Ouput Solution Summary</td></tr><tr><td>3</td><td colspan="3">Number of stages.N=</td><td>3</td><td colspan="2">Res. limit. W=</td><td>4</td><td></td><td colspan="2" rowspan="5">Stage <br> Optimum <br> Solution</td><td>✘</td><td>f</td><td>m</td><td>✘</td><td>f</td><td>m</td></tr><tr><td>4</td><td colspan="2">Current stage=</td><td>3</td><td>w3=</td><td>1</td><td>r3=</td><td>14</td><td></td><td colspan="3">Stage 3</td><td></td><td></td><td></td></tr><tr><td>5</td><td colspan="3">Are m3 values correct?</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>yes</td><td>0</td><td>0</td><td>0</td><td></td><td></td><td></td></tr><tr><td>6</td><td></td><td colspan="2">m3=</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>1</td><td>14</td><td>1</td><td></td><td></td><td></td></tr><tr><td>7</td><td>Stage4</td><td colspan="2">r3*m3=</td><td>0</td><td>14</td><td>28</td><td>42</td><td>56</td><td>2</td><td>28</td><td>2</td><td></td><td></td><td></td></tr><tr><td>8</td><td>f4</td><td colspan="2">w3*m3=</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>13</td><td>m3</td><td>3</td><td>42</td><td>3</td><td></td><td></td><td></td></tr><tr><td>9</td><td></td><td>x3=</td><td>0</td><td>0</td><td>111111</td><td>111111</td><td>111111</td><td>111111</td><td>0</td><td>0</td><td>4</td><td>56</td><td>4</td><td></td><td></td><td></td></tr><tr><td>10</td><td></td><td>x3=</td><td>1</td><td>0</td><td>14</td><td>111111</td><td>111111</td><td>111111</td><td>14</td><td>1</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>11</td><td></td><td>x3=</td><td>2</td><td>0</td><td>14</td><td>28</td><td>111111</td><td>1111111</td><td>28</td><td>2</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>12</td><td></td><td>x3=</td><td>3</td><td>0</td><td>14</td><td>28</td><td>42</td><td>111111</td><td>42</td><td>3</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>13</td><td></td><td>x3=</td><td>4</td><td>0</td><td>14</td><td>28</td><td>42</td><td>56</td><td>56</td><td>4</td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table>

Stage 2:

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>0</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td></tr><tr><td>1</td><td colspan="16">Dynamic Programming (Backward) Knapsack Model</td></tr><tr><td>2</td><td colspan="10">Input Data and Stage Calculations</td><td colspan="6">Ouput Solution Summary</td></tr><tr><td>3</td><td colspan="3">Number of stages, $N =$</td><td>3</td><td colspan="2">Res. limit, W=</td><td>4</td><td></td><td rowspan="5" colspan="2">Stage <br> Optimum <br> Solution</td><td>✘</td><td>f</td><td>m</td><td>✘</td><td>f</td><td>m</td></tr><tr><td>4</td><td colspan="2">Current stage=</td><td>2</td><td>w2 =</td><td>3</td><td>r2=</td><td>47</td><td></td><td colspan="3">Stage 3</td><td colspan="3">Stage 2</td></tr><tr><td>5</td><td colspan="3">Are m2 values correct?</td><td>yes</td><td>yes</td><td>delete</td><td>delete</td><td>delete</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr><tr><td>6</td><td rowspan="2">Stage3</td><td colspan="2">m2=</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>1</td><td>14</td><td>1</td><td>1</td><td>14</td><td>0</td></tr><tr><td>7</td><td colspan="2">r2*m2=</td><td>0</td><td>47</td><td></td><td></td><td></td><td>2</td><td>28</td><td>2</td><td>2</td><td>28</td><td>0</td></tr><tr><td>8</td><td>f3</td><td colspan="2">w2*m2=</td><td>0</td><td>3</td><td></td><td></td><td></td><td>f2</td><td>m2</td><td>3</td><td>42</td><td>3</td><td>3</td><td>47</td><td>1</td></tr><tr><td>9</td><td>0</td><td>x2=</td><td>0</td><td>0</td><td>111111</td><td></td><td></td><td></td><td>0</td><td>0</td><td>4</td><td>56</td><td>4</td><td>4</td><td>61</td><td>1</td></tr><tr><td>10</td><td>14</td><td>x2=</td><td>1</td><td>14</td><td>111111</td><td></td><td></td><td></td><td>14</td><td>0</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>11</td><td>28</td><td>x2=</td><td>2</td><td>28</td><td>111111</td><td></td><td></td><td></td><td>28</td><td>0</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>12</td><td>42</td><td>x2=</td><td>3</td><td>42</td><td>47</td><td></td><td></td><td></td><td>47</td><td>1</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>13</td><td>56</td><td>x2=</td><td>4</td><td>56</td><td>61</td><td></td><td></td><td></td><td>61</td><td>1</td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table>

Stage 1:

<table><tr><td>清</td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td>F</td><td>G</td><td>H</td><td>0</td><td>P</td><td>Q</td><td>R</td><td>S</td><td>T</td><td>U</td><td>V</td></tr><tr><td>1</td><td colspan="16">Dynamic Programming (Backward) Knapsack Model</td></tr><tr><td>2</td><td colspan="10">Input Data and Stage Calculations</td><td colspan="6">Ouput Solution Summary</td></tr><tr><td>3</td><td colspan="3">Number of stages, N=</td><td>3</td><td colspan="2">Res. limit, W=</td><td>4</td><td></td><td colspan="2" rowspan="5">Stage <br> Optimum <br> Solution</td><td>✘</td><td>f</td><td>m</td><td>✘</td><td>f</td><td>m</td></tr><tr><td>4</td><td colspan="2">Current stage=</td><td>1</td><td>w1=</td><td>2</td><td>r1=</td><td>31</td><td></td><td colspan="3">Stage 3</td><td colspan="3">Stage 2</td></tr><tr><td>5</td><td colspan="3">Are m1 values correct?</td><td>yes</td><td>yes</td><td>yes</td><td>delete</td><td>delete</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td><td>0</td></tr><tr><td>6</td><td rowspan="2">Stage2</td><td colspan="2">m1=</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>1</td><td>14</td><td>1</td><td>1</td><td>14</td><td>0</td></tr><tr><td>7</td><td colspan="2">r1*m1=</td><td>0</td><td>31</td><td>62</td><td></td><td></td><td>2</td><td>28</td><td>2</td><td>2</td><td>28</td><td>0</td></tr><tr><td>8</td><td>f2</td><td colspan="2">w1*m1=</td><td>0</td><td>2</td><td>4</td><td></td><td></td><td>f1</td><td>m1</td><td>3</td><td>42</td><td>3</td><td>3</td><td>47</td><td>1</td></tr><tr><td>9</td><td>0</td><td>x1=</td><td>0</td><td>0</td><td>111111</td><td>1111111</td><td></td><td></td><td>0</td><td>0</td><td>4</td><td>56</td><td>4</td><td>4</td><td>61</td><td>1</td></tr><tr><td>10</td><td>14</td><td>x1=</td><td>1</td><td>14</td><td>111111</td><td>111111</td><td></td><td></td><td>14</td><td>0</td><td></td><td></td><td></td><td colspan="3">Stage 1</td></tr><tr><td>11</td><td>26</td><td>x1=</td><td>2</td><td>28</td><td>31</td><td>111111</td><td></td><td></td><td>31</td><td>1</td><td></td><td></td><td></td><td>0</td><td>0</td><td>0</td></tr><tr><td>12</td><td>47</td><td>x1=</td><td>3</td><td>47</td><td>45</td><td>111111</td><td></td><td></td><td>47</td><td>0</td><td></td><td></td><td></td><td>1</td><td>14</td><td>0</td></tr><tr><td>13</td><td>61</td><td>x1=</td><td>4</td><td>61</td><td>59</td><td>62</td><td></td><td></td><td>62</td><td>2</td><td></td><td></td><td></td><td>2</td><td>31</td><td>1</td></tr><tr><td>14</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>3</td><td>47</td><td>0</td></tr><tr><td>15</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td>62</td><td>2</td></tr></table>

FIGURE 12.4

Excel DP model for the knapsack problem of Example 12.3-1 (file excelKnapsack.xls)

Now that stage 3 calculations are complete, take the following steps to create a permanent record of the optimal solution of the current stage and to prepare the spreadsheet for next stage:

Step 1. Copy the ${x}_{3}$ -values, C9:C13, and paste them in Q5:Q9 in the optimum solution summary section. Next, copy the $\left( {{f}_{3},{m}_{3}}\right)$ -values, O9:P13, and paste them in R5:S9. Remember that you need to paste values only, which requires selecting Paste Special from Edit menu and Values from the dialogue box.

Step 2. Copy the ${f}_{3}$ -values in R5:R9, and paste them in A9:A13 (you do not need Paste Special in this step).

Step 3. Change cell C4 to 2, and enter the new values of ${w}_{2},{r}_{2}$ , and ${m}_{2}$ for stage 2.

Step 2 places ${f}_{i + 1}\left( {{x}_{i} - {w}_{i}{m}_{i}}\right)$ in column A in preparation for calculating ${f}_{i}\left( {x}_{i}\right)$ at stage $i$ (see the recursive formula for the knapsack problem in Example 12.3-1). A similar procedure is repeated for stage 1. When stage 1 is complete, the solution summary can be used to read the optimum solution, as was explained in Example 12.3-1. Note that the organization of the output solution summary area (columns Q:V) is free formatted, and you can organize its contents in any manner you desire.

#### 12.3.2 Workforce Size Model

Labor needs in construction projects can be met through hiring and firing of workers. Both activities incur cost. The goal is to minimize the total cost of labor needed for the project.

Assume that the duration of the project is $n$ weeks and that the minimum labor force required in week $i$ is ${b}_{i}$ workers. The model assumes that additional cost is incurred if a week's workforce exceeds the minimum requirement or if additional hiring takes place in a week. For simplicity, no cost is incurred when firing takes place.

The cost of maintaining a workforce ${x}_{i}$ larger than the minimum ${b}_{i}$ in week $i$ incurs excess cost ${C}_{1}\left( {{x}_{i} - {b}_{i}}\right)$ . If ${x}_{i} > {x}_{i - 1}$ , hiring occurs at the additional cost of ${C}_{2}\left( {{x}_{i} - {x}_{i - 1}}\right)$ .

The elements of the DP model are defined as follows:

1. Stage $i$ is represented by week $i, i = 1,2,\ldots , n$ .

2. The alternatives at stage $i$ are ${x}_{i}$ , the number of laborers in week $i$ .

3. The state at stage $i$ is ${x}_{i - 1}$ , the number of laborers available in week $i - 1$ .

The DP recursive equation is given as

$$
{f}_{n + 1}\left( {x}_{n}\right)  \equiv  0
$$

$$
{f}_{i}\left( {x}_{i - 1}\right)  = \mathop{\min }\limits_{{{x}_{i} \geq  {b}_{i}}}\left\{  {{C}_{1}\left( {{x}_{i} - {b}_{i}}\right)  + {C}_{2}\left( {{x}_{i} - {x}_{i - 1}}\right)  + {f}_{i + 1}\left( {x}_{i}\right) }\right\}  , i = 1,2,\ldots , n
$$

The computations start at stage $n$ and terminate at stage 1 .

## Example 12.3-2

A contractor estimates that the size of the workforce needed over the next 5 weeks is 5, 7, 8, 4, and 6 workers, respectively. Excess labor kept on the force will cost \$300 per worker per week, and new hiring in any week will incur a fixed cost of \$400 plus \$200 per worker per week.

The data of the problem are

$$
{b}_{1} = 5,{b}_{2} = 7,{b}_{3} = 8,{b}_{4} = 4,{b}_{5} = 6
$$

$$
{C}_{1}\left( {{x}_{i} - {b}_{i}}\right)  = 3\left( {{x}_{i} - {b}_{i}}\right) ,{x}_{i} > {b}_{i}, i = 1,2,\ldots ,5
$$

$$
{C}_{2}\left( {{x}_{i} - {x}_{i - 1}}\right)  = 4 + 2\left( {{x}_{i} - {x}_{i - 1}}\right) ,{x}_{i} > {x}_{i - 1}, i = 1,2,\ldots ,5
$$

The cost functions ${C}_{1}$ and ${C}_{2}$ are in hundreds of dollars.

Stage 5. $\left( {{b}_{5} = 6}\right)$

<table><tr><td rowspan="2">${x}_{4}$</td><td>${C}_{1}\left( {{x}_{5} - 6}\right)  + {C}_{2}\left( {{x}_{5} - {x}_{4}}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{5} = 6$</td><td>${f}_{5}\left( {x}_{4}\right)$</td><td>${x}_{5}^{ * }$</td></tr><tr><td>4</td><td>$3\left( 0\right)  + 4 + 2\left( 2\right)  = 8$</td><td>8</td><td>6</td></tr><tr><td>5</td><td>$3\left( 0\right)  + 4 + 2\left( 1\right)  = 6$</td><td>6</td><td>6</td></tr><tr><td>6</td><td>$3\left( 0\right)  + 0 \; = 0$</td><td>0</td><td>6</td></tr></table>

Stage 4. $\left( {{b}_{4} = 4}\right)$

<table><tr><td rowspan="2">${x}_{3}$</td><td colspan="3">${C}_{1}\left( {{x}_{4} - 4}\right)  + {C}_{2}\left( {{x}_{4} - {x}_{3}}\right)  + {f}_{5}\left( {x}_{4}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{4} = 4$</td><td>${x}_{4} = 5$</td><td>${x}_{4} = 6$</td><td>${f}_{4}\left( {x}_{3}\right)$</td><td>${x}_{4}^{ * }$</td></tr><tr><td>8</td><td>$3\left( 0\right)  + 0 + 8 = 8$</td><td>$3\left( 1\right)  + 0 + 6 = 9$</td><td>$3\left( 2\right)  + 0 + 0 = 6$</td><td>6</td><td>6</td></tr></table>

Stage 3. $\left( {{b}_{3} = 8}\right)$

<table><tr><td rowspan="2">${x}_{2}$</td><td>${C}_{1}\left( {{x}_{3} - 8}\right)  + {C}_{2}\left( {{x}_{3} - {x}_{2}}\right)  + {f}_{4}\left( {x}_{3}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{3} = 8$</td><td>${f}_{3}\left( {x}_{2}\right)$</td><td>${x}_{6}^{ * }$</td></tr><tr><td>7</td><td>$3\left( 0\right)  + 4 + 2\left( 1\right)  + 6 = {12}$</td><td>12</td><td>8</td></tr><tr><td>8</td><td>$3\left( 0\right)  + 0 \; + 6 = 6$</td><td>6</td><td>8</td></tr></table>

Stage 2. $\left( {{b}_{2} = 7}\right)$

<table><tr><td rowspan="2">${x}_{1}$</td><td colspan="2">${C}_{1}\left( {{x}_{2} - 7}\right)  + {C}_{2}\left( {{x}_{3} - {x}_{2}}\right)  + {f}_{3}\left( {x}_{2}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{2} = 7$</td><td>${x}_{2} = 8$</td><td>${f}_{2}\left( {x}_{1}\right)$</td><td>${x}_{2}^{ * }$</td></tr><tr><td>5</td><td>$3\left( 0\right)  + 4 + 2\left( 2\right)  + {12} = {20}$</td><td>$3\left( 1\right)  + 4 + 2\left( 3\right)  + 6 = {19}$</td><td>19</td><td>8</td></tr><tr><td>6</td><td>$3\left( 0\right)  + 4 + 2\left( 1\right)  + {12} = {18}$</td><td>$3\left( 1\right)  + 4 + 2\left( 2\right)  + 6 = {17}$</td><td>17</td><td>8</td></tr><tr><td>7</td><td>$3\left( 0\right)  + 0 \; + {12} = {12}$</td><td>$3\left( 1\right)  + 4 + 2\left( 1\right)  + 6 = {15}$</td><td>12</td><td>7</td></tr><tr><td>8</td><td>$3\left( 0\right)  + 0 \; + {12} = {12}$</td><td>$3\left( 1\right)  + 0 \; + 6 = 9$</td><td>9</td><td>8</td></tr></table>

Stage 1. $\left( {{b}_{1} = 5}\right)$

<table><tr><td rowspan="2">${x}_{0}$</td><td colspan="4">${C}_{1}\left( {{x}_{1} - 5}\right)  + {C}_{2}\left( {{x}_{1} - {x}_{0}}\right)  + {f}_{2}\left( {x}_{1}\right)$</td><td colspan="2">Optimum solution</td></tr><tr><td>${x}_{1} = 5$</td><td>${x}_{1} = 6$</td><td>${x}_{1} = 7$</td><td>${x}_{1} = 8$</td><td>${f}_{1}\left( {x}_{0}\right)$</td><td>${x}_{1}^{ * }$</td></tr><tr><td>0</td><td>$3\left( 0\right)  + 4 + 2\left( 5\right)$ <br> $+ {19} = {33}$</td><td>$3\left( 1\right)  + 4 + 2\left( 6\right)$ <br> $+ {17} = {36}$</td><td>$3\left( 2\right)  + 4 + 2\left( 7\right)$ <br> $+ {12} = {36}$</td><td>$3\left( 2\right)  + 4 + 2\left( 8\right)$ <br> $+ 9 = {35}$</td><td>33</td><td>5</td></tr></table>

The optimum solution is determined as

$$
{x}_{0} = 0 \rightarrow  {x}_{1}^{ * } = 5 \rightarrow  {x}_{2}^{ * } = 8 \rightarrow  {x}_{3}^{ * } = 8 \rightarrow  {x}_{4}^{ * } = 6 \rightarrow  {x}_{5}^{ * } = 6
$$

The solution can be translated to the following plan:

<table><tr><td>Week $i$</td><td>Minimum labor force $\left( {b}_{\mathrm{i}}\right)$</td><td>Actual labor force $\left( {x}_{\mathrm{i}}\right)$</td><td>Decision</td><td>Cost</td></tr><tr><td>1</td><td>5</td><td>5</td><td>Hire 5 workers</td><td>$4 + 2 \times  5 = {14}$</td></tr><tr><td>2</td><td>7</td><td>8</td><td>Hire 3 workers</td><td>$4 + 2 \times  3 + 1 \times  3 = {13}$</td></tr><tr><td>3</td><td>8</td><td>8</td><td>No change</td><td>0</td></tr><tr><td>4</td><td>4</td><td>6</td><td>Fire 2 workers</td><td>$3 \times  2 = 6$</td></tr><tr><td>5</td><td>6</td><td>6</td><td>No change</td><td>0</td></tr></table>

The total cost is ${f}_{1}\left( 0\right)  = \$ {3300}$ .

#### 12.3.3 Equipment Replacement Model

Machines that stay longer in service incur higher maintenance cost and may be replaced after a number of years in operation. The situation deals with determining the most economical age of a machine.

Suppose that the machine replacement problem spans $n$ years. At the start of each year, a machine is either kept in service an extra year or replaced with a new one. Let $r\left( t\right) , c\left( t\right)$ , and $s\left( t\right)$ represent the yearly revenue, operating cost, and salvage value, respectively, of a $t$ -year-old machine. The cost of acquiring a new machine in any year is $I$ .

The elements of the DP model are as follows:

1. Stage $i$ is represented by year $i, i = 1,2,\ldots , n$ .

2. The alternatives at stage (year) $i$ are keep (K) or replace (R) the machine at the start of year $i$ .

3. The state at stage $i$ is the age of the machine at the start of year $i$ .

Given that the machine is $t$ years old at the start of year $i$ , define

${f}_{i}\left( t\right)  =$ maximum net income for years $i, i + 1,\ldots$ , and $n$

The recursive equation is

$$
{f}_{n}\left( t\right)  = \max \left\{  \begin{array}{ll} r\left( t\right)  - c\left( t\right)  + s\left( {t + 1}\right) , & \text{ if KEEP } \\  r\left( 0\right)  + s\left( t\right)  + s\left( 1\right)  - I - c\left( 0\right) , & \text{ if REPLACE } \end{array}\right.
$$

$$
{f}_{i}\left( t\right)  = \max \left\{  \begin{array}{ll} r\left( t\right)  - c\left( t\right)  + {f}_{i + 1}\left( {t + 1}\right) , & \text{ if KEEP } \\  r\left( 0\right)  + s\left( t\right)  - I - c\left( 0\right)  + {f}_{i + 1}\left( 1\right) , & \text{ if REPLACE } \end{array}\right\}  , i = 1,2,\ldots , n - 1
$$

## Example 12.3-3

A company needs to determine the optimal replacement policy for a current 3-year-old machine over the next 4 years $\left( {n = 4}\right)$ . A 6-year-old machine must be replaced. The cost of a new machine is \$100,000. The following table gives the data of the problem:

<table><tr><td>Age, $t$ (yr)</td><td>Revenue, $r\left( t\right) \left( \$ \right)$</td><td>Operating cost, $c\left( t\right) \left( \$ \right)$</td><td>Salvage value, $s\left( t\right) \left( \$ \right)$</td></tr><tr><td>0</td><td>20,000</td><td>200</td><td>-</td></tr><tr><td>1</td><td>19,000</td><td>600</td><td>80,000</td></tr><tr><td>2</td><td>18,500</td><td>1200</td><td>60,000</td></tr><tr><td>3</td><td>17,200</td><td>1500</td><td>50,000</td></tr><tr><td>4</td><td>15,500</td><td>1700</td><td>30,000</td></tr><tr><td>5</td><td>14,000</td><td>1800</td><td>10,000</td></tr><tr><td>6</td><td>12,200</td><td>2200</td><td>5000</td></tr></table>

The determination of the feasible values for the age of the machine at each stage is somewhat tricky. Figure 12.5 summarizes the network representing the problem. At the start of year 1, we have a 3-year-old machine. We can either replace it $\left( R\right)$ or keep it $\left( K\right)$ for another year. If replacement occurs, the new machine will be 1 year old at the start of year 2; otherwise, the kept machine will be 4 years old. The same logic applies at the start of years 2 to 4. If a 1-year-old machine is replaced at the start of years 2, 3, and 4, its replacement will be 1 year old at the start of the following year. Also, at the start of year 4, a 6-year-old machine must be replaced, and at the end of year 4 (end of the planning horizon), we salvage $\left( S\right)$ the machine.

The network shows that at the start of year 2, the possible ages of the machine are 1 and 4 years. For the start of year 3, the possible ages are 1, 2, and 5 years, and for the start of year 4, the possible ages are 1, 2, 3, and 6 years. The network also assumes that the machine will be salvaged at the start of year 5 regardless of age.

FIGURE 12.5

Representation of machine age as a function of decision year in Example 12.3-3

![bo_d56m4vjef24c73bhe620_14_391_1302_1184_871_0.jpg](bo_d56m4vjef24c73bhe620_14_391_1302_1184_871_0.jpg)

The solution of the network in Figure 12.5 is equivalent to finding the longest route (i.e., maximum revenue) from the start of year 1 to the end of year 4. We will use the tabular form to solve the problem. All values are in thousands of dollars. Note that if a machine is replaced in year 4 (i.e., end of the planning horizon), its revenue will include the salvage value, $s\left( t\right)$ , of the replaced machine and the salvage value, $s\left( 1\right)$ , of the replacement machine. Also, if in year 4 a machine of age $t$ is kept, its salvage value will be $s\left( {t + 1}\right)$ .

Stage 4.

<table><tr><td rowspan="2">$t$</td><td>$K$</td><td>$R$</td><td colspan="2">Optimum solution</td></tr><tr><td>$r\left( t\right)  + s\left( {t + 1}\right)  - c\left( t\right)$</td><td>$r\left( 0\right)  + s\left( t\right)  + s\left( 1\right)  - c\left( 0\right)  - I$</td><td>${f}_{4}\left( t\right)$</td><td>Decision</td></tr><tr><td>1</td><td>${19.0} + {60} - {.6} = {78.4}$</td><td>${20} + {80} + {80} - {.2} - {100} = {79.8}$</td><td>79.8</td><td>$R$</td></tr><tr><td>2</td><td>${18.5} + {50} - {1.2} = {67.3}$</td><td>${20} + {60} + {80} - {.2} - {100} = {59.8}$</td><td>67.3</td><td>$K$</td></tr><tr><td>3</td><td>${17.2} + {30} - {1.5} = {45.7}$</td><td>${20} + {50} + {80} - {.2} - {100} = {49.8}$</td><td>49.8</td><td>$R$</td></tr><tr><td>6</td><td>(Must replace)</td><td>${20} + 5 + {80} - {.2} - {100} = {4.8}$</td><td>4.8</td><td>$R$</td></tr></table>

Stage 3.

<table><tr><td rowspan="2">$t$</td><td>$K$</td><td>$R$</td><td colspan="2">Optimum solution</td></tr><tr><td>$r\left( t\right)  - c\left( t\right)  + {f}_{4}\left( {t + 1}\right)$</td><td>$r\left( 0\right)  + s\left( t\right)  - c\left( 0\right)  - I + {f}_{4}\left( 1\right)$</td><td>${f}_{3}\left( t\right)$</td><td>Decision</td></tr><tr><td>1</td><td>${19.0} - {.6} + {67.3} = {85.7}$</td><td>${20} + {80} - {.2} - {100} + {79.8} = {79.6}$</td><td>85.7</td><td>$K$</td></tr><tr><td>2</td><td>${18.5} - {1.2} + {49.8} = {67.1}$</td><td>${20} + {60} - {.2} - {100} + {79.8} = {59.6}$</td><td>67.1</td><td>$K$</td></tr><tr><td>5</td><td>${14.0} - {1.8} + {4.8} = {17.0}$</td><td>${20} + {10} - {.2} - {100} + {79.8} = {9.6}$</td><td>17.0</td><td>$R$</td></tr></table>

Stage 2.

<table><tr><td rowspan="2">$t$</td><td>$K$</td><td>$R$</td><td colspan="2">Optimum solution</td></tr><tr><td>$r\left( t\right)  - c\left( t\right)  + {f}_{3}\left( {t + 1}\right)$</td><td>$R\left( 0\right)  + s\left( t\right)  - c\left( 0\right)  - I + {f}_{3}\left( 1\right)$</td><td>${f}_{2}\left( t\right)$</td><td>Decision</td></tr><tr><td>1</td><td>19.0 - .6 + 67.1 = 85.5</td><td>${20} + {80} - {.2} - {100} + {85.7} = {85.5}$</td><td>85.5</td><td>$K$ or $R$</td></tr><tr><td>4</td><td>15.5 - 1.7 + 17.0 = 30.8</td><td>${20} + {30} - {.2} - {100} + {85.7} = {35.5}$</td><td>35.5</td><td>$R$</td></tr></table>

Stage 1.

<table><tr><td></td><td>$K$</td><td>$R$</td><td colspan="2">Optimum solution</td></tr><tr><td>$t$</td><td>$r\left( t\right)  - c\left( t\right)  + {f}_{2}\left( {t + 1}\right)$</td><td>$R\left( 0\right)  + s\left( t\right)  - c\left( 0\right)  - I + {f}_{2}\left( 1\right)$</td><td>${f}_{1}\left( t\right)$</td><td>Decision</td></tr><tr><td>3</td><td>17.2 - 1.5 + 35.5 = 51.2</td><td>${20} + {50} - {.2} - {100} + {85.5} = {55.3}$</td><td>55.3</td><td>$R$</td></tr></table>

Figure 12.6 summarizes the optimal solution. At the start of year 1, given $t = 3$ , the optimal decision is to replace the machine. Thus, the new machine will be 1 year old at the start of year 2, and $t = 1$ at the start of year 2 calls for either keeping or replacing the machine. If it is replaced, the new machine will be 1 year old at the start of year 3; otherwise, the kept machine will be 2 years old. The process is continued in this manner until year 4 is reached.

![bo_d56m4vjef24c73bhe620_16_462_197_1030_294_0.jpg](bo_d56m4vjef24c73bhe620_16_462_197_1030_294_0.jpg)

FIGURE 12.6

Solution of Example 12.3-3

The alternative optimal policies starting in year 1 are $\left( {R, K, K, R}\right)$ and $\left( {R, R, K, K}\right)$ . The total cost is \$55,300.

#### 12.3.4 Investment Model

Suppose that you want to invest the amounts ${P}_{1},{P}_{2},\ldots ,{P}_{n}$ at the start of each of the next $n$ years. You have two investment opportunities in two banks: First Bank pays an interest rate ${r}_{1}$ , and Second Bank pays ${r}_{2}$ , both compounded annually. To encourage deposits, both banks pay bonuses on new investments in the form of a percentage of the amount invested. The respective bonus percentages for First Bank and Second Bank are ${q}_{i1}$ and ${q}_{i2}$ for year $i$ . Bonuses are paid at the end of the year in which the investment is made and may be reinvested in either bank in the immediately succeeding year. This means that only bonuses and fresh new money may be invested in either bank. However, once an investment is deposited, it must remain in the bank until the end of year $n$ .

The elements of the DP model are as follows:

1. Stage $i$ is represented by year $i, i = 1,2,\ldots , n$ .

2. The alternatives at stage $i$ are ${I}_{i}$ and ${\bar{I}}_{i}$ , the amounts invested in First Bank and Second Bank, respectively.

3. The state, ${x}_{i}$ , at stage $i$ is the amount of capital available for investment at the start of year $i$ .

We note that ${\bar{I}}_{i} = {x}_{i} - {I}_{i}$ by definition. Thus

$$
{x}_{1} = {P}_{1}
$$

$$
{x}_{i} = {P}_{i} + {q}_{i - 1,1}{I}_{i - 1} + {q}_{i - 1,2}\left( {{x}_{i - 1} - {I}_{i - 1}}\right)
$$

$$
= {P}_{i} + \left( {{q}_{i - 1,1} - {q}_{i - 1,2}}\right) {I}_{i - 1} + {q}_{i - 1,2}{x}_{i - 1}, i = 2,3,\ldots , n
$$

The reinvestment amount ${x}_{i}$ includes only new money plus any bonus from investments made in year $i - 1$ .

Define

${f}_{i}\left( {x}_{i}\right)  =$ optimal value of the investments for years $i, i + 1,\ldots$ , and $n$ , given ${x}_{i}$

Next, define ${s}_{i}$ as the accumulated sum at the end of year $n$ , given that ${I}_{i}$ and $\left( {{x}_{i} - {I}_{i}}\right)$ are the investments made in year $i$ in First Bank and Second Bank, respectively. Letting ${\alpha }_{k} = \left( {1 + {r}_{k}}\right) , k = 1,2$ , the problem can be stated as

$$
\text{ Maximize }z = {s}_{1} + {s}_{2} + \ldots  + {s}_{n}
$$

where

$$
{s}_{i} = {I}_{i}{\alpha }_{1}^{n + 1 - i} + \left( {{x}_{i} - {I}_{i}}\right) {\alpha }_{2}^{n + 1 - i}
$$

$$
= \left( {{\alpha }_{1}^{n + 1 - i} - {\alpha }_{2}^{n + 1 - i}}\right) {I}_{i} + {\alpha }_{2}^{n + 1 - i}{x}_{i}, i = 1,2,\ldots , n - 1
$$

$$
{s}_{n} = \left( {{\alpha }_{1} + {q}_{n1} - {\alpha }_{2} - {q}_{n2}}\right) {I}_{n} + \left( {{\alpha }_{2} + {q}_{n2}}\right) {x}_{n}
$$

The terms ${q}_{n1}$ and ${q}_{n2}$ in ${s}_{n}$ are added because the bonuses for year $n$ are part of the final accumulated sum of money from the investment.

The backward DP recursive equation is thus given as

$$
{f}_{n + 1}\left( {x}_{n + 1}\right)  \equiv  0
$$

$$
{f}_{i}\left( {x}_{i}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{i} \leq  {x}_{i}}}\left\{  {{s}_{i} + {f}_{i + 1}\left( {x}_{i + 1}\right) }\right\}  , i = 1,2,\ldots , n - 1
$$

As given previously, ${x}_{i + 1}$ is defined in terms of ${x}_{i}$ .

## Example 12.3-4

Suppose that you want to invest \$4000 now and \$2000 at the start of years 2 to 4 . The interest rate offered by First Bank is 8% compounded annually, and the bonuses over the next 4 years are 1.8%, 1.7%, 2.1%, and 2.5%, respectively. The annual interest rate offered by Second Bank is .2% lower than that of First Bank, but its bonus is .5% higher. The objective is to maximize the accumulated capital at the end of 4 years.

Using the notation introduced previously, we have

$$
{P}_{1} = \$ 4,{000},{P}_{2} = {P}_{3} = {P}_{4} = \$ {2000}
$$

$$
{\alpha }_{1} = \left( {1 + {.08}}\right)  = {1.08}
$$

$$
{\alpha }_{2} = \left( {1 + {.078}}\right)  = {1.078}
$$

$$
{q}_{11} = {.018},{q}_{21} = {.017},{q}_{31} = {.021},{q}_{41} = {.025}
$$

$$
{q}_{12} = {.023},{q}_{22} = {.022},{q}_{32} = {.026},{q}_{42} = {.030}
$$

Stage 4.

$$
{f}_{4}\left( {x}_{4}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{4} \leq  {x}_{4}}}\left\{  {s}_{4}\right\}
$$

where

$$
{s}_{4} = \left( {{\alpha }_{1} + {q}_{41} - {\alpha }_{2} - {q}_{42}}\right) {I}_{4} + \left( {{\alpha }_{2} + {q}_{42}}\right) {x}_{4} =  - {.003}{I}_{4} + {1.108}{x}_{4}
$$

The function ${s}_{4}$ is linear in ${I}_{4}$ in the range $0 \leq  {I}_{4} \leq  {x}_{4}$ , and its maximum occurs at ${I}_{4} = 0$ because of the negative coefficient of ${I}_{4}$ . Thus, the optimum solution for stage 5 can be summarized as

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{4}\left( {x}_{4}\right)$</td><td>${I}_{4}^{ * }$</td></tr><tr><td>${x}_{4}$</td><td>${1.108}{x}_{4}$</td><td>0</td></tr></table>

Stage 3.

$$
{f}_{3}\left( {x}_{3}\right)  = \mathop{\max }\limits_{{0 \leq  {l}_{3} \leq  {x}_{3}}}\left\{  {{s}_{3} + {f}_{4}\left( {x}_{4}\right) }\right\}
$$

where

$$
{s}_{3} = \left( {{1.08}^{2} - {1.078}^{2}}\right) {I}_{3} + {1.078}^{2}{x}_{3} = {.00432}{I}_{3} + {1.1621}{x}_{3}
$$

$$
{x}_{4} = {2000} - {.005}{I}_{3} + {.026}{x}_{3}
$$

Thus,

$$
{f}_{3}\left( {x}_{3}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{3} \leq  {x}_{3}}}\left\{  {{.00432}{I}_{3} + {1.1621}{x}_{3} + {1.108}\left( {{2000} - {.005}{I}_{3} + {0.026}{x}_{3}}\right\}  }\right.
$$

$$
= \mathop{\max }\limits_{{0 \leq  {I}_{3} \leq  {x}_{3}}}\left\{  {{2216} - {.00122}{I}_{3} + {1.1909}{x}_{3}}\right\}
$$

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{3}\left( {x}_{3}\right)$</td><td>${I}_{3}^{ * }$</td></tr><tr><td>${x}_{3}$</td><td>${2216} + {1.1909}{x}_{3}$</td><td>0</td></tr></table>

Stage 2.

$$
{f}_{2}\left( {x}_{2}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{2} \leq  {x}_{2}}}\left\{  {{s}_{2} + {f}_{3}\left( {x}_{3}\right) }\right\}
$$

where

$$
{s}_{2} = \left( {{1.08}^{3} - {1.078}^{3}}\right) {I}_{2} + {1.078}^{3}{x}_{2} = {.006985}{I}_{2} + {1.25273}{x}_{2}
$$

$$
{x}_{3} = {2000} - {.005}{I}_{2} + {.022}{x}_{2}
$$

Thus,

$$
{f}_{2}\left( {x}_{2}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{2} \leq  {x}_{2}}}\left\{  {{.006985}{I}_{2} + {1.25273}{x}_{2} + {2216} + {1.1909}\left( {{2000} - {.005}{I}_{2} + {.022}{x}_{2}}\right) }\right\}
$$

$$
= \mathop{\max }\limits_{{0 \leq  {I}_{2} \leq  {x}_{2}}}\left\{  {{4597.8} + {.0010305}{I}_{2} + {1.27893}{x}_{2}}\right\}
$$

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{2}\left( {x}_{2}\right)$</td><td>${I}_{2}^{ * }$</td></tr><tr><td>${x}_{2}$</td><td>${4597.8} + {1.27996}{x}_{2}$</td><td>${x}_{2}$</td></tr></table>

Stage 1.

$$
{f}_{1}\left( {x}_{1}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{1} \leq  {x}_{1}}}\left\{  {{s}_{1} + {f}_{2}\left( {x}_{2}\right) }\right\}
$$

where

$$
{s}_{1} = \left( {{1.08}^{4} - {1.078}^{4}}\right) {I}_{1} + {1.078}^{4}{x}_{1} = {.01005}{I}_{2} + {1.3504}{x}_{1}
$$

$$
{x}_{2} = {2000} - {.005}{I}_{1} + {.023}{x}_{1}
$$

Thus,

$$
{f}_{1}\left( {x}_{1}\right)  = \mathop{\max }\limits_{{0 \leq  {I}_{1} \leq  {x}_{1}}}\left\{  {{.01005}{I}_{1} + {1.3504}{x}_{1} + {4597.8} + {1.27996}\left( {{2000} - {.005}{I}_{1} + {.023}{x}_{1}}\right) }\right\}
$$

$$
= \mathop{\max }\limits_{{0 \leq  {I}_{1} \leq  {x}_{1}}}\left\{  {{7157.7} + {.00365}{I}_{1} + {1.37984}{x}_{1}}\right\}
$$

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{1}\left( {x}_{1}\right)$</td><td>${I}_{1}^{ * }$</td></tr><tr><td>${x}_{1} = \$ {4000}$</td><td>7157.7 + 1.38349 ${x}_{1}$</td><td>\$4,000</td></tr></table>

Working backward and noting that ${I}_{1}^{ * } = {4000},{I}_{2}^{ * } = {x}_{2},{I}_{3}^{ * } = {I}_{4}^{ * } = 0$ , we get

$$
{x}_{1} = {4000}
$$

$$
{x}_{2} = {2000} - {.005} \times  {4000} + {.023} \times  {4000} = \$ {2072}
$$

$$
{x}_{3} = {2000} - {.005} \times  {2072} + {.022} \times  {2072} = \$ {2035.22}
$$

$$
{x}_{4} = {2000} - {.005} \times  0 + {.026} \times  \$ {2035.22} = \$ {2052.92}
$$

The optimum solution is thus summarized as

<table><tr><td>Year</td><td>Optimum solution</td><td>Decision</td><td>Accumulation</td></tr><tr><td>1</td><td>${I}_{1}^{ * } = {x}_{1}$</td><td>Invest ${x}_{1} = \$ {4000}$ in First Bank</td><td>${s}_{1} = \$ {5441.80}$</td></tr><tr><td>2</td><td>${I}_{2}^{ * } = {x}_{2}$</td><td>Invest ${x}_{2} = \$ {2072}$ in First Bank</td><td>${s}_{2} = \$ {2610.13}$</td></tr><tr><td>3</td><td>${I}_{3}^{ * } = 0$</td><td>Invest ${x}_{3} = \$ {2035.22}$ in Second Bank</td><td>${s}_{3} = \$ {2365.13}$</td></tr><tr><td>4</td><td>${I}_{4}^{ * } = 0$</td><td>Invest ${x}_{4} = \$ {2052.92}$ in Second Bank</td><td>${s}_{4} = \$ {2274.64}$</td></tr></table>

Total accumulation $= {f}_{1}\left( {x}_{1}\right)  = {7157.7} + {1.38349}\left( {4000}\right)  = \$ {12},{691.66}\left( { = {s}_{1} + {s}_{2} + {s}_{3} + {s}_{4}}\right)$

#### 12.3.5 Inventory Models

DP has important applications in the area of inventory control. Chapters 13 and 16 present some of these applications. The models in Chapter 13 are deterministic, and those in Chapter 16 are probabilistic. Other probabilistic DP applications are given in Chapter 24 on the website.

### 12.4 PROBLEM OF DIMENSIONALITY

In all the DP models presented in this chapter, the state at any stage is represented by a single element. For example, in the knapsack model (Section 12.3.1), the only restriction is the weight of the item. More realistically in this case, the volume of the knapsack may also be another viable restriction, in which case the state at any stage is said to be two dimensional: weight and volume.

The increase in the number of state variables increases the computations at each stage. This is particularly clear in DP tabular computations because the number of rows in each tableau corresponds to all possible combinations of state variables. This computational difficulty is sometimes referred to in the literature as the curse of dimensionality.

The following example is chosen to demonstrate the problem of dimensionality. It also serves to show the relationship between linear and dynamic programming.

## Example 12.4-1

Acme Manufacturing produces two products. The daily capacity of the manufacturing process is 430 minutes. Product 1 requires 2 minutes per unit, and product 2 requires 1 minute per unit. There is no limit on the amount produced of product 1, but the maximum daily demand for product 2 is 230 units. The unit profit of product 1 is \$2 and that of product 2 is \$5. Find the optimal solution by DP.

The problem is represented by the following linear program:

$$
\text{ Maximize }z = 2{x}_{1} + 5{x}_{2}
$$

subject to

$$
2{x}_{1} + {x}_{2} \leq  {430}
$$

$$
{x}_{2} \leq  {230}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

The elements of the DP model are as follows:

1. Stage $i$ corresponds to product $i, i = 1,2$ .

2. Alternative ${x}_{i}$ is the amount of product $i, i = 1,2$ .

3. State $\left( {{v}_{2},{w}_{2}}\right)$ represents the amounts of resources 1 and 2 (production time and demand limits) used in stage 2.

4. State $\left( {{v}_{1},{w}_{1}}\right)$ represents the amounts of resources 1 and 2 (production time and demand limits) used in stages 1 and 2.

Stage 2.

Define ${f}_{2}\left( {{v}_{2},{w}_{2}}\right)$ as the maximum profit for stage 2 (product 2), given the state $\left( {{v}_{2},{w}_{2}}\right)$ . Then

$$
{f}_{2}\left( {{v}_{2},{w}_{2}}\right)  = \mathop{\max }\limits_{\substack{{0 \leq  {x}_{2} \leq  {v}_{2}} \\  {0 \leq  {x}_{2} \leq  {w}_{2}} }}\left\{  {5{x}_{2}}\right\}
$$

Thus, $\max \left\{  {5{x}_{2}}\right\}$ occurs at ${x}_{2} = \min \left\{  {{v}_{2},{w}_{2}}\right\}$ , and the solution for stage 2 is

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{2}\left( {{v}_{2},{w}_{2}}\right)$</td><td>${x}_{2}$</td></tr><tr><td>$\left( {{v}_{2},{w}_{2}}\right)$</td><td>$5\min \left\{  {{v}_{2},{w}_{2}}\right\}$</td><td>$\min \left\{  {{v}_{2},{w}_{2}}\right\}$</td></tr></table>

Stage 1.

$$
{f}_{1}\left( {{v}_{1},{w}_{1}}\right)  = \mathop{\max }\limits_{{0 \leq  2{x}_{1} \leq  {v}_{1}}}\left\{  {2{x}_{1} + {f}_{2}\left( {{v}_{1} - 2{x}_{1},{w}_{1}}\right) }\right\}
$$

$$
= \mathop{\max }\limits_{{0 \leq  {x}_{1} \leq  {v}_{1}/2}}\left\{  {2{x}_{1} + 5\min \left( {{v}_{1} - 2{x}_{1},{w}_{1}}\right) }\right\}
$$

The optimization of stage 1 involves the solution of a (generally more difficult) minimax problem. For the present problem, we set ${v}_{1} = {430}$ and ${w}_{1} = {230}$ , which gives $0 \leq  {x}_{1} \leq  {215}$ . Because min $\left( {{430} - 2{x}_{1},{230}}\right)$ is the lower envelope of two intersecting lines (verify!), it follows that

$$
\min \left( {{430} - 2{x}_{1},{230}}\right)  = \left\{  \begin{array}{ll} {230}, & 0 \leq  {x}_{1} \leq  {100} \\  {430} - 2{x}_{1}, & {100} \leq  {x}_{1} \leq  {215} \end{array}\right.
$$

and

$$
{f}_{1}\left( {{430},{230}}\right)  = \mathop{\max }\limits_{{0 \leq  {x}_{1} \leq  {215}}}\left\{  {2{x}_{1} + 5\min \left( {{430} - 2{x}_{1},{230}}\right) }\right\}
$$

$$
= \mathop{\max }\limits_{{x}_{1}}\left\{  \begin{array}{ll} 2{x}_{1} + {1150}, & 0 \leq  {x}_{1} \leq  {100} \\   - 8{x}_{1} + {2150}, & {100} \leq  {x}_{1} \leq  {215} \end{array}\right.
$$

You can verify graphically that the optimum value of ${f}_{1}\left( {{430},{230}}\right)$ occurs at ${x}_{1} = {100}$ . Thus, we get

<table><tr><td rowspan="2">State</td><td colspan="2">Optimum solution</td></tr><tr><td>${f}_{1}\left( {{v}_{1},{w}_{1}}\right)$</td><td>${x}_{1}$</td></tr><tr><td>(430,230)</td><td>1,350</td><td>100</td></tr></table>

To determine the optimum value of ${x}_{2}$ , we note that

$$
{v}_{2} = {v}_{1} - 2{x}_{1} = {430} - {200} = {230}
$$

$$
{w}_{2} = {w}_{1} - 0 = {230}
$$

Consequently,

$$
{x}_{2} = \min \left( {{v}_{2},{w}_{2}}\right)  = {230}
$$

The complete optimum solution is thus summarized as

$$
{x}_{1} = {100}\text{ units, }{x}_{2} = {230}\text{ units, }z = \$ {1350}
$$

## BIBLIOGRAPHY

Bertsekas, D., Dynamic Programming: Deterministic and Stochastic Models, Prentice Hall, Upper Saddle River, NJ, 1987.

Denardo, E., Dynamic Programming Theory and Applications, Prentice Hall, Upper Saddle River, NJ, 1982.

Dreyfus, S., and A. Law, The Art and Theory of Dynamic Programming, Academic Press, New York, 1977.

Sntedovich, M., Dynamic Programming, Marcel Dekker, New York, 1991.

Case Study: Optimization of Crosscutting and Log Allocation at Weyerhaeuser ${}^{5}$

Tool: DP

## Area of application: Log mill operation

## Description of the situation:

Mature trees are harvested and crosscut into logs in different mills to manufacture different end products (such as construction lumber, plywood, wafer boards, and paper). Log specifications (e.g., lengths and end diameters) for each mill depend on the end product the mill produces. With harvested trees measuring up to ${100}\mathrm{{ft}}$ in length, the number of crosscut combinations meeting mill requirements can be large. Different revenues can be realized depending on the way logs are cut from a tree. The objective is to determine the crosscut combination that maximizes the total revenue.

## Mathematical model:

The basis of the model is that it is not practical to develop an optimum solution that applies to an "average" tree because, in general, harvested trees come in different lengths and end diameters. Thus optimum crosscutting and log allocation must apply to individual trees.

A simplifying assumption of the model is that the usable length $L$ (feet) of a harvested tree is a multiple of a minimum length $K$ (feet). Additionally, the length of a log cut from the tree is also a multiple of $K$ . This means that logs can only be as small as $K$ feet and as large as ${NK}$ feet, where, by definition, $N \leq  \frac{L}{K}$ .

Define

$M =$ Number of mills requesting logs

$I = \frac{L}{K}$

${R}_{m}\left( {i, j}\right)  =$ Revenue at mill $m$ from a log of length ${jK}$ cut from the larger end of a stem (or trunk) of length ${iK}, m = 1,2,\ldots , M;i = 1,2,\ldots , I;j = 1,2,\ldots , N;j \leq  i$

$c =$ Cost of making a crosscut at point $i$ of the tree, $i = 1,2,\ldots , I - 1$

$$
{c}_{ij} = \left\{  \begin{array}{l} c,\text{ if }j < i \\  0,\text{ if }j = i \end{array}\right.
$$

The definition of ${c}_{ij}$ recognizes that if the length ${iK}$ of the stem equals the desired log length ${jK}$ , then no cuts are made.

To understand the meaning of the notation ${R}_{m}\left( {i, j}\right)$ , Figure 12.7 provides a representation of a tree with $I = 8$ and $L = {8K}$ . The crosscuts at points $A$ and $B$ result in one log for mill 1 and two for mill 2. The cutting starts from the larger end of the tree and produces log 1 for mill 2 by making a crosscut at point $A$ . The cut corresponds to $\left( {i = 8, j = 3}\right)$ and produces the revenue ${R}_{2}\left( {8,3}\right)$ . The remaining stem now has a length ${5K}$ . The next crosscut at point $B$ produces log 2 for mill 1 with the length ${2K}$ . This log corresponds to $\left( {i = 5, j = 2}\right)$ and generates the revenue ${R}_{1}\left( {5,2}\right)$ . The remaining stem of length ${3K}$ exactly equals the length of $\log 3$ for mill 2. Hence no further cutting is needed. The associated revenue is ${R}_{1}\left( {3,3}\right)$ . The crosscutting cost associated with the solution is ${c}_{83} = c,{c}_{52} = c$ , and ${c}_{33} = 0$ .

The problem can be formulated and solved as a DP model.

---

${}^{5}$ Lembersky, M. R., and U. H. Chi,"Decision Simulators Speed Implementation and Improve Operations," Interfaces, Vol. 14, No. 4, pp. 1-15, 1984.

---

![bo_d56m4vjef24c73bhe620_23_489_194_888_365_0.jpg](bo_d56m4vjef24c73bhe620_23_489_194_888_365_0.jpg)

FIGURE 12.7

Typical solution in a two-mill situation

Let

$f\left( i\right)  =$ Maximum revenue when the length of the remaining stem is ${iK}, i = 1,2,\ldots , I$

The DP recursive equation is then given as

$$
f\left( 0\right)  \equiv  0
$$

$$
f\left( i\right)  = \mathop{\max }\limits_{\substack{{j = 1,2,\ldots ,\min \left( {i, N}\right) } \\  {m = 1,2,\ldots M} }}\left\{  {{R}_{m}\left( {i, j}\right)  - {c}_{ij} + f\left( {i - j}\right) }\right\}  , i = 1,2,\ldots , I
$$

The idea is that given a stem of length ${iK}, f\left( i\right)$ is a function of the revenue of cutting a log of length $j\left( { \leq  i}\right)$ minus the cost of making a crosscut plus the best cumulative revenue from the remaining stem of length $\left( {i - j}\right) K$ .

## Example computations:

The recursive equation is computed in the order $f\left( 1\right) , f\left( 2\right) ,\ldots , f\left( I\right)$ . The situation deals with two mills $\left( {M = 2}\right)$ , a tree of length $L = {12}\mathrm{{ft}}$ , and a minimum log length $K = 2\mathrm{{ft}}$ , thus yielding $I = 6$ . The cost of a crosscut is $c = \$ {.15}$ . Either mill will accept logs of length2,4,6,8, or 10 ft. This means that $N = 5$ . Figure 12.8 provides the spreadsheet solution of the example (file excelCase8.xls). The basic DP calculations (rows 15-20) are partially automated and will change automatically when ${R}_{m}\left( {i, j}\right)$ in rows 6-11 are altered. All italicized boldface elements are entered manually. ${}^{6}$ The spreadsheet is limited to problems with $I = 6, N = 5$ , and $M = 2$ , in essence allowing changes in the entries of ${R}_{m}\left( {i, j}\right)$ only. ${}^{7}$ The values of ${R}_{m}\left( {i, j}\right) , j \leq  i$ , are given in rows 5 through 11 in the spreadsheet. Note that for a specific $j = {j}^{ * }$ , the value of ${R}_{m}\left( {i,{j}^{ * }}\right)$ increases with $i$ to reflect increases in end diameters of the log.

To illustrate the DP calculations in rows 15-20, note that each stage consists of one row because the state of the system at stage $i$ consists of one value only - namely, the partial stem length. At stage $i = 1$ , the (remaining) stem length is ${1K}$ , hence resulting in one log only of length ${1K}$ (i.e., $j = 1$ ). Also, ${c}_{11} = 0$ because no cutting takes place. Thus,

$$
f\left( 1\right)  = \max \left\{  {{R}_{1}\left( {1,1}\right)  - {c}_{11} + f\left( 0\right) ,{R}_{2}\left( {1,1}\right)  - {c}_{11} + f\left( 0\right) }\right\}
$$

$$
= \max \{ 1 - 0 + 0,{1.1} - 0 + 0\}
$$

$$
= {1.1}
$$

---

${}^{6}$ It is a straightforward Excel exercise to automate columns M and N. I chose not to do that to engage the reader in taking part in determining the optimum solution.

${}^{7}$ The spreadsheet formulas should provide sufficient information to extend the spreadsheet to other input data. Also, a general spreadsheet solution can be developed using (the more involved) VBA macros to specify the size of the matrices ${R}_{m}\left( {i, j}\right)$ and to automate all the calculations.

---

<br>1<br>2<br>3<br>4<br>5<br>1<br>2<br>3<br>4<br>5<br>6<br>1<br>1.00<br>1.10<br>7<br>2<br>1.10<br>1.15<br>1.10<br>2.30<br>8<br>3<br>1.40<br>1.60<br>2.80<br>1.33<br>2.40<br>3.40<br>9<br>4<br>1.90<br>1.90<br>3.90<br>4.10<br>2.10<br>3.30<br>4.20<br>4.10<br>10<br>5<br>2.10<br>2.90<br>4.40<br>4.80<br>7.20<br>2.20<br>3.60<br>4.30<br>4.60<br>6.00<br>11<br>6<br>2.10<br>3.50<br>4.70<br>6.10<br>8.30<br>2.20<br>4.50<br>4.40<br>5.00<br>6.30<br>12<br>13<br>Calculations:<br>f(i)<br>(j*, m*)<br>14<br>i<br>j=1<br>j=2<br>j=3<br>j=4<br>j=5<br>j=1<br>j=2<br>j=3<br>j=4<br>j=5<br>\$0.00<br>15<br>1<br>1.00<br>1.10<br>\$ 1.10<br>(1,2)<br>16<br>2<br>2.05<br>1.15<br>2.05<br>2.30<br>\$ 2.30<br>(2,2)<br>17<br>3<br>3.55<br>2.55<br>2.80<br>3.48<br>3.35<br>3.40<br>\$ 3.55<br>(1,1)<br>18<br>4<br>5.30<br>4.05<br>4.85<br>4.10<br>5.50<br>5.45<br>5.15<br>4.10<br>\$ 5.50<br>(1,2)<br>19<br>5<br>7.45<br>6.30<br>6.55<br>5.75<br>7.20<br>7.55<br>7.00<br>6.45<br>5.55<br>6.00<br>\$ 7.55<br>(1,2)<br>20<br>6<br>9.50<br>8.85<br>8.10<br>8.25<br>9.25<br>9.60<br>9.85<br>7.80<br>7.15<br>7.25<br>\$ 9.85<br>(2,2)<br>21<br>Value $=$<br>\$ 9.85<br>22<br>23<br>m2<br>m1<br>m2<br>m2<br>24<br>25<br>i=1<br>i=2<br>i=3<br>i=4<br>i=5<br>i=6<br>26<br>27<br>$f\left( 0\right) \equiv 0, f\left( i\right) = \mathop{\max }\limits_{{j = 1,2,\ldots ,\min \left( {i, N}\right) }}\left\{ {{R}_{m}\left( {i, j}\right) - {c}_{ij} + f\left( {i - j}\right) }\right\} , i = 1,2,\ldots , I$<br>28<br>29<br>30 -->

![bo_d56m4vjef24c73bhe620_24_395_204_1168_1129_0.jpg](bo_d56m4vjef24c73bhe620_24_395_204_1168_1129_0.jpg)

FIGURE 12.8

Spreadsheet solution of the mill example problem

The associated optimum decision at $i = 1$ calls for a log of length ${1K}\left( {{j}^{ * } = 1}\right)$ for mill $2\left( {{m}^{ * } = 2}\right)$ , or $\left( {{j}^{ * },{m}^{ * }}\right)  = \left( {1,2}\right)$ .

For stage $2\left( {i = 2}\right)$ , logs can assume a length of ${1K}$ or ${2K}$ (i.e., $j = 1$ or 2) for both mills $\left( {m = 1\text{ or 2 }}\right)$ . Thus,

$$
f\left( 2\right)  = \max \left\{  {{R}_{1}\left( {2,1}\right)  - {c}_{21} + f\left( 1\right) ,{R}_{1}\left( {2,2}\right)  - {c}_{22} + f\left( 0\right) ,{R}_{2}\left( {2,1}\right)  - {c}_{21} + f\left( 1\right) ,}\right.
$$

$$
\left. {{R}_{2}\left( {2,2}\right)  - {c}_{22} + f\left( 0\right) }\right\}
$$

$$
= \max \{ {1.1} - {.15} + {1.1},{1.15} - 0 + 0,{1.1} - {.15} + {1.1},{2.3} - 0 + 0\}
$$

$$
= \max \{ {2.05},{1.15},{2.05},{2.3}\}  = {2.3}
$$

The associated optimum decision is $\left( {{j}^{ * },{m}^{ * }}\right)  = \left( {2,2}\right)$ , which calls for cutting one log of length ${2K}$ for mill 2.

The remaining calculations are carried out in a similar manner as shown in Figure 12.8, rows 15-20. Note that entries B15:F20, H15:L20, and M15:M20 are automated in the spreadsheet. The entries $\left( {{j}^{ * },{m}^{ * }}\right)$ in N15:N20 are created manually after the automated computations in rows 15-20 are completed. Manually highlighted cells in rows 15-20 define $f\left( i\right) , i = 1,2,\ldots ,6.$

The optimum solution is read from cells N15:N20 as follows:

$$
\left( {i = 6}\right)  \rightarrow  \left( {{j}^{ * },{m}^{ * }}\right)  = \left( {2,2}\right)  \rightarrow  \left( {i = 4}\right)  \rightarrow  \left( {{j}^{ * },{m}^{ * }}\right)  = \left( {1,2}\right)  \rightarrow
$$

$$
\left( {i = 3}\right)  \rightarrow  \left( {{j}^{ * },{m}^{ * }}\right)  = \left( {1,1}\right)  \rightarrow  \left( {i = 2}\right)  \rightarrow  \left( {{j}^{ * },{m}^{ * }}\right)  = \left( {2,2}\right)
$$

The solution translates to making cuts at $i = 2,3$ , and 4 and produces a total value of $\$ {9.85}$ for the tree.

## Practical considerations:

The results of the DP optimization model are used by field operators in the day-to-day operation of the mill. Thus the implementation of the model must be user-friendly - meaning that the (intimidating) DP calculations are transparent to the user. This is precisely what Lem-berskey and Chi [1] did when they developed the VISION (Video Interactive Stem Inspection and OptimizatioN) computer system. The system is equipped with a database of large representative samples of tree stems from the regions where trees are harvested. The data include the geometry of the stem as well as its quality (e.g., location of knots) and the value (in dollars) for stems with different lengths and diameters. In addition, quality characteristics for the different mills are provided.

A typical user session with VISION includes the following steps:

Step 1: The operator may select a sample stem from the database or create one using the graphic capabilities of VISION. This will result in a realistic representation of the stem on the computer screen. The mills requesting the logs are also selected from the database.

Step 2: After inspecting the stem on the screen, the operator can "cut" the stem into logs based on experience. Next, an optimum DP solution is requested. In both cases, graphic displays of the created logs together with their associated values are projected on the screen. The user is then given the chance to compare the two solutions. In particular, the DP solution is examined to make sure that the created logs meet quality specifications. If not, the user may elect to modify the cuts. In each case, the associated value of the stem is displayed for comparison.

In VISION, DP optimization is transparent totally to the user. In addition, the interactive graphic nature of the output makes the system ideal for training operators and improving their decision-making skills. The design of the system shows how complex mathematical models can be imbedded within a user-friendly computer system.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>12.1</td><td>12-1 to 12-2</td><td>12.3.3</td><td>12-23 to 12-27</td></tr><tr><td>12.2</td><td>12-3 to 12-5</td><td>12.3.4</td><td>12-28 to 12-30</td></tr><tr><td>12.3.1</td><td>12-6 to 12-18</td><td>12.4</td><td>12-31 to 12-32</td></tr><tr><td>12.3.2</td><td>12-19 to 12-22</td><td></td><td></td></tr></table>

*12-1. Solve Example 12.1-1, assuming the following routes are used:

$$
d\left( {1,2}\right)  = 5, d\left( {1,3}\right)  = 9, d\left( {1,4}\right)  = 8
$$

$$
d\left( {2,5}\right)  = {10}, d\left( {2,6}\right)  = {17}
$$

$$
d\left( {3,5}\right)  = 4, d\left( {3,6}\right)  = {10}
$$

$$
d\left( {4,5}\right)  = 9, d\left( {4,6}\right)  = 9
$$

$$
d\left( {5,7}\right)  = {19}
$$

$$
d\left( {6,7}\right)  = 9
$$

12-2. I am an avid hiker. Last summer, my friend G. Don and I went on a 5-day hike-and-camp trip in the beautiful White Mountains in New Hampshire. We decided to limit our hiking to an area comprising three well-known peaks: Mounts Washington, Jefferson, and Adams. Mount Washington has a 6-mile base-to-peak trail. The corresponding base-to-peak trails for Mounts Jefferson and Adams are 4 and 5 miles, respectively. The (two-way) trails joining the bases of the three mountains are 3 miles between Mounts Washington and Jefferson, 2 miles between Mounts Jefferson and Adams, and 5 miles between Mounts Adams and Washington. We started on the first day at the base of Mount Washington and returned to the same spot at the end of 5 days. Our goal was to hike as many miles as we could. We also decided to climb exactly one mountain each day and to camp at the base of the mountain we would be climbing the next day. Additionally, we decided that the same mountain could not be visited in any two consecutive days. Use DP to plan the 5-day hike.

12-3. For Problem 12-1, develop the backward recursive equation, and use it to find the optimum solution.

12-4. For Problem 12-2, develop the backward recursive equation, and use it to find the optimum solution.

*12-5. For the network in Figure 12.9, it is desired to determine the shortest route between cities 1 to 7 Define the stages and the states using backward recursion, and then solve the problem.

![bo_d56m4vjef24c73bhe620_26_519_1618_660_466_0.jpg](bo_d56m4vjef24c73bhe620_26_519_1618_660_466_0.jpg)

FIGURE 12.9

Network for Problem 12-5

12-6. In Example 12.3-1, determine the optimum solution, assuming that the maximum weight capacity of the vessel is 2 tons. Repeat the question for a weight capacity of 5 tons. ${}^{8}$

12-7. Solve the cargo-loading problem of Example 12.3-1 for each of the following sets of data:

*(a) ${w}_{1} = 4,{r}_{1} = {70},{w}_{2} = 1,{r}_{2} = {20},{w}_{3} = 2,{r}_{3} = {40}, W = 6$

(b) ${w}_{1} = 1,{r}_{1} = {15},{w}_{2} = 2,{r}_{2} = {30},{w}_{3} = 3,{r}_{3} = {40}, W = 4$

12-8. In the cargo-loading model of Example 12.3-1, suppose that the revenue per item includes a constant amount that is realized only if the item is chosen, as the following table shows:

<table><tr><td>Item</td><td>Revenue</td></tr><tr><td>1</td><td>$\left\{  \begin{array}{l}  - 5 + {31}{m}_{1}, \\  0, \end{array}\right.$ if ${m}_{1} > 0$ otherwise</td></tr><tr><td>2</td><td>$\left\{  \begin{array}{l}  - {15} + {47}{m}_{2}, \\  0, \end{array}\right.$ if ${m}_{2} > 0$ otherwise</td></tr><tr><td>3</td><td>$\left\{  \begin{array}{l}  - 4 + {14}{m}_{3}, \\  0, \end{array}\right.$ if ${m}_{3} > 0$ otherwise</td></tr></table>

Find the optimal solution using DP. (Hint: You can use the Excel file excelSetupKnap-sack.xls to check your calculations.)

12-9. A wilderness hiker must pack three items: food, first-aid kits, and clothes. The backpack has a capacity of $3{\mathrm{{ft}}}^{3}$ . Each unit of food takes $1{\mathrm{{ft}}}^{3}$ . A first-aid kit occupies ${}^{1}/{}_{4}{\mathrm{{ft}}}^{3}$ , and each piece of cloth takes about $1/2{\mathrm{{ft}}}^{3}$ . The hiker assigns the priority weights 3, 4 , and 5 to food, first aid, and clothes, respectively, which means that clothes are the most valuable of the three items. From experience, the hiker must take at least one unit of each item and no more than two first-aid kits. How many of each item should the hiker take?

*12-10. A student must select 10 electives from four different departments, with at least one course from each department. The 10 courses are allocated to the four departments in a manner that maximizes "knowledge." The student measures knowledge on a 100-point scale and comes up with the following chart:

<table><tr><td rowspan="2">Department</td><td colspan="7">Number of courses</td></tr><tr><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>≥7</td></tr><tr><td>I</td><td>25</td><td>50</td><td>60</td><td>80</td><td>100</td><td>100</td><td>100</td></tr><tr><td>II</td><td>20</td><td>70</td><td>90</td><td>100</td><td>100</td><td>100</td><td>100</td></tr><tr><td>III</td><td>40</td><td>60</td><td>80</td><td>100</td><td>100</td><td>100</td><td>100</td></tr><tr><td>IV</td><td>10</td><td>20</td><td>30</td><td>40</td><td>50</td><td>60</td><td>70</td></tr></table>

How should the student select the courses?

---

${}^{8}$ In Problems 12-6 to 12-18, you are encouraged where applicable to verify hand computations using the template excelKnapsack.xls.

---

12-11. I have a small backyard garden that measures ${10} \times  {20}\mathrm{{ft}}$ . This spring I plan to plant three types of vegetables: tomatoes, green beans, and corn. The garden is organized in 10-foot rows. The corn and tomatoes rows are 2 ft wide, and the beans rows are 3 ft wide. I like tomatoes the most and beans the least, and on a scale of 1 to 10, I would assign 10 to tomatoes, 7 to corn, and 3 to beans. Regardless of my preferences, my wife insists that I plant at least one row of green beans and no more than two rows of tomatoes. How many rows of each vegetable should I plant?

*12-12. Habitat for Humanity is a wonderful (U.S.-based) international charity organization that builds homes for needy families using volunteer labor and donated building materials. An eligible family can choose from three home sizes: 1000, 1100, and ${1200}{\mathrm{{ft}}}^{2}$ . Each size requires a certain number of labor volunteers. The Fayetteville, Arkansas, chapter has received five applications for the upcoming 6 months. The committee in charge assigns a score to each application based on several factors. A higher score signifies higher need. For the next 6 months, the chapter can count on a maximum of 23 volunteers. The following data summarize the scores for the applications and the required number of volunteers. Which applications should the committee approve?

<table><tr><td>Application</td><td>House size $\left( {\mathrm{{ft}}}^{2}\right)$</td><td>Score</td><td>Number of volunteers</td></tr><tr><td>1</td><td>1200</td><td>78</td><td>7</td></tr><tr><td>2</td><td>1000</td><td>64</td><td>4</td></tr><tr><td>3</td><td>1100</td><td>68</td><td>6</td></tr><tr><td>4</td><td>1000</td><td>62</td><td>5</td></tr><tr><td>5</td><td>1200</td><td>85</td><td>8</td></tr></table>

12-13. Sheriff Bassam is up for reelection in Washington County. The funds available for the campaign are about \$10,000. Although the reelection committee would like to launch the campaign in all five precincts of the county, limited funds dictate otherwise. The table given below lists the voting population and the amount of funds needed to launch an effective campaign in each precinct. A precinct can receive either all its allotted funds or none. How should the funds be allocated?

<table><tr><td>Precinct</td><td>Population</td><td>Required funds (\$)</td></tr><tr><td>1</td><td>3100</td><td>3500</td></tr><tr><td>2</td><td>2600</td><td>2500</td></tr><tr><td>3</td><td>3500</td><td>4000</td></tr><tr><td>4</td><td>2800</td><td>3000</td></tr><tr><td>5</td><td>2400</td><td>2000</td></tr></table>

12-14. An electronic device consists of three components. The three components are in series so that the failure of one component causes the failure of the device. The reliability (probability of no failure) of the device can be improved by installing one or two standby units in each component. The table listed below charts the reliability, $r$ , and the cost, $c$ . The total capital available for the construction of the device is $\$ {10},{000}$ . How should the device be constructed? (Hint: The objective is to maximize the reliability, ${r}_{1}{r}_{2}{r}_{3}$ , of the device. This means that the decomposition of the objective function is multiplicative rather than additive.)

<table><tr><td rowspan="2">Number of parallel units</td><td colspan="2">Component 1</td><td colspan="2">Component 2</td><td colspan="2">Component 3</td></tr><tr><td>${r}_{1}$</td><td>${c}_{1}\left( \$ \right)$</td><td>${r}_{2}$</td><td>${c}_{2}\left( \$ \right)$</td><td>${r}_{3}$</td><td>${c}_{3}\left( s\right)$</td></tr><tr><td>1</td><td>.6</td><td>1000</td><td>.7</td><td>3000</td><td>.5</td><td>2000</td></tr><tr><td>2</td><td>.8</td><td>2000</td><td>.8</td><td>5000</td><td>.7</td><td>4000</td></tr><tr><td>3</td><td>.9</td><td>3000</td><td>.9</td><td>6000</td><td>.9</td><td>5000</td></tr></table>

12-15. Solve the following model by DP:

$$
\text{ Maximize }z = \mathop{\prod }\limits_{{i = 1}}^{n}{y}_{i}
$$

subject to

$$
{y}_{1} + {y}_{2} + \ldots  + {y}_{n} = c
$$

$$
{y}_{j} \geq  0, j = 1,2,\ldots , n
$$

(Hint: This problem is similar to Problem 12-14, except that the variable ${y}_{j}$ is continuous.)

12-16. Solve the following problem by DP:

$$
\text{ Minimize }z = {y}_{1}^{2} + {y}_{2}^{2} + \ldots  + {y}_{n}^{2}
$$

subject to

$$
\mathop{\prod }\limits_{{i = 1}}^{n}{y}_{i} = c
$$

$$
{y}_{i} > 0, i = 1,2,\ldots , n
$$

12-17. Solve the following problem by DP:

$$
\text{ Maximize }z = {\left( {y}_{1} + 2\right) }^{2} + {y}_{2}{y}_{3} + {\left( {y}_{4} - 5\right) }^{2}
$$

subject to

$$
{y}_{1} + {y}_{2} + {y}_{3} + {y}_{4} \leq  5
$$

$$
{y}_{i} \geq  0\text{ and integer, }i = 1,2,3,4
$$

12-18. Solve the following problem by DP:

$$
\text{ Minimize }z = \max \left\{  {f\left( {y}_{1}\right) , f\left( {y}_{2}\right) ,\ldots , f\left( {y}_{n}\right) }\right\}
$$

subject to

$$
{y}_{1} + {y}_{2} + \ldots  + {y}_{n} = c
$$

$$
{y}_{i} \geq  0, i = 1,2,\ldots , n
$$

Provide the solution for the special case of $n = 3, c = {10}$ , and $f\left( {y}_{1}\right)  = {y}_{1} + 5$ , $f\left( {y}_{2}\right)  = 5{y}_{2} + 3$ , and $f\left( {y}_{3}\right)  = {y}_{3} - 2$ .

12-19. Solve Example 12.3.2 for each of the following minimum labor requirements:

*(a) ${b}_{1} = 6,{b}_{2} = 5,{b}_{3} = 3,{b}_{4} = 6,{b}_{5} = 8$

(b) ${b}_{1} = 6,{b}_{2} = 4,{b}_{3} = 7,{b}_{4} = 8,{b}_{5} = 2$

12-20. In Example 12.3-2, if a severance pay of \$100 is incurred for each fired worker, determine the optimum solution.

*12-21. Luxor Travel arranges 1-week tours to southern Egypt. The agency provides 7, 4, 7, and 8 rental cars over the next 4 weeks. Luxor Travel subcontracts with a local car dealer to supply rental needs. The dealer charges a rental fee of \$220 per car per week, plus a flat fee of \$500 for any rental transaction. Luxor, however, may elect to keep the rentals for an additional week and simply continue to pay the rent. What is the best way for Luxor Travel to handle the rental situation?

12-22. GECO is contracted for the next 4 years to supply aircraft engines at the rate of four engines a year. Available production capacity and production costs vary from year to year. GECO can produce five engines in year 1, six in year 2, three in year 3, and five in year 4. The corresponding production costs per engine over the next 4 years are \$200,000,\$330,000,\$350,000, and \$420,000, respectively. GECO can elect to produce more than it needs in a certain year, in which case the engines must be properly stored until shipment date. The storage cost per engine also varies from year to year, and is estimated to be \$20,000 for year 1, \$30,000 for year 2, \$40,000 for year 3, and \$50,000 for year 4. Currently, at the start of year 1, GECO has one engine ready for shipping. Develop an optimal production plan for GECO.

12-23. In each of the following cases, develop the network, and find the optimal solution for the model in Example 12.3-3:

(a) The machine is 2 years old at the start of year 1.

(b) The machine is 1 year old at the start of year 1.

(c) The machine is bought new at the start of year 1.

*12-24. My son, age 13, has a lawn-mowing business with 10 customers. For each customer, he cuts the grass 3 times a year, which earns him \$50 for each mowing. He has just paid \$200 for a new mower. The maintenance and operating cost of the mower is \$120 for the first year in service and increases by 20% a year thereafter. A 1-year-old mower has a resale value of \$150, which decreases by 10% a year thereafter. My son, who plans to keep his business until he is 16 , thinks that it is more economical to buy a new mower every 2 years. He bases his decision on the fact that the price of a new mower will increase only by 10% a year. Is his decision justified?

12-25. Circle Farms wants to develop a replacement policy for its 2-year-old tractor over the next 5 years. A tractor must be kept in service for at least 3 years, but must be disposed of after 5 years. The current purchase price of a tractor is \$40,000 and increases by 10% a year. The salvage value of a 1-year-old tractor is \$30,000 and decreases by 10% a year. The current annual operating cost of the tractor is \$1300 but is expected to increase by 10% a year.

(a) Formulate the problem as a shortest-route problem.

(b) Develop the associated recursive equation.

(c) Determine the optimal replacement policy of the tractor over the next 5 years.

12-26. Consider the equipment replacement problem over a period of $n$ years. A new piece of equipment costs $c$ dollars, and its resale value after $t$ years in operation is $s\left( t\right)  = n - t$ for $n > t$ and zero otherwise. The annual revenue is a function of the age $t$ and is given by $r\left( t\right)  = {n}^{2} - {t}^{2}$ for $n > t$ and zero otherwise.

(a) Formulate the problem as a DP model.

(b) Find the optimal replacement policy given that $c = \$ {10},{000}, n = 5$ , and the equipment is 2 years old.

12-27. Solve Problem 12-26, assuming that the equipment is 1 year old and that $n = 4$ , $c = \$ {6000}$ , and $r\left( t\right)  = \frac{n}{1 + t}$ .

12-28. Solve Example 12.3-4, assuming that ${r}_{1} = {.085}$ and ${r}_{2} = {.08}$ . Additionally, assume that ${P}_{1} = \$ {5000},{P}_{2} = \$ {4000},{P}_{3} = \$ {3000}$ , and ${P}_{4} = \$ {2000}$ .

12-29. An investor with an initial capital of $\$ {10},{000}$ must decide at the end of each year how much to spend and how much to invest in a savings account. Each dollar invested returns $\alpha  = \$ {1.09}$ at the end of the year. The satisfaction derived from spending $\$ y$ in any one year is quantified monetarily as $\sqrt[5]{y}$ . Solve the problem by DP for a span of 5 years.

12-30. A farmer owns $k$ sheep. At the end of each year, a decision is made as to how many to sell or keep. The profit from selling a sheep in year $i$ is ${p}_{i}$ . The sheep kept in year $i$ will double in number in year $i + 1$ . The farmer plans to sell out completely at the end of $n$ years.

*(a) Derive the general recursive equation for the problem.

(b) Solve the problem for $n = 3$ years, $k = 2$ sheep, ${p}_{1} = \$ {100},{p}_{2} = \$ {130}$ , and ${p}_{3} = \$ {120}$ .

12-31. Solve the following problems by DP.

(a) Maximize $z = 4{x}_{1} + {14}{x}_{2}$ subject to

$$
2{x}_{1} + 7{x}_{2} \leq  {21}
$$

$$
7{x}_{1} + 2{x}_{2} \leq  {21}
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

(b) Maximize $z = 8{x}_{1} + 7{x}_{2}$ subject to

$$
2{x}_{1} + {x}_{2} \leq  8
$$

$$
5{x}_{1} + 2{x}_{2} \leq  {15}
$$

$$
{x}_{1},{x}_{2} \geq  0\text{ and integer }
$$

(c) Maximize $z = 7{x}_{1}^{2} + 6{x}_{1} + 5{x}_{2}^{2}$

subject to

$$
{x}_{1} + 2{x}_{2} \leq  {10}
$$

$$
{x}_{1} - 3{x}_{2} \leq  9
$$

$$
{x}_{1},{x}_{2} \geq  0
$$

12-32. In the $n$ -item knapsack problem of Example 12.3-1, suppose that the weight and volume limitations are $W$ and $V$ , respectively. Given that ${w}_{i},{v}_{i}$ , and ${r}_{i}$ are the weight, value, and revenue per unit, respectively, of item $i$ , write the DP backward recursive equation for the problem.