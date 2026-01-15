## CHAPTER 11 Traveling Salesperson Problem (TSP)

## Real-Life Application

The Australian Defence Sciences and Technology Organisation employs synthetic aperture radar mounted on an aircraft to obtain high-resolution images of up to 20 rectangular swaths of land. Originally, flight path covering a sequence of swaths was done visually using time-consuming and usually suboptimal mapping software. Subsequently, a TSP-based software was developed to plan missions with up to 20 swaths. The new software can plan a mission in less than 20 seconds, compared with 1 hr using the visual process. Additionally, the average mission length is 15% less than the one obtained manually. ${}^{1}$

### 11.1 SCOPE OF THE TSP

Classically, the TSP problem deals with finding the shortest (closed) tour in an $n$ -city situation, where each city is visited exactly once before returning back to the starting point. The associated TSP model is defined by two pieces of data:

1. The number of cities, $n$ .

2. The distances ${d}_{ij}$ between cities $i$ and $j\left( {{d}_{ij} = \infty }\right.$ if cities $i$ and $j$ are not linked).

The maximum number of tours in an $n$ -city situation is $\left( {n - 1}\right)$ ! if the network is directed (i.e., ${d}_{ij} \neq  {d}_{ji}$ ) and half that much if it is not.

In reality, TSP applications extend well beyond the classical definition of visiting cities. The real-life application given at the start of this chapter describes mission planning for synthetic aperture radar surveillance. The Aha! Moment below describes a noted TSP application in the late nineteenth century that ushered the first known use of mathematical modeling in archaeology (a field mainly dominated by art historians and linguists). A brief list of other TSP applications is given in Problem 11-1. Additional applications are also given in Problems 11-2 to 11-14.

---

${}^{1}$ Details of the study can be found in D. Panton and A. Elbers,"Mission Planning for Synthetic Aperture Radar Surveillance," Interfaces, Vol. 29, No. 2, pp. 73-88, 1999.

---

## Aha! Moment: Earliest Mathematical Model in Archaeology, or How to "Seriate" Ancient Egyptian Graves Using TSP ${}^{2}$

In 1894, the eminent British Egyptologist Flinders Petrie (1853-1942) excavated a vast site of predynastic graves west of the Nile in Naqada, Egypt. A standard method, called seriation, was used to establish the chronological order (or time sequence) of the relative dates the graves were built. The method employs classifications of time-based changes of artifacts, such as stone tools and pottery fragments.

The Naqada tomb site boasted an abundance of potteries used to store essentials Ancient Egyptians thought necessary for the afterlife. Petrie kept meticulous records of the potteries in each grave, but needed a systematic process to translate the data into a chronological order of the time the graves were constructed. He started with some 900 promising graves, classifying their potteries into 9 principal styles. He then designed (narrow) paper slips each comprised of 10 columns. The first column holds the grave code and the remaining nine columns represented the nine pottery styles. Codes of the styles found in a grave were entered in their proper columns. A column is left blank if its style is not found in the grave. In the end, a column entry in a slip is viewed in a 0-1 (binary) fashion representing the absence or presence of a pottery style in the grave.

The data slips allowed the determination of a numeric score representing the closeness (in time) of two graves: a count of the entries that differ from one another among all nine pottery styles. For example, the following two slips yield a score of 4 as shown by the underlines:

Grave 1: absent, present, present, present, absent, present, present, present, absent, present

Grave 2: absent, absent, absent, present, present, present, present, present, present

A zero or small score indicates that the two graves are likely built within the same era; otherwise, large scores suggest the graves originated in distinct eras. Using this line of reasoning, Petrie physically ordered the slips vertically so that graves with similar scores were placed close to one another (cf. Nearest Neighbor heuristic, Section 11.4.1) and was thus able to infer a chronological order of the relative times the graves were constructed. Petrie noted that his seriation problem could be solved by finding the arrangement of all graves that minimizes the sum of their associated scores.

In today's terminology, Petrie's seriation problem is a classical TSP application in which the graves stand for cities and the scores represent the lapses ("distances") between the times two graves were constructed. Though Petrie described his model in archaeological terms (rather than mathematically), it is clear that he had an exceptional mathematical mind. Remarkably, using the binary code he developed in the late nineteenth century to represent (absence-presence of) a pottery style in a grave site, Petrie's numeric score is the same as what is now known as Hamming distance, devised in 1950 by Richard Hamming and currently used in telecommunications and information science.

---

${}^{2}$ Thomas L. Gertzen and Martin Grotschel, Flinders Petrie (1853-1942), the Travelling Salesman Problem, and the Beginning of Mathematical Modeling in Archaeology, Documenta Mathematica, Extra Vol. ISMP, pp. 199-210, 2012.

---

Because of the similarity between the seriation problem and the TSP, Petrie is credited with ushering in the use of the first "mathematical" model in archaeology.

As a historical note, Petrie had no formal schooling and his knowledge in mathematics included two self-taught courses in algebra and trigonometry at age 24. Yet, his discoveries as an archaeologist resulted in a prestigious professorship in Egyptology at University College London. Among Petrie's students was Howard Carter who later discovered the tomb of "boy king" Tutankhamun in 1922. Petrie remained committed to scientific discovery even after his own death, as he donated his skull (and brain) to the Royal College of Surgeons of England to permit study of his own exceptional intellectual abilities. The Petrie Museum of Egyptian Archaeology in London houses more than 80,000 pieces and ranks fourth in Egyptian artifacts after the Cairo Museum, the British Museum, and the Ägyptisches Museum, Berlin.

### 11.2 TSP MATHEMATICAL MODEL

As stated in Section 11.1, a TSP model is defined by the number of cities $n$ and the distance matrix $\begin{Vmatrix}{d}_{ij}\end{Vmatrix}$ . The definition of a tour disallows linking a city to itself by assigning a very high penalty to the diagonal elements of the distance matrix. A TSP is symmetric if ${d}_{ij} = {d}_{ji}$ for all $i$ and $j$ ; else it is asymmetric.

Define

$$
{x}_{ij} = \left\{  \begin{array}{l} 1,\text{ if city }j\text{ is reached from city }i \\  0,\text{ otherwise } \end{array}\right.
$$

The TSP model is given as

$$
\text{ Minimize }z = \mathop{\sum }\limits_{{i = 1}}^{n}\mathop{\sum }\limits_{{j = 1}}^{n}{d}_{ij}{x}_{ij},{d}_{ij} = \infty \text{ for all }i = j
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{x}_{ij} = 1, i = 1,2,\ldots , n \tag{1}
$$

$$
\mathop{\sum }\limits_{{i = 1}}^{n}{x}_{ij} = 1, j = 1,2,\ldots , n \tag{2}
$$

$$
{x}_{ij} = \left( {0,1}\right) \tag{3}
$$

$$
\text{ Solution forms a roundtrip }n\text{ -city tour } \tag{4}
$$

Constraints (1), (2), and (3) define a regular assignment model (Section 5.4) in which ${x}_{ij} = 1$ if node (city) $i$ is linked to node (city) $j$ , and zero otherwise. If the solution of the assignment model happens to be a tour [i.e., it satisfies constraint (4)], then it is automatically optimal for the TSP. This is a rare occurrence, however, and the assignment model is likely to consist of subtours. Additional computations are then needed to determine the optimal tour solution. Figure 11.1 demonstrates a 5-city TSP with a tour and a subtour solution. The nodes represent cities, and the arcs represent two-way routes that can be distinct if the TSP is asymmetric.

![bo_d56m4sref24c73bhe60g_3_315_198_1240_561_0.jpg](bo_d56m4sref24c73bhe60g_3_315_198_1240_561_0.jpg)

FIGURE 11.1

A 5-city TSP example with a tour or subtour solution of the associated assignment model depending on the specific distance matrix instance

## Example 11.2-1

The daily production schedule at the Rainbow Company includes batches of white $\left( W\right)$ , yellow $\left( Y\right)$ , red $\left( R\right)$ , and black $\left( B\right)$ paints. The production facility must be cleaned between successive batches. Table 11.1 summarizes the cleanup times in minutes. The objective is to determine the sequencing of colors that minimizes the total cleanup time.

In the TSP model, each color represents a "city," and the cleanup time between two successive colors represents "distance." Let $M$ be a sufficiently large penalty and define

$$
{x}_{ij} = 1\text{ if paint }j\text{ follows paint }i\text{ and zero otherwise }
$$

The TSP model is given as

$$
\text{ Minimize }z = {10}{x}_{WY} + {17}{x}_{WB} + {15}{x}_{WR} + {20}{x}_{YW} + {19}{x}_{YB} + {18}{x}_{YR} + {50}{x}_{BW} + {44}{x}_{BY}
$$

$$
+ {22}{x}_{BR} + {45}{x}_{RW} + {40}{x}_{RY} + {20}{x}_{RB} + M\left( {{x}_{WW} + {x}_{yy} + {x}_{BB} + {x}_{RR}}\right)
$$

TABLE 11.1 Interbatch Cleanup Times (in minutes) for the Paint Production Problem

<table><tr><td rowspan="2">Paint</td><td colspan="4">Interbatch cleanup time (min)</td></tr><tr><td>White</td><td>Yellow</td><td>Black</td><td>Red</td></tr><tr><td>White</td><td>$\infty$</td><td>10</td><td>17</td><td>15</td></tr><tr><td>Yellow</td><td>20</td><td>$\infty$</td><td>19</td><td>18</td></tr><tr><td>Black</td><td>50</td><td>44</td><td>$\infty$</td><td>22</td></tr><tr><td>Red</td><td>45</td><td>40</td><td>20</td><td>00</td></tr></table>

subject to

$$
{x}_{WW} + {x}_{WY} + {x}_{WB} + {x}_{WR} = 1
$$

$$
{x}_{YW} + {x}_{YY} + {x}_{YB} + {x}_{YR} = 1
$$

$$
{x}_{BW} + {x}_{BY} + {x}_{BB} + {x}_{BR} = 1
$$

$$
{x}_{RW} + {x}_{RY} + {x}_{RB} + {x}_{RR} = 1
$$

$$
{x}_{WW} + {x}_{YW} + {x}_{BW} + {x}_{RW} = 1
$$

$$
{x}_{WY} + {x}_{YY} + {x}_{BY} + {x}_{RY} = 1
$$

$$
{x}_{WB} + {x}_{YB} + {x}_{BB} + {x}_{RB} = 1
$$

$$
{x}_{WR} + {x}_{YR} + {x}_{BR} + {x}_{RR} = 1
$$

$$
{x}_{ij} = \left( {0,1}\right) \text{ for all }i\text{ and }j
$$

$$
\text{ Solution is a tour (loop) }
$$

The use of the penalty $M$ in the objective function is equivalent to deleting ${x}_{WW},{x}_{YY},{x}_{BB}$ , and ${x}_{RR}$ from the model. The underlying assignment-model structure is the basis for the development of the TSP algorithms.

TSP solution. A straightforward way to solve TSP is exhaustive enumeration. The maximum number of tours in an $n$ -city problem is $\left( {n - 1}\right)$ !. For the present example, exhaustive enumeration is feasible because the number of possible tours is small $\left( { = 6}\right)$ . Table 11.2 lists and evaluates all six tours and shows that tour $W \rightarrow  Y \rightarrow  B \rightarrow  R \rightarrow  W$ is optimum.

Exhaustive enumeration is not practical for the general TSP. Instead, Section 11.3 presents two exact integer programming algorithms: branch-and-bound (B&B) and cutting plane. Both algorithms are rooted in the solution of the assignment model, with added restrictions to guarantee a tour solution. Unfortunately, as is typical with most integer programming algorithms, the proposed methods are not computationally reliable. For this reason, heuristics are used to provide good (but not necessarily optimal) solutions to the problem. Three of these heuristics are presented in Section 11.5.

Interpretation of the optimum solution. The optimum production sequence $W \rightarrow  Y \rightarrow \; B \rightarrow  R \rightarrow  W$ in Table 11.2 starts with the white color, followed by yellow, then black, and then red. It is really immaterial which color we use to start the production cycle because the solution is a closed-tour. For example, the sequences $B \rightarrow  R \rightarrow  W \rightarrow  Y \rightarrow  B$ and $Y \rightarrow  B \rightarrow  R \rightarrow  W \rightarrow  Y$ are also optimal.

TABLE 11.2 Solution of the Paint Sequencing Problem by Exhaustive Enumeration

<table><tr><td>Production loop</td><td>Total cleanup time (min)</td></tr><tr><td>$W \rightarrow  Y \rightarrow  B \rightarrow  R \rightarrow  W$</td><td>${10} + {19} + {22} + {45} = {96}$</td></tr><tr><td>$W \rightarrow  Y \rightarrow  R \rightarrow  B \rightarrow  W$</td><td>${10} + {18} + {20} + {50} = {98}$</td></tr><tr><td>$W \rightarrow  B \rightarrow  Y \rightarrow  R \rightarrow  W$</td><td>${17} + {44} + {18} + {45} = {124}$</td></tr><tr><td>$W \rightarrow  R \rightarrow  B \rightarrow  Y \rightarrow  W$</td><td>${17} + {22} + {40} + {20} = {99}$</td></tr><tr><td>$W \rightarrow  R \rightarrow  B \rightarrow  Y \rightarrow  W$</td><td>${15} + {20} + {44} + {20} = {99}$</td></tr><tr><td>$W \rightarrow  R \rightarrow  Y \rightarrow  B \rightarrow  W$</td><td>${15} + {40} + {19} + {50} = {124}$</td></tr></table>

Open-tour TSP. Open tours occur when a return to the starting city is not required. This case can be demonstrated in the paint problem when production is limited to exactly one batch of each color. For example, in the open-tour sequence, $B \rightarrow  W \rightarrow  Y \rightarrow  R$ , the last "city" $\left( R\right)$ does not link back to the starting "city" $\left( B\right)$ .

The condition can be accounted for in an $n$ -city situation by adding a fictitious city, $n + 1$ , with zero distances to and from all the real cities-that is, ${d}_{i, n + 1} = 0, i = 1,2,\ldots , n$ and ${d}_{n + 1, j} = 0, j = 1,2,\ldots , n$ . For the paint example, the new distance matrix becomes

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {10} & {17} & {15} & 0 \\  {20} & \infty & {19} & {18} & 0 \\  {50} & {44} & \infty & {22} & 0 \\  {45} & {40} & {20} & \infty & 0 \\  0 & 0 & 0 & 0 & \infty  \end{matrix}\right)
$$

