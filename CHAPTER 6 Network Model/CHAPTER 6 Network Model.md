## CHAPTER 6 Network Model ^chapter


```markmap
---
markmap:
  height: 643
---
# [[#^chapter|CHAPTER 6: Network Model]]
## [[#^reallife|Real-Life Application: Saving Federal Travel Dollars]]
### [[#^travelgoal|Goal: choose host city minimizing total travel + per-diem cost]]
### [[#^travelmethod|Method: shortest-route (Floyd) on airfare network]]
## [[#^scope|6.1 Scope & Definition of Network Models]]
### [[#^situations|Typical network OR situations (design, routing, flow, scheduling, min-cost flow)]]
### [[#^netterms|Network notation and core terms (N/A, flow, directed arc, path/cycle, tree)]]
### [[#^covered|Algorithms covered (MST, shortest route, maximal flow, CPM)]]
## [[#^konigsberg|Example 6.1-1: Bridges of Königsberg]]
## [[#^aha|Aha Moment: Why network pictures matter]]
## [[#^mst|6.2 Minimal Spanning Tree Algorithm]]
### [[#^mstgoal|Goal: connect all nodes with minimum total length]]
### [[#^mstidea|Idea: grow a connected set by repeatedly adding the shortest link]]
### [[#^mstexample|Example 6.2-1: Midwest TV Cable (iteration-based construction)]]
### [[#^mstremark|Remark: LP formulation exists but is impractical (cycle constraints)]]
## [[#^shortest|6.3 Shortest-Route Problem]]
### [[#^srmodel|Model: shortest route between a source and destination]]
### [[#^srapplications|Applications beyond distance (replacement, reliability, puzzles)]]
#### [[#^equip|Equipment replacement as a shortest-route model]]
#### [[#^reliable|Most reliable route via logarithmic transformation]]
#### [[#^jug|Three-jug puzzle as a state-space shortest route]]
### [[#^sralgos|Algorithms: Dijkstra and Floyd]]
#### [[#^dijkstra|Dijkstra labeling (temporary/permanent) and backtracking]]
#### [[#^floyd|Floyd triple-operation matrix updates]]
### [[#^srlp|LP formulation: unit flow + flow conservation]]
### [[#^srsolver|Solver spreadsheet perspective]]
### [[#^srampl|AMPL modeling note]]
## [[#^maxflow|6.4 Maximal Flow Model]]
### [[#^cuts|Cuts and bottlenecks (min-cut idea)]]
### [[#^mfalgos|Breakthrough paths, residual capacities, and backtracking]]
### [[#^mflp|LP formulation for maximal flow]]
### [[#^mfsolver|Solver note]]
### [[#^mfampl|AMPL note]]
## [[#^cpmpert|6.5 CPM and PERT]]
### [[#^netrep|Network representation rules and dummy activities]]
### [[#^cpm|CPM computations: forward/backward pass and critical path]]
### [[#^floats|Scheduling: floats (TF/FF) and red-flagging]]
### [[#^cpmlp|LP formulation of CPM (longest path)]]
### [[#^pert|PERT: a/m/b estimates, mean/variance, normal approximation]]
## [[#^casestudy|Case Study: Saving Federal Travel Dollars]]
### [[#^travelassumptions|Assumptions: car vs air travel, per-diems, arrivals/departures]]
### [[#^numerical|Numerical example: 12-city illustration and tables]]
### [[#^besthost|Conclusion: pick city with minimum total event cost]]
```

## Real-Life Application-Saving Federal Travel Dollars ^reallife

U.S. federal government offices are located in most cities in the United States, and federal employees are required to attend development conferences and training courses offered around the country. The location of the city hosting conferences/training events can impact travel costs. The goal of the study is to determine the optimal location of host city for a scheduled conference/training event. For fiscal year 1997, the developed model was estimated to have saved at least \$400,000. Details of the study are presented at the end of the chapter. ^travelgoal

### 6.1 SCOPE AND DEFINITION OF NETWORK MODELS ^scope

Many operations research situations can be modeled and solved as networks (nodes connected by branches): ^situations

1. Design of an offshore natural-gas pipeline network connecting wellheads in the Gulf of Mexico to an inshore delivery point with the objective of minimizing the cost of constructing the pipeline.

2. Determination of the shortest route between two cities in an existing network of roads.

3. Determination of the maximum capacity (in tons per year) of a coal slurry pipeline network joining coal mines in Wyoming with power plants in Houston. (Slurry pipelines transport coal by pumping water through specially designed pipes.)

4. Determination of the time schedule (start and completion dates) for the activities of a construction project.

5. Determination of the minimum-cost flow schedule from oil fields to refineries through a pipeline network.

The solution of these situations is accomplished through a variety of network optimization algorithms. This chapter presents four of these algorithms. ^covered

1. Minimal spanning tree (situation 1)

2. Shortest-route algorithm (situation 2)

3. Maximal-flow algorithm (situation 3)

4. Critical Path Method (CPM) algorithm (situation 4)

For the fifth situation, the minimum-cost capacitated network algorithm is presented in Section 22.1 on the website.

Network definitions. A network consists of a set of nodes linked by arcs (or branches). ^netterms

The notation for describing a network is $\left( {N, A}\right)$ , where $N$ is the set of nodes, and $A$ is the set of arcs. As an illustration, the network in Figure 6.1 is described as ^notation

$$
N = \{ 1,2,3,4,5\}
$$

$$
A = \{ \left( {1,2}\right) ,\left( {1,3}\right) ,\left( {2,3}\right) ,\left( {2,5}\right) ,\left( {3,4}\right) ,\left( {3,5}\right) ,\left( {4,2}\right) ,\left( {4,5}\right) \}
$$

Associated with each network is a flow (e.g., oil products flow in a pipeline and automobile traffic flow in highways). The maximum flow in a network can be finite or infinite, depending on the capacity of its arcs. ^flow

An arc is said to be directed or oriented if it allows positive flow in one direction only. A directed network has all directed arcs. ^directed

A path is a set of arcs joining two distinct nodes, passing through other nodes in the network. For example, in Figure 6.1, arcs $\left( {1,2}\right) ,\left( {2,3}\right) ,\left( {3,4}\right)$ , and $\left( {4,5}\right)$ form a path between nodes 1 and 5. ^path

A path forms a cycle or a loop if it connects a node back to itself through other nodes. In Figure 6.1, arcs $\left( {2,3}\right) ,\left( {3,4}\right)$ , and $\left( {4,2}\right)$ form a cycle. ^cycle

A network is said to be connected if every two distinct nodes are linked by at least one path. The network in Figure 6.1 demonstrates this type of network. ^connected

A tree is a cycle-free connected network comprised of a subset of all the nodes. ^tree

A spanning tree links all the nodes of the network. Figure 6.2 provides examples of a tree and a spanning tree from the network in Figure 6.1. ^spanning

![bo_d56m3tv7aajc73800n00_1_504_1561_474_219_0.jpg](bo_d56m3tv7aajc73800n00_1_504_1561_474_219_0.jpg)

FIGURE 6.1

Example of $\left( {N, A}\right)$ Network

FIGURE 6.2

Examples of a tree and a spanning tree

![bo_d56m3tv7aajc73800n00_1_526_1903_820_275_0.jpg](bo_d56m3tv7aajc73800n00_1_526_1903_820_275_0.jpg)

## Example 6.1-1 (Bridges of Königsberg) ^konigsberg

The Prussian city of Königsberg (now Kalingrad in Russia) was founded in 1254 on the banks of river Pergel with seven bridges connecting its four sections (labeled $A, B, C$ , and $D$ ) as shown in Figure 6.3. A question was raised as to whether a round-trip could be constructed to visit all four sections of the city, crossing each bridge exactly once. A section could be visited multiple times, if necessary.

In the mid-eighteenth century, the famed mathematician Leonhard Euler developed a special "path construction" argument to prove that it was impossible to construct such a trip. Later, in the early nineteenth century, the same problem was solved by representing the situation as a network with nodes representing the sections and (distinct) arcs representing the bridges, as shown in Figure 6.4. ^euler

FIGURE 6.3

Bridges of Königsberg

![bo_d56m3tv7aajc73800n00_2_529_894_902_443_0.jpg](bo_d56m3tv7aajc73800n00_2_529_894_902_443_0.jpg)

FIGURE 6.4

Network representation of Königsberg problem

![bo_d56m3tv7aajc73800n00_2_541_1558_878_567_0.jpg](bo_d56m3tv7aajc73800n00_2_541_1558_878_567_0.jpg)

## Aha! Moment: It is Said that a Picture is Worth a Thousand Words! ^aha

In OR, this cannot be more true than in a network model. Network representation provides, at a glance, all the information about a problem, an outstanding feature indeed. And this all happens because of the simplicity and versatility of the ensemble of nodes and arcs in modeling many real-life situations. To be sure, the Bridges of Königsberg problem was solved by Leonard Euler in the eighteenth century using lengthy logical arguments. In the process, Euler laid the foundation for the network representation of the situation (Figure 6.4) that made the answer almost intuitive. Euler's work was the seed for what is currently known as graph theory, with its present immense contribution to solving intricate real-life problems.

The network representation greatly facilitates the development of almost intuitive algorithmic rules. This point of view is supported by G. Dantzig, R. Fulkerson, and S. Johnson in their 1954 seminal paper (see bibliography of Chapter 11) for solving a 49-city traveling salesman problem by hand using a network representation imposed on a map of the United States. They state, "...This [network representation] speeds up the entire iterative process, makes it easy to follow, and sometimes makes it easy to develop new restraints that are not likely to be obtained by less visual methods."

### 6.2 MINIMAL SPANNING TREE ALGORITHM ^mst

The minimal spanning tree links the nodes of a network using the smallest total length of connecting branches. A typical application occurs in the pavement of roads linking towns, either directly or passing through other towns. The minimal spanning tree solution provides the most economical design of the road system. ^mstgoal

Let $N = \{ 1,2,\ldots , n\}$ be the set of nodes of the network and define ^mstidea

${C}_{k} =$ Set of nodes that have been permanently connected at iteration $k$ ^mstsets

${\bar{C}}_{k} =$ Set of nodes as yet to be connected permanently after iteration $k$

The following steps describe the minimal spanning tree algorithm: ^mststeps

Step 0. Set ${C}_{0} = \varnothing$ and ${\bar{C}}_{0} = N$ . ^mststepzero

Step 1. Start with any node $i$ in the unconnected set ${\bar{C}}_{0}$ and set ${C}_{1} = \{ i\}$ , rendering ${\bar{C}}_{1} = N - \{ i\}$ . Set $k = 2$ . ^mststepone

General step $k$ . Select a node, ${j}^{ * }$ , in the unconnected set ${\bar{C}}_{k - 1}$ that yields the shortest arc to a node in the connected set ${C}_{k - 1}$ . Link ${j}^{ * }$ permanently to ${C}_{k - 1}$ and remove it from ${\bar{C}}_{k - 1}$ to obtain ${C}_{k}$ and ${\bar{C}}_{k}$ , respectively. Stop if ${\bar{C}}_{k}$ is empty; else, set $k = k + 1$ and repeat the step. ^mststepk

Example 6.2-1 ^mstexample

Midwest TV Cable Company is providing cable service to five new housing developments. Figure 6.5 depicts possible TV connections to the five areas, with cable miles affixed on each arc. The goal is to determine the most economical cable network.

![bo_d56m3tv7aajc73800n00_4_612_199_735_514_0.jpg](bo_d56m3tv7aajc73800n00_4_612_199_735_514_0.jpg)

FIGURE 6.5

Cable connections for Midwest TV Company

The algorithm starts at node 1 (actually, any other node can be a starting point), which gives ${C}_{1} = \{ 1\}$ and ${\bar{C}}_{1} = \{ 2,3,4,5,6\}$ . The iterations of the algorithm are summarized in Figure 6.6. The thin arcs provide all the candidate links between $C$ and $\bar{C}$ . The thick arcs are the permanent links of the connected set $C$ , and the dashed arc is the new (permanent) link added at each iteration. For example, in iteration 1, branch $\left( {1,2}\right)$ is the shortest link $\left( { = 1\text{ mile }}\right)$ among all the candidate branches from node 1 to nodes2,3,4, and 5 in the unconnected set ${\bar{C}}_{1}$ . Hence, link $\left( {1,2}\right)$ is made permanent and ${j}^{ * } = 2$ , which yields ${C}_{2} = \{ 1,2\} ,{\bar{C}}_{2} = \{ 3,4,5,6\}$ .

The solution is given by the minimal spanning tree shown in iteration 6 of Figure 6.6. The resulting minimum cable miles needed to provide the desired cable service are $1 + 3 + \; 4 + 3 + 5 = {16}$ miles.

Remarks. In theory, a minimal spanning tree can be formulated and solved as a linear program. However, LP is not a practical option because numerous constraints must be added to exclude all cycles, resulting in a huge LP, even for small networks. ^mstremark

## TORA Moment ^msttora

You can use TORA to generate the iterations of the minimal spanning tree. From Main menu, select Network models $\Rightarrow$ Minimal spanning tree. Next, from SOLVE/MODIFY menu, select Solve problem $\Rightarrow$ Go to output screen. In the output screen, select a Starting node, then use Next iteration or All iterations to generate the successive iterations. You can restart the iterations by selecting a new Starting Node. File toraEx6.2-1.txt gives TORA's data for Example 6.2-1.

### 6.3 SHORTEST-ROUTE PROBLEM ^shortest

The shortest-route problem determines the shortest route between a source and destination in a transportation network. Other situations can be represented by the same model, as illustrated by the following examples. ^srmodel

![bo_d56m3tv7aajc73800n00_5_341_193_1184_1466_0.jpg](bo_d56m3tv7aajc73800n00_5_341_193_1184_1466_0.jpg)

FIGURE 6.6

Solution iterations for Midwest TV Company

#### 6.3.1 Examples of the Shortest-Route Applications ^srapplications

## Example 6.3-1 (Equipment Replacement) ^equip

RentCar is developing a replacement policy for its car fleet over a 4-year planning horizon. At the start of each year, a car is either replaced or kept in operation for an extra year. A car must be in service from 1 to 3 years. The following table provides the replacement cost as a function of the year a car is acquired and the number of years in operation.

![bo_d56m3tv7aajc73800n00_6_415_199_1129_353_0.jpg](bo_d56m3tv7aajc73800n00_6_415_199_1129_353_0.jpg)

FIGURE 6.7

Equipment replacement problem as a shortest-route model

| Equipment acquired at start of year | 1 year | 2 years | 3 years |
| --- | --- | --- | --- |
| 1 | 4000 | 5400 | 9800 |
| 2 | 4300 | 6200 | 8700 |
| 3 | 4800 | 7100 | - |
| 4 | 4900 | - | - |

The problem can be formulated as a network in which nodes 1 to 5 represent the start of years 1 to 5. Arcs from node 1 (year 1) can reach nodes 2, 3, and 4 because a car must be in operation from 1 to 3 years. The arcs from the other nodes can be interpreted similarly. The length of each arc equals the replacement cost. The solution of the problem is equivalent to finding the shortest route between nodes 1 and 5.

Figure 6.7 shows the resulting network. Using TORA, ${}^{1}$ the shortest route is $1 \rightarrow  3 \rightarrow  5$ . The solution says that a car acquired at the start of year 1 (node 1) must be replaced after 2 years at the start of year 3 (node 3). The replacement car will then be kept in service until the end of year 4. The total cost of this replacement policy is $\$ {12},{500}\left( { = \$ 5,{400} + \$ 7,{100}}\right)$ .

## Example 6.3-2 (Most Reliable Route) ^reliable

I. Q. Smart drives daily to work. Having just completed a course in network analysis, Smart is able to determine the shortest route to work. Unfortunately, the selected route is heavily patrolled by police, and with all the fines paid for speeding, the shortest route may not be the best choice. Smart has thus decided to choose a route that maximizes the probability of not being stopped by police.

The network in Figure 6.8 shows the possible routes from home to work, and the associated probabilities of not being stopped on each segment. The probability of not being stopped on a route is the product of the probabilities of its segments. For example, the probability of not receiving a fine on the route $1 \rightarrow  3 \rightarrow  5 \rightarrow  7$ is ${.9} \times  {.3} \times  {.25} = {.0675}$ . Smart’s objective is to select the route that maximizes the probability of not being fined.

---

${}^{1}$ From Main menu, select Network models $\Rightarrow$ Shortest route. From SOLVE/MODIFY menu, select Solve problem $\Rightarrow$ Shortest routes.

---

![bo_d56m3tv7aajc73800n00_7_546_202_780_284_0.jpg](bo_d56m3tv7aajc73800n00_7_546_202_780_284_0.jpg)

FIGURE 6.8

Most-reliable-route network model

![bo_d56m3tv7aajc73800n00_7_547_680_779_287_0.jpg](bo_d56m3tv7aajc73800n00_7_547_680_779_287_0.jpg)

FIGURE 6.9

Most-reliable-route representation as a shortest-route model

The problem can be formulated as a shortest-route model by using logarithmic transformation to convert the product probability into the sum of the logarithms of probabilities - that is, ${p}_{1k} = {p}_{1} \times  {p}_{2} \times  \ldots  \times  {p}_{k}$ is transformed to $\log {p}_{1k} = \log {p}_{1} + \log {p}_{2} + \ldots  + \log {p}_{k}$ . ^logtransform

The two functions ${p}_{1k}$ and $\log {p}_{1k}$ are both monotone decreasing in $k$ ; thus maximizing ${p}_{1k}$ is equivalent to maximizing $\log {p}_{1k}$ , which in turn is equivalent to minimizing $- \log {p}_{1k}$ . Thus, replacing ${p}_{j}$ with $- \log {p}_{j}$ for all $j$ in the network, the problem is converted to the shortest-route network in Figure 6.9.

Using TORA, the shortest route in Figure 6.9 passes through nodes 1, 3, 5, and 7 with a corresponding "length" of 1.1707, or $\log {p}_{17} =  - {1.1707}$ . Thus, the maximum probability of not being stopped is ${p}_{17} = {10}^{-{1.1707}} = {.0675}$ , not a very encouraging news for Smart!

