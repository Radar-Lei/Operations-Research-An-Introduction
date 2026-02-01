# CHAPTER 5: Transportation Model and Its Variants ^chapter



```markmap
---
markmap:
  height: 643
---
# [[#^chapter|CHAPTER 5: Transportation Model and Its Variants]]

## [[#^reallife|Real-Life Application: Scheduling Appointments at Trade Events]]

## [[#^definition|Transportation Model (Definition)]]
### [[#^mgauto|Example: MG Auto (Plants → Distribution Centers)]]
### [[#^tableau|Transportation Tableau (Compact Representation)]]
### [[#^balance|Balancing Unbalanced Models (Dummy Source/Destination)]]
#### [[#^dummysource|Dummy Source for Shortage (Demand > Supply)]]
#### [[#^dummydestination|Dummy Destination for Surplus (Supply > Demand)]]
### [[#^history|A Brief History (Monge → Hitchcock → Kantorovich → Dantzig)]]

## [[#^nontraditional|Nontraditional Transportation Models]]
### [[#^prodinventory|Production–Inventory Control as Transportation]]
#### [[#^parallels|Element-by-Element Analogy (Transportation ↔ Inventory)]]
#### [[#^unitcost|Unit “Transportation” Cost Construction (Production + Holding/Penalty)]]
### [[#^toolsharpen|Tool Sharpening Scheduling as Transportation]]
#### [[#^demanddata|Weekly Demand Data (Targets)]]
#### [[#^modeling|Modeling Trick (New Blades + Sharpening Delays + Disposal)]]
#### [[#^rotation|Multiple-Week Rotation Remark (Rolling Horizon)]]

## [[#^algorithm|Transportation Algorithm]]
### [[#^handcomputation|Why Study the Classical Hand Algorithm?]]
### [[#^steps|Simplex-Like Steps (Start → Optimality → Pivot)]]
### [[#^starting|Starting Basic Feasible Solution Methods]]
#### [[#^northwest|Northwest-Corner Method (Fast, Cost-Ignoring)]]
#### [[#^leastcost|Least-Cost Method (Greedy on Cheapest Cells)]]
#### [[#^vogel|Vogel Approximation Method (Penalty-Based Heuristic)]]
### [[#^iteration|Iterative Improvement (Optimality + Feasibility Without Row Ops)]]
#### [[#^multipliers|Method of Multipliers (Compute u/v for Basic Cells)]]
#### [[#^entering|Entering Variable Rule (Most Positive Reduced Cost)]]
#### [[#^loop|Closed Loop Pivot (±θ Adjustments on Corners)]]
#### [[#^theta|Choosing θ and Leaving Variable (Maintain Nonnegativity)]]
#### [[#^transshipment|Transshipment Note (Intermediate Nodes via Modeling Trick)]]
#### [[#^duality|Simplex/Duality Explanation (Reduced Costs as u+v−c)]]

## [[#^assignment|Assignment Model]]
### [[#^hungarian|Hungarian Method (Hand Algorithm for 0–1 Assignment)]]
#### [[#^hungariansteps|Core Steps (Row/Column Reduction → Try Zero Assignment)]]
#### [[#^coverlines|When Zeros Fail: Cover Zeros and Recreate More Zeros]]
### [[#^simplexhungarian|Simplex Explanation and Dual Interpretation]]
#### [[#^constantshift|Row/Column Shifts Change Objective by a Constant Only]]

## [[#^casestudy|Case Study: Scheduling Appointments (ATC Trade Events)]]
### [[#^threedim|Three-Dimensional Assignment (Buyer × Seller × Time Slot)]]
### [[#^preference|Preference Scoring (Combine Buyer/Seller Rankings into cij)]]
### [[#^reliability|Reliability of Input Data (Collection Tool Constraints)]]
### [[#^casesolution|Solution Approach (LP/ILP + Satisfaction Measures)]]
### [[#^walking|Practical Walking Constraints (Transition Feasibility)]]
### [[#^heuristic|Heuristic for the Restricted Model (Solve Session-by-Session)]]
### [[#^quality|Measuring Heuristic Quality (Gap vs Unrestricted Optimum)]]

## [[#^problems|End-of-Chapter Problems]]
```

## Real-Life Application-Scheduling Appointments at Australian Trade Events ^reallife

The Australian Tourist Commission (ATC) organizes trade events around the world to provide a forum for Australian sellers to meet international buyers of tourism products. During these events, sellers are stationed in booths and are visited by buyers according to scheduled appointments. Because of the limited number of time slots available in each event and the fact that the number of buyers and sellers can be quite large (one such event held in Melbourne in 1997 attracted 620 sellers and 700 buyers), ATC attempts to schedule the seller-buyer appointments in advance of the event in a manner that maximizes preferences. The model has resulted in greater satisfaction for both the buyers and sellers.

Details of the study are presented at the end of the chapter.

### 5.1 DEFINITION OF THE TRANSPORTATION MODEL

The problem is represented by the network in Figure 5.1. There are $m$ sources and $n$ destinations, each represented by a node. The arcs represent the routes linking the sources and the destinations. Arc $\left( {i, j}\right)$ joining source $i$ to destination $j$ carries two pieces of information: the transportation cost per unit, ${c}_{ij}$ , and the amount shipped, ${x}_{ij}$ . The amount of supply at source $i$ is ${a}_{i}$ , and the amount of demand at destination $j$ is ${b}_{j}$ . The objective of the model is to minimize the total transportation cost while satisfying all the supply and demand restrictions. ^definition

## Example 5.1-1 ^mgauto

MG Auto has three plants in Los Angeles, Detroit, and New Orleans and two major distribution centers in Denver and Miami. The quarterly capacities of the three plants are 1000, 1500, and 1200 cars, and the demands at the two distribution centers for the same period are 2300 and 1400 cars. The mileage chart between the plants and the distribution centers is given in Table 5.1.

![bo_d56m4e77aajc73800n7g_1_497_200_880_424_0.jpg](bo_d56m4e77aajc73800n7g_1_497_200_880_424_0.jpg)

FIGURE 5.1

Representation of the transportation model with nodes and arcs

TABLE 5.1 Mileage Chart

|              | Denver | Miami |
|--------------|--------|-------|
| Los Angeles  | 1000   | 2690  |
| Detroit      | 1250   | 1350  |
| New Orleans  | 1275   | 850   |

The trucking company in charge of transporting the cars charges 8 cents per mile per car. Thus, the transportation costs per car on the different routes, rounded to the closest dollar, are computed from Table 5.1 as shown in Table 5.2.

The LP model of the problem is

$$
\text{ Minimize }z = {80}{x}_{11} + {215}{x}_{12} + {100}{x}_{21} + {108}{x}_{22} + {102}{x}_{31} + {68}{x}_{32}
$$

subject to

$$
{x}_{11} + {x}_{12}\; = {1000}\text{ (Los Angeles) }
$$

$$
{x}_{21} + {x}_{22}\; = {1500}\text{ (Detroit) }
$$

$$
+ {x}_{31} + {x}_{32} = {1200}\text{ (New Oreleans) }
$$

$$
{x}_{11}\; + {x}_{21}\; + {x}_{31}\; = {2300}\text{ (Denver) }
$$

$$
{x}_{12}\; + {x}_{22}\; + {x}_{32} = {1400}\text{ (Miami) }
$$

$$
{x}_{ij} \geq  0, i = 1,2,3, j = 1,2
$$

All the constraints are equations because the total supply $\left( { = {1000} + {1500} + {1200} = {3700}\text{ cars }}\right)$ equals the total demand $\left( { = {2300} + {1400} = {3700}\text{ cars }}\right)$ .

TABLE 5.2 Transportation Cost per Car

|                 | Denver (1) | Miami (2) |
|-----------------|------------|-----------|
| Los Angeles (1) | \$80       | \$215     |
| Detroit (2)     | \$100      | \$108     |
| New Orleans (3) | \$102      | \$68      |

TABLE 5.3 MG Transportation Model

|   | Denver | Miami | Supply |
|---|--------|-------|--------|
| Los Angeles | 80 $x_{11}$ | 215 $x_{12}$ | 1000 |
| Detroit | 100 $x_{21}$ | 108 $x_{22}$ | 1500 |
| New Orleans | 102 $x_{31}$ | 68 $x_{32}$ | 1200 |
| Demand | 2300 | 1400 |  |

The special structure of the transportation problem allows a compact representation of the problem using the transportation tableau format in Table 5.3. This format is convenient for modeling many situations that do not deal with transporting goods, as demonstrated in Section 5.2. ^tableau

The optimal solution in Figure 5.2 (obtained by TORA ${}^{1}$ ) ships 1000 cars from Los Angeles to Denver $\left( {{x}_{11} = {1000}}\right) ,{1300}$ from Detroit to Denver $\left( {{x}_{21} = {1300}}\right) ,{200}$ from Detroit to Miami $\left( {{x}_{22} = {200}}\right)$ , and 1200 from New Orleans to Miami $\left( {{x}_{32} = {1000}}\right)$ . The associated minimum transportation cost is computed as ${1000} \times  \$ {80} + {1300} \times  \$ {100} + {200} \times  \$ {108} + {1200} \times \; \$ {68} = \$ {313},{200}$ .

Balancing the transportation model. The transportation tableau representation assumes that model is balanced, meaning that the total demand equals to the total supply (which happened to be true-coincidentally-in the MG model). If the model is unbalanced, a dummy source or a dummy destination must be added to restore balance. ^balance

## Example 5.1-2 ^dummysource

In the MG model, suppose that the Detroit plant capacity is 1300 cars (instead of 1500). The total supply (= 3500 cars) is less than the total demand (= 3700 cars), meaning that part of the demand at Denver and Miami will not be satisfied.

Because the demand exceeds the supply, a dummy plant (source) with a capacity of 200 cars (= 3700 - 3500) is added to balance the model. The unit transportation cost from the dummy plant to the two destinations is zero because the plant does not exist. ^dummysource

![bo_d56m4e77aajc73800n7g_2_307_1608_681_405_0.jpg](bo_d56m4e77aajc73800n7g_2_307_1608_681_405_0.jpg)

FIGURE 5.2

Optimal solution of MG Auto model

---

${}^{1}$ To use TORA, from Main Menu select Transportation Model. From the SOLVE/MODIFY menu, select Solve $\Rightarrow$ Final solution to obtain a summary of the optimum solution. A detailed description of the iterative solution of the transportation model is given in Section 5.3.3.

---

TABLE 5.4 MG Model with Dummy Plant

|             | Denver     | Miami      | Supply |
|-------------|-----------|------------|--------|
| Los Angeles | 80<br>1000 | 215        | 1000   |
| Detroit     | 100<br>1300 | 108       | 1300   |
| New Orleans | 102        | 68<br>1200 | 1200   |
| Dummy Plant | 0          | 0<br>200   | 200    |
| Demand      | 2300       | 1400       |        |

Table 5.4 gives the balanced model together with its optimum solution. The solution shows that the dummy plant ships 200 cars to Miami, which means that Miami will be 200 cars short of satisfying its demand of 1400 cars.

We can make sure that a specific destination does not experience shortage by assigning a very high unit transportation cost from the dummy source to that destination. For example, a penalty of \$1000 in the dummy-Miami cell will prevent shortage at Miami. Of course, we cannot use this "trick" with all the destinations, because shortage must take place somewhere.

The case where the supply exceeds the demand can be demonstrated by assuming that the demand at Denver is 1900 cars only. In this case, we need to add a dummy distribution center to "receive" the surplus supply. Again, the unit transportation cost to the dummy distribution center is zero, unless we require a factory to "ship out" completely. In this case, a high unit transportation cost is assigned from the designated factory to the dummy destination. ^dummydestination

Table 5.5 gives the new model and its optimal solution (obtained by TORA). The solution shows that the Detroit plant will have a surplus of 400 cars.

TABLE 5.5 MG Model with Dummy Destination

|             | Denver     | Miami      | Dummy    | Supply |
|-------------|-----------|------------|----------|--------|
| Los Angeles | 80<br>1000 | 215        | 0        | 1000   |
| Detroit     | 100<br>900 | 108<br>200 | 0<br>400 | 1500   |
| New Orleans | 102        | 68<br>1200 | 0        | 1200   |
| Demand      | 1900       | 1400       | 400      |        |

## Aha! Moment: A Brief History of the Transportation Model. ${}^{2}$ ^history

