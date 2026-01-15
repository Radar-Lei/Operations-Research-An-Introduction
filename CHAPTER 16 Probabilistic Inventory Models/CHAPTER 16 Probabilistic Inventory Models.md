## CHAPTER 16 Probabilistic Inventory Models

## Real-Life Application—Inventory Decisions in Dell's Supply Chain

Dell, Inc., implements a direct-sales business model in which personal computers are sold directly to customers in the United States. When an order arrives from a customer, the specifications are sent to a manufacturing plant in Austin, Texas, where the computer is built, tested, and packaged in about 8 hours. Dell carries little inventory. Its suppliers, normally located in Southeast Asia, are required to keep what is known as "revolving" inventory on hand in revolvers (warehouses) near the manufacturing plants. These revolvers are owned by Dell and leased to the suppliers. Dell then "pulls" parts as needed from the revolvers, and it is the suppliers' responsibility to replenish the inventory to meet Dell's demand. Although Dell does not own the inventory in the revolvers, its cost is indirectly passed on to customers through component pricing. Thus, any reduction in inventory directly benefits Dell's customers by reducing product prices. The proposed solution has resulted in an estimated \$2.7 million in annual savings. Case 14 in Chapter 26 on the website provides the details.

### 16.1 CONTINUOUS REVIEW MODELS

This section presents two models: (1) a "probabilitized" version of the deterministic EOQ (Section 13.3.1) that uses a buffer stock to account for probabilistic demand and (2) a more exact probabilistic EOQ model that includes the random demand directly in the formulation.

#### 16.1.1 "Probabilitized" EOQ Model

Some practitioners have sought to adapt the deterministic EOQ model (Section 13.3.1) to approximate the probabilistic nature of demand. The critical period during the inventory cycle occurs between placing and receiving orders. This is the time period when shortage (running out of stock) could occur. The idea then is to maintain a constant buffer stock that will put a cap on the probability of shortage. Intuitively, lower shortage probability entails larger buffer stock, and vice versa.

![bo_d56m5dbef24c73bhe66g_1_433_202_1017_544_0.jpg](bo_d56m5dbef24c73bhe66g_1_433_202_1017_544_0.jpg)

FIGURE 16.1

Buffer stock, $B$ , imposed on the classical EOQ model

Figure 16.1 depicts the relationship between the buffer stock, $B$ , and the parameters of the deterministic EOQ model that include the lead time, $L$ ; the average demand during lead time, ${\mu }_{L}$ ; and the EOQ, ${y}^{ * }$ . Note that $L$ is the effective lead time as defined in Section 13.3.1.

The main assumption of the model is that the demand per unit time is normal with mean $D$ and standard deviation $\sigma  -$ that is, $N\left( {D,\sigma }\right)$ . Under this assumption, the demand during lead time $L$ must also be normal with mean ${\mu }_{L} = {DL}$ and standard deviation ${\sigma }_{L} = \sqrt{L{\sigma }^{2}}$ . The formula for ${\sigma }_{L}$ assumes that $L$ is (approximated, if necessary, by) an integer value.

The size of the buffer $B$ is determined such that the probability of shortage during $L$ is at most $\alpha$ . Let ${x}_{L}$ be the demand during lead time $L$ , then

$$
P\left\{  {{x}_{L} \geq  B + {\mu }_{L}}\right\}   \leq  \alpha
$$

Using $N\left( {0,1}\right) , z = \frac{{x}_{L} - {\mu }_{L}}{{\sigma }_{L}}$ (as defined in Section 14.4.4), we get

$$
P\left\{  {z \geq  \frac{B}{{\sigma }_{L}}}\right\}   \leq  \alpha
$$

Figure 16.2 defines the parameter ${K}_{\alpha }$ for the standard normal distribution such that $P\left\{  {z \geq  {k}_{\alpha }}\right\}   \leq  \alpha$ . It follows that

$$
B \geq  {\sigma }_{L}{K}_{\alpha }
$$

The amount ${\sigma }_{L}{K}_{\alpha }$ provides the minimum value of $B$ . (The value of ${K}_{\alpha }$ can be determined from the standard normal table in Appendix A or by using file excelStatTables.xls.)

![bo_d56m5dbef24c73bhe66g_2_457_199_572_480_0.jpg](bo_d56m5dbef24c73bhe66g_2_457_199_572_480_0.jpg)

FIGURE 16.2

Probability of running out of stock, $P\left\{  {z \geq  {K}_{\alpha }}\right\}   = \alpha$

Example 16.1-1

In Example 13.3-1 dealing with determining the inventory policy of neon lights, the EOQ is 1000 units. Assume that the daily demand is $N\left( {{100},{10}}\right)$ -that is, $D = {100}$ units and standard deviation $\sigma  = {10}$ units. Determine the buffer size, $B$ , using $\alpha  = {.05}$ .

From Example 13.3-1, the effective lead time is $L = 2$ days. Thus,

$$
{\mu }_{L} = {DL} = {100} \times  2 = {200}\text{ units }
$$