## Example 6.3-3 (Three-Jug Puzzle) ^jug

An 8-gallon jug is filled with fluid. Given two empty 5- and 3-gallon jugs, divide the 8 gallons of fluid into two equal parts using only the three jugs. What is the smallest number of transfers (decantations) needed to achieve this result?

You probably can solve this puzzle by inspection. Nevertheless, the representation of the problem as a shortest-route model is interesting.

A node is defined by a triple index representing the amounts of fluid in the 8-, 5-, and 3-gallon jugs, respectively. This means that the network starts with node $\left( {8,0,0}\right)$ and terminates with the desired solution node $\left( {4,4,0}\right)$ . A new node is generated from the current node by decanting fluid from one jug into another.

Figure 6.10 shows different routes that lead from the start node $\left( {8,0,0}\right)$ to the end node $\left( {4,4,0}\right)$ . The arc between two successive nodes represents a single transfer, and hence it can be assumed to have a length of 1 unit. The problem reduces to determining the shortest route between node $\left( {8,0,0}\right)$ and node $\left( {4,4,0}\right)$ .

![bo_d56m3tv7aajc73800n00_8_330_200_1295_513_0.jpg](bo_d56m3tv7aajc73800n00_8_330_200_1295_513_0.jpg)

FIGURE 6.10

Three-jug puzzle representation as a shortest-route model

The optimal solution, given by the bottom path in Figure 6.10, requires 7 decantations.

#### 6.3.2 Shortest-Route Algorithms ^sralgos

This section presents two algorithms for solving both cyclic (i.e., containing loops) and acyclic networks:

1. Dijkstra's algorithm for determining the shortest routes between the source node and every other node in the network.

2. Floyd's algorithm for determining the shortest route between any two nodes in the network.

Essentially, Floyd's algorithm subsumes Dijkstra's.

Dijkstra’s algorithm. Let ${u}_{i}$ be the shortest distance from source node 1 to node $i$ , and define ${d}_{ij}\left( { \geq  0}\right)$ as the length of arc $\left( {i, j}\right)$ . The algorithm defines the label for an immediately succeeding node $j$ as ^dijkstra

$$
\left\lbrack  {{u}_{j}, i}\right\rbrack   = \left\lbrack  {{u}_{i} + {d}_{ij}, i}\right\rbrack  ,{d}_{ij} \geq  0
$$

The label for the starting node is $\left\lbrack  {0, - }\right\rbrack$ , indicating that the node has no predecessor.

Node labels in Dijkstra's algorithm are of two types: temporary and permanent. A temporary label at a node is modified if a shorter route to the node can be found. Otherwise, the temporary status is changed to permanent.

Step 0. Label the source node (node 1) with the permanent label $\left\lbrack  {0, - }\right\rbrack$ . Set $i = 1$ . General step $i$ .

(a) Compute the temporary labels $\left\lbrack  {{u}_{i} + {d}_{ij}, i}\right\rbrack$ for each node $j$ with ${d}_{ij} > 0$ , provided $j$ is not permanently labeled. If node $j$ already has an existing temporary label $\left\lbrack  {{u}_{j}, k}\right\rbrack$ via another node $k$ and if ${u}_{i} + {d}_{ij} < {u}_{j}$ , replace $\left\lbrack  {{u}_{j},}\right. \; k\rbrack$ with $\left\lbrack  {{u}_{i} + {d}_{ij}, i}\right\rbrack$ .

(b) If all the nodes have permanent labels, stop. Otherwise, select the label $\left\lbrack  {{u}_{r}, s}\right\rbrack$ having the shortest distance $\left( { = {u}_{r}}\right)$ among all the temporary labels (break ties arbitrarily). Set $i = r$ and repeat step $i$ .

## Example 6.3-4

The network in Figure 6.11 gives the permissible routes and their lengths in miles between city 1 (node 1) and four other cities (nodes 2 to 5). Determine the shortest routes between city 1 and each of the remaining four cities.

Iteration 0. Assign the permanent label $\left\lbrack  {0, - }\right\rbrack$ to node 1.

Iteration 1. Nodes 2 and 3 can be reached from (the last permanently labeled) node 1. Thus, the list of labeled nodes (temporary and permanent) becomes

| Node | Label | Status |
| --- | --- | --- |
| 1 | [0,-] | Permanent |
| 2 | $\left\lbrack  {0 + {100},1}\right\rbrack   = \left\lbrack  {{100},1}\right\rbrack$ | Temporary |
| 3 | $\left\lbrack  {0 + {30},1}\right\rbrack   = \left\lbrack  {{30},1}\right\rbrack$ | Temporary |

For the two temporary labels $\left\lbrack  {{100},1}\right\rbrack$ and $\left\lbrack  {{30},1}\right\rbrack$ , node 3 yields the smaller distance $\left( {{u}_{3} = {30}}\right)$ . Thus, the status of node 3 is changed to permanent.

eration 2. Nodes 4 and 5 can be reached from node 3, and the list of labeled nodes becomes

| Node | Label                                                                                | Status    |
| ---- | ------------------------------------------------------------------------------------ | --------- |
| 1    | $\left\lbrack  {0, - }\right\rbrack$                                                 | Permanent |
| 2    | [100, 1]                                                                             | Temporary |
| 3    | [30, 1]                                                                              | Permanent |
| 4    | $\left\lbrack  {{30} + {10},3}\right\rbrack   = \left\lbrack  {{40},3}\right\rbrack$ | Temporary |
| 5    | $\left\lbrack  {{30} + {60},3}\right\rbrack   = \left\lbrack  {{90},3}\right\rbrack$ | Temporary |

Temporary label $\left\lbrack  {{40},3}\right\rbrack$ at node 4 is now permanent $\left( {{u}_{4} = {40}}\right)$ .

FIGURE 6.11

Network Example for Dijkstra's shortest-route algorithm

![bo_d56m3tv7aajc73800n00_9_526_1787_823_381_0.jpg](bo_d56m3tv7aajc73800n00_9_526_1787_823_381_0.jpg)

Iteration 3. Nodes 2 and 5 can be reached from node 4. Thus, the list of labeled nodes is updated as

| Node | Label | Status |
| --- | --- | --- |
| 1 | $\left\lbrack  {0, - }\right\rbrack$ | Permanent |
| 2 | $\left\lbrack  {{40} + {15},4}\right\rbrack   = \left\lbrack  {{55},4}\right\rbrack$ | Temporary |
| 3 | $\left\lbrack  {{30},1}\right\rbrack$ | Permanent |
| 4 | [40, 3] | Permanent |
| 5 | [90, 3] or<br>$\left\lbrack  {{40} + {50},4}\right\rbrack   = \left\lbrack  {{90},4}\right\rbrack$ | Temporary |

At node 2, the new label $\left\lbrack  {{55},4}\right\rbrack$ replaces the temporary label $\left\lbrack  {{100},1}\right\rbrack$ from iteration 1 because it provides a shorter route. Also, in iteration 3, node 5 has two alternative labels with the same distance $\left( {{u}_{5} = {90}}\right)$ . Temporary label $\left\lbrack  {{55},4}\right\rbrack$ at node 2 is now permanent $\left( {{u}_{2} = {55}}\right)$ .

Iteration 4. Only permanently labeled node 3 can be reached from node 2. Hence node 3 cannot be relabeled. The new list of labels remains the same as in iteration 3 except that the label at node 2 is now permanent. This leaves node 5 as the only temporary label. Because node 5 does not lead to other nodes, its label becomes permanent, and the process ends.

The computations of the algorithm can be carried out directly on the network, as Figure 6.12 demonstrates.

The shortest route between nodes 1 and any other node in the network is determined beginning at the desired destination node and backtracking to the starting node using the information in the permanent labels. For example, the following sequence determines the shortest route from node 1 to node 2:

$$
\left( \mathbf{2}\right)  \rightarrow  \left\lbrack  {{55},\mathbf{4}}\right\rbrack   \rightarrow  \left( \mathbf{4}\right)  \rightarrow  \left\lbrack  {{40},\mathbf{3}}\right\rbrack   \rightarrow  \left( \mathbf{3}\right)  \rightarrow  \left\lbrack  {{30},\mathbf{1}}\right\rbrack   \rightarrow  \left( \mathbf{1}\right)
$$

Thus, the desired route is $1 \rightarrow  3 \rightarrow  4 \rightarrow  2$ with a total length of 55 miles.

FIGURE 6.12

Dijkstra's labeling procedure

![bo_d56m3tv7aajc73800n00_10_459_1590_1041_494_0.jpg](bo_d56m3tv7aajc73800n00_10_459_1590_1041_494_0.jpg)

( ) = iteration

![bo_d56m3tv7aajc73800n00_11_410_197_711_260_0.jpg](bo_d56m3tv7aajc73800n00_11_410_197_711_260_0.jpg)

FIGURE 6.13

Floyd's triple operation

TORA Moment

TORA can be used to generate Dijkstra's iterations. From SOLVE/MODIFY menu, select Solve problem $\Rightarrow$ Iterations $\Rightarrow$ Dijkstra’s algorithm. File toraEx6.3-4.txt provides TORA’s data for Example 6.3-4.

Floyd's algorithm. Floyd's algorithm is more general than Dijkstra's because it determines the shortest route between any two nodes in the network. The algorithm represents an $n$ -node network as a square matrix with $n$ rows and $n$ columns. Entry $\left( {i, j}\right)$ of the matrix gives the distance ${d}_{ij}$ from node $i$ to node $j$ , which is finite if $i$ is linked directly to $j$ , and infinite otherwise. ^floyd

The idea of Floyd’s algorithm is straightforward. Given three nodes $i, j$ , and $k$ in Figure 6.13 with the connecting distances shown on the three arcs, it is shorter to reach $j$ from $i$ passing through $k$ if

$$
{d}_{ik} + {d}_{kj} < {d}_{ij}
$$

In this case, it is optimal to replace the direct route from $i \rightarrow  j$ with the indirect route $i \rightarrow  k \rightarrow  j$ . This triple operation exchange is applied to the distance matrix using the following steps:

Step 0. Define the starting distance matrix ${D}_{0}$ and node sequence matrix ${S}_{0}$ (all diagonal elements are blocked). Set $k = 1$ .

|  | 1 | 2 | ... | $j$ | ... | $n$ |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | - | ${d}_{12}$ | ... | ${d}_{ij}$ | ... | ${d}_{1n}$ |
| 2 | ${d}_{21}$ | - | ... | ${d}_{2j}$ | ... | ${d}_{2n}$ |
| $\vdots$ | : | : | : | $\vdots$ | $\vdots$ | : |
| ${D}_{0} = I$ | ${d}_{i1}$ | ${d}_{i2}$ | ... | ${d}_{ij}$ | ... | ${d}_{in}$ |
| : | $\vdots$ | $\vdots$ | : | : | $\vdots$ | : |
| $N$ | ${D}_{n1}$ | ${d}_{n2}$ | ... | ${d}_{nj}$ | ... | - |

1 2 ... $j$ ... $n$

1 - 2 ... $j$ ... $n$

2 1 - ... $j$ ... $n$

${S}_{0} = \; \vdots \; \vdots \; \vdots \; \vdots \; \vdots \; \vdots$

$i$ 1 2 ... $j$ ... $n$

$\vdots$ : : : $\vdots \; \vdots$ :

$n$ 1 2 ... $j$ ... -

![bo_d56m3tv7aajc73800n00_12_475_199_660_613_0.jpg](bo_d56m3tv7aajc73800n00_12_475_199_660_613_0.jpg)

FIGURE 6.14

Implementation of triple operation in matrix form

General step $\mathbf{k}$ . Define row $k$ and column $k$ as pivot row and pivot column. Apply the triple operation to each element ${d}_{ij}$ in ${D}_{k - 1}$ , for all $i$ and $j$ . If the condition

$$
{d}_{ik} + {d}_{kj} < {d}_{ij},\left( {i \neq  k, j \neq  k\text{ , and }i \neq  j}\right)
$$

is satisfied, make the following changes:

(a) Create ${D}_{k}$ by replacing ${d}_{ij}$ in ${D}_{k - 1}$ with ${d}_{ik} + {d}_{kj}$ .

(b) Create ${S}_{k}$ by replacing ${s}_{ij}$ in ${S}_{k - 1}$ with $k$ . Set $k = k + 1$ . If $k = n + 1$ , stop; else repeat step $k$ .

Step $k$ of the algorithm can be explained by representing ${D}_{k - 1}$ as shown in Figure 6.14. Here, row $k$ and column $k$ define the current pivot row and column. Row $i$ represents any of the rows $1,2,\ldots$ , and $k - 1$ , and row $p$ represents any of the rows $k + 1$ , $k + 2,\ldots$ , and $n$ . Similarly, column $j$ represents any of the columns $1,2,\ldots$ , and $k - 1$ , and column $q$ represents any of the columns $k + 1, k + 2,\ldots$ , and $n$ . The triple operation can be applied as follows: If the sum of the elements on the pivot row and the pivot column (shown by squares) is smaller than the associated intersection element (shown by a circle), then it is optimal to replace the intersection distance by the sum of the pivot distances.

After $n$ steps, we can determine the shortest route between nodes $i$ and $j$ from the matrices ${D}_{n}$ and ${S}_{n}$ using the following rules:

1. From ${D}_{n},{d}_{ij}$ gives the shortest distance between nodes $i$ and $j$ .

2. From ${S}_{n}$ , determine the intermediate node $k = {s}_{ij}$ that yields the route $i \rightarrow  k \rightarrow  j$ . If ${s}_{ik} = k$ and ${s}_{kj} = j$ , stop; all the intermediate nodes of the route have been found. Otherwise, repeat the procedure between nodes $i$ and $k$ and between nodes $k$ and $j$ .

## Example 6.3-5

For the network in Figure 6.15, find the shortest routes between every two nodes. The distances (in miles) are given on the arcs. Arc (3, 5) is directional - no traffic is allowed from node 5 to node 3. All the other arcs allow two-way traffic.

![bo_d56m3tv7aajc73800n00_13_426_201_640_310_0.jpg](bo_d56m3tv7aajc73800n00_13_426_201_640_310_0.jpg)

FIGURE 6.15

Network for Example 6.3-5

Iteration 0. The matrices ${D}_{0}$ and ${S}_{0}$ give the initial representation of the network. ${D}_{0}$ is symmetrical, except that ${d}_{53} = \infty$ because no traffic is allowed from node 5 to node 3.

${D}_{0} \; {S}_{0}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 2 | 3 | 4 | 5 |
| 2 | 1 | - | 3 | 4 | 5 |
| 3 | 1 | 2 | - | 4 | 5 |
| 4 | 1 | 2 | 3 | - | 5 |
| 5 | 1 | 2 | 3 | 4 | - |

1 2 3 4 5

1 - 3 10 $\infty \; \infty$ 1

2 3 - $\infty$ 5 $\infty$ 2

3 10 $\infty$ - 6 15 3

4 $\infty$ 5 6 - 4 4

5 0 $\infty \; \infty$ 4 - 5

Set $k = 1$ . The pivot row and column are shown by the lightly shaded first row and first column in the ${D}_{0}$ -matrix. The darker cells, ${d}_{23}$ and ${d}_{32}$ , are the only ones that can be improved by the triple operation. Thus, ${D}_{1}$ and ${S}_{1}$ are obtained from ${D}_{0}$ and ${S}_{0}$ in the following manner:

1. Replace ${d}_{23}$ with ${d}_{21} + {d}_{13} = 3 + {10} = {13}$ and set ${s}_{23} = 1$ .

2. Replace ${d}_{32}$ with ${d}_{31} + {d}_{12} = {10} + 3 = {13}$ and set ${s}_{32} = 1$ .

These changes are shown in bold in matrices ${D}_{1}$ and ${S}_{1}$ .

${S}_{1}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 2 | 3 | 4 | 5 |
| 2 | 1 | - | 1 | 4 | 5 |
| 3 | 1 | 1 | - | 4 | 5 |
| 4 | 1 | 2 | 3 | - | 5 |
| 5 | 1 | 2 | 3 | 4 | - |

${D}_{1}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 3 | 10 | 00 | 00 |
| 2 | 3 | - | 13 | 5 | 10 |
| 3 | 10 | 13 | - | 6 | 15 |
| 4 | $\infty$ | 5 | 6 | - | 4 |
| 5 | $\infty$ | $\infty$ | $\infty$ | 4 | - |

1

2

3

4

5

Iteration 2. Set $k = 2$ , as shown by the lightly shaded row and column in ${D}_{1}$ . The triple operation is applied to the darker cells in ${D}_{1}$ and ${S}_{1}$ . The resulting changes are shown in bold in ${D}_{2}$ and ${S}_{2}$ .

${D}_{2}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 3 | 10 | 8 | 00 |
| 2 | 3 | - | 13 | 5 | 00 |
| 3 | 10 | 13 | - | 6 | 15 |
| 4 | 8 | 5 | 6 | - | 4 |
| 5 | 00 | $\infty$ | 00 | 4 | - |

${S}_{2}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 2 | 3 | 2 | 5 |
| 2 | 1 | - | 1 | 4 | 5 |
| 3 | 1 | 1 | - | 4 | 5 |
| 4 | 2 | 2 | 3 | - | 5 |
| 5 | 1 | 2 | 3 | 4 | - |

Iteration 3. Set $k = 3$ , as shown by the shaded row and column in ${D}_{2}$ . The new matrices are given by ${D}_{3}$ and ${S}_{3}$ .

![bo_d56m3tv7aajc73800n00_14_518_308_1110_317_0.jpg](bo_d56m3tv7aajc73800n00_14_518_308_1110_317_0.jpg)

tion 4. Set $k = 4$ , as shown by the shaded row and column in ${D}_{3}$ . The new matrices are given by ${D}_{4}$ and ${S}_{4}$ .

${D}_{4}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 3 | 10 | 8 | 12 |
| 2 | 3 | - | 11 | 5 | 9 |
| 3 | 10 | 11 | - | 6 | 10 |
| 4 | 8 | 5 | 6 | - | 4 |
| 5 | 12 | 9 | 10 | 4 | - |

${S}_{4}$