In 1781, French mathematician Gaspard Monge (1746-1818), working with Napoleon Bonaparte's army, published a mathematical model dealing with transporting soil at the least possible cost among different construction sites for the purpose of building military forts and roads. Though Monge laid a theoretical foundation for solving the transportation problem, no algorithm was developed until 1941 when American mathematician Frank L. Hitchcock (1875-1957) published his solution of Monge's problem. In 1939, Russian economist Leonid V. Kantorovich published a booklet titled The Mathematical Method of Production Planning and Organization that in effect laid the foundation for today's linear programming. However, Kantorovich did not become aware of Monge's 1781 paper until 1947 when he immediately recognized the similarities between his work and Monge's. Meanwhile, Dutch American Tjalling C. Koopmans (1910-1985) had been studying the transportation problem independently in support of WWII efforts, and it was only in the late 1950s that he discovered Kantorovich's work on linear programming and transportation. Koopmans was instrumental in reprinting Kantorovich's booklet in the United States, ${}^{3}$ ushering the dissemination of Kantorovich's work in the West. By then, American mathematician George B. Danzig had already developed his simplex method in 1947 for solving any linear programming problem, including the transportation model.

In 1975, Leonid V. Kantorovich and Tjalling C. Koopmans shared the Nobel Prize in Economics.

### 5.2 NONTRADITIONAL TRANSPORTATION MODELS ^nontraditional

The application of the transportation model is not limited to transporting goods. This section presents two nontraditional applications in the areas of production-inventory control and tool sharpening service.

## Example 5.2-1 (Production-Inventory Control) ^prodinventory

Boralis manufactures backpacks for serious hikers. The demand for its product during the peak period of March to June of each year is 100, 200, 180, and 300 units, respectively. The company uses part-time labor to accommodate fluctuations in demand. It is estimated that Boralis can produce 50, 180, 280, and 270 units in March through June. A current month's demand may be satisfied in one of three ways.

1. Current month's production at the cost of \$40 per pack.

2. Surplus production in an earlier month at an additional holding cost of \$.50 per pack per month

3. Surplus production in a later month (back-ordering) at an additional penalty cost of \$2.00 per pack per month.

Boralis wishes to determine the optimal production schedule for the four months.

---

${}^{2}$ A. M. Vershik, Long History of the Monge-Kantorovich Transportation Problem, The Mathematical Intelligencer, Springer Science + Business Media New York, 2013, DOI 10.1007/s00283-013-9380-x.

${}^{3}$ L. V. Kantorovich, Mathematical methods in the organization and planning of production, Leningrad University, 1939. English translation: Management Science, Vol. 6, No. 4, pp. 363-422, 1960.

---

The following table summarizes the parallels between the elements of the production-inventory problem and the transportation model: ^parallels

| Transportation | Production inventory |
|---|---|
| 1. Source $i$ | 1. Production period $i$ |
| 2. Destination $j$ | 2. Demand period $j$ |
| 3. Supply amount at source $i$ | 3. Production capacity of period $i$ |
| 4. Demand at destination $j$ | 4. Demand for period $j$ |
| 5. Unit transportation cost from source $i$ to destination $j$ | 5. Unit cost (production + holding + penalty) in period $i$ for period $j$ |

The resulting transportation model is given in Table 5.6.

The unit "transportation" cost from period $i$ to period $j$ is computed as ^unitcost