$$
{\sigma }_{L} = \sqrt{{\sigma }^{2}L} = \sqrt{{10}^{2} \times  2} = {14.14}\text{ units }
$$

Given ${K}_{.05} = {1.645}$ , the buffer size is computed as

$$
B \geq  {14.14} \times  {1.645} \approx  {23}\text{ neon lights }
$$

The (buffered) optimal inventory policy calls for ordering 1000 units whenever the inventory level drops to ${223}\left( { = B + {\mu }_{L} = {23} + 2 \times  {100}}\right)$ units.

#### 16.1.2 Probabilistic EOQ Model

The basis for the development of the "probabilitized" EOQ model in Section 16.1.1 is "plausible," but there is no reason to believe that the model yields an optimal inventory policy. The fact that pertinent information regarding the probabilistic nature of demand is initially ignored, only to be "revived" in a totally independent manner at a later stage of the calculations, is sufficient to refute optimality. To remedy the situation, this section presents a more accurate model in which the probabilistic nature of the demand is included directly in the formulation of the model. Of course, higher accuracy comes at the expense of more complex computations.

Figure 16.3 depicts a typical change in inventory level with time. Shortage may or may not occur during (possibly random) lead times, as illustrated by cycles 1 and 2, respectively. The policy calls for ordering the quantity $y$ whenever the amount of inventory on hand drops to level $R$ . As in the deterministic case, the reorder level $R$ is a function of the lead time between placing and receiving an order. The optimal values of $y$ and $R$ are determined by minimizing the expected sum of setup, holding, and shortage costs per unit time.

![bo_d56m5dbef24c73bhe66g_3_348_199_817_429_0.jpg](bo_d56m5dbef24c73bhe66g_3_348_199_817_429_0.jpg)

FIGURE 16.3

Probabilistic inventory model with shortage

The model is based on three assumptions:

1. Unfilled demand during lead time is backlogged.

2. No more than one outstanding order is allowed.

3. The distribution of demand during lead time remains stationary with time.

To develop the total cost function per unit time, let

$$
f\left( x\right)  = \text{ pdf of demand, }x\text{ , during lead time }
$$

$D =$ Expected demand per unit time

$h =$ Holding cost per inventory unit per unit time

$$
p = \text{ Shortage cost per inventory unit }
$$

$K =$ Setup cost per order

The elements of the cost function are now determined.

1. Setup cost. The approximate number of orders per unit time is $\frac{D}{y}$ , so that the setup cost per unit time is approximately $\frac{KD}{y}$ .

2. Expected holding cost. Given $I$ is the average inventory level, the expected holding cost per unit time is ${hI}$ . The average inventory level is computed as

$$
I = \frac{\left( {y + E\{ R - x\} }\right)  + E\{ R - x\} }{2} = \frac{y}{2} + R - E\{ x\}
$$

The formula averages the starting and ending expected inventories in a cycle- $y + E\{ R - x\}$ and $E\{ R - x\}$ , respectively. As an approximation, the expression ignores the case where $R - E\{ x\}$ may be negative.

3. Expected shortage cost. Shortage occurs when $x > R$ . Its expected value per cycle is computed as

$$
S = {\int }_{R}^{\infty }\left( {x - R}\right) f\left( x\right) {dx}
$$

Because $p$ is assumed to be proportional to the shortage quantity only, the expected shortage cost per cycle is ${pS}$ , and, based on $\frac{D}{y}$ cycles per unit time, the shortage cost per unit time is $\frac{pS}{y/D} = \frac{pDS}{y}$ .

The resulting total cost function per unit time is

$$
\operatorname{TCU}\left( {y, R}\right)  = \frac{DK}{y} + h\left( {\frac{y}{2} + R - E\{ x\} }\right)  + \frac{pD}{y}{\int }_{R}^{\infty }\left( {x - R}\right) f\left( x\right) {dx}
$$

The optimal values, ${y}^{ * }$ and ${R}^{ * }$ , are determined from

$$
\frac{\partial \mathrm{{TCU}}}{\partial y} =  - \left( \frac{DK}{{y}^{2}}\right)  + \frac{h}{2} - \frac{pDS}{{y}^{2}} = 0
$$

$$
\frac{\partial \mathrm{{TCU}}}{\partial R} = h - \left( \frac{pD}{y}\right) {\int }_{R}^{\infty }f\left( x\right) {dx} = 0
$$

These two equations yield

$$
{y}^{ * } = \sqrt{\frac{{2D}\left( {K + {pS}}\right) }{h}} \tag{1}
$$

$$
{\int }_{{R}^{ * }}^{\infty }f\left( x\right) {dx} = \frac{h{y}^{ * }}{pD} \tag{2}
$$

The optimal values of ${y}^{ * }$ and ${R}^{ * }$ cannot be determined in closed forms. An iterative algorithm, developed by Hadley and Whitin (1963, pp. 169-174), is applied to (1) and (2) to find the solution. The algorithm converges in a finite number of iterations, provided a feasible solution exists.