|  | 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- | --- |
| 1 | - | 2 | 3 | 2 | 4 |
| 2 | 1 | - | 4 | 4 | 4 |
| 3 | 1 | 4 | - | 4 | 4 |
| 4 | 2 | 2 | 3 | - | 5 |
| 5 | 4 | 4 | 4 | 4 | - |

Iteration 5. Set $k = 5$ , as shown by the shaded row and column in ${D}_{4}$ . No further improvements are possible in this iteration.

The final matrices ${D}_{4}$ and ${S}_{4}$ contain all the information needed to determine the shortest route between any two nodes in the network. For example, from ${D}_{4}$ , the shortest distance from node 1 to node 5 is ${d}_{15} = {12}$ miles. To determine the associated route, recall that a segment $\left( {i, j}\right)$ represents a direct link only if ${s}_{ij} = j$ . Otherwise, $i$ and $j$ are linked through at least one other intermediate node. Because ${s}_{15} = 4 \neq  5$ , the route is initially given as $1 \rightarrow  4 \rightarrow  5$ . Now, because ${s}_{14} = 2 \neq  4$ , the segment $\left( {1,4}\right)$ is not a direct link, and $1 \rightarrow  4$ is replaced with $1 \rightarrow  2 \rightarrow  4$ , and the route $1 \rightarrow  4 \rightarrow  5$ now becomes $1 \rightarrow  2 \rightarrow  4 \rightarrow  5$ . Next, because ${s}_{12} = 2,{s}_{24} = 4$ , and ${s}_{45} = 5$ , no further "dissecting" is needed, and $1 \rightarrow  2 \rightarrow  4 \rightarrow  5$ defines the shortest route.

## TORA Moment

As in Dijkstra's algorithm, TORA can be used to generate Floyd's iterations. From SOLVE/ MODIFY menu, select Solve problem $\Rightarrow$ Iterations $\Rightarrow$ Floyd’s algorithm. File toraEx6.3-5.txt provides TORA's data for Example 6.3-5.

#### 6.3.3 Linear Programming Formulation of the Shortest-Route Problem ^srlp

This section provides an LP model for the shortest-route problem. The model is general in the sense that it can be used to find the shortest route between any two nodes in the network. In this regard, it is equivalent to Floyd's algorithm.

We wish to determine the shortest route between any two nodes $s$ and $t$ in an $n$ - node network. The LP assumes that one unit of flow enters the network at node $s$ and leaves at node $t$ .

Define

$$
{x}_{ij} = \text{ amount of flow in arc }\left( {i, j}\right)
$$

$$
= \left\{  \begin{array}{l} 1,\text{ if arc }\left( {i, j}\right) \text{ is on the shortest route } \\  0,\text{ otherwise } \end{array}\right.
$$

$$
{c}_{ij} = \text{ length of arc }\left( {i, j}\right)
$$

Thus, the objective function of the linear program becomes

$$
\text{ Minimize }z = \mathop{\sum }\limits_{\substack{\text{ all defined } \\  \text{ arcs }\left( {i, j}\right)  }}{c}_{ij}{x}_{ij}
$$

The constraints represent the conservation-of-flow equation at each node:

Total input flow $=$ Total output flow

Mathematically, this translates for node $j$ to

![bo_d56m3tv7aajc73800n00_15_402_897_1072_165_0.jpg](bo_d56m3tv7aajc73800n00_15_402_897_1072_165_0.jpg)

Example 6.3-6

In the network of Example 6.3-4, suppose that we want to determine the shortest route from node 1 to node 2-that is, $s = 1$ and $t = 2$ . Figure 6.16 shows how the unit of flow enters at node 1 and leaves at node 2.

We can see from the network that the flow-conservation equation yield

$$
\text{ Node 1: }\;1 = {x}_{12} + {x}_{13}
$$

$$
\text{ Node 2: }{x}_{12} + {x}_{42} = {x}_{23} + 1
$$

$$
\text{ Node 3: }{x}_{13} + {x}_{23} = {x}_{34} + {x}_{35}
$$

$$
\text{ Node 4: }\;{x}_{34} = {x}_{42} + {x}_{45}
$$

$$
\text{ Node 5: }{x}_{35} + {x}_{45} = 0
$$

FIGURE 6.16

Insertion of unit flow to determine shortest route between node $s = 1$ and node $t = 2$

![bo_d56m3tv7aajc73800n00_15_436_1749_1004_421_0.jpg](bo_d56m3tv7aajc73800n00_15_436_1749_1004_421_0.jpg)

The complete LP can be expressed as

|  | ${x}_{12}$ | ${x}_{13}$ | ${x}_{23}$ | ${x}_{34}$ | ${x}_{35}$ | ${x}_{42}$ | ${x}_{45}$ | RHS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Minimize $z =$ | 100 | 30 | 20 | 10 | 60 | 15 | 50 |  |
| Node 1 | 1 | 1 |  |  |  |  |  | $= 1$ |
| Node 2 | -1 |  | 1 |  |  | -1 |  | $= -1$ |
| Node 3 |  | -1 | -1 | 1 | 1 |  |  | $= 0$ |
| Node 4 |  |  |  | -1 |  | 1 | 1 | $= 0$ |
| Node 5 |  |  |  |  | -1 |  | -1 | $= 0$ |

Notice that column ${x}_{ij}$ has exactly one " 1 " in row $i$ and one " -1 " in row $j$ , a typical property of a network LP. Notice also that by examining the network, node 5 and its incoming arcs can be deleted altogether; meaning that node 5 constraint and the variables ${x}_{35}$ and ${x}_{45}$ can be removed from the LP. Of course, the given LP is sufficiently "smart" to yield ${x}_{35} = {x}_{45} = 0$ in the optimum solution.

The optimal solution (obtained by TORA, file tora Ex6.3-6.txt) is

$$
z = {55},{x}_{13} = 1,{x}_{34} = 1,{x}_{42} = 1
$$

This solution gives the shortest route from node 1 to node 2 as $1 \rightarrow  3 \rightarrow  4 \rightarrow  2$ , and the associated distance is $z = {55}$ (miles).

Remarks. The linear programming formulation is versatile in that the model can be modified to locate the shortest route between any two nodes, simply changing the location of "1" and "-1" in the right-hand side to correspond to the start and end nodes, respectively. Of course, the network in Figure 6.16 is directed, allowing one-directional flow only, and hence may result in infeasibility for certain start-end node selections (e.g., start at node 5 and end at node 1). The situation can be rectified by adding new variables to represent the new routes.

## Solver Moment ^srsolver

Figure 6.17 provides the Excel Solver spreadsheet for finding the shortest route between start node N1 and end node N2 of Example 6.3-6 (file solverEx6.3-6.xls). The input data of the model is the distance matrix in cells B3:E6. Node N1 has no column because it has no incoming arcs, and node N5 has no row because it has no outgoing arcs. An empty cell represents a nonexisting route segment (i.e., infinite length arc). (We will see shortly how the blank cell provision is recognized in the spreadsheet formulas.) Nodes N1 and N2 are designated as the start and end nodes by entering 1 in F3 and B7, respectively. These designations can be changed as desired. For example, to find the shortest route from node N2 to node N4, enter 1 in each of F4 and D7.

As explained in the LP of Example 6.3-6, the constraints of the problem are of the general form:

$$
\text{ (Net output flow) - (Net input flow) } = 0
$$

This definition is adapted to the spreadsheet layout by incorporating the external unit flow directly in Net output flow and Net input flow of the equation-that is,

$$
\left\lbrack  {\left( \begin{matrix} \text{ Out-arcs flow from }\mathrm{{Ni}} \\  \text{ to all other nodes } \end{matrix}\right)  - \left( \begin{matrix} \text{ External in-unit flow } \\  \text{ into }\mathrm{{Ni}} \end{matrix}\right)  - \left\lbrack  {\left( \begin{matrix} \text{ in-arcs flow into }\mathrm{{Ni}}\text{ from } \\  \text{ all other nodes } \end{matrix}\right)  - \left( \begin{matrix} \text{ External out-unit flow } \\  \text{ from }\mathrm{{Ni}} \end{matrix}\right) }\right\rbrack   = 0}\right\rbrack
$$

![bo_d56m3tv7aajc73800n00_17_359_209_1140_871_0.jpg](bo_d56m3tv7aajc73800n00_17_359_209_1140_871_0.jpg)

FIGURE 6.17

Excel Solver solution of the shortest route between nodes 1 and 2 in Example 6.3-6 (file solverEx6.3-6.xls)

In the spreadsheet, B3:E6 designate the input distance matrix, B9:E12 designate the solution cells, F3:F6 designate the (external) output unit-flow, and B7:E7 designate the (external) input unit-flow. Thus,

$$
\text{ Node N1 equation: [SUM(B9:E9) - F3] - [0 - 0] = 0 }
$$

$$
\text{ Node N2 equation: [SUM(B10:E10) - F4] - [SUM(B9:B12) - B7] = 0 }
$$

$$
\text{ Node N3 equation: [SUM(B11:E11) - F5] - [SUM(C9:C12) - C7] = 0 }
$$

$$
\text{ Node N4 equation: [SUM(B12:E12) - F6] - [SUM(D9:D12) - D7] = 0 }
$$

Node N5 equation: $\left\lbrack  \begin{array}{ll} 0 &  - 0 \end{array}\right\rbrack   - \left\lbrack  {\text{ SUM(E9:E12) } - \text{ E7] } = 0}\right\rbrack$

The assumption of this spreadsheet is that blank cells in the distance matrix B3:E6 represent blocked routes. We can use SUMIF, in place of SUM, to automatically account for this condition. ${}^{2}$ The following two instructions show how the modified formulas are entered in the spreadsheet.

1. Enter = SUMIF (B3:E3," >0", B9:E9) -F3 in cell F9 and copy it in cells F10:F12.

2. Enter $=$ SUMIF (B3:B6,">0", B9:B12) -B7 in cell B14 and copy it in cells C14: E14. The remainder of the spreadsheet formulas are entered as follows:

---

${}^{2}$ The idea is that the spreadsheet treats a blank cell as a zero value. If a problem happens to have a zero distance between two nodes, the zero distance can be replaced with a very small positive value.

---

1. Enter =OFFSET (A\$14,0, ROW (A1)) in cell G10 and copy it in cells G11:G13 to transpose the input flow to column G.

2. Enter 0 in each of G9 and F13 to indicate that N1 has no in-arcs or external out-unit flow and N5 has no out-arcs or external in-unit flow.

3. Enter $=$ F9-G9 in cell H9 and copy it in cells H10:H13 to compute the net flow.

4. For the objective function, enter in cell G14=SUMPRODUCT (B3:E6, B9:E12) or, equivalently, = SUMPRODUCT (distance, solution).

The spreadsheet is now ready for the application of Solver as shown in Figure 6.17. Cells B9:E12 represent the model solution. If cell (Ni, Nj) = 1, then leg (Ni, Nj) is on the shortest route. The output in Figure 6.17 yields the solution (N1-N3 = 1, N3-N4 = 1, and N4-N2 = 1). The optimal route is $1 \rightarrow  3 \rightarrow  4 \rightarrow  2$ , with a total distance of 55 miles. ${}^{3}$

Remarks. In most textbooks, the network is defined by its explicit arcs as (node $i$ , node $j$ , distance), a cumbersome modeling representation particularly when the number of arcs is large. Our model is driven by the compact distance matrix (B3:E6) and its external flows (E3:E6 and B7:E7). It may be argued, however, that our model could deal with a much larger number of variables. For instance, Example 6.3-6 has 7 arcs and hence 7 variables, as opposed to $4 \times  4 = {16}$ variables in our formulation. Keep in mind that, by using SUMIF, the flow constraints are exactly the same as in other presentations. This means that the additional 9 variables appear only in the objective function and with zero coefficients (blank entries in B3:E6). Pre-solvers in commercial software will spot this "oddity" and automatically exclude the additional variables from the objective function prior to solving the problem, thus rendering the same model as in other presentations.

## AMPL Moment ^srampl

File amplEx6.3-6a.txt provides the AMPL model for solving Example 6.3-6. The model is general in the sense that it can be used to find the shortest route between any two nodes in a problem of any size. Explanation of the model is given in Section C. 9 on the website.

### 6.4 MAXIMAL FLOW MODEL ^maxflow

Consider a network of pipelines that transports crude oil from oil wells to refineries. Intermediate booster and pumping stations are installed at appropriate design distances to move the crude in the network. Each pipe segment has a finite discharge rate (or capacity) of crude flow. A pipe segment may be uni- or bidirectional, depending on its design. Figure 6.18 demonstrates a typical pipeline network. The goal is to determine the maximum flow capacity of the network. ^mfmotivation

---

${}^{3}$ The solution of the model exhibits a curious occurrence: If the constraint netFlow $= 0$ is replaced with outFlow $=$ inflow in the Solver Parameters dialogue box, Solver fails to find a feasible solution, even after adjusting precision in the Solver Option box. (To reproduce this experience, solution cells B9:E12 must all be zero or blank.) More curious yet, if the constraints are replaced with inFlow = outFlow, the optimum is found. It is not clear why this peculiarity occurs, but the problem may be related to roundoff error. Hopefully, newer versions of Solver have accounted for this "oddity" by now.

---

![bo_d56m3tv7aajc73800n00_19_419_196_1033_461_0.jpg](bo_d56m3tv7aajc73800n00_19_419_196_1033_461_0.jpg)

FIGURE 6.18

Capacitated network connecting wells and refineries through booster stations

![bo_d56m3tv7aajc73800n00_19_453_824_427_92_0.jpg](bo_d56m3tv7aajc73800n00_19_453_824_427_92_0.jpg)

FIGURE 6.19

Arc Flows ${C}_{ij}$ from $i \rightarrow  j$ and ${C}_{ji}$ from $j \rightarrow  i$

The solution of the proposed problem requires adding a single source and a single sink using unidirectional infinite capacity arcs, as shown by dashed arcs in Figure 6.18.

For arc $\left( {i, j}\right)$ , the notation $\left( {{C}_{ij},{C}_{ji}}\right)$ gives the flow capacities in the two directions $i \rightarrow  j$ and $j \rightarrow  i$ . To eliminate ambiguity, we place ${C}_{ij}$ next to node $i$ and ${C}_{ji}$ next to node $j$ , as shown in Figure 6.19.

#### 6.4.1 Enumeration of Cuts ^cuts

A cut defines a set of arcs whose removal from the network disrupts flow between the source and sink nodes. The cut capacity equals the sum of the capacities of its set of arcs. Among all possible cuts in the network, the cut with the smallest capacity is the bottleneck that determines the maximum flow in the network.

## Example 6.4-1

Consider the network in Figure 6.20. The bidirectional capacities are shown on the respective arcs using the convention in Figure 6.19. For example, for arc (3, 4), the flow limit is 10 units from 3 to 4 and 5 units from 4 to 3 .

Figure 6.20 illustrates three cuts with the following capacities:

| Cut | Associated arcs | Capacity |
| --- | --- | --- |
| 1 | $\left( {1,2}\right) ,\left( {1,3}\right) ,\left( {1,4}\right)$ | ${20} + {30} + {10} = {60}$ |
| 2 | $\left( {1,3}\right) ,\left( {1,4}\right) ,\left( {2,3}\right) ,\left( {2,5}\right)$ | ${30} + {10} + {40} + {30} = {110}$ |
| 3 | $\left( {2,5}\right) ,\left( {3,5}\right) ,\left( {4,5}\right)$ | ${30} + {20} + {20} = {70}$ |

The only information from the three cuts is that the maximum flow in the network cannot exceed 60 units. To determine the maximum flow, it is necessary to enumerate all the cuts, a difficult task for the general network. Thus, the need for an efficient algorithm is imperative.

![bo_d56m3tv7aajc73800n00_20_593_199_772_625_0.jpg](bo_d56m3tv7aajc73800n00_20_593_199_772_625_0.jpg)

FIGURE 6.20

Examples of cuts in flow networks

#### 6.4.2 Maximal Flow Algorithm ^mfalgos

The maximal flow algorithm is based on finding breakthrough paths with positive flow between the source and sink nodes. Each path commits part or all of the capacities of its arcs to the total flow in the network.

Consider arc $\left( {i, j}\right)$ with the bidirectional (design) capacities $\left( {{C}_{ij},{C}_{ji}}\right)$ . As portions of these capacities are committed to the flow in the arc, the residuals (or unused capacities) of the arc are updated. We use the notation $\left( {{c}_{ij},{c}_{ji}}\right)$ to represent the residuals.

For a node $j$ that receives flow from node $i$ , we attach a label $\left\lbrack  {{a}_{j}, i}\right\rbrack$ , where ${a}_{j}$ is the flow from node $i$ to node $j$ .

Step 1. For all arcs $\left( {i, j}\right)$ , set the residual capacity equal to the design capacity - that is, $\left( {{c}_{ij},{c}_{ji}}\right)  = \left( {{C}_{ij},{C}_{ji}}\right)$ . Let ${a}_{1} = \infty$ , and label source node 1 with $\left\lbrack  {\infty , - }\right\rbrack$ . Set $i = 1$ , and go to step 2 .

Step 2. Determine ${S}_{i}$ , the set of unlabeled nodes $j$ that can be reached directly from node $i$ by arcs with positive residuals (i.e., ${c}_{ij} > 0$ for all $j \in  {S}_{i}$ ). If ${S}_{i} \neq  \varnothing$ , go to step 3 . Otherwise, a partial path is dead-ended at node $i$ . Go to step 4.

Step 3. Determine $k \in  {S}_{i}$ such that

$$
{c}_{ik} = \mathop{\max }\limits_{{{j\varepsilon }{S}_{i}}}\left\{  {c}_{ij}\right\}
$$

Set ${a}_{k} = {c}_{ik}$ and label node $k$ with $\left\lbrack  {{a}_{k}, i}\right\rbrack$ . If $k = n$ , the sink node has been labeled, and a breakthrough path is found, go to step 5 . Otherwise, set $i = k$ , and go to step 2.