Row 5 and column 5 represent the fictitious color.

The optimum tour is

$$
W \rightarrow  Y \rightarrow  R \rightarrow  B \rightarrow  \text{ Fictitious } \rightarrow  W\text{ , length } = {48}\mathrm{\;{min}}
$$

The solution can be read by rearranging the tour starting and terminating points with the fictitious color:

$$
\text{ Fictitious } \rightarrow  W \rightarrow  Y \rightarrow  R \rightarrow  B \rightarrow  \text{ Fictitious }
$$

Removing the fictitious color, we get the following open-tour solution:

$$
W \rightarrow  Y \rightarrow  R \rightarrow  B
$$

It is important to note that the open-tour optimum solution cannot be obtained from the optimum closed-tour solution $\left( {W \rightarrow  Y \rightarrow  B \rightarrow  R \rightarrow  W}\right)$ directly.

Lower bound on the optimum tour length. A lower bound on the optimum tour length can be useful in solving the TSP by either the exact or the heuristic algorithms. In the case of the exact algorithms, a tight lower bound restricts the feasible space and thus makes the algorithm more efficient (particularly in the case of B&B). For the heuristics, a lower bound can be used to judge the quality of the heuristic solution.

There are a number of methods for estimating a lower bound. Two of them are presented here:

1. Assignment model. The assignment model is a relaxation of the TSP model, and its optimum solution provides a lower bound on the optimum tour length. Indeed, if the optimum solution of the assignment model is feasible (i.e., a tour), then it is also optimum for the TSP.

The solution of the (closed tour) assignment model for the paint problem yields a lower bound of ${72}\mathrm{\;{min}}$ .

2. Linear programming. A lower bound in an $n$ -city situation can be determined by inscribing the largest nonoverlapping circles around all the cities. Let ${r}_{j}, j = 1,2,\ldots , n$ , be the largest radius of a circle inscribed around city $j$ . The optimum value of the following LP provides a lower bound:

$$
\text{ Maximize }z = 2\left( {{r}_{1} + {r}_{2} + \ldots  + {r}_{n}}\right)
$$

subject to

$$
{r}_{i} + {r}_{j} \leq  \min \left( {{d}_{ij},{d}_{ji}}\right) i, j = 1,2,\ldots , n, i < j
$$

The objective function recognizes that a salesperson entering the circle around city $i$ must cover a distance of at least $2{r}_{i}$ before entering the circle domain of any other city in the network. The constraints guarantee that none of the circles overlap.

For the paint example, we have

$$
\text{ Maximize }z = 2\left( {{r}_{W} + {r}_{Y} + {r}_{B} + {r}_{R}}\right)
$$

subject to

$$
{r}_{W} + {r}_{y} \leq  \min \left( {{10},{20}}\right)
$$

$$
{r}_{W} + {r}_{B} \leq  \min \left( {{17},{50}}\right)
$$

$$
{r}_{W} + {r}_{R} \leq  \min \left( {{15},{45}}\right)
$$

$$
{r}_{Y} + {r}_{B} \leq  \min \left( {{19},{44}}\right)
$$

$$
{r}_{Y} + {r}_{R} \leq  \min \left( {{18},{40}}\right)
$$

$$
{r}_{B} + {r}_{R} \leq  \min \left( {{22},{20}}\right)
$$

$$
{r}_{W},{r}_{Y},{r}_{B},{r}_{R}, \geq  0
$$

The solution yields a lower bound of ${60}\mathrm{\;{min}}$ , which is not as tight as the one obtained from the assignment model $\left( { = {72}\mathrm{\;{min}}}\right)$ . Actually, experimentation with the two methods suggests that the assignment model consistently yields tighter lower bounds, particularly when the TSP is asymmetric. Note that the LP will always provide a trivial zero-value lower bound for an open-tour TSP because the zero "in-out" distances of the fictitious city set a zero limit on all the radii.

## AMPL Moment

The assignment and the LP models given above for estimating the lower bound can be solved using the following AMPL files provided on the website:

---

model amplAssign.txt; data amplInputData.txt; commands solutionAssign.txt;

model amplLP.txt; data amplInputData.txt; commands solutionLP.txt;

---

File amplInputData.txt provides the TSP data of the paint problem.

### 11.3 EXACT TSP ALGORITHMS

This section presents two exact IP algorithms: B&B and cutting plane. Both algorithms guarantee optimality theoretically. The computational issue is a different story-meaning that the algorithms may fail to produce the optimum in a reasonable amount of time, prompting the development of the heuristics in Sections 11.4 and 11.5.

#### 11.3.1 B&B Algorithm

The idea of the B&B algorithm is to start with the optimum solution of the associated assignment problem. If the solution is a tour, the process ends. Otherwise, restrictions are imposed on the resulting solution to disallow subtours. The idea is to create branches that assign a zero value to each of the variables of one of the subtours. Normally, the subtour with the smallest number of cities is selected for branching because it creates the smallest number of branches.

If the solution of the assignment problem at any node is a tour, its objective value provides an upper bound on the optimum tour length. If it does not, further branching at the node is required. A subproblem is fathomed if it yields a smaller upper bound, or if there is evidence that it cannot lead to a better upper bound. The optimum tour is given at the node with the smallest upper bound.

The following example provides the details of the TSP B&B algorithm.

Example 11.3-1

Consider the following 5-city TSP distance matrix:

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {10} & 3 & 6 & 9 \\  5 & \infty & 5 & 4 & 2 \\  4 & 9 & \infty & 7 & 8 \\  7 & 1 & 3 & \infty & 4 \\  3 & 2 & 6 & 5 & \infty  \end{matrix}\right)
$$

The associated assignment is solved using AMPL, TORA, or Excel. The solution is

$$
z = {15},\left( {{x}_{13} = {x}_{31} = 1}\right) ,\left( {{x}_{25} = {x}_{54} = {x}_{42} = 1}\right) \text{ , all others } = 0
$$

It consists of two subtours, 1-3-1 and 2-5-4-2, and constitutes the starting node of the B&B search tree, as shown at node 1 in Figure 11.2.

In the present example, we will use an arbitrary tour, 1-2-3-4-5-1, to determine the initial upper bound-namely, ${10} + 5 + 7 + 4 + 3 = {29}$ units. Alternatively, the heuristics in Sections 11.4 and 11.5 may be used to yield improved (smaller) upper bounds. The estimated

FIGURE 11.2 upper bound means that the optimum tour length cannot exceed 29. Future B&B nodes seek smaller upper bounds, if any exists.

B&B solution of the TSP problem of Example 11.3-1

![bo_d56m4sref24c73bhe60g_7_429_1351_1016_819_0.jpg](bo_d56m4sref24c73bhe60g_7_429_1351_1016_819_0.jpg)

At node 1 of the B&B tree, the smaller subtour 1-3-1 creates branch ${x}_{13} = 0$ leading to node 2 and ${x}_{31} = 0$ leading to node 3 . The associated assignment problems at nodes 2 and 3 are created from the problem at node 1 by setting ${d}_{13} = \infty$ and ${d}_{31} = \infty$ , respectively.

At this point, we can examine either node 2 or node 3, and we arbitrarily choose to explore node 2. Its assignment solution is 2-5-2 and 1-4-3-1 with $z = {17}$ . Because the solution is not a tour, we select the smaller subtour 2-5-2 for branching: branch ${x}_{25} = 0$ leads to node 4 and branch ${x}_{52} = 0$ leads to node 5 .

We now have three unexplored subproblems: nodes 3, 4, and 5. We arbitrarily examine the subproblem at node 4, setting ${d}_{25} = \infty$ in the distance matrix at node 2 . The resulting solution, tour 1-4-5-2-3-1, yields the smaller upper bound $z = {21}$ .

The two subproblems at nodes 3 and 5 remain unexplored. Arbitrarily selecting subproblem 5, we set ${d}_{52} = \infty$ in the distance matrix at node 2 . The result is tour 1-4-2-5-3-1 with the smaller upper bound $z = {19}$ . Subproblem 3 is the only one that remains unexplored. Substituting ${d}_{31} = \infty$ in the distance matrix at node 1, we get yet a better tour solution: 1-3-4-2-5-1 with the smaller upper bound $z = {16}$ .

All the nodes in the tree have been examined, thus completing the B&B search. The optimal tour is the one associated with the smallest upper bound: 1-3-4-2-5-1 with length 16 units.

Remarks. The solution of Example 11.3-1 reveals two points:

1. The search sequence $1 \rightarrow  2 \rightarrow  4 \rightarrow  5 \rightarrow  3$ was selected deliberately to demonstrate a worst case scenario in the B&B algorithm, in the sense that it requires exploring 5 nodes. Had we explored node $3\left( {{x}_{31} = 0}\right)$ prior to node $2\left( {{x}_{13} = 0}\right)$ , we would have encountered the upper bound $z = {16}$ units, and concluded that branching at node 2, with $z = {17}$ , cannot lead to a better solution, thus eliminating the need to explore nodes 4 and 5.

Generally, there are no exact rules for selecting the best search sequence, save some rules of thumb. For example, at a given node we can start with the branch having the largest ${d}_{ij}$ among all the created branches. The hope is that the elimination of the largest tour leg would lead to a tour with a smaller length. In Example 11.3-1, this rule would have given priority to node 3 over node 2 because ${d}_{31}\left( { = 4}\right)$ is larger than ${d}_{13}\left( { = 3}\right)$ , as desired. Another rule calls for sequencing the exploration of the nodes horizontally (rather vertically), that is, breadth before depth. The idea is that nodes closer to the starting node are more likely to produce tighter upper bounds because the number of additional constraints (of the type ${x}_{ij} = 0$ ) is smaller. This rule also would have produced the computationally efficient search $1 \rightarrow  2 \rightarrow  3$ .

2. The heuristics in Sections 11.4 and 11.5 can enhance the computational efficiency of the B&B algorithm by providing a "tight" upper bound. For example, the nearest-neighbor heuristic in Section 11.4.1 yields the tour 1-3-4-2-5-1 with length $z = {16}$ . This tight upper bound would have immediately eliminated the need to explore node 2 (the distance matrix is all integer, thus no better solution can be found at node 2).

## AMPL Moment

Interactive AMPL commands are ideal for the implementation of the TSP B&B algorithm using the general assignment model file amplAssign.txt. The data of the problem is given in file Ex11.3-1.txt. The file solutionAssign.txt solves and displays the solution. The following

table summarizes the AMPL commands needed to create the B&B tree in Figure 11.2 (Example 11.3-1) interactively:

<table><tr><td>AMPL commands</td><td>Result</td></tr><tr><td>ampl: model amplAssign.txt;data Ex11.3-1.txt; commands solutionAssign.txt;</td><td>Node 1 solution</td></tr><tr><td>ampl: fix x [1,3] :=0;commands <br> solutionAssign.txt;</td><td>Node 2 solution</td></tr><tr><td>rpl: fix x [2,5]:=0;commands solutionAssign.txt;</td><td>Node 4 solution</td></tr><tr><td>ampl: unfix x[2,5]; fix x[5,2]:=0; commands solutionAssign.txt;</td><td>Node 5 solution</td></tr><tr><td>ampl: unfix $x\left\lbrack  {5,2}\right\rbrack$ ; unfix $x\left\lbrack  {1,3}\right\rbrack$ ; fix $x\left\lbrack  {3,1}\right\rbrack   \mathrel{\text{ := }} 0$ ; commands solutionAssign.txt;</td><td>Node 3 solution</td></tr></table>

## TORA Moment

TORA can also be used to generate the B&B tree. Start with the assignment model at node 1. The branch condition ${x}_{ij} = 0$ is effected by using Solve/Modify Input Data to change the upper bound on ${x}_{ij}$ to zero.

#### 11.3.2 Cutting-Plane Algorithm

In the cutting-plane algorithm, a set of constraints is added to the assignment problem to exclude subtour solutions. Define a continuous variable ${u}_{j}\left( { \geq  0}\right)$ for city $j = 2,3,\ldots$ , and $n$ . The desired additional constraints (cutting planes) are

$$
{u}_{i} - {u}_{j} + n{x}_{ij} \leq  n - 1, i = 2,3,\ldots , n;j = 2,3,\ldots , n;i \neq  j
$$

The addition of these cuts to the assignment model produces a mixed integer linear program with binary ${x}_{ij}$ and continuous ${u}_{j}$ .

Example 11.3-2

Consider the following distance matrix of a 4-city TSP problem:

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix}  - & {13} & {21} & {26} \\  {10} &  - & {29} & {20} \\  {30} & {20} &  - & 5 \\  {12} & {30} & 7 &  -  \end{matrix}\right)
$$

The complete mixed integer problem consists of the assignment model and the additional constraints in Table 11.3. All ${x}_{ij} = \left( {0,1}\right)$ and all ${u}_{j} \geq  0$ .