For $R = 0$ , equation (1) and (2) yield

$$
\widehat{y} = \sqrt{\frac{{2D}\left( {K + {pE}\{ x\} }\right) }{2}}
$$

$$
\widetilde{y} = \frac{PD}{h}
$$

Unique optimal values of $y$ and $R$ exist when $\widetilde{y} \geq  \widehat{y}$ . The smallest value of ${y}^{ * }$ is $\sqrt{\frac{2KD}{h}}$ , which occurs when $S = 0$ .

The steps of the algorithm are

Step 0. Use the initial solution ${y}_{1} = {y}^{ * } = \sqrt{\frac{2KD}{h}}$ , and let ${R}_{0} = 0$ . Set $i = 1$ , and go to step $i$ .

Step 1. Use ${y}_{i}$ to determine ${R}_{i}$ from Equation ( 2). If ${R}_{i} \approx  {R}_{i - 1}$ , stop; the optimal solution is ${y}^{ * } = {y}_{i}$ , and ${R}^{ * } = {R}_{i}$ . Otherwise, use ${R}_{i}$ in Equation (1) to compute ${y}_{i}$ . Set $i = i + 1$ , and repeat step $i$ .

## Example 16.1-2

Electro uses resin in its manufacturing process at the rate of 1000 gallons per month. It cost Electro \$100 to place an order. The holding cost per gallon per month is \$2, and the shortage cost per gallon is \$10. Historical data show that the demand during lead time is uniform in the range $\left( {0,{100}}\right)$ gallons. Determine the optimal ordering policy for Electro.

Using the symbols of the model, we have

$D = {1000}$ gallons per month

$K = \$ {100}$ per order

$h = \$ 2$ per gallon per month

$p = \$ {10}$ per gallon

$$
f\left( x\right)  = \frac{1}{100},0 \leq  x \leq  {100}
$$

$E\{ x\}  = {50}$ gallons

First, we need to check whether the problem has a unique solution. Using the equations for $\widehat{y}$ and $\widetilde{y}$ we get

$$
\widehat{y} = \sqrt{\frac{2 \times  {1000}\left( {{100} + {10} \times  {50}}\right) }{2}} = {774.6}\text{ gallons }
$$

$$
\widetilde{y} = \frac{{10} \times  {1000}}{2} = {5000}\text{ gallons }
$$

Because $\widetilde{y} \geq  \widehat{y}$ , a unique solution exists for ${y}^{ * }$ and ${R}^{ * }$ .

The expression for $S$ is computed as

$$
S = {\int }_{R}^{100}\left( {x - R}\right) \frac{1}{100}{dx} = \frac{{R}^{2}}{200} - R + {50}
$$

Using $S$ in Equations (1) and (2), we obtain

$$
{y}_{i} = \sqrt{\frac{2 \times  {1000}\left( {{100} + {10S}}\right) }{2}} = \sqrt{{100},{000} + {10},{000S}}\text{ gallons } \tag{3}
$$

$$
{\int }_{R}^{100}\frac{1}{100}{dx} = \frac{2{y}_{i}}{{10} \times  {1000}} \tag{4}
$$

Equation (4) yields

$$
{R}_{i} = {100} - \frac{{y}_{i}}{50} \tag{5}
$$

We now use Equations (3) and (5) to determine the optimum solution.

Iteration 1

$$
{y}_{1} = \sqrt{\frac{2KD}{h}} = \sqrt{\frac{2 \times  {1000} \times  {100}}{2}} = {316.23}\text{ gallons }
$$

$$
{R}_{1} = {100} - \frac{316.23}{50} = {93.68}\text{ gallons }
$$

Iteration 2

$$
S = \frac{{R}_{1}^{2}}{200} - {R}_{1} + {50} = {.19971}\text{ gallons }
$$

$$
{y}_{2} = \sqrt{{100},{000} + {10},{000} \times  {.19971}} = {319.37}\text{ gallons }
$$

Hence,

$$
{R}_{2} = {100} - \frac{319.39}{50} -  = {93.612}
$$

Iteration 3

$$
S = \frac{{R}_{2}^{2}}{200} - {R}_{2} + {50} = {.20399}\text{ gallon }
$$

$$
{y}_{3} = \sqrt{{100},{000} + {10},{000} \times  {.20399}} = {319.44}\text{ gallons }
$$

Thus,

$$
{R}_{3} = {100} - \frac{319.44}{50} = {93.611}\text{ gallons }
$$

Because ${y}_{3} \approx  {y}_{2}$ and ${R}_{3} \approx  {R}_{2}$ , the optimum is ${R}^{ * } \approx  {93.611}$ gallons, ${y}^{ * } \approx  {319.44}$ gallons. File excelContRev.xls can be used to determine the solution to any degree of accuracy by specifying the tolerance $\left| {{R}_{i - 1} - {R}_{i}}\right|$ . The optimal inventory policy calls for ordering approximately 320 gallons whenever the inventory level drops to 94 gallons.

### 16.2 SINGLE-PERIOD MODELS

