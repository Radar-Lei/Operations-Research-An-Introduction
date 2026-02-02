## CHAPTER 13 Inventory Modeling (with Introduction to Supply Chains)

```markmap
---
markmap:
  height: 643
---
# Inventory Modeling (with Introduction to Supply Chains)

## Real-Life Application
- [[#^kroger|Kroger Case Study]]
  - Pharmacy inventory management
  - Results: $80M revenue increase, $120M inventory reduction
  - Tool: Spreadsheet simulation-optimization

## Supply Chain Perspective
- [[#^supplychain|Supply Chain Flow]]
  - Goods: Supplier → Manufacturer → Retailer → Consumer
  - Funds: Supplier ← Manufacturer ← Retailer ← Consumer
  - Information: Bidirectional among all entities
  - [[#^balanceeff|Balance: Responsiveness vs Efficiency]]

### Inventory Metrics
- [[#^turnover|Turnover Ratio]]
  - Formula: Cost of goods sold / Average inventory cost
  - Assessment: < 1 (excessive), high (desirable), very high (stock-out risk)
- [[#^daysinv|Days in Inventory]]
  - Formula: $360 / \text{Turnover ratio}$

### Cost Components
- [[#^costcomponents|Total Inventory Cost]]
  - Purchasing cost
  - Setup (ordering) cost
  - Holding (carrying) cost
  - Shortage cost
  - [[#^conflictingcosts|Conflicting costs require trade-off]]

## Demand Types
### Four Categories
- [[#^demandtypes|Demand Classification]]
  - Deterministic: Constant or variable over time
  - Probabilistic: Stationary or nonstationary over time
- [[#^coefficient|Assessment using Coefficient of Variation (V)]]
  - [[#^guideline|V < 20%: Consider deterministic]]
  - [[#^guideline|V high: Probabilistic]]

## Static EOQ Models
### Classical EOQ
- [[#^eoq|EOQ Model]]
  - Assumptions: Constant demand, instantaneous replenishment, no shortages
  - Formula: $y^* = \sqrt{2KD/h}$
  - Cycle length: $t_0 = y/D$
  - Reorder point: $LD$ units ($L$ = lead time)
  - [[#^reorder|Effective lead time: $L_e = L - n \cdot t_0^*$]]

### EOQ with Price Breaks
- [[#^pricebreaks|Price Breaks Model]]
  - Unit price decreases for orders > q
  - Two cost functions: $\text{TCU}_1 (y \le q)$, $\text{TCU}_2 (y > q)$
  - Optimal solution: y* depends on price breakpoint location
  - Three zones: I $(0, y_m)$, II $(y_m, Q)$, III $(Q, \infty)$
  - Solution: $y^* = y_m$ (zones I or III) or $y^* = q$ (zone II)

### Multi-Item EOQ
- [[#^multiitem|Multi-Item with Storage Limitation]]
  - Items compete for limited storage space
  - Mathematical model: Minimize sum of individual TCU functions
  - Constraint: Sum of storage requirements ≤ available space
  - Solution: Try unconstrained EOQ first, then use nonlinear programming

## Dynamic EOQ Models
### No-Setup Model
- [[#^nosetup|No-Setup EOQ]]
  - No fixed ordering cost
  - Multiple production levels (regular time, overtime)
  - [[#^convexcost|Convex production cost function]]
  - [[#^transportation|Solved as transportation model]]
  - Solution: Assign demand to cheapest routes first

### Setup EOQ Model
- [[#^setup|Setup EOQ with Dynamic Programming]]
  - [[#^recursive|Forward recursive algorithm]]
  - [[#^endinventory|State: End-of-period inventory level]]
  - Decision: Production quantity
  - Cost function: Production + holding costs
  - Special case: Constant/decreasing marginal costs
    - [[#^contiguous|Optimal: Produce for exact demand of contiguous periods]]
    - [[#^productionorinventory|Either new production OR inventory, never both]]

### Heuristic Methods
- [[#^silvermeal|Silver-Meal Heuristic]]
  - Valid for constant unit production cost
  - Objective: Minimize setup + holding cost per period
  - Algorithm: Find $t^*$ minimizing $\text{TCU}(i,t)$
  - Repeat for each planning period

## Implementation Issues
- [[#^issues|Implementation Challenges]]
  - Model selection
  - Cost parameter estimation
  - No universal rules available

## Case Study: Kroger Pharmacy
- [[#^krogerdetail|Kroger Case Details]]
  - 2000 in-store pharmacies
  - $8B retail value, 2500 drugs per pharmacy
  - (s, S) periodic review policy
  - Demand: Intermittent, irregular, empirical distribution
  - Tool: Spreadsheet simulation with local search algorithm
  - Results: $80M revenue increase, $120M inventory reduction
```


## Real-Life Application: Kroger Improves Pharmacy Inventory Management ^kroger

The Kroger Company operates approximately 2500 pharmacies in its stores across the United States. Drug shortages and excessive inventory were kept in check through the use of a spreadsheet simulation optimization model. The use of the spreadsheet made it easy to gain wide acceptance by both the management and pharmacy personnel. Kroger reports an increase in revenue of \$80 million and a reduction in inventory of more than \$120 million from November 2011 to March 2013. The full case study is presented at the end of the chapter.

### 13.1 INVENTORY PROBLEM: A SUPPLY CHAIN PERSPECTIVE ${}^{1}$

Supply chain is a recent modeling conceptualization of end-to-end flow of goods, funds, and information among four principal entities: supplier, manufacturer, retailer, and consumer. Directions of flow can be summarized as

Goods flow: Supplier $\rightarrow$ Manufacturer $\rightarrow$ Retailer $\rightarrow$ Consumer

Funds flow: Supplier $\leftarrow$ Manufacturer $\leftarrow$ Retailer $\leftarrow$ Consumer

Information flow: Supplier $\leftrightarrow$ Manufacturer $\leftrightarrow$ Retailer $\leftrightarrow$ Consumer ^supplychain

Goods flow starts at the supplier and ends at the consumer. Funds flow starts at the consumer, the main source of revenue for the entire chain, and moves upstream, allotting portions of the revenue to retailer, manufacturer, and supplier. Information flow requires close collaboration among all the entities of the chain. Among the most crucial information exchange is the sales data at the consumer level. This data is used to predict the nature of the demand distribution, which is subsequently used to determine the optimum levels and movements of goods at/to all locations in the supply chain. From this standpoint, it is important to recognize that no member of the supply chain should attempt to gain economic advantages at the expense of another member. In the end, such policy will result in a higher cost for the final product and, hence, lower revenue for all the members of the supply chain.

---

${}^{1}$ This brief presentation of supply chains is not intended to compete with the rich resources on the subject already available in the literature. The intent is to introduce the inventory problem in the relevant context of the encompassing modeling view of supply chains.

---

The arrows in the supply chain representation given above symbolize the distance and time lapse separations among the physical locations of the four entities of the chain. The important implication here is that each location must maintain a level of inventory to guarantee a reasonable degree of operational responsiveness (to client's needs). At the same time, the supply chain must be efficient, in the sense that the inventory cost of storing, transporting, handling, and running out of stock must be kept in check. Thus, in deciding the level of inventory, a balance must be maintained between level of responsiveness and the degree of efficiency. ^balanceeff

#### 13.1.1 An Inventory Metric in Supply Chains ^turnover

Businesses use simple ratios and formulas to evaluate the impact of inventories on the financial health of the company. A common metric is the following turnover ratio:

$$
\text{ Turnover ratio } = \frac{\text{ Cost of goods sold in a period }}{\text{ Cost of average inventory in the same period }}
$$

It measures the number of times a business has sold through its inventory during a specified period (usually a year) to realize given sales. Note importantly that the numerator is the cost and not the revenue of goods sold.

As a general rule, a ratio less than 1 is a strong indicator that a business carries too much inventory for its realized sales volume. A high turnover ratio, on the other hand, is desirable because it indicates lower inventory and high sales volume. However, unreasonably high inventory turnover could be an indication that the business is carrying low inventory, giving rise to lost sales caused by stock-outages.

All the data for computing this ratio are usually taken from the (end-of-year) balance sheet of the company. For this reason, the turnover ratio is computed over a 1-year period and the average inventory is the simple average of the beginning and ending inventory costs for the year. This simple average assumes that inventory is depleted uniformly over the year, which may not be true. For example, distortion will occur in the extreme case of the inventory staying constant for the first 10 months of the year and then depleted sharply during the Christmas shopping months of November and December. This bias can be alleviated by tracking the actual inventory on a monthly or quarterly basis. However, collecting the information for this task may be costly (as opposed to simply using balance sheet data).

A companion metric of the turnover ratio is the number of days inventory is held ^daysinv in the system before it is turned over, computed as:

$$
\text{ Days in inventory } = \frac{360}{\text{ Turnover ratio }}
$$

Example 13.1-1

The following table summarizes financial information taken from the balance sheets of a hypothetical company.

|  | (Million \$) | (Million \$) | (Million \$) |
|---|---|---|---|
| December 31, 2014 | December 31, 2013 | December 31, 2012 |  |
| Cost of goods sold | 3989.1 | 3872.1 | 3562.7 |
| Inventories: |  |  |  |
| Supplies | 310.2 | 210.4 | 156.2 |
| Raw materials | 189.7 | 199.4 | 172.6 |
| Work-in-process | 339.1 | 310.5 | 342.3 |
| Finished goods | 200.1 | 196.4 | 150.7 |

Assess how well the company is managing its inventory.

The following table summarizes the calculation of the turnover ratios:

| (Million \$)       | 2014                       | 2013                       | 2012   |
| ------------------ | -------------------------- | -------------------------- | ------ |
| Cost of goods sold | 3989.1                     | 3872.1                     | 3562.7 |
| Total inventory    | 1039.1                     | 916.7                      | 821.8  |
| Average inventory  | (1039.1 + 916.7)/2 = 977.9 | (916.7 + 821.8)/2 = 869.25 |        |
| Turnover ratio     | (3989.1/977.9) = 4.08      | (3872.1/869.25) = 4.45     |        |
| Days in inventory  | (365/4.08) = 89.46         | (365/4.45) = 82.02         |        |

The calculations show an unfavorable inventory situation: Low inventory turns (approximately 4 times a year) in 2013 and 2014 and high average days in inventory (over 80 days). Moreover, a worsening inventory situation occurs in 2014 compared to 2013.

The results above deals with assessing the inventory situation based on (end-of-year) balance sheet information. It provides generic metrics that simply pinpoint whether or not the inventory held by a business over the past year was in line with expectations. In this regard, the metrics do not suggest solutions for reducing excessive inventories as much as raise red flags about the inventory situation.

To alleviate the problem, it is necessary to devise tools suitable for determining the optimum inventory levels at all operational levels of the supply chain, from raw material to finished goods. These tools can be used to target a single item or a group of (homogeneous) items.

The nature of demand for an item can be broadly categorized as either deterministic or probabilistic. This categorization is a key factor in the development of inventory optimization tools. The remainder of this chapter deals with the (more analytically amenable) deterministic case. The probabilistic case will be presented in Chapter 16 following a review of probability and statistics in Chapter 14.

#### 13.1.2 Elements of the Inventory Optimization Model ^costcomponents

Most businesses must maintain inventory on hand to deal with uncertainties in demand. Too much inventory increases the holding cost of maintaining inventory in stock (capital, storage, maintenance, and handling), and too little increases shortage cost (lost sales, disruption in production, and loss of customer's goodwill). As units are withdrawn from stock, inventory is replenished periodically by initiating new orders from suppliers, with each new order incurring a (fixed) setup cost that is independent of the size of the order. In most cases, the purchase price from the supplier is discounted for large-size orders. What this all means is that the associated total inventory cost can be expressed as

$$
\left( \begin{matrix} \text{ Total } \\  \text{ inventory } \\  \text{ cost } \end{matrix}\right)  = \left( \begin{matrix} \text{ Purchasing } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Setup } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Holding } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Shortage } \\  \text{ cost } \end{matrix}\right)
$$

These are conflicting costs, in the sense that smaller order sizes will reduce the holding cost (per unit time) while, at the same time, increasing the remaining costs, and vice versa. In this situation, the best that can be done is to seek a trade-off among these costs by deciding an inventory level that minimizes the total inventory cost. ^conflictingcosts

The inventory problem reduces to devising an inventory policy that answers two questions:

1. How much to order?

2. When to order?

The basis of the inventory model is the following generic cost function:

$$
\left( \begin{matrix} \text{ Total } \\  \text{ inventory } \\  \text{ cost } \end{matrix}\right)  = \left( \begin{matrix} \text{ Purchasing } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Setup } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Holding } \\  \text{ cost } \end{matrix}\right)  + \left( \begin{matrix} \text{ Shortage } \\  \text{ cost } \end{matrix}\right)
$$

A description of the components of the cost function is given subsequently:

1. Purchasing cost is the price per unit of an inventory item. At times, the item is offered at a discount if the order size exceeds a certain amount, which is a factor in deciding how much to order.

2. Setup cost represents the fixed charge incurred when an order is placed. It can also include the cost associated with receiving a shipment. The cost is fixed regardless of the size of the order requested or the shipment received.

3. Holding cost represents the cost of maintaining inventory in stock. It includes the interest on capital and the cost of storage, maintenance, handling, obsolescence, and shrinkage due to fraud or theft.

4. Shortage cost is the penalty incurred when stock is out. It includes potential loss of income, disruption in production, the additional cost of ordering emergency shipments (usually overnight), and the (hard-to-estimate) subjective cost of loss in customer goodwill.

The described costs are conflicting, in the sense that an increase in one may result in the reduction of another (e.g., more frequent ordering results in higher setup cost but lower inventory holding cost). The purpose of the minimization of the total inventory cost function is to balance these conflicting costs.

How much to order simply translates to determining the size of the order at replenishment time. When to order is a bit more involved. An inventory system may require periodic reviews (e.g., ordering at the start of every week or month), or it may be based on continuous reviews, placing a new order whenever the inventory level drops to a specific reorder point. An example of the two types occurs in retail stores. The review is periodic if the item is replenished every week or month. It is continuous if replenishment takes place whenever the inventory level dips below a certain level.

The presentation above gives a unifying framework for deciding the optimum inventory policy. Yet, the specific models for determining these policies are as diverse as the different situations they handle. In general, the complexity of the resulting models depends to a great degree on the degree of uncertainty in the demand for the inventory item.

### 13.2 ROLE OF DEMAND IN THE DEVELOPMENT OF INVENTORY MODELS ^demandrole

In general, the analytic complexity of inventory models depends on whether the demand is deterministic or probabilistic. Within either category, the demand may or may not vary with time. For example, the consumption of natural gas used in heating homes is seasonal. Though the seasonal pattern repeats itself annually, a same-month consumption may vary from year to year, depending, for example, on the severity of weather.

In practical situations, the demand pattern in an inventory model may assume one of four types:

1. Deterministic and constant (static) with time.