The optimum solution is ${u}_{2} = 0,{u}_{3} = 2,{u}_{4} = 3,{x}_{12} = {x}_{23} = {x}_{34} = {x}_{41} = 1$ . The corresponding tour is 1-2-3-4-1 with length 59 . The solution satisfies all the additional constraints. (Verify!)

To demonstrate that the given optimum solution cannot satisfy a subtour solution, consider the subtour $\left( {1 - 2 - 1,3 - 4 - 3}\right)$ , or ${x}_{12} = {x}_{21} = 1,{x}_{34} = {x}_{43} = 1$ . The optimum values ${u}_{2} = 0,{u}_{3} = 2$ , and ${u}_{4} = 3$ together with ${x}_{43} = 1$ do not satisfy constraint $6,4{x}_{43} + {u}_{4} - {u}_{3} \leq  3$ , in Table 11.3. [Convince yourself that the same conclusion is true for other subtour solutions, such as (3-2-3, 1-4-1).]

TABLE 11.3 Cuts for Excluding Subtours in the Assignment Model of Example 11.3-2

<table><tr><td>No.</td><td>${x}_{11}$</td><td>${x}_{12}$</td><td>${x}_{13}$</td><td>${x}_{14}$</td><td>${x}_{21}$</td><td>${x}_{22}$</td><td>${x}_{23}$</td><td>${x}_{24}$</td><td>${x}_{31}$</td><td>${x}_{32}$</td><td>${x}_{33}$</td><td>${x}_{34}$</td><td>${x}_{41}$</td><td>${x}_{42}$</td><td>${x}_{43}$</td><td>${x}_{44}$</td><td>${u}_{2}$</td><td>${u}_{3}$</td><td>${u}_{4}$</td><td></td></tr><tr><td>1</td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>1</td><td>-1</td><td></td><td>≤3</td></tr><tr><td>2</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>1</td><td></td><td>-1</td><td>≤3</td></tr><tr><td>3</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td></td><td></td><td></td><td></td><td>-1</td><td>1</td><td></td><td>≤3</td></tr><tr><td>4</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td></td><td></td><td></td><td>1</td><td>-1</td><td>≤3</td></tr><tr><td>5</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td>-1</td><td></td><td>1</td><td>≤3</td></tr><tr><td>6</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>4</td><td></td><td></td><td>-1</td><td>1</td><td>≤3</td></tr></table>

The disadvantage of the cutting-plane model is that the size of the resulting mixed integer linear program grows exponentially with the number of cities, making the model computationally intractable. When this happens, the only recourse is to use either the B&B algorithm or one of the heuristics in Sections 11.4 and 11.5.

## AMPL Moment

A general AMPL model of the cutting-plane algorithm is given in file amplCut.txt. The 4-city TSP of Example 11.3-2 uses the following AMPL commands:

model amplCut.txt; data Ex11.3-2.txt; commands SolutionCut.txt;

The output is presented in the following convenient format:

---

Optimal tour length = 59.00

Optimal tour: 1- 2- 3- 4- 1

---

### 11.4 LOCAL SEARCH HEURISTICS

This section presents two local search heuristics for TSP: nearest-neighbor and reversal. Local search heuristics terminate at a local optimum. One way to improve the quality of the solution is to repeat the search using randomly generated starting tours. Another option is to use metaheuristics, whose basic idea is to escape entrapment at a local optimum. The metaheuristics will be covered in Section 11.5.

#### 11.4.1 Nearest-Neighbor Heuristic

As the name suggests, a TSP solution can be found by starting with a city (node) and then connecting it to the closest unlinked city (break ties arbitrarily). The just-added city is then linked to its nearest unlinked city. The process continues until a tour is formed.

Example 11.4-1

The matrix below summarizes the distances in miles in a 5-city TSP.

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {120} & {220} & {150} & {210} \\  {120} & \infty & {100} & {110} & {130} \\  {220} & {80} & \infty & {160} & {185} \\  {150} & \infty & {160} & \infty & {190} \\  {210} & {130} & {185} & \infty & \infty  \end{matrix}\right)
$$

The heuristic can start from any of the five cities. Each starting city may lead to a different tour. Table 11.4 provides the steps of the heuristic starting at city 3. (Distances for previously selected cities are replaced with -).

The resulting tour, 3-2-4-1-5-3, has a total length of 80 + 110 + 150 + 210 + 185 = 735 miles. Observe that the quality of the solution depends on the selection of the starting city. For example, starting from city 1, the resulting tour is 1-2-3-4-5-1 with length 780 miles (try it!). A better solution may thus be found by repeating the heuristic starting with different cities.

#### 11.4.2 Reversal Heuristic

In an $n$ -city TSP, the reversal heuristic attempts to improve a current tour by reversing the order of nodes of an open subtour (a subtour is open if it is missing exactly one leg). For example, consider tour 1-3-5-2-4-1 in Figure 11.3. Reversal of open subtour 3-5-2 produces the new tour 1-2-5-3-4-1 by deleting legs 1-3 and 2-4 and adding legs 1-2 and 3-4, as Figure 11.3 shows. The smallest number of reversed subtour is 2 (e.g.,3-5 or 5-2). The largest number is $n - 2$ if the distance matrix is symmetric and $n - 1$ if it is asymmetric. ${}^{3}$ The heuristic scans all reversals in search for a better tour.

The length of the starting tour in the reversal heuristic need not be finite (i.e., it could have missing legs). Indeed, starting with a finite-length tour does not appear to offer a particular advantage regarding the quality of the final solution (see Problem 11-24, for an illustration).

TABLE 11.4 Steps of the Nearest-Neighbor Heuristic for Solving the TSP of Example 11.4-1

<table><tr><td>Step</td><td>Action</td><td>Tour construction</td></tr><tr><td>1</td><td>Start at city 3</td><td>3</td></tr><tr><td>2</td><td>City 2 is closest to city 3 $\left( {{d}_{32} = \min \{ {220},\mathbf{{80}},\infty ,{160},{185}\} }\right.$ )</td><td>3-2-4</td></tr><tr><td>3</td><td>City 4 is closest to city $2\left( {{d}_{24} = \min \{ {120},\infty ,-,{110},{130}\} }\right)$</td><td>3-2-4</td></tr><tr><td>4</td><td>City 1 is closest to city $4\left( {{d}_{41} = \min \{ {150},\infty ,-,-, - ,{190}\} }\right)$</td><td>3-2-4-1</td></tr><tr><td>5</td><td>City 5 is closest to city $1\left( {{d}_{15} = \min \{ \infty , - ,-,-, - ,{210}\} }\right)$</td><td>3-2-4-1-5</td></tr><tr><td>6</td><td>Add city 3 to complete the tour</td><td>3-2-4-1-5-3</td></tr></table>

---

${}^{3}$ In a symmetric distance matrix, the $\left( {n - 1}\right)$ -city subtour reversal does not produce a different tour. For example, reversing 2-4-5-3 in the tour 1-2-4-5-3-1 yields the identical tour 1-3-5-4-2-1 when the distance matrix is symmetric $\left( {{d}_{ij} = {d}_{ji}}\right.$ , for all $i$ and $\left. j\right)$ . This may not be true in the asymmetric case because legs $i - j$ and $j - i$ may not be equal.

---

![bo_d56m4sref24c73bhe60g_12_411_200_488_378_0.jpg](bo_d56m4sref24c73bhe60g_12_411_200_488_378_0.jpg)

FIGURE 11.3

Subtour reversal 3-5-2 in tour 1-3-5-2-4-1 produces tour 1-2-5-3-4-1 by deleting legs 1-3 and 2-4 and adding legs 1-2 and 3-4

Example 11.4-2

Consider the TSP of Example 11.4-1. The (self-explanatory) reversal steps are carried out in Table 11.5 starting with an arbitrary tour 1-4-3-5-2-1 of length 745 miles.

The four-at-a-time reversal is investigated because the distance matrix is asymmetric. Also, none of the reversals can include the home city of the initial tour (= 1 in this example) as this will not yield a feasible tour. For example, the reversal 1-4 leads to 4-1-3-5-2-1, which is not a tour.

The solution determined by the reversal heuristic is a function of the starting tour. For example, if we start with 2-3-4-1-5-2 with length 750 miles, the heuristic produces a different tour: 2-5-1-4-3-2 with length 730 miles (verify!). For this reason, the quality of the solution can be improved if the heuristic is repeated with different starting tours.

## Excel Moment

Figure 11.4 provides a general Excel spreadsheet (file excelReversalTSP.xls) using the rules given above (a subset of the model provides the nearest-neighbor solution-see options 1 and 4 given below). The distance matrix may be entered manually, or it may be populated randomly (symmetric or asymmetric) with specified density. The heuristic automatically checks for matrix symmetry and adjusts the maximum reversal level accordingly. It also automates four options for the starting tour:

1. Option all applies the nearest-neighbor heuristic using each of the cities as a starting point. The best amongst the resulting tours is then used to start the reversal heuristic.

2. Option tour allows the use of a specific starting tour.

3. Option random generates a random starting tour.

4. Option specific city number applies the nearest-neighbor heuristic starting at the designated city.

TABLE 11.5 Application of the Reversal Heuristic to the TSP of Example 11.4-1.

<table><tr><td>Type</td><td>Reversal</td><td>Tour</td><td>Length</td></tr><tr><td>Start</td><td>-</td><td>(1-4-3-5-2-1)</td><td>745</td></tr><tr><td rowspan="3">Two-at-a-time <br> reversal</td><td>4-3</td><td>1-3-4-5-2-1</td><td>820</td></tr><tr><td>3-5</td><td>(1-4-5-3-2-1)</td><td>725</td></tr><tr><td>5-2</td><td>1-4-3-2-5-1</td><td>730</td></tr><tr><td rowspan="2">Three-at-a-time reversal</td><td>4-3-5</td><td>1-5-3-4-2-1</td><td>00</td></tr><tr><td>3-5-2</td><td>1-4-2-5-3-1</td><td>00</td></tr><tr><td>Four-at-a-time reversal</td><td>4-3-5-2</td><td>1-2-5-3-4-1</td><td>745</td></tr></table>

![bo_d56m4sref24c73bhe60g_13_375_207_1121_468_0.jpg](bo_d56m4sref24c73bhe60g_13_375_207_1121_468_0.jpg)

FIGURE 11.4

Execution of the TSP heuristic using Excel spreadsheet (file excelReversalTSP.xls)

## Aha! Moment: TSP Computational Experience, or How to Reproduce Leonardo da Vinci's Mona Lisa! ${}^{4}$

TSP has been in circulation since the nineteenth century. But interest in solving the problem did not start in earnest until G. Dantzig, R. Fulkerson, and S. Johnson (1954) developed an LP-based algorithm for determining the optimal (shortest) tour for visiting 49 cities in the continental United States. Lacking computers then, the problem was solved by hand (it took only a few weeks, the horror!). ${}^{5}$ Since then, and with the advent of modern computing, much larger instances were solved culminating in 2004 with the optimal tour of 24,978 cities in Sweden.

In a different application setting, TSP was used in the mid-1980s at Bell Labs to manufacture a computer chip that required laser-vaporization of 85,900 interconnections of simple logic gates. The goal was to move the laser on the chip from one location to the next tracing the shortest tour (smallest total travel distance). Attempts to find the solution started in 1991 and culminated in 2006 with the optimum tour. Amazingly, this 15-year "crusade" has resulted in less than .1% (0.0923%, to be exact) reduction in the length of the tour found in 1991. In a practical sense, it would appear that the 1991 solution is just as good as that of 2006. On the other hand, academic posturing demands nothing but the best!

Another application from the world of art is the reproduction of Leonardo da Vinci's Mona Lisa using a continuous-line drawing among stipples (dots) characterizing the original painting (where shades of darkness are mimicked by how close or far apart the stipples are). An instance of $n$ dots representing the relative locations of these stipples completely defines the associated TSP. In 2009, a challenge was made to solve the Mona Lisa instance using $n = {100},{000}$ stipples. Since then, the gap relative to a lower bound on the shortest length of the tour (computed by an LP relaxation of the TSP) was reduced from 2212 distance units to 107 as of 2012. When the optimal of the Mona Lisa TSP is eventually found, the problem will be the largest ever attempted. And the race continues!

---

${}^{4}$ http://www.math.uwaterloo.ca/tsp/index.html, accessed 05-10-2015,2:33P.M.

${}^{5}$ For the sake of comparison, a 49-city instance can now be solved in a split second using Concorde TSP Solver. For information about Concorde, refer to the University of Waterloo website, op. cit.

---

### 11.5 METAHEURISTICS

The drawback of the local search heuristics in Section 11.4 is possible entrapment at a local optimum. Metaheuristics, as explained in Chapter 10, are designed to alleviate this problem. This section details the application of tabu, simulated annealing, and genetic search to TSP. It is recommended that you review related material in Chapter 10 before proceeding with the rest of this chapter.

#### 11.5.1 TSP Tabu Algorithm

As explained in Section 10.3.1, tabu search escapes entrapment at local optima by permitting inferior search moves. A tabu list prevents repeating previously encountered solutions during a specified number of successive iterations, called tenure period. A tabu move can be accepted if it leads to an improved solution. For the TSP model, the elements of the tabu search are defined as follows:

1. Starting tour. Four options are available: (a) a specific tour, (b) a specific starting city for a tour constructed by the nearest-neighbor heuristic (Section 11.4.1), (c) the best among all tours constructed by the nearest-neighbor heuristic using each of cities $1,2,\ldots$ , and $n$ as a starting point, and (d) a random tour.

2. Subtour reversal. Two added tour legs replace two deleted ones to produce a new tour (see Section 11.4.2 for details).

3. Neighborhood at iteration i. All tours (including infeasible ones with infinite length) generated by applying subtour reversals to tour $i$ .