This section deals with inventory items that are in stock during a single time period. At the end of the period, leftover units, if any, are disposed of, as in fashion items. Two models will be developed. The difference between the two models is whether or not a setup cost is incurred for placing an order.

The symbols used in the development of the models include

$K =$ Setup cost per order

$h =$ Holding cost per held unit during the period

$p =$ Penalty cost per shortage unit during the period

$f\left( D\right)  =$ pdf of demand, $D$ , during the period

$y =$ Order quantity

$x =$ Inventory on hand before an order is placed.

The model determines the optimal value of $y$ that minimizes the sum of the expected holding and shortage costs. Given optimal $y\left( { = {y}^{ * }}\right)$ , the inventory policy calls for ordering ${y}^{ * } - x$ if $x < y$ ; otherwise, no order is placed.

#### 16.2.1 No-Setup Model (Newsvendor Model)

This model is known in the literature as the newsvendor model (the original classical name is the newsboy model). It deals with stocking and selling newspapers and periodicals.

The assumptions of the model are:

1. Demand occurs instantaneously at the start of the period immediately after the order is received.

2. No setup cost is incurred.

Figure 16.4 demonstrates the inventory position after the demand, $D$ , is satisfied. If $D < y$ , the quantity $y - D$ is held during the period. Otherwise, a shortage amount $D - y$ will result if $D > y$ .

The expected cost for the period, $E\{ C\left( y\right) \}$ , is expressed as

$$
E\{ C\left( y\right) \}  = h{\int }_{0}^{y}\left( {y - D}\right) f\left( D\right) {dD} + p{\int }_{y}^{\infty }\left( {D - y}\right) f\left( D\right) {dD}
$$

FIGURE 16.4

Holding and shortage inventory in a single-period model

![bo_d56m5dbef24c73bhe66g_7_422_1760_1026_376_0.jpg](bo_d56m5dbef24c73bhe66g_7_422_1760_1026_376_0.jpg)

The function $E\{ C\left( y\right) \}$ can be shown to be convex in $y$ , thus having a unique minimum. Taking the first derivative of $E\{ C\left( y\right) \}$ with respect to $y$ and equating it to zero, we get

$$
h{\int }_{0}^{y}f\left( D\right) {dD} - p{\int }_{0}^{\infty }f\left( D\right) {dD} = 0
$$

or

$$
{hP}\{ D \leq  y\}  - p\left( {1 - P\{ D \leq  y\} }\right)  = 0
$$

or

$$
P\left\{  {D \leq  {y}^{ * }}\right\}   = \frac{p}{p + h}
$$

If the demand, $D$ , is discrete, then the associated cost function is

$$
E\{ C\left( y\right) \}  = h\mathop{\sum }\limits_{{D = 0}}^{y}\left( {y - D}\right) f\left( D\right)  + p\mathop{\sum }\limits_{{D = y + 1}}^{\infty }\left( {D - y}\right) f\left( D\right)
$$

The necessary conditions for optimality are

$$
E\{ C\left( {y - 1}\right) \}  \geq  E\{ C\left( y\right) \} \text{ and }E\{ C\left( {y + 1}\right) \}  \geq  E\{ C\left( y\right) \}
$$

These conditions are also sufficient because $E\{ C\left( y\right) \}$ is a convex function. After some algebraic manipulations, the application of these conditions yields the following inequalities for determining ${y}^{ * }$ :

$$
P\left\{  {D \leq  {y}^{ * } - 1}\right\}   \leq  \frac{p}{p + h} \leq  P\left\{  {D \leq  {y}^{ * }}\right\}
$$

## Example 16.2-1

The owner of a newsstand wants to determine the number of newspapers of USA Now to be stocked at the start of each day. The owner pays 30 cents for a copy and sells it for 75 cents. The sale of the newspaper typically occurs between 7:00 and 8:00 A.M. (practically, instant demand). Newspapers left at the end of the day are recycled for an income of 5 cents a copy. How many copies should the owner stock every morning, assuming that the demand for the day can be described as

(a) A normal distribution with mean 300 copies and standard deviation 20 copies.

(b) A discrete pdf, $f\left( D\right)$ , defined as

<table><tr><td>$D$</td><td>200</td><td>220</td><td>300</td><td>320</td><td>340</td></tr><tr><td>$f\left( D\right)$</td><td>.1</td><td>.2</td><td>.4</td><td>.2</td><td>.1</td></tr></table>

The holding and penalty costs are not defined directly in this situation. The data of the problem indicate that each unsold copy will cost the owner ${30} - 5 = {25}$ cents and that the penalty for running out of stock is ${75} - {30} = {45}$ cents per copy. Thus, in terms of the parameters of the inventory problem, we have $h = {25}$ cents per copy per day and $p = {45}$ cents per copy per day.

First, we determine the critical ratio as

$$
\frac{p}{p + h} = \frac{45}{{45} + {25}} = {.643}
$$