Step 4. (Backtracking). If $i = 1$ , no breakthrough is possible; go to step 6. Otherwise, let $r$ be the node (on the partial path) that was labeled immediately before current node $i$ , and remove $i$ from the set of nodes adjacent to $r$ . Set $i = r$ , and go to step 2.

Step 5. (Determination of residuals). Let ${N}_{p} = \left( {1,{k}_{1},{k}_{2},\ldots , n}\right)$ define the nodes of the $p$ th breakthrough path from source node 1 to sink node $n$ . Then the maximum flow along the path is computed as

$$
{f}_{p} = \min \left\{  {{a}_{1},{a}_{{k}_{1}},{a}_{{k}_{2}},\ldots ,{a}_{n}}\right\}
$$

The residual capacity of each arc along the breakthrough path is decreased by ${f}_{p}$ in the direction of the flow and increased by ${f}_{p}$ in the reverse direction-that is, for nodes $i$ and $j$ on the path, the residual flow is changed from the current $\left( {{c}_{ij},{c}_{ji}}\right)$ to

(a) $\;\left( {{c}_{ij} - {f}_{p},{c}_{ji} + {f}_{p}}\right)$ if the flow is from $i$ to $j$

(b) $\left( {{c}_{ij} + {f}_{p},{c}_{ji} - {f}_{p}}\right)$ if the flow is from $j$ to $i$

Reinstate any nodes that were removed in step 4. Set $i = 1$ , and return to step 2.

Step 6. (Solution).

(a) Given that $m$ breakthrough paths have been determined, the maximal flow in the network is

$$
F = {f}_{1} + {f}_{2} + \ldots  + {f}_{m}
$$

(b) Using the (initial) design capacities and final residuals of arc $\left( {i, j}\right)$ , $\left( {{C}_{ij},{C}_{ji}}\right)$ , and $\left( {{c}_{ij},{c}_{ji}}\right)$ , respectively, the optimal flow in arc $\left( {i, j}\right)$ is determined by computing $\left( {\alpha ,\beta }\right)  = \left( {{C}_{ij} - {c}_{ij},{C}_{ji} - {c}_{ji}}\right)$ . If $\alpha  > 0$ , the optimal flow from $i$ to $j$ is $\alpha$ . Otherwise, if $\beta  > 0$ , the optimal flow from $j$ to $i$ is $\beta$ . (It is impossible to have both $\alpha$ and $\beta$ positive.)

The backtracking process of step 4 is invoked when the algorithm dead-ends at an intermediate node. The flow adjustment in step 5 can be explained via the simple flow network in Figure 6.21. Network (a) gives the first breakthrough path ${N}_{1} = \{ 1,2,3,4\}$ with its maximum flow ${f}_{1} = 5$ . Thus, the residuals of each of arcs $\left( {1,2}\right) ,\left( {2,3}\right)$ , and $\left( {3,4}\right)$ are changed from $\left( {5,0}\right)$ to $\left( {0,5}\right)$ , per step 5 . Network (b) now gives the second breakthrough path ${N}_{2} = \{ 1,3,2,4\}$ with ${f}_{2} = 5$ . After making the necessary flow adjustments, we get network (c), where no further breakthroughs are possible. What happened in the transition from (b) to (c) is nothing but a cancellation of a previously committed flow in the direction $2 \rightarrow  3$ , in essence allowing the flow to on paths $1 \rightarrow  2 \rightarrow  4$ and $1 \rightarrow  3 \rightarrow  4$ only (maximum flow $= 5 + 5 = {10}$ ). The algorithm "remembers" that a flow from 2 to 3 has been committed previously because of the earlier adjustment of the capacity in the reverse direction (per step 5).

FIGURE 6.21

Use of residuals to calculate maximum flow

![bo_d56m3tv7aajc73800n00_21_305_1714_1267_424_0.jpg](bo_d56m3tv7aajc73800n00_21_305_1714_1267_424_0.jpg)

## Example 6.4-2

Determine the maximal flow in the network of Example 6.4-1 (Figure 6.20). Figure 6.22 provides a graphical summary of the iterations of the algorithm. You will find it helpful to compare the description of the iterations with the graphical summary.

Iteration 1. Set the initial residuals $\left( {{c}_{ij},{c}_{ji}}\right)$ equal to the initial capacities $\left( {{C}_{ij},{C}_{ji}}\right)$ .

Step 1. Set ${a}_{1} = \infty$ and label node 1 with $\left\lbrack  {\infty , - }\right\rbrack$ . Set $i = 1$ .

Step 2. ${S}_{1} = \{ 2,3,4\} \left( { \neq  \varnothing }\right)$ .

Step 3. $k = 3$ , because ${c}_{13} = \max \left\{  {{c}_{12},{c}_{13},{c}_{14}}\right\}   = \max \{ {20},{30},{10}\}  = {30}$ . Set ${a}_{3} = {c}_{13} = {30}$ , and label node 3 with $\left\lbrack  {{30},1}\right\rbrack$ . Set $i = 3$ , and repeat step 2 .

Step 2. ${S}_{3} = \left( {4,5}\right)$ .

Step 3. $k = 5$ and ${a}_{5} = {c}_{35} = \max \{ {10},{20}\}  = {20}$ . Label node 5 with $\left\lbrack  {{20},3}\right\rbrack$ . Breakthrough is achieved. Go to step 5.

Step 5. The breakthrough path is determined from the labels starting at node 5 and moving backward to node 1 - that is, $\left( \mathbf{5}\right)  \rightarrow  \left\lbrack  {{20},\mathbf{3}}\right\rbrack   \rightarrow  \left( \mathbf{3}\right)  \rightarrow  \left\lbrack  {{30},\mathbf{1}}\right\rbrack   \rightarrow  \left( \mathbf{1}\right)$ . Thus, ${N}_{1} = \{ 1,3,5\}$ and ${f}_{1} = \min \left\{  {{a}_{1},{a}_{3},{a}_{5}}\right\}   = \{ \infty ,{30},{20}\}  = {20}$ . The residual capacities along path ${N}_{1}$ are

$$
\left( {{c}_{13},{c}_{31}}\right)  = \left( {{30} - {20},0 + {20}}\right)  = \left( {{10},{20}}\right)
$$

$$
\left( {{c}_{35},{c}_{53}}\right)  = \left( {{20} - {20},0 + {20}}\right)  = \left( {0,{20}}\right)
$$

Iteration 2.

Step 1. Set ${a}_{1} = \infty$ , and label node 1 with $\left\lbrack  {\infty , - }\right\rbrack$ . Set $i = 1$ .

Step 2. ${S}_{1} = \{ 2,3,4\}$ .

Step 3. $k = 2$ and ${a}_{2} = {c}_{12} = \max \{ {20},{10},{10}\}  = {20}$ . Set $i = 2$ , and repeat step 2.

Step 2. ${S}_{2} = \{ 3,5\}$ .

Step 3. $k = 3$ and ${a}_{3} = {c}_{23} = {40}$ . Label node 3 with $\left\lbrack  {{40},2}\right\rbrack$ . Set $i = 3$ , and repeat step 2 .

Step 2. ${S}_{3} = \{ 4\}$ (note that ${c}_{35} = 0$ -hence, node 5 cannot be included in ${S}_{3}$ ).

Step 3. $k = 4$ and ${a}_{4} = {c}_{34} = {10}$ . Label node 4 with $\left\lbrack  {{10},3}\right\rbrack$ . Set $i = 4$ , and repeat step 2 .

Step 2. ${S}_{4} = \{ 5\}$ (note that nodes 1 and 3 are already labeled-hence, they cannot be included in ${S}_{4}$ ).

Step 3. $k = 5$ and ${a}_{5} = {c}_{45} = {20}$ . Label node 5 with $\left\lbrack  {{20},4}\right\rbrack$ . Breakthrough has been achieved. Go to step 5.

![bo_d56m3tv7aajc73800n00_23_291_188_1292_1474_0.jpg](bo_d56m3tv7aajc73800n00_23_291_188_1292_1474_0.jpg)

FIGURE 6.22

Iterations of the maximum flow algorithm of Example 6.4-2

Step 5. ${N}_{2} = \{ 1,2,3,4,5\}$ and ${f}_{2} = \min \{ \infty ,{20},{40},{10},{20}\}  = {10}$ . The residuals along the path of ${N}_{2}$ are

$$
\left( {{c}_{12},{c}_{21}}\right)  = \left( {{20} - {10},0 + {10}}\right)  = \left( {{10},{10}}\right)
$$

$$
\left( {{c}_{23},{c}_{32}}\right)  = \left( {{40} - {10},0 + {10}}\right)  = \left( {{30},{10}}\right)
$$

$$
\left( {{c}_{34},{c}_{43}}\right)  = \left( {{10} - {10},5 + {10}}\right)  = \left( {0,{15}}\right)
$$

$$
\left( {{c}_{45},{c}_{54}}\right)  = \left( {{20} - {10},0 + {10}}\right)  = \left( {{10},{10}}\right)
$$

Iteration 3.

Step 1. Set ${a}_{1} = \infty$ and label node 1 with $\left\lbrack  {\infty , - }\right\rbrack$ . Set $i = 1$ .

Step 2. ${S}_{1} = \{ 2,3,4\}$ .

Step 3. $k = 2$ and ${a}_{2} = {c}_{12} = \max \{ {10},{10},{10}\}  = {10}$ . (Though ties are broken arbitrarily, TORA always selects the tied node with the smallest index. We will use this convention throughout the example.) Label node 2 with $\left\lbrack  {{10},1}\right\rbrack$ . Set $i = 2$ , and repeat step 2 .

Step 2. ${S}_{2} = \{ 3,5\}$ .

Step 3. $k = 3$ and ${a}_{3} = {c}_{23} = {30}$ . Label node 3 with $\left\lbrack  {{30},2}\right\rbrack$ . Set $i = 3$ , and repeat step 2 .

Step 2. ${S}_{3} = \varnothing$ (because ${c}_{34} = {c}_{35} = 0$ ). Go to step 4 to backtrack.

Step 4. Backtracking. The label $\left\lbrack  {{30},2}\right\rbrack$ at node 3 gives the immediately preceding node $r = 2$ . Remove node 3 from further consideration in this iteration by crossing it out. Set $i = r = 2$ , and repeat step 2 .

Step 2. ${S}_{2} = \{ 5\}$ (note that node 3 has been removed in the backtracking step).

Step 3. $k = 5$ and ${a}_{5} = {c}_{25} = {30}$ . Label node 5 with [30,2]. Breakthrough has been achieved go to step 5 .

Step 5. ${N}_{3} = \{ 1,2,5\}$ and ${c}_{5} = \min \{ \infty ,{10},{30}\}  = {10}$ . The residuals along the path of ${N}_{3}$ are

$$
\left( {{c}_{12},{c}_{21}}\right)  = \left( {{10} - {10},{10} + {10}}\right)  = \left( {0,{20}}\right)
$$

$$
\left( {{c}_{25},{c}_{52}}\right)  = \left( {{30} - {10},0 + {10}}\right)  = \left( {{20},{10}}\right)
$$

Iteration 4.

This iteration yields ${N}_{4} = \{ 1,3,2,5\}$ with ${f}_{4} = {10}$ (verify!).

## Iteration 5.

This iteration yields ${N}_{5} = \{ 1,4,5\}$ with ${f}_{5} = {10}$ (verify!).

## Iteration 6.

All the arcs out of node 1 have zero residuals. Hence, no further breakthroughs are possible. We turn to step 6 to determine the solution.

Step 6. Maximal flow in the network is $F = {f}_{1} + {f}_{2} + \ldots  + {f}_{5} = {20} + {10} + {10} + {10} + \; {10} = {60}$ units. The flow in the individual arcs is computed by subtracting the last residuals $\left( {{c}_{ij},{c}_{ji}}\right)$ in iteration 6 from the design capacities $\left( {{C}_{ij},{C}_{ji}}\right)$ , as the following table shows:

| Arc | $\left( {{C}_{ij},{C}_{ji}}\right)  - {\left( {c}_{ij},{c}_{ji}\right) }_{6}$ | Flow amount | Direction |
| --- | --- | --- | --- |
| (1,2) | $\left( {{20},0}\right)  - \left( {0,{20}}\right)  = \left( {{20}, - {20}}\right)$ | 20 | $1 \rightarrow  2$ |
| (1,3) | $\left( {{30},0}\right)  - \left( {0,{30}}\right)  = \left( {{30}, - {30}}\right)$ | 30 | $1 \rightarrow  3$ |
| (1,4) | $\left( {{10},0}\right)  - \left( {0,{10}}\right)  = \left( {{10}, - {10}}\right)$ | 10 | $1 \rightarrow  4$ |
| (2,3) | $\left( {{40},0}\right)  - \left( {{40},0}\right)  = \left( {0,0}\right)$ | 0 | - |
| (2,5) | $\left( {{30},0}\right)  - \left( {{10},{20}}\right)  = \left( {{20}, - {20}}\right)$ | 20 | $2 \rightarrow  5$ |
| (3, 4) | $\left( {{10},5}\right)  - \left( {0,{15}}\right)  = \left( {{10}, - {10}}\right)$ | 10 | $3 \rightarrow  4$ |
| (3, 5) | $\left( {{20},0}\right)  - \left( {0,{20}}\right)  = \left( {{20}, - {20}}\right)$ | 20 | $3 \rightarrow  5$ |
| (4,3) | $\left( {5,{10}}\right)  - \left( {{15},0}\right)  = \left( {-{10},{10}}\right)$ | 0 | - |
| (4,5) | $\left( {{20},0}\right)  - \left( {0,{20}}\right)  = \left( {{20}, - {20}}\right)$ | 20 | $4 \rightarrow  5$ |

## TORA Moment

You can use TORA to solve the maximal flow model in an automated mode or one iteration at a time. From the SOLVE/MODIFY menu, select Solve Problem. After specifying the output format, go to the output screen and select either Maximum Flows or Iterations. File toraEx6.4-2. txt provides TORA's data for Example 6.4-2.

#### 6.4.3 Linear Programming Formulation of Maximal Flow Mode ^mflp

Define ${x}_{ij}$ as the amount of flow in arc $\left( {i, j}\right)$ with capacity ${C}_{ij}$ . The objective is to determine ${x}_{ij}$ for all $i$ and $j$ that maximizes the flow between start node $s$ and terminal node $t$ subject to flow restrictions (input flow = output flow) at all but nodes $s$ and $t$ .

## Example 6.4-3

In the maximal flow model of Figure 6.22 (Example 6.4-2), $s = 1$ and $t = 5$ . The following table summarizes the associated LP with two different, but equivalent, objective functions depending on whether we maximize the output from start node $1\left( { = {z}_{1}}\right)$ or the input to terminal node $5\left( { = {z}_{2}}\right)$ .

|  | ${x}_{12}$ | ${x}_{13}$ | ${x}_{14}$ | ${x}_{23}$ | ${x}_{25}$ | ${x}_{34}$ | ${x}_{35}$ | ${x}_{43}$ | ${x}_{45}$ | RHS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Maximize ${z}_{1} =$<br>Maximize ${z}_{2} =$ | 1 | 1 | 1 |  | 1 |  | 1 |  | 1 |  |
| Node 2 | 1 |  |  | -1 | -1 |  |  |  |  | $= 0$ |
| Node 3 |  | 1 |  | 1 |  | -1 | -1 | 1 |  | $= 0$ |
| Node 4 |  |  | 1 |  |  | 1 |  | -1 | -1 | $= 0$ |
| Capacity | 20 | 30 | 10 | 40 | 30 | 10 | 20 | 5 | 20 |  |

The optimal solution using either objective function is

$$
{x}_{12} = {20},{x}_{13} = {30},{x}_{14} = {10},{x}_{25} = {20},{x}_{34} = {10},{x}_{35} = {20},{x}_{45} = {20}
$$

The associated maximum flow is ${z}_{1} = {z}_{2} = {60}$ .

## Solver Moment ^mfsolver

Figure 6.23 gives the Excel Solver model for the maximum flow model of Example 6.4-2 (file solverEx6.4-2.xls). The general idea is similar to that of the shortest-route model, detailed following Example 6.3-6. The main differences include: (1) there are no flow equations for the start node 1 and end node 5, and (2) the objective is to maximize the total outflow at start node 1 (F9) or, equivalently, the total inflow at terminal node 5 (G13). File solverEx6.4-2.xls uses G13 as the target cell. Try executing the model with G13 replacing F9.

![bo_d56m3tv7aajc73800n00_26_376_195_1213_897_0.jpg](bo_d56m3tv7aajc73800n00_26_376_195_1213_897_0.jpg)

FIGURE 6.23

Excel Solver solution of the maximal flow model of 6.4-2 (file solverEx6.4-2.xls)

## AMPL Moment ^mfampl

File amplEx6.4-2.txt provides the AMPL model for the maximal flow problem between any two nodes in the network of Example 6.4-2. The model is applicable to any number of nodes. Explanation of the model is detailed in Section C.9 on the website.

### 6.5 CPM AND PERT ^cpmpert

CPM (Critical Path Method) and PERT (Program Evaluation and Review Technique) are network-based methods designed to assist in the planning, scheduling, and control of projects. A project is defined as a collection of interrelated activities with each activity consuming time and resources. The objective of CPM and PERT is to devise analytic tools for scheduling the activities. Figure 6.24 summarizes the steps of the techniques. First, we define the activities of the project, their precedence relationships, and their time requirements. Next, the precedence relationships among the activities are modeled as a network. The third step involves specific computations for developing the time schedule. During the actual execution phase, execution of the activities may not proceed as planned, in the sense that some of the activities may be expedited or delayed. When this happens, the schedule is updated to reflect the realities on the ground. This is the reason for including a feedback loop in Figure 6.24.

![bo_d56m3tv7aajc73800n00_27_419_199_1038_284_0.jpg](bo_d56m3tv7aajc73800n00_27_419_199_1038_284_0.jpg)

FIGURE 6.24

Phases for project planning with CPM-PERT

The two techniques, CPM and PERT, were developed independently. They differ in that CPM assumes deterministic activity durations and PERT assumes probabilistic durations. ^cpmdiff

#### 6.5.1 Network Representation ^netrep

Each activity is represented by an arc pointing in the direction of progress in the project. The nodes of the network establish the precedence relationships among the different activities. Three rules are available for constructing the network.