4. Tabu move. A reversal tour is tabu if both of its deleted legs are on the tabu list.

5. Next move at iteration $i$ . Identify the shortest tour in neighborhood $i$ and select it as the next move if it is non-tabu, or if it is tabu but yields a better solution. Else, exclude the shortest (tabu) tour and repeat the test with the next shortest neighborhood tour.

6. Tabu tenure period $\tau$ at iteration $i$ . The tenure period is the (random or deterministic) number of successive iterations a tabu element stays on the tabu list.

7. Changes in tabu list at iteration $i$ . Reversal legs defining tour $i$ from tour $i - 1$ are added to the list. Tour legs completing tenure (those that entered the list at iteration $i - \tau  + 1$ ) are deleted from the list.

## Example 11.5-1

We will use the distance matrix of Example 11.4-1 to demonstrate the application of the tabu metaheuristic.

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {120} & {220} & {150} & {210} \\  {120} & \infty & {100} & {110} & {130} \\  {220} & {80} & \infty & {160} & {185} \\  {150} & \infty & {160} & \infty & {190} \\  {210} & {130} & {185} & \infty & \infty  \end{matrix}\right)
$$

Assume a tabu tenure $\tau  = 2$ iterations and use 1-2-3-4-5-1 of length 780 as the starting tour.

Table 11.6 provides five iterations. In iterations 1, 2, and 3, the shortest tours are non-tabu. In iteration 4, the shortest tour, 1-4-3-5-2-1 of length 745, is tabu because the reversal requires deleting legs 4-5 and 3-2, and both are on the tabu list. Since the (tabu) tour is not better than the best recorded solution (tour 1-4-5-3-2-1 of length 725 in iteration 3), the next shortest tour, 1-4-5-2-3-1 of length 790, which happens to be non-tabu, defines the next move.

In iteration 5, the two tours 1-4-5-3-2-1 (length = 725) and 1-4-3-2-5-1 (length = 730) are tabu (and neither provides a better tour). The next best tour in the neighborhood, 1-4-2-5-3-1 (of infinite length), is non-tabu and hence represents the next move. Note that only one deleted leg (4-5) in the selected tour 1-4-2-5-3-1 appears on the tabu list, which is not sufficient to declare the tour tabu because both deleted legs must be on the list. Note also that the top tour 1-5-4-2-3-1 (of infinite length) is not selected because it is missing two legs, compared with one missing leg in the selected tour, 1-4-2-5-3-1.

TABLE 11.6 Tabu Heuristic Solution of Example 11.5-1 with Tenure Period $\tau  = \mathbf{2}$ Iterations

<table><tr><td>Iteration</td><td>Reversal</td><td>Tour</td><td>Length (miles)</td><td>Delete</td><td>Add</td><td>Tabu list $\left( {t = 2}\right)$</td></tr><tr><td>0</td><td>-</td><td>1-2-3-4-5-1</td><td>780</td><td></td><td></td><td>-</td></tr><tr><td rowspan="6">1</td><td>2-3</td><td>1-3-2-4-5-1</td><td>810</td><td></td><td></td><td></td></tr><tr><td>3-4</td><td>1-2-4-3-5-1</td><td>785</td><td></td><td></td><td></td></tr><tr><td>4-5</td><td>1-2-3-5-4-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>2-3-4</td><td>1-4-3-2-5-1</td><td>730</td><td>1-2, 5-4</td><td>1-4, 2-5</td><td>1-4, 2-5</td></tr><tr><td>3-4-5</td><td>1-2-5-4-3-1</td><td>00</td><td></td><td></td><td></td></tr><tr><td>2-3-4-5</td><td>1-5-4-3-2-1</td><td>00</td><td></td><td></td><td></td></tr><tr><td rowspan="6">2</td><td>4-3</td><td>1-3-4-2-5-1</td><td>00</td><td></td><td></td><td></td></tr><tr><td>3-2</td><td>1-4-2-3-5-1</td><td>00</td><td></td><td></td><td></td></tr><tr><td>2-5</td><td>1-4-3-5-2-1</td><td>745</td><td>3-2, 5-1</td><td>3-5, 2-1</td><td>1-4, 2-5, 3-5, 2-1</td></tr><tr><td>4-3-2</td><td>1-2-3-4-5-1</td><td>780</td><td></td><td></td><td></td></tr><tr><td>3-2-5</td><td>1-4-5-2-3-1</td><td>790</td><td></td><td></td><td></td></tr><tr><td>4-3-2-5</td><td>1-5-2-3-4-1</td><td>750</td><td></td><td></td><td></td></tr><tr><td rowspan="6">3</td><td>4-3</td><td>1-3-4-5-2-1</td><td>820</td><td></td><td></td><td></td></tr><tr><td>3-5</td><td>1-4-5-3-2-1</td><td>725</td><td>4-3, 5-2</td><td>4-5, 3-2</td><td>3-5, 2-1, 4-5, 3-2</td></tr><tr><td>5-2</td><td>1-4-3-2-5-1</td><td>730</td><td></td><td></td><td></td></tr><tr><td>4-3-5</td><td>1-5-3-4-2-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>3-5-2</td><td>1-4-2-5-3-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>4-3-5-2</td><td>1-2-5-3-4-1</td><td>745</td><td></td><td></td><td></td></tr><tr><td rowspan="6">4</td><td>4-5</td><td>1-5-4-3-2-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>5-3</td><td>1-4-3-5-2-1</td><td>745</td><td>4-5, 3-2</td><td>-</td><td>Tabu</td></tr><tr><td>3-2</td><td>1-4-5-2-3-1</td><td>790</td><td>5-3, 2-1</td><td>5-2, 3-1</td><td>4-5, 3-2, 5-2, 3-1</td></tr><tr><td>4-5-3</td><td>1-3-5-4-2-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>5-3-2</td><td>1-4-2-3-5-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>4-5-3-2</td><td>1-2-3-5-4-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td rowspan="6">5</td><td>4-5</td><td>1-5-4-2-3-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>5-2</td><td>1-4-2-5-3-1</td><td>60</td><td>4-5, 2-3</td><td>4-2, 5-3</td><td>5-2, 3-1, 4-2, 5-3</td></tr><tr><td>2-3</td><td>1-4-5-3-2-1</td><td>725</td><td>5-2, 3-1</td><td>-</td><td>Tabu</td></tr><tr><td>4-5-2</td><td>1-2-5-4-3-1</td><td>$\infty$</td><td></td><td></td><td></td></tr><tr><td>5-2-3</td><td>1-4-3-2-5-1</td><td>730</td><td>4-5, 3-1</td><td>-</td><td>Tabu</td></tr><tr><td>4-5-2-3</td><td>1-3-2-5-4-1</td><td>$\infty$</td><td></td><td></td><td></td></tr></table>

## Excel Moment

Figure 11.5 presents the Excel spreadsheet (file excelTabuTSP.xls) for applying tabu search to the TSP model. To facilitate experimentation, symmetric or asymmetric TSPs can be generated randomly. Also, the initial tour can be specified either deterministically or randomly. The on/off buttons (row 6 of the spreadsheet) reveal/suppress the details of the iterations, including changes in the tabu list.

## FIGURE 11.5

TSP tabu metaheuristic using Excel spreadsheet (file excelTabuTSP.xls)

<table><tr><td></td><td>A</td><td>B</td><td>C</td><td>D</td><td>E</td><td></td><td>F</td><td></td><td>G</td><td>H</td></tr><tr><td>1</td><td colspan="10">Traveling Salesperson Tabu Heuristic</td></tr><tr><td>2</td><td colspan="3">Input steps: (See comment in cell A4)</td><td colspan="7">Output steps: (See comments in cells D4, D6, and G3)</td></tr><tr><td>3</td><td>Step 1:</td><td>Nbr of cities=</td><td>5</td><td>Steps 3a&b:</td><td colspan="2">Nbr of iters=</td><td colspan="2">20</td><td>Tenure period=</td><td>[1, 6]</td></tr><tr><td>4 <br> 5</td><td>Step 2:</td><td colspan="2">Format input area</td><td>Steps 4a&b:</td><td>Start <br> option:</td><td colspan="2">tour</td><td>-</td><td colspan="2">Execute heuristic</td></tr><tr><td>6</td><td colspan="3">Iteration calculations: © ON ○ OFF</td><td>Next move:</td><td colspan="4">Bestreversal -</td><td colspan="2">(Best local optimum in red)</td></tr><tr><td>7</td><td>Start city</td><td colspan="8">Tour</td><td>Length</td></tr><tr><td>8</td><td>initial</td><td colspan="8">$1 - 2 - 3 - 4 - 5 - 1$</td><td>780</td></tr><tr><td>9</td><td>Iteration 1</td><td colspan="8"></td><td></td></tr><tr><td>10</td><td>2-3</td><td colspan="8">1-3-2-4-5-1</td><td>810</td></tr><tr><td>11</td><td>3-4</td><td colspan="8">$1 - 2 - 4 - 3 - 5 - 1$</td><td>785</td></tr><tr><td>12</td><td>4-5</td><td colspan="8">$1 - 2 - 3 - 5 - 4 - 1$</td><td>1E+10</td></tr><tr><td>13</td><td>2-3-4</td><td colspan="8">$1 - 4 - 3 - 2 - 5 - 1$</td><td>730</td></tr><tr><td>14</td><td>3-4-5</td><td colspan="8">$1 - 2 - 5 - 4 - 3 - 1$</td><td>1E+10</td></tr><tr><td>15</td><td>2-3-4-5</td><td colspan="8">1-5-4-3-2-1</td><td>1E+10</td></tr></table>

![bo_d56m4sref24c73bhe60g_16_334_1342_902_746_0.jpg](bo_d56m4sref24c73bhe60g_16_334_1342_902_746_0.jpg)

#### 11.5.2 TSP Simulated Annealing Algorithm

Section 10.3.2 explains that at any iteration in simulated annealing, a no-worse neighborhood solution is always accepted as the next move. If no such solution exists, the search can move to an inferior neighborhood solution conditionally if

$$
R < {e}^{\left( \frac{{L}_{\text{ cur }} - {L}_{\text{ next }}}{T}\right) }
$$

where

$$
R = \left( {0,1}\right) \text{ Random number }
$$

$$
{L}_{\text{ cur }} = \text{ Tour length at current iteration }
$$

$$
{L}_{\text{ next }} = \text{ (Inferior) Tour length at next iteration }\left( { > {L}_{\text{ cur }}}\right)
$$

$$
T = \text{ Temperature }
$$

The temperature $T$ assumes smaller values as the number of search iterations increases, thus decreasing the value of ${e}^{\left( \frac{{L}_{\text{ cur }} - {L}_{\text{ next }}}{T}\right) }$ , rendering a more selective search. Also, the acceptance measure favors moves whose objective value, ${L}_{\text{ next }}$ , is closer to the current objective value, ${L}_{\text{ cur, because it }}$ increases the value of ${e}^{\left( \frac{{L}_{\text{ cur }} - {L}_{\text{ next }}}{T}\right) }$ .

The principal components of simulating annealing are as follows:

1. Starting tour. Four options are available: (a) A specific tour, (b) a specific starting city for a tour constructed by the nearest-neighbor heuristic (Section 11.4.1), (c) the best among all tours constructed by the nearest-neighbor heuristic using each of cities $1,2,\ldots$ , and $n$ as a starting point, and (d) a random tour.

2. Subtour reversal. Two added tour legs replace two deleted legs to produce a new tour (see Section 11.4.2 for details).

3. Temperature schedule. $\left\{  {{T}_{k}, k = 0,1,\ldots }\right\}  ,{T}_{0} =$ starting temperature, ${T}_{k} = \; {r}_{k}{T}_{k - 1},0 < {r}_{k} < 1, k = 1,2,\ldots$ , with the change from one temperature to the next taking place every $t$ accept-iterations.

4. Neighborhood at iteration i. All tours (including infeasible ones with infinite length) generated from applying subtour reversals (Section 11.4.2) to tour $i$ .

5. Next move at iteration $i$ . Select the subtour reversal that is no worse than the current best tour; else, scan tours in neighborhood $i$ in ascending order of tour length until a move is accepted (using the probability measure).

## Example 11.5-2

We will use the distance matrix of Example 11.4-1 to demonstrate the application of simulated annealing metaheuristic.

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {120} & {220} & {150} & {210} \\  {120} & \infty & {100} & {110} & {130} \\  {220} & {80} & \infty & {160} & {185} \\  {150} & \infty & {160} & \infty & {190} \\  {210} & {130} & {185} & \infty & \infty  \end{matrix}\right)
$$

Assume the temperature schedule ${T}_{k} = {.5}{T}_{k - 1}$ with ${T}_{0} = {50}$ . A change fom ${T}_{k - 1}$ to ${T}_{k}$ takes place every two accept-iterations. The example starts with the infeasible (infinite length) tour 3-2-5-4-1-3.

TABLE 11.7 Simulated Annealing Solution of Example 11.5-2 with ${T}_{k} = {.5}{T}_{k - 1},{T}_{0} = {50}$ , and Change from ${T}_{k - 1}$ to ${T}_{k}$ Taking Place Every Two Accept-Iterations