Case (a). The demand $D$ is $N\left( {{300},{20}}\right)$ . We can use excelStatTables.xls to determine the optimum order quantity by entering 300 in F15, 20 in G15, and .643 in L15, which gives the desired answer of 307.33 newspapers in R15. Alternatively, we can use the standard normal tables in Appendix A. Define

$$
z = \frac{D - {300}}{20}
$$

Then from the normal tables

$$
P\{ z \leq  {.366}\}  \approx  {.643}
$$

or

$$
\frac{{y}^{ * } - {300}}{20} = {.366}
$$

Thus, ${y}^{ * } = {307.3}$ . The optimal order is approximately 308 copies.

Case (b). The demand $D$ follows a discrete pdf, $f\left( D\right)$ . First, we determine the CDF $P\{ D \leq  y\}$ as

<table><tr><td>$y$</td><td>200</td><td>220</td><td>300</td><td>320</td><td>340</td></tr><tr><td>$P\{ D \leq  y\}$</td><td>.1</td><td>.3</td><td>.7</td><td>.9</td><td>1.0</td></tr></table>

For the computed critical ratio of .643, we have

$$
P\left( {D \leq  {220}}\right)  \leq  {.643} \leq  P\left( {D \leq  {300}}\right)
$$

It only follows that ${y}^{ * } = {300}$ copies.

#### 16.2.2 Setup Model (s-S Policy)

The present model differs from the one in Section 16.2.1 in that a setup cost $K$ is incurred. Using the same notation, the total expected cost per period is

$$
E\{ \bar{C}\left( y\right) \}  = K + E\{ C\left( y\right) \}
$$

$$
= K + h{\int }_{0}^{y}\left( {y - D}\right) f\left( D\right) {dD} + p{\int }_{y}^{\infty }\left( {D - y}\right) f\left( D\right) {dD}
$$

As shown in Section 16.2.1, the optimum value ${y}^{ * }$ must satisfy

$$
P\left\{  {y \leq  {y}^{ * }}\right\}   = \frac{p}{p + h}
$$

Because $K$ is constant, the minimum value of $E\{ \bar{C}\left( y\right) \}$ must also occur at ${y}^{ * }$ .

In Figure 16.5, $S = {y}^{ * }$ , and the value of $s\left( { < S}\right)$ is determined from the equation

$$
E\{ C\left( s\right) \}  = E\{ \bar{C}\left( S\right) \}  = K + E\{ C\left( S\right) \} , s < S
$$

The equation yields another value ${s}_{1}\left( { > S}\right)$ , which is discarded.

Assume that $x$ is the amount on hand before an order is placed. How much should be ordered? This question is answered under three conditions:

1. $x < s$ .

2. $s \leq  x \leq  S$ .

3. $x > S$ .

Case $1\left( {x < s}\right)$ . Because $x$ is already on hand, its equivalent cost is given by $E\{ C\left( x\right) \}$ . If any additional amount $y - x\left( {y > x}\right)$ is ordered, the corresponding cost given $y$ is $E\{ \bar{C}\left( y\right) \}$ , which includes the setup cost $K$ . From Figure 16.5, we have

$$
\mathop{\min }\limits_{{y > x}}E\{ \bar{C}\left( y\right) \}  = E\left( {\bar{C}\left( S\right) }\right)  < E\{ C\left( x\right) \}
$$

Thus, the optimal inventory policy in this case is to order $S - x$ units.

Case $2\left( {s \leq  x \leq  S}\right)$ . From Figure 16.5, we have

$$
E\{ C\left( x\right) \}  \leq  \mathop{\min }\limits_{{y > x}}E\{ \bar{C}\left( y\right) \}  = E\left( {\bar{C}\left( S\right) }\right)
$$

Thus, it is not advantageous to order in this case and ${y}^{ * } = x$ .

Case $3\left( {x > S}\right)$ . From Figure 16.5, we have for $y > x$ ,

$$
E\{ C\left( x\right) \}  < E\{ \bar{C}\left( y\right) \}
$$

![bo_d56m5dbef24c73bhe66g_10_420_1704_639_410_0.jpg](bo_d56m5dbef24c73bhe66g_10_420_1704_639_410_0.jpg)

FIGURE 16.5

$\left( {s - S}\right)$ optimal ordering policy in a single-period model with setup cost

This condition indicates that, as in case (2), it is not advantageous to place an order - that is, ${y}^{ * } = x$ .

The optimal inventory policy, frequently referred to as the s-S policy, is summarized as

$$
\text{ If }x < s\text{ , order }S - x
$$

$$
\text{ If }x \geq  s\text{ , do not order }
$$

The optimality of the $s - S$ policy is guaranteed because the associated cost function is convex.

## Example 16.2-2

The daily demand for an item during a single period occurs instantaneously at the start of the period. The pdf of the demand is uniform between 0 and 10 units. The unit holding cost of the item during the period is \$.50, and the unit penalty cost for running out of stock is \$4.50. A fixed cost of \$25 is incurred each time an order is placed. Determine the optimal inventory policy for the item.

To determine ${y}^{ * }$ , consider