Rule 1. Each activity is represented by one, and only one, arc.

Rule 2. Each activity must be identified by two distinct end nodes.

Figure 6.25 shows how a dummy activity can be used to provide unique representation of two concurrent activities, $A$ and $B$ . By definition, a (dashed) dummy activity consumes no time or resources. Inserting a dummy activity in one of the four ways shown in Figure 6.25 maintains the concurrence of $A$ and $B$ and provides unique end nodes for the two activities (to satisfy rule 2).

FIGURE 6.25

Use of dummy activity to produce unique representation of concurrent activities

![bo_d56m3tv7aajc73800n00_27_332_1646_1202_525_0.jpg](bo_d56m3tv7aajc73800n00_27_332_1646_1202_525_0.jpg)

![bo_d56m3tv7aajc73800n00_28_477_202_547_297_0.jpg](bo_d56m3tv7aajc73800n00_28_477_202_547_297_0.jpg)

FIGURE 6.26

Use of dummy activity to ensure correct precedence relationship

Rule 3. To maintain the correct precedence relationships, the following questions must be answered as each activity is added to the network:

(a) What activities immediately precede the current activity?

(b) What activities immediately follow the current activity?

(c) What activities are concurrent with the current activity?

The answers to these questions may require the use of dummy activities to ensure correct precedence among the activities. For example, consider the following segment of a project:

1. Activity $C$ starts immediately after activities $A$ and $B$ have been completed.

2. Activity $E$ can start after activity $B$ is completed.

Part (a) of Figure 6.26 shows the incorrect representation of the precedence relationship because it requires both $A$ and $B$ to be completed before $E$ can start. In part (b), the use of a dummy activity rectifies the situation.

## Example 6.5-1

A publisher has a contract with an author to publish a textbook. The author submits a hard copy and a computer file of the manuscript. The (simplified) activities associated with the production of the textbook are summarized in the following table:

| Activity | Predecessor(s) | Duration (weeks) |
| --- | --- | --- |
| $A$: Manuscript proofreading by editor | - | 3 |
| $B$: Sample pages preparation | - | 2 |
| $C$: Book cover design | - | 4 |
| $D$: Artwork preparation | - | 3 |
| $E$: Author's approval of edited manuscript and sample pages | $A, B$ | 2 |
| $F$: Book formatting | $E$ | 4 |
| $G$: Author’s review of formatted pages | $F$ | 2 |
| $H$: Author’s review of artwork | $D$ | 1 |
| $I$: Production of printing plates | $G, H$ | 2 |
| $J$: Book production and binding | $C, I$ | 4 |

Figure 6.27 provides the project network. Dummy activity $\left( {2,3}\right)$ produces unique end nodes for concurrent activities $A$ and $B$ . It is convenient to number the nodes in ascending order pointing toward the direction of progress in the project.

![bo_d56m3tv7aajc73800n00_29_302_196_1270_267_0.jpg](bo_d56m3tv7aajc73800n00_29_302_196_1270_267_0.jpg)

FIGURE 6.27

Project network for Example 6.5-1

#### 6.5.2 Critical Path Method (CPM) Computations ^cpm

The end result in CPM is a time schedule for the project (see Figure 6.24). To achieve this goal, special computations are carried out to produce the following information:

1. Total duration needed to complete the project

2. Classification of the activities of the project as critical and noncritical

An activity is critical if its start and finish times are predetermined (fixed). A activity is noncritical if it can be scheduled in a time span greater than its duration, permitting flexible start and finish times (within limits). A delay in the start time of a critical activity definitely causes a delay in the completion of the entire project, whereas a delay in a noncritical activity may not affect the completion date of the project.

To carry out the necessary computations, we define an event as a point in time at which activities are completed and succeeding ones are started. In terms of the network, an event corresponds to a node. Let

$$
{\square }_{j} = \text{ Earliest occurrence time of event }j
$$

$$
{\Delta }_{j} = \text{ Latest occurrence time of event }j
$$

$$
{D}_{ij} = \text{ Duration of activity }\left( {i, j}\right)
$$

All event occurrence times are measured from the start time of the project. The span $\left( {{\square }_{i},{\Delta }_{j}}\right)$ defines the time period during which activity $\left( {i, j}\right)$ , of duration ${D}_{ij}$ , is scheduled. If activity $\left( {i, j}\right)$ is critical, then ${D}_{ij} = {\Delta }_{j} - {\square }_{i}$ . Otherwise, ${D}_{ij} < {\Delta }_{j} - {\square }_{i}$ for noncritical activity $\left( {i, j}\right)$ .

The critical path calculations involve two passes: The forward pass determines the earliest occurrence times of the events, and the backward pass calculates their latest occurrence times.

Forward pass (earliest occurrence times, $\square$ ). The computations start at node 1 and advance recursively to node $n$ .

Initial Step. Set ${\square }_{1} = 0$ to indicate that the project starts at time 0 .

General Step $j$ . Given that nodes $p, q,\ldots$ , and $v$ are linked directly to node $j$ by incoming activities $\left( {p, j}\right) ,\left( {q, j}\right) ,\ldots$ , and $\left( {v, j}\right)$ and that the earliest occurrence times of events (nodes) $p, q,\ldots$ , and $v$ have already been computed, then the earliest occurrence time of event $j$ is computed as

$$
{\square }_{j} = \max \left\{  {{\square }_{p} + {D}_{pj},{\square }_{q} + {D}_{qj},\ldots ,{\square }_{v} + {D}_{vj}}\right\}
$$

The forward pass is complete when ${\square }_{n}$ at node $n$ has been computed. By definition, ${\square }_{j}$ is the longest path (duration) to node $j$ .

Backward pass (latest occurrence times, $\Delta$ ). The backward pass computations start at node $n$ and ends at node 1 .

Initial Step. Set ${\Delta }_{n} = {\square }_{n}$ to indicate that latest occurrences of the last node equals the duration of the project.

General Step $j$ . Given that nodes $p, q,\ldots$ , and $v$ are linked directly to node $j$ by outgoing activities $\left( {j, p}\right) ,\left( {j, q}\right) ,\ldots$ , and $\left( {j, v}\right)$ and that the latest occurrence times of nodes $p, q,\ldots$ , and $v$ have already been computed, the latest occurrence time of node $j$ is $c$ .

$$
{\Delta }_{j} = \min \left\{  {{\Delta }_{p} - {D}_{jp},{\Delta }_{q} - {D}_{jq},\ldots ,{\Delta }_{v} - {D}_{jv}}\right\}
$$

The backward pass ends with ${\Delta }_{1} = 0$ at node 1 .

Based on the preceding calculations, an activity $\left( {i, j}\right)$ will be critical if it satisfies three conditions.

1. ${\Delta }_{i} = {\square }_{i}$

2. ${\Delta }_{j} = {\square }_{j}$

3. ${\Delta }_{j} - {\square }_{i} = {D}_{ij}$

The three conditions state that the earliest and latest occurrence times of end nodes $i$ and $j$ are equal, and the duration ${D}_{ij}$ fits "snugly" in the specified time span. An activity that does not satisfy all three conditions is noncritical.

By definition, the critical activities of a network constitute the longest path spanning the project network from start to finish.

## Example 6.5-2

Determine the critical path for the project network in Figure 6.28. All the durations are in days.

## Forward Pass

Node 1. Set ${\square }_{1} = 0$

Node 2. ${\square }_{2} = {\square }_{1} + {D}_{12} = 0 + 5 = 5$

Node 3. ${\square }_{3} = \max \left\{  {{\square }_{1} + {D}_{13},{\square }_{2} + {D}_{23}}\right\}   = \max \{ 0 + 6,5 + 3\}  = 8$

![bo_d56m3tv7aajc73800n00_31_363_199_1144_674_0.jpg](bo_d56m3tv7aajc73800n00_31_363_199_1144_674_0.jpg)

FIGURE 6.28

Forward and backward pass calculations for the project of Example 6.5-2

---

Node 4. ${\square }_{4} = {\square }_{2} + {D}_{24} = 5 + 8 = {13}$

Node 5. ${\square }_{5} = \max \left\{  {{\square }_{3} + {D}_{35},{\square }_{4} + {D}_{45}}\right\}   = \max \{ 8 + 2,{13} + 0\}  = {13}$

Node 6. ${\square }_{6} = \max \left\{  {{\square }_{3} + {D}_{36},{\square }_{4} + {D}_{46},{\square }_{5} + {D}_{56}}\right\}$

	$= \max \{ 8 + {11},{13} + 1,{13} + {12}\}  = {25}$

---

The computations show that the project can be completed in 25 days.

## Backward Pass

---

	Node 6. Set ${\Delta }_{6} = {\square }_{6} = {25}$

	Node 5. ${\Delta }_{5} = {\Delta }_{6} - {D}_{56} = {25} - {12} = {13}$

Node 4. ${\Delta }_{4} = \min \left\{  {{\Delta }_{6} - {D}_{46},{\Delta }_{5} - {D}_{45}}\right\}   = \min \{ {25} - 1,{13} - 0\}  = {13}$

	Node 3. ${\Delta }_{3} = \min \left\{  {{\Delta }_{6} - {D}_{36},{\Delta }_{5} - {D}_{35}}\right\}   = \min \{ {25} - {11},{13} - 2\}  = {11}$

	Node 2. ${\Delta }_{2} = \min \left\{  {{\Delta }_{4} - {D}_{24},{\Delta }_{3} - {D}_{23}}\right\}   = \min \{ {13} - 8,{11} - 3\}  = 5$

Node 1. ${\Delta }_{1} = \min \left\{  {{\Delta }_{3} - {D}_{13},{\Delta }_{2} - {D}_{2}}\right\}   = \min \{ {11} - 6,5 - 5\}  = 0$

---

Correct computations will always end with ${\Delta }_{1} = 0$ . The computations can be made directly on the network as shown in Figure 6.28.

As expected, the critical path $1 \rightarrow  2 \rightarrow  4 \rightarrow  5 \rightarrow  6$ spans the network from start (node 1) to finish (node 6). The sum of the durations of the critical activities $\lbrack \left( {1,2}\right) ,\left( {2,4}\right) ,\left( {4,5}\right)$ , and $\left( {5,6}\right) \rbrack$ equals the duration of the project $\left( { = {25}\text{ days }}\right)$ . Observe that activity $\left( {4,6}\right)$ satisfies the first two conditions for a critical activity $\left( {{\Delta }_{4} = {\square }_{4} = {13}}\right.$ and $\left. {{\Delta }_{6} = {\square }_{6} = {25}}\right)$ but not the third $\left( {{\Delta }_{6} - {\square }_{4} \neq  {D}_{46}}\right)$ . Hence, the activity is noncritical.

#### 6.5.3 Construction of the Time Schedule ^floats

This section shows how the information obtained from the calculations in Section 6.5.2 can be used to develop the time schedule. We recognize that for an activity $\left( {i, j}\right) ,{\square }_{i}$ represents the earliest start time, and ${\Delta }_{j}$ represents the latest completion time. Thus, the interval $\left( {{\square }_{i},{\Delta }_{j}}\right)$ delineates the (maximum) time span during which activity $\left( {i, j}\right)$ can be scheduled without causing a delay in the entire project.

Construction of Preliminary Schedule. The method for constructing a preliminary schedule is illustrated by an example.

## Example 6.5-3

Determine the time schedule for the project of Example 6.5-2 (Figure 6.28).

We can get a preliminary time schedule for the different activities of the project by delineating their respective time spans as shown in Figure 6.29.

1. The critical activities (shown by solid lines) are staggered one right after the other to ensure that the project is completed within its specified 25-day duration.

2. The noncritical activities (shown by dashed lines) have permissible time spans greater than their respective durations, thus allowing slack (or "leeway") in scheduling them within their allotted time intervals.

How do we schedule the noncritical activities within their respective spans? Normally, it is preferable to start each noncritical activity as early as possible. In this manner, remaining slack periods can be used to compensate for unexpected delays in the activity. It may be necessary, however, to delay the start of a noncritical activity past its earliest start time. For example, in Figure 6.29, suppose that each of the noncritical activities $E$ and $F$ requires the use of a bulldozer and that only one is available. Scheduling both $E$ and $F$ as early as possible requires two bulldozers between times 8 and 10. We can remove the overlap by starting $E$ at time 8 and pushing the start time of $F$ to somewhere between times 10 and 14 .

FIGURE 6.29

Preliminary schedule for the project of Example 6.5-2

![bo_d56m3tv7aajc73800n00_32_365_1408_1232_697_0.jpg](bo_d56m3tv7aajc73800n00_32_365_1408_1232_697_0.jpg)

If all the noncritical activities can be scheduled as early as possible, the resulting schedule is always feasible. Otherwise, some precedence relationships may be violated if noncritical activities are delayed past their earliest time. Take, for example, activities $C$ and $E$ in Figure 6.29. In the project network (Figure 6.28), though $C$ must be completed before $E$ , the spans of $C$ and $E$ in Figure 6.29 allow scheduling $C$ between times 6 and 9, and $E$ between times 8 and 10, which violates the requirement that $C$ precede $E$ . The need for a "red flag" that automatically reveals schedule conflict is thus evident. Such information is provided by computing the floats for the noncritical activities.

Determination of the floats. Floats are the slack times available within the allotted span of the noncritical activity. The most common types are the total float and the free float.

Figure 6.30 gives a convenient summary for computing the total float $\left( {T{F}_{ij}}\right)$ and the free float $\left( {F{F}_{ij}}\right)$ for an activity $\left( {i, j}\right)$ .

$$
T{F}_{ij} = {\Delta }_{j} - {\square }_{i} - {D}_{ij}
$$

$$
F{F}_{ij} = {\square }_{j} - {\square }_{i} - {D}_{ij}
$$

By definition, $F{F}_{ij} \leq  T{F}_{ij}$ .

Red-Flagging Rule. For a noncritical activity $\left( {i, j}\right)$ , if $F{F}_{ij} < T{F}_{ij}$ , then its start can be delayed by at most $F{F}_{ij}$ , relative to its earliest start time ${\overrightarrow{\square }}_{i}$ , without causing schedule conflict. Any delay larger than $F{F}_{ij}$ (but not more than $T{F}_{ij}$ ) must be coupled with an equal delay (relative to ${\square }_{j}$ ) in the start time of all the activities leaving node $j$ .

The implication of the rule is that, if $F{F}_{ij} = T{F}_{ij}$ , a noncritical activity $\left( {i, j}\right)$ can be scheduled anywhere in the interval $\left( {{\square }_{i},{\Delta }_{j}}\right)$ without causing schedule conflict. Otherwise, if $F{F}_{ij} < T{F}_{ij}$ , activity $\left( {i, j}\right)$ is red-flagged for the possibility of causing delay in the start time of the activities leaving node $j$ .

FIGURE 6.30

Computation of total and free floats

![bo_d56m3tv7aajc73800n00_33_561_1730_751_447_0.jpg](bo_d56m3tv7aajc73800n00_33_561_1730_751_447_0.jpg)

Example 6.5-4

Compute the floats for the noncritical activities of the network in Example 6.5-2, and discuss their use in finalizing a schedule for the project.

The following table summarizes the computations of the total and free floats. For manual computations, it is more convenient to do the calculations directly on the network using the procedure in Figure 6.30.

| Noncritical activity | Duration | Total float (TF) | Free float $\left( {FF}\right)$ |
| --- | --- | --- | --- |
| $B\left( {1,3}\right)$ | 6 | ${11} - 0 - 6 = 5$ | $8 - 0 - 6 = 2$ |
| $C\left( {2,3}\right)$ | 3 | ${11} - 5 - 3 = 3$ | $8 - 5 - 3 = 0$ |
| $E\left( {3,5}\right)$ | 2 | ${13} - 8 - 2 = 3$ | ${13} - 8 - 2 = 3$ |
| $F\left( {3,6}\right)$ | 11 | ${25} - 8 - {11} = 6$ | ${25} - 8 - {11} = 6$ |
| $G\left( {4,6}\right)$ | 1 | ${25} - {13} - 1 = {11}$ | ${25} - {13} - 1 = {11}$ |

The computations red-flag activities $B$ and $C$ because their ${FF} < {TF}$ . The remaining activities $\left( {E, F\text{ , and }G}\right)$ have ${FF} = {TF}$ and hence can be scheduled anywhere between their earliest start and latest completion times.

To investigate the significance of red-flagged activities, consider activity $B$ , with ${TF} = 5$ days and ${FF} = 2$ days. This activity can start any time between 0 and 2 (its FF). On the other hand, starting $B$ past time 2 up to time 5 (its ${TF}$ ), the start times of the immediately succeeding activities $E$ and $F$ must be pushed forward relative to their earliest start time $\left( { = 8}\right)$ by at least an equal delay period.

As for red-flagged activity $C$ , its zero ${FF}$ means that any delay in starting $C$ past its earliest start time $\left( { = 5}\right)$ must be coupled with at least an equal delay in the start time of its successor activities $E$ and $F$ .

## TORA Moment

TORA provides useful tutorial tools for CPM calculations and for constructing the time schedule. To use these tools, select Project Planning ⇒ CPM - Critical Path Method from Main Menu. In the output screen, you have the option to select CPM Calculations to produce step-by-step computations of the forward pass, backward pass, and the floats or CPM Bar Chart to construct and experiment with the time schedule.

File toraEx6.5-2.txt provides TORA's data for Example 6.5-2. If you elect to generate the output using the Next Step option, TORA will guide you through the details of the forward and backward pass calculations.

Figure 6.31 provides TORA schedule produced by CPM Bar Chart option for the project of Example 6.5-2. The default bar chart automatically schedules all noncritical activities as early as possible. You can study the impact of delaying the start time of a noncritical activity by using the self-explanatory drop-down lists on the left of the screen. The impact of a delay of a noncritical activity will be shown directly on the bar chart together with an explanation. For example, if you delay the start of activity $B$ by more than 2 time units, the succeeding activities $E$ and $F$ will be delayed by an amount equal to the difference between the delay and free float of activity $B$ . Specifically, given that the free float for $B$ is 2 time units, if $B$ is delayed by 3 time units, then the start of $E$ and $F$ must be delayed by at least $3 - 2 = 1$ time unit. This situation is demonstrated in Figure 6.31.