<table><tr><td>Iteration</td><td>Reversal</td><td>Tour</td><td>Length (miles)</td><td>${L}_{\mathrm{{cur}}}$</td><td>${L}_{\text{ next }}$</td><td>$T$</td><td>$p = {e}^{\left( \frac{{L}_{\mathrm{{cur}}} - {L}_{\mathrm{{next}}}}{T}\right) }$</td><td>$R$</td><td>Decision</td></tr><tr><td>0</td><td>-</td><td>3-2-5-4-1-3</td><td>$\infty$</td><td>$\infty$</td><td></td><td>50</td><td>-</td><td></td><td>-</td></tr><tr><td>1</td><td>2-5</td><td>3-5-2-4-1-3</td><td>795</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td>5-4</td><td>3-2-4-5-1-3</td><td>810</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td>4-1</td><td>3-2-5-1-4-3</td><td>730</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td>2-5-4</td><td>3-4-5-2-1-3</td><td>820</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td>5-4-1</td><td>3-2-1-4-5-3</td><td>725</td><td>$\infty$</td><td>725</td><td>50</td><td>-</td><td></td><td>Accept move, ${L}_{\text{ next }} < {L}_{\text{ cur }}$</td></tr><tr><td></td><td>2-5-4-1</td><td>3-1-4-5-2-3</td><td>790</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td rowspan="7">2</td><td>2-1</td><td>3-1-2-4-5-3</td><td>825</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td>1-4</td><td>3-2-4-1-5-3</td><td>735</td><td>725</td><td>735</td><td>50</td><td>.8187</td><td>.8536</td><td>Reject move, $R > p$</td></tr><tr><td>4-5</td><td>3-2-1-5-4-3</td><td>$\infty$</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td>2-1-4</td><td>3-4-1-2-5-3</td><td>745</td><td>725</td><td>745</td><td>50</td><td>.6703</td><td>.3701</td><td>Accept move, $R < p$</td></tr><tr><td>1-4-5</td><td>3-2-5-4-1-3</td><td>$\infty$</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td>2-1-4-5</td><td>3-5-4-1-2-3</td><td>$\infty$</td><td></td><td></td><td>50</td><td></td><td></td><td></td></tr><tr><td></td><td></td><td>00</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td rowspan="6">3</td><td>4-1</td><td>3-1-4-2-5-3</td><td>0</td><td></td><td></td><td>25</td><td></td><td></td><td></td></tr><tr><td>1-2</td><td>3-4-2-1-5-3</td><td>00</td><td></td><td></td><td>25</td><td></td><td></td><td></td></tr><tr><td>2-5</td><td>3-4-1-5-2-3</td><td>750</td><td></td><td></td><td>25</td><td></td><td></td><td></td></tr><tr><td>4-1-2</td><td>3-2-1-4-5-3</td><td>725</td><td>745</td><td>725</td><td>25</td><td></td><td></td><td>Accept move, ${L}_{\text{ next }} < {L}_{\text{ cur }}$</td></tr><tr><td>1-2-5</td><td>3-4-5-2-1-3</td><td>820</td><td></td><td></td><td>25</td><td></td><td></td><td></td></tr><tr><td>4-1-2-5</td><td>3-5-2-1-4-3</td><td>745</td><td></td><td></td><td>25</td><td></td><td></td><td></td></tr></table>

Table 11.7 details the computations for three iterations. The best reversal move 5-4-1 in iteration 1 is accepted because it yields a better tour length $\left( {{L}_{\text{ next }} = {725}}\right.$ versus $\left. {{L}_{\text{ cur }} = \infty }\right)$ . This means that tour 3-2-1-4-5-3 is the best solution available so far. Iteration 2 produces inferior moves, meaning that the previous move, 5-4-1 in iteration 1, is a local minimum. Hence, we scan all the tours in iteration 2 in ascending order of tour length until a tour is accepted (if all tours are rejected, either the scan is repeated using a new round of random numbers or the search ends). Move 1-4 with a tour length of 735 is rejected because $R = {.8536}$ is larger than $p = {e}^{\left( \frac{{725} - {735}}{50}\right) } = {.8187}$ . The next-in-order move,2-1-4, with tour length of 745 is accepted because $R = {.3701}$ is less than $p = {e}^{\left( \frac{{725} - {745}}{50}\right) } = {.6703}$ .

At iteration 3, two accept-iterations have been realized at iterations 1 and 2. Hence, the temperature is changed from 50 to ${.5}\left( {50}\right)  = {25}$ . The iterative process then continues until a terminating condition takes place.

## Excel Moment

Figure 11.6 provides a snapshot of simulated annealing application to TSP (file excelSimu-latedAnnealingTSP.xls). The spreadsheet follows the general layout of the tabu spreadsheet in Figure 11.5.

A B C D E F G H

1 Traveling Salesperson Simulated Annealing Heuristic

2 Input steps: (See comment in cell A5) Output steps: (See comments in cells D4, D5, and D6)

3 Steps 3a&b: Nbr of iters= 50 TempAcceptIters 4

Step 1: Nbr of cities= 5

4 Steps 4a&b: Initial temp= 50 Reduction ratio= 0.5

Execute heuristic

5

Step 2: Format input area Steps 5a&b:

Start tour

-

option: 6

7 Iteration calculations: ON ○ OFF Next move: Bestreversal - GREEN = Accept, RED = Reject

8 Start city Tour Length

9 initial 3-2-5-4-1-3 1E+10

10 Iter 1 reversals

11 2-5 3-5-2-4-1-3 795

12 5-4 3-2-4-5-1-3 810

13 4-1 3-2-5-1-4-3 730

14 2-5-4 3-4-5-2-1-3 820

15 5-4-1 3-2-1-4-5-3 725

16 2-5-4-1 3-1-4-5-2-3 790

1 J K L M N 0 Q

1

2 Check here if symmetric Enter density: 0.9 (blank cell $= \infty$ )

3 Click to populate DISTANCE matrix randomly in the range (1, 100)

4 1 2 3 4 5

5 1 120 220 150 210

6 2 120 100 110 130

7 3 220 80 160 185

8 4 150 160 190

9 5 210 130 185

10 Step 4c: Enter initial tour (if TOUR option is selected in Step 5a):

11 1 3

12 Search best tour found at iteration 1

13 Tour length: 725

14 Tour: 3-2-1-4-5-3

FIGURE 11.6

TSP simulated annealing metaheuristic using Excel spreadsheet (file excelSimulatedAnnealingTSP.xls)

#### 11.5.3 TSP Genetic Algorithm

In the genetic metaheuristic introduced in Section 10.3.3, two parents are selected from a population to create two children. The children then become parents themselves replacing the two least fit (in terms of tour length) parents in the population. The process of creating children and of retiring parents is repeated until a termination condition is reached.

The following is a description of the main elements of the genetic metaheuristic as it applies to the TSP.

1. Gene coding. The coding can be binary or numeric. The literature presents heuristics based on both types of coding. This presentation adopts the direct numeric tour code (e.g., 1-2-5-4-3-1).

2. Initial population. The first step is to identify the sets of outgoing nodes from each node in the network that can be reached by a finite tour leg. Starting from a specific (home) node, a tour is constructed by adding in the rightmost position a unique nonredundant node selected from among all the outgoing nodes of the last-added node. If a point is reached where no unique outgoing node exists, the entire process is repeated until a finite-length tour is found.

TABLE 11.8 Steps for Creating Children C1 and C2 from Parents P1 and P2 Using Order Crossover

<table><tr><td>Step</td><td>Action</td><td>Example (assume $n = 7$ nodes)</td></tr><tr><td>0</td><td>Select P1 and P2 from population.</td><td>P1 = 1-2-5-4-3-7-6 (link back to node 1) <br> P2 = 5-4-2-6-3-1-7 (link back to tour 5)</td></tr><tr><td>1</td><td>Randomly select two crossover points, ${c}_{1}$ and ${c}_{2}$ with ${c}_{1} < {c}_{2}$ .</td><td>$R = {.4425}$ yields ${c}_{1} = \operatorname{int}\left( {7 \times  {.3425}}\right)  + 1 = 3$ <br> $R = {.7123}$ yields ${c}_{2} = \operatorname{int}\left( {7 \times  {.7123}}\right)  + 1 = 5$</td></tr><tr><td>2</td><td>Swap positions $\left( {{c}_{1},{c}_{1} + 1,\ldots ,{c}_{2}}\right)$ in P1 and P2 to partially form C2 and C1, respectively.</td><td>C1 = ?-?-2-6-3-?-? <br> C2 = ?-?-5-4-3-?-?</td></tr><tr><td>3</td><td>Create list L1(L2) by rearranging the</td><td>L1 = (7,6,1,2,5,4,3)</td></tr><tr><td></td><td>elements of P1(P2) in the clockwise order <br> ${c}_{2} + 1,{c}_{2} + 2,\ldots , n,1,2,\ldots ,{c}_{2}$ .</td><td>$\mathrm{L}2 = \left( {1,7,5,4,2,6,3}\right)$</td></tr><tr><td>4</td><td>From L1 (L2), create ${\mathrm{{L1}}}^{\prime }\left( {\mathrm{{L2}}}^{\prime }\right)$ by deleting</td><td>$\mathrm{L}{1}^{\prime } = \mathrm{L}1 - \left( {2,6,3}\right)  = \left( {7,1,\mathbf{5},\mathbf{4}}\right)$</td></tr><tr><td></td><td>the nodes already assigned to C1(C2) in step 2 <br> while preserving the order in L1 and L2.</td><td>$\mathrm{L}{2}^{\prime } = \mathrm{L}2 - \left( {5,4,3}\right)  = \left( {\underline{1,7},\mathbf{2},\mathbf{6}}\right)$</td></tr><tr><td>5</td><td>Assign the elements of ${\mathrm{{L1}}}^{\prime }\left( {\mathrm{{L2}}}^{\prime }\right)$ to the</td><td>$\mathrm{C}1 = \mathbf{5} - \mathbf{4} - 2 - 6 - 3 - 7 - 1$ (link back to node 5)</td></tr><tr><td></td><td>missing elements in $\mathrm{C}1\left( {\mathrm{C}2}\right)$ in the order <br> ${c}_{2} + 1,{c}_{2} + 2,\ldots , n,1,2,\ldots ,{c}_{1} - 1$ .</td><td>C2 = 2-6-5-4-3-1-7 (link back to node 2)</td></tr></table>

The requirement stipulating that outgoing nodes be reached by finite links guarantees that the constructed tour is feasible (has a finite length). Unlike tabu and simulated annealing where a new search move can be infeasible, infeasible parent tours may never lead to the creation of feasible child tours. This result is particularly true when the distance matrix is sparse.

3. Child creation. The process starts by selecting two parents, P1 and P2, whose genes are swapped to create two children, C1 and C2. We will assume that P1 represents the best parent (in terms of tour length) and P2 the next best. There are numerous ways for gene swapping [see Larrañaga et al. (1999) for a list of 25 such procedures]. In this presentation, we will use the order crossover procedure, whose steps are explained in Table 11.8.

The proposed procedure for creating children may lead to infeasible tours (with missing legs). If this happens, the procedure should be repeated as necessary until offspring feasibility is realized.

4. Mutation. Mutation in child genes takes place with a small probability of about .1, interchanging the nodes of two randomly selected positions in the tour (excluding those of the home node). Random selection may be repeated to secure two distinct positions.

## Example 11.5-3

We will use the TSP of Example 11.4-1 to demonstrate the application of the genetic heuristic.

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {120} & {220} & {150} & {210} \\  {120} & \infty & {100} & {110} & {130} \\  {220} & {80} & \infty & {160} & {185} \\  {150} & \infty & {160} & \infty & {190} \\  {210} & {130} & {185} & \infty & \infty  \end{matrix}\right)
$$

The list of outgoing nodes can be determined from the distance matrix as

<table><tr><td>Node $i$</td><td>Outgoing nodes</td></tr><tr><td>1</td><td>$\{ 2,3,4,5\}$</td></tr><tr><td>2</td><td>$\{ 1,3,4,5\}$</td></tr><tr><td>3</td><td>$\{ 1,2,4,5\}$</td></tr><tr><td>4</td><td>$\{ 1,3,5\}$</td></tr><tr><td>5</td><td>$\{ 1,2,3\}$</td></tr></table>

Table 11.9 provides the details of iterations 1, 2, and 11. Iteration 11 provides the best solution (which also happens to be optimum). The intervening iterations were omitted to conserve space.

We demonstrate the determination of initial population (6 parents) in iteration 1 by considering parent 1. Starting with home node 1, node 4 is selected randomly from the outgoing node set $\{ 2,3,4,5\}$ . Next, the outgoing nodes from node 4 are $\{ 1,3,5\}  - \{ 1\}$ because $\{ 1\}$ is already in the partial tour. Selecting node 5 randomly yields the partial tour 1-4-5. The process is repeated until the full tour 1-4-5-2-3-1 is constructed. Keep in mind that if the construction of the tour is dead-ended (no new nodes can be added), then the entire process must be repeated anew. For example, tour construction cannot continue past partial tour 1-2-3-5 because there is no link from node 5 to (the only remaining) outgoing node 4.

TABLE 11.9 Genetic Algorithm Applied to TSP of Example 11.4-3