$$
\frac{p}{p + h} = \frac{4.5}{{4.5} + {.5}} = {.9}
$$

Also,

$$
P\left\{  {D \leq  {y}^{ * }}\right\}   = {\int }_{0}^{{y}^{ * }}\frac{1}{10}{dD} = \frac{{y}^{ * }}{10}
$$

Thus, $S = {y}^{ * } = 9$ .

The expected cost function is

$$
E\{ C\left( y\right) \}  = {.5}{\int }_{0}^{y}\frac{1}{10}\left( {y - D}\right) {dD} + {4.5}{\int }_{y}^{10}\frac{1}{10}\left( {D - y}\right) {dD}
$$

$$
= {.25}{y}^{2} - {4.5y} + {22.5}
$$

The value of $s$ is determined by solving

$$
E\{ C\left( s\right) \}  = K + E\{ C\left( S\right) \}
$$

or

$$
{.25}{s}^{2} - {4.5s} + {22.5} = {25} + {.25}{S}^{2} - {4.5S} + {22.5}
$$

Given $S = 9$ , the preceding equation reduces to

$$
{s}^{2} - {18s} - {19} = 0
$$

The solution of this equation is $s =  - 1$ or $s = {19}$ . The value of $s > S$ is discarded. Because the remaining value is negative $\left( { =  - 1}\right) , s$ has no feasible value. As Figure 16.6 shows, the optimal inventory policy in this case calls for not ordering the item. This result usually happens when the cost function is "flat" or when the setup cost is high relative to the other costs of the model.

![bo_d56m5dbef24c73bhe66g_12_309_196_802_443_0.jpg](bo_d56m5dbef24c73bhe66g_12_309_196_802_443_0.jpg)

FIGURE 16.6

$s - S$ policy applied to Example 16.2-2

### 16.3 MULTIPERIOD MODEL

This section presents a multiperiod model under the assumption of no setup cost. Additionally, the model allows backlog of demand and assumes a zero-delivery lag. It further assumes that the demand $D$ in any period is described by a stationary pdf, $f\left( D\right)$ .

The multiperiod model considers the discounted value of money. If $\alpha \left( { < 1}\right)$ is the discount factor per period, then an amount $\$ A$ available $n$ periods from now has a present value of $\$ {\alpha }^{n}A$ .

Suppose that the inventory situation encompasses $n$ periods and that unfilled demand can be backlogged exactly one period. Define

${F}_{i}\left( {x}_{i}\right)  =$ Maximum expected profit for periods $i, i + 1,\ldots$ , and $n$ , given that ${x}_{i}$ is the amount on hand before an order is placed in period $i$

Using the notation in Section 16.2 and assuming that $c$ and $r$ are the cost and revenue per unit, respectively, the inventory situation can be formulated using the following probabilistic dynamic programming model (see Chapter 24 on the website):

$$
{F}_{n + 1}\left( {{y}_{n} - D}\right)  = 0
$$

$$
{F}_{i}\left( {x}_{i}\right)  = \mathop{\max }\limits_{{{y}_{i} \geq  {x}_{i}}}\left\{  {-c\left( {{y}_{i} - {x}_{i}}\right)  + {\int }_{0}^{{y}_{i}}\left\lbrack  {{rD} - h\left( {{y}_{i} - D}\right) }\right\rbrack  f\left( D\right) {dD}}\right.
$$

$$
+ {\int }_{{y}_{i}}^{\infty }\left\lbrack  {r{y}_{i} + {\alpha r}\left( {D - {y}_{i}}\right)  - p\left( {D - {y}_{i}}\right) }\right\rbrack  f\left( D\right) {dD}
$$

$$
\left. {+\alpha {\int }_{0}^{\infty }{F}_{i + 1}\left( {{y}_{i} - D}\right) f\left( D\right) {dD}}\right\}  , i = 1,2,\ldots , n
$$

The value of ${x}_{i}$ may be negative because unfilled demand is backlogged. The quantity ${\alpha r}\left( {D - {y}_{i}}\right)$ in the second integral is included because $\left( {D - {y}_{i}}\right)$ is the unfilled demand in period $i$ that must be filled in period $i + 1$ .

The problem can be solved recursively. For the case where the number of periods is infinite, the recursive equation reduces to

$$
F\left( x\right)  = \mathop{\max }\limits_{{y \geq  x}}\left\{  {-c\left( {y - x}\right)  + {\int }_{0}^{y}\left\lbrack  {{rD} - h\left( {y - D}\right) }\right\rbrack  f\left( D\right) {dD}}\right.
$$

$$
+ {\int }_{y}^{\infty }\left\lbrack  {{ry} + {\alpha r}\left( {D - y}\right)  - p\left( {D - y}\right) }\right\rbrack  f\left( D\right) {dD}
$$

$$
\left. {+\alpha {\int }_{0}^{\infty }F\left( {y - D}\right) f\left( D\right) {dD}}\right\}
$$

where $x$ and $y$ are the inventory levels for each period before and after an order is received, respectively.