![bo_d56m3tv7aajc73800n00_35_286_200_1300_760_0.jpg](bo_d56m3tv7aajc73800n00_35_286_200_1300_760_0.jpg)

FIGURE 6.31

TORA bar chart output for Example 6.5-2 (file toraEx6.5-2.txt)

## AMPL Moment

File amplEx6.52.txt provides the AMPL model for the CPM. The model is driven by the data of Example 6.5-2. This AMPL model is a unique application because it is not an optimization problem. The details of the model are given in Appendix C.9 on the website.

#### 6.5.4 Linear Programming Formulation of CPM ^cpmlp

The CPM model seeks the longest path between the start and finish nodes of the project network. Its formulation as an LP is thus similar to the LP of the shortest-route model (Section 6.3.3). The only difference is that the objective function is maximized instead of minimized.

Define

${x}_{ij} =$ Amount of flow in activity $\left( {i, j}\right)$ , for all defined $i$ and $j \; {D}_{ij} =$ Duration of activity $\left( {i, j}\right)$ , for all defined $i$ and $j$

Thus, the objective function of the linear program becomes

$$
\text{ Maximize }z = \mathop{\sum }\limits_{\substack{\text{ all defined } \\  \text{ activities }\left( {i, j}\right)  }}{D}_{ij}{x}_{ij}
$$

For each node, there is one constraint that represents the conservation of flow:

$$
\text{ Total input flow } = \text{ Total output flow }
$$

All the variables, ${x}_{ij}$ , are nonnegative.

## Example 6.5-5

The LP formulation of the project of Example 6.5-2 (Figure 6.28) is given hereafter. Note that nodes 1 and 6 are the start and finish nodes, respectively.

|  | $A$<br>${x}_{12}$ | $B$<br>${x}_{13}$ | $C$<br>${x}_{23}$ | $D$<br>${x}_{24}$ | $E$<br>${x}_{35}$ | $F$<br>${x}_{36}$ | Dummy<br>${x}_{45}$ | $G$<br>${x}_{46}$ | $H$<br>${x}_{56}$ | RHS |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Maximize $z =$ | 6 | 6 | 3 | 8 | 2 | 11 | 0 | 1 | 12 |  |
| Node 1 | -1 | -1 |  |  |  |  |  |  |  | $= -1$ |
| Node 2 | 1 |  | -1 | -1 |  |  |  |  |  | $= 0$ |
| Node 3 |  | 1 | 1 |  | -1 | -1 |  |  |  | $= 0$ |
| Node 4 |  |  |  | 1 |  |  | -1 | -1 |  | $= 0$ |
| Node 5 |  |  |  |  | 1 |  | 1 |  | -1 | $= 0$ |
| Node 6 |  |  |  |  |  | 1 |  | 1 | 1 | $= 1$ |

The optimum solution is $z = {25},{x}_{12}\left( A\right)  = 1,{x}_{24}\left( D\right)  = 1,{x}_{45}\left( \text{ Dummy }\right)  = 1,{x}_{56}\left( H\right)  = 1$ , and all others $= 0$ . The solution defines the critical path as $A \rightarrow  D \rightarrow$ Dummy $\rightarrow  H$ , and the project duration is 25 days, but it does not provide the data needed to construct the CPM chart.

#### 6.5.5 PERT Networks ^pert

PERT differs from CPM in that it assumes probabilistic duration times based on three estimates:

1. Optimistic time, $a$ , which occurs when execution goes extremely well.

2. Most likely time, $m$ , which occurs when execution is done under normal conditions.

3. Pessimistic time, $b$ , which occurs when execution goes extremely poorly.

The most likely time, $m$ , falls in the range $\left( {a, b}\right)$ .

Based on the estimates, the average duration time, $\bar{D}$ , and variance, $v$ , are approximated as

$$
\bar{D} = \frac{a + {4m} + b}{6}
$$

$$
v = {\left( \frac{b - a}{6}\right) }^{2}
$$

CPM calculations given in Sections 6.5.2 and 6.5.3 may be applied directly, with $\bar{D}$ replacing the single estimate $D$ .

Given the random variable ${e}_{j}$ representing the earliest occurrence time of node, the probability that $j$ will occur by a scheduled time, ${S}_{j}$ , can be estimated in the following manner: Assume that all the activities in the network are statistically independent, first compute the mean, $E\left\{  {e}_{j}\right\}$ , and variance, $\operatorname{var}\left\{  {e}_{j}\right\}$ . If there is only one path from the start node to node $j$ , then the mean is the sum of expected durations, $\bar{D}$ , for all the activities along this path and the variance is the sum of the variances, $v$ , of the same activities. If more than one path leads to node $j$ , then it is necessary to determine the statistical distribution of the duration of the longest path, a rather difficult problem because it involves determining the distribution of the maximum of at least two random variables. A simplifying assumption calls for selecting the path to node $j$ having the longest average duration. If two or more paths have the same mean, the one with the largest variance is selected because it reflects the most uncertainty and, hence, leads to more conservative estimate of probabilities.

Given the mean and variance of the path to node $j, E\left\{  {e}_{j}\right\}$ and $\operatorname{var}\left\{  {e}_{j}\right\}$ , the probability that node $j$ occurs by time ${S}_{j}$ is approximated by the standard normal distribution, $z$ (see Section 14.4.4) - that is,

$$
P\left\{  {{e}_{j} \leq  {S}_{j}}\right\}   = P\left\{  {\frac{{e}_{j} - E\left\{  {e}_{j}\right\}  }{\sqrt{\operatorname{var}\left\{  {e}_{j}\right\}  }} \leq  \frac{{S}_{j} - E\left\{  {e}_{j}\right\}  }{\sqrt{\operatorname{var}\left\{  {e}_{j}\right\}  }}}\right\}   = P\left\{  {z \leq  {K}_{j}}\right\}
$$

Justification for the use of the normal distribution is that ${e}_{j}$ is the sum of independent random variables. According to the central limit theorem (see Section 14.4.4), ${e}_{j}$ is approximately normally distributed.

## Example 6.5-6

Consider the project of Example 6.5-2. To avoid repeating the critical path calculations, the values of $a, m$ , and $b$ in the following table are selected to yield $\overline{{D}_{ij}} = {D}_{ij}$ for all $i$ and $j$ in Example 6.5-2:

| Activity | $i - j$ | $\left( {a, m, b}\right)$ | Activity | $i - j$ | $\left( {a, m, b}\right)$ |
| --- | --- | --- | --- | --- | --- |
| $A$ | 1-2 | (3,5,7) | $E$ | 3-5 | $\left( {1,2,3}\right)$ |
| $B$ | 1-3 | (4,6,8) | $F$ | 3-6 | (9,11,13) |
| $C$ | 2-3 | (1,3,5) | $G$ | 4-6 | (1,1,1) |
| $D$ | 2-4 | (5,8,11) | $H$ | 5-6 | (10,12,14) |

The mean $\overline{{D}_{ij}}$ and variance ${v}_{ij}$ for the different activities are given in the following table. Note that a dummy activity with $\left( {a, m, b}\right)  = \left( {0,0,0}\right)$ has zero mean and variance.

| Activity | $i - j$ | $\overline{{D}_{ij}}$ | ${v}_{ij}$ | Activity | $i - j$ | $\overline{{D}_{ij}}$ | ${v}_{ij}$ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| $A$ | 1-2 | 5 | .444 | $E$ | 3-5 | 2 | .111 |
| $B$ | 1-3 | 6 | .444 | $F$ | 3-6 | 11 | .444 |
| $C$ | 2-3 | 3 | .444 | $G$ | 4-6 | 1 | .000 |
| $D$ | 2-4 | 8 | 1.000 | $H$ | 5-6 | 12 | .444 |

The next table gives the longest path from node 1 to the different nodes, together with their associated mean and standard deviation.

| Node | Longest path based on mean durations | Path mean | Path standard deviation |
| --- | --- | --- | --- |
| 2 | 1-2 | 5.00 | 0.67 |
| 3 | 1-2-3 | 8.00 | 0.94 |
| 4 | 1-2-4 | 13.00 | 1.20 |
| 5 | 1-2-4-5 | 13.00 | 1.20 |
| 6 | 1-2-4-5-6 | 25.00 | 1.37 |

The following table computes the probability that each node is realized by time ${S}_{j}$ (specified by the analyst):

| Node $j$ | Longest path | Path mean | Path standard deviation | ${S}_{j}$ | ${K}_{j}$ | $P\left\{  {z \leq  {K}_{j}}\right\}$ |
| --- | --- | --- | --- | --- | --- | --- |
| 2 | 1-2 | 5.00 | 0.67 | 5.00 | 0 | .5000 |
| 3 | 1-2-3 | 8.00 | 0.94 | 11.00 | 3.19 | .9993 |
| 4 | 1-2-4 | 13.00 | 1.20 | 12.00 | -.83 | .2033 |
| 5 | 1-2-4-5 | 13.00 | 1.20 | 14.00 | .83 | .7967 |
| 6 | 1-2-4-5-6 | 25.00 | 1.37 | 26.00 | .73 | .7673 |

## TORA Moment

TORA provides a module for carrying out PERT calculations. To use this module, select Project Planning $\Rightarrow$ PERT-Program Evaluation and Review Technique from Main Menu . In the output screen, you have the option to select Activity Mean/Var to compute the mean and variance for each activity or PERT Calculations to compute the mean and variance of the longest path to each node in the network. File toraEx6.5-6.txt provides TORA's data for Example 6.5-6.

## BIBLIOGRAPHY

Ahuja, R., T. Magnati, and J. Orlin, Network Flows: Theory, Algorithms, and Applications, Prentice Hall, Upper Saddle River, NJ, 1993.

Bazaraa, M., J. Jarvis, and H. Sherali, Linear Programming and Network Flow, 4th ed., Wiley, New York, 2009.

Charnes, A., and W. Cooper, "Some Network Characterization for Mathematical Programming and Accounting Applications to Planning and Control," The Accounting Review, Vol. 42, No. 3, pp. 24-52, 1967.

Evans, J., and E. Minieka, Optimization Algorithms for Networks and Graphs, 2nd ed., Marcel Dekker, New York, 1992.

Guéret, C., C. Prins, and M. Sevaux, Applications of Optimization with Xpress-MP, translated and revised by Susanne Heipke, Dash Optimization Ltd., London, 2002.

Glover, F., D. Klingman, and N. Phillips, Network Models and Their Applications in Practice, Wiley, New York, 1992.

Robinson, E., L. Gao, and S. Muggenborg, "Designing an Integrated Distribution System at Dow-Brands, Inc," Interfaces, Vol. 23, No. 3, pp. 107-117, 1993.

## Case Study: Saving Federal Travel Dollars4 ^casestudy

Tools: Shortest-route algorithm

## Area of application: Business travel

## Description of the situation:

U.S. federal government employees are required to attend development conferences and training courses. Currently, the selection of the city hosting conferences and training events is done without consideration of incurred travel cost. Because federal employees are located in offices scattered around the United States, the location of the host city can impact travel cost, depending on the number of participants and the locations from which they originate.

The General Services Administration (GSA) issues a yearly schedule of airfares that the government contracts with different U.S. air carriers. This schedule provides fares for approximately 5000 city-pair combinations in the contiguous 48 states. It also issues per-diem rates for all major cities and a flat daily rate for cities not included in the list. Participants using personal vehicles for travel receive a flat rate per mile. All rates are updated annually to reflect the cost-of-living increase. The travel cost from a location to the host city is a direct function of the number of participants, the cost of travel to the host city, and the per-diem allowed for the host city.

The problem is concerned with the optimal location of host city for an event, given a specified number of applicants from participating locations around the country.

## Analysis

The idea of the solution is simple: The host city must yield the lowest travel cost that includes transportation and per-diem allowance for the host city. The determination of the transportation cost requires identifying the locations from which participants depart. It is reasonable to assume that for locations within 100 miles from the host city, participants use personal vehicles as the selected mode of transportation. Others travel by air. The cost basis for air travelers consists of the sum of contracted airfares along the legs of the cheapest route to the host city. To determine such routes, it is necessary to identify the locations around the United States from which participants depart. Each such location is a possible host city candidate provided it offers adequate airport and conference facilities. In the present case, 261 such locations with 4640 contracted airport links are identified.

The determination of the cheapest airfare routes among the selected 261 locations with 4640 air links is no simple task because a trip may involve multiple legs. Floyd's algorithm (Section 6.3.2) is ideal for determining such routes. The "distance" between two locations is represented by the contracted airfare provided by the government. Per the contract, round trip cost is double the cost of the one-way trip. ^travelmethod

To simplify the analysis, the study does not allow the use of car rentals at destinations. The plausible assumption here is that the host hotel is in the vicinity of the airport, usually with free shuttle service.

Per-diems cover lodging, meals, and incidental expenses. Participants arrive the day before the event starts. However, those arriving from locations within 100 miles arrive the morning of the first day of the event. All participants will check out of the hotel on the last day. For the days of arrival and departure, government regulations for meals and incidental expenses allow only a 75% reimbursement of the full per-diem rate. ^travelassumptions

---

${}^{4}$ J. L. Huisingh, H. M. Yamauchi, and R. Zimmerman,"Saving Federal Travel Dollars," Interfaces, Vol. 31, No. 5, pp. 13-23, 2001.

---

## Numerical Example ^numerical

For the sake of this illustration, we will assume a 12-host-city situation. Table 6.1 provides the (late 1990s) contracted one-way airfares for admissible links among the cities. A blank entry indicates that the associated city pair does not have a direct air link.

Maximum lodging and per-diem allowances for the 12 cities together with their associated number of participants for an upcoming event are listed in Table 6.2. The duration of the event is 4 days. The standard mileage allowance for personal vehicles is \$.325 per mile (per the year 2000).

TABLE 6.1 One-Way Airfare for the 12-City Example

|  | SF | ORD | STL | LAX | TUL | DEN | DC | ATL | DAL | NY | MIA | SPI |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SF |  |  |  | \$70 |  | \$120 |  |  | \$220 |  |  |  |
| ORD |  |  | \$99 |  |  | \$140 | \$150 |  |  |  |  |  |
| STL |  | \$99 |  |  | \$95 | \$110 |  |  |  |  |  | \$78(a) |
| LAX | \$70 |  |  |  |  | \$130 |  |  |  |  |  |  |
| TUL |  |  | \$95 |  |  | \$105 |  |  | \$100 |  |  |  |
| DEN | \$120 | \$140 | \$110 | \$130 | \$105 |  |  |  |  |  |  |  |
| DC |  | \$150 |  |  |  |  |  | \$100 | \$195 | \$85 |  |  |
| ATL |  |  |  |  |  |  | \$100 |  |  |  | \$125 |  |
| DAL | \$220 |  |  |  | \$100 |  | \$195 |  |  |  |  |  |
| NY |  |  |  |  |  |  | \$85 |  |  |  | \$130 |  |
| MIA |  |  |  |  |  |  |  | \$125 |  | \$130 |  |  |
| SPI |  |  | \$78(a) |  |  |  |  |  |  |  |  |  |

(a) Air travel cost $= \$ {78}$ . Distance $< {100}$ miles $\left( { = {86}\text{ miles }}\right)$ . Personal car used for travel between STL and SPI.

TABLE 6.2 Lodging Cost, Per Diem, and Number of Participants in the 12-City Example

| City | Lodging per night (\$) | Per-diem (\$) | Number of participants |
| --- | --- | --- | --- |
| SF | 115.00 | 50.00 | 15 |
| ORD | 115.00 | 50.00 | 10 |
| STL | 85.00 | 48.00 | 8 |
| LAX | 120.00 | 55.00 | 18 |
| TUL | 70.00 | 35.00 | 5 |
| DEN | 90.00 | 40.00 | 9 |
| DC | 150.00 | 60.00 | 10 |
| ATL | 90.00 | 50.00 | 12 |
| DAL | 90.00 | 50.00 | 11 |
| NY | 190.00 | 60.00 | 12 |
| MIA | 120.00 | 50.00 | 8 |
| SPI | 60.00 | 35.00 | 2 |

TABLE 6.3 Cheapest Airfare in the 12-City Example

|  | ORD | STL | LAX | TUL | DEN | DC | ATL | DAL | NY | MIA | SPI |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SF | \$260 | \$230 | \$70 | \$225 | \$120 | \$410 | \$510 | \$220 | \$495 | \$625 | \$308 |
| ORD |  | \$99 | \$270 | \$194 | \$140 | \$150 | \$250 | \$294 | \$235 | \$365 | \$177 |
| STL |  |  | \$240 | \$95 | \$110 | \$249 | \$349 | \$195 | \$334 | \$464 | \$28* |
| LAX |  |  |  | \$235 | \$130 | \$420 | \$520 | \$290 | \$505 | \$635 | \$318 |
| TUL |  |  |  |  | \$105 | \$295 | \$395 | \$100 | \$380 | \$510 | \$173 |
| DEN |  |  |  |  |  | \$290 | \$390 | \$205 | \$375 | \$505 | \$188 |
| DC |  |  |  |  |  |  | \$100 | \$195 | \$85 | \$215 | \$327 |
| ATL |  |  |  |  |  |  |  | \$295 | \$185 | \$125 | \$427 |
| DAL |  |  |  |  |  |  |  |  | \$280 | \$410 | \$273 |
| NY |  |  |  |  |  |  |  |  |  | \$130 | \$412 |
| MIA |  |  |  |  |  |  |  |  |  |  | \$542 |

*Personal vehicle cost based on 86 miles (32.5 cents per mile)

The first step in the solution is to determine the cheapest airfare among all city pairs. This step is carried out by TORA (input file toraCase4.txt) using Floyd's shortest-route algorithm (Section 6.3.2). The results are summarized in Table 6.3. Blank entries symmetrically equal those above the main diagonal. Recall that these values represent the cost of one-way tickets and that the cost of round-trip tickets is double that amount. Floyd's algorithm automatically specifies the trip legs associated with each city pair.