<table><tr><td>Iteration</td><td>Member</td><td>Tour</td><td>Crossovers</td><td>Length (miles)</td></tr><tr><td rowspan="8">1</td><td>1</td><td>1-4-5-2-3-1</td><td></td><td>790</td></tr><tr><td>2</td><td>3-2-4-5-1-3</td><td></td><td>810</td></tr><tr><td>3</td><td>1-2-4-5-3-1</td><td></td><td>825</td></tr><tr><td>(Parent 2) 4</td><td>2-5-3-4-1-2</td><td></td><td>745</td></tr><tr><td>5</td><td>3-4-5-1-2-3</td><td></td><td>780</td></tr><tr><td>(Parent 1) 6</td><td>1-5-3-2-4-1</td><td></td><td>735</td></tr><tr><td>Child 1</td><td>5-2-3-4-1-5</td><td>3 and 5</td><td>750</td></tr><tr><td>Child 2</td><td>5-1-3-2-4-5</td><td></td><td>810</td></tr><tr><td rowspan="8">2</td><td>1</td><td>1-4-5-2-3-1</td><td></td><td>790</td></tr><tr><td>2</td><td>5-1-3-2-4-5</td><td></td><td>810</td></tr><tr><td>3</td><td>5-2-3-4-1-5</td><td></td><td>750</td></tr><tr><td>(Parent 2) 4</td><td>2-5-3-4-1-2</td><td></td><td>745</td></tr><tr><td>5</td><td>3-4-5-1-2-3</td><td></td><td>780</td></tr><tr><td>(Parent 1) 6</td><td>1-5-3-2-4-1</td><td></td><td>735</td></tr><tr><td>Child 1</td><td>5-3-2-4-1-5</td><td>4 and 5</td><td>735</td></tr><tr><td>Child 2</td><td>5-3-1-2-4-5</td><td></td><td>825</td></tr><tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr><tr><td rowspan="8">11</td><td>(Parent 2) 1</td><td>1-5-3-2-4-1</td><td rowspan="8">3 and 4</td><td>735</td></tr><tr><td>2</td><td>5-3-2-4-1-5</td><td>735</td></tr><tr><td>3</td><td>5-3-2-4-1-5</td><td>735</td></tr><tr><td>4</td><td>5-3-2-4-1-5</td><td>735</td></tr><tr><td>(Parent 1) 5</td><td>4-5-3-2-1-4</td><td>725</td></tr><tr><td>6</td><td>5-3-2-4-1-5</td><td>735</td></tr><tr><td>Child 1</td><td>4-5-3-2-1-4</td><td>725</td></tr><tr><td>Child 2</td><td>1-5-3-2-4-1</td><td>735</td></tr></table>

In iteration 1, P1 = 1-5-3-2-4 and P2 = 2-5-3-4-1 because they are the two fittest parents (note that the definitions of P1 and P2 do not include the last elements 1 and 2, respectively). Using the (randomly generated) crossover points ${c}_{1} = 3$ and ${c}_{2} = 5$ , we get partial $\mathrm{C}1 =$ ?-?-3-4-1 and $\mathrm{C}2 =$ ?-?-3-2-4.Next, ${\mathrm{{L1}}}^{\prime } = \{ 1,5,3,2,4\}  - \{ 3,4,1\}  = \{ 5,2\}$ , which yields $\mathrm{C}1 =$ 5-2-3-4-1. Similarly, ${\mathrm{{L2}}}^{\prime } = \{ 2,5,\mathbf{3},\mathbf{4},\mathbf{1}\}  - \{ 3,2,4\}  = \{ 5,1\}$ , which yields $\mathrm{C}2 = 5 - 1 - \mathbf{3} - \mathbf{2} - \mathbf{4}$ . Children C1 and C2 now replace the least-fit parents 2 and 3 corresponding to the worst (longest) tour lengths (810 and 825) to yield the new population to be used in iteration 2 (it is immaterial which child replaces which of the two worst parents).

For small problems, the iterations may "saturate" rather quickly, in the sense that the children become indistinguishable from the parents they replace, as iteration 11 demonstrates. The only recourse in this case is to restart a new execution cycle that allows the use of a new (randomized) starting condition.

## Excel Moment

Figure 11.7 provides a general Excel-based model for experimenting with the genetic meta-heuristic (file excelGeneticTSP.xls). The model can be executed one iteration at a time or it can be automated until a termination condition is reached. The randomization of the starting conditions provides different stating conditions each time the execution button is pressed.

FIGURE 11.7

TSP genetic metaheuristic using Excel spreadsheet (file excelGeneticTSP.xls)

![bo_d56m4sref24c73bhe60g_22_428_1207_1096_910_0.jpg](bo_d56m4sref24c73bhe60g_22_428_1207_1096_910_0.jpg)

## BIBLIOGRAPHY

Applegate, D., R. Bixby, V. Chvatal, and W. J. Cook, The Traveling Salesman Problem: A Computational Study, Princeton University Press, 2006.

Bosch, R. and A. Herman, "Continuous Line Drawings via the Traveling Salesman Problem," Operations Research Letters, Vol. 32, pp. 302-303, 2004.

Dantzig, G., D. Fulkerson, and S. Johnson, "Solution of a Large-Scale Traveling-Salesman Problem," Operations Research, Vol. 2, pp. 393-410, 1954.

Garfinkel, R., "Minimizing Wallpaper Waste. Part I: A Class of Travelling Salesman Problems," Operations Research, Vol. 25, pp. 741-751, 1977.

Gilmore, P., and R. Gomory, "Sequencing a One State-Variable Machine: A Solvable Case of the Travelling Salesman Problem," Operations Research, Vol. 12, pp. 655-679, 1964.

Larrañaga, P., C. Kuijpers, R. Murga, I. Inza, and S. Dizdarevich, "Genetic Algorithms for the Travelling Salesman Problem: A Review of Representations and Operators," Artificial Intelligence Review, Vol. 13, No. 2, pp. 129-170, 1999.

Laporte, G., "The Traveling Salesman Problem: An Overview of Exact and Approximate Algorithms," European Journal of Operational Research, Vol. 59, No. 2, pp. 231-247, 1992.

Lenstra, J., and A. Rinnooy Kan, "Some Simple Applications of the Traveling Salesman Problem," Operational Research Quarterly, Vol. 26, No. 4, pp. 717-733, 1975.

Ratliff, H., and A. Rosenthal, "Order-Picking in a Rectangular Warehouse: A Solvable Case of the Traveling Salesman Problem," Operations Research, Vol. 31, pp. 507-521, 1983.

Yamada, Y. and R. Nakano, "Genetic Algorithms for Job-Shop Scheduling Problems," Proceedings of Modern Heuristic for Decision Support, UNICOM Seminar, London, 18-19 March 1997, pp. 67-81.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>11.1</td><td>11-1 to 11-1</td><td>11.4</td><td>11-23 to 11-26</td></tr><tr><td>11.2</td><td>11-2 to 11-14</td><td>11.5.1</td><td>11-27 to 11-29</td></tr><tr><td>11.3.1</td><td>11-15 to 11-19</td><td>11.5.2</td><td>11-30 to 11-32</td></tr><tr><td>11.3.2</td><td>11-20 to 11-22</td><td>11.5.3</td><td>11-33 to 11-35</td></tr></table>

11-1. In each of the following instances, describe the data elements (cities and distances) needed to model the problem as a TSP.

(a) Seers Service Center schedules its daily repair visits to customers. The jobs are categorized and grouped and each group assigned to a repairperson. At the end of the assignment, the repairperson reports back to the service center.

(b) A baseball fan wishes to visit eight major league parks in (1) Seattle, (2) San Francisco, (3) Los Angeles, (4) Phoenix, (5) Denver, (6) Dallas, (7) Chicago, and (8) Tampa before returning home in Seattle. Each visit lasts about one week. The goal is to spend the least money on airfare.

*(c) A tourist in New York City wants to visit 8 tourist sites using local transportation. The tour starts and ends at a centrally located hotel. The tourist wants to spend the least money on transportation.

(d) A manager has $m$ employees working on $n$ projects. An employee may work on more than one project, which results in overlap of the assignments. Currently, the manager meets with each employee individually once a week. To reduce the total meeting time for all employees, the manager wants to hold group meetings involving shared projects. The objective is to reduce the traffic (number of employees) in and out of the meeting room.

(e) Meals-on-Wheels is a charity service that prepares meals in its central kitchen for delivery to people who qualify for the service. Ideally, all meals should be delivered within 20 minutes from the time they leave the kitchen. This means that the return time from the last location to the kitchen is not a factor in determining the sequence of deliveries.

(f) DNA sequencing. In genetic engineering, a collection of DNA strings, each of a specified length, is concatenated to form one universal string. The genes of individual DNA strings may overlap. The amount of overlaps between two successive strings is measurable in length units. The length of the universal string is the sum of the lengths of the individual strings less the overlaps. The goal is to concatenate the individual strings in a manner that minimizes the length of the universal string.

(g) Automatic guided vehicle. An AGV makes a round-trip, starting and ending at the mailroom, to deliver mail to departments on the factory floor. The AGV moves along horizontal and vertical aisles. The goal is to minimize the length of the round-trip.

(h) Integrated circuit board. Holes in identical circuit boards are drilled to mount electronic components. The boards are fed sequentially under a moving drill. The goal is to determine the sequence that completes drilling all the holes in a board in the shortest time possible.

(i) Protein clustering. Proteins are clustered using a numeric measure of similarity based on protein-to-protein interaction. Clustering information is used to predict unknown protein functions. The best cluster is the one that maximizes (minimizes) the sum of the measures of similarity (dissimilarity) between adjacent proteins.

(j) Celestial objects imaging. The US space agency NASA uses satellites for imaging celestial objects. The amount of fuel needed to reposition the satellites depends on the sequence in which the objects are imaged. The goal is to determine the optimal imaging sequence that minimizes fuel consumption.

(k) Mona Lisa TSP art. This intriguing application re-creates Leonardo da Vinci's Mona Lisa using a continuous line drawing. The general idea is to approximate the original painting by using computer graphics to cluster dots on a graph. The dots are then connected sequentially by piecewise-linear segments.

*11-2. A book salesperson who lives in Basin must call once a month on four customers located in Wald, Bon, Mena, and Kiln before returning home to Basin. The following table gives the distances in miles among the different cities.

<table><tr><td rowspan="2"></td><td colspan="5">Miles between cities</td></tr><tr><td>Basin</td><td>Wald</td><td>Bon</td><td>Mena</td><td>Kiln</td></tr><tr><td>Basin</td><td>0</td><td>125</td><td>225</td><td>155</td><td>215</td></tr><tr><td>Wald</td><td>125</td><td>0</td><td>85</td><td>115</td><td>135</td></tr><tr><td>Bon</td><td>225</td><td>85</td><td>0</td><td>165</td><td>190</td></tr><tr><td>Mena</td><td>155</td><td>115</td><td>165</td><td>0</td><td>195</td></tr><tr><td>Kiln</td><td>215</td><td>135</td><td>190</td><td>195</td><td>0</td></tr></table>

The objective is to minimize the total distance traveled by the salesperson.

(a) Write down the LP for computing a lower-bound estimate on the optimum tour length.

(b) Compare the lower bounds on the optimum tour length using both the assignment model and linear programming. Is the assignment model solution optimum for the TSP?

11-3. Seers Service Center schedules its daily repair visits to customers. The matrix $\begin{Vmatrix}{T}_{ij}\end{Vmatrix}$ below gives the travel time (in minutes) between the service center (row 1 and column 1) and seven jobs. The jobs are assigned to one of the repairpersons during an 8-hr shift. At the end of the day, the repairperson returns to the service center to complete paperwork.

$$
\begin{Vmatrix}{T}_{ij}\end{Vmatrix} = \left( \begin{matrix} 0 & {20} & {15} & {19} & {24} & {14} & {21} & {11} \\  {20} & 0 & {18} & {22} & {23} & {22} & 9 & {10} \\  {15} & {18} & 0 & {11} & {21} & {14} & {32} & {12} \\  {19} & {22} & {11} & 0 & {20} & {27} & {18} & {15} \\  {24} & {23} & {21} & {20} & 0 & {14} & {25} & {20} \\  {14} & {22} & {14} & {27} & {14} & 0 & {26} & {17} \\  {21} & 9 & {32} & {18} & {25} & {26} & 0 & {20} \\  {11} & {10} & {12} & {16} & {20} & {17} & {20} & {20} \end{matrix}\right)
$$

(a) Compare the lower bounds on the optimum tour length using both the assignment model and linear programming. Is the assignment model solution optimum for the TSP?

(b) Given that journeying between jobs is nonproductive and assuming a 1-hr lunch break, determine the maximum productivity of the repairperson during the day.

11-4. A baseball fan wishes to visit eight major league parks in (1) Seattle, (2) San Francisco, (3) Los Angeles, (4) Phoenix, (5) Denver, (6) Dallas, (7) Chicago, and (8)Tampa before returning home to Seattle. The fan will use air transportation between the different cities. The matrix $\begin{Vmatrix}{p}_{ij}\end{Vmatrix}$ below provides the price in dollars of one-way ticket between the 8 cities.

$$
\begin{Vmatrix}{p}_{ij}\end{Vmatrix} = \left( \begin{matrix} 0 & {255} & {305} & {295} & {245} & {325} & {385} & {455} \\  {255} & 0 & {190} & {220} & {230} & {300} & {310} & {395} \\  {305} & {190} & 0 & {140} & {310} & {295} & {390} & {410} \\  {295} & {220} & {140} & 0 & {200} & {275} & {285} & {350} \\  {245} & {230} & {310} & {200} & 0 & {240} & {255} & {400} \\  {325} & {300} & {295} & {275} & {240} & 0 & {260} & {370} \\  {385} & {310} & {390} & {285} & {255} & {260} & 0 & {420} \\  {455} & {295} & {400} & {350} & {400} & {320} & {400} & {270} \end{matrix}\right)
$$

The fan has budgeted \$2200 for air travel. Is this a realistic travel budget?

11-5. Proteins clustering. Proteins are clustered using an overall measure of similarity based on protein-protein interaction information. Clustering information is used to predict unknown protein functions. By definition, the best cluster maximizes the sum of the measures of similarity between adjacent proteins. Matrix $\begin{Vmatrix}{s}_{ij}\end{Vmatrix}$ below provides the measure of similarities (expressed as a percentage) among 8 proteins.