The optimal value of $y$ can be determined from the following necessary condition, which also happens to be sufficient because the expected revenue function $F\left( x\right)$ is concave:

$$
\frac{\partial \left( .\right) }{\partial y} =  - c - h{\int }_{0}^{y}f\left( D\right) {dD} + {\int }_{y}^{\infty }\left\lbrack  {\left( {1 - \alpha }\right) r + p}\right\rbrack  f\left( D\right) {dD}
$$

$$
+ \alpha {\int }_{0}^{\infty }\frac{\partial F\left( {y - D}\right) }{\partial y}f\left( D\right) {dD} = 0
$$

The value of $\frac{\partial F\left( {y - D}\right) }{\partial y}$ is determined as follows. If there are $\beta \left( { > 0}\right)$ more units on hand at the start of the next period, the profit for the next period will increase by ${c\beta }$ , because this much less has to be ordered. This means that

$$
\frac{\partial F\left( {y - D}\right) }{\partial y} = c
$$

The necessary condition thus becomes

$$
- c - h{\int }_{0}^{y}f\left( D\right) {dD} + \left\lbrack  {\left( {1 - \alpha }\right) r + p}\right\rbrack  \left( {1 - {\int }_{0}^{y}f\left( D\right) {dD}}\right)  + {\alpha c}{\int }_{0}^{\infty }f\left( D\right) {dD} = 0
$$

The optimum inventory level ${y}^{ * }$ is thus determined from

$$
{\int }_{0}^{{y}^{ * }}f\left( D\right) {dD} = \frac{p + \left( {1 - \alpha }\right) \left( {r - c}\right) }{p + h + \left( {1 - \alpha }\right) r}
$$

The optimal inventory policy for each period, given its entering inventory level $x$ , is thus given as

$$
\text{ If }x < {y}^{ * }\text{ , order }{y}^{ * } - x
$$

$$
\text{ If }x \geq  {y}^{ * }\text{ , do not order }
$$

## BIBLIOGRAPHY

Cohen, R., and F. Dunford, "Forecasting for Inventory Control: An Example of When 'Simple' Means 'Better'," Interfaces, Vol. 16, No. 6, pp. 95-99, 1986.

Hadley, G., and T. Whitin, Analysis of Inventory Systems, Prentice Hall, Upper Saddle River, NJ, 1963.

Nahmias, S., Production and Operations Analysis, 5th ed., Irwin, Homewood, IL, 2005.

Silver, E., D. Pyke, and R. Peterson, Decision Systems for Inventory Management and Production Control, 3rd ed., Wiley, New York, 1998.

Zipken, P., Foundations of Inventory Management, McGraw-Hill, Boston, 2000.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>16.1.1</td><td>16-1 to 16-3</td></tr><tr><td>16.1.2</td><td>16-4 to 16-7</td></tr><tr><td>16.2.1</td><td>16-8 to 16-15</td></tr><tr><td>16.2.2</td><td>16-16 to 16-18</td></tr><tr><td>16.3</td><td>16-19 to 16-21</td></tr></table>

16-1. In Example 16.1-1, determine the optimal inventory policy for each of the following cases:

*(a) Lead time $= {15}$ days.

(b) Lead time $= {25}$ days.

(c) Lead time $= {10}$ days.

(d) Lead time $= {12}$ days.

16-2. The daily demand for a popular CD in a music store is approximately $N\left( {{200},{20}}\right)$ . The cost of keeping the CD on the shelves is $\$ {.04}$ per disc per day. It costs the store $\$ {100}$ to place a new order. There is a 7-day lead time for delivery. Determine the store's optimal inventory policy given that the store wishes to limit the probability of shortage to at most .02.

16-3. The daily demand for camera films at a gift shop is $N\left( {{300},5}\right)$ . The cost of holding a roll in the shop is \$.02 per day, and the fixed cost of placing a replenishment order is \$30. The shop's inventory policy is to order 150 rolls whenever the inventory level drops to 80 units. It simultaneously maintains a buffer of 20 rolls at all times.

(a) Determine the probability of running out of stock.

(b) Given the data of the situation, recommend an inventory policy for the shop given that the shortage probability cannot exceed .10.

16-4. For the data given in Example 16.1-2, determine the following:

(a) The approximate number of orders per month.

(b) The expected monthly setup cost.

(c) The expected holding cost per month.

(d) The expected shortage cost per month.

(e) The probability of running out of stock during lead time.

*16-5. Solve Example 16.1-2, assuming that the demand during lead time is uniform between 0 and 50 gallons.

*16-6. In Example 16.1-2, suppose that the demand during lead time is uniform between 40 and 60 gallons. Compare the solution with that obtained in Example 16.1-2, and interpret the results. (Hint: In both problems, $E\{ x\}$ is the same, but the variance in the present problem is smaller.)

16-7. Find the optimal solution for Example 16.1-2, assuming that the demand during lead time is $N\left( {{100},2}\right)$ . Assume that $D = {10},{000}$ gallons per month, $h = \$ 2$ per gallon per month, $p = \$ 4$ per gallon, and $K = \$ {20}$ .