The final step in the solution is to determine the total cost of the event for all the participants, given that the event is held at one of the listed cities. The city providing the smallest total cost is then selected as the host city.

To demonstrate the computations, suppose that STL is the candidate host city. The associated total cost is then computed as:

$$
\text{ Travel cost } = 2 \times  \left( {{15} \times  {230} + {10} \times  {99} + {18} \times  {240} + 5 \times  {95} + 9 \times  {110} + {10} \times  {249}}\right.
$$

$$
+ {12} \times  {349} + {11} \times  {195} + {12} \times  {334} + 8 \times  {464}) + 2 \times  \left( {2 \times  {86}}\right)  \times  {.325}
$$

$$
= \$ {53},{647.80}
$$

$$
\text{ Lodging cost } = \$ {85} \times  \left\lbrack  {\left( {{15} + {10} + {18} + 5 + 9 + {10} + {12} + {11} + {12} + 8}\right)  \times  4 + 2 \times  3}\right\rbrack
$$

$$
= \$ {37},{910}
$$

Per-diem cost $= \$ {48} \times  \lbrack \left( {{15} + {10} + {18} + 5 + 9 + {10} + {12} + {11} + {12} + 8}\right)$

$$
\times  {4.5} + \left( {2 + 8}\right)  \times  {3.5}\rbrack
$$

$$
= \$ {25},{440}
$$

Note that because SPI is located 86 miles ( $< {100}$ miles) from STL, its participants drive personal vehicles and arrive at STL the morning of the first day of the event. Thus, their per-diem is based on ${3}^{1}/2$ days and their lodging is based on 3 nights only. Participants from STL receive per diem for ${3}^{1}/2$ days and no lodging. All other participants arrive at STL a day earlier, and their per-diem is based on ${4}^{1}/2$ days and 4 nights of lodging.

The computations for all host cities can be done conveniently with a spreadsheet (file excelCase4.xls-all the formulas are appended as cell comments). The results show that TUL offers the lowest total cost (\$108,365), followed by DEN (\$111,332) and then STL (\$115,750). ^besthost

| Section | Assigned Problems | Section | Assigned Problems |
| --- | --- | --- | --- |
| 6.1 | 6-1 to 6-6 | 6.4.3 | 6-39 to 6-41 |
| 6.2 | 6-7 to 6-12 | 6.5.1 | 6-42 to 6-51 |
| 6.3.1 | 6-13 to 6-17 | 6.5.2 | 6-52 to 6-57 |
| 6.3.2 | 6-18 to 6-24 | 6.5.3 | 6-58 to 6-64 |
| 6.3.3 | 6-25 to 6-27 | 6.5.4 | 6-65 to 6-66 |
| 6.4.1 | 6-28 to 6-28 | 6.5.5 | 6-67 to 6-67 |
| 6.4.2 | 6-29 to 6-38 |  |  |

*6-1. For each network in Figure 6.32, determine (a) a path, (b) a cycle, (c) a tree, and (d) a spanning tree.

6-2. Determine the sets $N$ and $A$ for the networks in Figure 6.32.

6-3. Draw the network defined by

$$
N = \{ 1,2,3,4,5\}
$$

$$
A = \{ \left( {1,2}\right) ,\left( {1,5}\right) ,\left( {2,3}\right) ,\left( {2,4}\right) ,\left( {3,4}\right) ,\left( {3,5}\right) ,\left( {4,3}\right) ,\left( {4,5}\right) ,\left( {5,2}\right) \}
$$

6-4. In Example 6.1-1,

(a) Specify the smallest number and locations of additional bridges needed to construct (i) a round-trip starting from $A$ , and (ii) a trip that starts from $A$ and ends in $C$ . Construct the resulting network, and determine the legs of the trip.

(b) During World War II, two of the bridges were destroyed. With the remaining five bridges, it became possible to make a trip from $A$ to $C$ (crossing each bridge exactly once). Which two bridges were destroyed (not fair consulting the Internet!)?

*6-5. Consider eight equal squares arranged in three rows, with two squares in the first row, four in the second, and two in the third. The squares of each row are arranged symmetrically about the vertical axis. Fill the squares with distinct numbers in the range 1 to 8 so that no two adjacent vertical, horizontal, or diagonal squares hold consecutive numbers. Use a network representation to find the solution in a systematic way.

6-6. Three inmates escorted by three guards must be transported by boat from the mainland to a penitentiary island to serve their sentences. The boat cannot transfer more than two persons in either direction. The inmates are certain to overpower the guards if they outnumber them anywhere at any time. Develop a network model that designs the boat trips in a manner that ensures a safe transfer of the inmates.

FIGURE 6.32

Networks for Problems 6-1 and 6-2

![bo_d56m3tv7aajc73800n00_42_541_1715_878_455_0.jpg](bo_d56m3tv7aajc73800n00_42_541_1715_878_455_0.jpg)

6-7. Solve Example 6.2-1 starting at node 6 (instead of node 1), and show that the algorithm produces the same solution.

6-8. Determine the minimal spanning tree of the network of Example 6.2-1 under each of the following separate conditions:

*(a) Nodes 5 and 6 are linked by a 2-mile cable.

(b) Nodes 2 and 5 cannot be linked.

(c) Nodes 2 and 6 are linked by a 4-mile cable.

(d) The cable between nodes 1 and 2 is 8 miles long.

(e) Nodes 3 and 5 are linked by a 2-mile cable.

(f) Node 2 cannot be linked directly to nodes 3 and 5.

6-9. In intermodal transportation, loaded truck trailers are shipped between railroad terminals on special flatbed carts. Figure 6.33 shows the location of the main railroad terminals in the United States and the existing railroad tracks. The objective is to decide which tracks should be "revitalized" to handle the intermodal traffic. In particular, the Los Angeles (LA) terminal must be linked directly to Chicago (CH) to accommodate expected heavy traffic. Other than that, all the remaining terminals can be linked, directly or indirectly, such that the total length (in miles) of the selected tracks is minimized. Determine the segments of the railroad tracks that must be included in the revitalization program.

6-10. Figure 6.34 gives the mileage of the feasible links connecting nine offshore natural gas wellheads with an inshore delivery point. Because wellhead 1 is the closest to shore, it is equipped with sufficient pumping and storage capacity to pump the output of the remaining eight wells to the delivery point. Determine the minimum pipeline network that links the wellheads to the delivery point.

*6-11. In Figure 6.34 of Problem 6-10, suppose that the wellheads can be divided into two groups depending on gas pressure: a high-pressure group that includes wells 2, 3, 4, and 7, and a low-pressure group that includes wells 5, 6, 8, and 9. Because of pressure difference, it is not possible to link the wellheads from the two groups. At the same time, both groups must be connected to the delivery point through wellhead 1. Determine the minimum pipeline network for this situation.

FIGURE 6.33

Network for Problem 6-9

![bo_d56m3tv7aajc73800n00_43_500_1628_875_556_0.jpg](bo_d56m3tv7aajc73800n00_43_500_1628_875_556_0.jpg)

![bo_d56m3tv7aajc73800n00_44_447_197_590_650_0.jpg](bo_d56m3tv7aajc73800n00_44_447_197_590_650_0.jpg)

FIGURE 6.34

Network for Problem 6-10 and 6-11

6-12. Electro produces 15 electronic parts on 10 machines. The company wants to group the machines into cells designed to minimize the "dissimilarities" among the parts processed in each cell. A measure of "dissimilarity," ${d}_{ij}$ , among the parts processed on machines $i$ and $j$ can be expressed as

$$
{d}_{ij} = 1 - \frac{{n}_{ij}}{{n}_{ij} + {m}_{ij}}
$$

where ${n}_{ij}$ is the number of parts shared between machines $i$ and $j$ , and ${m}_{ij}$ is the number of parts that are used by either machine $i$ or machine $j$ only.

The following table assigns the parts to machines:

| Machine | Assigned parts |
| --- | --- |
| 1 | 1,6 |
| 2 | 2,3,7,8,9,12,13,15 |
| 3 | 3, 5, 10, 14 |
| 4 | 2,7,8,11,12,13 |
| 5 | 3, 5, 10, 11, 14 |
| 6 | 1, 4, 5, 9, 10 |
| 7 | 2,5,7,8,9,10 |
| 8 | 3, 4, 15 |
| 9 | 4,10 |
| 10 | 3,8,10,14,15 |

(a) Express the problem as a network model.

(b) Show that the determination of the cells can be based on the minimal spanning tree solution.

(c) For the data given in the preceding table, construct the two- and three-cell solutions.

*6-13. Reconstruct the equipment replacement model of Example 6.3-1, assuming that a car must be kept in service for at least 2 years, with a maximum service life of 4 years. The planning horizon is from the start of year 1 to the end of year 5 . The following table provides the necessary data.

| Year acquired | 2 years | 3 years | 4 years |
| --- | --- | --- | --- |
| 1 | 3800 | 4100 | 6900 |
| 2 | 4100 | 4890 | 7200 |
| 3 | 4200 | 5300 | 7300 |
| 4 | 4800 | 5800 | - |
| 5 | 5400 | - | - |

6-14. Figure 6.35 provides the communication network between two stations, 1 and 7. The probability that a link in the network will operate without failure is shown on each arc. Messages are sent from station 1 to station 7, and the objective is to determine the route that maximizes the probability of a successful transmission. Formulate the situation as a shortest-route model, and determine the optimum solution.

6-15. Production Planning. DirectCo sells an item whose demands over the next 4 months are100,140,210, and 180 units, respectively. The company can stock just enough supply to meet each month's demand, or it can overstock to meet the demand for two or more consecutive months. In the latter case, a holding cost of \$1.20 is charged per overstocked unit per month. DirectCo estimates the unit purchase prices for the next 4 months to be $\$ {15},\$ {12},\$ {10}$ , and $\$ {14}$ , respectively. A setup cost of $\$ {200}$ is incurred each time a purchase order is placed. The company wants to develop a purchasing plan that will minimize the total costs of ordering, purchasing, and holding the item in stock. Formulate the problem as a shortest-route model, and use TORA to find the optimum solution.

*6-16. Knapsack Problem. A hiker has a 5-ft ${}^{3}$ backpack and needs to decide on the most valuable items to take on the hiking trip. There are three items from which to choose. Their volumes are 2,3, and $4{\mathrm{{ft}}}^{3}$ , and the hiker estimates their associated values on a scale from 0 to 100 as 30, 50, and 70, respectively. Express the problem as longest-route network, and find the optimal solution. (Hint: A node in the network may be defined as $\left\lbrack  {i, v}\right\rbrack$ , where $i$ is the item number considered for packing, and $v$ is the volume remaining immediately before a decision is made on $i$ . To solve with TORA, convert the longest-route to a shortest-route problem by using negative arc length.)

FIGURE 6.35

Network for Problem 6-14

![bo_d56m3tv7aajc73800n00_45_478_1662_918_511_0.jpg](bo_d56m3tv7aajc73800n00_45_478_1662_918_511_0.jpg)

6-17. An old-fashioned electric toaster has two spring-loaded base-hinged doors. The two doors open outward in opposite directions away from the heating element. A slice of bread is toasted one side at a time by pushing open one of the doors with one hand and placing the slice with the other hand. After one side is toasted, the slice is turned over to get the other side toasted. The goal is to determine the sequence of operations (placing, toasting, turning, and removing) needed to toast three slices of bread in the shortest possible time. Formulate the problem as a shortest-route model, using the following elemental times for the different operations:

| Operation | Time (seconds) |
| --- | --- |
| Place one slice in either side | 3 |
| Toast one side | 30 |
| Turn slice already in toaster | 1 |
| Remove slice from either side | 3 |

6-18. The network in Figure 6.36 gives the distances in miles between pairs of cities 1, 2, ..., and 8. Use Dijkstra's algorithm to find the shortest route between the following cities:

(a) Cities 1 and 7.

(b) Cities 1 and 6.

*(c) Cities 4 and 8.

(d) Cities 2 and 7.

6-19. Use Dijkstra's algorithm to find the shortest route between node 1 and every other node in the network of Figure 6.37.

![bo_d56m3tv7aajc73800n00_46_343_1341_1284_832_0.jpg](bo_d56m3tv7aajc73800n00_46_343_1341_1284_832_0.jpg)

6-20. Use Dijkstra's algorithm to determine the optimal solution of each of the following problems:

(a) Problem 6-13.

(b) Problem 6-14.

(c) Problem 6-16.

6-21. In Example 6.3-5, use Floyd's algorithm to determine the shortest routes between each of the following pairs of nodes:

*(a) From node 5 to node 1.

(b) From node 3 to node 5.

(c) From node 1 to node 4.

(d) From node 3 to node 2.

6-22. Apply Floyd's algorithm to the network in Figure 6.38. Arcs (7, 6) and (6, 4) are unidirectional, and all the distances are in miles. Determine the shortest route between the following pairs of nodes:

(a) From node 1 to node 7.

(b) From node 7 to node 1.

(c) From node 6 to node 7.

6-23. The Tell-All mobile-phone company services six geographical areas. The satellite distances (in miles) among the six areas are given in Figure 6.39. Tell-All needs to determine the most efficient message routes that should be established between each two areas in the network.

*6-24. Six kids, Joe, Kay, Jim, Bob, Rae, and Kim, play a variation of hide and seek. The hiding place of a child is known only to a select few of the other children. A child is then paired with another with the objective of finding the partner's hiding place. This may be achieved through a chain of other kids who eventually will lead to discovering where the designated child is hiding. For example, suppose that Joe needs to find Kim and that Joe knows where Jim is hiding, who in turn knows where Kim is. Thus, Joe can find Kim by first finding Jim, who in turn will lead Joe to Kim. The following list provides the whereabouts of the children:

![bo_d56m3tv7aajc73800n00_47_355_1353_1168_822_0.jpg](bo_d56m3tv7aajc73800n00_47_355_1353_1168_822_0.jpg)

Joe knows the hiding places of Bob and Kim.

Kay knows the hiding places of Bob, Jim, and Rae.

Jim and Bob each know the hiding place of Kay only.

Rae knows where Kim is hiding.

Kim knows where Joe and Bob are hiding.

Devise a plan for each child to find every other child using the smallest number of contacts. What is the largest number of contacts made by any child?

6-25. In Example 6.3-6, use LP to determine the shortest routes between the following pairs of nodes:

*(a) Node 1 to node 5.

(b) Node 2 to node 5.

6-26. Modify solverEx6.3-6.xls to find the shortest route between the following pairs of nodes:

(a) Node 1 to node 5.

(b) Node 1 to node 4.

6-27. Adapt amplEx6.3-6b.txt for Problem 6-14, to find the shortest route between node 1 and node 6. The input data must be the raw probabilities. Use AMPL programming facilities to print/display the optimum transmission route and its success probability.

*6-28. For the network in Figure 6.20, determine two additional cuts, and find their capacities.

*6-29. In Example 6.4-2,

(a) Determine the surplus capacities for all the arcs.

(b) Determine the amount of flow through nodes 2, 3, and 4.

(c) Can the network flow be increased by increasing the capacities in the directions $3 \rightarrow  5$ and $4 \rightarrow  5$ ?

6-30. Determine the maximal flow and the optimum flow in each arc for the network in Figure 6.40.

![bo_d56m3tv7aajc73800n00_48_478_1620_715_544_0.jpg](bo_d56m3tv7aajc73800n00_48_478_1620_715_544_0.jpg)

FIGURE 6.40

Network for Problem 6-30

6-31. Three refineries send a gasoline product to two distribution terminals through a pipeline network. Any demand that cannot be satisfied through the network is acquired from other sources. The pipeline network is served by three pumping stations, as shown in Figure 6.41. The product flows in the network in the direction shown by the arrows. The capacity of each pipe segment (shown directly on the arcs) is in million bbl per day. Determine the following:

(a) The daily production at each refinery that matches the maximum capacity of the network.

(b) The daily demand at each terminal that matches the maximum capacity of the network.

(c) The daily capacity of each pump that matches the maximum capacity of the network.

6-32. Suppose that the maximum daily capacity of pump 6 in the network of Figure 6.41 is limited to 50 million bbl per day. Remodel the network to include this restriction. Then determine the maximum capacity of the network.

6-33. Chicken feed is transported by trucks from three silos to four farms. Some of the silos cannot ship directly to some of the farms. The capacities of the other routes are limited by the number of trucks available and the number of trips made daily. The following table shows the daily amounts of supply at the silos and demand at the farms (in thousands of pounds). The cell entries of the table specify the daily capacities of the associated routes.

|  | Farm 1 | Farm 2 | Farm 3 | Farm 4 | Supply |
| --- | --- | --- | --- | --- | --- |
| Silo 1 | 30 | 5 | 0 | 40 | 20 |
| Silo 2 | 0 | 0 | 5 | 90 | 20 |
| Silo 3 | 100 | 40 | 30 | 40 | 200 |
| Demand | 200 | 10 | 60 | 20 |  |

(a) Determine the schedule that satisfies the most demand.

(b) Will the proposed schedule satisfy all the demand at the farms?

6-34. In Problem 6-33, suppose that transshipping is allowed between silos 1 and 2 and silos 2 and 3. Suppose also that transshipping is allowed between farms 1 and 2, 2 and 3, and 3 and 4. The maximum two-way daily capacity on the proposed transshipping routes is 50 (thousand) lb. What is the effect of transshipping on the unsatisfied demands at the farms?

![bo_d56m3tv7aajc73800n00_49_452_1628_696_559_0.jpg](bo_d56m3tv7aajc73800n00_49_452_1628_696_559_0.jpg)

FIGURE 6.41

Network for Problems 6-31 and 6-32

*6-35. A parent has five (teenage) children and five household chores to assign to them. Past experience has shown that forcing chores on a child is counterproductive. With this in mind, the children are asked to list their preferences among the five chores, as the following table shows:

| Child | Preferred chore |
| --- | --- |
| Rif | 1, 3, 4, or 5 |
| Mai | 1 |
| Ben | 1 or 2 |
| Kim | 1, 2, or 5 |
| Ken | 2,5 |

The parent's modest goal now is to finish as many chores as possible while abiding by the children's preferences. Determine the maximum number of chores that can be completed and the assignment of chores to children.