2. Deterministic and variable (dynamic) with time.

3. Probabilistic and stationary over time.

4. Probabilistic and nonstationary over time.

This categorization assumes the availability of reliable data to forecast future demand. ^demandtypes

In terms of the development of inventory models, the first category is the simplest analytically, and the fourth is the most complex. On the other hand, the first category is the least likely to occur in practice and the fourth is the most prevalent. In practice, the goal is to balance model simplicity and model accuracy.

How can we decide if a certain approximation of demand is acceptable? An initial "guesstimate" is based on computing the mean and standard deviation of consumption for a specific period (e.g., monthly). The coefficient of variation, $V = \frac{\text{ Standard deviation }}{\text{ Mean }} \times  {100}$ , can then be used to assess the nature of demand using the following guideline: ${}^{2}$ ^coefficient

1. If the average monthly demand (taken over a number of years) is "approximately" constant and $V$ is reasonably small (<20%), then the demand may be considered deterministic and constant.

2. If the average monthly demand varies appreciably among the different months but $V$ remains reasonably small for all months, then the demand may be considered deterministic but variable.

3. If in Case ${1V}$ is high (>20%) but approximately constant, then the demand is probabilistic and stationary.

4. The remaining case is the probabilistic nonstationary demand, which occurs when the averages and coefficients of variation vary appreciably month to month. ^guideline

## Example 13.2-1

The data in Table 13.1 provide the monthly (January through December) consumption of natural gas in a rural residential home over a span of 10 years (1990-1999). The supplier sends a truck to fill a tank at the request of a homeowner.

From the standpoint of inventory modeling, it is reasonable to assume that each month represents a decision period for the placement of an order. The purpose of this example is to analyze the nature of the demand.

TABLE 13.1 Monthly (January through December) Consumption of Natural Gas

| Year | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet | Natural-Gas Consumption in Cubic Feet |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Jan | Feb | Mar | Apr | May | Jun | Jul | Aug | Sep | Oct | Nov | Dec |  |
| 1990 | 100 | 110 | 90 | 70 | 65 | 50 | 40 | 42 | 56 | 68 | 88 | 95 |
| 1991 | 110 | 125 | 98 | 80 | 60 | 53 | 44 | 45 | 63 | 77 | 92 | 99 |
| 1992 | 90 | 100 | 88 | 79 | 56 | 57 | 38 | 39 | 60 | 70 | 82 | 90 |
| 1993 | 121 | 130 | 95 | 90 | 70 | 58 | 41 | 44 | 70 | 80 | 95 | 100 |
| 1994 | 109 | 119 | 99 | 75 | 68 | 55 | 43 | 41 | 65 | 79 | 88 | 94 |
| 1995 | 130 | 122 | 100 | 85 | 73 | 58 | 42 | 43 | 64 | 75 | 80 | 101 |
| 1996 | 115 | 100 | 103 | 90 | 76 | 55 | 45 | 40 | 67 | 78 | 98 | 97 |
| 1997 | 130 | 115 | 100 | 95 | 80 | 60 | 49 | 48 | 64 | 85 | 96 | 105 |
| 1998 | 125 | 100 | 94 | 86 | 79 | 59 | 46 | 39 | 69 | 90 | 100 | 110 |
| 1999 | 87 | 80 | 78 | 75 | 69 | 48 | 39 | 41 | 50 | 70 | 88 | 93 |
| Mean | 111.7 | 110 | 95 | 82.5 | 69.6 | 55 | 42.7 | 42 | 62.8 | 77 | 91 | 98 |
| Std Dev | 15.54 | 15.2 | 7.5 | 7.99 | 7.82 | 3.9 | 3.4 | 2.9 | 6.09 | 6.9 | 6.7 | 6 |
| $V\left( \% \right)$ | 13.91 | 13.8 | 7.9 | 9.68 | 11.2 | 7.1 | 7.96 | 6.8 | 9.69 | 8.9 | 7.4 | 6.1 |

---

${}^{2}$ The coefficient of variation, $V$ , measures the relative variation or spread of the data around the mean. In general, higher values of $V$ indicate higher uncertainty in the use of the mean as an approximation of monthly consumption. For deterministic demand, $V = 0$ , because the associated standard deviation is zero.

---

An examination of the mean and the coefficient of variation, $V$ , in Table 13.1 reveals two results:

1. Average consumption is dynamic (not constant) because of the high average consumption during winter months.

2. The coefficient of variation, $V$ , is reasonably small $\left( { < {15}\% }\right)$ so, as a first assessment, the monthly demand can be considered approximately deterministic.

The conclusion is that the monthly demand is (approximately) deterministic but variable.

### 13.3 STATIC ECONOMIC-ORDER-QUANTITY MODELS ^staticeoq

This section presents three variations of the economic-order-quantity (EOQ) model with static (constant) demand. These models are simple analytically.

#### 13.3.1 Classical EOQ Model ^eoq

The simplest of the inventory models involves constant-rate demand with instantaneous order replenishment and no shortage. ^eoqassumptions Define

$$
y = \text{ Order quantity (number of units) }
$$

$$
D = \text{ Demand rate (units per unit time) }
$$

$$
{t}_{0} = \text{ Ordering cycle length (time units) }
$$

The inventory level follows the pattern depicted in Figure 13.1. When the inventory reaches zero level, an order of size $y$ units is received instantaneously. The stock is depleted uniformly at a constant demand rate, $D$ . The ordering cycle for this pattern is

$$
{t}_{0} = \frac{y}{D}\text{ time units }
$$

The cost model requires two cost parameters:

$K =$ Setup cost associated with the placement of an order (dollars per order)

$h =$ Holding cost (dollars per inventory unit per unit time)

FIGURE 13.1

Inventory pattern in the classical EOQ model

![bo_d56m533ef24c73bhe630_6_380_1760_1197_404_0.jpg](bo_d56m533ef24c73bhe630_6_380_1760_1197_404_0.jpg)

Given that the average inventory level is $\frac{y}{2}$ , the total cost per unit time (TCU) is

$$
\operatorname{TCU}\left( y\right)  = \text{ Setup cost per unit time + Holding cost per unit time }
$$

$$
= \frac{\text{ Setup cost } + \text{ Holding cost per cycle }{t}_{0}}{{t}_{0}}
$$

$$
= \frac{K + h\left( \frac{y}{2}\right) {t}_{0}}{{t}_{0}}
$$

$$
= \frac{K}{\left( \frac{y}{D}\right) } + h\left( \frac{y}{2}\right)
$$

The optimum value of the order quantity $y$ is determined by minimizing $\operatorname{TCU}\left( y\right)$ . Assuming $y$ is continuous, a necessary condition for optimality is

$$
\frac{d\operatorname{TCU}\left( y\right) }{dy} =  - \frac{KD}{{y}^{2}} + \frac{h}{2} = 0
$$

The condition is also sufficient because $\operatorname{TCU}\left( y\right)$ is convex.

The solution of the equation yields the EOQ ${y}^{ * }$ as

$$
{y}^{ * } = \sqrt{\frac{2KD}{h}}
$$

Thus, the optimum inventory policy for the proposed model is

$$
\text{ Order }{y}^{ * } = \sqrt{\frac{2KD}{h}}\text{ units every }{t}_{0}^{ * } = \frac{{y}^{ * }}{D}\text{ time units }
$$

Actually, a new order need not be received at the instant it is ordered. Instead, a positive lead time, $L$ , may occur between the placement and the receipt of an order, as reorder point occurs when the inventory level drops to ${LD}$ units. ^reorder

Figure 13.2 assumes that the lead time, $L$ , is less than the cycle length ${t}_{0}^{ * }$ , which may not be the case in general. In such cases, we define the effective lead time as ^effective

$$
{L}_{e} = L - n{t}_{0}^{ * }
$$

FIGURE 13.2

Reorder point in the classic EOQ model

![bo_d56m533ef24c73bhe630_7_327_1723_1217_461_0.jpg](bo_d56m533ef24c73bhe630_7_327_1723_1217_461_0.jpg)

The parameter $n$ is the largest integer value not exceeding $\frac{L}{{t}_{0}^{ * }}$ . The formula recognizes that after $n$ cycles the actual interval between the placement and the receipt of two successive orders is ${L}_{e}$ . Thus, the reorder point occurs at ${L}_{e}D$ units, and the inventory policy can be restated as

Order the quantity ${y}^{ * }$ whenever the inventory level drops to ${L}_{e}D$ units.

## Example 13.3-1

Neon lights on the U of A campus are replaced at the rate of 100 units per day. The physical plant orders the neon lights periodically. It costs \$100 to initiate a purchase order. A neon light kept in storage is estimated to cost about \$.02 per day. The lead time between placing and receiving an order is 12 days. Determine the optimal inventory policy for ordering the neon lights.

From the data of the problem, we have

$D = {100}$ units per day

$K = \$ {100}$ per order

$h = \$ {.02}$ per unit per day

$L = {12}$ days

Thus,

$$
{y}^{ * } = \sqrt{\frac{2KD}{h}} = \sqrt{\frac{2 \times  \$ {100} \times  {100}}{.02}} = {1000}\text{ neon lights }
$$

The associated cycle length is

$$
{t}_{0}^{ * } = \frac{{y}^{ * }}{D} = \frac{1000}{100} = {10}\text{ days }
$$

Because the lead time $L\left( { = {12}\text{ days }}\right)$ exceeds the cycle length ${t}_{0}^{ * }\left( { = {10}\text{ days }}\right)$ , we must compute ${L}_{e}$ . The number of integer cycles included in $L$ is

$$
n = \left( {\text{ largest integer } \leq  \frac{L}{{t}_{0}^{ * }}}\right)  = \left( {\text{ largest integer } \leq  \frac{12}{10}}\right)  = 1
$$

Thus,

$$
{L}_{e} = L - n{t}_{0}^{ * } = {12} - 1 \times  {10} = 2\text{ days }
$$

The reorder point thus occurs when the inventory level drops to

$$
{L}_{e}D = 2 \times  {100} = {200}\text{ neon lights }
$$

The inventory policy is

Order 1000 units whenever the inventory level drops to 200 units.

The daily inventory cost associated with the proposed policy is

$$
\operatorname{TCU}\left( y\right)  = \frac{K}{\left( \frac{y}{D}\right) } + h\left( \frac{y}{2}\right)
$$

$$
= \frac{\$ {100}}{\left( \frac{1000}{100}\right) } + \$ {.02}\left( \frac{1000}{2}\right)  = \$ {20}\text{ per day }
$$

510 Chapter 13 Inventory Modeling (with Introduction to Supply Chains)