$$
{c}_{ij} = \left\{  \begin{array}{l} \text{ Production cost in }i, i = j \\  \text{ Production cost in }i + \text{ holding cost from }i\text{ to }j, i < j \\  \text{ Production cost in }i + \text{ penaty cost from }i\text{ to }j, i > j \end{array}\right.
$$

For example,

$$
{c}_{11} = \$ {40.00}
$$

$$
{c}_{24} = \$ {40.00} + \left( {\$ {.50} + \$ {.50}}\right)  = \$ {41.00}
$$

$$
{c}_{41} = \$ {40.00} + \left( {\$ {2.00} + \$ {2.00} + \$ {2.00}}\right)  = \$ {46.00}
$$

The optimal solution is summarized in Figure 5.3. The dashed lines indicate back-ordering, the dotted lines indicate production for a future period, and the solid lines show production in a period for itself. The total cost is \$31,455.

TABLE 5.6 Transportation Model for Example 5.2-1

|        | 1       | 2       | 3       | 4       | Capacity |
|--------|---------|---------|---------|---------|----------|
| 1      | \$40.00 | \$40.50 | \$41.00 | \$41.50 | 50       |
| 2      | \$42.00 | \$40.00 | \$40.50 | \$41.00 | 180      |
| 3      | \$44.00 | \$42.00 | \$40.00 | \$40.50 | 280      |
| 4      | \$46.00 | \$44.00 | \$42.00 | \$40.00 | 270      |
| Demand | 100     | 200     | 180     | 300     |          |

![bo_d56m4e77aajc73800n7g_5_284_1698_1319_489_0.jpg](bo_d56m4e77aajc73800n7g_5_284_1698_1319_489_0.jpg)

## Example 5.2-2 (Tool Sharpening) ^toolsharpen

Arkansas Pacific operates a sawmill that produces boards from different types of lumber. Depending on the type of wood being milled, the demand for sharp blades varies from day to day according to the following 1-week (7-day) data: ^demanddata

|                | Mon. | Tue. | Wed. | Thu. | Fri. | Sat. | Sun. |
|----------------|------|------|------|------|------|------|------|
| Demand (blades) | 24   | 12   | 14   | 20   | 18   | 14   | 22   |

The mill can satisfy the daily demand in four ways:

1. New blades at the cost of \$12 a piece.

2. Overnight sharpening service for \$6 a blade.

3. One-day sharpening service for \$5 a blade.

4. Two-day sharpening service for \$3 a blade.

The situation can be represented as a transportation model with eight sources and seven destinations. The destinations represent the 7 days of the week. The sources of the model are defined as follows: Source 1 corresponds to buying new blades, which, in the extreme, can cover the demand for all 7 days (= 24 + 12 + 14 + 20 + 18 + 14 + 22 = 124). Sources 2 to 8 correspond to the 7 days of the week. The amount of supply for each of these sources equals the number of used blades at the end of the associated day. For example, source 2 (Monday) will have a supply of used blades equal to the demand for Monday. The unit "transportation cost" for the model is \$12 for new blade, \$6 for overnight sharpening, \$5 for 1-day sharpening, or \$3 all else. The "disposal" column is a dummy destination for balancing the model. The complete model and its solution are given in Table 5.7. ^modeling

The following table summarizes the optimum solution at a total cost of \$818 (file toraEx5.2-2.txt).

| Period | New | Overnight | 1-Day | ≥2-Day | Disposal |
|--------|-----|-----------|-------|--------|----------|
| Mon.   | 24 (Mon.) | 0 | 14 (Wed.) | 10 (Thu.) | 0 |
| Tues.  | 12 (Tue.) | 0 | 0 | 12 (Fri.) | 0 |
| Wed.   | 0 | 10 (Thu.) | 4 (Fri.) | 0 | 0 |
| Thu.   | 0 | 2 (Fri.) | 0 | 18 (Sun.) | 0 |
| Fri.   | 0 | 14 (Sat.) | 4 (Sun.) | 0 | 0 |
| Sat.   | 0 | 0 |  | 0 | 14 |
| Sun.   | 0 | 0 |  | 0 | 22 |

Remarks. The model in Table 5.7 assumes one week of operation only. For multiple weeks, the model must deal with the rotational nature of the days of the week, in the sense that this week's days can act as sources for next week's demand. One way to handle this situation is to assume that the very first week of operation starts with all new blades for each day. From there on, we use a model consisting of exactly seven sources and seven destinations corresponding to the days of the week. The new model will be similar to Table 5.7 less source "New" and destination "Disposal." Also, only main-diagonal cells will be blocked (unit cost $= M$ ). The remaining cells will have a unit cost of \$3.00, \$5.00, or \$6.00. For example, sharpening on Sunday of this week will cost \$6 for Monday of next week, 5 \$ for Tuesday, and \$3 for all else - meaning, the unit costs for Sunday row of the tableau will read \$6, \$5, \$3, \$3, \$3, \$3, \$3, and $M$ , respectively. ^rotation

TABLE 5.7 Tool-Sharpening Problem Expressed as a Transportation Model

|         | 1 Mon.      | 2 Tue.      | 3 Wed.      | 4 Thu.      | 5 Fri.      | 6 Sat.      | 7 Sun.      | 8 Disposal  | Supply |
|---------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|-------------|--------|
| 1-New   | \$12<br>24  | \$12<br>12  | \$12        | \$12        | \$12        | \$12        | \$12        | \$0<br>88    | 124    |
| 2-Mon.  | $M$         | \$6         | \$5<br>14   | \$3<br>10   | \$3         | \$3         | \$3         | \$0          | 24     |
| 3-Tue.  | $M$         | $M$         | \$6         | \$5         | \$3<br>12   | \$3         | \$3         | \$0          | 12     |
| 4-Wed.  | $M$         | $M$         | $M$         | \$6<br>10   | \$5<br>4    | \$3         | \$3         | \$0          | 14     |
| 5-Thu.  | $M$         | $M$         | $M$         | $M$         | \$6<br>2    | \$5         | \$3<br>18   | \$0          | 20     |
| 6-Fri.  | $M$         | $M$         | $M$         | $M$         | $M$         | \$6<br>14   | \$5<br>4    | \$0          | 18     |
| 7-Sat.  | $M$         | $M$         | $M$         | $M$         | $M$         | $M$         | \$6<br>0    | \$0<br>14    | 14     |
| 8-Sun.  | $M$         | $M$         | $M$         | $M$         | $M$         | $M$         | $M$         | \$0<br>22    | 22     |
| Demand  | 24          | 12          | 14          | 20          | 18          | 14          | 22          | 124         |        |


Intuitively, and without solving the new transportation model at all, it is obvious that the cheapest sharpening service (≥2-day) can be used to satisfy all the demand starting from week 2 on. This intuitive conclusion can be confirmed by solving the new model (file toraEx5.2-2a.txt).

### 5.3 THE TRANSPORTATION ALGORITHM ^algorithm

## Aha! Moment: Looking at the Bright Side of Hand Computations: The Classical Transportation Model! ^handcomputation

The special transportation algorithm that will be presented in this section was developed early on when hand computations were the norm and shortcuts were warranted. Today, powerful computer codes can solve transportation models of any size as a regular LP. But there is more to the transportation model than the hand computations. First, its historical significance in the evolution of OR techniques is important and must be preserved. Second, the special transportation tableau format can facilitate modeling a number of situations that do not deal directly with transporting goods (see Section 5.2). Third, the algorithmic hand computations boast such (almost intuitive) simplicity that a beginner can get a "feel" of what optimization is about (could that have been the reason that some early-on textbooks presented the transportation model-also known then as the stepping-stone method-ahead of the more computationally demanding simplex method?). Lastly, the transportation algorithm does provide insight into the use of the theoretical primal-dual relationships (introduced in Section 4.2) to achieve a practical end result - that of developing simple rules for hand computations. The exercise is theoretically intriguing.

The basic steps of the transportation algorithm are exactly those of the simplex method (Chapter 3). However, instead of using the regular simplex tableau, we take advantage of the special structure of the transportation model to carry out the algorithmic computations more conveniently. ^steps

Step 1. Determine a starting basic feasible solution, and go to step 2.

Step 2. Use the optimality condition of the simplex method to determine the entering variable from among all the nonbasic variables. If the optimality condition is satisfied, stop. Otherwise, go to step 3.

Step 3. Use the feasibility condition of the simplex method to determine the leaving variable from among all the current basic variables, and find the new basic solution. Return to step 2.

The details of the algorithm are explained in Sections 5.3.1 and 5.3.2 using the following example.

## Example 5.3-1 (SunRay Transport)

SunRay Transport Company ships truckloads of grain from three silos to four mills. The supply (in truckloads) and the demand (also in truckloads) together with the unit transportation costs per truckload on the different routes are summarized in Table 5.8. The unit transportation costs, ${c}_{ij}$ (shown in the northeast corner of each box), are in hundreds of dollars. The model seeks the minimum cost shipping schedule between the silos and the mills.

TABLE 5.8 SunRay Transportation Model

![bo_d56m4e77aajc73800n7g_8_587_1534_787_606_0.jpg](bo_d56m4e77aajc73800n7g_8_587_1534_787_606_0.jpg)

#### 5.3.1 Determination of the Starting Solution ^starting

A general transportation model with $m$ sources and $n$ destinations has $m + n$ constraint equations, one for each source and each destination. However, because the transportation model is always balanced (sum of the supply $=$ sum of the demand), one of the equations is redundant, reducing the model to $m + n - 1$ independent equations and $m + n - 1$ basic variables. In Example 5.3-1, the starting solution has $3 + 4 - 1 = 6$ basic variables.

The special structure of the transportation problem allows securing a nonartifi-cial starting basic solution using one of three methods: ${}^{4}$

1. Northwest-corner method

2. Least-cost method

3. Vogel approximation method

The first method is "mechanical" in nature in that its main purpose is to provide a starting (basic feasible) solution regardless of the cost. The remaining two are heuristics that seek a better-quality (smaller objective value) starting solution. In general, the Vogel heuristic is best and the northwest-corner method is the worst. The trade-off is that the northwest-corner method involves the least amount of computations.

Northwest-corner method. The method starts at the northwest-corner cell (route) of the tableau (variable ${x}_{11}$ ). ^northwest

Step 1. Allocate as much as possible to the selected cell, and adjust the associated amounts of supply and demand by subtracting the allocated amount.

Step 2. Cross out the row or column with zero supply or demand to indicate that no further assignments can be made in that row or column. If both a row and a column net to zero simultaneously, cross out one only, and leave a zero supply (demand) in the uncrossed-out row (column).

Step 3. If exactly one row or column is left uncrossed out, stop. Otherwise, move to the cell to the right if a column has just been crossed out or below if a row has been crossed out. Go to step 1.

## Example 5.3-2

The application of the procedure to the model of Example 5.3-1 gives the starting basic solution in Table 5.9. The arrows show the order in which the allocated amounts are generated.

The starting basic solution is ${x}_{11} = 5,{x}_{12} = {10},{x}_{22} = 5,{x}_{23} = {15},{x}_{24} = 5,{x}_{34} = {10}$ .

The associated cost of the schedule is $z = 5 \times  {10} + {10} \times  2 + 5 \times  7 + {15} \times  9 + 5 \times  {20} + \; {10} \times  {18} = \$ {520}.$

Least-cost method. The least-cost method finds a better starting solution by targeting the cheapest routes. It assigns as much as possible to the cell with the smallest unit cost (ties are broken arbitrarily). Next, the satisfied row or column is crossed out and the amounts of supply and demand are adjusted accordingly. If both a row and a column are satisfied simultaneously, only one is crossed out, the same as in the northwest-corner method. Next, select the uncrossed-out cell with the smallest unit cost and repeat the process until exactly one row or column is left uncrossed out. ^leastcost

---

${}^{4}$ All three methods are featured in TORA. See the end of Section 5.3.3.

---

![bo_d56m4e77aajc73800n7g_10_543_232_853_480_0.jpg](bo_d56m4e77aajc73800n7g_10_543_232_853_480_0.jpg)

## Example 5.3-3

The least-cost method is applied to Example 5.3-1.

1. Cell $\left( {1,2}\right)$ has the least unit cost in the tableau $\left( { = \$ 2}\right)$ . The most that can be shipped through $\left( {1,2}\right)$ is ${x}_{12} = {15}$ truckloads, which happens to satisfy both row 1 and column 2 simultaneously. We arbitrarily cross out column 2 and adjust the supply in row 1 to 0.

2. Cell $\left( {3,1}\right)$ has the smallest uncrossed-out unit cost $\left( { = \$ 4}\right)$ . Assign ${x}_{31} = 5$ , and cross out column 1 because it is satisfied, and adjust the demand of row 3 to ${10} - 5 = 5$ truckloads.

3. Continuing in the same manner, we successively assign 15 truckloads to cell (2, 3), 0 truckloads to cell $\left( {1,4}\right) ,5$ truckloads to cell $\left( {3,4}\right)$ , and 10 truckload to cell $\left( {2,4}\right)$ (verify!).

The resulting starting solution is summarized in Table 5.10. The arrows show the order in which the allocations are made. The starting solution (consisting of six basic variables) is ${x}_{12} = {15},{x}_{14} = 0,{x}_{23} = {15},{x}_{24} = {10},{x}_{31} = 5,{x}_{34} = 5$ . The associated objective value is $z = {15} \times  2 + 0 \times  {11} + {15} \times  9 + {10} \times  {20} + 5 \times  4 + 5 \times  {18} = \$ {475}$ , which happens to be better than the northwest-corner solution.

TABLE 5.10 Least-Cost Starting Solution

![bo_d56m4e77aajc73800n7g_10_508_1721_909_438_0.jpg](bo_d56m4e77aajc73800n7g_10_508_1721_909_438_0.jpg)

Vogel approximation method (VAM). VAM is an improved version of the least-cost method that generally, but not always, produces better starting solutions. ^vogel

Step 1. For each row (column), determine a penalty measure by subtracting the smallest unit cost in the row (column) from the next smallest unit cost in the same row (column). This penalty is actually a measure of lost opportunity one forgoes if the smallest unit cost cell is not chosen.

Step 2. Identify the row or column with the largest penalty, breaking ties arbitrarily. Allocate as much as possible to the variable with the least unit cost in the selected row or column. Adjust the supply and demand, and cross out the satisfied row or column. If a row and a column are satisfied simultaneously, only one of the two is crossed out, and the remaining row (column) is assigned zero supply (demand).

Step 3. (a) If exactly one row or column with zero supply or demand remains uncrossed out, stop.

(b) If one row (column) with positive supply (demand) remains uncrossed out, determine the basic variables in the row (column) by the least-cost method. Stop.

(c) If all the uncrossed-out rows and columns have (remaining) zero supply and demand, determine the zero basic variables by the least-cost method. Stop.

(d) Otherwise, go to step 1.

## Example 5.3-4

VAM is applied to Example 5.3-1. Table 5.11 computes the first set of penalties.

Because row 3 has the largest penalty $\left( { = {10}}\right)$ and cell $\left( {3,1}\right)$ has the smallest unit cost in that row, the amount 5 is assigned to ${x}_{31}$ . Column 1 is now satisfied and must be crossed out. Next, new penalties are recomputed as in Table 5.12, showing that row 1 has the highest penalty $\left( { = 9}\right)$ . Hence, we assign the maximum amount possible to cell $\left( {1,2}\right)$ , which yields ${x}_{12} = {15}$ and simultaneously satisfies both row 1 and column 2. We arbitrarily cross out column 2 and adjust the supply in row 1 to zero.

TABLE 5.11 Row and Column Penalties in VAM

![bo_d56m4e77aajc73800n7g_11_389_1681_1090_438_0.jpg](bo_d56m4e77aajc73800n7g_11_389_1681_1090_438_0.jpg)

TABLE 5.12 First Assignment in VAM $\left( {{x}_{31} = 5}\right)$

![bo_d56m4e77aajc73800n7g_12_472_263_1013_452_0.jpg](bo_d56m4e77aajc73800n7g_12_472_263_1013_452_0.jpg)

Continuing in the same manner, row 2 will produce the highest penalty $\left( { = {11}}\right)$ , and we assign ${x}_{23} = {15}$ , which crosses out column 3 and leaves 10 units in row 2 . Only column 4 is left, and it has a positive supply of 15 units. Applying the least-cost method to that column, we successively assign ${x}_{14} = 0,{x}_{34} = 5$ , and ${x}_{24} = {10}$ (verify!). The associated objective value for this solution is $z = {15} \times  2 + 0 \times  {11} + {15} \times  9 + {10} \times  {20} + 5 \times  4 + 5 \times  {18} = \$ {475}$ . This solution happens to have the same objective value as in the least-cost method.

## Aha! Moment: By Whatever Name, NW Rule Boasts Elegant Simplicity!

There is nothing really sacred about initiating the northwest (NW) rule from the northwest-corner cell and cascading downward until reaching the southeast corner (SE) because the same solution will ensue if the procedure is initiated from the SE corner, zigzagging upward toward the NW cell (recall that all we are doing is solve ${x}_{ij} = \min$ \{remainders of supply $i$ and demand $j\}$ , try it!). In fact, initiating the procedure from the northeast corner (NE) and cascading downward toward the southwest corner (SW), and vice versa, will produce a valid, though different, starting basic feasible solution. This, incidentally, is evident by the fact that least-cost and Vogel can start from any cell and still produce a basic feasible solution. But regardless of the specific cell used to find the starting solution, the NW rule boasts elegant simplicity not shared by the least-cost and Vogel methods. And this simplicity could be an advantage in some practical situations. "Imagine Facebook trying to use a (literally huge) transportation problem to assign customer traffic to servers and that there is no time, cost data, or value to solve the transportation problem as an LP. At that scale, using the NW rule to produce a feasible solution is likely better than hoping LP come back, in any amount of time, with the optimum solution."5

---

${}^{5}$ Michael Trick (Carnegie Mellon University) proposed this neat application to me (his text is copied here verbatim) in an email dated March 13, 2015, in partial response to my questioning the practical usefulness of the NW corner rule and the transportation algorithm (among other hand-computational classical OR techniques).

---

#### 5.3.2 Iterative Computations of the Transportation Algorithm ^iteration

After determining the starting solution (using one of the methods in Section 5.3.1), we use the following algorithm to determine the optimum solution:

Step 1. Use the simplex optimality condition to determine the entering variable. If the optimality condition is satisfied, stop. Otherwise, go to step 2.

Step 2. Determine the leaving variable using the simplex feasibility condition. Change the basis, and return to step 1.

The optimality and feasibility conditions do not involve the familiar row operations used in the simplex method. Instead, the special structure of the transportation model allows simpler (hand) computations.

## Example 5.3-5

Solve the transportation model of Example 5.3-1, starting with the northwest-corner solution.

Table 5.13 gives the northwest-corner starting solution as determined in Table 5.9 in Example 5.3-2. The determination of the entering variable from among the current nonbasic variables (those that are not part of the starting basic solution) is done by computing the nonbasic coefficients in the $z$ -row, using the method of multipliers (which, as shown in Section 5.3.3, is rooted in LP duality theory).

In the method of multipliers, we associate the multipliers ${u}_{i}$ and ${v}_{j}$ with row $i$ and column $j$ of the transportation tableau. For each current basic variable ${x}_{ij}$ , these multipliers are shown in Section 5.3.3 to satisfy the following equations: ^multipliers

$$
{u}_{i} + {v}_{j} = {c}_{ij}\text{ , for each basic }{x}_{ij}
$$

As Table 5.13 shows, the starting solution has six basic variables, which leads to six equations in seven unknowns. To solve these equations, the method of multipliers calls for setting any of the

TABLE 5.13 Starting Iteration

|        | 1       | 2       | 3       | 4        | Supply |
|--------|---------|---------|---------|----------|--------|
| 1      | 10<br>5 | 2<br>10 | 20      | 11       | 15     |
| 2      | 12      | 7<br>5  | 9<br>15 | 20<br>5  | 25     |
| 3      | 4       | 14      | 16      | 18<br>10 | 10     |
| Demand | 5       | 15      | 15      | 15       |        |

multiplier equal to zero. We will arbitrarily set ${u}_{1} = 0$ , and then solve for the remaining variables as shown in the following table:

| Basic variable | (u, v) -Equation | Solution                           |
| -------------- | ---------------- | ---------------------------------- |
| $x_{11}$       | $u_1 + v_1 = 10$ | Set $u_1 = 0 \Rightarrow v_1 = 10$ |
| $x_{12}$       | $u_1 + v_2 = 2$  | $u_1 = 0 \Rightarrow v_2 = 2$      |
| $x_{22}$       | $u_2 + v_2 = 7$  | $v_2 = 2 \Rightarrow u_2 = 5$      |
| $x_{23}$       | $u_2 + v_3 = 9$  | $u_2 = 5 \Rightarrow v_3 = 4$      |
| $x_{24}$       | $u_2 + v_4 = 20$ | $u_2 = 5 \Rightarrow v_4 = 15$     |
| $x_{34}$       | $u_3 + v_4 = 18$ | $v_4 = 15 \Rightarrow u_3 = 3$     |

To summarize, we have

$$
{u}_{1} = 0,{u}_{2} = 5,{u}_{3} = 3
$$

$$
{v}_{1} = {10},{v}_{2} = 2,{v}_{3} = 4,{v}_{4} = {15}
$$

Next, we use ${u}_{i}$ and ${v}_{j}$ to evaluate the nonbasic variables by computing

$$
{u}_{i} + {v}_{j} - {c}_{ij}\text{ , for each nonbasic }{x}_{ij}
$$

The results of these evaluations are shown in the following table:

| Nonbasic variable | ${u}_{i} + {v}_{j} - {c}_{ij}$ |
|---|---|
| ${x}_{13}$ | ${u}_{1} + {v}_{3} - {c}_{13} = 0 + 4 - {20} =  - {16}$ |
| ${x}_{14}$ | ${u}_{1} + {v}_{4} - {c}_{14} = 0 + {15} - {11} = 4$ |
| ${x}_{21}$ | ${u}_{2} + {v}_{1} - {c}_{21} = 5 + {10} - {12} = 3$ |
| ${x}_{31}$ | ${u}_{3} + {v}_{1} - {c}_{31} = 3 + {10} - 4 = \mathbf{9}$ |
| ${x}_{32}$ | ${u}_{3} + {v}_{2} - {c}_{32} = 3 + 2 - {14} =  - 9$ |
| ${x}_{33}$ | ${u}_{3} + {v}_{3} - {c}_{33} = 3 + 4 - {16} =  - 9$ |

The preceding information, together with the fact that ${u}_{i} + {v}_{j} - {c}_{ij} = 0$ for basic ${x}_{ij}$ , is actually equivalent to computing the $z$ -row of the simplex tableau, as the following summary shows:

|   | ${x}_{11}$ | ${x}_{12}$ | ${x}_{13}$ | ${x}_{14}$ | ${x}_{21}$ | ${x}_{22}$ | ${x}_{23}$ | ${x}_{24}$ | ${x}_{31}$ | ${x}_{32}$ | ${x}_{33}$ | ${x}_{34}$ |
|---|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|------------|
| Z | 0          | 0          | -16        | 4          | 3          | 0          | 0          | 0          | 9          | -9         | -9         | 0          |

Because the transportation model minimizes cost, the entering variable is the one having the most positive coefficient in the $z$ -row-namely, ${x}_{31}$ is the entering variable. ^entering

All the preceding computations are usually done directly on the transportation tableau as shown in Table 5.14, meaning that it is not necessary to write the $\left( {u, v}\right)$ -equations explicitly. Instead, we start by setting ${u}_{1} = {0}^{6}$ Then we can compute the $v$ -values of all the columns that have basic variables in row 1 - namely, ${v}_{1}$ and ${v}_{2}$ . Next, we compute ${u}_{2}$ based on the $\left( {u, v}\right)$ -equation of basic ${x}_{22}$ . Now, given ${u}_{2}$ , we can compute ${v}_{3}$ and ${v}_{4}$ . Finally, we determine ${u}_{3}$ using the basic equation of ${x}_{33}$ . The next step is to evaluate the nonbasic variables by computing ${u}_{i} + {v}_{j} - {c}_{ij}$ for each nonbasic ${x}_{ij}$ , as shown in Table 5.14 in the boxed southeast corner of each cell.

---

${}^{6}$ The tutorial module of TORA is designed to demonstrate that assigning a zero initial value to any $u$ or $v$ produces the same $u + v - c$ for all the nonbasic variables. See the TORA moment following this example.

---

TABLE 5.14 Iteration 1 Calculations

|              | ${v}_{1} = {10}$ | ${v}_{2} = 2$ | ${v}_{3} = 4$ | ${v}_{4} = {15}$ | Supply |
|--------------|------------------|---------------|---------------|------------------|--------|
| ${u}_{1} \equiv  0$ | 10<br>5           | 2<br>10        | 20<br>-16      | 11<br>4           | 15     |
| ${u}_{2} = 5$       | 12<br>3           | 7<br>5         | 9<br>15        | 20<br>5           | 25     |
| ${u}_{3} = 3$       | 4<br>9            | 14<br>-9       | 16<br>-9       | 18<br>10          | 10     |
| Demand       | 5                | 15            | 15            | 15               |        |

Having identified ${x}_{31}$ as the entering variable, we need to determine the leaving variable. Remember that if ${x}_{31}$ enters the solution to become basic, one of the current basic variables must leave as nonbasic (at zero level).

The selection of ${x}_{31}$ as the entering variable means shipping through this route reduces the total shipping cost. What is the most that we can ship through the new route? Observe in Table 5.14 that if route $\left( {3,1}\right)$ ships $\theta$ units (i.e., ${x}_{31} = \theta$ ), then the maximum value of $\theta$ is determined based on two conditions:

1. Supply limits and demand requirements remain satisfied.

2. Shipments through all routes remain nonnegative.

These two conditions determine the maximum value of $\theta$ and the leaving variable in the following manner. First, construct a closed loop that starts and ends at the entering variable cell (3,1). The loop consists of connected horizontal and vertical segments only (no diagonals are allowed) whose corner elements (excluding the entering variable cell) must coincide with a current basic variable. ${}^{7}$ Table 5.15 shows the loop for ${x}_{31}$ . Exactly one loop exists for a given entering variable. ^loop

Next, we assign the amount $\theta$ to the entering variable cell $\left( {3,1}\right)$ . For the supply and demand limits to remain satisfied, we must alternate between subtracting and adding the amount $\theta$ at the successive corners of the loop as shown in Table 5.15 (it is immaterial if the loop is traced in a clockwise or counterclockwise direction). For $\theta  \geq  0$ , the new values of all the variables remain nonnegative if

$$
{x}_{11} = 5 - \theta  \geq  0
$$

$$
{x}_{22} = 5 - \theta  \geq  0
$$

$$
{x}_{34} = {10} - \theta  \geq  0
$$

---

${}^{7}$ TORA’s tutorial module allows you to determine the corner cells of the closed loop interactively, with immediate feedback regarding the validity of your selections. See the TORA moment immediately following this example.

---

TABLE 5.15 Determination of the Closed Loop for ${x}_{31}$

| ${v}_{1} = {10} \; {v}_{2} = 2$ | ${v}_{3} = 4$ | ${v}_{4} = {15}$ | Supply |
|---|---|---|---|
| 10 2<br>${u}_{1} \equiv  0$ 5 $\theta  <  -  -$ -----<br>- + A<br>12 7<br>${u}_{2} = 5$<br>3 -<br>4 14<br>${u}_{3} = 3$<br>+ 9 -9<br>Demand 5 15 | 20<br>-16<br>9<br>16<br>-9<br>15 | 11<br>4<br>20<br>$5 + \theta$<br>18<br>-<br>15 | 15<br>25<br>10 |

The corresponding maximum value of $\theta$ is 5, which occurs when both ${x}_{11}$ and ${x}_{22}$ reach zero level. Either ${x}_{11}$ or ${x}_{22}$ leaves the solution. Intuitively, though not crucial, it may be advantageous computationally to break the tie by selecting the variable with the higher unit cost. Hence we choose ${x}_{11}$ (with ${c}_{11} = {10}$ as opposed to ${c}_{22} = 7$ ) as the leaving variable. ^theta

The values of the basic variables at the corners of the closed loop are adjusted to accommodate setting ${x}_{31} = 5$ , as Table 5.16 shows. Because each unit shipped through route $\left( {3,1}\right)$ reduces the shipping cost by $\$ 9\left( { = {u}_{3} + {v}_{1} - {c}_{31}}\right)$ , the total cost associated with the new schedule is $\$ 9 \times  5 = \$ {45}$ less than in the previous schedule. Thus, the new cost is \$520 - \$45 = \$475.

Given the new basic solution, we repeat the computation of the multipliers $u$ and $v$ , as Table 5.16 shows. The entering variable is ${x}_{14}$ . The closed loop shows that ${x}_{14} = {10}$ and that the leaving variable is ${x}_{24}$ .

The new solution, shown in Table 5.17, costs $\$ 4 \times  {10} = \$ {40}$ less than the preceding one, thus yielding the new cost $\$ {475} - \$ {40} = \$ {435}$ . The new values of ${u}_{i} + {v}_{j} - {c}_{ij}$ are now negative for all nonbasic ${x}_{ij}$ . Thus, the solution in Table 5.17 is optimal.

TABLE 5.16 Iteration 2 Calculations

|              | ${v}_{1} = 1 \; {v}_{2} = 2$ | ${v}_{3} = 4$ | ${v}_{4} = {15}$ | Supply |
|--------------|------------------------------|---------------|------------------|--------|
| ${u}_{1} \equiv  0$ | 10 2<br>15 -<br>-9 - A | 20<br>-16      | 11<br>一 θ<br>+ 暂 4 | 15     |
| ${u}_{2} = 5$       | 12 暂 7<br>0 + $\theta  <  -$<br>-6 + | 9<br>15 | ✓ 20<br>- | 25 |
| ${u}_{3} = 3$ 5     | 4 14<br>-9              | 16<br>-9       | 18<br>5           | 10     |
| Demand       | 5                            | 15            | 15               |        |

TABLE 5.17 Iteration 3 Calculations (Optimal)

![bo_d56m4e77aajc73800n7g_17_464_268_939_487_0.jpg](bo_d56m4e77aajc73800n7g_17_464_268_939_487_0.jpg)

The following table summarizes the optimum solution:

| From silo | To mill | Number of truckloads |
|----------|---------|----------------------|
| 1        | 2       | 5                    |
| 1        | 4       | 10                   |
| 2        | 2       | 10                   |
| 2        | 3       | 15                   |
| 3        | 1       | 5                    |
| 3        | 4       | 5                    |
| Optimal cost |  | \$435 |

Transshipment model. The transportation model assumes direct shipments between sources and destinations. This may not be the case in many situations where it may be cheaper to transship through intermediate nodes before reaching the final destination. A modeling trick based on the use of buffers can be used to convert the transshipment model into a regular transportation model. The conversion idea is interesting theoretically, but it is rarely implemented in practice because the transshipment model (and, indeed, the transportation model itself) is a special case of the highly efficient minimum cost capacitated network model presented in Section 22.1 on the website. Nevertheless, for the sake of completeness, the transshipment model is presented as an appendix at the end of Section 22.1. ^transshipment

## TORA Moment

From Solve/Modify Menu, select Solve $\Rightarrow$ Iterations, and choose one of the three methods (northwest-corner, least-cost, or Vogel) to start the transportation model iterations. The iterations module offers two useful interactive features:

1. You can set any $u$ or $v$ equal to zero before generating iteration 2 (the default is ${u}_{1} = 0$ ). Although the values of ${u}_{i}$ and ${v}_{j}$ change, the evaluation of the nonbasic cells $\left( { = {u}_{i} + {v}_{j} - {c}_{ij}}\right)$ remains the same.

2. You can test your understanding of the selection of the closed loop by clicking (in any order) the corner cells that comprise the path. If your selection is correct, the cell will change color (green for entering variable, red for leaving variable, and gray otherwise).

## Solver Moment

Figure 5.4 provides the Excel Solver template for Example 5.3-1 (file solverEx5.3-1.xls), together with all the formulas and the definition of range names.

In the input section, data include unit cost matrix (cells B4:E6), source names (cells A4:A6), destination names (cells B3:E3), supply (cells F4:F6), and demand (cells B7:E7). In the output section, cells B11:E13 provide the optimal solution in matrix form. The total cost formula is in target cell A10.

## FIGURE 5.4

Excel Solver solution of the transportation model of Example 5.3-1 (file solverEx5.3-1.xls)

![bo_d56m4e77aajc73800n7g_18_366_844_1228_1320_0.jpg](bo_d56m4e77aajc73800n7g_18_366_844_1228_1320_0.jpg)

## AMPL Moment

Files amplEx5.3-1a.txt, amplEx5.3-1b.txt, and amplEx5.3-1c.txt provide three AMPL models for Example 5.3-1. Details are explained in Section C.9 on the website.

#### 5.3.3 Simplex Method Explanation of the Method of Multipliers ^duality

The relationship between the method of multipliers and the simplex method can be explained based on the primal-dual relationships (Section 4.2 ). From the special structure of the LP representing the transportation model (see Example 5.1-1 for an illustration), the associated dual problem can be written as

$$
\text{ Maximize }z = \mathop{\sum }\limits_{{i = 1}}^{m}{a}_{i}{u}_{i} + \mathop{\sum }\limits_{{j = 1}}^{n}{b}_{j}{v}_{j}
$$

subject to

$$
{u}_{i} + {v}_{j} \leq  {c}_{ij}\text{ , all }i\text{ and }j
$$

$$
{u}_{i}\text{ and }{v}_{j}\text{ unrestricted }
$$

where

${a}_{i} =$ Supply amount at source $i$

${b}_{j} =$ Demand amount at destination $j$

${c}_{ij} =$ Unit transportation cost from source $i$ to destination $j$

${u}_{i} =$ Dual variable of the constraint associated with source $i$

${v}_{j} =$ Dual variable of the constraint associated with destination $j$

From Formula 2, Section 4.2.4, the objective-function coefficients (reduced costs) of the variable ${x}_{ij}$ equal the difference between the left- and right-hand sides of the corresponding dual constraint - that is, ${u}_{i} + {v}_{j} - {c}_{ij}$ . However, we know that this quantity must equal zero for each basic variable, which produces the following result:

$$
{u}_{i} + {v}_{j} = {c}_{ij}\text{ , for each basic variable }{x}_{ij}\text{ . }
$$

There are $m + n - 1$ such equations whose solution (after assuming an arbitrary value ${u}_{1} = 0$ ) yields the multipliers ${u}_{i}$ and ${v}_{j}$ . Once these multipliers are computed, the entering variable is determined from all the nonbasic variables as the one having the largest positive ${u}_{i} + {v}_{j} - {c}_{ij}$ .

The assignment of an arbitrary value to one of the dual variables (i.e., ${u}_{1} = 0$ ) may appear inconsistent with the way the dual variables are computed using Method 2 in Section 4.2.3. Namely, for a given basic solution (and, hence, inverse), the dual values must be unique. Problem 5-31 addresses this point.

### 5.4 THE ASSIGNMENT MODEL ^assignment

The classical assignment model deals with matching workers (with varying skills) to jobs. Presumably, skill variation affects the cost of completing a job. The goal is to determine the minimum cost assignment of workers to jobs. The general assignment model with $n$ workers and $n$ jobs is represented in Table 5.18. The element ${c}_{ij}$ represents the cost of assigning worker $i$ to job $j\left( {i, j = 1,2,\ldots , n}\right)$ . There is no loss of generality in assuming that the number of workers and the number of jobs are equal, because we can always add fictitious workers or fictitious jobs to satisfy this assumption.

The assignment model is a special case of the transportation model where workers represent sources and jobs represent destinations. The supply (demand) amount at each source (destination) exactly equals 1 . The cost of "transporting" worker $i$ to job $j$ is ${c}_{ij}$ . In effect, the assignment model can be solved directly as a regular transportation model (or as a regular LP). Nevertheless, the fact that all the supply and demand amounts equal 1 has led to the development of a simple solution algorithm called the Hungarian method. Although the new solution method appears totally unrelated to the transportation model, the algorithm is actually rooted in the simplex method, just as the transportation model is.

#### 5.4.1 The Hungarian Method ${}^{8}$ ^hungarian

We will use two examples to present the mechanics of the new algorithm. The next section provides a simplex-based explanation of the procedure.

![bo_d56m4e77aajc73800n7g_20_715_1424_604_422_0.jpg](bo_d56m4e77aajc73800n7g_20_715_1424_604_422_0.jpg)

---

${}^{8}$ As with the transportation model, the classical Hungarian method, designed primarily for hand computations, is something of the past and is presented here for historical reasons. Today, the need for such computational shortcuts is not warranted, as the problem can be solved by highly efficient LP computer codes. Perhaps the benefit from studying these classical techniques is that they are based on a sophisticated theory that reduces the solution steps to simple rules suitable for hand computations.

---

## Example 5.4-1

Joe Klyne's three children, John, Karen, and Terri, want to earn some money for personal expenses. Mr. Klyne has chosen three chores for his children: mowing the lawn, painting the garage door, and washing the family cars. To avoid anticipated sibling competition, he asks them to submit individual (secret) bids for what they feel is fair pay for each of the three chores. Table 5.19 summarizes the bids received. The children will abide by their father's decision regarding the assignment of chores.

The assignment problem will be solved by the Hungarian method.

Step 1. Determine ${p}_{i}$ , the minimum cost element of row $i$ in the original cost matrix, and subtract it from all the elements of row $i, i = 1,2,3$ . ^hungariansteps

Step 2. For the matrix created in step 1, determine ${q}_{j}$ , the minimum cost element of column $j$ , and subtract it from all the elements of column $j, j = 1,2,3$ .

Step 3. From the matrix in step 2, attempt to find a feasible assignment among all the resulting zero entries.

3a. If such an assignment can be found, it is optimal.

3b. Else, additional calculations are needed (as will be explained in Example 5.4-2).

Table 5.20 shows the application of the three steps to the current problem.

The cells with underscored zero entries in step 3 provide the (feasible) optimum solution: John gets the paint job, Karen gets to mow the lawn, and Terri gets to wash the family cars. The total cost to Mr. Klyne is $9 + {10} + 8 = \$ {27}$ . This amount also will always equal $\left( {{p}_{1} + {p}_{2} + {p}_{3}}\right)  + \left( {{q}_{1} + {q}_{2} + {q}_{3}}\right)  = \left( {9 + 9 + 8}\right)  + \left( {0 + 1 + 0}\right)  = \$ {27}$ . (A justification of this result is given in the next section.)

TABLE 5.19 Klyne's Assignment Problem

|       | Mow  | Paint | Wash |
|-------|------|-------|------|
| John  | \$15 | \$10  | \$9  |
| Karen | \$9  | \$15  | \$10 |
| Terri | \$10 | \$12  | \$8  |

TABLE 5.20 Application of the Hungarian Method to the Assignment Problem of Example 5.4-1

**Step 1 (row reduction)**

|       | Mow | Paint | Wash | Row min |
|-------|-----|-------|------|---------|
| John  | 15  | 10    | 9    | ${p}_{1} = 9$ |
| Karen | 9   | 15    | 10   | ${p}_{2} = 9$ |
| Terri | 10  | 12    | 8    | ${p}_{3} = 8$ |

**Step 2 (column reduction after Step 1)**

|       | Mow | Paint | Wash |
|-------|-----|-------|------|
| John  | 6   | 1     | 0    |
| Karen | 0   | 6     | 1    |
| Terri | 2   | 4     | 0    |

Column min: ${q}_{1} = 0$, ${q}_{2} = 1$, ${q}_{3} = 0$

**Step 3 (find a feasible zero assignment)**

|       | Mow | Paint | Wash |
|-------|-----|-------|------|
| John  | 6   | 0     | 0    |
| Karen | 0   | 5     | 1    |
| Terri | 2   | 3     | 0    |

As stated in step 3 of the Hungarian method, the zeros created by steps 1 and 2 may not yield a feasible solution directly. In this case, further steps are needed to find the optimal (feasible) assignment. The following example demonstrates this situation.

## Example 5.4-2

Suppose that the situation discussed in Example 5.4-1 is extended to four children and four chores. Table 5.21 summarizes the cost elements of the problem.

The application of steps 1 and 2 to the matrix in Table 5.21 (using ${p}_{1} = 1,{p}_{2} = 7,{p}_{3} = 4$ , ${p}_{4} = 5,{q}_{1} = 0,{q}_{2} = 0,{q}_{3} = 3$ , and ${q}_{4} = 0$ ) yields the reduced matrix in Table 5.22 (verify!):

The locations of the zero entries do not allow assigning unique chores to all the children. For example, if we assign child 1 to chore 1, then column 1 will be eliminated, and child 3 will not have a zero entry in the remaining three columns. This obstacle can be accounted for by adding the following step to the procedure given in Example 5.4-1:

Step 3b. If no feasible zero-element assignments can be found, ^coverlines

(i) Draw the minimum number of horizontal and vertical lines in the last reduced matrix to cover all the zero entries.

(ii) Select the smallest uncovered entry, subtract it from every uncovered entry, and then add it to every entry at the intersection of two lines.

(iii) If no feasible assignment can be found among the resulting zero entries, repeat step 3a.

The application of step 3b to the last matrix produces the shaded cells in Table 5.23. The smallest unshaded entry (shown underscored) equals 1 . This entry is added to the intersection cells and subtracted from the remaining shaded cells to produce the matrix in Table 5.24, and the optimal solution shown by underscored zeros.

TABLE 5.21 Assignment Model

| Child | Chore 1 | Chore 2 | Chore 3 | Chore 4 |
|------|---------|---------|---------|---------|
| 1    | \$1     | \$4     | \$6     | \$3     |
| 2    | \$9     | \$7     | \$10    | \$9     |
| 3    | \$4     | \$5     | \$11    | \$7     |
| 4    | \$8     | \$7     | \$8     | \$5     |

TABLE 5.22 Reduced Assignment Matrix

| Child | Chore 1 | Chore 2 | Chore 3 | Chore 4 |
|------|---------|---------|---------|---------|
| 1    | 0       | 3       | 2       | 2       |
| 2    | 2       | 0       | 0       | 2       |
| 3    | 0       | 1       | 4       | 3       |
| 4    | 3       | 2       | 0       | 0       |

TABLE 5.23 Application of Step 3b

| Child | Chore 1 | Chore 2 | Chore 3 | Chore 4 |
|------|---------|---------|---------|---------|
| 1    | 0       | 3       | 2       | 2       |
| 2    | 2       | 0       | 0       | 2       |
| 3    | 0       | 1       | 4       | 3       |
| 4    | 3       | 2       | 0       | 0       |

TABLE 5.24 Optimal Assignment

| Child | Chore 1 | Chore 2 | Chore 3 | Chore 4 |
|------|---------|---------|---------|---------|
| 1    | 0       | 2       | 1       | 1       |
| 2    | 3       | 0       | 0       | 2       |
| 3    | 0       | 0       | 3       | 2       |
| 4    | 4       | 2       | 0       | 0       |

AMPL Moment

File amplEx5.4-2.txt provides the AMPL model for the assignment model. The model is similar to that of the transportation model.

#### 5.4.2 Simplex Explanation of the Hungarian Method ^simplexhungarian

The assignment problem in which $n$ workers are assigned to $n$ jobs can be represented as an LP model in the following manner: Let ${c}_{ij}$ be the cost of assigning worker $i$ to job $j$ , and define

$$
{x}_{ij} = \left\{  \begin{array}{ll} 1, & \text{ if worker }i\text{ is assigned to job }j \\  0, & \text{ otherwise } \end{array}\right.
$$

Then the LP model is given as

$$
\text{ Minimize }z = \mathop{\sum }\limits_{{i = 1}}^{n}\mathop{\sum }\limits_{{j = 1}}^{n}{c}_{ij}{x}_{ij}
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{x}_{ij} = 1, i = 1,2,\ldots , n
$$

$$
\mathop{\sum }\limits_{{i = 1}}^{n}{x}_{ij} = 1, j = 1,2,\ldots , n
$$

$$
{x}_{ij} = 0\text{ or }1
$$

The optimal solution of the preceding LP model remains unchanged if a constant is added to or subtracted from any row or column of the cost matrix $\left( {c}_{ij}\right)$ . To prove this point, let ${p}_{i}$ and ${q}_{j}$ be constants subtracted from row $i$ and column $j$ . Thus, the cost element ${c}_{ij}$ is changed to ^constantshift

$$
{c}_{ij}^{\prime } = {c}_{ij} - {p}_{i} - {q}_{j}
$$

Now

$$
\mathop{\sum }\limits_{i}\mathop{\sum }\limits_{j}{c}_{ij}^{\prime }{x}_{ij} = \mathop{\sum }\limits_{i}\mathop{\sum }\limits_{j}\left( {{c}_{ij} - {p}_{i} - {q}_{j}}\right) {x}_{ij} = \mathop{\sum }\limits_{i}\mathop{\sum }\limits_{j}{c}_{ij}{x}_{ij} - \mathop{\sum }\limits_{i}{p}_{i}\left( {\mathop{\sum }\limits_{j}{x}_{ij}}\right)  - \mathop{\sum }\limits_{j}{q}_{j}\left( {\mathop{\sum }\limits_{i}{x}_{ij}}\right)
$$

$$
= \mathop{\sum }\limits_{i}\mathop{\sum }\limits_{j}{c}_{ij}{x}_{ij} - \mathop{\sum }\limits_{i}{p}_{i}\left( 1\right)  - \mathop{\sum }\limits_{j}{q}_{j}\left( 1\right)
$$

$$
= \mathop{\sum }\limits_{i}\mathop{\sum }\limits_{j}{c}_{ij}{x}_{ij} - \text{ constant }
$$

Because the new objective function differs from the original by a constant, the optimum values of ${x}_{ij}$ are the same in both cases. The development shows that steps 1 and 2 of the Hungarian method, which call for subtracting ${p}_{i}$ from row $i$ and then subtracting ${q}_{j}$ from column $j$ , produce an equivalent assignment model. In this regard, if a feasible solution can be found among the zero entries of the cost matrix created by steps 1 and 2, then it must be optimum (because the cost in the modified matrix cannot be less than zero).

If the created zero entries cannot yield a feasible solution (as Example 5.4-2 demonstrates), then step 2a (dealing with the covering of the zero entries) must be applied. The validity of this procedure is again rooted in the simplex method of linear programming and can be explained by duality theory (Chapter 4) and the complementary slackness theorem (Chapter 7). We will not present the details of the proof here because they are somewhat involved.

The reason $\left( {{p}_{1} + {p}_{2} + \ldots  + {p}_{n}}\right)  + \left( {{q}_{1} + {q}_{2} + \ldots  + {q}_{n}}\right)$ gives the optimal objective value is that it represents the dual objective function of the assignment model. This result can be seen through comparison with the dual objective function of the transportation model given in Section 5.3.3. [See Bazaraa and Associates (2009) for the details.]

## BIBLIOGRAPHY

Bazaraa, M., J. Jarvis, and H. Sherali, Linear Programming and Network Flows, 4th ed., Wiley, New York, 2009.

Dantzig, G., Linear Programming and Extensions, Princeton University Press, Princeton, NJ, 1963.

Hansen, P., and R. Wendell, "A Note on Airline Commuting," Interfaces, Vol. 12, No. 1, pp. 85-87, 1982.

Murty, K., Network Programming, Prentice Hall, Upper Saddle River, NJ, 1992.

## Case Study: Scheduling Appointments at Australian Tourist Commission Trade Events ${}^{9}$ ^casestudy

Tools: Assignment model, heuristics

## Area of application: Tourism

## Description of the situation:

The Australian Tourist Commission (ATC) organizes trade events around the world to provide a forum for Australian sellers to meet international buyers of tourism products that include accommodation, tours, transport, and others. During these events, sellers are stationed in booths and are visited by buyers according to prescheduled appointments. Because of the limited time slots available in each event and the fact that the number of buyers and sellers can be quite large (one such event held in Melbourne in 1997 attracted 620 sellers and 700 buyers), ATC attempts to schedule the seller-buyer appointments in advance of the event in a manner that maximizes preferences. The idea is to match mutual interests to produce the most effective use of available time slots during the event.

## Analysis: ^threedim

The problem is viewed as a three-dimensional assignment model representing the buyers, the sellers, and the scheduled time slots. For an event with $m$ buyers, $n$ sellers, and $T$ time slots, define

$$
{x}_{ijt} = \left\{  \begin{array}{l} 1,\text{ if buyer }i\text{ meets with seller }j\text{ in period }t \\  0,\text{ otherwise } \end{array}\right.
$$

$$
{c}_{ij} = \text{ A score representing the mutual preferences of buyer }i\text{ and seller }j
$$

The associated assignment model can be expressed as

$$
\text{ Maximize }z = \mathop{\sum }\limits_{{i = 1}}^{m}\mathop{\sum }\limits_{{j = 1}}^{n}{c}_{ij}\left( {\mathop{\sum }\limits_{{t = 1}}^{T}{x}_{ijt}}\right)
$$

subject to

$$
\mathop{\sum }\limits_{{i = 1}}^{m}{x}_{ijt} \leq  1, j = 1,2,\ldots , n, t = 1,2,\ldots , T
$$

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{x}_{ijt} \leq  1, i = 1,2,\ldots , m, t = 1,2,\ldots , T
$$

$$
\mathop{\sum }\limits_{{t = 1}}^{T}{x}_{ijt} \leq  1, i = 1,2,\ldots , m, j = 1,2,\ldots , n
$$

$$
{x}_{ijt} = \left( {0,1}\right) \text{ for all }i, j\text{ , and }t
$$

The model expresses the basic restrictions of an assignment model: Each buyer or seller can meet at most one person per session, and a specific buyer-seller meeting can take place in at most one session. In the objective function, the coefficients ${c}_{ij}$ -representing the buyer-seller preferences for meetings-are not session dependent, the assumption being that buyers and sellers are indifferent to session time.

---

${}^{9}$ A. T. Ernst, R. G. J. Mills, and P. Welgama,“Scheduling Appointments at Trade Events for the Australian Tourist Commission," Interfaces, Vol. 33, No. 3, pp. 12-23, 2003.

---

How are the coefficients ${c}_{ij}$ determined? Following the registration of all buyers and sellers, each seller provides ATC with a prioritized list of buyers whom the seller wants to see. A similar list is demanded of each buyer with respect to sellers. The list assigns the value 1 to the top choice, with larger values implying lower preferences. These lists need not be exhaustive, in the sense that sellers and buyers are free to express interest in meeting with some but not all registered counterparts. For example, in a list with 100 sellers, a buyer may seek meetings with 10 sellers only, in which case the expressed preferences will be $1,2,\ldots ,{10}$ for the selected sellers.

The raw data gathered from the buyers/sellers list may then be expressed algebraically as

${b}_{ij} =$ ranking assigned by buyer $i$ to a meeting with seller $j \; {s}_{ji} =$ ranking assigned by seller $j$ to a meeting with buyer $i \; B =$ maximum number of preferences elected by all buyers $S =$ maximum number of preferences elected by all sellers $\alpha  =$ relative weight of buyer preferences (in calculating scores ${c}_{ij}$ ), $0 < \alpha  < 1 \; 1 - \alpha  =$ relative weight of seller preferences.

From these definitions, the objective coefficients ${c}_{ij}$ can be calculated as ^preference

$$
{c}_{ij} = \left\{  \begin{array}{ll} 1 + \alpha \left( \frac{B - {b}_{ij}}{B}\right)  + \left( {1 - \alpha }\right) \left( \frac{S - {s}_{ji}}{S}\right) , & \text{ if }{b}_{ij} \neq  0\text{ and }{s}_{ji} \neq  0 \\  1 + \alpha \left( \frac{B - {b}_{ij}}{B}\right) , & \text{ if }{b}_{ij} \neq  0\text{ and }{s}_{ji} = 0 \\  1 + \left( {1 - \alpha }\right) \left( \frac{S - {s}_{ji}}{S}\right) , & \text{ if }{b}_{ij} = 0\text{ and }{s}_{ji} \neq  0 \\  0, & \text{ if }{b}_{ij} = {s}_{ji} = 0 \end{array}\right.
$$

The logic behind these formulas is that a smaller value of ${b}_{ij}$ means a higher value of $\left( {B - {b}_{ij}}\right)$ and, hence, a higher score assigned to a requested meeting between buyer $i$ and seller $j$ . A similar interpretation is given to the score $S - {s}_{ji}$ for seller $j$ ’s requested meeting with buyer $i$ . Both scores are normalized to values between 0 and 1 by dividing them by $B$ and $S$ , respectively, and then are weighted by $\alpha$ and $1 - \alpha$ to reflect the relative importance of the buyer and seller preferences, $0 < \alpha  < 1$ , with values of $\alpha$ less than .5 favoring sellers’ preferences. Note that ${b}_{ij} = 0$ and ${s}_{ji} = 0$ indicate that no meetings are requested between buyer $i$ and seller $j$ . The quantity 1 appears in the top three formulas of ${c}_{ij}$ to give it a relatively larger preference than the case where no meetings are requested (i.e., ${b}_{ij} = {s}_{ji} = 0$ ). The normalization of the raw scores ensures that $0 \leq  {c}_{ij} < 2$ .

## Reliability of input data: ^reliability

A crucial issue in the present situation is the reliability of the preference data provided by buyers and sellers. A preference collection tool is devised to guarantee that the following restrictions are observed:

1. Lists of buyers and sellers are made available only after the registration deadline has passed.

2. Only registered buyers and sellers can participate in the process.

3. Participants' preferences are kept confidential by ATC. They may not be seen or altered by other participants.

Under these restrictions, an interactive Internet site is created to allow participants to enter their preferences conveniently. More importantly, the design of the site ensures valid input data. For example, the system prevents a buyer from seeking more than one meeting with the same seller, and vice versa.

## Solution of the problem: ^casesolution

The given assignment model is straightforward and can be solved by available LP packages. File amplCase3a.txt and file amplCase3b.txt provide two AMPL models for this situation. The data for the two models are given in a spreadsheet format (file excelCase3.xls). In the first model, the spreadsheet is used to calculate the coefficients ${c}_{ij}$ , which are then used as input data. In the second model, the raw preference scores, ${b}_{ij}$ and ${s}_{ji}$ , are the input data and the model itself calculates the coefficients ${c}_{ij}$ . The advantage of the second is that it allows computing the percentages of buyer and seller satisfaction regarding their expressed preferences.

The output of model amplCase3b.txt for the data in file excelCase3.xls (6 buyers, 7 sellers, and 6 sessions) is given in Figure 5.5. It provides the assignment of buyers to sellers within each session as well as the percent satisfaction for each buyer and seller for a weight factor $\alpha  = {.5}$ . The results show high buyer and seller satisfactions (92% and 86%, respectively). If $\alpha  < {.5}$ , seller satisfaction will increase.

## Practical considerations: ^walking

For the solution of the assignment model to be realistic, it must take into consideration the delays between successive appointments. Essentially, a buyer, once through with an appointment, will most likely have to move to another cubical for the next appointment. A feasible schedule must thus account for the transition time between successive appointments. The following walking constraints achieve this result:

$$
{x}_{ijt} + \mathop{\sum }\limits_{{k \in  {J}_{i}}}{x}_{i, k, t + 1} = 1, i = 1,\ldots , m, j = 1,\ldots , n, t = 1,\ldots , T
$$

The set ${J}_{i}$ represents the sellers buyer $i$ cannot reach in period $t + 1$ without experiencing undue delay. The logic is that if buyer $i$ has an appointment with seller $j$ in period $t\left( {{x}_{ijt} = 1}\right)$ , then the same buyer may not schedule a next-period $\left( {t + 1}\right)$ appointment with seller $k$ who cannot be reached without delay (i.e., ${x}_{i, k, t + 1} = 0$ ). We can reduce the number of such constraints by eliminating period $t$ that occurs at the end of a session block (e.g., coffee breaks, lunch break, and end of day).

The additional constraints increase the computational difficulty of the model considerably. In fact, the model may not be solvable as an integer linear program considering the computational limitations of present-day IP algorithms. This is the reason a heuristic is needed to determine a "good" solution for the problem.

The heuristic used to solve the new restricted model is summarized as follows: ^heuristic

For each period $t$

1. Set ${x}_{ijt} = 0$ if the location of buyer $i$ ’s last meeting in period $t - 1$ does not allow reaching seller $j$ in period $t$ .

2. Set ${x}_{ijt} = 0$ if a meeting between $i$ and $j$ has been prescheduled.

3. Solve the resulting two-dimensional assignment model.

Next $t$

The quality of the heuristic solution can be measured by comparing its objective value (preference measure) with that of the original assignment model (with no walking constraints). ^quality
Reported

Case Study: Scheduling Appointments at Australian Tourist Commission Trade Events 235

---

										Optimal score = 50.87

										Optimal assignments:

										Session 1:

											Assign buyer 1 to seller 1

											Assign buyer 2 to seller 5

											Assign buyer 3 to seller 4

											Assign buyer 4 to seller 6

											Assign buyer 5 to seller 2

											Assign buyer 6 to seller 7

										Session 2:

											Assign buyer 1 to seller 3

											Assign buyer 2 to seller 6

											Assign buyer 3 to seller 5

											Assign buyer 4 to seller 2

											Assign buyer 5 to seller 1

											Assign buyer 6 to seller 4

										Session 3:

											Assign buyer 1 to seller 2

											Assign buyer 2 to seller 4

											Assign buyer 3 to seller 6

											Assign buyer 4 to seller 5

											Assign buyer 5 to seller 3

											Assign buyer 6 to seller 1

										Session 4:

											Assign buyer 1 to seller 5

											Assign buyer 2 to seller 3

											Assign buyer 3 to seller 1

											Assign buyer 4 to seller 7

											Assign buyer 5 to seller 4

											Assign buyer 6 to seller 2

										Session 5:

											Assign buyer 2 to seller 2

											Assign buyer 3 to seller 3

											Assign buyer 4 to seller 4

											Assign buyer 5 to seller 5

											Assign buyer 6 to seller 6

										Session 6:

											Assign buyer 1 to seller 4

											Assign buyer 2 to seller 7

											Assign buyer 3 to seller 2

											Assign buyer 4 to seller 1

											Assign buyer 5 to seller 6

											Assign buyer 6 to seller 5

										Buyers satisfaction: Average = 92

| Buyer | 1 | 2 | 3 | 4 | 5 | 6 |
|------|---|---|---|---|---|---|
| Percent | 100 | 86 | 100 | 80 | 86 | 100 |

										Sellers satisfaction: Average = 86

											Seller: 1 2 3 4 5 6 																																		FIGURE 5.5

										Percent: 83100 60 100 100 100 60

---

results show that for five separate events the gap between the two solutions was less than 10%, indicating that the heuristic provides reliable solutions.

Of course, the devised solution does not guarantee that all preferences will be met because of the limit on the available number of time slots. Interestingly, the results recommended by the heuristic show that at least 80% of the highest-priority meetings (with preference 1) are selected by the solution. This percentage declines almost linearly with the increase in expressed scores (higher score indicates lower preference).

## PROBLEMS10 ^problems

| Section | Assigned Problems |
|---------|------------------|
| 5.1     | 5-1 to 5-13       |
| 5.2     | 5-14 to 5-21      |
| 5.3.1   | 5-22              |
| 5.3.2   | 5-23 to 5-29      |
| 5.3.3   | 5-30 to 5-31      |
| 5.4.1   | 5-32 to 5-38      |

5-1. True or False?

(a) To balance a transportation model, it is necessary to add a dummy source or a dummy destination bur never both.

(b) The amounts shipped to a dummy destination represent surplus at the shipping source.

(c) The amounts shipped from a dummy source represent shortages at the receiving destinations.

5-2. In each of the following cases, determine whether a dummy source or a dummy destination must be added to balance the model.

(a) Supply: ${a}_{1} = {100},{a}_{2} = {50},{a}_{3} = {40},{a}_{4} = {60}$ Demand: ${b}_{1} = {100},{b}_{2} = {50},{b}_{3} = {70},{b}_{4} = {90}$

(b) Supply: ${a}_{1} = {15},{a}_{2} = {44}$

Demand: ${b}_{1} = {25},{b}_{2} = {15},{b}_{3} = {10}$

5-3. In Table 5.4 of Example 5.1-2, where a dummy plant is added, what does the solution mean when the dummy plant "ships" 150 cars to Denver and 50 cars to Miami?

*5-4. In Table 5.5 of Example 5.1-2, where a dummy destination is added, suppose that the Detroit plant must ship out all its production. How can this restriction be implemented in the model?

5-5. In Example 5.1-2, suppose that for the case where the demand exceeds the supply (Table 5.4), a penalty is levied at the rate of \$300 and \$190 for each undelivered car at Denver and Miami, respectively. Additionally, no deliveries are made from the Los Angeles plant to the Miami distribution center. Set up the model, and determine the optimal shipping schedule for the problem.

*5-6. Three electric power plants with capacities of 25,40, and 30 million kWh supply electricity to three cities. The maximum demands at the three cities are estimated at 30, 35, and 25 million kWh. The price per million kWh at the three cities is given in Table 5.25.

---

${}^{10}$ You may use TORA where appropriate to find the optimum solution. AMPL and Solver models are introduced at the end of Section 5.3.2.

---

TABLE 5.25 Price/Million kWh for Problem 5-6

| Plant | City 1 | City 2 | City 3 |
|------|--------|--------|--------|
| 1    | \$600  | \$700  | \$400  |
| 2    | \$320  | \$300  | \$350  |
| 3    | \$500  | \$480  | \$450  |

During the month of August, there is a 20% increase in demand at each of the three cities, which can be met by purchasing electricity from another network at a premium rate of \$1000 per million kWh. The network is not linked to city 3 , however. The utility company wishes to determine the most economical plan for the distribution and purchase of additional energy.

(a) Formulate the problem as a transportation model.

(b) Determine an optimal distribution plan for the utility company.

(c) Determine the cost of the additional power purchased by each of the three cities.

5-7. Solve Problem 5-6, assuming that there is a 10% power transmission loss through the network.

5-8. Three refineries with daily capacities of 6, 5, and 8 million gallons, respectively, supply three distribution areas with daily demands of 4, 8, and 7 million gallons, respectively. Gasoline is transported to the three distribution areas through a network of pipelines. The transportation cost is 10 cents per 1000 gallons per pipeline mile. Table 5.26 gives the mileage between the refineries and the distribution areas. Refinery 1 is not connected to distribution area 3.

(a) Construct the associated transportation model.

(b) Determine the optimum shipping schedule in the network.

*5-9. In Problem 5-8, suppose that the capacity of refinery 3 is 6 million gallons only and that distribution area 1 must receive all its demand. Additionally, any shortages at areas 2 and 3 will incur a penalty of 5 cents per gallon.

(a) Formulate the problem as a transportation model.

(b) Determine the optimum shipping schedule.

5-10. In Problem 5-8, suppose that the daily demand at area 3 drops to 4 million gallons. Surplus production at refineries 1 and 2 is diverted to other distribution areas by truck. The transportation cost per 100 gallons is \$1.50 from refinery 1 and \$2.20 from refinery 2. Refinery 3 can divert its surplus production to other chemical processes within the plant.

(a) Construct the associated transportation model.

(b) Determine the optimum shipping schedule in the network.

TABLE 5.26 Mileage Chart for Problem 5-8

|             | Distribution area 1 | Distribution area 2 | Distribution area 3 |
|-------------|----------------------|----------------------|----------------------|
| Refinery 1  | 180                  | 180                  | -                    |
| Refinery 2  | 300                  | 800                  | 900                  |
| Refinery 3  | 220                  | 200                  | 120                  |

5-11. Three orchards supply crates of oranges to four retailers. The daily demand amounts at the four retailers are 150, 150, 400, and 100 crates, respectively. Supplies at the three orchards are dictated by available regular labor and are estimated at 150, 200, and 250 crates daily. However, both orchards 1 and 2 have indicated that they could supply more crates, if necessary, by using overtime labor. Orchard 3 does not offer this option. The transportation costs per crate from the orchards to the retailers are given in Table 5.27.

(a) Formulate the problem as a transportation model.

(b) Solve the problem.

(c) How many crates should orchards 1 and 2 supply using overtime labor?

5-12. Cars are shipped from three distribution centers to five dealers. The shipping cost is based on the mileage between the sources and the destinations and is independent of whether the truck makes the trip with partial or full loads. Table 5.28 summarizes the mileage between the distribution centers and the dealers together with the monthly supply and demand figures given in number of cars. A full truckload includes 18 cars. The transportation cost per truck mile is \$25.

(a) Formulate the associated transportation model.

(b) Determine the optimal shipping schedule.

5-13. MG Auto, of Example 5.1-1, produces four car models: M1, M2, M3, and M4. The Detroit plant produces models ${M1},{M2}$ , and ${M4}$ . Models ${M1}$ and ${M2}$ are also produced in New Orleans. The Los Angeles plant manufactures models ${M3}$ and ${M4}$ . The capacities of the various plants and the demands at the distribution centers are given in Table 5.29.

The mileage chart is the same as given in Example 5.1-1, and the transportation rate remains at 8 cents per car mile for all models. Additionally, it is possible to satisfy a percentage of the demand for some models from the supply of others according to the specifications in Table 5.30.

(a) Formulate the corresponding transportation model.

(b) Determine the optimum shipping schedule. (Hint: Add four new destinations corresponding to the new combinations $\left\lbrack  {{M1},{M2}}\right\rbrack  ,\left\lbrack  {{M3},{M4}}\right\rbrack  ,\left\lbrack  {{M1},{M3}}\right\rbrack$ , and $\left\lbrack  {{M2},{M4}}\right\rbrack$ . The demands at the new destinations are determined from the given percentages.)

TABLE 5.27 Transportation Cost/Crate for Problem 5-11

|           | Retailer 1 | Retailer 2 | Retailer 3 | Retailer 4 |
|-----------|------------|------------|------------|------------|
| Orchard 1 | \$1        | \$2        | \$3        | \$2        |
| Orchard 2 | \$2        | \$4        | \$1        | \$2        |
| Orchard 3 | \$1        | \$3        | \$5        | \$3        |

TABLE 5.28 Mileage Chart and Supply and Demand for Problem 5-12

|          | Dealer 1 | Dealer 2 | Dealer 3 | Dealer 4 | Dealer 5 | Supply |
|----------|----------|----------|----------|----------|----------|--------|
| Center 1 | 100      | 150      | 200      | 140      | 35       | 400    |
| Center 2 | 50       | 70       | 60       | 65       | 80       | 200    |
| Center 3 | 40       | 90       | 100      | 150      | 130      | 150    |
| Demand   | 100      | 200      | 150      | 160      | 140      |        |

TABLE 5.29 Capacities and Demands for Problem 5-13

**Plant capacities**

| Plant | ${M1}$ | ${M2}$ | ${M3}$ | ${M4}$ | Totals |
|------|--------|--------|--------|--------|--------|
| Los Angeles  | -   | -   | 700 | 300 | 1000 |
| Detroit      | 500 | 600 | -   | 400 | 1500 |
| New Orleans  | 800 | 400 | -   | -   | 1200 |

**Distribution center demands**

| Distribution center | ${M1}$ | ${M2}$ | ${M3}$ | ${M4}$ | Totals |
|---------------------|--------|--------|--------|--------|--------|
| Denver | 700 | 500 | 500 | 600 | 2300 |
| Miami  | 600 | 500 | 200 | 100 | 1400 |

TABLE 5.30 Interchangeable Models for Problem 5-13

| Distribution center | Percentage of demand | Interchangeable models |
|---------------------|----------------------|------------------------|
| Denver              | 10                   | M1, M2                 |
| Denver              | 20                   | M3, M4                 |
| Miami               | 10                   | M1, M3                 |
| Miami               | 5                    | M2, M4                 |

5-14. In Example 5.2-1, suppose that the holding cost per unit is period-dependent and is given by 20,15, and 35 cents for periods 1, 2, and 3, respectively. The penalty cost is \$1 per period and the production costs remain as given in the example. Determine the optimum solution and interpret the results.

*5-15. In Example 5.2-2, suppose that the sharpening service offers 3-day service for \$1 a blade on Monday and Tuesday (days 1 and 2). Reformulate the problem, and interpret the optimum solution.

5-16. In Example 5.2-2, if a blade is not used the day it is sharpened, a holding cost of 50 cents per blade per day is incurred. Reformulate the model, and interpret the optimum solution.

5-17. JoShop wants to assign four different categories of machines to five types of tasks. The numbers of machines available in the four categories are 25, 30, 20, and 30 . The numbers of jobs in the five tasks are30,10,20,25, and 20 . Machine category 4 cannot be assigned to task type 4. Table 5.31 provides the unit cost (in dollars) of assigning a machine category to a task type. The objective of the problem is to determine the optimum number of machines in each category to be assigned to each task type. Solve the problem and interpret the solution.

TABLE 5.31 Unit Costs for Problem 5-17

| Machine category | Task 1 | Task 2 | Task 3 | Task 4 | Task 5 |
|------------------|--------|--------|--------|--------|--------|
| 1                | 10     | 2      | 3      | 15     | 9      |
| 2                | 5      | 10     | 15     | 2      | 4      |
| 3                | 15     | 5      | 14     | 7      | 15     |
| 4                | 20     | 15     | 13     | -      | 8      |

*5-18. The demand for a perishable item over the next four months is 400, 300, 420, and 380 tons, respectively. The supply capacities for the same months are 500, 600, 200, and 300 tons. The purchase price per ton varies from month to month and is estimated at \$100, \$140, \$120, and \$150, respectively. Because the item is perishable, a current month's supply must be consumed within 3 months (starting with current month). The storage cost per ton per month is \$3. The nature of the item does not allow back-ordering. Solve the problem as a transportation model, and determine the optimum delivery schedule for the item over the next 4 months.

5-19. The demand for a special small engine over the next five quarters is200,150,300,250, and 400 units, respectively. The manufacturer supplying the engine has different production capacities estimated at 180, 230, 430, 300, and 300 for the five quarters. Back-ordering is not allowed, but the manufacturer may use overtime to fill the immediate demand, if necessary. The overtime capacity for each period is half the regular capacity. The production costs per unit for the five periods are $\$ {100},\$ {96},\$ {116},\$ {102}$ , and $\$ {106}$ , respectively. The overtime production cost per engine is 50% higher than the regular production cost. If an engine is produced now for use in later periods, an additional storage cost of \$4 per engine per period is incurred. Formulate the problem as a transportation model. Determine the optimum number of engines to be produced during regular time and overtime of each period.

5-20. Periodic preventive maintenance is carried out on aircraft engines, where an important component must be replaced. The numbers of aircraft scheduled for such maintenance over the next six months are estimated at200,180,300,198,230, and 290, respectively. All maintenance work is done during the first day of the month, where a used component may be replaced with a new or an overhauled component. The overhauling of used components may be done in a local repair facility, where they will be ready for use at the beginning of next month, or they may be sent to a central repair shop, where a delay of 3 months (including the month in which maintenance occurs) is expected. The repair cost in the local shop is \$120 per component. At the central facility, the cost is only \$35 per component. An overhauled component used in a later month will incur an additional storage cost of \$1.50 per unit per month. New components may be purchased at \$200 each in month 1, with a 5% price increase every 2 months. Formulate the problem as a transportation model, and determine the optimal schedule for satisfying the demand for the component over the next six months.

5-21. The National Parks Service is receiving four bids for logging at three pine forests in Arkansas. The three locations include 20,000,30,000, and 10,000 acres. A single bidder can bid for at most 50% of the total acreage available. The bids per acre at the three locations are given in Table 5.32. Bidder 2 does not wish to bid on location 1, and bidder 3 cannot bid on location 2.

(a) In the present situation, we need to maximize the total bidding revenue for the Parks Service. Show how the problem can be formulated as a transportation model.

(b) Determine the acreage that should be assigned to each of the four bidders.

TABLE 5.32 Bids per Acre for Problem 5-21

| Bidder | Location 1 | Location 2 | Location 3 |
|--------|------------|------------|------------|
| 1      | \$520      | \$210      | \$570      |
| 2      | -          | \$510      | \$495      |
| 3      | \$650      | -          | \$240      |
| 4      | \$180      | \$430      | \$710      |

TABLE 5.33 Data for Problem 5-22

| (a)      |   | (b) |   |   |   | (c) |   |   |
|----------|---|-----|---|---|---|-----|---|---|
| 0 2 1 6  | 1 | 2   | 6 | 7 | 5 | 1   | 8 | 12 |
| 2 1 5 7  | 0 | 4   | 2 | 12 | 2 | 4 | 0 | 14 |
| 2 4 3 7  | 3 | 1   | 5 | 11 | 3 | 6 | 7 | 4 |
| 5 5 10   | 10 | 10 | 10 |   | 9 | 10 | 11 |   |

TABLE 5.34 Transportation Models for Problem 5-23

![bo_d56m4e77aajc73800n7g_34_516_623_1019_248_0.jpg](bo_d56m4e77aajc73800n7g_34_516_623_1019_248_0.jpg)

5-22. Compare the starting solutions obtained by the northwest-corner, least-cost, and Vogel methods for each of the models in Table 5.33.

5-23. Consider the transportation models in Table 5.34.

(a) Use the northwest-corner method to find the starting solution.

(b) Develop the iterations that lead to the optimum solution.

(c) TORA Experiment. Use TORA's Iterations module to compare the effect of using the northwest-corner rule, least-cost method, and Vogel method on the number of iterations leading to the optimum solution.

(d) Solver Experiment. Solve the problem by modifying file solverEx5.3-1.xls.

(e) AMPL Experiment. Solve the problem by modifying file amplEx5.3-1b.txt.

5-24. In the transportation problem in Table 5.35, the total demand exceeds the total supply. Suppose that the penalty costs per unit of unsatisfied demand are \$2, \$5, and \$3 for destinations 1, 2, and 3, respectively. Use the least-cost starting solution and compute the iterations leading to the optimum solution.

5-25. Solve Problem 5-24, assuming that the demand at destination 1 must be satisfied completely.

(a) Find the optimal solution.

(b) Solver Experiment. Solve the problem by modifying file solverEx5.3-1.xls.

(c) AMPL Experiment. Solve the problem by modifying file amplEx5.3-1b.txt.

5-26. In the unbalanced transportation problem in Table 5.36, if a unit from a source is not shipped out (to any of the destinations), a storage cost is incurred at the rate of \$5, \$4, and \$3 per unit for sources 1, 2, and 3, respectively. Additionally, all the supply at source 2 must be shipped out completely to make room for a new product. Use Vogel's starting solution, and determine all the iterations leading to the optimum shipping schedule.

![bo_d56m4e77aajc73800n7g_34_781_1895_481_266_0.jpg](bo_d56m4e77aajc73800n7g_34_781_1895_481_266_0.jpg)

![bo_d56m4e77aajc73800n7g_35_740_205_480_274_0.jpg](bo_d56m4e77aajc73800n7g_35_740_205_480_274_0.jpg)

*5-27. In a $3 \times  3$ transportation problem, let ${x}_{ij}$ be the amount shipped from source $i$ to destination $j$ , and let ${c}_{ij}$ be the corresponding transportation cost per unit. The amounts of supply at sources 1, 2, and 3 are 15, 30, and 85 units, respectively, and the demands at destinations 1, 2, and 3 are 20, 30, and 80 units, respectively. Assume that the starting northwest-corner solution is optimal and that the associated values of the multipliers are given as ${u}_{1} =  - 2,{u}_{2} = 3,{u}_{3} = 5,{v}_{1} = 2,{v}_{2} = 5$ , and ${v}_{3} = {10}$ .

(a) Find the associated optimal cost.

(b) Determine the smallest value of ${c}_{ij}$ for each nonbasic variable that will maintain the optimality of the northwest-corner solution.

5-28. The transportation problem in Table 5.37 gives the indicated degenerate basic solution (i.e., at least one of the basic variables is zero). Suppose that the multipliers associated with this solution are ${u}_{1} = 1,{u}_{2} =  - 1,{v}_{1} = 2,{v}_{2} = 2$ , and ${v}_{3} = 5$ and that the unit cost for all (basic and nonbasic) zero ${x}_{ij}$ variables is given by

$$
{c}_{ij} = i + {j\theta }, - \infty  < \theta  < \infty
$$

(a) If the given solution is optimal, determine the associated optimal value of the objective function.

(b) Determine the value of $\theta$ that will guarantee the optimality of the given solution. (Hint: Locate the zero basic variable.)

5-29. Consider the problem

$$
\text{ Minimize }z = \mathop{\sum }\limits_{{i = 1}}^{m}\mathop{\sum }\limits_{{j = 1}}^{n}{c}_{ij}{x}_{ij}
$$

subject to

$$
\mathop{\sum }\limits_{{j = 1}}^{n}{x}_{ij} \geq  {a}_{i}, i = 1,2,\ldots , m
$$

$$
\mathop{\sum }\limits_{{i = 1}}^{m}{x}_{ij} \geq  {b}_{j}, j = 1,2,\ldots , n
$$

$$
{x}_{ij} \geq  0\text{ , all }i\text{ and }j
$$

TABLE 5.37 Data for Problem 5-28

| 1  | 2  | 3  | Notes |
|----|----|----|-------|
| 10 |    |    | 10<br>40 |
|    | 20 | 20 |       |
| 10 | 20 | 20 |       |

![bo_d56m4e77aajc73800n7g_36_713_202_480_243_0.jpg](bo_d56m4e77aajc73800n7g_36_713_202_480_243_0.jpg)

It may appear logical to assume that the optimum solution will require the first (second) set of inequalities to be replaced with equations if $\sum {a}_{i} \geq  \sum {b}_{j}\left( {\sum {a}_{i} \leq  \sum {b}_{j}}\right)$ . The counterexample in Table 5.38 shows that this assumption is not correct.

Show that the application of the suggested procedure yields the solution ${x}_{11} = 2,{x}_{12} = 3,{x}_{22} = 4$ , and ${x}_{23} = 2$ , with $z = \$ {27}$ , which is worse than the feasible solution ${x}_{11} = 2,{x}_{12} = 7$ , and ${x}_{23} = 6$ , with $z = \$ {15}$ .

5-30. Write the dual problem for the LP of the transportation problem in Example 5.3-5 (Table 5.21). Compute the associated optimum dual objective value using the optimal dual values given in Table 5.25, and show that it equals the optimal cost given in the example.

5-31. In the transportation model, one of the dual variables assumes an arbitrary value. This means that for the same basic solution, the values of the associated dual variables are not unique. The result appears to contradict the theory of linear programming, where the dual values are determined as the product of the vector of the objective coefficients for the basic variables and the associated inverse basic matrix (see Method 2, Section 4.2.3). Show that for the transportation model, although the inverse basis is unique, the vector of basic objective coefficients need not be so. Specifically, show that if ${c}_{ij}$ is changed to ${c}_{ij} + k$ for all $i$ and $j$ , where $k$ is a constant, then the optimal values of ${x}_{ij}$ will remain the same. Hence, the use of an arbitrary value for a dual variable is implicitly equivalent to assuming that a specific constant $k$ is added to all ${c}_{ij}$ .

5-32. Consider the assignment models in Table 5.39.

(a) Solve by the Hungarian method.

(b) TORA Experiment. Express the problem as an LP, and solve it with TORA.

(c) TORA Experiment. Use TORA to solve the problem as a transportation model.

(d) Solver Experiment. Modify Excel file solverEx5.3-1.xls to solve the problem.

(e) AMPL Experiment. Modify file amplEx5.3b-1.txt to solve the problem.

5-33. JoShop needs to assign four jobs to four workers. The cost of performing a job is a function of the skills of the workers. Table 5.40 summarizes the cost of the assignments. Worker 1 cannot do job 3, and worker 3 cannot do job 4. Determine the optimal assignment using the Hungarian method.

TABLE 5.39 Data for Problem 5-32

| (i) |  |  |  |  | (ii) |  |  |  |  |
|-----|---|---|---|---|------|---|---|---|---|
| \$3 | \$8 | \$2 | \$10 | \$3 | \$3 | \$9 | \$2 | \$2 | \$7 |
| \$6 | \$5 | \$2 | \$7  | \$5 | \$6 | \$1 | \$5 | \$6 | \$6 |
| \$6 | \$4 | \$2 | \$7  | \$5 | \$9 | \$4 | \$7 | \$10 | \$3 |
| \$8 | \$4 | \$2 | \$3  | \$5 | \$2 | \$5 | \$4 | \$2  | \$1 |
| \$7 | \$8 | \$6 | \$7  | \$7 | \$9 | \$6 | \$2 | \$4  | \$6 |

TABLE 5.40 Data for Problem 5-33

| Worker | Job 1 | Job 2 | Job 3 | Job 4 |
|--------|-------|-------|-------|-------|
| 1      | \$50  | \$50  | -     | \$20  |
| 2      | \$70  | \$40  | \$20  | \$30  |
| 3      | \$90  | \$30  | \$50  | -     |
| 4      | \$70  | \$20  | \$60  | \$70  |

5-34. In the JoShop model of Problem 5-33, suppose that an additional (fifth) worker becomes available for performing the four jobs at the respective costs of \$60, \$45, \$30, and \$80. Is it economical to replace one of the current four workers with the new one?

5-35. In the model of Problem 5-33, suppose that JoShop has just received a fifth job and that the respective costs of performing it by the four current workers are \$20, \$10, \$20, and \$80. Moreover, job 1 cannot be displaced by the newly arriving job. Should the new job take priority over any of the four jobs JoShop already has?

*5-36. A business executive must make the four round-trips listed in Table 5.41 between the head office in Dallas and a branch office in Atlanta.

The price of a round-trip ticket from Dallas is \$400. A 25% discount is granted if the dates of arrival and departure of a ticket span a weekend (Saturday and Sunday). If the stay in Atlanta lasts more than 21 days, the discount is increased to 30%. A one-way ticket between Dallas and Atlanta (either direction) costs \$250. How should the executive purchase the tickets?

*5-37. Figure 5.6 gives a schematic layout of a machine shop with its existing work centers designated by squares 1, 2, 3, and 4. Four new work centers, I, II, III, and IV, are to be added to the shop at the locations designated by circles $a, b, c$ , and $d$ . The objective is to assign the new centers to the proposed locations to minimize the total materials handling traffic between the existing centers and the proposed ones. Table 5.42 summarizes the frequency of trips between the new centers and the old ones. Materials handling equipment travels along the rectangular aisles intersecting at the locations of the centers. For example, the one-way travel distance (in meters) between center 1 and location $b$ is ${30} + {20} = {50}\mathrm{\;m}$ .

5-38. In the Industrial Engineering Department at the University of Arkansas, INEG 4904 is a capstone design course intended to allow teams of students to apply the knowledge and skills learned in the undergraduate curriculum to a practical problem. The members of each team select a project manager, identify an appropriate scope for their project, write and present a proposal, perform necessary tasks for meeting the project objectives, and write and present a final report. The course instructor identifies potential projects and provides appropriate information sheets for each, including contact at the sponsoring organization, project summary, and potential skills needed to complete the project.

TABLE 5.41 Data for Problem 5-36

| Departure date from Dallas | Return date to Dallas |
|----------------------------|-----------------------|
| Monday, June 3             | Friday, June 7        |
| Monday, June 10            | Wednesday, June 12    |
| Monday, June 17            | Friday, June 21       |
| Tuesday, June 25           | Friday, June 28       |

![bo_d56m4e77aajc73800n7g_38_485_199_980_859_0.jpg](bo_d56m4e77aajc73800n7g_38_485_199_980_859_0.jpg)

FIGURE 5.6

Machine shop layout for Problem 5-37

TABLE 5.42 Data for Problem 5-37

| Existing center | New center I | New center II | New center III | New center IV |
|----------------|--------------|---------------|----------------|---------------|
| 1              | 10           | 2             | 4              | 3             |
| 2              | 7            | 1             | 9              | 5             |
| 3              | 0            | 8             | 6              | 2             |
| 4              | 11           | 4             | 0              | 7             |

Each design team is required to submit a report justifying the selection of team members and the team manager. The report also provides a ranking for each project in order of preference, including justification regarding proper matching of the team's skills with the project objectives. In a specific semester, the following projects were identified: Boeing F-15, Boeing F-18, Boeing Simulation, Cargil, Cobb-Vantress, ConAgra, Cooper, DaySpring (layout), DaySpring (material handling), J. B. Hunt, Raytheon, Tyson South, Tyson East, Walmart, and Yellow Transportation. The projects for Boeing and Raytheon require U.S. citizenship of all team members. Of the 11 design teams available for this semester, four do not meet this requirement.

Devise a procedure for assigning projects to teams, and justify the arguments you use to reach a decision.

This page intentionally left blank