6-36. Four factories are engaged in the production of four types of toys. The following table lists the toys that can be produced by each factory.

| Factory | Toys productions mix |
| --- | --- |
| 1 | 1,2,3 |
| 2 | 2,3 |
| 3 | 1,3,4 |
| 4 | 1,3,4 |

All toys require approximately the same per-unit labor and material. The daily capacities of the four factories are250,180,300, and 200 toys, respectively. The daily demands for the four toys are 200, 150, 350, and 100 units, respectively. Determine the factories' production schedules that will most satisfy the demands for the four toys.

6-37. The academic council at the $\mathrm{U}$ of $\mathrm{A}$ is seeking representation from among six students who are affiliated with four honor societies. The academic council representation includes three areas: mathematics, art, and engineering. At most two students in each area can be on the council. The following table shows the membership of the six students in the four honor societies:

| Society | Affiliated students |
| --- | --- |
| 1 | 1, 2, 3, 4 |
| 2 | 1, 3, 6 |
| 3 | 2, 3, 4, 5 |
| 4 | 1, 2, 4, 6 |

The students who are skilled in the areas of mathematics, art, and engineering are shown in the following table:

| Area | Skilled students |
| --- | --- |
| Mathematics | 1, 2, 3, 4 |
| Art | 1,3,4,5 |
| Engineering | 1,4,5,6 |

A student who is skilled in more than one area must be assigned exclusively to one area only. Can all four honor societies be represented on the council?

6-38. Maximal/minimal flow in networks with lower bounds. The maximal flow algorithm given in this section assumes that all the arcs have zero lower bounds. In some models, the lower bounds may be strictly positive, and we may be interested in finding the maximal or minimal flow in the network (see case 6-3 in Appendix E). The presence of the lower bound poses difficulty because the network may not have a feasible flow at all. The objective of this exercise is to show that any maximal and minimal flow model with positive lower bounds can be solved using two steps.

Step 1. Find an initial feasible solution for the network with positive lower bounds.

Step 2. Using the feasible solution in step 1, find the maximal or minimal flow in the original network.

(a) Show that an arc $\left( {i, j}\right)$ with flow limited by ${l}_{ij} \leq  {x}_{ij} \leq  {u}_{ij}$ can be represented equivalently by a sink with demand ${l}_{ij}$ at node $i$ and a source with supply ${l}_{ij}$ at node $j$ with flow limited by $0 \leq  {x}_{ij} \leq  {u}_{ij} - {l}_{ij}$ .

(b) Show that finding a feasible solution for the original network is equivalent to finding the maximal flow ${x}_{ij}^{\prime }$ in the network after (1) modifying the bounds on ${x}_{ij}$ to $0 \leq  {x}_{ij}^{\prime } \leq  {u}_{ij} - {l}_{ij}$ ,(2) "lumping" all the resulting sources into one supersource with outgoing arc capacities ${l}_{ij}$ ,(3) "lumping" all the resulting sinks into one supersink with incoming arc capacities ${l}_{ij}$ , and (4) connecting the terminal node $t$ to the source node $s$ in the original network by a return infinite-capacity arc. A feasible solution exists if the maximal flow in the new network equals the sum of the lower bounds in the original network. Apply the procedure to the following network and find a feasible flow solution:

| Arc $\left( {i, j}\right)$ | $\left( {{l}_{ij},{u}_{ij}}\right)$ |
| --- | --- |
| (1,2) | (5,20) |
| (1,3) | (0,15) |
| (2,3) | (4,10) |
| (2,4) | (3,15) |
| (3,4) | (0,20) |

(c) Use the feasible solution for the network in (b) together with the maximal flow algorithm to determine the minimal flow in the original network. (Hint: First, compute the residue network given the initial feasible solution. Next, determine the maximum flow from the end node to the start node. This is equivalent to finding the maximum flow that should be canceled from the start node to the end node. Now, combining the feasible and maximal flow solutions yields the minimal flow in the original network.)

(d) Use the feasible solution for the network in (b) together with the maximal flow model to determine the maximal flow in the original network. (Hint: As in part (c), start with the residue network. Next, apply the breakthrough algorithm to the resulting residue network exactly as in the regular maximal flow model.)

6-39. Model each of the following problems as a linear program, then solve using Solver or AMPL.

(a) Problem 6-32.

(b) Problem 6-35.

(c) Problem 6-39.

6-40. Jim lives in Denver, Colorado, and likes to spend his annual vacation in Yellowstone National Park in Wyoming. Being a nature lover, Jim tries to drive a different scenic route each year. After consulting the appropriate maps, Jim has represented his preferred routes between Denver (D) and Yellowstone (Y) by the network in Figure 6.42. Nodes 1 through 14 represent intermediate cities. Although driving distance is not an issue, Jim's stipulation is that selected routes between D and Y do not include any common cities. Determine (using AMPL or Solver) all the distinct routes available to Jim. (Hint: Modify the maximal flow LP model to determine the maximum number of unique paths between $D$ and $Y$ .)

6-41. Guéret and Associate (2002), Section 12.1. A military telecommunication system connecting 9 sites is given in Figure 6.43. Sites 4 and 7 must continue to communicate even if as many as three other sites are destroyed by enemy actions. Does the present communication network meet this requirement? Use AMPL and Solver to work out the problem.

FIGURE 6.42

Network for Problem 6-40

![bo_d56m3tv7aajc73800n00_52_363_949_1227_599_0.jpg](bo_d56m3tv7aajc73800n00_52_363_949_1227_599_0.jpg)

FIGURE 6.43

Network for Problem 6-41

![bo_d56m3tv7aajc73800n00_52_510_1729_944_444_0.jpg](bo_d56m3tv7aajc73800n00_52_510_1729_944_444_0.jpg)

6-42. Construct the project network comprised of activities $A$ to $M$ with the following precedence relationships:

(a) $A, B$ , and $C$ , the first activities of the project, can be executed concurrently.

(b) $A$ and $B$ precede $D$ .

(c) $B$ precedes $E, F$ , and $H$ .

(d) $F$ and $C$ precede $G$ and $M$ .

(e) $E$ and $H$ precede $I$ and $J$ .

(f) $C, D, F$ , and $J$ precede $K$ .

(g) $K$ and $M$ precedes $L$ .

(h) $I, G$ , and $L$ are the terminal activities of the project.

6-43. Construct the project network comprised of activities $A$ to $P$ that satisfies the following precedence relationships:

(a) $A, B$ , and $C$ , the first activities of the project, can be executed concurrently.

(b) $D, E$ , and $F$ follow $A$ .

(c) $I$ and $G$ follow both $B$ and $D$ .

(d) $H$ follows both $C$ and $G$ .

(e) $K$ and $L$ follow $I$ .

(f) $J$ succeeds both $E$ and $H$ .

(g) $M$ and $N$ succeed $F$ , but cannot start until both $E$ and $H$ are completed.

(h) $O$ succeeds $M$ and $I$ .

(i) $P$ succeeds $J, L$ , and $O$ .

(j) $K, N$ , and $P$ are the terminal activities of the project.

*6-44. The footings of a building can be completed in four consecutive sections. The activities for each section include (1) digging, (2) placing steel, and (3) pouring concrete. The digging of one section cannot start until that of the preceding section has been completed. The same restriction applies to pouring concrete. Develop the project network.

6-45. In Problem 6-44, suppose that 10% of the plumbing work can be started simultaneously with the digging of the first section but before any concrete is poured. After each section of the footings is completed, an additional 5% of the plumbing can be started provided that the preceding 5% portion is complete. The remaining plumbing can be completed at the end of the project. Construct the project network.

6-46. An opinion survey involves designing and printing questionnaires, hiring and training personnel, selecting participants, mailing questionnaires, and analyzing the data. Construct the project network, stating all assumptions.

6-47. The activities in the following table describe the construction of a new house. Construct the associated project network.

| Activity | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- |
| A | Clear site | - | 1 |
| B | Bring utilities to site | - | 2 |
| C | Excavate | $A$ | 1 |
| D | Pour foundation | $C$ | 2 |
| E | Outside plumbing | $B, C$ | 6 |
| $F$ | Frame house | $D$ | 10 |
| $G$ | Do electric wiring | $F$ | 3 |
| $H$ | Lay floor | $G$ | 1 |
| $I$ | Lay roof | $F$ | 1 |
| $J$ | Inside plumbing | $E, H$ | 5 |
| $K$ | Shingling | $I$ | 2 |
| $L$ | Outside sheathing insulation | $F, J$ | 1 |
| $M$ | Install windows and outside doors | $F$ | 2 |
| $N$ | Do brick work | $L, M$ | 4 |
| $O$ | Insulate walls and ceiling | $G, J$ | 2 |
| $P$ | Cover walls and ceiling | $O$ | 2 |
| $Q$ | Insulate roof | $I, P$ | 1 |
| $R$ | Finish interior | $P$ | 7 |
| $S$ | Finish exterior | $I, N$ | 7 |
| $T$ | Landscape | $S$ | 3 |

6-48. A company is in the process of preparing a budget for launching a new product. The following table provides the associated activities and their durations. Construct the project network.

| Activity | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- |
| A | Forecast sales volume | - | 10 |
| B | Study competitive market | - | 7 |
| C | Design item and facilities | $A$ | 5 |
| D | Prepare production schedule | $C$ | 3 |
| E | Estimate cost of production | $D$ | 2 |
| $F$ | Set sales price | $B, E$ | 1 |
| $G$ | Prepare budget | $E, F$ | 14 |

6-49. The activities involved in a candlelight choir service are listed in the following table. Construct the project network.

| Activity | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- |
| A | Select music | - | 2 |
| B | Learn music | $A$ | 14 |
| C | Make copies and buy books | $A$ | 14 |
| D | Tryouts | $B, C$ | 3 |
| E | Rehearsals | $D$ | 70 |
| $F$ | Rent candelabra | $D$ | 14 |
| $G$ | Decorate candelabra | $F$ | 1 |
| $H$ | Set up decorations | $D$ | 1 |
| $I$ | Order choir robe stoles | $D$ | 7 |
| $J$ | Check out public address system | $D$ | 7 |
| $K$ | Select music tracks | $J$ | 14 |
| $L$ | Set up public address system | $K$ | 1 |
| $M$ | Final rehearsal | $E, G, L$ | 1 |
| $N$ | Choir party | $H, L, M$ | 1 |
| $O$ | Final program | $I, N$ | 1 |

| Activity | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- |
| A | Job review | - | 1 |
| B | Advise customers of temporary outage | $A$ | $\frac{1}{2}$ |
| C | Requisition stores | $A$ | 1 |
| D | Scout job | $A$ | $\frac{1}{2}$ |
| E | Secure poles and material | $C, D$ | 3 |
| F | Distribute poles | $E$ | $3\frac{1}{2}$ |
| $G$ | Pole location coordination | $D$ | $\frac{1}{2}$ |
| $H$ | Re-stake | $G$ | $\frac{1}{2}$ |
| $I$ | Dig holes | $H$ | 3 |
| $J$ | Frame and set poles | $F, I$ | 4 |
| $K$ | Cover old conductors | $F, I$ | 1 |
| $L$ | Pull new conductors | $J, K$ | 2 |
| $M$ | Install remaining material | $L$ | 2 |
| $N$ | Sag conductor | $L$ | 2 |
| $O$ | Trim trees | $D$ | 2 |
| $P$ | De-energize and switch lines | $B, M, N, O$ | $\frac{1}{10}$ |
| $Q$ | Energize and switch new line | $P$ | $\frac{1}{2}$ |
| $R$ | Clean up | $Q$ | 1 |
| S | Remove old conductor | $Q$ | 1 |
| T | Remove old poles | $S$ | 2 |
| $U$ | Return material to stores | $R, T$ | 2 |

6-50. The widening of a road section requires relocating ("reconductoring") 1700 ft of 13.8-kV overhead primary line. The following table summarizes the activities of the project. Construct the associated project network.

6-51. The following table gives the activities for buying a new car. Construct the project network:

| Activity | Description | Predecessor(s) | Duration (days) |
| --- | --- | --- | --- |
| $A$ | Conduct feasibility study | - | 3 |
| $B$ | Find potential buyer for present car | $A$ | 14 |
| $C$ | List possible models | $A$ | 1 |
| $D$ | Research all possible models | $C$ | 3 |
| $E$ | Conduct interview with mechanic | $C$ | 1 |
| $F$ | Collect dealer propaganda | $C$ | 2 |
| $G$ | Compile pertinent data | $D, E, F$ | 1 |
| $H$ | Choose top three models | $G$ | 1 |
| $I$ | Test-drive all three choices | $H$ | 3 |
| $J$ | Gather warranty and financing data | $H$ | 2 |
| $K$ | Choose one car | $I, J$ | 2 |
| $L$ | Choose dealer | $K$ | 2 |
| $M$ | Search for desired color and options | $L$ | 4 |
| $N$ | Test-drive chosen model once again | $L$ | 1 |
| $O$ | Purchase new car | $B, M, N$ | 3 |

*6-52. Determine the critical path for the project network in Figure 6.44.

6-53. Determine the critical path for the project networks in Figure 6.45.

6-54. Determine the critical path for the project in Problem 6-47.

6-55. Determine the critical path for the project in Problem 6-49.

6-56. Determine the critical path for the project in Problem 6-50.

6-57. Determine the critical path for the project in Problem 6-51.

![bo_d56m3tv7aajc73800n00_56_301_190_1331_951_0.jpg](bo_d56m3tv7aajc73800n00_56_301_190_1331_951_0.jpg)

FIGURE 6.45

Project network for Problem 6-53

6-58. Given an activity $\left( {i, j}\right)$ with duration ${D}_{ij}$ and its earliest start time ${\square }_{i}$ and its latest completion time ${\Delta }_{j}$ , determine the earliest completion and the latest start times of $\left( {i, j}\right)$ .

6-59. What are the total and free floats of a critical activity? Explain.

*6-60. For each of the following activities, determine the maximum delay in the starting time relative to its earliest start time that will allow all the immediately succeeding activities to be scheduled anywhere between their earliest and latest completion times.

(a) ${TF} = {20},{FF} = {20}, D = 8$

(b) ${TF} = 8,{FF} = 3, D =  - 2$

(c) ${TF} = 5,{FF} = 0, D = 3$

6-61. In Example 6.5-4, use the floats to answer the following:

(a) If activity $B$ is started at time 1, and activity $C$ is started at time 5, determine the earliest start times for $E$ and $F$ .

(b) If activity $B$ is started at time 3, and activity $C$ is started at time 7, determine the earliest start times for $E$ and $F$ .

(c) How is the scheduling of other activities impacted if activity $B$ starts at time 6?

*6-62. In the project of Example 6.5-2 (Figure 6.28), assume that the durations of activities $B$ and $F$ are changed from 6 and 11 days to 20 and 25 days, respectively.

(a) Determine the critical path.

(b) Determine the total and free floats for the network, and identify the red-flagged activities.

(c) If activity $A$ is started at time 5, determine the earliest possible start times for activities $C, D, E$ , and $G$ .

(d) If activities $F, G$ , and $H$ require the same equipment, determine the minimum number of units needed of this equipment.

6-63. Compute the floats and identify the red-flagged activities for the projects (a) and (b) in Figure 6.30, then develop the time schedules under the following conditions:

Project (a)

(i) Activity $\left( {1,5}\right)$ cannot start any earlier than time 14.

(ii) Activities $\left( {5,6}\right)$ and $\left( {5,7}\right)$ use the same equipment, of which only one unit is available.

(iii) All other activities start as early as possible.

Project (b)

(i) Activity $\left( {1,3}\right)$ must be scheduled at its earliest start time while accounting for the requirement that $\left( {1,2}\right) ,\left( {1,3}\right)$ , and $\left( {1,6}\right)$ use a special piece of equipment, of which only 1 unit is available.

(ii) All other activities start as early as possible.

6-64. (Job shop scheduling) Three jobs, J1, J2, and J3, are processed on 3 machines, M1, M2, and M3, according to the following sequences (processing times are shown in parentheses):

J1: M3(3) - M1(4) - M2(6)

J2: M2(1) - M3(5) - M1(9)

J3: M3(2) - M2(8) - M1(7)

The order in which the jobs are processed on the different machines is predetermined as:

M1: J1 - J2 - J3

M2: J2 - J3 - J1

M3: J3 - J1 - J2

(a) Represent the problem as a CPM network for which the critical path determines the make span of all three jobs.

(b) Use the critical path calculations to develop the scheduling of the jobs (Gantt chart), assuming that each operation is scheduled at its earliest start time.

6-65. Use LP to determine the critical path for the project network in Figure 6.44.

6-66. Use LP to determine the critical path for the project networks in Figure 6.45.

6-67. Consider Problem 6-53. The estimates $\left( {a, m, b}\right)$ are listed in the following table:

| Project (a) activity | $\left( {a, m, b}\right)$ | Project (a) activity | $\left( {a, m, b}\right)$ | Project (b) activity | $\left( {a, m, b}\right)$ | Project (b) activity | $\left( {a, m, b}\right)$ |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1-2 | (5, 6, 8) | 3-6 | $\left( {3,4,5}\right)$ | 1-2 | (1,3,4) | 3-7 | (12,13,14) |
| 1-4 | (1,3,4) | 4-6 | (4,8,10) | 1-3 | (5, 7, 8) | 4-5 | (10,12,15) |
| 1-5 | (2, 4, 5) | 4-7 | (5,6,8) | 1-4 | (6, 7, 9) | 4-7 | (8,10,12) |
| 2-3 | (4, 5, 6) | 5-6 | (9,10,15) | 1-6 | (1, 2, 3) | 5-6 | (7,8,11) |
| 2-5 | (7, 8, 10) | 5-7 | (4,6,8) | 2-3 | (3, 4, 5) | 5-7 | (2, 4, 8) |
| 2-6 | (8,9,13) | 6-7 | (3, 4, 5) | 2-5 | (7, 8, 9) | 6-7 | (5, 6, 7) |
| 3-4 | (5, 9, 19) |  |  | 3-4 | (10,15,20) |  |  |

Determine the probabilities that the different nodes of the project are realized without delay.