$$
\begin{Vmatrix}{s}_{ij}\end{Vmatrix} = \left( \begin{matrix} {100} & {20} & {30} & {29} & {24} & {22} & {38} & {45} \\  {20} & {100} & {10} & {22} & 0 & {15} & {31} & 0 \\  {30} & {10} & {100} & {14} & {11} & {95} & {30} & {41} \\  {29} & {22} & {14} & {100} & {20} & {27} & {28} & {50} \\  {24} & 0 & {11} & {20} & {100} & {24} & {55} & 0 \\  {22} & {15} & {95} & {27} & {24} & {100} & {26} & {37} \\  {38} & {31} & {30} & {28} & {55} & {26} & {100} & {40} \\  {45} & 0 & {41} & {50} & 0 & {37} & {40} & {100} \end{matrix}\right)
$$

(a) Define the distance matrix of the TSP.

(b) Determine an upper bound on the measure of similarity for the optimum protein cluster.

11-6. A tourist in New York City uses local transportation to visit 8 sites. The start and end and the order in which the sites are visited are unimportant. What is important is to spend the least amount of money on transportation. Matrix $\begin{Vmatrix}{c}_{ij}\end{Vmatrix}$ below provides the fares in dollars between the different locations.

$$
\begin{Vmatrix}{c}_{ij}\end{Vmatrix} = \left( \begin{matrix} 0 & {20} & {30} & {25} & {12} & {33} & {44} & {57} \\  {22} & 0 & {19} & {20} & {20} & {29} & {43} & {45} \\  {28} & {19} & 0 & {17} & {38} & {48} & {55} & {60} \\  {25} & {20} & {19} & 0 & {28} & {35} & {40} & {55} \\  {12} & {18} & {34} & {25} & 0 & {21} & {30} & {40} \\  {35} & {25} & {45} & {30} & {20} & 0 & {25} & {39} \\  {47} & {39} & {50} & {35} & {28} & {20} & 0 & {28} \\  {60} & {38} & {45} & {50} & {33} & {40} & {25} & 0 \end{matrix}\right)
$$

The tourist is budgeting \$120 for cab cost to all eight sites. Is this a realistic expectation? (Hint: This is an open-tour TSP.)

*11-7. A manager has a total of 10 employees working on six projects. Projects are reviewed weekly with each employee. A project may employ more than one employee resulting in assignment overlaps, as the following table shows:

![bo_d56m4sref24c73bhe60g_26_776_1680_494_463_0.jpg](bo_d56m4sref24c73bhe60g_26_776_1680_494_463_0.jpg)

Currently, the manager meets individually once a week with each employee. Each meeting lasts about 20 min for a total of 3 hr and 20 min for all 10 employees. To reduce the total time, the manager wants to hold group meetings depending on shared projects. The objective is to schedule the meetings in a way that will reduce the traffic (number of employees) in and out of the meeting room.

(a) Define the cities and the distance matrix of the TSP.

(b) Determine a lower bound on the optimum tour length using the assignment model. Is the assignment model solution optimum for the TSP?

11-8. Meals-on-Wheels is a charity service that prepares meals in its central facility for delivery to people who qualify for the service. Ideally, all meals should be delivered within 20 min from the time they leave the kitchen. This means that the return time from the last-meal location to the kitchen is not a factor in determining the sequence of deliveries. The charity is in the process of determining the delivery route. The first pilot schedule includes seven recipients with the following travel times, $\begin{Vmatrix}{t}_{ij}\end{Vmatrix}$ (row 1 and column 1 represent the kitchen).

$$
\begin{Vmatrix}{t}_{ij}\end{Vmatrix} = \left( \begin{matrix} 0 & {10} & {12} & 5 & {17} & 9 & {13} & 7 \\  {10} & 0 & 9 & {20} & 8 & {11} & 3 & 5 \\  {12} & 9 & 0 & {14} & 4 & {10} & 1 & {16} \\  5 & {20} & {14} & 0 & {20} & 5 & {28} & {10} \\  {17} & 8 & 4 & {20} & 0 & {21} & 4 & 9 \\  9 & {11} & {10} & 5 & {21} & 0 & 2 & 3 \\  {13} & 3 & 1 & {28} & 4 & 2 & 0 & 2 \\  7 & 5 & {16} & {10} & 9 & 3 & 2 & 0 \end{matrix}\right)
$$

(a) Compare the lower bounds on the optimum tour length using both the assignment model and linear programming. Is the assignment model solution optimum for the TSP?

(b) Based on the information in (a), is it possible to deliver the eight meals within the 20-min time window?

11-9. (Integrated circuit boards) Circuit boards (such as those used in PCs) are drilled with holes for mounting different electronic components. The boards are fed one at a time under a moving drill. The matrix $\begin{Vmatrix}{d}_{ij}\end{Vmatrix}$ below provides the distances (in millimeters) between pairs of 6 holes of a specific circuit board.

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix}  - & {1.3} & {.5} & {2.6} & {4.1} & {3.2} \\  {1.3} &  - & {3.5} & {4.7} & {3.0} & {5.3} \\  {.5} & {3.5} &  - & {3.5} & {4.6} & {6.2} \\  {2.6} & {4.7} & {3.5} &  - & {3.8} & 9 \\  {4.1} & {3.0} & {4.6} & {3.8} &  - & {1.9} \\  {3.2} & {5.3} & {6.2} & 9 & {1.9} &  -  \end{matrix}\right)
$$

Suppose that the drill moves at a linear speed of 9 millimeters per second and that it takes .7 second to drill hole. Determine an upper bound on the production rate (boards per hour).

11-10. DNA sequencing. In genetic engineering, a collection of DNA strings, each of length ${10}\mathrm{{ft}}$ , is concatenated to form one universal string. The genes of individual DNA strings may overlap, thus producing a universal string with length less than the sum of the individual lengths. The matrix $\begin{Vmatrix}{O}_{ij}\end{Vmatrix}$ below provides the length in feet of overlaps for a hypothetical case of six DNA strings.

$$
\begin{Vmatrix}{O}_{ij}\end{Vmatrix} = \left( \begin{matrix}  - & 1 & 0 & 3 & 4 & 3 \\  1 &  - & 4 & 5 & 3 & 2 \\  0 & 4 &  - & 3 & 5 & 6 \\  3 & 5 & 3 &  - & 2 & 1 \\  4 & 3 & 5 & 2 &  - & 2 \\  3 & 2 & 6 & 1 & 2 &  -  \end{matrix}\right)
$$

Compare the lower bounds on the optimum tour length using both the assignment model and linear programming. Is the assignment model solution optimum for the TSP?

11-11. The U.S. space agency, NASA, uses satellites for imaging celestial objects. The amount of fuel needed to reposition the satellites is a function of the sequence in which the objects are imaged. The matrix $\begin{Vmatrix}{c}_{ij}\end{Vmatrix}$ below provides units of fuel consumption used to realign the satellites with the objects.

$$
\begin{Vmatrix}{c}_{ij}\end{Vmatrix} = \left( \begin{matrix}  - & {1.5} & {2.6} & {3.1} & {4.4} & {3.8} \\  {1.9} &  - & {4.7} & {5.3} & {3.9} & {2.7} \\  {2.9} & {4.3} &  - & {3.5} & {5.4} & {6.2} \\  {3.4} & {5.1} & {3.6} &  - & {2.2} & {1.9} \\  {4.4} & {3.4} & {5.9} & {2.4} &  - & {2.6} \\  {3.1} & {2.7} & {6.5} & {1.1} & {2.9} &  -  \end{matrix}\right)
$$

Suppose that the cost per fuel unit is \$12. Estimate a lower bound on the cost of imaging all six objects.

11-12. Automatic guided vehicle. An AGV makes a round-trip (starting and ending at the mail-room) to deliver mail to 5 departments on a factory floor. Using the mailroom as the origin $\left( {0,0}\right)$ , the $\left( {x, y}\right)$ locations of the delivery spots are $\left( {{10},{30}}\right) ,\left( {{10},{50}}\right) ,\left( {{30},{10}}\right) ,({40}$ , 40), and (50,60) for the five departments. All distances are in meters. The AGV moves along horizontal and vertical aisles only. The objective is to minimize the length of the round-trip.

(a) Define the cities and the distance matrix of the TSP model.

(b) Assuming that the AGV moves at a speed of 35 meters per minute, can the round-trip be made in less than 5 minutes?

11-13. Wallpaper cutting, Garfinkel (1977). Covering the walls of a room usually requires cutting sheets of different lengths to account for doors and windows, and the like. The sheets are cut from a single roll, and their start points must be aligned to match the repeating pattern of the roll. The amount of waste thus depends on the sequence in which the sheets are cut. For the purpose of determining the waste, we can regard a single pattern as a unit length (regardless of its real measurement) and then express the length of a sheet in terms of this unit. For example, a sheet of length 9.50 patterns requires 10 consecutive patterns. If the matching of the patterns on the wall requires starting the sheet a quarter of the way down from the first pattern, then the sheet (of length 9.50 patterns) must end three quarters of the way down the tenth pattern. Thus, waste in a sheet can take place in the first and last patterns only, and its amount is always less than the length of a full pattern.

Let $0 \leq  {s}_{i} \leq  1$ and $0 \leq  {e}_{i} \leq  1$ be the locations of the cuts down the first and last patterns. Then for sheet $i$ of length ${L}_{i}$ pattern, we have

$$
{e}_{i} = \left( {{s}_{i} + {L}_{i}}\right) {\;\operatorname{mod}\;\left( 1\right) }
$$

For the example just cited, $s = {.25}$ and $e = \left( {{.25} + {9.5}}\right) {\;\operatorname{mod}\;\left( 1\right) } = {.75}$ .

The waste between two sequential sheets, $i$ and $j$ , in which sheet $i$ is immediately followed by sheet $j$ , can be computed in the following manner: If ${s}_{j} \geq  {e}_{i}$ , the waste is ${s}_{j} - {e}_{i}$ . Else, if ${s}_{j} < {e}_{i}$ , then the end cut of $i$ and the start cut of $j$ overlap. The result is that the start cut ${s}_{j}$ of sheet $j$ must be made in the pattern that immediately follows the one in which the end cut ${e}_{i}$ of sheet $i$ has been made. In this case, the resulting waste is $1 - {e}_{i} + {s}_{j}$ .

Actually, the two amounts of waste $\left( {{s}_{j} - {e}_{i}}\right.$ and $\left. {1 - {e}_{i} + {s}_{j}}\right)$ can be expressed in one expression as

$$
{w}_{ij} = \left( {{s}_{j} - {e}_{i}}\right) {\;\operatorname{mod}\;\left( 1\right) }
$$

For example, given ${e}_{1} = {.8}$ and ${s}_{2} = {.35}$ , we use the formula for ${s}_{2} < {e}_{1}$ to get ${w}_{12} = 1 - {.8} \; + {.35} = {.55}$ . The same result can be obtained using ${w}_{12} = \left( {{.35} - {.8}}\right) {\;\operatorname{mod}\;\left( 1\right) } = \left( {-{.45}}\right) \; {\;\operatorname{mod}\;\left( 1\right) } = \left( {-1 + {.55}}\right) {\;\operatorname{mod}\;\left( 1\right) } = {.55}.$

To account for the waste resulting from the cut in the first pattern of the first sheet (node 1) and the last pattern of the last sheet (node $n$ ), a dummy sheet (node $n + 1)$ is added with its ${s}_{n + 1} = {e}_{n + 1} = 0$ . The length of a tour passing through all $n + 1$ nodes provides the total waste resulting from a specific sequence. The problem can now be modeled as an $\left( {n + 1}\right)$ -node TSP with distance ${w}_{ij}$ .

(a) Compute the matrix ${w}_{ij}$ for the following set of raw data (for convenience, spreadsheet excelWallPaper.xls automates the computations of ${w}_{ij}$ .):

<table><tr><td>Sheet, $i$</td><td>Pattern start cut, ${s}_{i}$</td><td>Sheet length, ${L}_{i}$</td></tr><tr><td>1</td><td>0</td><td>10.47</td></tr><tr><td>2</td><td>.342</td><td>3.82</td></tr><tr><td>3</td><td>.825</td><td>5.93</td></tr><tr><td>4</td><td>.585</td><td>8.14</td></tr><tr><td>5</td><td>.126</td><td>1.91</td></tr><tr><td>6</td><td>.435</td><td>6.32</td></tr></table>

(b) Show that the optimum solution of the associated assignment produces the optimum tour.

(c) Quantify the total waste as a percentage of the length of all sheets.

11-14. Warehouse order picking, Ratliff and Rosenthal (1983). In a rectangular warehouse, a stacker overhead crane is used to pick and deliver orders between specified locations in the warehouse. The tasks of the crane involve the following: (1) picking a load at a location, (2) delivering a load to a location, and (3) moving unloaded to reach a picking location. Suppose that there are $n$ orders to be picked and delivered. The goal would be to complete all the orders while minimizing the unproductive time of the crane [item (3)]. The unproductive times can be computed based on the pickup and delivery locations of the orders and the lateral and traversal speeds of the crane, among other factors. For the purpose of this situation, the crane starts on the orders from an idle state and also terminates in an idle state after all orders are completed.

For a specific pool of eight orders, the times (in minutes) to reach the locations of orders $1,2,\ldots$ , and 8 from idle state are.1,.4,1.1,2.3,1.4,2.1,1.9, and 1.3, respectively. The following table provides the unproductive times (in minutes) associated with the sequencing of the orders:

$$
\begin{Vmatrix}{t}_{ij}\end{Vmatrix} = \left( \begin{matrix} 0 & {1.0} & {1.2} & {.5} & {1.7} & {.9} & {1.3} & {.7} \\  {1.1} & 0 & {.9} & {2.0} & {.8} & {1.1} & {.3} & {.5} \\  {1.2} & {1.9} & 0 & {1.4} & {.4} & {1.0} & 1 & {1.6} \\  {1.5} & {2.3} & {.4} & 0 & {2.0} & {1.5} & {2.8} & 1 \\  {1.2} & {1.8} & {1.4} & {2.5} & 0 & {2.1} & {.4} & {.9} \\  9 & {1.1} & {1.0} & {.5} & {2.1} & 0 & {.2} & {.3} \\  {1.3} & {.8} & {1.2} & {2.4} & {1.6} & 0 & {1.2} & {3.5} \\  {1.7} & {1.5} & {1.6} & {1.0} & {1.3} & {2.0} & 0 & 0 \end{matrix}\right)
$$

(a) Define the cities and distance matrix of the TSP model.

(b) Determine a lower bound on the unproductive time during the completion of all orders.

11-15. Solve Example 11.3-1 using subtour 2-5-4-2 to start the branching process at node 1, using the following sequences for exploring the nodes:

(a) Explore all the subproblems horizontally from left to right in each tier before proceeding to the next tier.

(b) Follow each path vertically from node 1, always selecting the leftmost branch, until the path ends at a fathomed node.

11-16. Solve Problem 11-2, by B&B.

*11-17. Solve Problem 11-7, by B&B.

11-18. Solve Problem 11-9, by B&B.

11-19. AMPL experiment. Use AMPL files amplAssign.txt and solutionAssign.txt to solve Problem 11-6, by B&B.

11-20. Write down the cuts associated with the following TSP:

$$
\begin{Vmatrix}{d}_{ij}\end{Vmatrix} = \left( \begin{matrix} \infty & {43} & {21} & {20} & {10} \\  {12} & \infty & 9 & {22} & {30} \\  {20} & {10} & \infty & 5 & {13} \\  {14} & {30} & {42} & \infty & {20} \\  {44} & 7 & 9 & {10} & \infty  \end{matrix}\right)
$$

11-21. AMPL experiment. Use AMPL to solve the following TSP problem by the cutting-plane algorithm:

(a) Problem 11-3.

(b) Problem 11-4.

(c) Problem 11-12.

11-22. AMPL experiment. In the circuit board model of Problem 11-9, the input data are usually given in terms of the $\left( {x, y}\right)$ -coordinates of the holes rather than the distance between the respective holes. Specifically, consider the following $\left( {x, y}\right)$ coordinates for a 9-hole board:

<table><tr><td></td><td>Hole</td><td>$\left( {x, y}\right)$ in mm</td></tr><tr><td></td><td>1</td><td>(1,2)</td></tr><tr><td></td><td>2</td><td>(4,2)</td></tr><tr><td></td><td>3</td><td>(3,7)</td></tr><tr><td></td><td>4</td><td>(5,3)</td></tr><tr><td></td><td>5</td><td>(8, 4)</td></tr><tr><td></td><td>6</td><td>(7, 5)</td></tr><tr><td></td><td>7</td><td>(3, 4)</td></tr><tr><td></td><td>8</td><td>(6,1)</td></tr><tr><td></td><td>9</td><td>(5,6)</td></tr></table>

The drill always traverses the shortest distance between two successive holes.

(a) Modify the data file to determine the optimum drilling tour using the (x-y) coordinates.

(b) Determine the production rate in boards per hour given that the drill moving speed is $5\mathrm{\;{mm}}/\mathrm{{sec}}$ and the drilling time per hole is ${.5}\mathrm{{sec}}$ . Use files amplCut.txt and solutionCut.txt.

11-23. In Table 11.5 of Example 11.4-2, specify the deleted and added legs associated with each of the two-at-a-time reversals.

11-24. In Table 11.5 of Example 11.4-2, use the infinite-length disconnected tour 3-2-5-4-1-3 (i.e., a tour missing at least one leg) as a starting tour to demonstrate that the subtour reversal heuristic can still lead to a solution that is just as good as when the heuristic starts with a connected tour.

11-25. Apply the reversal heuristic to the following problems starting with best nearest-neighbor tour:

(a) The paint sequencing problem of Example 11.1-1.

(b) Problem 11-2.

(c) Problem 11-5.

(d) Problem 11-6.

11-26. Excel-AMPL Experiment. The matrix below provides the distances among 10 cities (all missing entries $= \infty$ ). (For convenience, file Prob.txt gives the distance matrix in AMPL format.)

<table><tr><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>1</td><td></td><td>100</td><td>2</td><td>11</td><td>80</td><td>5</td><td>39</td><td>95</td><td></td><td>28</td></tr><tr><td>2</td><td>17</td><td></td><td>42</td><td>33</td><td>21</td><td>59</td><td>46</td><td></td><td>79</td><td>29</td></tr><tr><td>3</td><td></td><td>63</td><td></td><td>57</td><td>92</td><td></td><td>55</td><td></td><td>68</td><td>52</td></tr><tr><td>4</td><td>36</td><td>27</td><td>25</td><td></td><td>40</td><td>49</td><td>48</td><td>63</td><td>16</td><td></td></tr><tr><td>5</td><td>51</td><td>11</td><td>46</td><td>60</td><td></td><td>22</td><td>11</td><td>13</td><td>54</td><td>55</td></tr><tr><td>6</td><td></td><td>20</td><td>46</td><td>15</td><td>93</td><td></td><td>76</td><td>47</td><td>21</td><td>10</td></tr><tr><td>7</td><td>17</td><td></td><td>45</td><td>88</td><td>28</td><td>26</td><td></td><td>33</td><td>30</td><td>49</td></tr><tr><td>8</td><td>35</td><td>49</td><td>87</td><td>76</td><td></td><td>55</td><td>64</td><td></td><td></td><td>93</td></tr><tr><td>9</td><td>35</td><td>48</td><td>100</td><td>3</td><td>55</td><td></td><td>41</td><td></td><td></td><td>73</td></tr><tr><td>10</td><td></td><td>50</td><td>70</td><td>43</td><td>82</td><td>43</td><td>23</td><td>49</td><td>89</td><td></td></tr></table>

Use file excelReversalTSP.xls to implement the following situations:

(a) Use the nearest-neighbor heuristic to determine the associated tour starting at node 1.

(b) Determine the tour using the reversal heuristic starting with the tour 4-5-3-2-6-7-8- 10-9-1-4-5.

(c) Determine the tour using the reversal heuristic starting with the best nearest-neighbor tour.

Compare the quality of the solutions in parts (a), (b), and (c) with the exact optimum solution obtained by AMPL.

11-27. Carry out three more iterations of Example 11.5-1.

11-28. Apply tabu to the following problems starting with best nearest-neighbor tour:

(a) The paint sequencing problem of Example 11.1-1.

(b) Problem 11-2.

(c) Problem 11-5.

(d) Problem 11-6.

11-29. Excel-AMPL Experiment. The matrix below provides the distances among 10 cities (all off-diagonal missing entries $= \infty$ ). (For convenience, file prob11-29.txt gives the distance data in AMPL format.)

<table><tr><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>1</td><td></td><td>100</td><td>2</td><td>11</td><td>80</td><td>5</td><td>39</td><td>95</td><td></td><td>28</td></tr><tr><td>2</td><td>17</td><td></td><td>42</td><td>33</td><td>21</td><td>59</td><td>46</td><td></td><td>79</td><td>29</td></tr><tr><td>3</td><td></td><td>63</td><td></td><td>57</td><td>92</td><td></td><td>55</td><td></td><td>68</td><td>52</td></tr><tr><td>4</td><td>36</td><td>27</td><td>25</td><td></td><td>40</td><td>49</td><td>48</td><td>63</td><td>16</td><td></td></tr><tr><td>5</td><td>51</td><td>11</td><td>46</td><td>60</td><td></td><td>22</td><td>11</td><td>13</td><td>54</td><td>55</td></tr><tr><td>6</td><td></td><td>20</td><td>46</td><td>15</td><td>93</td><td></td><td>76</td><td>47</td><td>21</td><td>10</td></tr><tr><td>7</td><td>17</td><td></td><td>45</td><td>88</td><td>28</td><td>26</td><td></td><td>33</td><td>30</td><td>49</td></tr><tr><td>8</td><td>35</td><td>49</td><td>87</td><td>76</td><td></td><td>55</td><td>64</td><td></td><td></td><td>93</td></tr><tr><td>9</td><td>35</td><td>48</td><td>100</td><td>3</td><td>55</td><td></td><td>41</td><td></td><td></td><td>73</td></tr><tr><td>10</td><td></td><td>50</td><td>70</td><td>43</td><td>82</td><td>43</td><td>23</td><td>49</td><td>89</td><td></td></tr></table>

Use file ExcelTabuTSP.xls starting with the following:

(a) A random tour.

(b) Tour 4-5-3-2-6-7-8-10-9-1-4.

(c) The best nearest-neighbor tour.

Compare the quality of the solutions in parts (a), (b), and (c) with the exact optimum solution obtained by AMPL using file amplCut.txt.

11-30. Carry out three more iterations of Example 11.5-2.

11-31. Apply simulated annealing to the following problems starting with best nearest-neighbor tour:

(a) The paint sequencing problem of Example 11.1-1.

(b) Problem 11-2.

(c) Problem 11-5.

(d) Problem 11-6.

11-32. Excel-AMPL Experiment. The matrix below provides the distances among 10 cities (all off-diagonal missing entries $= \infty$ ). (For convenience, file prob11-32.txt gives the distance data in AMPL format.)

<table><tr><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>1</td><td></td><td>100</td><td>2</td><td>11</td><td>80</td><td>5</td><td>39</td><td>95</td><td></td><td>28</td></tr><tr><td>2</td><td>17</td><td></td><td>42</td><td>33</td><td>21</td><td>59</td><td>46</td><td></td><td>79</td><td>29</td></tr><tr><td>3</td><td></td><td>63</td><td></td><td>57</td><td>92</td><td></td><td>55</td><td></td><td>68</td><td>52</td></tr><tr><td>4</td><td>36</td><td>27</td><td>25</td><td></td><td>40</td><td>49</td><td>48</td><td>63</td><td>16</td><td></td></tr><tr><td>5</td><td>51</td><td>11</td><td>46</td><td>60</td><td></td><td>22</td><td>11</td><td>13</td><td>54</td><td>55</td></tr><tr><td>6</td><td></td><td>20</td><td>46</td><td>15</td><td>93</td><td></td><td>76</td><td>47</td><td>21</td><td>10</td></tr><tr><td>7</td><td>17</td><td></td><td>45</td><td>88</td><td>28</td><td>26</td><td></td><td>33</td><td>30</td><td>49</td></tr><tr><td>8</td><td>35</td><td>49</td><td>87</td><td>76</td><td></td><td>55</td><td>64</td><td></td><td></td><td>93</td></tr><tr><td>9</td><td>35</td><td>48</td><td>100</td><td>3</td><td>55</td><td></td><td>41</td><td></td><td></td><td>73</td></tr><tr><td>10</td><td></td><td>50</td><td>70</td><td>43</td><td>82</td><td>43</td><td>23</td><td>49</td><td>89</td><td></td></tr></table>

Use file excelSimulatedAnnealingTSP.xls starting with the following:

(a) A random tour.

(b) Tour 4-5-3-2-6-7-8-10-9-1-4.

(c) The best nearest-neighbor tour.

Compare the quality of the solutions in parts (a), (b), and (c) with the exact optimum solution obtained by AMPL.

11-33. Carry out iterations 3 and 4 in Example 11.5-3.

11-34. Apply the genetic metaheuristic to the following problems starting with best nearest-neighbor tour:

(a) The paint sequencing problem of Example 11.1-1.

(b) Problem 11-2.

(c) Problem 11-5.

(d) Problem 11-6.

11-35. Excel-AMPL Experiment. The matrix below provides the distances among 10 cities (all off-diagonal missing entries $= \infty$ ). (For convenience, file prob11-35.txt gives the distance data in AMPL format.)

<table><tr><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td></tr><tr><td>1</td><td></td><td>100</td><td>2</td><td>11</td><td>80</td><td>5</td><td>39</td><td>95</td><td></td><td>28</td></tr><tr><td>2</td><td>17</td><td></td><td>42</td><td>33</td><td>21</td><td>59</td><td>46</td><td></td><td>79</td><td>29</td></tr><tr><td>3</td><td></td><td>63</td><td></td><td>57</td><td>92</td><td></td><td>55</td><td></td><td>68</td><td>52</td></tr><tr><td>4</td><td>36</td><td>27</td><td>25</td><td></td><td>40</td><td>49</td><td>48</td><td>63</td><td>16</td><td></td></tr><tr><td>5</td><td>51</td><td>11</td><td>46</td><td>60</td><td></td><td>22</td><td>11</td><td>13</td><td>54</td><td>55</td></tr><tr><td>6</td><td></td><td>20</td><td>46</td><td>15</td><td>93</td><td></td><td>76</td><td>47</td><td>21</td><td>10</td></tr><tr><td>7</td><td>17</td><td></td><td>45</td><td>88</td><td>28</td><td>26</td><td></td><td>33</td><td>30</td><td>49</td></tr><tr><td>8</td><td>35</td><td>49</td><td>87</td><td>76</td><td></td><td>55</td><td>64</td><td></td><td></td><td>93</td></tr><tr><td>9</td><td>35</td><td>48</td><td>100</td><td>3</td><td>55</td><td></td><td>41</td><td></td><td></td><td>73</td></tr><tr><td>10</td><td></td><td>50</td><td>70</td><td>43</td><td>82</td><td>43</td><td>23</td><td>49</td><td>89</td><td></td></tr></table>

Use file excelGeneticTSP.xls starting with the following:

(a) A random tour.

(b) Tour 4-5-3-2-6-7-8-10-9-1-4-5.

(c) The best nearest-neighbor tour.

Compare the quality of the solutions in parts (a), (b), and (c) with the exact optimum solution obtained by AMPL.