16-8. For the single-period model, show that for the discrete demand the optimal order quantity is determined from

$$
P\left\{  {D \leq  {y}^{ * } - 1}\right\}   \leq  \frac{p}{p + h} \leq  P\left\{  {D \leq  {y}^{ * }}\right\}
$$

16-9. The demand for an item during a single period occurs instantaneously at the start of the period. The associated pdf is uniform between 15 and 20 units. Because of the difficulty in estimating the cost parameters, the order quantity is determined such that the probability of either surplus or shortage does not exceed .1. Is it possible to satisfy both conditions simultaneously?

*16-10. The unit holding cost in a single-period inventory situation is \$1. If the order quantity is 4 units, find the permissible range of the unit penalty cost implied by the optimal conditions. Assume that the demand occurs instantaneously at the start of the period and that the pdf of demand is as follows:

<table><tr><td>$D$</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr><tr><td>$f\left( D\right)$</td><td>.05</td><td>.1</td><td>.1</td><td>.2</td><td>.25</td><td>.15</td><td>.05</td><td>.05</td><td>.05</td></tr></table>

16-11. The U of A Bookstore offers a program of reproducing class notes for participating professors. Professor Yataha teaches a freshmen-level class with an enrollment of between 100 and 150 students, uniformly distributed. A copy costs \$10 to produce, and it sells for \$25. The students purchase their books at the start of the semester. Any unsold copies of Professor Yataha's notes are shredded for recycling. In the meantime, once the bookstore runs out of copies, no additional copies are printed. If the bookstore wants to maximize its revenues, how many copies should it print?

16-12. QuickStop provides its customers with coffee and donuts at 6:00 A.M. each day. The convenience store buys the donuts for 7 cents apiece and sells them for 25 cents apiece until 8:00 a.m. After 8:00 a.m., the donuts sell for 5 cents apiece. The number of customers buying donuts between 6:00 and 8:00 is uniformly distributed between 30 and 50. Each customer usually orders 3 donuts with coffee. Approximately how many dozen donuts should QuickStop stock every morning to maximize revenues?

*16-13. Colony Shop is stocking heavy coats for next winter. Colony pays \$50 for a coat and sells it for \$110. At the end of the winter season, Colony offers the coats at \$55 each. The demand for coats during the winter season is more than 20 but less than or equal to 30, all with equal probabilities. Because the winter season is short, the unit holding cost is negligible. Also, Colony's manager does not believe that any penalty would result from coat shortages. Determine the optimal order quantity that will maximize the revenue for Colony Shop. You may use continuous approximation.

16-14. For the single-period model, suppose that the item is consumed uniformly during the period (rather than instantaneously at the start of the period). Develop the associated cost model, and find the optimal order quantity.

16-15. Solve Example 16.2-1, assuming that the demand is continuous and uniform during the period and that the pdf of demand is uniform between 0 and 100. (Hint: Use the results of Problem 16-14.)

*16-16. Determine the optimal inventory policy for the situation in Example 16.2-2, assuming that the setup cost is \$5.

16-17. In the single-period model in Section 16.2.1, suppose that the model maximizes profit and that a setup cost $K$ is incurred. Given that $r$ is the unit selling price and using the information in Section 16.2.1, develop an expression for the expected profit, and determine the optimal order quantity. Solve the problem numerically for $r = \$ 3, c = \$ 2, p = \$ 4, h = \$ 1$ , and $K = \$ {10}$ . The demand pdf is uniform between 0 and 10.

16-18. Work Problem 16-12, assuming that there is a fixed cost of \$10 associated with the delivery of donuts.

16-19. Consider a two-period probabilistic inventory model in which the demand is backlogged, and orders are received with zero delivery lag. The demand pdf per period is uniform between 0 and 10 , and the cost parameters are given as

Unit selling price $= \$ 2$

Unit purchase price $= \$ 1$

Unit holding cost per month $= \$ {.10}$

Unit penalty cost per month $= \$ 3$

Discount factor $= {.8}$

Find the optimal inventory policy for the two periods, assuming that the initial inventory for period 1 is zero.

*16-20. The pdf of the demand per period in an infinite-horizon inventory model is given as

$$
f\left( D\right)  = {.08D},0 \leq  D \leq  5
$$

The unit cost parameters are

Unit selling price $= \$ {10}$

Unit purchase price $= \$ 8$

Unit holding cost per month $= \$ 1$

Unit penalty cost per month $= \$ {10}$

Discount factor $= {.9}$

Determine the optimal inventory policy assuming zero delivery lag and that the unfilled demand is backlogged.

16-21. Consider the infinite-horizon inventory situation with zero delivery lag and backlogged demand. Develop the optimal inventory policy based on the minimization of cost given that

$$
\text{ Holding cost for }z\text{ units } = h{z}^{2}
$$

$$
\text{ Penalty cost for }z\text{ units } = p{x}^{2}
$$

Show that for the special case where $h = p$ , the optimal solution is independent of pdf of demand.

This page intentionally left blank