|  | B | C | D |
|---|---|---|---|
| 1 General Economic Order Quantity (EOQ) | 1 General Economic Order Quantity (EOQ) | 1 General Economic Order Quantity (EOQ) | 1 General Economic Order Quantity (EOQ) |
| 2 Input data: (Enter -1 in column C if data element does not apply) | 2 Input data: (Enter -1 in column C if data element does not apply) | 2 Input data: (Enter -1 in column C if data element does not apply) | 2 Input data: (Enter -1 in column C if data element does not apply) |
| 3 | Item cost, c1 = | -1 |  |
| 4 | Qty discount limit, $q =$ | -1 |  |
| 5 | Item cost, c2 = | -1 |  |
| 6 | Setup cost, K = | 100 |  |
| 7 | Demand rate, D = | 100 |  |
| 8 | Production rate, a = | -1 |  |
| 9 | Unit holding cost, h = | 0.02 |  |
| 10 | Unit penalty cost, p = | -1 |  |
| 11 | Lead time, L = | 12 |  |
| 12 Model output results: | 12 Model output results: | 12 Model output results: | 12 Model output results: |
| 13 | Order qty, y* = | 1000.00 | 1000.00 |
| 14 | Shortage qty, w* = | 0.00 | 0.00 |
| 15 | Reorder point, R = | 200.00 | 200.00 |
| 16 | TCU(y*) = | 20.00 | 20.00 |
| 17 | Purchase/prod. Cost = | 0.00 | 0.00 |
| 18 | Setup cost/unit time = | 10.00 | 10.00 |
| 19 | Holding cost /unit time = | 10.00 | 10.00 |
| 20 | Shortage cost/unit time = ( | 0.00 | 0.00 |
| 21 Optimal inventory policy: Order 1000.00 units when level drops to 200.00 units | 21 Optimal inventory policy: Order 1000.00 units when level drops to 200.00 units | 21 Optimal inventory policy: Order 1000.00 units when level drops to 200.00 units | 21 Optimal inventory policy: Order 1000.00 units when level drops to 200.00 units |
| 22 Model intermediate calculations: | 22 Model intermediate calculations: | 22 Model intermediate calculations: | 22 Model intermediate calculations: |
| 23 | ym = | 1000.00 | 1000.00 |
| 24 | TCU1(ym)= | Not applicable | Not applicable |
| 25 | Q-equation: | Not applicable | Not applicable |
| 26 | Q = | Not applicable | Not applicable |
| 27 | cycle length, t0 = | 10.00 | 10.00 |
| 28 | Optimization zone = | Not applicable | Not applicable |
| 29 | Effective lead time. Le = | 2.00 | 2.00 |

FIGURE 13.3

Excel solution of Example 13.3-1 (file excelEOQ.xls)

## Excel Moment

File exelEOQ.xls is designed to carry out the computations for the general EOQ with shortage and simultaneous production-consumption operation (see Problem 13-12). It also solves the price-breaks situation presented in Section 13.3.2. To use the template with the special case of Example 13.3-1, enter -1 in cells C3:C5, C8, and C10 to indicate that the corresponding data are not applicable, as shown in Figure 13.3.

## Aha! Moment: EOQ History, or Giving Credit Where Credit Is Due!

Practically all the inventory control literature (including editions 3 through 9 of this book) has identified the classical EOQ as the "Wilson formula," in recognition of R. H. Wilson, who, as a business and industry consultant, was instrumental in promoting the use of the formula. In point of fact, the formula was developed by Ford W. Harris in ${1913}_{,}{}^{3}$ some 15 years before

---

${}^{3}$ Harris, Ford W. [Reprint from 1913] "How Many Parts to Make at Once," Operations Research, Vol. 38, No. 6, pp. 947-950, 1990.

---

Wilson started publishing accounts of its use in his consulting work. Yet, Harris's contribution was obscured and misplaced, whether accidently or by design, for nearly 75 years until Donald Erlenkotter of the University of California, Los Angles, set the record straight, publishing a series of articles starting in 1989 detailing the circumstances that led to this unfortunate lapse in EOQ history. ${}^{4}$

Perhaps one of the reasons for not giving Harris his due credit is that he was not academic, hence he lacked the exposure afforded in academic circles. In fact, Harris did not have any formal education past a high school diploma. Yet, through tutoring and self-study, he was hired as an engineer at Westinghouse, where he patented numerous inventions. Later, once again relying on self-study, he decided to change careers and became a successful patent lawyer.

#### 13.3.2 EOQ with Price Breaks ^pricebreaks

This model is the same as in Section 13.3.1, except that the inventory item may be purchased at a discount if the size of the order, $y$ , exceeds a given limit, $q$ . Mathematically, the unit purchasing price, $c$ , is given as

$$
c = \left\{  \begin{array}{l} {c}_{1},\text{ if }y \leq  q \\  {c}_{2},\text{ if }y > q \end{array}\right\}  ,{c}_{1} > {c}_{2}
$$

Hence,

$$
\text{ Purchasing cost per unit time } = \left\{  \begin{array}{l} \frac{{c}_{1}y}{{t}_{0}} = \frac{{c}_{1}y}{\left( \frac{y}{D}\right) } = D{c}_{1}, y \leq  q \\  \frac{{c}_{2}y}{{t}_{0}} = \frac{{c}_{2}y}{\left( \frac{y}{D}\right) } = D{c}_{2}, y > q \end{array}\right.
$$

Using the notation in Section 13.3.1, the total cost per unit time is

$$
\operatorname{TCU}\left( y\right)  = \left\{  \begin{array}{l} {\operatorname{TCU}}_{1}\left( y\right)  = D{c}_{1} + \frac{KD}{y} + \frac{h}{2}y, y \leq  q \\  {\operatorname{TCU}}_{2}\left( y\right)  = D{c}_{2} + \frac{KD}{y} + \frac{h}{2}y, y > q \end{array}\right.
$$

The functions ${\mathrm{{TCU}}}_{1}$ and ${\mathrm{{TCU}}}_{2}$ are graphed in Figure 13.4. Because the two functions differ only by a constant amount, their minima must coincide at ^twocosts

$$
{y}_{m} = \sqrt{\frac{2KD}{h}}
$$

---

${}^{4}$ Erlenkotter, D.,“Ford Whitman Harris’s Economical Lot Size Model," International Journal of Production Economics, Vol. 155. pp. 12-15, 2014.

---

![bo_d56m533ef24c73bhe630_11_400_201_527_413_0.jpg](bo_d56m533ef24c73bhe630_11_400_201_527_413_0.jpg)

FIGURE 13.4

Inventory cost function with price breaks

The determination of the optimum order quantity ${y}^{ * }$ depends on where the price breakpoint, $q$ , lies with respect to zones I, II, and III, delineated in Figure 13.4 by the ranges $\left( {0,{y}_{m}}\right\rbrack  ,\left( {{y}_{m}, Q}\right\rbrack$ , and $\left( {Q,\infty }\right)$ , respectively. ^threezones The value of $Q\left( { > {y}_{m}}\right)$ is determined from the equation

$$
{\mathrm{{TCU}}}_{2}\left( Q\right)  = {\mathrm{{TCU}}}_{1}\left( {y}_{m}\right)
$$

or

$$
{c}_{2}D + \frac{KD}{Q} + \frac{hQ}{2} = {\mathrm{{TCU}}}_{1}\left( {y}_{m}\right)
$$

which simplifies to

$$
{Q}^{2} + \left( \frac{2\left( {{c}_{2}D - {\mathrm{{TCU}}}_{1}\left( {y}_{m}\right) }\right) }{h}\right) Q + \frac{2KD}{h} = 0
$$

Figure 13.5 shows that the desired optimum quantity ${y}^{ * }$ is

$$
{y}^{ * } = \left\{  \begin{array}{l} {y}_{m},\text{ if }q\text{ is in zones I or III } \\  q,\text{ if }q\text{ is in zone II } \end{array}\right.
$$

The steps for determining ${y}^{ * }$ are as follows:

Step 1. Determine ${y}_{m} = \sqrt{\frac{2KD}{h}}$ . If $q$ is in zone I, then ${y}^{ * } = {y}_{m}$ . Otherwise, go to step 2.

Step 2. Determine $Q\left( { > {y}_{m}}\right)$ from the $Q$ -equation

$$
{Q}^{2} + \left( \frac{2\left( {{c}_{2}D - {\mathrm{{TCU}}}_{1}\left( {y}_{m}\right) }\right) }{h}\right) Q + \frac{2KD}{h} = 0
$$

Define zones II and III. If $q$ is in zone II, ${y}^{ * } = q$ . Otherwise, $q$ is in zone III, and ${y}^{ * } = {y}_{m}$ .

![bo_d56m533ef24c73bhe630_12_333_199_1299_919_0.jpg](bo_d56m533ef24c73bhe630_12_333_199_1299_919_0.jpg)

FIGURE 13.5

Optimum solution of the inventory problems with price breaks

## Example 13.3-2

LubeCar specializes in fast automobile oil change. The garage buys car oil in bulk at \$3 per gallon discounted to \$2.50 per gallon if the order quantity is more than 1000 gallons. The garage services approximately 150 cars per day, and each oil change takes 1.25 gallons. LubeCar stores bulk oil at the cost of \$.02 per gallon per day. Also, the cost of placing an order is \$20. There is a 2-day lead time for delivery. Determine the optimal inventory policy.

The consumption of oil per day is

$D = {150}$ cars per day $\times  {1.25}$ gallons per car $= {187.5}$ gallons per day

We also have

$h = \$ {.02}$ per gallon per day

$K = \$ {20}$ per order

$$
L = 2\text{ days }
$$

$$
{c}_{1} = \$ 3\text{ per gallon }
$$

${c}_{2} = \$ {2.50}$ per gallon

$q = {1000}$ gallons

Step 1. Compute

$$
{y}_{m} = \sqrt{\frac{2KD}{h}} = \sqrt{\frac{2 \times  {20} \times  {187.5}}{.02}} = {612.37}\text{ gallons }
$$

Because $q = {1000}$ is larger than ${y}_{m} = {612.37}$ , we move to step 2 .

Step 2. Determine $Q$ .

$$
{\mathrm{{TCU}}}_{1}\left( {y}_{m}\right)  = {c}_{1}D + \frac{KD}{{y}_{m}} + \frac{h{y}_{m}}{2}
$$

$$
= 3 \times  {187.5} + \frac{{20} \times  {187.5}}{612.37} + \frac{{.02} \times  {612.37}}{2}
$$

$$
= {574.75}
$$

Hence, the $Q$ -equation is calculated as

$$
{Q}^{2} + \left( \frac{2 \times  \left( {{2.5} \times  {187.5} - {574.75}}\right) }{.02}\right) Q + \frac{2 \times  {20} \times  {187.5}}{.02} = 0
$$

or

$$
{Q}^{2} - {10},{599.74Q} + {375},{000} = 0
$$

The solution $Q = {10},{564.25}\left( { > {y}_{m}}\right)$ defines the zones as

$$
\text{ Zone I } = \left( {0,{612.37}}\right)
$$

$$
\text{ Zone II } = \left( {{612.37},{10},{564.25}}\right)
$$

$$
\text{ Zone III } = \left( {{10},{564.25},\infty }\right)
$$

Now, $q\left( { = {1000}}\right)$ falls in zone II, which yields the optimal order quantity ${y}^{ * } = q =$ 1000 gallons.

Given a 2-day lead time, the reorder point is ${2D} = 2 \times  {187.5} = {375}$ gallons. Thus, the optimal inventory policy is

Order 1000 gallons when the inventory level drops to 375 gallons.

## Excel Moment

File excelEOQ.xls solves the discount price situation as a special case of template in Figure 13.3. Enter applicable data in the input data section C3:C11. The output gives the optimal inventory policy as well as all the intermediate calculations of the model.

#### 13.3.3 Multi-Item EOQ with Storage Limitation ^multiitem

This model deals with multiple items whose individual inventory fluctuations follow the pattern as in Figure 13.1 (no shortage allowed). The difference is that the items compete for a limited storage space. ^competespace

Define for item $i, i = 1,2,\ldots , n$ ,

${D}_{i} =$ Demand rate

${K}_{i} =$ Setup cost

${h}_{i} =$ Unit holding cost per unit time

${y}_{i} =$ Order quantity

${a}_{i} =$ Storage area requirement per inventory unit

$A =$ Maximum available storage area for all $n$ items

Under the assumption of no shortage, the mathematical model representing the inventory situation is given as

$$
\text{ Minimize }\operatorname{TCU}\left( {{y}_{1},{y}_{2},\ldots ,{y}_{n}}\right)  = \mathop{\sum }\limits_{{i = 1}}^{n}\left( {\frac{{K}_{i}{D}_{i}}{{y}_{i}} + \frac{{h}_{i}{y}_{i}}{2}}\right)
$$

subject to

$$
\mathop{\sum }\limits_{{i = 1}}^{n}{a}_{i}{y}_{i} \leq  A
$$

$$
{y}_{i} > 0, i = 1,2,\ldots , n
$$

To solve the problem, we try the unconstrained solution first:

$$
{y}_{i}^{ * } = \sqrt{\frac{2{K}_{i}{D}_{i}}{{h}_{i}}}, i = 1,2,\ldots , n
$$

If the solution satisfies the constraint, then the process ends. Otherwise, the constraint is binding and must be accounted for.

In previous editions of this book, we used the (rather involved) Lagrangean algorithm and trial-and-error calculations to find the constrained optimum solution. With the availability of powerful packages (such as AMPL and Solver), the problem can be solved directly as a nonlinear program, as will be demonstrated in the following example.

## Example 13.3-3

The following data describe three inventory items:

| Item $i$ | ${K}_{i}\left( \mathbb{s}\right)$ | ${D}_{i}$ (units per day) | ${h}_{i}\left( \$ \right)$ | ${a}_{1}\left( {\mathrm{{ft}}}^{2}\right)$ |
|---|---|---|---|---|
| 1 | 10 | 2 | .30 | 1 |
| 2 | 5 | 4 | .10 | 1 |
| 3 | 15 | 4 | .20 | 1 |
| Total available storage area $= {25}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {25}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {25}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {25}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {25}{\mathrm{{ft}}}^{2}$ |

The unconstrained optimum values, ${y}_{i}^{ * } = \sqrt{\frac{2{K}_{i}{D}_{i}}{{h}_{i}}}, i = 1,2,3$ , are 11.55,20.00, and 24.49 units, respectively, which violate the storage constraint ${y}_{1} + {y}_{2} + {y}_{3} \leq  {25}$ . The constrained problem can be solved as a nonlinear program using Solver or AMPL as explained below.

The optimum solution is ${y}_{1}^{ * } = {6.34}$ units, ${y}_{2}^{ * } = {7.09}$ units, ${y}_{3}^{ * } = {11.57}$ units, and cost $=$ \$13.62/day.

## Solver Moment

Figure 13.6 shows how Solver can be used to solve Example 13.3-3 as a nonlinear program (file solverConstrEOQ.xls). Details of the formulas used in the template and of the Solver parameters are shown in the figure. As with most nonlinear programs, initial solution values must be given (in this template, ${y}_{1} = {y}_{2} = {y}_{3} = 1$ in row 9). A nonzero initial value is mandatory because the objective function includes division by ${y}_{i}$ . Indeed, it may be a good idea to replace ${K}_{i}{D}_{i}/{y}_{i}$ with ${K}_{i}{D}_{i}/\left( {{y}_{i} + \Delta }\right)$ , where $\Delta$ is a very small positive value, to avoid division by zero during the iterations. In general, different initial values may be needed before a (local optimum) solution is found. In this example, the resulting solution is the global optimum because the objective function and the constraints are well behaved (convex objective function and convex solution space).

## AMPL Moment

The AMPL nonlinear model for the general multi-item EOQ with storage limitation (file amplConstrEOQ.txt) is explained in Figure C.16 in Appendix C on the website.

FIGURE 13.6

Solver template for Example 13.3-3 (file solverConstrEOQ.xls)

![bo_d56m533ef24c73bhe630_15_482_1419_904_742_0.jpg](bo_d56m533ef24c73bhe630_15_482_1419_904_742_0.jpg)

### 13.4 DYNAMIC EOQ MODELS ^dynamiceoq

These models differ from those in Section 13.3 in two respects:

1. The inventory level is reviewed periodically over a finite number of equal periods.

2. The demand per period, though deterministic, is dynamic, in that it varies from one period to the next.

A situation in which dynamic deterministic demand occurs is materials requirement planning (MRP). The idea of MRP is described by an example. Suppose that the quarterly demands over the next year for two final models, ${M1}$ and ${M2}$ , of a given product are 100 and 150 units, respectively. Deliveries of the quarterly lots are made at the end of each quarter. The production lead time is 2 months for ${M1}$ and 1 month for ${M2}$ . Each unit of ${M1}$ and ${M2}$ uses 2 units of a subassembly $S$ . The lead time for the production of $S$ is 1 month.

Figure 13.7 depicts the production schedules for ${M1}$ and ${M2}$ . The schedules start with the quarterly demand for the two models (shown by solid arrows) occurring at the end of months 3,6,9, and 12. Given the lead times for ${M1}$ and ${M2}$ , the dashed arrows show the planned starts of each production lot.

To start the production of the two models on time, the delivery of subassembly $S$ must coincide with the occurrence of the dashed ${M1}$ and ${M2}$ arrows. This information is shown by the solid arrows in the $S$ -chart, where the resulting $S$ -demand is 2 units per unit of ${M1}$ or ${M2}$ . Using a lead time of 1 month, the dashed arrows on the $S$ -chart give the production schedules for $S$ . From these two schedules, the combined demand for $S$ corresponding to ${M1}$ and ${M2}$ can then be determined as shown at the bottom of Figure 13.7. The resulting variable but known demand for $S$ is typical of the situation where dynamic EOQ applies.

FIGURE 13.7

Example of dynamic demand generated by MRP

![bo_d56m533ef24c73bhe630_16_321_1368_1311_809_0.jpg](bo_d56m533ef24c73bhe630_16_321_1368_1311_809_0.jpg)

Two models are presented in this section. The first model assumes no setup (ordering) cost, and the second one does. This seemingly "small" variation makes a difference in the complexity of the model.

#### 13.4.1 No-Setup EOQ Model ^nosetup

This model involves a planning horizon of $n$ equal periods. Each period has a limited production capacity with one or more production levels (e.g., regular time and overtime represent two production levels). ^productionlevels A current period may produce more than its immediate demand to satisfy the need in later periods, in which case an inventory holding cost takes place.

The general assumptions of the model are as follows:

1. No setup cost is incurred in any period.

2. No shortage is allowed.

3. The unit production cost function in any period either is constant or has increasing (convex) marginal costs. ^convexcost

4. The unit holding cost in any period is constant.

The absence of shortage signifies that delayed production in future periods cannot fill the demand in a current period. This assumption requires the cumulative production capacity for periods $1,2,\ldots$ , and $i$ to equal at least the cumulative demand for the same periods.

Figure 13.8 illustrates the unit production cost function with increasing margins. For example, regular time and overtime production correspond to two levels where the unit production cost during overtime exceeds that regular time.

The $n$ -period problem can be formulated as a transportation model (see Chapter 5) with ${kn}$ sources and $n$ destinations, where $k$ is the number of production levels per period (e.g., $k = 2$ if each period uses regular time and overtime). ^transportation The production capacity of each of the ${kn}$ production-level sources equals the supply amounts. The demand amounts are specified by each period's demand. The unit "transportation" cost from a source to a destination is the sum of the applicable production and holding costs per unit. The solution of the problem as a transportation model determines the minimum-cost production amounts in each production level.

![bo_d56m533ef24c73bhe630_17_369_1691_643_497_0.jpg](bo_d56m533ef24c73bhe630_17_369_1691_643_497_0.jpg)

FIGURE 13.8

Convex unit production cost function

The resulting transportation model can be solved without using the familiar transportation technique presented in Chapter 5. The validity of the new solution algorithm rests on the special assumptions of no shortage and a convex production-cost function. ^transportation

## Example 13.4-1

Metalco produces draft deflectors for use in home fireplaces during the months of December to March. The demand starts slow, peaks in the middle of the season, and tapers off toward the end. Because of the popularity of the product, Metalco may use overtime to satisfy the demand. The following table provides the production capacities and the demands for the four winter months:

| Month | Capacity | Capacity | Demand (units) |
|---|---|---|---|
| Regular (units) | Overtime (units) |  |  |
| 1 | 90 | 50 | 100 |
| 2 | 100 | 60 | 190 |
| 3 | 120 | 80 | 210 |
| 4 | 110 | 70 | 160 |

Unit production cost in any period is $\$ 6$ during regular time and $\$ 9$ during overtime. Holding cost per unit per month is \$.10.

To ensure that the model has a feasible solution when shortage is not allowed, each month's cumulative supply cannot be smaller than its cumulative demand, as the following table shows:

| Month | Cumulative supply              | Cumulative demand       |
| ----- | ------------------------------ | ----------------------- |
| 1     | ${90} + {50} = {140}$          | 100                     |
| 2     | ${140} + {100} + {60} = {300}$ | ${100} + {190} = {290}$ |
| 3     | ${300} + {120} + {80} = {500}$ | ${290} + {210} = {500}$ |
| 4     | ${500} + {110} + {70} = {680}$ | ${500} + {160} = {660}$ |

Table 13.2 summarizes the model and its solution. The symbols ${R}_{i}$ and ${O}_{i}$ represent regular and overtime production levels in period $i, i = 1,2,3,4$ . Because cumulative supply at period 4 exceeds cumulative demand, a dummy surplus destination is added to balance the model as shown in Table 13.2. All the "transportation" routes from a previous to a current period are blocked because no shortage is allowed.

The unit "transportation" cost is the sum of applicable production and holding costs. For example, unit cost from ${R}_{1}$ to period 1 equals unit production cost only $\left( { = \$ 6}\right)$ , whereas unit cost from ${O}_{1}$ to period 4 equals unit production cost in ${O}_{1}$ plus unit holding cost from period 1 to period 4-that is, $\$ 9 + \left( {\$ {.1} + \$ {.1} + \$ {.1}}\right)  = \$ {9.30}$ . The unit cost to any surplus destination is zero.

The model is solved starting at column 1 and ending at the surplus column. For each column, the demand is satisfied giving priority to its cheapest routes. ${}^{5}$ ^cheapestroutes For column 1, route $\left( {{R}_{1},1}\right)$ is the cheapest and is thus assigned the maximum feasible amount $= \min \{ {90},{100}\}  = {90}$ units. This assignment leaves 10 unsatisfied units in column 1. The next-cheapest route in column 1 is $\left( {{O}_{1},1}\right)$ , to which ${10}\left( { = \min \{ {50},{10}\} }\right)$ are assigned. The demand for period 1 is now satisfied.

---

${}^{5}$ For a proof of the optimality of this procedure, see S. M. Johnson,"Sequential Production Planning over Time at Minimum Cost," Management Science, Vol. 3, pp. 435-437, 1957.

---

TABLE 13.2 Solution of Example 13.4-1

![bo_d56m533ef24c73bhe630_19_380_262_1101_880_0.jpg](bo_d56m533ef24c73bhe630_19_380_262_1101_880_0.jpg)

Next, we move to column 2. The assignments in this column occur in the following order: 100 units to $\left( {{R}_{2},2}\right) ,{60}$ units to $\left( {{O}_{2},2}\right)$ , and 30 units to $\left( {{O}_{1},2}\right)$ . The unit costs of these assignments are $\$ 6,\$ 9$ , and $\$ {9.10}$ , respectively. We did not use the route $\left( {{R}_{1},2}\right)$ , whose unit cost is $\$ {6.10}$ , because all the supply of ${R}_{1}$ has been assigned to period 1 already.

Continuing in the same manner, we satisfy the demands of column 3 and then column 4. The optimum solution (shown in boldface in Table 13.2) is summarized as follows:

| Period | Production Schedule |
|---|---|
| Regular 1 | Produce 90 units for period 1. |
| Overtime 1 | Produce 50 units: 10 units for period 1, 30 for 2, and 10 for 3. |
| Regular 2 | Produce 100 units for period 2. |
| Overtime 2 | Produce 60 units for period 2. |
| Regular 3 | Produce 120 units for period 3. |
| Overtime 3 | Produce 80 units for period 3. |
| Regular 4 | Produce 110 units for period 4. |
| Overtime 4 | Produce 50 units for period 4, with 20 units of idle capacity. |

The associated total cost is ${90} \times  \$ 6 + {10} \times  \$ 9 + {30} \times  \$ {9.10} + {100} \times  \$ 6 + {60} \times  \$ 9 + {10} \times \; \$ {9.20} + {120} \times  \$ 6 + {80} \times  \$ 9 + {110} \times  \$ 6 + {50} \times  \$ 9 = \$ {4685}.$

#### 13.4.2 Setup EOQ Model ^setup

In this situation, no shortage is allowed, and a setup cost is incurred each time a new production lot is started. Two solution methods will be presented: an exact dynamic programming algorithm and a heuristic.

Figure 13.9 summarizes the inventory situation schematically. The symbols shown in the figure are defined for period $i, i = 1,2,\ldots , n$ , as

${z}_{i} =$ Amount ordered

${D}_{i} =$ Demand for period $i$

${x}_{i} =$ Inventory at the start of period $i$

The cost elements of the situation are defined as

${K}_{i} =$ Setup cost in period $i$

${h}_{i} =$ Unit inventory holding cost from period $i$ to $i + 1$

The associated production cost function for period $i$ is

$$
{C}_{i}\left( {z}_{i}\right)  = \left\{  \begin{array}{ll} 0, & {z}_{i} = 0 \\  {K}_{i} + {c}_{i}\left( {z}_{i}\right) , & {z}_{i} > 0 \end{array}\right.
$$

The function ${c}_{i}\left( {z}_{i}\right)$ is the marginal production cost function, given ${z}_{i}$ .

General dynamic programming algorithm. In the absence of shortage, the inventory model is based on minimizing the sum of production and holding costs for all $n$ periods. For simplicity, we will assume that the holding cost for period $i$ is based on end-of-period inventory, defined as

$$
{x}_{i + 1} = {x}_{i} + {z}_{i} - {D}_{i}
$$

For the forward recursive equation, the state at stage (period) $i$ is defined as ${x}_{i + 1}$ , the end-of-period inventory level. ^endinventory In the extreme case, the remaining inventory, ${x}_{i + 1}$ , can satisfy the demand for all the remaining periods-that is,

$$
0 \leq  {x}_{i + 1} \leq  {D}_{i + 1} + \ldots  + {D}_{n}
$$

FIGURE 13.9

Elements of the dynamic inventory model with setup cost

![bo_d56m533ef24c73bhe630_20_387_1956_1182_214_0.jpg](bo_d56m533ef24c73bhe630_20_387_1956_1182_214_0.jpg)

Let ${f}_{i}\left( {x}_{i + 1}\right)$ be the minimum inventory cost for periods $1,2,\ldots$ , and $i$ given the end-of-period inventory ${x}_{i + 1}$ . The forward recursive equation is ^recursive

$$
{f}_{1}\left( {x}_{2}\right)  = \mathop{\min }\limits_{{{z}_{1} = {D}_{1} + {x}_{2} - {x}_{1}}}\left\{  {{C}_{1}\left( {z}_{1}\right)  + {h}_{1}{x}_{2}}\right\}
$$

$$
{f}_{i}\left( {x}_{i + 1}\right)  = \mathop{\min }\limits_{{0 \leq  {z}_{i} \leq  {D}_{i} + {x}_{i + 1}}}\left\{  {{C}_{i}\left( {z}_{i}\right)  + {h}_{i}{x}_{i + 1} + {f}_{i - 1}\left( {{x}_{i + 1} + {D}_{i} - {z}_{i}}\right) }\right\}  , i = 2,3,\ldots , n
$$

Note that for period $1,{z}_{1}$ exactly equals ${D}_{1} + {x}_{2} - {x}_{1}$ . For $i > 1,{z}_{i}$ can be zero because ${D}_{i}$ can be satisfied from the production in preceding periods.

## Example 13.4-2

The following table provides the data for a 3-period inventory situation:

| Period  $i$ | Demand ${D}_{i}$ (units) | Setup cost ${K}_{i}\left( \mathbb{s}\right)$ | Holding cost ${h}_{i}\left( \mathbb{s}\right)$ |
|---|---|---|---|
| 1 | 3 | 3 | 1 |
| 2 | 2 | 7 | 3 |
| 3 | 4 | 6 | 2 |

The demand occurs in discrete units, and the starting inventory is ${x}_{1} = 1$ unit. The unit production cost, ${c}_{i}\left( {z}_{i}\right)$ , is $\$ {10}$ for the first 3 units and $\$ {20}$ for each additional unit-that is,

$$
{c}_{i}\left( {z}_{i}\right)  = \left\{  \begin{array}{ll} {10}{z}_{i}, & 0 \leq  {z}_{i} \leq  3 \\  {30} + {20}\left( {{z}_{i} - 3}\right) , & {z}_{i} \geq  4 \end{array}\right.
$$

Determine the optimal inventory policy.

Period 1: ${D}_{1} = 3,0 \leq  {x}_{2} \leq  2 + 4 = 6,{z}_{1} = {x}_{2} + {D}_{1} - {x}_{1} = {x}_{2} + 2$

|  |  | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | ${C}_{1}\left( {z}_{1}\right)$ | Optimal solution | Optimal solution |
|---|---|---|---|---|---|---|---|---|---|---|
| ${z}_{1} = 2$ | 3 | 4 | 5 | 6 | 7 | 8 |  |  |  |  |
| ${x}_{2}$ | ${h}_{1}{x}_{2}$ | ${C}_{1}\left( {z}_{1}\right)  = {23}$ | 33 | 53 | 73 | 93 | 113 | 133 | ${f}_{1}\left( {x}_{2}\right)$ | ${z}_{1}^{ * }$ |
| 0 | 0 | 23 |  |  |  |  |  |  | 23 | 2 |
| 1 | 1 |  | 34 |  |  |  |  |  | 34 | 3 |
| 2 | 2 |  |  | 55 |  |  |  |  | 55 | 4 |
| 3 | 3 |  |  |  | 76 |  |  |  | 76 | 5 |
| 4 | 4 |  |  |  |  | 97 |  |  | 97 | 6 |
| 5 | 5 |  |  |  |  |  | 118 |  | 118 | 7 |
| 6 | 6 |  |  |  |  |  |  | 139 | 139 | 8 |

Note that because ${x}_{1} = 1$ , the smallest value of ${z}_{1}$ is ${D}_{1} - {x}_{1} = 3 - 1 = 2$ .

Period 2: ${D}_{2} = 2,0 \leq  {x}_{3} \leq  4,0 \leq  {z}_{2} \leq  {D}_{2} + {x}_{3} = {x}_{3} + 2$

| ${x}_{3}$                           | ${h}_{2}{x}_{3}$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | Optimal solution | Optimal solution |
| ----------------------------------- | ---------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | ---------------- | ---------------- |
| ${z}_{2} = 0$                       | 1                | 2                                                                                                     | 3                                                                                                     | 4                                                                                                     | 5                                                                                                     | 6                                                                                                     |                                                                                                       |                                                                                                       |                  |                  |
| ${C}_{2}\left( {z}_{2}\right)  = 0$ | 17               | 27                                                                                                    | 37                                                                                                    | 57                                                                                                    | 77                                                                                                    | 97                                                                                                    | ${f}_{2}\left( {x}_{3}\right)$                                                                        | ${z}_{2}^{ * }$                                                                                       |                  |                  |
| 0                                   | 0                | $0 + {55}$                                                                                            | 17 + 34                                                                                               | 27 + 23                                                                                               |                                                                                                       |                                                                                                       |                                                                                                       |                                                                                                       | 50               | 2                |
|                                     | $= {55}$         | $= {51}$                                                                                              | $= {50}$                                                                                              |                                                                                                       |                                                                                                       |                                                                                                       |                                                                                                       |                                                                                                       |                  |                  |
| 1                                   | 3                | $3 + {76}$                                                                                            | 20 + 55                                                                                               | 30 + 34                                                                                               | 40 + 23                                                                                               |                                                                                                       |                                                                                                       |                                                                                                       | 63               | 3                |
|                                     | $= {79}$         | $= {75}$                                                                                              | $= {64}$                                                                                              | $= {63}$                                                                                              |                                                                                                       |                                                                                                       |                                                                                                       |                                                                                                       |                  |                  |
| 2                                   | 6                | 6 + 97                                                                                                | 23 + 76                                                                                               | 33 + 55                                                                                               | 43 + 34                                                                                               | 63 + 23                                                                                               |                                                                                                       |                                                                                                       | 77               | 3                |
|                                     |                  | $= {103}$                                                                                             | $= {99}$                                                                                              | $= {88}$                                                                                              | $= {77}$                                                                                              | $= {86}$                                                                                              |                                                                                                       |                                                                                                       |                  |                  |
| 3                                   | 9                | 9 + 118                                                                                               | 26 + 97                                                                                               | 36 + 76                                                                                               | 46 + 55                                                                                               | 66 + 34                                                                                               | ${86} + {23}$                                                                                         |                                                                                                       | 100              | 4                |
|                                     |                  | $= {127}$                                                                                             | $= {123}$                                                                                             | $= {112}$                                                                                             | $= {101}$                                                                                             | $= {100}$                                                                                             | $= {109}$                                                                                             |                                                                                                       |                  |                  |
| 4                                   | 12               | ${12} + {139}$                                                                                        | 29 + 118                                                                                              | 39 + 97                                                                                               | 49 + 76                                                                                               | 69 + 55                                                                                               | ${89} + {34}$                                                                                         | 109 + 23                                                                                              | 123              | 5                |
|                                     |                  | $= {151}$                                                                                             | $= {147}$                                                                                             | $= {136}$                                                                                             | $= {125}$                                                                                             | $= {124}$                                                                                             | $= {123}$                                                                                             | $= {132}$                                                                                             |                  |                  |

Period 3: ${D}_{3} = 4,{x}_{4} = 0,0 \leq  {z}_{3} \leq  {D}_{3} + {x}_{4} = 4$

| ${x}_{4}$ | ${h}_{3}{x}_{4}$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | Optimal solution | Optimal solution |
|---|---|---|---|---|---|---|---|
| ${z}_{3} = 0$ | 1 | 2 | 3 | 4 |  |  |  |  |
| ${C}_{3}\left( {z}_{3}\right)  = 0$ | 16 | 26 | 36 | 56 | ${f}_{3}\left( {x}_{4}\right)$ | ${z}_{3}^{ * }$ |  |  |
| 0 | 0 | 0 + 123  $= {123}$ | 16 + 100  $= {116}$ | 26 + 77  $= {103}$ | 36 + 63  $= {99}$ | 56 + 50  $= {106}$ | 99 | 3 |

The optimum solution is read in the following manner:

$$
\left( {{x}_{4} = 0}\right)  \rightarrow  {z}_{3} = 3 \rightarrow  \left( {{x}_{3} = 0 + 4 - 3 = 1}\right)  \rightarrow  {z}_{2} = 3
$$

$$
\rightarrow  \left( {{x}_{2} = 1 + 2 - 3 = 0}\right)  \rightarrow  {z}_{1} = 2
$$

Thus, the optimum solution is ${z}_{1}^{ * } = 2,{z}_{2}^{ * } = 3$ , and ${z}_{3}^{ * } = 3$ , with a total cost of \$99.

## Excel Moment

Template excelDPInv.xls is designed to solve the general DP inventory problem with up to 10 periods. The design of the spreadsheet is similar to that of excelKnapsack.xls given in Section 12.3.1, where the computations are carried out one stage a time and user input is needed to link successive stages.

Figure 13.10 shows the application of excelDPInv.xls to Example 13.4-2. The input data are entered for each stage. The computations start with period 1. Note how the cost function ${c}_{i}\left( {z}_{i}\right)$ is entered in row 3: (G3 = 10, H3 = 20, I3 = 3) means that the unit cost is \$10 for the first three items and \$20 for additional items. Note also that the amount entered for ${D}_{1}$ must be the net after the initial inventory has been written off $\left( { = 3 - {x}_{1} = 3 - 1 = 2}\right)$ . Additionally, you need to create the feasible values of the variable ${z}_{1}$ . The spreadsheet automatically checks if the entered values are correct, and issues self-explanatory messages in row 6 (yes, no, or delete).

Period 1:

| 2 | A | B | C | D | E | F | G | H | 1 | J | K | S | T U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model | General (Forward) Dynamic Programming Inventory Model |
| 2 | 1 | Number of periods, N- | Number of periods, N- | Number of periods, N- | 3 | Current | period- | 1 |  |  |  | Optimum | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution |
| 3 | N | K1= | 3 | h1= | 1 | c1(z1)= | 10 | 20 | 3 |  |  | Summary | Summary | Summary | Summary | Summary | Summary |  |
| 4 | P | Period | 1 | 2 | 3 |  |  |  |  |  |  | ✘ | f | Z | ✘ | f | Z |  |
| 5 | U | D(1 to 3)- | 2 | 2 | 4 |  |  |  |  |  |  | Period 1 | Period 1 | Period 1 |  |  |  |  |
| 6 | T | Are z1 values correct? | Are z1 values correct? | Are z1 values correct? | yes | yes | yes | yes | yes | yes | yes | 0 | 23 | 2 |  |  |  |  |
| 7 |  | Period 0 | z1= | z1= | 2 | 3 | 4 | 5 | 6 | 7 | 8 | Period1 | 1 | 34 | 3 |  |  |  |
| 8 |  | f0 | C1(z1)= | C1(z1)= | 23 | 33 | 53 | 73 | 93 | 113 | 133 | f1 z1 | 2 | 55 | 4 |  |  |  |
| 9 | S |  | x2= | 0 | 23 | 1111111 | 1111111 | 1111111 | 1111111 | 1111111 | 1111111 | 23 | 2 3 | 76 | 5 |  |  |  |
| 10 | T |  | x2= | 1 | 1111111 | 34 | 1111111 | 1111111 | 1111111 | 1111111 | 1111111 | 34 | 3 4 | 97 | 6 |  |  |  |
| 11 | A |  | x2= | 2 | 1111111 | 1111111 | 55 | 1111111 | 1111111 | 1111111 | 1111111 | 55 | 4 5 | 118 | 7 |  |  |  |
| 12 | G |  | x2= | 3 | 1111111 | 1111111 | 1111111 | 76 | 1111111 | 1111111 | 1111111 | 76 | 5 6 | 139 | B |  |  |  |
| 13 | E |  | x2= | 4 | 1111111 | 1111111 | 1111111 | 1111111 | 97 | 1111111 | 1111111 | 97 | 6 |  |  |  |  |  |
| 14 |  |  | x2= | 5 | 1111111 | 1111111 | 1111111 | 1111111 | 1111111 | 118 | 1111111 | 118 | 7 |  |  |  |  |  |
| 15 | C |  | x2= | 6 | 1111111 | 1111111 | 1111111 | 111111 | 1111111 | 1111111 | 139 | 139 | 8 |  |  |  |  |  |

Period 2:

| 7 | A | B | C | D | E | F | G | H | 1 | J | K | S | T | U | V | W | X | Y | 2 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model |
| 2 | 1 | Number of periods, N- | Number of periods, N- | Number of periods, N- | 3 | Current | period- | 2 |  |  |  |  |  | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution |
| 3 | N | K2- | 7 | h2= | 3 | c2(z2)- | 10 | 20 | 3 |  |  |  |  | Summary | Summary | Summary | Summary | Summary | Summary |
| 4 | P | Period | 1 | 2 | 3 |  |  |  |  |  |  |  |  | ✘ | f | Z | ✘ | f | Z |
| 5 | U | D(1 to 3)= | 2 | 2 | 4 |  |  |  |  |  |  |  |  | Period 1 | Period 1 | Period 1 | Period 2 | Period 2 | Period 2 |
| 6 | T | Are z2 values correct? | Are z2 values correct? | Are z2 values correct? | yes | yes | yes | yes | yes | yes | yes | Optimum | Optimum | 0 | 23 | 2 | 0 | 50 | 2 |
| 7 |  | Period 1 | z2- | z2- | 0 | 1 | 2 | 3 | 4 | 5 | 6 | Period2 | Period2 | 1 | 34 | 3 | 1 | 63 | 3 |
| 8 |  | f1 | C2(z2)= | C2(z2)= | 0 | 17 | 27 | 37 | 57 | 77 | 97 | f2 | z2 | 2 | 55 | 4 | 2 | 77 | 3 |
| 9 | S | 23 | x3= | 0 | 55 | 51 | 50 | 111111 | 1111111 | 1111111 | 1111111 | 50 | 2 | 3 | 76 | 5 | 3 | 100 | 4 |
| 10 | T | 34 | x3= | 1 | 79 | 75 | 64 | 63 | 1111111 | 1111111 | 1111111 | 63 | 3 | 4 | 97 | 6 | 4 | 123 | 5 |
| 11 | A | 55 | x3= | 2 | 103 | 99 | 88 | 77 | 86 | 1111111 | 1111111 | 77 | 3 | 5 | 118 | 7 |  | Period 3 |  |
| 12 | G | 76 | x3= | 3 | 127 | 123 | 112 | 101 | 100 | 109 | 1111111 | 100 | 4 | 6 | 139 | 8 |  |  |  |
| 13 | E | 97 | x3= | 4 | 151 | 147 | 136 | 125 | 124 | 123 | 132 | 123 | 5 |  |  |  |  |  |  |
| 14 |  | 118 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| 15 | C | 139 |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |

Period 3:

|  | A | B | C | D | E | F | G | H | 1 | J | K | S | T U | V | W | X | Y | Z |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model | 1 General (Forward) Dynamic Programming Inventory Model |
| 2 | I | Number of periods, N= | Number of periods, N= | Number of periods, N= | 3 | Current | period= | 3 |  |  |  |  | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution | Optimum solution |
| 3 | N | K3= | 6 | h3= | 2 | c3(z3)- | 10 | 20 | 3 |  |  |  | Summary | Summary | Summary | Summary | Summary | Summary |
| 4 | P | Period | 7 | 2 | 3 |  |  |  |  |  |  |  | ✘ | f | Z | ✘ | f | Z |
| 5 | U | D(1 to 3)= | 2 | 2 | 4 |  |  |  |  |  |  |  | Period 1 | Period 1 | Period 1 | Period 2 | Period 2 | Period 2 |
| 6 | T | Are z3 values correct? | Are z3 values correct? | Are z3 values correct? | yes | yes | yes | yes | yes |  |  | Optimum | 0 | 23 | 2 | 0 | 50 | 2 |
| 7 |  | Period 2 | z3= | z3= | 0 | 1 | 2 | 3 | 4 |  |  | Period3 | 1 | 34 | 3 | 1 | 63 | 3 |
| B |  | f2 | C3(z3)= | C3(z3)= | 0 | 16 | 26 | 36 | 56 |  |  | f3 z3 | 2 | 55 | 4 | 2 | 77 | 3 |
| 9 | S | 50 | x4= | 0 | 123 | 116 | 103 | 99 | 106 |  |  | 99 | 3 3 | 76 | 5 | 3 | 100 | 4 |
| 10 | T | 63 |  |  |  |  |  |  |  |  |  |  | 4 | 97 | 6 | 4 | 123 | 5 |
| 11 | A | 77 |  |  |  |  |  |  |  |  |  |  | 5 | 118 | 7 | Period 3 | Period 3 | Period 3 |
| 12 | G | 100 |  |  |  |  |  |  |  |  |  |  | 6 | 139 | 8 | 0 | 99 | 3 |

FIGURE 13.10

Excel DP solution of Example 13.4-2 (file excelDPInv.xls)

Once all input data have been entered, the optimum values of ${f}_{i}$ and ${z}_{i}$ for the stage are given in columns S and T. Next, a permanent record for period 1 solution, $\left( {{x}_{1},{f}_{1},{z}_{1}}\right)$ , is created in the optimum solution summary section of the spreadsheet, as Figure 13.10 shows. This requires copying D9:D15 and S9:T15 and then pasting them using pastespecial + values (you may need to review the proper procedure for creating the permanent record given in conjunction with excelKnapsack.xls in Section 12.3.1).

Next, to prepare for stage 2, copy ${f}_{1}$ from the permanent record and paste it in column A, as shown in Figure 13.10. All that is needed now is to update the input data for period 2. The process is repeated for period 3.

Dynamic programming algorithm with constant or decreasing marginal costs. The general DP given above is applicable with any cost function. This generalization dictates that the state ${x}_{i}$ and the alternatives ${z}_{i}$ at stage $i$ assume values in increments of 1, which could result in large tableaus when the demand amounts are large. ^constantcosts

A special case of the general DP model holds promise in reducing the volume of computations. In this special situation, both the unit production and the unit holding costs are nonincreasing (concave) functions of the production quantity and the inventory level, respectively. This situation typically occurs when the unit cost function is constant or when quantity discount is allowed.

Under the given conditions, it can be proved that ${}^{6}$

1. Given zero initial inventory $\left( {{x}_{1} = 0}\right)$ , it is optimal to satisfy the demand in any period $i$ either from new production or from entering inventory, but never from both-that is, ${z}_{i}{x}_{i} = 0$ . ^productionorinventory (For the case with positive initial inventory, ${x}_{1} > 0$ , the amount can be written off from the demands of the successive periods until it is exhausted.)

2. The optimal production quantity, ${z}_{i}$ , for period $i$ must either be zero or it must satisfy the exact demand for one or more contiguous succeeding periods. ^contiguous

## Example 13.4-3

A four-period inventory model operates with the following data:

| Period $i$ | Demand ${D}_{i}$ (units) | Setup cost ${K}_{i}\left( \mathbb{s}\right)$ |
|---|---|---|
| 1 | 76 | 98 |
| 2 | 26 | 114 |
| 3 | 90 | 185 |
| 4 | 67 | 70 |

The initial inventory ${x}_{1}$ is 15 units, the unit production cost is $\$ 2$ , and the unit holding cost per period is $\$ 1$ for all the periods. (For simplicity, the unit production and holding costs are the same for all the periods.)

The solution is determined by the forward algorithm given previously, except that the values of ${x}_{i + 1}$ and ${z}_{i}$ now assume "lump" sums rather than in increments of one. Because ${x}_{1} = {15}$ , the demand for the first period is adjusted to ${76} - {15} = {61}$ units.

Period 1. ${D}_{1} = {61}$

| ${x}_{2}$ | ${h}_{1}{x}_{2}$ | ${C}_{1}\left( {z}_{1}\right)  + {h}_{1}{x}_{2}$ | ${C}_{1}\left( {z}_{1}\right)  + {h}_{1}{x}_{2}$ | ${C}_{1}\left( {z}_{1}\right)  + {h}_{1}{x}_{2}$ | ${C}_{1}\left( {z}_{1}\right)  + {h}_{1}{x}_{2}$ | Optimal solution | Optimal solution |
|---|---|---|---|---|---|---|---|
| ${z}_{1} = {61}$ | 87 | 177 | 244 |  |  |  |  |
| ${C}_{1}\left( {z}_{1}\right)  = {220}$ | 272 | 452 | 586 | ${f}_{1}\left( {x}_{2}\right)$ | ${z}_{1}^{ * }$ |  |  |
| 0 | 0 | 220 |  |  |  | 220 | 61 |
| 26 | 26 |  | 298 |  |  | 298 | 87 |
| 116 | 116 |  |  | 568 |  | 568 | 177 |
| 183 | 183 |  |  |  | 769 | 769 | 244 |
| Order in 1 for | Order in 1 for | 1 | 1,2 | 1,2,3 | 1,2,3,4 |  |  |

---

${}^{6}$ See H. Wagner and T. Whitin,"Dynamic Version of the Economic Lot Size Model," Management Science, Vol. 5, pp. 89-96, 1958. The optimality proof imposes the restrictive assumption of constant and identical cost functions for all the periods. The assumption was later relaxed by A. Veinott Jr. to allow different concave cost functions.

---

Period 2. ${D}_{2} = {26}$

| ${x}_{3}$ | ${h}_{2}{x}_{3}$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | ${C}_{2}\left( {z}_{2}\right)  + {h}_{2}{x}_{3} + {f}_{1}\left( {{x}_{3} + {D}_{2} - {z}_{2}}\right)$ | Optimal solution | Optimal solution |
|---|---|---|---|---|---|---|---|
| ${z}_{2} = 0$ | 26 | 116 | 183 |  |  |  |  |
| ${C}_{2}\left( {z}_{2}\right)  = 0$ | 166 | 346 | 480 | ${f}_{2}\left( {x}_{3}\right)$ | ${z}_{2}^{ * }$ |  |  |
| 0 | 0 | 0 + 298 | 166 + 220 |  |  | 298 | 0 |
|  |  | $= {298}$ | $= {386}$ |  |  |  |  |
| 90 | 90 | 90 + 568 |  | 436 + 220 |  | 656 | 116 |
|  |  | $= {658}$ |  | $= {656}$ |  |  |  |
| 157 | 157 | 157 + 769 |  |  | 637 + 220 | 857 | 183 |
|  |  | $= {926}$ |  |  | $= {857}$ |  |  |
| Order in 2 for | Order in 2 for | - | 2 | 2,3 | 2, 3, 4 |  |  |

Period 3. ${D}_{3} = {90}$

| ${x}_{4}$ | ${h}_{3}{x}_{4}$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | ${C}_{3}\left( {z}_{3}\right)  + {h}_{3}{x}_{4} + {f}_{2}\left( {{x}_{4} + {D}_{3} - {z}_{3}}\right)$ | Optimal solution | Optimal solution |
|---|---|---|---|---|---|---|
| ${z}_{3} = 0$ | 90 | 157 |  |  |  |  |
| ${C}_{3}\left( {z}_{3}\right)  = 0$ | 365 | 499 | ${f}_{3}\left( {x}_{4}\right)$ | ${z}_{3}^{ * }$ |  |  |
| 0 | 0 | $0 + {656} = {656}$ | ${365} + {298} = {663}$ |  | 656 | 0 |
| 67 | 67 | ${67} + {857} = {924}$ |  | ${566} + {298} = {864}$ | 864 | 157 |
| Order in 3 for | Order in 3 for | - | 3 | 3,4 |  |  |

Period 4. ${D}_{4} = {67}$

| ${x}_{5}$ | ${h}_{4}{x}_{5}$ | ${C}_{4}\left( {z}_{4}\right)  + {h}_{4}{x}_{5} + {f}_{3}\left( {{x}_{5} + {D}_{4} - {z}_{4}}\right)$ | ${C}_{4}\left( {z}_{4}\right)  + {h}_{4}{x}_{5} + {f}_{3}\left( {{x}_{5} + {D}_{4} - {z}_{4}}\right)$ | Optimal solution | Optimal solution |
|---|---|---|---|---|
| ${z}_{4} = 0$ | 67 |  |  |  |  |
| ${C}_{4}\left( {z}_{4}\right)  = 0$ | 204 | ${f}_{4}\left( {x}_{5}\right)$ | ${z}_{4}^{ * }$ |  |  |
| 0 | 0 | $0 + {864} = {864}$ | ${204} + {656} = {860}$ | 860 | 67 |
| Order in 4 for | Order in 4 for | - | 4 |  |  |

The optimal policy is determined from the tableaus as follows:

$$
\left( {{x}_{5} = 0}\right)  \rightarrow  {z}_{4} = {67}\rbrack  \rightarrow  \left( {{x}_{4} = 0}\right)  \rightarrow  {z}_{3} = 0
$$

$$
\rightarrow  \left( {{x}_{3} = {90}}\right)  \rightarrow  {z}_{2} = {116}\rbrack  \rightarrow  \left( {{x}_{2} = 0}\right)  \rightarrow  {z}_{1} = {61}
$$

This gives ${z}_{1}^{ * } = {61},{z}_{2}^{ * } = {116},{z}_{3}^{ * } = 0$ , and ${z}_{4}^{ * } = {67}$ , at a total cost of $\$ {860}$ .

## Excel Moment

Template excelWagnerWhitin.xls is similar to that of the general model excelDPInv.xls. The only difference is that lump sums are used for the state $x$ and alternative $z$ . Also, for simplicity, the new spreadsheet does not allow for quantity discount. The template is limited to a maximum of 10 periods. Remember to use paste special + values when creating the output solution summary (columns Q:V).

Silver-Meal heuristic. This heuristic is valid only when the unit production cost is constant and identical for all the periods. For this reason, it balances only the setup and holding costs.

The heuristic identifies the successive future periods whose demand can be filled from the production of the current period. The objective is to minimize the associated setup and holding costs per period. ^silvermeal

Suppose that we produce in period $i$ for periods $i, i + 1,\ldots$ , and $t, i < t$ , and define $\operatorname{TC}\left( {i, t}\right)$ as the associated setup and holding costs for the same periods. Using the same notation of the DP models, we have

$$
\operatorname{TC}\left( {i, t}\right)  = \left\{  \begin{array}{ll} {K}_{i}, & t = i \\  {K}_{i} + {h}_{i}{D}_{i + 1} + \left( {{h}_{i} + {h}_{i + 1}}\right) {D}_{i + 2} + \ldots  + \left( {\mathop{\sum }\limits_{{k = i}}^{{t - 1}}{h}_{k}}\right) {D}_{t}, & t > i \end{array}\right.
$$

Next, define $\operatorname{TCU}\left( {i, t}\right)$ as the associated cost per period-that is,

$$
\operatorname{TCU}\left( {i, t}\right)  = \frac{\operatorname{TC}\left( {i, t}\right) }{t - i + 1}
$$

Given a current period $i$ , the heuristic determines ${t}^{ * }$ that minimizes $\operatorname{TCU}\left( {i, t}\right)$ .

The function $\operatorname{TC}\left( {i, t}\right)$ can be computed recursively as

$$
\mathrm{{TC}}\left( {i, i}\right)  = {K}_{i}
$$

$$
\mathrm{{TC}}\left( {i, t}\right)  = \mathrm{{TC}}\left( {i, t - 1}\right)  + \left( {\mathop{\sum }\limits_{{k = i}}^{{t - 1}}{h}_{k}}\right) {D}_{t}, t = i + 1, i + 2,\ldots , n
$$

Step 0. Set $i = 1$ .

Step 1. Determine the local minimum ${t}^{ * }$ that satisfies the following two conditions:

$$
\operatorname{TCU}\left( {i,{t}^{ * } - 1}\right)  \geq  \operatorname{TCU}\left( {i,{t}^{ * }}\right)
$$

$$
\operatorname{TCU}\left( {i,{t}^{ * } + 1}\right)  \geq  \operatorname{TCU}\left( {i,{t}^{ * }}\right)
$$

The heuristic calls for ordering the amount $\left( {{D}_{i} + {D}_{i + 1} + \ldots  + {D}_{t}^{ * }}\right)$ in period $i$ for periods $i, i + 1,\ldots$ , and ${t}^{ * }$ .

Step 2. Set $i = {t}^{ * } + 1$ . If $i > n$ , stop; the entire planning horizon has been covered. Otherwise, go to step 1.

Example 13.4-4

Find the optimal inventory policy for the following six-period inventory situation:

| Period $i$ | ${D}_{i}$ (units) | ${K}_{i}\left( \mathbb{S}\right)$ | ${h}_{i}\left( \$ \right)$ |
|---|---|---|---|
| 1 | 10 | 20 | 1 |
| 2 | 15 | 17 | 1 |
| 3 | 7 | 10 | 1 |
| 4 | 20 | 18 | 3 |
| 5 | 13 | 5 | 1 |
| 6 | 25 | 50 | 1 |

The unit production cost is $\$ 2$ for all the periods.

Iteration $\mathbf{1}\left( {i = 1,{K}_{1} = \$ {20}}\right)$ . The function $\operatorname{TC}\left( {1, t}\right)$ is computed recursively in $t$ . For example, given $\operatorname{TC}\left( {1,1}\right)  = \$ {20},\operatorname{TC}\left( {1,2}\right)  = \operatorname{TC}\left( {1,1}\right)  + {h}_{1}{D}_{2} = {20} + 1 \times  {15} = \$ {35}$ .

| Period $t$ | ${D}_{i}$ | $\operatorname{TC}\left( {1, t}\right)$ | $\operatorname{TCU}\left( {1, t}\right)$ |
|---|---|---|---|
| 1 | 10 | \$20 | $\frac{20}{1} = \$ {20.00}$ |
| 2 | 15 | ${20} + 1 \times  {15} = \$ {35}$ | $\frac{35}{2} = \$ {17.50}$ |
| 3 | 7 | ${35} + \left( {1 + 1}\right)  \times  7 = \$ {94}$ | $\frac{49}{3} = \$ {16.33}$ |
| 4 | 20 | ${49} + \left( {1 + 1 + 1}\right)  \times  {20} = \$ {109}$ | $\frac{109}{4} = \$ {27.25}$ |

The local minimum occurs at ${t}^{ * } = 3$ , which calls for ordering ${10} + {15} + 7 = {32}$ units in period 1 for periods 1 to 3 . Set $i = {t}^{ * } + 1 = 3 + 1 = 4$ .

Iteration 2 (i = 4, ${\mathbf{K}}_{\mathbf{4}} = \$ \mathbf{{18}}$ ).

| Period $t$ | ${D}_{\mathrm{i}}$ | $\operatorname{TC}\left( {4, t}\right)$ | $\operatorname{TCU}\left( {4, t}\right)$ |
|---|---|---|---|
| 4 | 20 | \$18 | $\frac{18}{1} = \$ {18.00}$ |
| 5 | 13 | ${18} + 3 \times  {13} = \$ {57}$ | $\frac{57}{2} = \$ {28.50}$ |

The calculations show that ${t}^{ * } = 4$ , which calls for ordering 20 units in period 4 for period 4 . Set $i = 4 + 1 = 5$ .

Iteration $3\left( {i = 5,{K}_{5} = \$ 5}\right)$

| Period $t$ | ${D}_{r}$ | $\operatorname{TC}\left( {5, t}\right)$ | $\operatorname{TCU}\left( {5, t}\right)$ |
|---|---|---|---|
| 5 | 13 | \$5 | $\frac{5}{1} = \$ {5.00}$ |
| 5 | 13 | \$5 | $\frac{5}{1} = \$ 5$ |
| 6 | 25 | $5 + 1 \times  {25} = \$ {30}$ | $\frac{30}{2} = \$ {15}$ |

The minimum occurs at ${t}^{ * } = 5$ , which requires ordering 13 units in period 5 for period 5 . Next, we set $i = 5 + 1 = 6$ . However, because $i = 6$ is the last period of the planning horizon, we must order 25 unit in period 6 for period 6 .

Remarks. The following table compares the heuristic and the exact DP solution. We have deleted the unit production cost in the dynamic programming model because it is not included in the heuristic computations.

| Period | Heuristic | Heuristic | Dynamic programming | Dynamic programming |
|---|---|---|---|---|---|
| Units produced | Cost (\$) | Units produced | Cost (\$) |  |
| 1 | 32 | 49 | 10 | 20 |
| 2 | 0 | 0 | 22 | 24 |
| 3 | 0 | 0 | 0 | 0 |
| 4 | 20 | 18 | 20 | 18 |
| 5 | 13 | 5 | 38 | 30 |
| 6 | 25 | 50 | 0 | 0 |
| Total | 90 | 122 | 90 | 92 |

The heuristic production schedule costs about ${32}\%$ more than that of the DP solution (\$122 vs. \$92). The "inadequate" performance of the heuristic may be attributed to the nature of the data, as the problem may lie in the extreme setup cost values for periods 5 and 6. Nevertheless, the example shows that the heuristic does not have the capability to "look ahead" for better scheduling opportunities. For example, ordering in period 5 for periods 5 and 6 (instead of ordering for each period separately) can save \$25, which will bring the total heuristic cost down to \$97.

## Excel Moment

Excel template excelSilverMeal.xls is designed to carry out all the iterative computations and provide the final solution. The procedure starts with entering the data needed to drive the calculations, including $N, K, h$ , and $D$ for all the periods (these entries are highlighted in turquoise in the spreadsheet). The user must then initiate each iteration manually until all the periods have been covered.

Figure 13.11 shows the application of the Excel heuristic to Example 13.4-4. The first iteration is initiated by entering the value 1 in cell J11, signaling that iteration 1 starts at period 1. The spreadsheet will then generate as many rows as the number of periods, $N\left( { = 6\text{ in this example }}\right)$ . The period number will be listed in ascending order in cells K11:K16. Now, examine TCU in column P (highlighted in turquoise) and locate the period that corresponds to the local minimum at $t = 3$ with TCU = \$16.33. This means that the next iteration will start at period 4. Now, skip a blank row, and enter the value 4 in J18. This action, which produces the calculations for iteration 2, shows that its local minimum will be at period 4 (TCU = \$18.00) and signals the start of iteration 3 at period 5. Again, entering 5 in J22, the local minimum for iteration 3 occurs at node 5. Next, entering the value 6 in J25 produces the terminating iteration of the problem. The spreadsheet will automatically update the associated optimal policy and its total cost, as shown in Figure 13.11.

530 Chapter 13 Inventory Modeling (with Introduction to Supply Chains)

![bo_d56m533ef24c73bhe630_29_376_202_1127_721_0.jpg](bo_d56m533ef24c73bhe630_29_376_202_1127_721_0.jpg)

FIGURE 13.11

Excel solution of Example 13.4-4 using Silver-Meal heuristic (file ExcelSilverMeal.xls)

### 13.5 STICKY ISSUES IN INVENTORY MODELING ^issues

Implementation of inventory modeling in practice faces two hurdles:

1. Selection of the appropriate model.

2. Estimation of the cost parameters.

The task of selecting an appropriate model is exacerbated by the plethora of available inventory models (many presented in this chapter and more to come in Chapter 16). Each model is a simplified version of the general inventory problem. Unfortunately, the complexity of the inventory problem makes it analytically impossible to develop a unified mathematical model that fits all situations. And of course, when all available mathematical models fail to deliver, there is always the alternative of modeling the situation using simulation (Chapter 19) and/or heuristics (Chapter 10)-see also the case study at the end of this chapter for an illustration of the use of imbedded spreadsheet simulation in inventory modeling.

With regard to the estimation of inventory cost parameters, it is true that despite the complexity of the inventory problem, all inventory situations share a common objective; namely,

$$
\text{ Minimize (setup cost + holding cost + shortage cost) }
$$

But even with this unified objective, there is the challenge of how the associated cost parameters (for example, $K, h$ , and $p$ defined earlier in this chapter) are determined in practice.

The topic of estimating inventory cost parameters has not received the same level of attention in the literature as the (sometimes highly theoretical) development of new mathematical models. And those papers that deal with the subject matter only offer general guidelines with sketchy details. The reason is that cost parameters are highly business specific, ranging from the familiar retailing and manufacturing businesses to the highly bureaucratic government entities. As such, the problem of estimating cost parameters is indeed tough, and no amount of details can lead to universal rules that cover all situations.

## BIBLIOGRAPHY

Bishop, J. "Experience with a Successful System for Forecasting and Inventory Control," Operations Research, Vol. 22, No. 6, pp. 1224-1231, 1974.

Lewis, T., "Personal Operations Research: Practicing OR on Ourselves," Interfaces, Vol. 26, No. 5, pp. 34-41, 1996.

Muckstadt, J., and A. Sapra, Principles of Inventory Management, Springer, 2009.

Nahmias, S., Production and Operations Analysis, 6th ed., McGrawHill/Irwin, New York, 2008.

Silver, E., D. Pyke, and R. Peterson, Decision Systems for Inventory Management and Production Control, 3rd ed., Wiley, New York, 1998.

Tersine, R., Principles of Inventory and Materials Management, 4th ed., North Holland, New York, 1993.

Waters, D., Inventory Control and Management, 2nd ed., Wiley, New York, 2003.

## Case Study: Kroger Improves Pharmacy Inventory Management ^krogerdetail ${}^{7}$

Application Area: Pharmacies inventory control

Tools: Inventory formulas, heuristics, spreadsheet simulation

## Software: Excel

## Description of the situation

The Kroger Co., a supermarket chain, operates close to 2000 in-store pharmacies in the United States with a total retail value of about \$8 billion. Most pharmacies typically carry an average of 2500 drugs each. The pharmacies receive the majority of their drug supplies from Kroger's warehouses. The rest is shipped from third-party warehouses.

The pressing issue has been how to manage the enormous drug inventory problem at the store level. Understocking means frequent shortages with its negative impact on revenue and customer loyalty, and overstocking leads to tying up capital, high maintenance cost, and possible drug obsolescence. The goal of good inventory management at Kroger is to strike a balance between overstocking and understocking.

---

${}^{7}$ Based on Zhang, X. D., Meiser, Y. Liu, B. Bonner, and L. Lin,"Kroger Uses Simulation-Optimization to Improve Pharmacy Inventory Management," Interfaces, Vol. 44, No. 1, pp. 70-84, 2014.

---

## Inventory policy

Kroger pharmacy employs the $\left( {s, S}\right)$ periodic review policy that calls for bringing the inventory level up to $S$ whenever the inventory position (on hand + on order) drops below the reorder point $s$ . Thus, if at review time the current inventory level is $x\left( { < s}\right)$ , an order of size $S - x$ is placed. Otherwise ordering must await the next review process. Order sizes are rounded up to a multiple of a prespecified package size. Reviews take place during the review period, normally one or two days before a scheduled delivery.

The ultimate goal of this study is to determine the quantities $s$ and $S$ of the inventory policy that will minimize the total inventory cost comprised of the three traditional cost of carrying inventory: (1) cost of placing an order, (2) inventory holding cost, and (3) shortage cost. The developed model must be user-friendly for the pharmacy personnel in charge of determining the inventory policy for the thousands of drugs each pharmacy carries.

## Nature of demand

Typical demand for a drug per customer per day occurs in discrete values of 0 , or 30-, 60-, and 90-day supplies. Higher quantities (e.g., 120-, 150-, and 180-day supplies) can occur when multiple customers buy the same drug on any one day. Demand for a specific drug varies widely among store locations depending on demographic factors, population composition, and prevailing diseases. The end result is that demand for the majority of the drugs is intermittent and irregular and likely cannot be represented by known theoretical distributions. The most practical way to model such demand is to use direct sampling from the empirical discrete distribution.

## Spreadsheet simulation model

The spreadsheet was selected as the software of choice for modeling Kroger's inventory problem because it is a familiar tool to most computer users. This advantage was important in gaining the acceptance of the final software, not only by Kroger management but also by the pharmacy personnel responsible for deciding the inventory policy for each drug.

Figure 13.12 illustrates a 20-day spreadsheet simulation (normally the simulation runs for a full year). ${}^{8}$ Each spreadsheet deals with a single drug. Daily demand data (A9:A28) for the drug are generated randomly from the empirical discrete distribution of approximately one year of historical data. Column A provides one such (random) scenario using the inverse sampling method. ${}^{9}$ This scenario now forms a deterministic equivalence of the empirical demand distribution. It should remain unaltered throughout subsequent iterative search comparisons aimed at determining an acceptable inventory policy.

The main input data that drive the simulation are the periodic review values $s$ and $S$ in (B2:B3). The initial $\left( {s, S}\right)$ values used to start iterative simulations are

$Q =$ Economic order quantity (computed using file excelEOQ.xls, Section 13.3.1) $s =$ maximum demand of an order period based on historical data

$$
S = s + Q
$$

The output results of the simulation are then used to search for an $\left( {s, S}\right)$ policy with lower cost, and, if found, the new $\left( {s, S}\right)$ values are entered in (B2:B3) and the simulation is run anew for the same demand stream in column A. The procedure is repeated until no better policy can be found, as will be explained below.

---

${}^{8}$ I had no access to any of the software or the spreadsheets used in the Interfaces article. I developed this spreadsheet using fictitious data. The goal is to demonstrate the functionality of the simulation.

${}^{9}$ The inverse method for generating random discrete samples is presented in Section 19.3.2.

---

| 4 | A | B | C | D | E | F | G | H |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Input | Input | Input | Input | Output | Output | Output | Output |
| 2 | Reorder pt. s | 120 | Start wk day | Thu |  | Average demand | 24.00 | Normalize |
| 3 | Up-to qty. S | 180 | Starting inv | 100 |  | Average inventory | 85.00 | d cost, $C$ |
| 4 | Reviews occur on MWF Pkge. Size | Reviews occur on MWF Pkge. Size | Reviews occur on MWF Pkge. Size | 10 | Average shortage | Average shortage | 25 | 15.31250 |
| 5 |  |  | Lead time | 2 | Number of orders | Number of orders | 5 |  |
| 6 |  |  |  |  | Min. inv. Held (I+) | Min. inv. Held (I+) | 30 |  |
| 7 |  |  |  |  | Max. shortage (I-) | Max. shortage (I-) | 30 |  |

| 8 | Demand | Week days | Beginning inventory | Inventory position | Place order? | Order quantity | Quantity received | Ending inventory |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 9 | 0 | Thu | 100 | 100 |  | 0 | 0 | 100 |
| 10 | 60 | Fri | 100 | 100 | yes | 80 | 0 | 40 |
| 11 | 60 | Sat | 40 | 120 |  | 0 | 0 | -20 |
| 12 | 0 | Sun | -20 | 60 |  | 0 | 80 | 60 |
| 13 | 0 | Mon | 60 | 60 | yes | 120 | 0 | 60 |
| 14 | 30 | Tue | 60 | 180 |  | 0 | 0 | 30 |
| 15 | 0 | Wed | 30 | 150 |  | 0 | 120 | 150 |
| 16 | 0 | Thu | 150 | 150 |  | 0 | 0 | 150 |
| 17 | 0 | Fri | 150 | 150 |  | 0 | 0 | 150 |
| 18 | 0 | Sat | 150 | 150 |  | 0 | 0 | 150 |
| 19 | 0 | Sun | 150 | 150 |  | 0 | 0 | 150 |
| 20 | 30 | Mon | 150 | 150 |  | 0 | 0 | 120 |
| 21 | 60 | Tue | 120 | 120 |  | 0 | 0 | 60 |
| 22 | 30 | Wed | 60 | 60 | yes | 120 | 0 | 30 |
| 23 | 60 | Thu | 30 | 150 |  | 0 | 0 | -30 |
| 24 | 0 | Fri | -30 | 90 | yes | 90 | 120 | 90 |
| 25 | 60 | Sat | 90 | 180 |  | 0 | 0 | 30 |
| 26 | 90 | Sun | 30 | 120 |  | 0 | 90 | 30 |
| 27 | 0 | Mon | 30 | 30 | yes | 150 | 0 | 30 |
| 28 | 0 | Tue | 30 | 180 |  | 0 | 0 | 30 |

FIGURE 13.12

Excel spreadsheet simulation of a specific $\left( {s, S}\right)$ policy for a given stream of daily demand (file excelKrogerCase9.xls)

The remaining input data provide start week day (D2), starting inventory (D3), package size (D4), and lead time (D5). The start week day is used to enhance readability. All orders are rounded up to multiples of the package size. For simplicity this spreadsheet uses a constant lead time (= 2 days). Realistically, the lead time may be random (e.g., 2 days with probability .6 and 3 days with probability .4).

The spreadsheet calculations are based on the following ordering policy and simulation formulas:

## Ordering policy:

1. On a review day, if (inventory position) $< s$ order ( $S$ -inventory position), else do not order.

2. Inventory position reviewed on days MWF.

3. Order is placed at end of day and remains outstanding throughout lead time.

4. Filled order is received at end of day.

5. All unfilled demand is backordered (no lost sales).

Simulation formulas (day i):

1. (Beginning inventory) ${)}_{i} = {\left( \text{ Ending inventory }\right) }_{i - 1}$

2. (Ending inventory) ${}_{i} = {\left( \text{ Beginning inventory }\right) }_{i} + {\left( \text{ Received order }\right) }_{i} - {\left( \text{ Demand }\right) }_{i}$

3. (Inventory position) ${}_{i} = {\text{ (Beginning inventory) }}_{i} + {\text{ (On order) }}_{i - 1}$

The primary reason for assuming the backordering policy is that it provides information about shortages. Successive simulations are then carried out to determine a periodic review $\left( {s, S}\right)$ -policy that will reduce if not eliminate shortages.

A summary output of the simulation includes average demand (G2); average positive ending inventory (G3); average shortage ending inventory (G4); number of placed orders (G5); minimum positive ending inventory, ${I}^{ + }$ (G6); and maximum shortage ending inventory, ${I}^{ - }$ (G7).

The output data include the (normalized) total inventory cost per day (H4) comprised of the sum of order setup cost, holding cost, and shortage cost. ${}^{10}$ This cost function evaluates different periodic review policies.

As explained next, the output data minimum positive inventory (G6) and maximum shortage (G7) are used to direct the search for finding a better inventory policy.

## Local search algorithm

One way to find a good, if not optimal, solution is to assume a reasonable range of discrete values for $s$ (e.g.,120 to 300 in steps of 10) and $Q$ (e.g.,10 to 100 in steps of 10) and then run the simulation for all possible combinations $s$ and $S\left( { = s + Q}\right)$ . This, of course, is not efficient. The alternative is to devise heuristics that could lead to a good solution quickly.

The search starts with an initial review policy $\left( {s, s + Q}\right)$ defined previously. The values used in Figure 13.12 are $s = {120}$ and $Q = {60}$ , giving $S = {180}$ . Define $\left( {s, S}\right)$ as the best review policy so far found with cost $C$ (initially, $C = \infty$ ) and quantities ${I}^{ + }$ and ${I}^{ - }$ (G6:G7). The idea is to look for a better review policy in the neighborhood of $\left( {s, S}\right)$ based on two steps:

Step 1. (Fixed $Q$ ):

(a) Set ${s}^{\prime } = s + {I}^{ - }$ and ${S}^{\prime } = {s}^{\prime } + Q$ and run the simulation for the new policy $\left( {{s}^{\prime },{S}^{\prime }}\right)$ . If it yields a lower cost, update $\left( {s, S}\right)  = \left( {{s}^{\prime },{S}^{\prime }}\right)$ and repeat (a). Else go to (b).

(b) Set ${s}^{\prime } = s - {I}^{ + }$ and ${S}^{\prime } = {s}^{\prime } + Q$ and run the simulation for the new policy $\left( {{s}^{\prime },{S}^{\prime }}\right)$ . If it yields a lower cost, update $\left( {s, S}\right)  = \left( {{s}^{\prime },{S}^{\prime }}\right)$ and repeat (a). Else, no better solution can be found for fixed $Q$ . Go to Step 2.

Step 2. (Variable $Q$ ): Let $r = \min \left( {{I}^{ + },{I}^{ - }}\right)$ .

(a) Set ${S}^{\prime } = S + r$ , yielding ${Q}^{\prime } = {S}^{\prime } - s\left( { > Q}\right)$ , and run the simulation for the new policy $\left( {s,{S}^{\prime }}\right)$ . If it yields a lower cost, update $\left( {s, S}\right)  = \left( {{s}^{\prime }, S}\right)$ and go to step 1(a). Else go to (b).

(b) Set ${s}^{\prime } = s - r$ , yielding ${Q}^{\prime } = S - {s}^{\prime }\left( { < Q}\right)$ , and run the simulation for the new policy $\left( {s,{S}^{\prime }}\right)$ . If it yields a lower cost, update $\left( {s, S}\right)  = \left( {{s}^{\prime }, S}\right)$ and go to step 1(a). Else, no better solution can be found for variable $Q$ . Stop.

---

${}^{10}$ The source article does not specify the cost parameters of the total cost function nor does it explain how they are determined. For the lack of better data, I used a "normalized" definition in which the holding and shortage costs per unit per day are percentages of the setup cost (1% and 2.5%, respectively).

---

In step $1, Q$ is kept fixed by changing (increasing or decreasing) $s$ and $S$ by equal amounts. Step 1(a) increases both $s$ and $S$ in an attempt to eliminate the shortage ${I}^{ - }$ and step 1(b) tires to bring the minimum ending inventory ${I}^{ + }$ to zero by decreasing both $s$ and $S$ . If step 1 fails to produce a better solution for a fixed $Q$ , step 2 (with a similar line of reasoning as in step 1) varies the value of $Q$ by changing $s$ and $S$ , one at a time. When step 2 cannot produce a better review policy, the search ends with the last $\left( {s, S}\right)$ providing the best heuristic solution.

## Implementation

Kroger reports that developed model was implemented in 2011 in all the pharmacies in the United States. It has resulted in appreciable reduction in shortages and increase in revenues. The increase in revenues is estimated at \$80 million and was coupled with a reduction in inventory of about \$120 million.

Plans are underway to extend the model to other store departments. In particular, perishable products could benefit from a similar inventory control application with the goal of eliminating losses resulting from spoilage.

## PROBLEMS

| Section | Assigned Problems | Section | Assigned Problems |
|---|---|---|---|
| 13.1.1 | 13-1 to 13-2 | 13.3.3 | 13-18 to 13-21 |
| 13.3.1 | 13-3 to 13-12 | 13.4.1 | 13-22 to 13-25 |
| 13.3.2 | 13-13 to 13-17 | 13.4.2 | 13-26 to 13-36 |

*13-1. The current-year balance sheet of a company shows a beginning and end inventories of \$90.4 million and \$20.2 million, respectively. The net revenue from sales for the year is \$210.3 million and the gross profit is \$30.4 million. The final report claims that the company's average days-in-inventory is about 4 months. Assess the company's claim.

13-2. A small business financial data show that its inventory level of an item held steady at 100 units during the first 9 months of the year. Sales accelerated during the last quarter in time for Christmas shopping, ending the year with only 20 units left in stock. The company estimates the total inventory cost at \$.10 per unit per day. It sells the item at \$190 per unit, a markup of 60% over cost. Assess the company's inventory situation based on (a) simple inventory average based on starting and ending levels, and (b) the actual inventory average.

13-3. In each of the following cases, no shortage is allowed, and the lead time between placing and receiving an order is 35 days. Determine the optimal inventory policy and the associated cost per day.

(a) $K = \$ {120}, h = \$ {.04}, D = {25}$ units per day

(b) $K = \$ {80}, h = \$ {.03}, D = {35}$ units per day

(c) $K = \$ {100}, h = \$ {.02}, D = {50}$ units per day

(d) $K = \$ {110}, h = \$ {.03}, D = {25}$ units per day

*13-4. McBurger orders ground meat at the start of each week to cover the week's demand of 300 lb. The fixed cost per order is \$20. It costs about \$.03 per lb per day to refrigerate and store the meat.

(a) Determine the inventory cost per week of the present ordering policy.

(b) Determine the optimal inventory policy that McBurger should use, assuming zero lead time between the placement and receipt of an order.

13-5. A company stocks an item that is consumed at the rate of 60 units per day. It costs the company \$25 each time an order is placed. An inventory unit held in stock for a week will cost \$.36.

(a) Determine the optimum inventory policy, assuming a lead time of 2 weeks.

(b) Determine the optimum number of orders per year (based on 365 days per year).

*13-6. Two inventory policies have been suggested by the purchasing department of a company:

Policy 1. Order 150 units. The reorder point is 50 units, and the time between placing and receiving an order is 10 days.

Policy 2. Order 200 units. The reorder point is 75 units, and the time between placing and receiving an order is 15 days.

The setup cost per order is \$20, and the holding cost per unit inventory per day is \$.02.

(a) Which of the two policies should the company adopt?

(b) If you were in charge of devising an inventory policy for the company, what would you recommend assuming that the supplier requires a lead time of 22 days?

13-7. Walmark Store compresses and palletizes empty merchandise cartons for recycling. The store generates five pallets a day. The cost of storing a pallet in the store's back lot is \$.10 per day. The company that moves the pallets to the recycling center charges a flat fee of \$100 for the rental of its loading equipment plus a variable transportation cost of \$3 per pallet. Graph the change in number of pallets with time, and devise an optimal policy for hauling the pallets to the recycling center.

13-8. A hotel uses an external laundry service to provide clean towels. The hotel generates 600 soiled towels a day. The laundry service picks up the soiled towels and replaces them with clean ones at regular intervals. There is a fixed charge of \$81 per pickup and delivery service, in addition to the variable cost of \$.60 per towel. It costs the hotel \$.02 a day to store a soiled towel and \$.01 per day to store a clean one. How often should the hotel use the pickup and delivery service? (Hint: There are two types of inventory items in this situation. As the level of the soiled towels increases, that of clean towels decreases at an equal rate.)

13-9. Lewis (1996). An employee of a multinational company is on loan from the United States to the company's subsidiary in Europe. During the year, the employee's financial obligations in the United States (e.g., mortgage and insurance premium payments) amount to \$12,000, distributed evenly over the months of the year. The employee can meet these obligations by depositing the entire sum in a U.S. bank prior to departure for Europe. However, at present the interest rate in the United States is quite low (about 1.5% per year) in comparison with the interest rate in Europe (6.5% per year). The cost of sending funds from overseas is \$50 per transaction. Determine an optimal policy for transferring funds from Europe to the United States, and discuss the practical implementation of the solution. State all the assumptions.

13-10. Consider the inventory situation in which the stock is replenished uniformly (rather than instantaneously) at the rate $a$ . Consumption occurs at the constant rate $D$ . Because consumption also occurs during the replenishment period, it is necessary that $a > D$ . The setup cost is $K$ per order, and the holding cost is $h$ per unit per unit time. If $y$ is the order size and no shortage is allowed, show that

(a) The maximum inventory level is $y\left( {1 - \frac{D}{a}}\right)$ .

(b) The total cost per unit time given $y$ is

$$
\operatorname{TCU}\left( y\right)  = \frac{KD}{y} + \frac{h}{2}\left( {1 - \frac{D}{a}}\right) y
$$

(c) The economic order quantity is

$$
{y}^{ * } = \sqrt{\frac{2KD}{h\left( {1 - \frac{D}{a}}\right) }}, D < a
$$

(d) Show that the EOQ under instantaneous replenishment can be derived from the formula in (c).

13-11. A company can produce an item or buy it from a contractor. If it is produced, it will cost \$20 each time the machines are set up. The production rate is 100 units per day. If it is bought from a contractor, it will cost \$15 each time an order is placed. The cost of maintaining the item in stock, whether bought or produced, is \$.02 per unit per day. The company's usage of the item is estimated at 26,000 units annually. Assuming that no shortage is allowed, should the company buy or produce?

13-12. In Problem 13-10, suppose that shortage is allowed at a penalty cost of $p$ per unit per unit time.

(a) If $w$ is the maximum shortage during the inventory cycle, show that

$$
\operatorname{TCU}\left( {y, w}\right)  = \frac{KD}{y} + \frac{h{\left\{  y\left( 1 - \frac{D}{a}\right)  - w\right\}  }^{2} + p{w}^{2}}{2\left( {1 - \frac{D}{a}}\right) y}
$$

$$
{y}^{ * } = \sqrt{\frac{{2KD}\left( {p + h}\right) }{{ph}\left( {1 - \frac{D}{a}}\right) }}
$$

$$
{w}^{ * } = \sqrt{\frac{{2KDh}\left( {1 - \frac{D}{a}}\right) }{p\left( {p + h}\right) }}
$$

(b) Show that the EOQ results in Section 13.3.1 can be derived from the general formulas in (a).

13-13. Consider the hotel laundry service situation in Problem 13-8. The normal charge for washing a soiled towel is \$.60, but the laundry service will charge only \$.45 if the hotel delivers them in lots of at least 2600 towels. Should the hotel take advantage of the discount?

*13-14. An item is consumed at the rate of 30 items per day. The holding cost per unit per day is \$.05, and the setup cost is \$100. Suppose that no shortage is allowed and that the purchasing cost per unit is \$10 for any quantity not exceeding 500 units and \$8 otherwise. The lead time is 21 days. Determine the optimal inventory policy.

13-15. An item sells for \$30 a unit, but a 10% discount is offered for lots of 200 units or more. A company uses this item at the rate of 20 units per day. The setup cost for ordering a lot is \$50, and the holding cost per unit per day is \$.30. The lead time is 15 days. Should the company take advantage of the discount?

*13-16. In Problem 13-15, determine the range on the price discount percentage that, when offered for lots of size 150 units or more, will not result in any financial advantage to the company.

13-17. In the inventory model discussed in Section 13.3.2, suppose that the holding cost per unit per unit time is ${h}_{1}$ for quantities below $q$ and ${h}_{2}$ otherwise, ${h}_{1} > {h}_{2}$ . Show how the economic lot size is determined.

*13-18. The following data describe five inventory items: ${}^{11}$

| Item $i$ | ${K}_{i}\left( \mathbb{s}\right)$ | ${D}_{i}$ (units per day) | ${h}_{i}\left( \$ \right)$ | ${a}_{i}\left( {\mathrm{{ft}}}^{2}\right)$ |
|---|---|---|---|---|
| 1 | 35 | 22 | 0.35 | 1.0 |
| 2 | 28 | 34 | 0.15 | 0.8 |
| 3 | 30 | 14 | 0.28 | 1.1 |
| 4 | 25 | 21 | 0.30 | 0.5 |
| 5 | 20 | 26 | 0.42 | 1.2 |
| Total available storage area $= {22}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {22}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {22}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {22}{\mathrm{{ft}}}^{2}$ | Total available storage area $= {22}{\mathrm{{ft}}}^{2}$ |

Determine the optimal order quantities.

13-19. Solve the model of Example 13.3-3, assuming that we require the sum of the average inventories for all the items to be less than 25 units.

13-20. In Problem 13-19, assume that the only restriction is a limit of \$1000 on the amount of capital that can be invested in inventory. The purchase costs per unit of items 1, 2, and 3 are \$100, \$55, and \$100, respectively. Determine the optimum solution.

*13-21. The following data describe four inventory items:

| Item $i$ | ${K}_{i}\left( \mathbb{s}\right)$ | ${D}_{i}$ (units per day) | ${h}_{i}\left( \mathbb{s}\right)$ |
|---|---|---|---|
| 1 | 100 | 10 | .1 |
| 2 | 50 | 20 | .2 |
| 3 | 90 | 5 | .2 |
| 4 | 20 | 10 | .1 |

The company wishes to determine the economic order quantity for each of the four items such that the total number of orders per 365-day year is at most 150. Formulate the problem as a nonlinear program, and find the optimum solution.

13-22. In Figure 13.7, determine the combined requirements for subassembly $S$ in each of the following cases:

* (a) Lead time for ${M1}$ is only one period.

(b) Lead time for ${M1}$ is three periods.

13-23. Solve Example 13.4-1, assuming that the unit production and holding costs are as given in the following table:

| Period $i$ | Regular time unit cost (\$) | Overtime unit cost (\$) | Unit holding cost (\$) to period $i + 1$ |
|---|---|---|---|
| 1 | 5.00 | 7.50 | .10 |
| 2 | 3.00 | 4.50 | .15 |
| 3 | 4.00 | 6.00 | .12 |
| 4 | 1.00 | 1.50 | .20 |

13-24. An item is manufactured to meet known demand for four periods according to the following data:

| Production range (units) | Unit production cost (\$) for period | Unit production cost (\$) for period | Unit production cost (\$) for period | Unit production cost (\$) for period |
|---|---|---|---|---|---|
| 1 | 2 | 3 | 4 |  |
| 1-3 | 1 | 2 | 2 | 3 |
| 4-11 | 1 | 4 | 5 | 4 |
| 12-15 | 2 | 4 | 7 | 5 |
| 16-25 | 5 | 6 | 10 | 7 |
| Unit holding cost to next period (\$) | .30 | .35 | .20 | .25 |
| Total demand (units) | 11 | 4 | 17 | 29 |

(a) Find the optimal solution, indicating the number of units to be produced in each period.

(b) Suppose that 30 additional units are needed in period 4. Where should they be produced?

*13-25. The demand for a product over the next five periods may be filled from regular production, overtime production, or subcontracting. Subcontracting may be used only if the overtime capacity has been used. The following table gives the supply, demand, and cost data of the situation:

| Period | Production capacity (units) | Production capacity (units) | Production capacity (units) | Production capacity (units) |
|---|---|---|---|---|---|
| Regular time | Overtime | Subcontracting | Demand |  |
| 1 | 100 | 50 | 30 | 153 |
| 2 | 40 | 60 | 80 | 200 |
| 3 | 90 | 80 | 70 | 150 |
| 4 | 60 | 50 | 20 | 200 |
| 5 | 70 | 50 | 100 | 203 |

The unit production costs for the three levels in each period are \$4, \$6, and \$7, respectively. The unit holding cost per period is \$.50. Determine the optimal solution.

*13-26. Consider Example 13.4-2.

(a) Will ${x}_{4} = 0$ in the optimum solution?

(b) For each of the following two cases, determine the feasible ranges for ${z}_{1},{z}_{2},{z}_{3},{x}_{1}$ , ${x}_{2}$ , and ${x}_{3}$ . (You will find it helpful to represent each situation as in Figure 13.10.)

(i) ${x}_{1} = 3$ and all the remaining data are the same.

(ii) ${x}_{1} = 0,{D}_{1} = 5,{D}_{2} = 4$ , and ${D}_{3} = 5$ .

*13-27. (a) Find the optimal solution for the following four-period inventory model:

| Period $i$ | Demand ${D}_{i}$ (units) | Setup cost ${K}_{i}\left( \mathbb{s}\right)$ | Holding cost ${h}_{i}\left( \$ \right)$ |
|---|---|---|---|
| 1 | 5 | 5 | 1 |
| 2 | 2 | 7 | 1 |
| 3 | 3 | 9 | 1 |
| 4 | 3 | 7 | 1 |

The unit production cost is $\$ 1$ each for the first 6 units and $\$ 2$ each for additional units.

(b) Verify the computations using excelDPInv.xls.

13-28. Suppose that the inventory-holding cost is based on the average inventory during the period. Develop the corresponding forward recursive equation.

13-29. Develop the backward recursive equation for the model, and then use it to solve Example 13.4-2.

13-30. Develop the backward recursive equation for the model, assuming that the inventory-holding cost is based on the average inventory in the period.

*13-31. Solve Example 13.4-3, assuming that the initial inventory is 80 units. You may use excelWagnerWhitin.xls to check your calculations.

13-32. Solve the following 10-period deterministic inventory model. Assume an initial inventory of 50 units.

| Period $i$ | Demand ${D}_{i}$ (units) | Unit production cost (\$) | Unit holding cost (\$) | Setup cost (\$) |
|---|---|---|---|---|---|
| 1 | 150 | 6 | 1 | 100 |
| 2 | 100 | 6 | 1 | 100 |
| 3 | 20 | 4 | 2 | 100 |
| 4 | 40 | 4 | 1 | 200 |
| 5 | 70 | 6 | 2 | 200 |
| 6 | 90 | 8 | 3 | 200 |
| 7 | 130 | 4 | 1 | 300 |
| 8 | 180 | 4 | 4 | 300 |
| 9 | 140 | 2 | 2 | 300 |
| 10 | 50 | 6 | 1 | 300 |

13-33. Find the optimal inventory policy for the following five-period model. The unit production cost is \$10 for all periods. The unit holding cost is \$1 per period.

| Period $i$ | Demand ${D}_{i}$ (units) | Setup cost ${K}_{1}\left( \mathbb{S}\right)$ |
|---|---|---|
| 1 | 50 | 80 |
| 2 | 70 | 70 |
| 3 | 100 | 60 |
| 4 | 30 | 80 |
| 5 | 60 | 60 |

13-34. Find the optimal inventory policy for the following six-period inventory situation: The unit production cost is \$2 for all the periods.

| Period $i$ | ${D}_{i}$ (units) | ${K}_{i}\left( \mathbb{s}\right)$ | ${h}_{i}\left( \$ \right)$ |
|---|---|---|---|
| 1 | 10 | 20 | 1 |
| 2 | 15 | 17 | 1 |
| 3 | 7 | 10 | 1 |
| 4 | 20 | 18 | 3 |
| 5 | 13 | 5 | 1 |
| 6 | 25 | 50 | 1 |

*13-35. The demand for fishing poles is at its minimum during the month of December and reaches its maximum during the month of April. Fishing Hole, Inc., estimates the

December demand at 50 poles. It increases by 10 poles a month until it reaches 90 in April. Thereafter, the demand decreases by 5 poles a month. The setup cost for a production lot is \$250, except during the peak demand months of February to April, when it increases to \$300. The production cost per pole is approximately constant at \$15 throughout the year, and the holding cost per pole per month is \$1. Fishing Hole is developing next year's (January through December) production plan. How should it schedule its production facilities?

13-36. A small publisher reprints a novel to satisfy the demand over the next 12 months. The demand estimates for the successive months are100,120,50,70,90,105,115,95,80,85, 100, and 110. The setup cost for reprinting the book is \$200, and the holding cost per book per month is \$1.20. Determine the optimal reprint schedule.

This page intentionally left blank