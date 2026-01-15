## CHAPTER 18 Queuing Systems

## Real-Life Application—Study of an Internal Transport System in a Manufacturing Plant

Three trucks are used in a manufacturing plant to transport materials. The trucks wait in a central parking lot until requested. A truck answering a request will travel to the customer location, carry a load to its destination, and then return to the central parking lot. The principal departments using the service are production, workshop, and maintenance. Complaints about long waits for a free truck have prompted users, especially production, to request adding a fourth truck to the fleet. This is an unusual application, because queuing theory is used to show that the source of long delays is mainly logistical and that with a simple change in the operating procedure of the truck pool, a fourth truck is not needed. Details of the study are given at the end of the chapter.

### 18.1 WHY STUDY QUEUES?

Waiting for service is part of daily life. We wait for service in restaurants, we queue up to board a plane, and we line up for service in post offices. And the waiting phenomenon is not an experience limited to human beings: Jobs wait to be processed on a machine, planes circle in stack before given permission to land, and cars stop at traffic lights. Eliminating waiting altogether is not a feasible option because the cost of installing and operating the service facility can be prohibitive. Our only recourse is to strike a balance between cost of offering a service and the cost of waiting experienced by customers. Queuing analysis is the vehicle for achieving this goal.

The study of queues deals with quantifying the phenomenon of waiting using representative measures of performance, such as average queue length, average waiting time in queue, and average facility utilization. The following example demonstrates how these measures can be used to design a service facility.

Example 18.1-1

McBurger is a fast-food restaurant with three service counters. The manager wants to expedite service. A study reveals the following relationship between the number of service counters and the waiting time for service:

<table><tr><td>Number of cashiers</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td></tr><tr><td>Average waiting time (min)</td><td>16.2</td><td>10.3</td><td>6.9</td><td>4.8</td><td>2.9</td><td>1.9</td><td>1.3</td></tr></table>

An examination of these data shows a 7-min average waiting time for the present 3-counter situation. Five counters would reduce waiting to about 3 minutes.

Cost-based model. The results of queuing analysis can be incorporated in a cost optimization mode that seeks the minimization of the sum of the cost of offering the service and the cost of waiting by customers. Figure 18.1 depicts a typical cost model (in dollars per unit time) where the cost of service increases with the increase in the level of service (e.g., the number of service counters). At the same time, the cost of waiting decreases with the increase in level of service.

The main obstacle in implementing cost models is the difficulty of determining the cost of waiting, particularly when waiting is experienced by human beings. This point is discussed in Section 18.9.

### 18.2 ELEMENTS OF A QUEUING MODEL

The principal players in a queuing situation are the customer and the server. Customers arrive at a (service) facility from a source. On arrival, a customer can start service immediately or wait in a queue if the facility is busy. When a facility completes a service, it automatically "pulls" a waiting customer, if any, from the queue. If the queue is empty, the facility becomes idle until a new customer arrives.

![bo_d56m5ibef24c73bhe68g_1_297_1569_789_545_0.jpg](bo_d56m5ibef24c73bhe68g_1_297_1569_789_545_0.jpg)

FIGURE 18.1

Cost-based queuing decision model

From the standpoint of analyzing queues, the arrival of customers is represented by the interarrival time (time between successive arrivals), and the service is measured by the service time per customer. Generally, the interarrival and service times are probabilistic (e.g., operation of a post office) or deterministic (e.g., arrival of applicants for job interviewer for a doctor's appointment).

Queue size plays a role in the analysis of queues. It may be finite (as in the buffer area between two successive machines) or, for all practical purposes, infinite (as in mail-order facilities).

Queue discipline, which represents the order in which customers are selected from a queue, is an important factor in the analysis of queuing models. The most common discipline is first-in, first-out (FIFO). Other disciplines include last-in, first-out (LIFO) and service in random order (SIRO). Customers may also be selected from the queue based on some order of priority. For example, rush jobs in a shop are processed ahead of regular jobs.

Queuing behavior plays a role in waiting-line analysis. Customers may jockey from a longer queue to a shorter one to reduce waiting time, they may balk from joining a queue altogether because of anticipated long delay, or they may renege from a queue because they have been waiting too long.

The design of the service facility may include parallel servers (e.g., post office or bank operation). The servers may also be arranged in series (e.g., jobs processed on successive machines), or they may be networked (e.g., routers in a computer network).

The source from which customers are generated may be finite or infinite. A finite source limits the number of arriving customers (e.g., machines requesting the service of a repairperson). An infinite source is, for all practical purposes, forever abundant (e.g., calls arriving at a telephone exchange).

Variations in the elements of a queuing situation give rise to a variety of mathematical queuing models. This chapter provides examples of these models. Complex queuing situations that cannot be represented mathematically are usually analyzed by using simulation (see Chapter 19).

---

## Aha! Moment: Perception of Waiting, and the Cultural Factor!

Of course mathematical queuing models should be employed to design efficient queuing operations, especially when dealing with machines or computer/telephone networks. But when the operations involve humans, particularly as customers, there are factors that mathematics may not be able to handle, that of human boredom while waiting. In these cases, an important psychology-of-waiting-principle must be acknowledged: Time goes faster when people are occupied doing something. And this is exactly what happened in the two real situations I cited in Section 1.6: In the elevator situation patrons were kept busy watching themselves and others in large mirrors in the entry way while awaiting elevators; and in the Houston airport case, passengers were kept busy walking longer before reaching the luggage area simply by parking arriving planes at the farthest gate from the carousels. In both cases, complaints about waiting disappeared, not by implementing queuing model-based improvements in the physical facilities but by altering patrons' perception of waiting, even though the actual time of completing the activity remained unchanged. Indeed, I often wondered why tabloids are featured in supermarkets near check-outs rather than in magazines/newspapers/books section (mind you, I am not equating the two contents!). I think that the display is done on purpose to keep customers occupied reading "far-out" sensational headlines while awaiting check-out.

---

And there is no better than Disney when it comes to using ploys to alleviate waiting boredom in its massive theme parks, including posting digital timers along the waiting lines that inflate the waits so guests will be pleasantly surprised when they beat expectations, making lines look shorter by using serpentine queues, placing visual and sound attractions all along the waiting line to entertain guests, and establishing a central command (run by "imagineers," no less!) that anticipates congestion spots and immediately amasses needed resources to alleviate or eliminate the problem.

Of course, perception of waiting and its negative effects can be a cultural thing; and what may appear unacceptable queuing behavior in some countries could be perfectly acceptable in others. I recall an experience while living for an extended period overseas. I was standing in line in a bank almost within reach of the teller when a man walked in and formed his own one-person line directly at the window. This is when I shouted, "Hey, you need to stand in line like the rest of us," upon which the man responded "What is your problem? I am not standing in your line!" Perplexed by his logic, I suddenly heard the bank teller, apparently alerted by the ongoing commotion, calling my name (he knew me from previous visits) and asking if he could be of help. Realizing that I probably was the only "odd" person around, I simply followed the adage "When in Rome ..." and advanced to the window to finish my transaction. The amazing thing is that no one else in the line objected to any of what was taking place (the man forming his own line, the teller's offer to help ahead of others before me, and my cutting in line to finish my transaction). It was not an issue for them. And one wonders why the line was formed in the first place!

### 18.3 ROLE OF EXPONENTIAL DISTRIBUTION

In most queuing situations, arrivals occur randomly. Randomness means that the occurrence of an event (e.g., arrival of a customer or completion of a service) is not influenced by the length of time that has elapsed since the occurrence of the last event.

Random interarrival and service times are described quantitatively in queuing models by the exponential distribution, which is defined as

$$
f\left( t\right)  = \lambda {e}^{-{\lambda t}}, t > 0
$$

Section 12.4.3 shows that for the exponential distribution

$$
E\{ t\}  = \frac{1}{\lambda }
$$

$$
P\{ t \leq  T\}  = {\int }_{0}^{T}\lambda {e}^{-{\lambda t}}{dt} = 1 - {e}^{-{\lambda T}}
$$

The definition of $E\{ t\}$ shows that $\lambda$ is the rate per unit time at which events (arrivals or departures) are generated.

The exponential distribution describes a totally random phenomenon. For example, if the time now is 8:20 A.M. and the last arrival has occurred at 8:02 A.M., the probability that the next arrival will occur by 8:29 is a function of the interval from 8:20 to 8:29 only, and it is totally independent of the length of time that has elapsed since the occurrence of the last event (8:02 to 8:20).

The totally random property of the exponential is referred to as forgetfulness or lack of memory. Given $f\left( t\right)$ is the exponential distribution of the time, $t$ , between successive (arrival) events, if $S$ is the interval since the occurrence of the last event, then the forgetfulness property implies that

$$
P\{ t > T + S \mid  t > S\}  = P\{ t > T\}
$$

To prove this result, we note that for the exponential with mean $\frac{1}{\lambda }$ ,

$$
P\{ t > Y\}  = 1 - P\{ t < Y\}  = {e}^{-{\lambda Y}}
$$

Thus,

$$
P\{ t > T + S \mid  t > S\}  = \frac{P\{ t > T + S, t > S\} }{P\{ t > S\} } = \frac{P\{ t > T + S\} }{P\{ t > S\} }
$$

$$
= \frac{{e}^{-\lambda \left( {T + S}\right) }}{{e}^{-{\lambda S}}} = {e}^{-{\lambda T}}
$$

$$
= P\{ t > T\}
$$

## Example 18.3-1

A service machine always has a standby unit for immediate replacement upon failure. The time to failure of the machine (or its standby unit) is exponential and occurs every 5 hours, on the average. The machine operator claims that the machine is "in the habit" of breaking down every night around 8:30 P.M. Analyze the operator's claim.

The average failure rate of the machine is $\lambda  = \frac{1}{5} = {.2}$ failure per hour. Thus, the exponential distribution of the time to failure is

$$
f\left( t\right)  = {.2}{e}^{-{.2t}}, t > 0
$$

Regarding the operator's claim, we know offhand that it cannot be true because it conflicts with the fact that the time between breakdowns is exponential and, hence, totally random. The probability that a failure will occur by 8:30 P.M. cannot be used to support or refute the operator's claim, because the value of such probability depends on the time (relative to 8:30 P.M.) at which it is computed. For example, if the time now is 8:20 P.M., then there is a low probability that the operator's claim is right-namely,

$$
p\left\{  {t < \frac{10}{60}}\right\}   = 1 - {e}^{-{.2}\left( \frac{10}{60}\right) } = {.03278}
$$

If the time now is 1:00 P.M., then the probability that a failure will occur by 8:30 P.M. increases to approximately .777 (verify!). These two extreme values show that the operator's claim is not true.

### 18.4 PURE BIRTH AND DEATH MODELS (RELATIONSHIP BETWEEN THE EXPONENTIAL AND POISSON DISTRIBUTIONS)

This section presents two queuing situations: the pure birth model, in which only arrivals occur, and the pure death model, in which only departures take place. An example of the pure birth model is the creation of birth certificates for newly born babies. The pure death model may be demonstrated by the random withdrawal of a stocked item in a store.

The exponential distribution is used to describe the interarrival time in the pure birth model and the interdeparture time in the pure death model. A by-product of the development of the two models is to show the close relationship between the exponential and the Poisson distributions, in the sense that one distribution automatically defines the other.

#### 18.4.1 Pure Birth Model

Define

$$
{p}_{0}\left( t\right)  = \text{ Probability of no arrivals during a period of time }t
$$

Given that the interarrival time is exponential and that the arrival rate is $\lambda$ customers per unit time, then

$$
{p}_{0}\left( t\right)  = P\{ \text{ interarrival time } \geq  t\}
$$

$$
= 1 - P\{ \text{ interarrival time } \leq  t\}
$$

$$
= 1 - \left( {1 - {e}^{-{\lambda t}}}\right)
$$

$$
= {e}^{-{\lambda t}}
$$

For a sufficiently small time interval $h > 0$ , we have

$$
{p}_{0}\left( h\right)  = {e}^{-{\lambda h}} = 1 - {\lambda h} + \frac{{\left( \lambda h\right) }^{2}}{2!} - \cdots  = 1 - {\lambda h} + 0\left( {h}^{2}\right)
$$

The exponential distribution is based on the assumption that during $h > 0$ , at most one event (arrival) can occur. Thus, as $h \rightarrow  0$ ,

$$
{p}_{1}\left( h\right)  = 1 - {p}_{0}\left( h\right)  \approx  {\lambda h}
$$

This result shows that the probability of an arrival during $h$ is directly proportional to $h$ , with the arrival rate, $\lambda$ , being the constant of proportionality.

To derive the distribution of the number of arrivals during a period $t$ when the interarrival time is exponential with mean $\frac{1}{\lambda }$ , define

$$
{p}_{n}\left( t\right)  = \text{ Probability of }n\text{ arrivals during }t
$$

For a sufficiently small $h > 0$ ,

$$
{p}_{n}\left( {t + h}\right)  \approx  {p}_{n}\left( t\right) \left( {1 - {\lambda h}}\right)  + {p}_{n - 1}\left( t\right) {\lambda h}, n > 0
$$

$$
{p}_{0}\left( {t + h}\right)  \approx  {p}_{0}\left( t\right) \left( {1 - {\lambda h}}\right) ,\;n = 0
$$

In the first equation, $n$ arrivals will be realized during $t + h$ if there are $n$ arrivals during $t$ and no arrivals during $h$ , or $n - 1$ arrivals during $t$ and one arrival during $h$ . All other combinations are not allowed because, according to the exponential distribution, at most one arrival can occur during a very small period $h$ . The product law of probability is applicable to the right-hand side of the equation because arrivals are independent. For the second equation, zero arrivals during $t + h$ can occur only if no arrivals occur during $t$ and $h$ .

Rearranging the terms and taking the limits as $h \rightarrow  0$ to obtain the first derivative of ${p}_{n}\left( t\right)$ with respect to $t$ , we get

$$
{p}_{n}^{\prime }\left( t\right)  = \mathop{\lim }\limits_{{h \rightarrow  0}}\frac{{p}_{n}\left( {t + h}\right)  - {p}_{n}\left( t\right) }{h} =  - \lambda {p}_{n}\left( t\right)  + \lambda {p}_{n - 1}\left( t\right) , n > 0
$$

$$
{p}_{0}^{\prime }\left( t\right)  = \mathop{\lim }\limits_{{h \rightarrow  0}}\frac{{p}_{0}\left( {t - h}\right)  - {p}_{0}\left( t\right) }{h} =  - \lambda {p}_{0}\left( t\right) ,\;n = 0
$$

The solution of the preceding difference-differential equations yields

$$
{p}_{n}\left( t\right)  = \frac{{\left( \lambda t\right) }^{n}{e}^{-{\lambda t}}}{n!}, n = 0,1,2,\ldots
$$

This is a Poisson distribution with mean $E\{ n \mid  t\}  = {\lambda t}$ arrivals during $t$ .

The preceding result shows that if the time between arrivals is exponential with mean $\frac{1}{\lambda }$ , then the number of arrivals during a specific period $t$ is Poisson with mean ${\lambda t}$ . The converse is also true.

The following table summarizes the relationships between the exponential and the Poisson, given the arrival rate $\lambda$ :

<table><tr><td></td><td>Exponential</td><td>Poisson</td></tr><tr><td>Random variable</td><td>Time between successive arrivals, $t$</td><td>Number of arrivals, $n$ , during a specified period $T$</td></tr><tr><td>Range</td><td>$t \geq  0$</td><td>$n = 0,1,2,\ldots$</td></tr><tr><td>Density function</td><td>$f\left( t\right)  = \lambda {e}^{-{\lambda t}}, t \geq  0$</td><td>${p}_{n}\left( T\right)  = \frac{{\left( \lambda T\right) }^{n}{e}^{-{\lambda T}}}{n!}, n = 0,1,2,\ldots$</td></tr><tr><td>Mean value</td><td>$\frac{1}{\lambda }$ time units</td><td>${\lambda T}$ arrivals during $T$</td></tr><tr><td>Cumulative probability</td><td>$P\{ t \leq  A\}  = 1 - {e}^{-{\lambda A}}$</td><td>${p}_{n \leq  N}\left( T\right)  = {p}_{0}\left( T\right)  + {p}_{1}\left( T\right)  + \cdots  + {p}_{N}\left( T\right)$</td></tr><tr><td>$P\{$ no arrivals during period $A\}$</td><td>$P\{ t > A\}  = {e}^{-{\lambda A}}$</td><td>${p}_{0}\left( A\right)  = {e}^{-{\lambda A}}$</td></tr></table>

Remark. The Poisson distribution has the unique property that its mean and variance are equal (see Section 14.4.2). This observation can be useful in making an initial "guesstimate" as to whether or not the empirical data describe a Poisson distribution: If the mean and variance of the sample are far apart, then in all likelihood the sample does not come from a Poisson distribution. The opposite is not necessarily true, however, and it will be necessary to carry out at least a goodness-of-fit test (Section 14.5) to accept or reject the hypothesis. Above all, one must have a "gut-feeling" reason as to why a process should be designated as completely random.

## Example 18.4-1

Babies are born in a large city at the rate of one birth every 12 minutes. The time between births follows an exponential distribution. Find the following:

(a) The average number of births per year.

(b) The probability that no births will occur during 1 day.

(c) The probability of issuing 50 birth certificates in 3 hours, given that 40 certificates were issued during the first 2 hours of the 3-hr period.

The birth rate per day is computed as

$$
\lambda  = \frac{{24} \times  {60}}{12} = {120}\text{ births/day }
$$

Thus, the number of births per year in the state is

$$
{\lambda t} = {120} \times  {365} = {43},{800}\text{ births/year }
$$

The probability of no births during 1 day is

$$
{p}_{0}\left( 1\right)  = \frac{{\left( {120} \times  1\right) }^{0}{e}^{-{120} \times  1}}{0!} = {e}^{-{120}} = 0
$$

Another way to compute the same probability is to note that no birth in any one day is equivalent to saying that the time between successive births exceeds one day. We can thus use the exponential distribution to compute the desired probability as

$$
P\{ t > 1\}  = {e}^{-{120}} = 0
$$

Because the distribution of the number of births is Poisson, the probability of issuing 50 certificates in 3 hours, given that 40 certificates were issued during the first 2 hours, is equivalent to having ${10}\left( { = {50} - {40}}\right)$ births in one $\left( { = 3 - 2}\right) \mathrm{{hr}}$ -that is,

$$
{p}_{10}\left( 1\right)  = \frac{{\left( \frac{60}{12} \times  1\right) }^{10}{e}^{-5 \times  1}}{{10}!} = {.01813}
$$

## Excel Moment

The calculations associated with the Poisson distribution and, indeed, all queuing formulas are tedious and require programming skill to secure reasonable computational accuracy. You can use Excel POISSON, POISSONDIST, and EXPONDIST functions to compute the individual and cumulative probabilities Poisson and exponential probabilities. These functions are also automated in exceStatTables.xls. For example, for a birth rate of 5 babies per hour, the probability of exactly 10 births in ${.5}\mathrm{{hr}}$ is computed by entering 2.5 in F16 and 10 in J16 to obtain the answer .000216 in M16. The cumulative probability of at most 10 births is given in O16 (= .999938). To determine the probability of the time between births being less than or equal to 18 minutes, use the exponential distribution by entering 2.5 in F9 and .3 in J9. The answer, .527633, is found in O9.

## TORA/Excel Moment

You can also use TORA (file toraEx18.4-1.txt) or template excelPoissonQ.xls to determine all significant $\left( { > {10}^{-5}}\right.$ in TORA and $> {10}^{-7}$ in Excel) Poisson probabilities automatically. In both cases, the input data are the same. For the pure birth model of Example 18.4-1, the data are as follows:

<table><tr><td>Lambda</td><td>Mu</td><td>$c$</td><td>System limit</td><td>Source limit</td></tr><tr><td>5</td><td>0</td><td>0</td><td>Infinity</td><td>Infinity</td></tr></table>

Note the entry under Lambda ${\lambda t} = 5 \times  1 = 5$ births per day. Note also that $\mathrm{{Mu}} = 0$ identifies the model as pure birth.

#### 18.4.2 Pure Death Model

In the pure death model, the system starts with $N$ customers at time 0, with no new arrivals allowed. Departures occur at the rate $\mu$ customers per unit time. To develop the difference-differential equations for the probability ${p}_{n}\left( t\right)$ of $n$ customers remaining after $t$ time units, we follow the arguments used with the pure birth model (Section 18.4.1). Thus,

$$
{p}_{N}\left( {t + h}\right)  = {p}_{N}\left( t\right) \left( {1 - {\mu h}}\right)
$$

$$
{p}_{n}\left( {t + h}\right)  = {p}_{n}\left( t\right) \left( {1 - {\mu h}}\right)  + {p}_{n + 1}\left( t\right) {\mu h},0 < n < N
$$

$$
{p}_{0}\left( {t + h}\right)  = {p}_{0}\left( t\right) \left( 1\right)  + {p}_{1}\left( t\right) {\mu h}
$$

As $h \rightarrow  0$ , we get

$$
{p}_{N}^{\prime }\left( t\right)  =  - \mu {p}_{N}\left( t\right)
$$

$$
{p}_{n}^{\prime }\left( t\right)  =  - \mu {p}_{n}\left( t\right)  + \mu {p}_{n + 1}\left( t\right) ,0 < n < N
$$

$$
{p}_{0}^{\prime }\left( t\right)  = \mu {p}_{1}\left( t\right)
$$

The solution of these equations yields the following truncated Poisson distribution:

$$
{p}_{n}\left( t\right)  = \frac{{\left( \mu t\right) }^{N - n}{e}^{-{\mu t}}}{\left( {N - n}\right) !}, n = 1,2,\ldots , N
$$

$$
{p}_{0}\left( t\right)  = 1 - \mathop{\sum }\limits_{{n - 1}}^{N}{p}_{n}\left( t\right)
$$

Example 18.4-2

The florist section in a grocery store stocks 18 dozen roses at the beginning of each week. On the average, the florist sells 3 dozens a day (one dozen at a time), but the actual demand follows a Poisson distribution. Whenever the stock level reaches 5 dozens, a new order of 18 new dozens is placed for delivery at the beginning of the following week. Because of the nature of the item, all roses left at the end of the week are disposed of. Determine the following:

(a) The probability of placing an order in any one day of the week.

(b) The average number of dozen roses discarded at the end of the week.

Because purchases occur at the rate of $\mu  = 3$ dozens per day, the probability of placing an order by the end of day $t$ is

$$
{p}_{n \leq  5}\left( t\right)  = {p}_{0}\left( t\right)  + {p}_{1}\left( t\right)  + \ldots  + {p}_{5}\left( t\right)
$$

$$
= {p}_{0}\left( t\right)  + \mathop{\sum }\limits_{{n = 1}}^{5}\frac{{\left( 3t\right) }^{{18} - n}{e}^{-{3t}}}{\left( {{18} - n}\right) !}, t = 1,2,\ldots ,7
$$

The calculations of ${p}_{n \leq  5}\left( t\right)$ are best done using excelPoissonQ.xls or TORA. TORA’s multiple scenarios may be more convenient in this case. The associated input data for the pure death model corresponding to $t = 1,2,\ldots$ , and 7 are Lambda $= 0,\mathrm{{Mu}} = {3t}, c = 1$ , System Limit $= {18}$ , and Source Limit $= {18}$ . Note that $t$ must be substituted out numerically as shown in file toraEx18.4-2.txt.

The output is summarized as follows:

<table><tr><td>$t$ (day)</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td></tr><tr><td>${\mu t}$</td><td>3</td><td>6</td><td>9</td><td>12</td><td>15</td><td>18</td><td>21</td></tr><tr><td>${p}_{n \leq  5}\left( t\right)$</td><td>.0000</td><td>.0088</td><td>.1242</td><td>.4240</td><td>.7324</td><td>.9083</td><td>.9755</td></tr></table>

The average number of dozen roses discarded at the end of the week $\left( {t = 7}\right)$ is $E\{ n \mid  t = 7\}$ . To calculate this value, we need ${p}_{n}\left( 7\right) , n = 0,1,2,\ldots ,{18}$ , which can be determined using provided software. The result is

$$
E\{ n \mid  t = 7\}  = \mathop{\sum }\limits_{{n = 0}}^{{18}}n{p}_{n}\left( 7\right)  = {.664} \approx  1\text{ dozen }
$$

### 18.5 GENERAL POISSON QUEUING MODEL

This section develops a general queuing model that combines both arrivals and departures based on the Poisson assumptions - that is, the interarrival and the service times follow the exponential distribution. The model is the basis for the derivation of the specialized Poisson models in Section 18.6.

The development of the generalized model is based on the long-run or steady-state behavior of the queuing situation, achieved after the system has been in operation for a sufficiently long time. This type of analysis contrasts with the transient (or warm-up) behavior that prevails during the early operation of the system. (One reason for not discussing the transient behavior in this chapter is its analytical complexity. Another reason is that the study of most queuing situations occurs under steady-state conditions.)

The general model assumes that both the arrival and departure rates are state dependent - meaning that they depend on the number of customers in the service facility. For example, at a highway toll booth, attendants tend to speed up toll collection during rush hours. Another example occurs in a shop where the rate of machine breakdown decreases as the number of broken machines increases (because only working machines are capable of generating new breakdowns).

Define

$n =$ Number of customers in the system (in-queue plus in-service)

${\lambda }_{n} =$ Arrival rate, given $n$ customers in the system

${\mu }_{n} =$ Departure rate, given $n$ customers in the system

${p}_{n} =$ Steady-state probability of $n$ customers in the system

The generalized model derives ${p}_{n}$ as a function of ${\lambda }_{n}$ and ${\mu }_{n}$ . These probabilities are then used to determine the system's measures of performance, such as the average queue length, the average waiting time, and the average utilization of the facility.

The probabilities ${p}_{n}$ are determined by using the transition-rate diagram in Figure 18.2. The queuing system is in state $n$ when the number of customers in the system is $n$ . As explained in Section 18.3, the probability of more than one event occurring during a small interval $h$ tends to zero as $h \rightarrow  0$ . This means that for $n > 0$ , state $n$ can change only to two possible states: $n - 1$ when a departure occurs at the rate ${\mu }_{n}$ , and $n + 1$ when an arrival occurs at the rate ${\lambda }_{n}$ . State 0 can only change to state 1 when an arrival occurs at the rate ${\lambda }_{0}$ . Notice that ${\mu }_{0}$ is undefined because no departures can occur if the system is empty.

![bo_d56m5ibef24c73bhe68g_10_529_201_901_229_0.jpg](bo_d56m5ibef24c73bhe68g_10_529_201_901_229_0.jpg)

FIGURE 18.2

Poisson queues transition diagram

Under steady-state conditions, for $n > 0$ , the expected rates of flow into and out of state $n$ must be equal. Based on the fact that state $n$ can be changed to states $n - 1$ and $n + 1$ only, we get

$$
\left( \begin{array}{l} \text{ Expected rate of } \\  \text{ flow into state }n \end{array}\right)  = {\lambda }_{n - 1}{p}_{n - 1} + {\mu }_{n + 1}{p}_{n + 1}
$$

Similarly,

$$
\left( \begin{matrix} \text{ Expected rate of } \\  \text{ flow out of state }n \end{matrix}\right)  = \left( {{\lambda }_{n} + {\mu }_{n}}\right) {p}_{n}
$$

Equating the two rates, we get the following balance equation:

$$
{\lambda }_{n - 1}{p}_{n - 1} + {\mu }_{n + 1}{p}_{n + 1} = \left( {{\lambda }_{n} + {\mu }_{n}}\right) {p}_{n}, n = 1,2,\ldots
$$

From Figure 18.2, the balance equation associated with $n = 0$ is

$$
{\lambda }_{0}{p}_{0} = {\mu }_{1}{p}_{1}
$$

The balance equations are solved recursively in terms of ${p}_{0}$ . For $n = 0$ , we have

$$
{p}_{1} = \left( \frac{{\lambda }_{0}}{{\mu }_{1}}\right) {p}_{0}
$$

Next, for $n = 1$ , we have

$$
{\lambda }_{0}{p}_{0} + {\mu }_{2}{p}_{2} = \left( {{\lambda }_{1} + {\mu }_{1}}\right) {p}_{1}
$$

Substituting ${p}_{1} = \left( \frac{{\lambda }_{0}}{{\mu }_{0}}\right) {p}_{0}$ and simplifying, we get (verify!)

$$
{p}_{2} = \left( \frac{{\lambda }_{1}{\lambda }_{0}}{{\mu }_{2}{\mu }_{1}}\right) {p}_{0}
$$

We can show by induction that

$$
{p}_{n} = \left( \frac{{\lambda }_{n - 1}{\lambda }_{n - 2}\ldots {\lambda }_{0}}{{\mu }_{n}{\mu }_{n - 1}\ldots {\mu }_{1}}\right) {p}_{0}, n = 1,2,\ldots
$$

The value of ${p}_{0}$ is determined from the equation $\mathop{\sum }\limits_{{n = 0}}^{\infty }{p}_{n} = 1$

## Example 18.5-1

B&K Groceries operates with three checkout counters. The manager uses the following schedule to determine the number of counters in operation, depending on the number of customers in line:

<table><tr><td>Number of customers in store</td><td>Number of counters in operation</td></tr><tr><td>1 to 3</td><td>1</td></tr><tr><td>4 to 6</td><td>2</td></tr><tr><td>More than 6</td><td>3</td></tr></table>

Customers arrive in the counters area according to a Poisson distribution with a mean rate of 10 customers per hour. The average checkout time per customer is exponential with mean 12 minutes. Determine the steady-state probability ${p}_{n}$ of $n$ customers in the checkout area.

From the information of the problem, we have

$$
{\lambda }_{n} = \lambda  = {10}\text{ customers per hour, }\;n = 0,1,\ldots
$$

$$
{\mu }_{n} = \left\{  \begin{array}{l} \frac{60}{12} = 5\text{ customers per hour, } \\  2 \times  5 = {10}\text{ customers per hour, } \\  3 \times  5 = {15}\text{ customers per hour, } \end{array}\right.
$$

Thus,

$$
{p}_{1} = \left( \frac{10}{5}\right) {p}_{0} = 2{p}_{0}
$$

$$
{p}_{2} = {\left( \frac{10}{5}\right) }^{2}{p}_{0} = 4{p}_{0}
$$

$$
{p}_{3} = {\left( \frac{10}{5}\right) }^{3}{p}_{0} = 8{p}_{0}
$$

$$
{p}_{4} = {\left( \frac{10}{5}\right) }^{3}\left( \frac{10}{10}\right) {p}_{0} = 8{p}_{0}
$$

$$
{p}_{5} = {\left( \frac{10}{5}\right) }^{3}{\left( \frac{10}{10}\right) }^{2}{p}_{0} = 8{p}_{0}
$$

$$
{p}_{6} = {\left( \frac{10}{5}\right) }^{3}{\left( \frac{10}{10}\right) }^{3}{p}_{0} = 8{p}_{0}
$$

$$
{p}_{n \geq  7} = {\left( \frac{10}{5}\right) }^{3}{\left( \frac{10}{10}\right) }^{3}{\left( \frac{10}{15}\right) }^{n - 6}{p}_{0} = 8{\left( \frac{2}{3}\right) }^{n - 6}{p}_{0}
$$

The value of ${p}_{0}$ is determined from the equation

$$
{p}_{0} + {p}_{0}\left\{  {2 + 4 + 8 + 8 + 8 + 8 + 8\left( \frac{2}{3}\right)  + 8{\left( \frac{2}{3}\right) }^{2} + 8{\left( \frac{2}{3}\right) }^{3} + \ldots }\right\}   = 1
$$

or, equivalently

$$
{p}_{0}\left\{  {{31} + 8\left( {1 + \left( \frac{2}{3}\right)  + {\left( \frac{2}{3}\right) }^{2} + \ldots }\right) }\right\}   = 1
$$

Using the geometric sum series

$$
\mathop{\sum }\limits_{{i = 0}}^{\infty }{x}^{i} = \frac{1}{1 - x},\left| x\right|  < 1
$$

we get

$$
{p}_{0}\left\{  {{31} + 8\left( \frac{1}{1 - \frac{2}{3}}\right) }\right\}   = 1
$$

Thus, ${p}_{0} = \frac{1}{55}$ .

Given ${p}_{0}$ , we can now determine ${p}_{n}$ for $n > 0$ . For example, the probability that only one counter will be open is computed as the probability that there are at most three customers in the system:

$$
{p}_{0} + {p}_{1} + {p}_{2} + {p}_{3} = \left( {1 + 2 + 4 + 8}\right) \left( \frac{1}{55}\right)  \approx  {.273}
$$

We can use ${p}_{n}$ to determine measures of performance for the B&K situation. For example,

$$
\left( \begin{matrix} \text{ Expeted number } \\  \text{ of idle counters } \end{matrix}\right)  = 3{p}_{0} + 2\left( {{p}_{1} + {p}_{2} + {p}_{3}}\right)  + 1\left( {{p}_{4} + {p}_{5} + {p}_{6}}\right)
$$

$$
+ 0\left( {{p}_{7} + {p}_{8} + \ldots }\right)
$$

$$
= 1\text{ counter }
$$

### 18.6 SPECIALIZED POISSON QUEUES

Figure 18.3 depicts the specialized Poisson queuing situation with $c$ parallel servers. A waiting customer is selected from the queue to start service with the first available server. The arrival rate at the system is $\lambda$ customers per unit time. All parallel servers are identical, meaning that the service rate for any server is $\mu$ customers per unit time. The number of customers in the system is defined to include those in service and those waiting in queue.

A convenient notation for summarizing the characteristics of the queuing situation in Figure 18.3 is given by the following format:

$$
\left( {a/b/c}\right)  : \left( {d/e/f}\right)
$$

where

$a =$ Arrivals distribution

$b =$ Departures (service time) distribution

$c =$ Number of parallel servers $\left( { = 1,2,\ldots ,\infty }\right)$

$d =$ Queue discipline

$e =$ Maximum number (finite or infinite) allowed in the system (in-queue plus in-service)

$f =$ Size of the calling source (finite or infinite)

FIGURE 18.3

Schematic representation of a queuing system with $c$ parallel servers

![bo_d56m5ibef24c73bhe68g_12_336_1600_1291_612_0.jpg](bo_d56m5ibef24c73bhe68g_12_336_1600_1291_612_0.jpg)

The standard notation for representing the arrivals and departures distributions (symbols $a$ and $b$ ) is

$M =$ Markovian (or Poisson) arrivals or departures distribution (or equivalently exponential interarrival or service time distribution)

$D =$ Constant (deterministic) time

${E}_{k} =$ Erlang or gamma distribution of time (or, equivalently, the sum of independent exponential distributions)

${GI} =$ General (generic) distribution of interarrival time

$G =$ General (generic) distribution of service time

The queue discipline notation (symbol $d$ ) includes

FIFO = First-in, first-out

LIFO = Last-in, first-out

SIRO = Service in random order

${GD} =$ General discipline (i.e., any type of discipline)

To illustrate the use of the notation, the model $\left( {M/D/{10}}\right)  : \left( {{GD}/{20}/\infty }\right)$ uses Poisson arrivals (or exponential interarrival time), constant service time, and 10 parallel servers. The queue discipline is ${GD}$ , and there is a limit of 20 customers on the entire system. The size of the source from which customers arrive is infinite.

As a historical note, the first three elements of the notation $\left( {a/b/c}\right)$ were devised by D. G. Kendall in 1953 and are known in the literature as the Kendall notation. In 1966, A. M. Lee added the symbols $d$ and $e$ to the notation. I added the last element, symbol $f$ , in 1968. The addition of $f$ is not meant to be "decorative," for it completes all the input data needed to compute the steady-state results of the Poisson queuing model using TORA and Excel spreadsheet, as will be explained subsequently.

Before presenting the details of the specialized Poisson queues, we show how the steady-state measures of performance of the generalized queuing situation can be derived from the steady-state probabilities ${p}_{n}$ given in Section 18.5.

## Aha! Moment: The Last Will Be First . . . , or How to Move Queues More Rapidly!

A paper titled "The curse of the first-in-first-out queue discipline" published in 2015 by two Danish economists, Trine T. Platz and Lars P. Østerdal, ${}^{1}$ purports that a (LIFO discipline can move queues faster in situations where the queue is totally under the control of the server (which precludes, for the most part, queues involving face-to-face human interaction). The authors provide a number of situations where their model results can be applicable: (1) planes circling in a stack awaiting landing, (2) planes taking off from an airport, (3) 4.5 million Danish taxpayers accessing their returns on the Internet (all returns are released online at a specified date and hour), and (4) phone-based support centers. In these situations, the server is invisible to the customer. Moreover, the server can manage the queue in any preferred order (including LIFO). Under such conditions, the authors' mathematical model shows that LIFO moves the queue more rapidly.

---

${}^{1}$ http://sciencenordic.com/queues-move-faster-if-last-person-served-first (accessed September 22,2015,6:00 AM).

---

The main argument of the authors is that FIFO, though perceived as the fairest of all queuing disciplines, is actually the worst when it comes to reducing the average wait. Nevertheless, they concede that the implementation of LIFO in queues involving face-to-face human interaction is highly improbable, barring a change in existing cultural habits.

Naturally, the provocative use of the LIFO rule was reported in global social media, albeit in a layperson's fashion. Readers' comments appearing in London's Daily Mail (a total of 128) were particularly revealing. The majority of the commenters are, as expected, British who are conditioned to strict FIFO queuing behavior. Practically all of them are willing to forgo the purported LIFO efficiency for the sake of the FIFO fairness. In particular, one commenter pointedly states (no doubt tongue-in-cheek) "I lost the will to live trying to read this [article]"!

#### 18.6.1 Steady-State Measures of Performance

The most commonly used measures of performance in a queuing situation are

${L}_{s} =$ Expected number of customers in system

${L}_{q} =$ Expected number of customers in queue

${W}_{s} =$ Expected waiting time in system

${W}_{q} =$ Expected waiting time in queue

$\bar{c} =$ Expected number of busy servers

Recall that the system includes both the queue and the service facility.

We show now how these measures are derived (directly or indirectly) from the steady-state probability of $n$ in the system ${p}_{n}$ as

$$
{L}_{s} = \mathop{\sum }\limits_{{n = 1}}^{\infty }n{p}_{n}
$$

$$
{L}_{q} = \mathop{\sum }\limits_{{n = c + 1}}^{\infty }\left( {n - c}\right) {p}_{n}
$$

The relationship between ${L}_{s}$ and ${W}_{s}$ (also ${L}_{q}$ and ${W}_{q}$ ) is known as Little’s formula, and it is given as

$$
{L}_{s} = {\lambda }_{\mathrm{{eff}}}{W}_{s}
$$

$$
{L}_{q} = {\lambda }_{\mathrm{{eff}}}{W}_{q}
$$

These relationships are valid under rather general conditions. The parameter ${\lambda }_{\text{ eff }}$ is the effective arrival rate at the system. It equals the (nominal) arrival rate $\lambda$ when all arriving customers can join the system. Otherwise, if some customers cannot join because the system is full (e.g., a parking lot), then ${\lambda }_{\text{ eff }} < \lambda$ . We will show later how ${\lambda }_{\text{ eff }}$ is determined.

A direct relationship also exists between ${W}_{s}$ and ${W}_{q}$ . By definition,

$$
\left( \begin{matrix} \text{ Expected waiting } \\  \text{ time in system } \end{matrix}\right)  = \left( \begin{matrix} \text{ Expected waiting } \\  \text{ time in queue } \end{matrix}\right)  + \left( \begin{matrix} \text{ Expected service } \\  \text{ time } \end{matrix}\right)
$$

This translates to

$$
{W}_{s} = {W}_{q} + \frac{1}{\mu }
$$

Next, we can relate ${L}_{s}$ to ${L}_{q}$ by multiplying both sides of the last formula by ${\lambda }_{\text{ eff }}$ , which together with Little's formula gives

$$
{L}_{s} = {L}_{q} + \frac{{\lambda }_{\text{ eff }}}{\mu }
$$

The difference between the average number in the system, ${L}_{s}$ , and the average number in the queue, ${L}_{q}$ , must equal the average number of busy servers, $\bar{c}$ . Thus,

$$
\bar{c} = {L}_{s} - {L}_{q} = \frac{{\lambda }_{\text{ eff }}}{\mu }
$$

It follows that

$$
\left( \begin{matrix} \text{ Facility } \\  \text{ utilization } \end{matrix}\right)  = \frac{\bar{c}}{c}
$$

Example 18.6-1

Visitors' parking at Ozark College is limited to five spaces only. Cars making use of this space arrive according to a Poisson distribution at the rate of six cars per hour. Parking time is exponentially distributed with a mean of 30 minutes. Visitors who cannot find an empty space on arrival may temporarily wait inside the lot until a parked car leaves. That temporary space can hold only three cars. Other cars that cannot park or find a temporary waiting space must go elsewhere. Determine the following:

(a) The probability, ${p}_{n}$ , of $n$ cars in the system.

(b) The effective arrival rate for cars that actually use the lot.

(c) The average number of cars in the lot.

(d) The average time a car waits for a parking space inside the lot.

(e) The average number of occupied parking spaces.

(f) The average utilization of the parking lot.

We note first that a parking space acts as a server, so that the system has a total of $c = 5$ parallel servers. Also, the maximum capacity of the system is $5 + 3 = 8$ cars.

The probability ${p}_{n}$ can be determined as a special case of the generalized model in Section 18.5 using

$$
{\lambda }_{n} = 6\text{ cars }/\text{ hour }, n = 0,1,2,\ldots ,8
$$

$$
{\mu }_{n} = \left\{  \begin{array}{l} n\left( \frac{60}{30}\right)  = {2n}\text{ cars hour, }n = 1,2,3,4,5 \\  5\left( \frac{60}{30}\right)  = {10}\text{ cars }/\text{ hour, }n = 6,7,8 \end{array}\right.
$$

From Section 18.5, we get

$$
{p}_{n} = \left\{  \begin{array}{ll} \frac{{3}^{n}}{n!}{p}_{0}, & n = 1,2,3,4,5 \\  \frac{{3}^{n}}{5!{5}^{n - 5}}{p}_{0}, & n = 6,7,8 \end{array}\right.
$$

The value of ${p}_{0}$ is computed by substituting ${p}_{n}, n = 1,2,\ldots ,8$ , in the following equation:

$$
{p}_{0} + {p}_{1} + \ldots  + {p}_{8} = 1
$$

or

$$
{p}_{0} + {p}_{0}\left( {\frac{3}{1!} + \frac{{3}^{2}}{2!} + \frac{{3}^{3}}{3!} + \frac{{3}^{4}}{4!} + \frac{{3}^{5}}{5!} + \frac{{3}^{6}}{5!5} + \frac{{3}^{7}}{5!{5}^{2}} + \frac{{3}^{8}}{5!{5}^{3}}}\right)  = 1
$$

This yields ${p}_{0} = {.04812}$ (verify!). From ${p}_{0}$ , we can now compute ${p}_{1}$ through ${p}_{8}$ as

<table><tr><td>$n$</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr><tr><td>${p}_{n}$</td><td>.14436</td><td>.21654</td><td>.21654</td><td>.16240</td><td>.09744</td><td>.05847</td><td>.03508</td><td>.02105</td></tr></table>

The effective arrival rate ${\lambda }_{\text{ eff }}$ can be computed by observing the schematic diagram in Figure 18.4, where customers arrive from the source at the rate $\lambda$ cars per hour. An arriving car may enter the parking lot at the rate ${\lambda }_{\text{ eff }}$ or it may go elsewhere at the rate ${\lambda }_{\text{ lost }}$ . This means that $\lambda  = {\lambda }_{\text{ eff }} + {\lambda }_{\text{ lost }}.$

A car will not be able to enter the parking lot if 8 cars are already in. This means that the proportion of cars that will not be able to enter the lot is ${p}_{8}$ . Thus,

$$
{\lambda }_{\text{ lost }} = \lambda {p}_{8} = 6 \times  {.02105} = {.1263}\text{ cars per hour }
$$

$$
{\lambda }_{\text{ eff }} = \lambda  - {\lambda }_{\text{ lost }} = 6 - {.1263} = {5.8737}\text{ cars per hour }
$$

The average number of cars in the lot (those waiting for or occupying a space) equals ${L}_{s}$ , the average number in the system. We can compute ${L}_{s}$ from ${p}_{n}$ as

$$
{L}_{s} = 0{p}_{0} + 1{p}_{1} + \ldots  + 8{p}_{8} = {3.1286}\text{ cars }
$$

A car waiting in the temporary space is actually a car in queue. Thus, its waiting time until a space is found is ${W}_{q}$ . To determine ${W}_{q}$ we use

$$
{W}_{q} = {W}_{s} - \frac{1}{\mu }
$$

Thus,

$$
{W}_{s} = \frac{{L}_{s}}{{\lambda }_{\text{ eff }}} = \frac{3.1286}{5.8737} = {.53265}\text{ hour }
$$

$$
{W}_{q} = {.53265} - \frac{1}{2} = {.03265}\text{ hour }
$$

The average number of occupied parking spaces is the same as the average number of busy servers:

$$
\bar{c} = {L}_{s} - {L}_{q} = \frac{{\lambda }_{\text{ eff }}}{\mu } = \frac{5.8737}{2} = {2.9368}\text{ spaces }
$$

![bo_d56m5ibef24c73bhe68g_16_386_1945_691_242_0.jpg](bo_d56m5ibef24c73bhe68g_16_386_1945_691_242_0.jpg)

FIGURE 18.4

Relationship between $\lambda ,{\lambda }_{\text{ eff }}$ , and ${\lambda }_{\text{ lost }}$

From $\bar{c}$ , we get

$$
\text{ Parking lot utilization } = \frac{\bar{c}}{c} = \frac{2.9368}{5} = {.58736}
$$

#### 18.6.2 Single-Server Models

This section presents two models for the single-server case $\left( {c = 1}\right)$ . The first model sets no limit on the maximum number in the system, and the second model assumes a finite system limit. Both models assume an infinite-capacity source. Arrivals occur at the rate $\lambda$ customers per unit time and the service rate is $\mu$ customers per unit time.

The results of the two models (and indeed of all the remaining models in Section 18.6) are derived as special cases of the results of the generalized model of Section 18.5.

The extended Kendall notation will be used to characterize each situation. Because the derivations of ${p}_{n}$ in Section 18.5 and of all the measures of performance in Section 18.6.1 are totally independent of a specific queue discipline, the symbol GD (general discipline) will be used with the notation.

$\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ . Using the notation of the general model, we have

$$
\left. \begin{array}{l} {\lambda }_{n} = \lambda \\  {\mu }_{n} = \mu  \end{array}\right\}  , n = 0,1,2,\ldots
$$

Also, ${\lambda }_{\text{ eff }} = \lambda$ and ${\lambda }_{\text{ lost }} = 0$ , because all arriving customers can join the system.

Letting $\rho  = \frac{\lambda }{\mu }$ , the expression for ${p}_{n}$ in the generalized model reduces to

$$
{p}_{n} = {\rho }^{n}{p}_{0}, n = 0,1,2,\ldots
$$

To determine the value of ${p}_{0}$ , we use the identity

$$
{p}_{0}\left( {1 + \rho  + {\rho }^{2} + \ldots }\right)  = 1
$$

The sum of the geometric series is $\left( \frac{1}{1 - \rho }\right)$ , provided $\rho  < 1$ . Thus

$$
{p}_{0} = 1 - \rho ,\rho  < 1
$$

The general formula for ${p}_{n}$ is thus given by the following geometric distribution:

$$
{p}_{n} = \left( {1 - \rho }\right) {\rho }^{n}, n = 1,2,\ldots \left( {\rho  < 1}\right)
$$

The mathematical derivation of ${p}_{n}$ imposes the condition $\rho  < 1$ , or $\lambda  < \mu$ . If $\lambda  \geq  \mu$ , the geometric series diverges, and the steady-state probabilities ${p}_{n}$ do not exist. This result makes intuitive sense, because unless the service rate is larger than the arrival rate, queue length will continually increase and no steady state can be reached.

The measure of performance ${L}_{q}$ can be derived in the following manner:

$$
{L}_{s} = \mathop{\sum }\limits_{{n = 0}}^{\infty }n{p}_{n} = \mathop{\sum }\limits_{{n = 0}}^{\infty }n\left( {1 - \rho }\right) {\rho }^{n}
$$

$$
= \left( {1 - \rho }\right) \rho \frac{d}{d\rho }\mathop{\sum }\limits_{{n = 0}}^{\infty }{\rho }^{n}
$$

$$
= \left( {1 - \rho }\right) \rho \frac{d}{d\rho }\left( \frac{1}{1 - \rho }\right)  = \frac{\rho }{1 - \rho }
$$

Because ${\lambda }_{\text{ eff }} = \lambda$ for the present situation, the remaining measures of performance are computed using the relationships in Section 18.6.1. Thus,

$$
{W}_{s} = \frac{{L}_{s}}{\lambda } = \frac{1}{\mu \left( {1 - \rho }\right) } = \frac{1}{\mu  - \lambda }
$$

$$
{W}_{q} = {W}_{s} - \frac{1}{\mu } = \frac{\rho }{\mu \left( {1 - \rho }\right) }
$$

$$
{L}_{q} = \lambda {W}_{q} = \frac{{\rho }^{2}}{1 - \rho }
$$

$$
\bar{c} = {L}_{s} - {L}_{q} = \rho
$$

## Example 18.6-2

Automata car wash is a one-bay facility. Cars arrive according to a Poisson distribution with a mean of 4 cars per hour and may wait in the facility's parking lot or on the street bordering the wash facility if the bay is busy. The time for washing and cleaning a car is exponential, with a mean of 10 minutes. This means that, for all practical purposes, there is no limit on the size of the system. The manager of the facility wants to determine the size of the parking lot.

For this situation, we have $\lambda  = 4$ cars per hour, and $\mu  = \frac{60}{10} = 6$ cars per hour. Because $\rho  = \frac{\lambda }{\mu } < 1$ , the system can operate under steady-state conditions. The TORA or excelPoissonQ .xls input for this model is

<table><tr><td>Lambda</td><td>Mu</td><td>$c$</td><td>System limit</td><td>Source limit</td></tr><tr><td>4</td><td>6</td><td>1</td><td>infinity</td><td>Infinity</td></tr></table>

The output of the model is shown in Figure 18.5. The average number of cars waiting in the queue, ${L}_{q}$ , is 1.33 cars.

Generally, using ${L}_{q}$ as the sole basis for the determination of the number of parking spaces is not advisable, because the design should, in some sense, account for the maximum possible length of the queue. For example, it may be more plausible to design the parking lot such that an arriving car will find a parking space at least 90% of the time. To do this, let $S$ represent the number of parking spaces. Having $S$ parking spaces is equivalent to having $S + 1$ spaces in the system (queue plus wash bay). An arriving car will find a space 90% of the time if there are at most $S$ cars in the system. This condition is equivalent to the following probability statement:

$$
{p}_{0} + {p}_{1} + \ldots  + {p}_{S} \geq  {.9}
$$

From Figure 18.5, cumulative ${p}_{n}$ for $n = 5$ is .91221 . This means that the condition is satisfied for $S \geq  5$ parking spaces.

The number of spaces $S$ can be determined also by using the mathematical definition of ${p}_{n}$ - that is,

$$
\left( {1 - \rho }\right) \left( {1 + \rho  + {\rho }^{2} + \ldots  + {\rho }^{S}}\right)  \geq  {.9}
$$

The sum of the truncated geometric series is $\frac{1 - {\rho }^{S + 1}}{1 - \rho }$ , which reduces the condition to

$$
\left( {1 - {\rho }^{S + 1}}\right)  \geq  {.9}
$$

Scenario 1: (M/M/1) : (GD/infinity/infinity)

<table><tr><td>Lambda = 4.00000 <br> Lambda eff $= {4.00000}$</td><td>Mu = 6.00000 Rho/c = 0.66667</td></tr><tr><td>Ls = 2.00000</td><td>Lq = 1.33333</td></tr><tr><td>Ws = 0.50000</td><td>Wq = 0.33333</td></tr></table>

<table><tr><td>n</td><td>Probability pn</td><td>Cumulative Pn</td><td>n</td><td>Probability pn</td><td>Cumulative Pn</td></tr><tr><td>0</td><td>0.33333</td><td>0.33333</td><td>13</td><td>0.00171</td><td>0.99657</td></tr><tr><td>1</td><td>0.22222</td><td>0.55556</td><td>14</td><td>0.00114</td><td>0.99772</td></tr><tr><td>2</td><td>0.14815</td><td>0.70370</td><td>15</td><td>0.00076</td><td>0.99848</td></tr><tr><td>3</td><td>0.09877</td><td>0.80247</td><td>16</td><td>0.00051</td><td>0.99899</td></tr><tr><td>4</td><td>0.06584</td><td>0.86831</td><td>17</td><td>0.00034</td><td>0.99932</td></tr><tr><td>5</td><td>0.04390</td><td>0.91221</td><td>18</td><td>0.00023</td><td>0.99955</td></tr><tr><td>6</td><td>0.02926</td><td>0.94147</td><td>19</td><td>0.00015</td><td>0.99970</td></tr><tr><td>7</td><td>0.01951</td><td>0.96098</td><td>20</td><td>0.00010</td><td>0.99980</td></tr><tr><td>8</td><td>0.01301</td><td>0.97399</td><td>21</td><td>0.00007</td><td>0.99987</td></tr><tr><td>9</td><td>0.00867</td><td>0.98266</td><td>22</td><td>0.00004</td><td>0.99991</td></tr><tr><td>10</td><td>0.00578</td><td>0.98844</td><td>23</td><td>0.00003</td><td>0.99994</td></tr><tr><td>11</td><td>0.00385</td><td>0.99229</td><td>24</td><td>0.00002</td><td>0.99996</td></tr><tr><td>12</td><td>0.00257</td><td>0.99486</td><td>25</td><td>0.00001</td><td>0.99997</td></tr></table>

FIGURE 18.5

TORA output of Example 18.6-2 (file toraEx18.6-2.txt)

Simplification of the inequality yields

$$
{\rho }^{S + 1} \leq  {.1}
$$

Taking the logarithms on both sides (and noting that $\log \left( x\right)  < 0$ for $0 < x < 1$ , which reverses the direction of the inequality), we get

$$
S \geq  \frac{\ln \left( {.1}\right) }{\ln \left( \frac{4}{6}\right) } - 1 = {4.679} \approx  5
$$

$\left( {M/M/1}\right)  : \left( {{GD}/N/\infty }\right)$ . This model differs from $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ in that there is a limit $N$ on the number in the system (maximum queue length $= N - 1$ ). Examples include manufacturing situations in which a machine may have a limited buffer space and a one-lane drive-in window in a fast-food restaurant. New arrivals are not allowed when the number of customers in the system reaches $N$ . Thus,

$$
{\lambda }_{n} = \left\{  \begin{array}{ll} \lambda , & n = 0,1,\ldots , N - 1 \\  0, & n = N, N + 1 \end{array}\right.
$$

$$
{\mu }_{n} = \mu ,\;n = 0,1,\ldots
$$

Using $\rho  = \frac{\lambda }{\mu }$ , the generalized model in Section 18.5 yields

$$
{p}_{n} = \left\{  \begin{array}{ll} {\rho }^{n}{p}_{0} & n \leq  N \\  0, & n > N \end{array}\right.
$$

The value of ${p}_{0}$ is determined from the equation $\mathop{\sum }\limits_{{n = 0}}^{\infty }{p}_{n} = 1$ , which yields

$$
{p}_{0}\left( {1 + \rho  + {p}^{2} + \ldots  + {\rho }^{N}}\right)  = 1
$$

or

Thus,

$$
{p}_{0} = \left\{  \begin{array}{ll} \frac{1 - \rho }{1 - {\rho }^{N + 1}}, & \rho  \neq  1 \\  \frac{1}{N + 1}, & \rho  = 1 \end{array}\right.
$$

$$
{p}_{n} = \left\{  \begin{matrix} \frac{\left( {1 - \rho }\right) {\rho }^{n}}{1 - {\rho }^{N + 1}}, & \rho  \neq  1 \\  \frac{1}{N + 1}, & \rho  = 1 \end{matrix}\right\}  , n = 0,1,\ldots , N
$$

The value of $\rho  = \frac{\lambda }{\mu }$ need not be less than 1 in this model, because arrivals at the system are controlled by the system limit $N$ . This means that ${\lambda }_{\text{ eff }}$ , rather than $\lambda$ , is the rate that matters in this case. Because customers will be lost when there are $N$ in the system, then, as shown in Figure 18.4,

$$
{\lambda }_{\text{ lost }} = \lambda {p}_{N}
$$

$$
{\lambda }_{\text{ eff }} = \lambda  - {\lambda }_{\text{ lost }} = \lambda \left( {1 - {p}_{N}}\right)
$$

In this case, ${\lambda }_{\text{ eff }} < \mu$ .

The expected number of customers in the system is computed as

$$
{L}_{s} = \mathop{\sum }\limits_{{n = 1}}^{N}n{p}_{n}
$$

$$
= \frac{1 - \rho }{1 - {\rho }^{N + 1}}\mathop{\sum }\limits_{{n = 0}}^{N}n{\rho }^{n}
$$

$$
= \left( \frac{1 - \rho }{1 - {\rho }^{N + 1}}\right) \rho \frac{d}{d\rho }\mathop{\sum }\limits_{{n = 0}}^{N}{\rho }^{n}
$$

$$
= \frac{\left( {1 - \rho }\right) \rho }{1 - {\rho }^{N + 1}}\frac{d}{d\rho }\left( \frac{1 - {\rho }^{N + 1}}{1 - \rho }\right)
$$

$$
= \frac{\rho \left\lbrack  {1 - \left( {N + 1}\right) {\rho }^{N} + N{\rho }^{N + 1}}\right\rbrack  }{\left( {1 - \rho }\right) \left( {1 - {\rho }^{N + 1}}\right) },\rho  \neq  1
$$

When $\rho  = 1,{L}_{s} = \frac{N}{2}$ (verify!). We can derive ${W}_{s},{W}_{q}$ , and ${L}_{q}$ from ${L}_{s}$ using ${\lambda }_{\text{ eff }}$ , as shown in Section 18.6.1.

The use of a hand calculator to compute the queuing formulas is at best cumbersome (the formulas get more complex in later models!). The use of TORA or the template excelPoissonQ.xls to handle these computations is recommended.

## Example 18.6-4

Consider the car wash facility of Example 18.6-2. Suppose that the facility has a total of four parking spaces. If the parking lot is full, newly arriving cars balk to other facilities. The owner wishes to determine the impact of the limited parking space on losing customers to the competition.

In terms of the notation of the model, the limit on the system is $N = 4 + 1 = 5$ . The following input data provide the output in Figure 18.6.

<table><tr><td>Lambda</td><td>Mu</td><td>$C$</td><td>System limit</td><td>Source limit</td></tr><tr><td>4</td><td>6</td><td>1</td><td>5</td><td>Infinity</td></tr></table>

Because the limit on the system is $N = 5$ , the proportion of lost customers is ${p}_{5} = {.04812}$ , which, based on a 24-hr day, is equivalent to losing the business of $\left( {\lambda {p}_{5}}\right)  \times  {24} = \; 4 \times  {.04812} \times  {24} = {4.62}$ cars a day. A decision regarding increasing the size of the parking lot should be based on the value of lost business.

Looking at the problem from a different angle, the expected total time in the system, ${W}_{s}$ , is .3736 hr, or approximately 22 minutes, down from 30 minutes in Example 18.6-3, when all arriving cars are allowed to join the facility. This reduction of about ${25}\%$ is secured at the expense of losing about 4.8% of all potential customers because of the limited parking space.

#### 18.6.3 Multiple-Server Models

This section considers three queuing models with multiple parallel servers. The first two models are the multiserver versions of the models in Section 18.6.2. The third model treats the self-service case, which is equivalent to having an infinite number of parallel servers.

FIGURE 18.6

TORA output of Example 18.6-4 (file toraEx18.6-4.txt)

Scenario 1: (M/M/1) : (GD/5/infinity)

<table><tr><td>Lambda = 4.00000</td><td>Mu = 6.00000</td></tr><tr><td>Lambda eff $= {3.80752}$</td><td>Rho/c = 0.66667</td></tr><tr><td>Ls = 1.42256</td><td>Lq = 0.78797</td></tr><tr><td>Ws = 0.37362</td><td>Wq = 0.20695</td></tr></table>

<table><tr><td>n</td><td>Probability pn</td><td>Cumulative Pn</td><td>n</td><td>Probability pn</td><td>Cumulative Pn</td></tr><tr><td>0</td><td>0.36541</td><td>0.36541</td><td>3</td><td>0.10827</td><td>0.87970</td></tr><tr><td>1</td><td>0.24361</td><td>0.60902</td><td>4</td><td>0.07218</td><td>0.95188</td></tr><tr><td>2</td><td>0.16241</td><td>0.77143</td><td>5</td><td>0.04812</td><td>1.00000</td></tr></table>

## Real-Life Application—Telephone Sales Workforce Planning at Qantas Airways

To reduce operating costs, Qantas Airways seeks to staff its main telephone sales reservation office efficiently while providing convenient service to its customers. Traditionally, staffing needs are estimated by forecasting future telephone calls based on historical increase in business. The increase in staff numbers is then calculated based on the projected average increase in telephone calls divided by the average number of calls an operator can handle. Because the calculations are based on averages, the additional number of hired staff does not take into account the fluctuations in demand during the day. In particular, long waiting time for service during peak business hours has resulted in customer complaints and lost business. The problem deals with the determination of a plan that strikes a balance between the number of hired operators and the customer needs. The solution uses $\left( {M/M/c}\right)$ queuing analysis imbedded into an integer programming model. Savings from the model in the Sydney office alone were around \$173,000 in fiscal year 1975-1976. The details of the study are given in Case 17, Chapter 26, on the website.

(MIMIc):(GD/ $\infty$ ). This model deals with $c$ identical parallel servers. The arrival rate is $\lambda$ and the service rate per server is $\mu$ . In this situation, ${\lambda }_{\text{ eff }} = \lambda$ because there is no limit on the number in the system.

The effect of using $c$ identical parallel servers is a proportionate increase in the facility service rate. In terms of the generalized model (Section 18.5), ${\lambda }_{n}$ and ${\mu }_{n}$ are thus defined as

$$
{\lambda }_{n} = \lambda ,\;n \geq  0
$$

$$
{\mu }_{n} = \left\{  \begin{array}{ll} {n\mu }, & n < c \\  {c\mu }, & n \geq  c \end{array}\right.
$$

Thus,

$$
{p}_{n} = \left\{  \begin{array}{ll} \frac{{\lambda }^{n}}{\mu \left( {2\mu }\right) \left( {3\mu }\right) \ldots \left( {n\mu }\right) }{p}_{0} = \frac{{\lambda }^{n}}{n!{\mu }^{n}}{p}_{0} = \frac{{\rho }^{n}}{n!}{p}_{0}, & n < c \\  \frac{{\lambda }^{n}}{\left( {\mathop{\prod }\limits_{{i = 1}}^{c}{i\mu }}\right) {\left( c\mu \right) }^{n - c}}{p}_{0} = \frac{{\lambda }^{n}}{c!{c}^{n - c}{\mu }^{n}}{p}_{0} = \frac{{\rho }^{n}}{c!{c}^{n - c}}{p}_{0}, & n \geq  c \end{array}\right.
$$

Letting $\rho  = \frac{\lambda }{\mu }$ , and assuming $\frac{\rho }{c} < 1$ , the value of ${p}_{0}$ is determined from $\mathop{\sum }\limits_{{n = 0}}^{\infty }{p}_{n} = 1$ , which gives,

$$
{p}_{0} = {\left\{  \mathop{\sum }\limits_{{n = 0}}^{{c - 1}}\frac{{\rho }^{n}}{n!} + \frac{{\rho }^{c}}{c!}\mathop{\sum }\limits_{{n = c}}^{\infty }{\left( \frac{\rho }{c}\right) }^{n - c}\right\}  }^{-1}
$$

$$
= {\left\{  \mathop{\sum }\limits_{{n = 0}}^{{c - 1}}\frac{{\rho }^{n}}{n!} + \frac{{\rho }^{c}}{c!}\left( \frac{1}{1 - \frac{\rho }{c}}\right) \right\}  }^{-1},\frac{\rho }{c} < 1
$$

The expression for ${L}_{q}$ can be determined as follows:

$$
{L}_{q} = \mathop{\sum }\limits_{{n = c}}^{\infty }\left( {n - c}\right) {p}_{n}
$$

$$
= \mathop{\sum }\limits_{{k = 0}}^{\infty }k{p}_{k + c}
$$

$$
= \mathop{\sum }\limits_{{k = 0}}^{\infty }k\frac{{\rho }^{k + c}}{{c}^{k}c!}{p}_{0}
$$

$$
= \frac{{\rho }^{c + 1}}{c!c}{p}_{0}\mathop{\sum }\limits_{{k = 0}}^{\infty }k{\left( \frac{\rho }{c}\right) }^{k - 1}
$$

$$
= \frac{{\rho }^{c + 1}}{c!c}{p}_{0}\frac{d}{d\left( \frac{\rho }{c}\right) }\mathop{\sum }\limits_{{k = 0}}^{\infty }{\left( \frac{\rho }{c}\right) }^{k}
$$

$$
= \frac{{\rho }^{c + 1}}{\left( {c - 1}\right) !{\left( c - \rho \right) }^{2}}{p}_{0}
$$

Because ${\lambda }_{\text{ eff }} = \lambda ,{L}_{s} = {L}_{q} + \rho$ . The measures ${W}_{s}$ and ${W}_{q}$ are determined by dividing ${L}_{s}$ and ${L}_{q}$ by $\lambda$ .

## Example 18.6-5

A community is served by two cab companies. Each company owns two cabs, and both share the market equally, with calls arriving at each company's dispatching office at the average rate of eight per hour. The average time per ride is 12 minutes. Calls arrive according to a Poisson distribution, and the ride time is exponential. The two companies have been bought by an investor and will be consolidated into a single dispatching office. Analyze the new owner's proposal.

From the standpoint of queuing, the cabs are the servers, and the cab ride is the service. Each company can be represented by the model $\left( {M/M/2}\right)  : \left( {{GD}/\infty /\infty }\right)$ with $\lambda  = 8$ calls per hour and $\mu  = \frac{60}{10} = 5$ rides per cab per hour. The consolidated model is $\left( {M/M/4}\right)  : \left( {{GD}/\infty /\infty }\right)$ with $\lambda  = 2 \times  8 = {16}$ calls per hour and $\mu  = 5$ rides per cab per hour.

A suitable measure for comparing the two models is the average waiting time for a ride, ${W}_{q}$ . The following table gives TORA comparative analysis input data:

<table><tr><td>Scenario</td><td>Lambda</td><td>Mu</td><td>$c$</td><td>System limit</td><td>Source limit</td></tr><tr><td>1</td><td>8</td><td>5</td><td>2</td><td>Infinity</td><td>Infinity</td></tr><tr><td>2</td><td>16</td><td>5</td><td>4</td><td>Infinity</td><td>Infinity</td></tr></table>

Figure 18.7 provides the output for the two scenarios. The results show that the waiting time for a ride is ${.356}\mathrm{{hr}}\left( { \approx  {21}\text{ minutes }}\right)$ for the two-cab situation and ${.149}\left( { \approx  9\text{ minutes }}\right)$ for the consolidated situation, a remarkable reduction of more than 50% and a clear evidence that the consolidation of the two companies is warranted.

Comparative analysis

<table><tr><td>C</td><td>Lambda</td><td>Mu</td><td>${\mathrm{L}}^{\prime }$ da eff</td><td>p0</td><td>Ls</td><td>Ws</td><td>Lq</td><td>Wq</td></tr><tr><td>2</td><td>8.000</td><td>5.000</td><td>8.00</td><td>0.110</td><td>4.444</td><td>0.556</td><td>2.844</td><td>0.356</td></tr><tr><td>4</td><td>16.000</td><td>5.000</td><td>16.00</td><td>0.027</td><td>5.586</td><td>0.349</td><td>2.386</td><td>0.149</td></tr></table>

FIGURE 18.7

TORA output for Example 18.6-5 (file toraEx18.6-5.txt)

Remarks. The conclusion from the preceding analysis is that service pools always provide a more efficient mode of operation. This conclusion is true even if the separate installations happen to be "very" busy (see Problem 18-69 and its mathematical generalization in Problem 18-77). Moreover, it appears intuitively plausible that service pools mode of operation should apply even if the queuing situation does not follow the Poisson model (for more on this point, see the Excel Moment following Section 19.5.2). Indeed, this remarkable result appears to have gained wide acceptance in the United States and abroad as can be witnessed in post offices, airport security checks and customs clearing of international arrivals, and store checkouts, among others.

$\left( {M/{Mc}}\right)  : \left( {{GD}/N/\infty }\right) , c \leq  N$ . This model differs from $\left( {M/{Mc}}\right)  : \left( {{GD}/\infty /\infty }\right)$ in that the system limit is finite and equal to $N$ . This means that the maximum queue size is $N - c$ . The arrival and service rates are $\lambda$ and $\mu$ . The effective arrival rate ${\lambda }_{\text{ eff }}$ is less than $\lambda$ because of the system limit, $N$ .

In terms of the generalized model (Section 18.5), ${\lambda }_{n}$ and ${\mu }_{n}$ for the current model are defined as

$$
{\lambda }_{n} = \left\{  \begin{array}{ll} \lambda , & 0 \leq  n \leq  N \\  0, & n > N \end{array}\right.
$$

$$
{\mu }_{n} = \left\{  \begin{array}{ll} {n\mu }, & 0 \leq  n \leq  c \\  {c\mu }, & c \leq  n \leq  N \end{array}\right.
$$

Substituting ${\lambda }_{n}$ and ${\mu }_{n}$ in the general expression in Section 18.5 and noting that $\rho  = \frac{\lambda }{\mu }$ , we get

$$
{p}_{n} = \left\{  \begin{matrix} \frac{{\rho }^{n}}{n!}{p}_{0}, & 0 \leq  n < c \\  \frac{{\rho }^{n}}{c!{c}^{n - c}}{p}_{0}, & c \leq  n \leq  N \end{matrix}\right.
$$

where

$$
{p}_{0} = \left\{  \begin{array}{ll} {\left( \mathop{\sum }\limits_{{n = 0}}^{{c - 1}}\frac{{\rho }^{n}}{n!} + \frac{{\rho }^{c}\left( {1 - {\left( \frac{\rho }{c}\right) }^{N - c + 1}}\right) }{c!\left( {1 - \frac{\rho }{c}}\right) }\right) }^{-1}, & \frac{\rho }{c} \neq  1 \\  {\left( \mathop{\sum }\limits_{{n = 0}}^{{c - 1}}\frac{{\rho }^{n}}{n!} + \frac{{\rho }^{c}}{c!}\left( N - c + 1\right) \right) }^{-1}, & \frac{\rho }{c} = 1 \end{array}\right.
$$

Next, we compute ${L}_{q}$ for the case where $\frac{\rho }{c} \neq  1$ as

$$
{L}_{q} = \mathop{\sum }\limits_{{n = c}}^{N}\left( {n - c}\right) {p}_{n}
$$

$$
= \mathop{\sum }\limits_{{j = 0}}^{{N - c}}j{p}_{j + c}
$$

$$
= \frac{{\rho }^{c}\rho }{c!c}{p}_{0}\mathop{\sum }\limits_{{j = 0}}^{{N - c}}j{\left( \frac{\rho }{c}\right) }^{j - 1}
$$

$$
= \frac{{\rho }^{c + 1}}{{cc}!}{p}_{0}\frac{d}{d\left( \frac{\rho }{c}\right) }\mathop{\sum }\limits_{{j = 0}}^{{N - c}}{\left( \frac{\rho }{c}\right) }^{j}
$$

$$
= \frac{{\rho }^{c + 1}}{\left( {c - 1}\right) !{\left( c - \rho \right) }^{2}}\left\{  {1 - {\left( \frac{\rho }{c}\right) }^{N - c + 1} - \left( {N - c + 1}\right) \left( {1 - \frac{\rho }{c}}\right) {\left( \frac{\rho }{c}\right) }^{N - c}}\right\}  {p}_{0}
$$

It can be shown that for $\frac{\rho }{c} = 1,{L}_{q}$ reduces to

$$
{L}_{q} = \frac{{\rho }^{c}\left( {N - c}\right) \left( {N - c + 1}\right) }{{2c}!}{p}_{0},\frac{\rho }{c} = 1
$$

To determine ${W}_{q}$ and hence ${W}_{s}$ and ${L}_{s}$ , we compute the value of ${\lambda }_{\text{ eff }}$ as

$$
{\lambda }_{\text{ lost }} = \lambda {p}_{N}
$$

$$
{\lambda }_{\text{ eff }} = \lambda  - {\lambda }_{\text{ lost }} = \left( {1 - {p}_{N}}\right) \lambda
$$

## Example 18.6-6

In the consolidated cab company problem of Example 18.6-5, suppose that new funds cannot be secured to purchase additional cabs. The owner was advised that one way to reduce the waiting time is for the dispatching office to inform new customers of potential excessive delay once the waiting list reaches six customers. The expectation is that these customers will seek service elsewhere, which in turn will reduce the average waiting time for those on the waiting list. Assess the situation.

Limiting the waiting list to 6 customers is equivalent to setting $N = 6 + 4 = {10}$ customers, leading to the model $\left( {M/M/4}\right)  : \left( {{GD}/{10}/\infty }\right)$ with $\lambda  = {16}$ customers per hour and $\mu  = 5$ rides per hour. The following input data provide the results in Figure 18.8.

<table><tr><td>Lambda</td><td>Mu</td><td>$C$</td><td>System limit</td><td>Source limit</td></tr><tr><td>16</td><td>5</td><td>4</td><td>10</td><td>Infinity</td></tr></table>

The average waiting time, ${W}_{q}$ , before setting a limit on the capacity of the system is ${.149}\mathrm{{hr}} \; \left( { \approx  9\text{ minutes }}\right)$ (see Figure 18.7), which is about twice the new average of ${.075}\mathrm{{hr}}\left( { \approx  {4.5}\text{ minutes }}\right)$ This remarkable reduction is achieved at the expense of losing about 3.6% of potential customers $\left( {{p}_{10} = {.03574}}\right)$ . However, this result does not reflect the intangible loss of customer goodwill on the operation of the company.

Scenario1: (M/M/4) : (GD/10/infinity)

<table><tr><td>Lambda = 16.00000</td><td>Mu =</td><td>5.00000</td><td></td></tr><tr><td>Lambda eff $= {15.42815}$</td><td>Rho/c =</td><td>0.80000</td><td></td></tr><tr><td>Ls = 4.23984</td><td>Lq =</td><td>1.15421</td><td></td></tr><tr><td>Ws = 0.27481</td><td>Wq =</td><td>0.07481</td><td></td></tr></table>

<table><tr><td>n</td><td>Probability pn</td><td>Cumulative Pn</td><td>n</td><td>Probability pn</td><td>Cumulative Pn</td></tr><tr><td>0</td><td>0.03121</td><td>0.03121</td><td>6</td><td>0.08726</td><td>0.79393</td></tr><tr><td>1</td><td>0.09986</td><td>0.13106</td><td>7</td><td>0.06981</td><td>0.86374</td></tr><tr><td>2</td><td>0.15977</td><td>0.29084</td><td>8</td><td>0.05584</td><td>0.91958</td></tr><tr><td>3</td><td>0.17043</td><td>0.46126</td><td>9</td><td>0.04468</td><td>0.96426</td></tr><tr><td>4</td><td>0.13634</td><td>0.59760</td><td>10</td><td>0.03574</td><td>1.00000</td></tr></table>

FIGURE 18.8

TORA output of Example 18.6-6 (file toraEx18.6-6.txt)

(M/M/∞):(GD/∞/∞)-Self-Service Model. In this model, the arrival and service rates are $\lambda$ and $\mu$ , respectively, and the number of servers is unlimited because the customer is also the server. A typical example is taking the written part of a driver's license test. Self-service gas stations and 24-hr ATM banks do not fall under this model because the servers in these cases are actually the gas pumps and the ATM machines.

In terms of the general model of Section 18.5, we have

$$
{\lambda }_{n} = \lambda ,\;n = 0,1,2,\ldots
$$

$$
{\mu }_{n} = {n\mu },\;n = 0,1,2,\ldots
$$

Thus,

$$
{p}_{n} = \frac{{\lambda }^{n}}{n!{\mu }^{n}}{p}_{0} = \frac{{\rho }^{n}}{n!}{p}_{0}, n = 0,1,2,\ldots
$$

Because $\mathop{\sum }\limits_{{n = 0}}^{\infty }{p}_{n} = 1$ , it follows that

$$
{p}_{0} = \frac{1}{1 + \rho  + \frac{{\rho }^{2}}{2!} + \ldots } = \frac{1}{{e}^{\rho }} = {e}^{-\rho }
$$

As a result,

$$
{p}_{n} = \frac{{e}^{-\rho }{\rho }^{n}}{n!}, n = 0,1,2,\ldots
$$

which is Poisson with mean ${L}_{s} = \rho$ . As should be expected, ${L}_{q}$ and ${W}_{q}$ are zero because it is a self-service facility.

## Example 18.6-7

An investor invests \$1000 a month, on average, in a stock market security. Because the investor must wait for good "buy" opportunity, the actual time of purchase is random. The investor usually keeps the securities for about 3 years on the average but will sell at random times when a good "sell" opportunity presents itself. Although the investor is generally recognized as a shrewd stock market player, past experience indicates that about 25% of the securities decline at about 20% a year. The remaining 75% appreciate at the rate of about 12% a year. Estimate the investor's (long-run) average equity in the stock market.

This situation can be treated as $\left( {M/M/\infty }\right)  : \left( {{GD}/\infty /\infty }\right)$ because, for all practical purposes, the investor does not have to wait in line to buy or to sell securities. The average time between order placements is 1 month, which yields $\lambda  = {12}$ securities per year. The rate of selling securities is $\mu  = \frac{1}{3}$ security per year. You can secure the model output using the following input:

<table><tr><td>Lambda</td><td>Mu</td><td>$c$</td><td>System limit</td><td>Source limit</td></tr><tr><td>12</td><td>.3333333</td><td>Infinity</td><td>Infinity</td><td>Infinity</td></tr></table>

Given the values of $\lambda$ and $\mu$ , we obtain

$$
{L}_{s} = \rho  = \frac{\lambda }{\mu } = {36}\text{ securities }
$$

The estimate of the (long-run) average annual net worth of the investor is

$$
\left( {{.25}{L}_{s} \times  \$ {1000}}\right) \left( {1 - {.20}}\right)  + \left( {{.75}{L}_{s} \times  \$ {1000}}\right) \left( {1 + {.12}}\right)  = \$ {63},{990}
$$

#### 18.6.4 Machine Servicing Model-(M/M/R):(GD/K/K), $R < K$

The venue for this model is a shop with $K$ machines. When a machine breaks down, one of $R$ repairpersons is called upon to do the repair. The rate of breakdown per machine is $\lambda$ breakdowns per unit time, and a repairperson will service broken machines at the rate of $\mu$ machines per unit time. All breakdowns and services follow the Poisson distribution.

The source in this model is finite because only machines in working order can break down and hence can generate calls for service. Once all machines are broken, no new calls for service can occur.

Given $\lambda$ , that is, the rate of breakdown per machine, the rate of breakdown for the entire shop is proportional to the number of working machines. In terms of the queuing model, having $n$ machines in the system signifies that $n$ machines are broken, and the associated rate of breakdown for the entire shop is

$$
{\lambda }_{n} = \left( {K - n}\right) \lambda ,0 \leq  n \leq  K
$$

In terms of the generalized model of Section 18.5, we have

$$
{\lambda }_{n} = \left\{  \begin{array}{ll} \left( {K - n}\right) \lambda , & 0 \leq  n \leq  K \\  0, & n \geq  K \end{array}\right.
$$

$$
{\mu }_{n} = \left\{  \begin{array}{ll} {n\mu }, & 0 \leq  n \leq  R \\  {R\mu }, & R \leq  n \leq  K \end{array}\right.
$$

From the generalized model, we can then obtain (verify!)

$$
{p}_{n} = \left\{  \begin{array}{ll} {C}_{n}^{K}{\rho }^{n}{p}_{0}, & 0 \leq  n \leq  R \\  {C}_{n}^{K}\frac{n!{\rho }^{n}}{R!{R}^{n - R}}{p}_{0}, & R \leq  n \leq  K \end{array}\right.
$$

$$
{p}_{0} = {\left( \mathop{\sum }\limits_{{n = 0}}^{R}{C}_{n}^{K}{\rho }^{n} + \mathop{\sum }\limits_{{n = R + 1}}^{K}{C}_{n}^{K}\frac{n!{\rho }^{n}}{R!{R}^{n - R}}\right) }^{-1}
$$

There is no closed form expression for ${L}_{s}$ , and hence it must be computed using the following basic definition:

$$
{L}_{s} = \mathop{\sum }\limits_{{n = 0}}^{K}n{p}_{n}
$$

The value of ${\lambda }_{\text{ eff }}$ is computed as

$$
{\lambda }_{\text{ eff }} = E\{ \lambda \left( {K - n}\right) \}  = \lambda \left( {K - {L}_{s}}\right)
$$

Using the formulas in Section 18.6.1, we can compute the remaining measures of performance ${W}_{s},{W}_{q}$ , and ${L}_{q}$ .

## Example 18.6-8

Toolco operates a machine shop with 22 machines. On the average, a machine breaks down every 2 hours. It takes an average of 12 minutes to complete a repair. Both the time between breakdowns and the repair time are exponential. Toolco is interested in determining the number of repairpersons needed to keep the shop running "smoothly."

The situation can be analyzed by investigating the productivity of the machines as a function of the number of repairpersons, defined as

$$
\left( \begin{matrix} \text{ Machines } \\  \text{ productivity } \end{matrix}\right)  = \frac{\text{ Available machines } - \text{ Broken machines }}{\text{ Available machines }} \times  {100}
$$

$$
= \frac{{22} - {L}_{s}}{22} \times  {100}
$$

The results for this situation can be obtained using the following input data: lambda = .5, mu $= 5, R = 1,2,3$ , or 4, system limit $= {22}$ , and source limit $= {22}$ . Figure 18.9 provides the

FIGURE 18.9

TORA comparative analysis output for Example 18.6-8 (file toraEx18.6-8.txt)

Comparative Analysis

<table><tr><td>C</td><td>Lambda</td><td>Mu</td><td>${\mathrm{L}}^{\prime }$ da eff</td><td>p0</td><td>Ls</td><td>Lq</td><td>Ws</td><td>Wq</td></tr><tr><td>1</td><td>0.500</td><td>5.00</td><td>4.9980</td><td>0.0004</td><td>12.0040</td><td>11.0044</td><td>2.4018</td><td>2.2018</td></tr><tr><td>2</td><td>0.500</td><td>5.00</td><td>8.8161</td><td>0.0564</td><td>4.3677</td><td>2.6045</td><td>0.4954</td><td>0.2954</td></tr><tr><td>3</td><td>0.500</td><td>5.00</td><td>9.7670</td><td>0.1078</td><td>2.4660</td><td>0.5128</td><td>0.2525</td><td>0.0525</td></tr><tr><td>4</td><td>0.500</td><td>5.00</td><td>9.9500</td><td>0.1199</td><td>2.1001</td><td>0.1102</td><td>0.2111</td><td>0.0111</td></tr></table>

output. The following table gives the associated productivity as a function of the number of repairpersons:

<table><tr><td>Repairperson, $R$</td><td>1</td><td>2</td><td>3</td><td>4</td></tr><tr><td>Machines productivity (100%)</td><td>45.44</td><td>80.15</td><td>88.79</td><td>90.45</td></tr><tr><td>Marginal increase (100%)</td><td>-</td><td>34.71</td><td>8.64</td><td>1.66</td></tr></table>

The results show that with one repairperson, the productivity is low $\left( { = {45.44}\% }\right)$ . By increasing the number of repairpersons to two, the productivity jumps by 34.71 to 80.15%. When the shop employs three repairpersons, the productivity increases only by about 8.64 to 88.79%, whereas four repairpersons will increase the productivity by a meager 1.66 to 90.45%.

Judging from these results, the use of two repairpersons is justifiable. The case for three repairpersons is not as strong, as it raises the productivity by only 8.64%. Perhaps a monetary comparison between the cost of hiring a third repairperson and the income attributed to the 8.64% increase in productivity can be used to settle this point (see Section 18.10 for discussion of cost models).

### 18.7 (M/G/1):(GD/∞/∞)—POLLACZEK-KHINTCHINE (P-K) FORMULA

Queuing models in which arrivals and departures do not follow the Poisson distribution are complex. In general, it is advisable to use simulation as an alternative tool for analyzing these situations (see Chapter 19).

This section presents one of the few non-Poisson queues for which analytic results are available. It deals with the case in which the service time, $t$ , is represented by any probability distribution with mean $E\{ t\}$ and variance $\operatorname{var}\{ t\}$ . The results of the model include the basic measures of performance ${L}_{s},{L}_{q},{W}_{s}$ , and ${W}_{q}$ , as well as ${p}_{0}$ . The model does not provide a closed-form expression for ${p}_{n}$ because of analytic intractability.

Let $\lambda$ be the arrival rate at the single-server facility. Given $E\{ t\}$ and $\operatorname{var}\{ t\}$ of the service-time distribution and that ${\lambda E}\{ t\}  < 1$ , it can be shown using sophisticated probability/Markov chain analysis that

$$
{L}_{s} = {\lambda E}\{ t\}  + \frac{{\lambda }^{2}\left( {{E}^{2}\{ t\}  + \operatorname{var}\{ t\} }\right) }{2\left( {1 - {\lambda E}\{ t\} }\right) },{\lambda E}\{ t\}  < 1
$$

The probability that the facility is empty (idle) is computed as

$$
{p}_{0} = 1 - {\lambda E}\{ t\}  = 1 - \rho
$$

Given ${\lambda }_{\text{ eff }} = \lambda$ , the remaining measures of performance $\left( {{L}_{q},{W}_{s}\text{ , and }{W}_{q}}\right)$ can be derived from ${L}_{s}$ , as explained in Section 18.6.1.

Template excelPKFormula.xls automates the calculations of this model.

## Example 18.7-1

In the Automata car wash facility of Example 18.6-2, suppose that a new system is installed so that the service time for all cars is constant and equal to 10 minutes. How does the new system affect the operation of the facility?

From Example 18.6-2, ${\lambda }_{\text{ eff }} = \lambda  = 4$ cars per hour. The service time is constant so that $E\{ t\}  = \frac{10}{60} = \frac{1}{6}\operatorname{hr}$ and $\operatorname{var}\{ t\}  = 0$ . Thus,

$$
{L}_{s} = 4\left( \frac{1}{6}\right)  + \frac{{4}^{2}\left( {{\left( \frac{1}{6}\right) }^{2} + 0}\right) }{2\left( {1 - \frac{4}{6}}\right) } = {1.33}\text{ cars }
$$

$$
{L}_{q} = {1.333} - \left( \frac{4}{6}\right)  = {.667}\text{ cars }
$$

$$
{W}_{s} = \frac{1.333}{4} = {.333}\mathrm{{hr}}
$$

$$
{W}_{q} = \frac{.667}{4} = {.167}\mathrm{{hr}}
$$

It is interesting to compare the waiting times with those of the Poisson case in Example 18.6-2, $\left( {M/D/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ . The arrival and departure rates are the same in both cases $(\lambda  = 4$ cars per hour and $\mu  = \frac{1}{E\{ t\} } = 6$ cars per hour). Yet, as the table given below shows, the expected waiting time is lower in the current model. The results make sense because a constant service time indicates more certainty in the operation of the facility. Indeed, the P-K formula shows that the waiting time increases when $\operatorname{Var}\{ t\}$ increases (again because of increase in uncertainty in the operation of the queuing system).

<table><tr><td></td><td>$\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$</td><td>$\left( {M/D/1}\right)  : \left( {{GD}/\infty /\infty }\right)$</td></tr><tr><td>${W}_{s}\left( \mathrm{{hr}}\right)$</td><td>.500</td><td>.333</td></tr><tr><td>${W}_{q}\left( \mathrm{{hr}}\right)$</td><td>.333</td><td>.167</td></tr></table>

### 18.8 OTHER QUEUING MODELS

The preceding sections have concentrated on the Poisson queuing models. Queuing literature is rich with other types of models. In particular, queues with priority for service, network queues, and non-Poisson G/G/c queues form an important body of the queuing theory literature. These models can be found in most specialized books on queuing theory.

Remarks. Poisson queuing models have enjoyed great successes in a number of areas including telecommunication and computing. Indeed, queuing theory got started in the early twentieth century by the Danish mathematician A. K. Erlang out of the practical need for deciding how many automatic telephone exchanges should be used to satisfy demand for placing telephone calls in his village. One of the convenient aspects of Poisson models is that, in practically all cases, the formulas for determining the system's steady-state measures of performance are computationally tractable. But alas!, not every queuing model is Poisson, and the variety of the real-life queuing situations in which the Poisson assumptions do not apply are numerous and tangible. The most promising models are Erlang’s $D/M/1$ and $D/M/c$ with constant interarrival time and Pollaczek-Khintchine $M/G/1$ model with general service-time distribution (Section 18.7). Though efforts were made to solve the general $G/G/c$ model in which any probability distribution can be used, the high-level mathematics associated with these models either resulted in "spotty" or approximate information about the system's measures of performance. Unfortunately, the quality and ease-of-use of these results are not on par with those of the Poisson models.

Simulation is an alternative tool for analyzing complex queuing situations literally by mimicking their real-life behavior on the computer. Measures of performance are obtained by observing the system's behavior and gathering relevant statistics as the simulation progresses in time. Although simulation is a highly flexible tool, it has its drawbacks. Chapter 19 is dedicated to presenting the details of this important tool.

### 18.9 QUEUING DECISION MODELS

The service level in a queuing facility is a function of the service rate, $\mu$ , and the number of parallel servers, $c$ . This section presents two decision models for determining "suitable" service levels for queuing systems: (1) a cost model and (2) an aspiration-level model. Both models recognize that higher service levels reduce the waiting time in the system. The goal is to strike a balance between service level and waiting.

#### 18.9.1 Cost Models

Cost models attempt to balance two conflicting costs:

1. Cost of offering the service.

2. Cost of delay in offering the service (customer waiting time).

An increase in one cost automatically causes a decrease in the other, as demonstrated earlier in Figure 18.1.

Letting $x\left( { = \mu \text{ or }c}\right)$ represent the service level, the cost model can be expressed as

$$
{ETC}\left( x\right)  = {EOC}\left( x\right)  + {EWC}\left( x\right)
$$

where

${ETC} =$ Expected total cost per unit time

${EOC} =$ Expected cost of operating the facility per unit time

${EWC} =$ Expected cost of waiting per unit time

The simplest forms for ${EOC}$ and ${EWC}$ are the following linear functions:

$$
{EOC}\left( x\right)  = {C}_{1}x
$$

$$
{EWC}\left( x\right)  = {C}_{2}{L}_{s}
$$

where

${C}_{1} =$ Marginal cost per unit of $x$ per unit time

${C}_{2} =$ Cost of waiting per unit time per (waiting) customer

The following two examples illustrate the use of the cost model. The first example assumes $x = \mu$ , and the second assumes $x = c$ .

Example 18.9-1

KeenCo Publishing is in the process of purchasing a high-speed commercial copier. Four models whose specifications are summarized below have been proposed by vendors.

<table><tr><td>Copier model</td><td>Operating cost (\$/hr)</td><td>Speed (sheets/min)</td></tr><tr><td>1</td><td>15</td><td>30</td></tr><tr><td>2</td><td>20</td><td>36</td></tr><tr><td>3</td><td>24</td><td>50</td></tr><tr><td>4</td><td>27</td><td>66</td></tr></table>

Jobs arrive at KeenCo in a Poisson stream at the rate of four jobs per 24-hr day. Job size is random but averages about 10,000 sheets per job. Contracts with the customers specify a penalty cost for late delivery of \$80 per jobs per day. Which copier should KeenCo purchase?

The total expected cost per day associated with copier $i$ is

$$
{ET}{C}_{i} = {EO}{C}_{i} + {EW}{C}_{i}
$$

$$
= {C}_{1i} \times  {24} + {C}_{2i}{L}_{si}
$$

$$
= {24}{C}_{1i} + {80}{L}_{si}, i = 1,2,3,4
$$

The values of ${C}_{1i}$ are given by the data of the problem. We determine ${L}_{si}$ by recognizing that, for all practical purposes, each copier can be treated as $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ model. The arrival rate is $\lambda  = 4$ jobs/day. The service rate ${\mu }_{i}$ associated with model $i$ is computed as

<table><tr><td>Model $i$</td><td>Service rate ${\mu }_{i}$ (jobs/day)</td></tr><tr><td>1</td><td>4.32</td></tr><tr><td>2</td><td>5.18</td></tr><tr><td>3</td><td>7.20</td></tr><tr><td>4</td><td>9.50</td></tr></table>

Computation of the service rate is demonstrated for model 1.

$$
\text{ Average time per job } = \frac{{10},{000}}{30} \times  \frac{1}{60} = {5.56}\mathrm{{hrs}}
$$

Thus,

$$
{\mu }_{1} = \frac{24}{5.56} = {4.32}\text{ jobs/day }
$$

The values of ${L}_{si}$ , computed by TORA or excePoissonQ.xls, are given in the following table:

<table><tr><td>Model $i$</td><td>${\lambda }_{i}$ (Jobs/day)</td><td>${\mu }_{i}$ (Jobs/day)</td><td>${L}_{si}$ (Jobs)</td></tr><tr><td>1</td><td>4</td><td>4.32</td><td>12.50</td></tr><tr><td>2</td><td>4</td><td>5.18</td><td>3.39</td></tr><tr><td>3</td><td>4</td><td>7.20</td><td>1.25</td></tr><tr><td>4</td><td>4</td><td>9.50</td><td>0.73</td></tr></table>

The costs for the four models are computed as follows:

<table><tr><td>Model $i$</td><td>${EO}{C}_{i}\left( \$ \right)$</td><td>${EW}{C}_{i}\left( \$ \right)$</td><td>${ET}{C}_{i}\left( \$ \right)$</td></tr><tr><td>1</td><td>360.00</td><td>1000.00</td><td>1360.00</td></tr><tr><td>2</td><td>480.00</td><td>271.20</td><td>751.20</td></tr><tr><td>3</td><td>576.00</td><td>100.00</td><td>676.00</td></tr><tr><td>4</td><td>648.00</td><td>58.40</td><td>706.40</td></tr></table>

Model 3 produces the lowest cost.

## Example 18.9-2

In a multiclerk tool crib facility, requests for tool exchange occur according to a Poisson distribution at the rate of 17.5 requests per hour. Each clerk can handle an average of 10 requests per hour. The cost of hiring a new clerk in the facility is $\$ {12}$ an hour. The cost of lost production per waiting machine per hour is approximately \$50. Determine the optimal number of clerks for the facility.

The situation corresponds to an $\left( {M/M/c}\right)$ model in which it is desired to determine the optimum value of $c$ . Thus, in the general cost model presented at the start of this section, we put $x = c$ , resulting in the following cost model:

$$
{ETC}\left( c\right)  = {C}_{1}c + {C}_{2}{L}_{s}\left( c\right)
$$

$$
= {12c} + {50}{L}_{s}\left( c\right)
$$

Note that ${L}_{s}\left( c\right)$ is a function of the number of (parallel) clerks in the crib.

We use $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ with $\lambda  = {17.5}$ requests per hour and $\mu  = {10}$ requests per hour. Steady state is reached only if $c > \frac{\lambda }{\mu }$ -that is, $c \geq  2$ for the present example. The table below provides the necessary calculations for determining optimal $c$ . The values of ${L}_{s}\left( c\right)$ (determined by excelPoissonQ.xls or TORA) show that the optimum number of clerks is 4.

<table><tr><td>$c$</td><td>${L}_{s}\left( c\right)$ (requests)</td><td>ETC(c) (\$)</td></tr><tr><td>2</td><td>7.467</td><td>397.35</td></tr><tr><td>3</td><td>2.217</td><td>146.85</td></tr><tr><td>4</td><td>1.842</td><td>140.10</td></tr><tr><td>5</td><td>1.769</td><td>148.45</td></tr><tr><td>6</td><td>1.754</td><td>159.70</td></tr></table>

#### 18.9.2 Aspiration Level Model

The viability of the cost model depends on how well we can estimate the cost parameters. Generally, these parameters are difficult to estimate, particularly the one associated with the waiting time of customers. The aspiration level model alleviates this difficulty by working directly with the measures of performance of the queuing situation. The idea is to determine an acceptable range for the service level $\left( {\mu \text{ or }c}\right)$ by specifying reasonable limits on conflicting measures of performance. Such limits are the aspiration levels the decision maker wishes to reach.

![bo_d56m5ibef24c73bhe68g_34_387_200_619_400_0.jpg](bo_d56m5ibef24c73bhe68g_34_387_200_619_400_0.jpg)

FIGURE 18.10

Application of aspiration levels in queuing decision making

The model is applied to the multiple-server model to determine an "acceptable" number of servers, ${c}^{ * }$ , taking into account two (conflicting) measures of performance:

1. The average time in the system, ${W}_{s}$ .

2. The idleness percentage of the servers, $X$ .

The idleness percentage can be computed as follows:

$$
X = \frac{c - \bar{c}}{c} \times  {100} = \frac{c - \left( {{L}_{s} - {L}_{q}}\right) }{c} \times  {100} = \left( {1 - \frac{{\lambda }_{\text{ eff }}}{c\mu }}\right)  \times  {100}
$$

(See Problem 18-79 for the proof.)

The problem reduces to determining the number of servers ${c}^{ * }$ such that

$$
{W}_{s} \leq  \alpha \text{ and }X \leq  \beta
$$

The constants $\alpha$ and $\beta$ are the levels of aspiration specified by the decision maker. For example, $\alpha  = 3$ minutes and $\beta  = {10}\%$ .

The solution of the problem may be determined by plotting ${W}_{s}$ and $X$ as a function of $c$ , as shown in Figure 18.10. By locating $\alpha$ and $\beta$ on the graph, we can determine an acceptable range for ${c}^{ * }$ . If the two conditions cannot be satisfied simultaneously, then one or both must be relaxed before a feasible range can be found.

## Example 18.9-3

In Example 18.9-2, suppose that it is desired to determine the number of clerks such that the expected waiting time until a tool is received stays below 5 minutes. Simultaneously, the percentage of idleness should be below 20%.

Offhand, and before any calculations are made, an aspiration limit of 5 minutes on the waiting time until a tool is received (i.e., ${W}_{s} \leq  5$ minutes) is unreachable because, according to the data of the problem, the average service time alone is 6 minutes.

The following table summarizes ${W}_{s}$ and $X$ as a function of $c$ :

<table><tr><td>$c$</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td></tr><tr><td>${W}_{s}\left( \min \right)$</td><td>25.4</td><td>7.6</td><td>6.3</td><td>6.1</td><td>6.0</td><td>6.0</td><td>6.0</td></tr><tr><td>$X\left( \% \right)$</td><td>12.5</td><td>41.7</td><td>56.3</td><td>65.0</td><td>70.8</td><td>75.0</td><td>78.0</td></tr></table>

Based on these results, we should either reduce the service time or recognize that the source of the problem is that tools are being requested at an unreasonably high rate $(\lambda  = {17.5}$ requests per hour). This, most likely, is the area that should be addressed. For example, we may want to investigate the reason for such high demand for tool replacement. Could it be that the design of the tool itself is faulty? Or could it be that the operators of the machines are purposely trying to disrupt production to express grievances?

## BIBLIOGRAPHY

Bose, S., An Introduction to Queuing Systems, Kluwer Academic Publishers, Boston, 2001.

Chhajed, D, and T. Lowe (eds.) Building Intuition: Insights From Basic Operations Management Models and Principles (Chapter 5), Springer Science, New York, 2008.

Gross, D., and M. Harris, Fundamentals of Queuing Theory, 3rd ed., Wiley, New York, 1998.

Lee, A., Applied Queuing Theory, St. Martin's Press, New York, 1966.

Lipsky, L., Queuing Theory, A Linear Algebraic Approach, Macmillan, New York, 1992.

Saaty, T., Elements of Queuing Theory with Applications, Dover, New York, 1983.

Stone, A., "Why Waiting Is Torture," The New York Times, August 18, 2012.

Tanner, M., Practical Queuing Analysis, McGraw-Hill, New York, 1995.

## Case Study: Analysis of an Internal Transport System in a Manufacturing Plant ${}^{2}$

Tools: Queuing theory, simulation

Area of application: Materials handling

## Description of the situation:

Three trucks are used to transport materials in a manufacturing plant. The trucks wait in a central parking lot until requested. A requested truck will travel to the customer location, carry load to destination, and then return to the central parking lot. The principal user of the service is production (P) followed by the workshop (W) and maintenance (M). Other departments (O) occasionally may request the use of the trucks. Complaints about the long wait for a free truck have prompted users, especially production, to request adding a fourth truck to the fleet. The study deals with the justification of the cost for a fourth truck.

## Input data summary:

Information on the operation of the internal transport system was collected over a period of 17 consecutive two-shift work days. Tables 18.1 and 18.2 provide a summary of the collected data. In Table 18.1, we have the average rate of requests (arrival rate), the average time the truck is in use (service time), and the average waiting time for a request. Table 18.2 gives the number of trucks in use as a function of the number of requests made throughout the observation period.

---

${}^{2}$ Source: G. P. Cosmetatos,"The Value of Queuing Theory-A Case Study," Interfaces, Vol. 9, No. 3, pp. 47-51, 1979.

---

TABLE 18.1 Summary Data of the Operation of the Internal Transport System

<table><tr><td rowspan="2"></td><td colspan="5">Truck user</td></tr><tr><td>$P$</td><td>$W$</td><td>$M$</td><td>$O$</td><td>Overall</td></tr><tr><td>Average number of truck requests per hour</td><td>3.02</td><td>.84</td><td>.26</td><td>.48</td><td>4.6</td></tr><tr><td>Average in-use truck time per request (min)</td><td>18.0</td><td>25.0</td><td>32.0</td><td>20.0</td><td>20.3</td></tr><tr><td>Standard deviation of truck time per request (min)</td><td>8.0</td><td>11.0</td><td>15.0</td><td>14.0</td><td>10.6</td></tr><tr><td>Average waiting time for a truck request (min)</td><td>9.2</td><td>9.4</td><td>9.2</td><td>8.4</td><td>9.0</td></tr></table>

<table><tr><td colspan="6">TABLE 18.2 Number of Trucks in Use as a Function of the Number of Requests</td></tr><tr><td rowspan="2"></td><td colspan="4">Number of trucks in use at the time a request is made</td><td rowspan="2">Total</td></tr><tr><td>0</td><td>1</td><td>2</td><td>3</td></tr><tr><td>Number of requests</td><td>862</td><td>28</td><td>167</td><td>115</td><td>1172</td></tr><tr><td>Percentage of total</td><td>73.6</td><td>2.4</td><td>14.2</td><td>9.8</td><td></td></tr></table>

## Analysis of the situation:

Analysis of the raw data used to obtain the information in Table 18.1 yields the following observations:

1. Requests for truck use are random and can be represented by a Poisson distribution.

2. The service time (in-use truck time from the moment it travels to the customer until it returns to the parking lot) is unimodal and skewed and does not appear to follow an exponential distribution. Perhaps the triangular distribution can be used to approximate the situation in this case.

3. Although no priority or allocation of trucks to users is in operation, truck drivers tend to show preference to closer customers.

The data in Table 18.2 lead to two observations:

a. In 73.6% of the requests, all three trucks are idle.

b. In only 9.8% of the requests, all three trucks are in use.

Because arrivals are random and can be described by a Poisson distribution and the service time is not exponential distribution, the queuing model that best represents the problem is the $M/G/c/\infty /\infty$ . However, computations for the $M/G/c$ model are not easily tractable. As a result, it is decided that an equivalent $M/M/c$ model may be used to provide an upper-bound estimate on the waiting time in the queue. The justification is that exponential service time is the "most random" of all distributions and hence will result in a worst-case scenario for the present situation. (By the same logic, the $M/D/c$ model provides a lower bound on the average queuing time because the service time is constant and hence represents the "least random" case.)

The following is a summary of the results of the $M/M/c$ model for $c = 3,\lambda  = \frac{4.6}{60} = {.0767}$ request per minute and $\mu  = \frac{1}{20.3} = {.0493}$ service per minute:

Probability that the system is empty, ${p}_{0} = {.197}$

Probability of at least three requests in the system, ${p}_{n \geq  3} = {.133}$

Average length of queue, ${L}_{q} = {.277}$ request

Average waiting time in queue, ${W}_{q} = {3.6}\mathrm{\;{min}}$

Looking at these results, one notices the perplexing observation that the upper bound on the average waiting time in the queue (estimated from the $M/M/c$ model) is much lower than what is actually observed ( ${W}_{q} = {3.6}\mathrm{\;{min}}$ versus the observed 9.0 minutes given in Table 18.2). This observation leads to one of two conclusions: Either the estimates of $\lambda$ and $\mu$ are inaccurate or the estimate of the average waiting is unreliable. A careful study of the data shows that the data are indeed reliable. To reinforce the results of the $M/M/c$ model, simulation is used in which the service-time distribution is approximated by a triangular distribution with parameters (15, 20.3, 30). The middle value represents the observed average service time and the lower and upper values are estimated based on the standard deviation of service time $\left( { = {10.6}\mathrm{\;{min}}}\right)$ and the observed minimum and maximum service times. The simulation can be carried out using Excel template excelMultiServer.xls with Poisson arrival rate of .0767 request per minute and triangular service time. With 10 replications that simulate 450 requests each, the average queuing time was found to vary from a minimum of 1.1 minutes to a maximum of 3.62 minutes and an average value of 2.07 minutes. This result gave more credence to the upper-bound result of 3.6 minutes obtained from the $M/M/c$ model. Moreover, the high waiting time obtained from the observed data ( $= {9.0}\mathrm{\;{min}}$ ) seems to contradict the data in Table 18.2, where 73.6% of the time all three trucks were idle when a service request arrived.

How can this inconsistency between observed and estimated results be explained? Going back to the plant floor to further study the operation of the transport system, an analyst made a fortunate observation: The layout of the parking lot was such that waiting trucks could not be seen by the users, who then assumed that no trucks were available. This in essence was equivalent to operating with less than three trucks, which in turn resulted in an artificial increase in waiting time. Once this problem had been discovered, the solution became obvious: Provide the truck drivers and the users with a two-way communication system. The proposed solution led to immediate improvement in service and a noticeable decrease in the waiting time.

Although the proposed solution was not "propelled" by queuing results in a direct manner, it was the logic inherent in queuing analysis that led to the discovery of data inconsistency and, hence, to pinpointing the source of the problem.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td><td>Section</td><td>Assigned Problems</td></tr><tr><td>18.1</td><td>18-1 to 18-2</td><td>18.6.2</td><td>18-50 to 18-67</td></tr><tr><td>18.2</td><td>18-3 to 18-7</td><td>18.6.3</td><td>18-68 to 18-94</td></tr><tr><td>18.3</td><td>18-8 to 18-20</td><td>18.6.4</td><td>18-95 to 18-103</td></tr><tr><td>18.4.1</td><td>18-21 to 18-28</td><td>18.7</td><td>18-104 to 18-112</td></tr><tr><td>18.4.2</td><td>18-29 to 18-38</td><td>18.9.1</td><td>18-113 to 18-125</td></tr><tr><td>18.5</td><td>18-39 to 18-47</td><td>18.9.2</td><td>18-126 to 18-127</td></tr><tr><td>18.6.1</td><td>18-48 to 18-49</td><td></td><td></td></tr></table>

*18-1. Suppose that further analysis of the McBurger restaurant (Example 18.1-1) reveals the following additional results:

<table><tr><td>Number of cashiers</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td></tr><tr><td>Idleness (%)</td><td>0</td><td>8</td><td>12</td><td>18</td><td>29</td><td>36</td><td>42</td></tr></table>

(a) What is the productivity of the operation (expressed as the percentage of time the employees are busy) when the number of cashiers is five?

(b) The manager wants to keep the average waiting time around 3 minutes and, simultaneously, maintain the efficiency of the facility at approximately 90%. Can the two goals be achieved? Explain.

18-2. Acme Metal Jobshop is in the process of purchasing a multipurpose drill press. Two models, $A$ and $B$ , are available with hourly operating costs of \$20 and \$35, respectively. Model $A$ is slower than model $B$ . Queuing analysis of similar machines shows that when $A$ is used, the average number of jobs in the queue is 4, which is ${30}\%$ higher than the queue size in $B$ . A delayed job represents lost income, which is estimated by Acme at \$10 per waiting job per hour. Which model should Acme purchase?

18-3. In each of the following situations, identify the customer and the server:

*(a) Planes arriving at an airport.

*(b) Taxi stand serving waiting passengers.

(c) Tools checked out from a crib in a machining shop.

(d) Letters processed in a post office.

(e) Registration for classes in a university.

(f) Legal court cases.

(g) Checkout operation in a supermarket.

*(h) Parking lot operation.

18-4. For each of the situations in Problem 18-3, identify the following: (a) nature of the calling source (finite or infinite), (b) nature of arriving customers (individually or in bulk), (c) type of the interarrival time (probabilistic or deterministic), (d) definition and type of service time, (f) queue capacity (finite or infinite), and (g) queue discipline.

18-5. Study the following system and identify the associated queuing situations. For each situation, define the customers, the server(s), the queue discipline, the service time, the maximum queue length, and the calling source. Orders for jobs are received at a workshop for processing. On receipt, the supervisor decides whether it is a rush or a regular job. Some orders require the use of one of several identical machines. The remaining orders are processed in a two-stage production line, of which two are available. In each group, one facility is assigned to handle rush jobs. Jobs arriving at any facility are processed in order of arrival. Completed orders are shipped on arrival from a shipping zone having a limited capacity. Sharpened tools for the different machines are supplied from a central tool crib. When a machine breaks down, a repairperson is summoned from the service pool to make the repair. Machines working on rush orders always receive priorities both in acquiring new tools from the crib and in receiving repair service.

18-6. True or False?

(a) An impatient waiting customer may not elect to renege.

(b) If a long waiting time is anticipated, an arriving customer may not elect to balk.

(c) Jockeying from one queue to another is exercised in hope of reducing waiting time.

18-7. In each of the situations in Problem 18-3, discuss the possibility of the customers jockeying, balking, and reneging.

18-8. (a) Explain your understanding of the relationship between the arrival rate $\lambda$ and the average interarrival time. What are the units describing each parameter?

(b) In each of the following cases, determine the average arrival rate per hour, $\lambda$ , and the average interarrival time in hours.

*(i) One arrival occurs every 20 minutes.

(ii) Two arrivals occur every 6 minutes.

(iii) Number of arrivals in a 30-minute period is 10.

(iv) The average interval between successive arrivals is .5 hour.

(c) In each of the following cases, determine the average service rate per hour, $\mu$ , and the average service time in hours.

*(i) One service is completed every 15 minutes.

(ii) Two departures occur every 15 minutes.

(iii) Number of customers served in a 30-minute period is 5.

(iv) The average service time is .3 hour.

18-9. In Example 18.3-1, determine the following:

(a) The average number of failures per day, assuming the service is offered 24 hours a day, 7 days a week.

(b) The probability of at least one failure in a 3-hour period.

(c) The probability that the next failure will not occur within 4 hours.

(d) If no failure has occurred 3 hours after the last failure, what is the probability that interfailure time is at least 5 hours?

18-10. The time between arrivals at the State Revenue Office is exponential with mean value .04 hour. The office opens at 8:00 A.M.

*(a) Write the exponential distribution that describes the interarrival time.

*(b) Find the probability that no customers will arrive at the office by 8:15 A.M.

(c) It is now 8:35 A.M. The last customer entered the office at 8:26. What is the probability that the next customer will arrive before 8:38 A.M.? That the next customer will not arrive by 8:40 A.M.?

(d) What is the average number of arriving customers between 8:10 and 8:45 A.M.?

18-11. Suppose that the time between breakdowns for a machine is exponential with mean 5 hours. If the machine has worked without failure during the last 4 hours, what is the probability that it will continue without failure during the next 2 hours? That it will break down during the next hour?

18-12. The time between arrivals at the game room in the student union is exponential, with mean 10 minutes.

(a) What is the arrival rate per hour?

(b) What is the probability that no students will arrive at the game room during the next 15 minutes?

(c) What is the probability that at least one student will visit the game room during the next 20 minutes?

18-13. The manager of a new fast-food restaurant wants to quantify the arrival process of customers by estimating the fraction of interarrival time intervals that will be (a) less than 1 minutes, (b) between 1 and 2 minutes, and (c) more than 2 minutes. Arrivals in similar restaurants occur at the rate of 20 customers per hour. The interarrival time is exponentially distributed.

*18-14. Ann and Jim, two employees in a fast-food restaurant, play the following game while waiting for customers to arrive: Jim pays Ann 2 cents if the next customer does not arrive within 1 minute; otherwise, Ann pays Jim 2 cents. Determine Jim's average payoff in an 8-hr period. The interarrival time is exponential with mean 1.5 minute.

18-15. Suppose that in Problem 18-14 the rules of the game are such that Jim pays Ann 2 cents if the next customer arrives after 1.5 minutes, and Ann pays Jim an equal amount if the next arrival is within 1 minute. For arrivals within the range 1 to 1.5 minutes, the game is a draw. Determine Jim's expected payoff in an 8-hr period.

18-16. In Problem 18-14, suppose that Ann pays Jim 2 cents if the next arrival occurs within 1 minute and 3 cents if the interarrival time is between 1 and 1.5 minutes. Ann receives from Jim 5 cents if the interarrival time is between 1.5 and 2 minutes and 6 cents if it is larger than 2 minutes. Determine Ann's expected payoff in an 8-hour period.

*18-17. A customer arriving at a McBurger fast-food restaurant within 4 minutes of the immediately preceding customer will receive a 10% discount. If the interarrival time is between 4 and 5 minutes, the discount is 6%. If the interarrival time is longer than 5 minutes, the customer gets 2% discount. The interarrival time is exponential with mean 6 minutes.

(a) Determine the probability that an arriving customer will receive the 10% discount.

(b) Determine the average discount per arriving customer.

18-18. The time between failures of a Kencore refrigerator is known to be exponential with mean value 9000 hrs (about 1 year of operation), and the company issues a 1-year warranty on the refrigerator. What are the chances that a breakdown repair will be covered by the warranty?

18-19. The U of A runs two bus lines on campus: red and green. The red line serves north campus, and the green line serves south campus with a transfer station linking the two lines. Green buses arrive randomly (exponential interarrival time) at the transfer station every 10 minutes. Red buses also arrive randomly every 7 minutes.

(a) What is the probability distribution of the waiting time for a student arriving on the red line to get on the green line?

(b) What is the probability distribution of the waiting time for a student arriving on the green line to get on the red line?

18-20. Prove that the mean and standard deviation of the exponential distribution are equal.

*18-21. In Example 18.4-1, suppose that the clerk who enters the information from birth certificates into the computer normally waits until at least 6 certificates have accumulated. Find the probability that the clerk will be entering a new batch every hour.

18-22. An art collector travels to art auctions once a month on the average. Each trip is guaranteed to produce one purchase. The time between trips is exponentially distributed. Determine the following:

(a) The probability that no purchase is made in a 2-month period.

(b) The probability that no more than 6 purchases are made per year.

(c) The probability that the time between successive trips will exceed 2 month.

18-23. In a bank operation, the arrival rate is 3 customers per minute. Determine the following:

(a) The average number of arrivals during 10 minutes.

(b) The probability that no arrivals will occur during the next minute.

(c) The probability that at least one arrival will occur during the next minute.

(d) The probability that the time between two successive arrivals is at least 2 minutes.

18-24. The time between arrivals at L&J restaurant is exponential with mean 5 minutes. The restaurant opens for business at 11:00 A.M. Determine the following:

*(a) The probability of having 10 arrivals in the restaurant by 11:12 A.M., given that 4 customers arrived by 11:05 A.M.

(b) The probability that a new customer will arrive between 11:29 and 11:36 A.M., given that the last customer arrived at 11:25 A.M.

18-25. The Springdale Public Library receives new books according to a Poisson distribution with mean 25 books per day. Each shelf in the stacks holds 100 books. Determine the following:

(a) The average number of shelves that will be stacked with new books each (30-day) month.

(b) The probability that more than 10 bookcases will be needed each month, given that a bookcase has 5 shelves.

18-26. The $\mathrm{U}$ of $\mathrm{A}$ runs two bus lines on campus: red and green. The red line serves north campus and the green line serves south campus with a transfer station linking the two lines. Green buses arrive randomly (according to a Poisson distribution) at the transfer station every 10 minutes. Red buses also arrive randomly every 7 minutes.

*(a) What is the probability that two buses (red and/or green) will stop at the station during a 5-minute interval?

(b) A student whose dormitory is located next to the station has a class in 10 minutes. Either bus will take the student to the classroom building. The ride takes 5 minutes, after which the student will walk for about 3 minutes to reach the classroom. What is the probability that the student will make it to class on time?

18-27. Prove that the mean and variance of the Poisson distribution during an interval $t$ equal ${\lambda t}$ , where $\lambda$ is the arrival rate.

18-28. Derive the Poisson distribution from the difference-differential equations of the pure birth model. Hint:The solution of the general differential equation

$$
{y}^{\prime } + a\left( t\right) y = b\left( t\right)
$$

is

$$
y = {e}^{-\int a\left( t\right) {dt}}\left\{  {\int b\left( t\right) {e}^{\int a\left( t\right) }{dt} + \text{ constant }}\right.
$$

18-29. In Example 18.4-2, use excelPoissonQ.xls or TORA to compute ${p}_{n}\left( 7\right) , n = 1,2,\ldots ,{18}$ , and then verify manually that these probabilities yield $E\{ n \mid  t = 7 \mid  \}  = {.664}$ dozen.

18-30. Consider Example 18.4-2. In each of the following cases, first write the answer algebraically, and then use excelPoissonQ.xls or TORA to provide numerical answers.

*(a) The probability that the stock is depleted after 3 days.

(b) The average number of dozen roses left at the end of the second day.

*(c) The probability that at least one dozen is purchased by the end of the fourth day, given that the last dozen was bought at the end of the third day.

(d) The probability that the time remaining until the next purchase is at most half a day, given that the last purchase occurred a day earlier.

(e) The probability that no purchases will occur during the first day.

(f) The probability that no order will be placed by the end of the week.

18-31. The Springdale High School band is performing a benefit concert in its new 400-seat auditorium. Local businesses buy the tickets in blocks of 5 and donate them to youth organizations. Tickets go on sale to business entities for 5 hours only the day before the concert. The process of placing orders for tickets is Poisson with a mean 12 calls per hour. Any (blocks of) tickets remaining after the box office is closed are sold at a discount as "rush tickets" 1 hour before the concert starts. Determine

(a) The probability that it will be possible to buy rush tickets.

(b) The average number of rush tickets available.

18-32. Each morning, the refrigerator in a small machine shop is stocked with two cases (24 cans per case) of soft drinks for use by the shop's 12 employees. The employees can quench their thirst at any time during the 8-hour work day (8:00 A.M. to 4:00 P.M.), and each employee is known to consume approximately 4 cans a day, but the process is totally random (Poisson distribution). What is the probability that an employee will not find a drink at noon (the start of the lunch period)? Just before the shop closes?

*18-33. A freshman student receives a bank deposit of \$100 a month from home to cover incidentals. Withdrawal checks of \$20 each occur randomly during the month and are spaced according to an exponential distribution with a mean value of 1 week. Determine the probability that the student will run out of incidental money before the end of the fourth week.

18-34. Inventory is withdrawn from a stock of 80 items according to a Poisson distribution at the rate of 5 items per day. Determine the following:

(a) The probability that 10 items are withdrawn during the first 2 days.

(b) The probability that no items are left at the end of 4 days.

(c) The average number of items withdrawn over a 4-day period.

18-35. A machine shop has just stocked 10 spare parts for the repair of a machine. Stock replenishment that brings the stock level back to 10 pieces occurs every 7 days. The time between breakdowns is exponential with mean 1 day. Determine the probability that the machine will remain broken for 2 days because no spare parts are available.

18-36. Demand for an item occurs according to a Poisson distribution with mean 3 per day. The maximum stock level is 25 items, which occurs on each Monday immediately after a new order is received. The order size depends on the number of units left at the end of the week on Saturday (business is closed on Sundays). Determine the following:

*(a) The average weekly size of the order.

*(b) The probability of shortage at the start of business on Friday.

(c) The probability that the weekly order size exceeds 10 units.

18-37. Prove that the distribution of the time between departures corresponding to the truncated Poisson in the pure death model is an exponential distribution with mean $\frac{1}{\mu }$ time units.

18-38. Derive the truncated Poisson distribution from the difference-differential equations of the pure death model using induction. [Note: See the hint in Problem 18-28.]

18-39. In Example 18.5-1, determine the following:

(a) The probability distribution of the number of open counters.

(b) The average number of busy counters.

18-40. In the B&K model of Example 18.5-1, suppose that the interarrival time at the checkout area is exponential with mean 8 minutes and that the checkout time per customer is also exponential with mean 12 minutes. Suppose further that B&K will add a fourth counter. Counters 1, 2, and 3 will open based on increments of two customers and counter 4 will open when there are 7 or more in the store. Determine the following:

(a) The steady-state probabilities, ${p}_{n}$ for all $n$ .

(b) The probability that a fourth counter will be needed.

(c) The average number of idle counters.

*18-41. In the B&K model of Example 18.5-1, suppose that all three counters are always open and that the operation is set up such that the customer will go to the first empty counter. Determine the following:

(a) The probability that all three counters will be in use.

(b) The probability that an arriving customer will not wait.

18-42. First Bank of Springdale operates a one-lane drive-in ATM machine. Cars arrive according to a Poisson distribution at the rate of 10 cars per hour. The time per car needed to complete the ATM transaction is exponential with mean 5 minutes. The lane can accommodate a total of 10 cars. Once the lane is full, other arriving cars seek service in another branch. Determine the following:

(a) The probability that an arriving car will not be able to use the ATM machine because the lane is full.

(b) The probability that a car will not be able to use the ATM machine immediately on arrival.

(c) The average number of cars in the lane.

18-43. Have you ever heard someone repeat the contradictory statement, "The place is so crowded no one goes there any more"? This statement can be interpreted as saying that the opportunity for balking increases with the increase in the number of customers seeking service. A possible platform for modeling this situation is to say that the arrival rate at the system decreases as the number of customers in the system increases. More specifically, we consider the simplified case of M&M Pool Club, where customers usually arrive in pairs to "shoot pool." The normal arrival rate is 6 pairs (of people) per hour. However, once the number of pairs in the pool hall exceeds 8 , the arrival rate drops to 5 pairs per hour. The arrival process is assumed to follow the Poisson distribution. Each pair shoots pool for an exponential time with mean 30 minutes. The pool hall has a total of 5 tables and can accommodate no more than 12 pairs at any one time. Determine the following:

(a) The probability that customers will begin balking.

(b) The probability that all tables are in use.

(c) The average number of tables in use.

(d) The average number of pairs waiting for a pool table to be available.

*18-44. A barbershop serves one customer at a time and provides three seats for waiting customers. If the place is full, customers go elsewhere. Arrivals occur according to a Poisson distribution with mean four per hour. The time to get a haircut is exponential with mean 15 minutes. Determine the following:

(a) The steady-state probabilities.

(b) The expected number of customers in the shop.

(c) The probability that customers will go elsewhere because the shop is full.

18-45. Consider a one-server queuing situation in which the arrival and service rates are given by

$$
{\lambda }_{n} = {10} - n, n = 0,1,2,3
$$

$$
{\mu }_{n} = \frac{n}{2} + 5, n = 1,2,3,4
$$

This situation is equivalent to reducing the arrival rate and increasing the service rate as the number in the system, $n$ , increases.

(a) Set up the transition diagram and determine the balance equation for the system.

(b) Determine the steady-state probabilities.

18-46. Consider the single-queue model where only one customer is allowed in the system. Customers who arrive and find the facility busy never return. Assume that the arrivals distribution is Poisson with mean $\lambda$ per unit time and that the service time is exponential with mean $\frac{1}{\mu }$ time units.

(a) Set up the transition diagram and determine the balance equations.

(b) Determine the steady-state probabilities.

(c) Determine the average number in the system.

18-47. The induction proof for deriving the general solution of the generalized model is applied as follows. Consider

$$
{p}_{k} = \mathop{\prod }\limits_{{i = 0}}^{{k - 1}}\left( \frac{{\lambda }_{i}}{{\mu }_{i + 1}}\right) {p}_{0, k}k = 0,1,2,\ldots
$$

We substitute for ${p}_{n - 1}$ and ${p}_{n - 2}$ in the general difference equation involving ${p}_{n},{p}_{n - 1}$ , and ${p}_{n - 2}$ to derive the desired expression for ${p}_{n}$ . Verify this procedure.

18-48. In Example 18.6-1, do the following:

*(a) Compute ${L}_{q}$ directly using the formula $\mathop{\sum }\limits_{{n = c + 1}}^{\infty }\left( {n - c}\right) {p}_{n}$ .

(b) Compute ${W}_{s}$ from ${L}_{q}$ .

*(c) Compute the average number of cars that will not be able to enter the parking lot during an 8-hr period.

*(d) By definition, the average number of empty spaces can be computed as $c - \left( {{L}_{s} - {L}_{q}}\right)$ or $\mathop{\sum }\limits_{{n = 0}}^{{c - 1}}\left( {c - n}\right) {p}_{n}$ . Show that the second definition can be derived directly from the first using algebraic manipulations.

18-49. Solve Example 18.6-1 using the following data: number of parking spaces $= 6$ , number of temporary spaces $= 4,\lambda  = {10}$ cars per hour, and average parking time $= {45}$ minutes.

18-50. In Example 18.6-2, do the following.

(a) Determine the percent utilization of the wash bay.

(b) Determine the probability that an arriving car must wait in the parking lot prior to entering the wash bay.

(c) If there are six parking spaces, determine the probability that an arriving car will find an empty parking space.

(d) How many parking spaces should be provided so that an arriving car may find a parking space 95% of the time?

*18-51. John Macko is a student at Ozark U. He does odd jobs to supplement his income. Job requests come every 5 days on the average, but the time between requests is exponential. The time for completing a job is also exponential with mean 4 days.

(a) What is the probability that John will be out of jobs?

(b) If John gets about \$50 a job, what is his average monthly income?

(c) If at the end of the semester, John decides to subcontract on the outstanding jobs at \$40 each. How much, on the average, should he expect to pay?

18-52. Over the years, Detective Columbo, of the Fayetteville Police Department, has had phenomenal success in solving every single crime case. It is only a matter of time before any case is solved. Columbo admits that the time per case is "totally random," but, on the average, each investigation will take about a week and half. Crimes in peaceful Fayetteville are not very common. They occur randomly at the rate of one crime per (4-week) month. Detective Columbo is asking for an assistant to share the heavy workload. Analyze Columbo's claim, particularly from the standpoint of the following points:

(a) The average number of cases awaiting investigation.

(b) The percentage of time the detective remains busy.

(c) The average time needed to solve a case.

18-53. Cars arrive at the Lincoln Tunnel toll gate according to a Poisson distribution, with a mean of 90 cars per hour. The time for passing the gate is exponential with mean 38 seconds. Drivers complain of the long waiting time, and authorities are willing to reduce the average passing time to 30 seconds by installing automatic toll-collecting devices, provided two conditions are satisfied: (1) the average number of waiting cars in the present system exceeds 5 and (2) the percentage of the gate idle time with the new device installed does not exceed 10%. Can the new device be justified?

*18-54. A fast-food restaurant has one drive-in window. Cars arrive according to a Poisson distribution at the rate of 2 cars every 5 minutes. The space in front of the window can accommodate at most 10 cars, including the one being served. Other cars can wait outside this space if necessary. The service time per customer is exponential, with a mean of 1.5 minutes. Determine the following:

(a) The probability that the facility is idle.

(b) The expected number of customers waiting to be served.

(c) The expected waiting time until a customer reaches the window to place an order.

(d) The probability that the waiting line will exceed the 10-space capacity.

18-55. Customers arrive at a one-window drive-in bank according to a Poisson distribution, with a mean of 10 per hour. The service time per customer is exponential, with a mean of 5 minutes. There are three spaces in front of the window, including the car being served. Other arriving cars line up outside this 3-car space.

(a) What is the probability that an arriving car can enter one of the 3-car spaces?

(b) What is the probability that an arriving car will wait outside the designated 3-car space?

(c) How long is an arriving customer expected to wait before starting service?

*(d) How many car spaces should be provided in front of the window (including the car being served) so that an arriving car can find a space there at least 90% of the time?

18-56. In the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ , give a plausible argument as to why ${L}_{s}$ does not equal ${L}_{q} + 1$ , in general. Under what condition will the equality hold?

18-57. For the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ , derive the expression for ${L}_{q}$ using the basic definition $\mathop{\sum }\limits_{{n = 2}}^{\infty }\left( {n - 1}\right) {p}_{n}$ .

18-58. For the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ , show that

(a) The expected number in the queue, given that the queue is not empty, $= \frac{1}{\left( 1 - \rho \right) }$ .

(b) The expected waiting time in the queue for those who must wait $= \left( \frac{1}{\mu  - \lambda }\right)$ .

*18-59. In Example 18.6-4, determine the following:

(a) Probability that an arriving car will go into the wash bay immediately on arrival.

(b) Expected waiting time until a service starts.

(c) Expected number of empty parking spaces.

(d) Probability that all parking spaces are occupied.

(e) Percent reduction in average service time that will limit the average time in the system to about 10 minutes. (Hint: Use trial and error with excelPoissonQ.xls or TORA.)

18-60. Consider the car wash facility of Example 18.6-4. Determine the number of parking spaces such that the percentage of cars that cannot find a space does not exceed 3%.

18-61. The time barber Joe takes to give a haircut is exponential with a mean of 12 minutes. Because of his popularity, customers usually arrive (according to a Poisson distribution) at a rate much higher than Joe can handle: six customers per hour. Joe will really feel comfortable if the arrival rate is effectively reduced to about four customers per hour. To accomplish this goal, he came up with the idea of providing limited seating in the waiting area so that newly arriving customers will go elsewhere when they discover that all the seats are taken. How many seats should Joe provide to accomplish his goal?

*18-62. The final assembly of electric generators at Electro is produced at the Poisson rate of 10 generators per hour. The generators are then conveyed on a belt to the inspection department for final testing. The belt can hold a maximum of 7 generators. An electronic sensor will automatically stop the conveyor once it is full, preventing the final assembly department from assembling more units until a space becomes available. The time to inspect the generators is exponential, with a mean of 15 minutes.

(a) What is the probability that the final assembly department will stop production?

(b) What is the average number of generators on the conveyor belt?

(c) The production engineer claims that interruptions in the assembly department can be reduced by increasing the capacity of the belt. In fact, the engineer claims that the capacity can be increased to the point where the assembly department can operate 95% of the time without interruption. Is this claim justifiable?

18-63. A cafeteria can seat a maximum of 50 persons. Customers arrive in a Poisson stream at the rate of 10 per hour and are served (one at a time) at the rate of 12 per hour.

(a) What is the probability that an arriving customer will not eat in the cafeteria because it is full?

(b) Suppose that three customers (with random arrival times) would like to be seated together. What is the probability that their wish can be fulfilled? (Assume that arrangements can be made to seat them together as long as three seats are available.)

18-64. Patients arrive at a 1-doctor clinic according to a Poisson distribution at the rate of 20 patients per hour. The waiting room does not accommodate more than 14 patients. Examination time per patient is exponential, with a mean of 8 minutes.

(a) What is the probability that an arriving patient will not wait?

(b) What is the probability that an arriving patient will find a seat in the room?

(c) What is the expected total time a patient spends in the clinic?

18-65. The probabilities ${p}_{n}$ of $n$ customers in the system for an $\left( {M/M/1}\right)  : \left( {{GD}/5/\infty }\right)$ are given in the following table:

<table><tr><td>$n$</td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td></tr><tr><td>${p}_{n}$</td><td>.399</td><td>.249</td><td>.156</td><td>.097</td><td>.061</td><td>.038</td></tr></table>

The arrival rate $\lambda$ is five customers per hour. The service rate $\mu$ is eight customers per hour. Compute the following:

*(a) Probability that an arriving customer will be able to enter the system.

*(b) Rate at which arriving customers will not be able to enter the system.

(c) Expected number in the system.

(d) Average waiting time in the queue.

18-66. Show that when $\rho  = 1$ for $\left( {M/M/1}\right)  : \left( {{GD}/N/\infty }\right)$ , the expected number in the system, ${L}_{s}$ , equals $\frac{N}{2}$ . (Hint: $1 + 2 + \ldots  + i = \frac{i\left( {i + 1}\right) }{2}$ .)

18-67. Show that ${\lambda }_{\text{ eff }}$ for $\left( {M/M/1}\right)  : \left( {{GD}/N/\infty }\right)$ can be computed from the formula

$$
{\lambda }_{\text{ eff }} = \mu \left( {{L}_{s} - {L}_{q}}\right)
$$

18-68. Consider Example 18.6-5.

(a) Show that the remarkable reduction in waiting time by more than 50% for the consolidated case is coupled with an increase in the percentage of time the servers remain busy.

(b) Suppose that calls for cab service in the consolidated company is increased to 20 customers per hour. What is the minimum number of cabs the company should employ?

(c) In Part (b), determine the minimum number of cabs that would limit the average waiting time for a ride to less than 5 minutes.

*18-69. In the cab company example, suppose that the average time per ride is actually about 14.5 minutes, so that the utilization $\left( { = \frac{\lambda }{\mu c}}\right)$ for the 2- and 4-cab operations increases to more than 96%. Is it still worthwhile to consolidate the two companies into one? Use the average waiting time for a ride as the comparison measure.

18-70. Determine the minimum number of parallel servers needed in each of the following (Poisson arrival/departure) situations to guarantee that the operation of the queuing situation will be stable (i.e., the queue length will not grow indefinitely):

(a) Customers arrive every 6 minutes and are served at the rate of 10 customers per hour.

(b) The average interarrival time is 3 minutes, and the average service time is 6 minutes.

(c) The arrival rate is 25 customers per hour, and the service rate per server is 40 customers per hour.

18-71. Customers arrive at Thrift Bank according to a Poisson distribution, with a mean of 45 customers per hour. Transactions per customer last about 5 minutes and are exponentially distributed. The bank wants to use a single-line multiple-teller operation, similar to the ones used in airports and post offices. The manager is conscious of the fact that customers may switch to other banks if they perceive that their wait in line is "excessive." For this reason, the manager wants to limit the average waiting time in the queue to no more than 3 minutes. How many tellers should the bank provide?

*18-72. McBurger fast-food restaurant has 3 cashiers. Customers arrive according to a Poisson distribution every 3 minutes and form one line to be served by the first available cashier. The time to fill an order is exponentially distributed with a mean of 5 minutes. The waiting room inside the restaurant is limited. However, the food is good, and customers are willing to line up outside the restaurant, if necessary. Determine the size of the waiting room inside the restaurant (excluding those at the cashiers) such that the probability that an arriving customer does not wait outside the restaurant is at least .999.

18-73. A small post office has two open windows. Customers arrive according to a Poisson distribution at the rate of 1 every 3 minutes. However, only 80% of them seek service at the windows. The service time per customer is exponential, with a mean of 5 minutes. All arriving customers form one line and access available windows on a FIFO basis.

(a) What is the probability that an arriving customer will wait in line?

(b) What is the probability that both windows are idle?

(c) What is the average length of the waiting line?

(d) Would it be possible to offer reasonable service with only one window? Explain.

18-74. The $\mathrm{U}$ of $\mathrm{A}$ computer center is equipped with four identical mainframe computers. The number of users at any time is 25. Each user is capable of submitting a job from a terminal every 15 minutes, on the average, but the actual time between submissions is exponential. Arriving jobs will automatically go to the first available computer. The execution time per submission is exponential with mean 2 minutes. Compute the following:

*(a) The probability that a job is not executed immediately upon submission.

(b) The average time until the output of a job is returned to the user.

(c) The average number of jobs awaiting execution.

(d) The percentage of time the entire computer center is idle.

*(e) The average number of idle computers.

18-75. Drake Airport services rural, suburban, and transit passengers. The arrival distribution for each of the three groups is Poisson with mean rates of 15, 10, and 20 passengers per hour, respectively. The time to check in a passenger is exponential with mean 6 minutes. Determine the number of counters that should be provided at Drake under each of the following conditions:

(a) The total average time to check a customer in is less than 15 minutes.

(b) The percentage of idleness of the counters does not exceed 10%.

(c) The probability that all counters are idle does not exceed .01.

18-76. In the United States, the use of single-line, multiple-server queues is common in post offices and in passenger check-in counters at airports. However, both grocery stores and banks (especially in smaller communities) tend to favor single-line, single-server setups, despite the fact that single-line, multiple-server queues offer a more efficient operation. Comment on this observation.

18-77. For the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model, Morse (1958, p. 103) shows that as $\frac{\rho }{c} \rightarrow  1$ ,

$$
{L}_{q} = \frac{\rho }{c - \rho }
$$

Noting that $\frac{\rho }{c} \rightarrow  1$ means that the servers are extremely busy, use this information to show that the ratio of the average waiting time in queue in the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model to that in the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ model approaches $\frac{1}{c}$ as $\frac{\rho }{c} \rightarrow  1$ . Thus, for $c = 2$ , the average waiting time can be reduced by ${50}\%$ . The conclusion from this exercise is that it is always advisable to pool services regardless of how "overloaded" the servers may be.

18-78. In the derivation of ${p}_{n}$ for the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model, indicate which part of the derivation requires the condition $\frac{\rho }{c} < 1$ . Explain verbally the meaning of the condition. What will happen if the condition is not satisfied?

18-79. Prove that ${L}_{s} = {L}_{q} + \bar{c}$ starting with the definition ${L}_{q} = \mathop{\sum }\limits_{{n = c + 1}}^{\infty }\left( {n - C}\right) {p}_{n}$ , where $\bar{c}$ is the average number of busy servers. Hence, show that $\bar{c} = \frac{{\lambda }_{\text{ eff }}}{\mu }$ .

18-80. Show that ${p}_{n}$ for the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ model can be obtained from that of the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model by setting $c = 1$ .

18-81. Show that for the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model

$$
{L}_{q} = \frac{c\rho }{{\left( c - \rho \right) }^{2}}{p}_{c}
$$

18-82. For the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model, show the following:

(a) The probability that a customer is waiting is $\frac{\rho }{\left( c - \rho \right) }{p}_{c}$ .

(b) The average number in the queue given that it is not empty is $\frac{c}{\left( c - \rho \right) }$ .

(c) The expected waiting time in the queue for customers who must wait is $\frac{1}{\mu \left( {c - \rho }\right) }$ .

18-83. In Example 18.6-6, determine the following:

(a) The expected number of idle cabs.

(b) The probability that a calling customer will be next to last on the list.

(c) The limit on the waiting list if it is desired to keep the waiting time in the queue to below 3.5 minutes.

18-84. Eat & Gas convenience store operates a two-pump gas station. The lane leading to the pumps can house at most 3 cars, excluding those being serviced. Arriving cars go elsewhere if the lane is full. The distribution of arriving cars is Poisson with mean 20 per hour. The time to fill up and pay for the purchase is exponential with mean 6 minutes. Determine the following:

(a) Percentage of cars that will seek business elsewhere.

(b) Percentage of time both pumps are in use.

*(c) Percent utilization of the two pumps.

*(d) Probability that an arriving car will not start service immediately, but will find an empty space in the lane.

(e) Capacity of the lane that will ensure that, on the average, no more than 10% of the arriving cars are turned away.

(f) Capacity of the lane that will ensure that the probability that both pumps are idle is .1 or less.

18-85. A small engine repair shop is run by three mechanics. Early in March of each year, people bring in their tillers and lawn mowers for service and maintenance. The shop is willing to accept all the tillers and mowers that customers bring in. However, when new customers see the floor of the shop covered with waiting jobs, they go elsewhere for more prompt service. The floor shop can house a maximum of 12 mowers or tillers, excluding those being serviced. The customers arrive at the shop every 15 minutes on the average, and it takes a mechanic an average of 40 minutes to complete each job. Both the interarrival and the service times are exponential. Determine the following:

(a) Average number of idle mechanics.

(b) Amount of business lost to competition per 8-hour day because of the limited capacity of the shop.

(c) Probability that the next arriving customer will be serviced by the shop.

(d) Probability that at least one of the mechanics will be idle.

(e) Average number of tillers or mowers awaiting service.

(f) A measure of the overall productivity of the shop.

18-86. At U of A, newly enrolled freshmen students are notorious for wanting to drive their cars to class (even though most of them are required to live on campus and can conveniently make use of the university's free transit system). During the first couple of weeks of the fall semester, traffic havoc prevails on campus as first-year students try desperately to find parking spaces. With unusual dedication, the students wait patiently in the lanes of the parking lot for someone to leave so they can park their cars. Let us consider a specific scenario: The parking lot has 30 parking spaces but can also accommodate 10 more cars in the lanes. These additional 10 cars cannot park in the lanes permanently and must await the availability of one of the 30 parking spaces. Freshman students arrive at the parking lot according to a Poisson distribution, with a mean of 20 cars per hour. The parking time per car averages about 60 minutes but actually follows an exponential distribution.

*(a) What is the percentage of freshmen who are turned away because they cannot enter the lot?

*(b) What is the probability that an arriving car will wait in the lanes?

(c) What is the probability that an arriving car will occupy the only remaining parking space on the lot?

*(d) Determine the average number of occupied parking spaces.

*(e) Determine the average number of spaces that are occupied in the lanes.

(f) Determine the number of freshmen who will not make it to class during an 8-hr period because the parking lot is totally full.

18-87. Verify the expression for ${p}_{0}$ for the $\left( {M/M/c}\right)  : \left( {{GD}/N/\infty }\right)$ model, given that $\frac{\rho }{c} \neq  1$ .

18-88. Prove the following equality for $\left( {M/M/c}\right)  : \left( {{GD}/N/\infty }\right)$ :

$$
{\lambda }_{\text{ eff }} = \mu \bar{c},
$$

where $\bar{c}$ is the number of busy servers.

18-89. Verify the expression for ${p}_{0}$ and ${L}_{q}$ for $\left( {M/M/c}\right)  : \left( {{GD}/N/\infty }\right)$ when $\frac{\rho }{c} = 1$ .

18-90. For $\left( {M/M/c}\right)  : \left( {{GD}/N/\infty }\right)$ with which $N = c$ , define ${\lambda }_{n}$ and ${\mu }_{n}$ in terms of the general model (Section 18.5), then show that the expression for ${p}_{n}$ is given as

$$
{p}_{n} = \frac{{\rho }^{n}}{n!}{p}_{0}, n = 1,2,\ldots , c
$$

where

$$
{p}_{0} = {\left( 1 + \mathop{\sum }\limits_{{n = 1}}^{c}\frac{{\rho }^{n}}{n!}\right) }^{-1}
$$

18-91. In Example 18.6-7, compute the following:

(a) The probability that the investor will sell out completely.

(b) The probability that the investor will own at least 20 securities.

(c) The probability that the investor will own between 20 and 30 securities, inclusive.

(d) The investor's net annual equity if only 20% of the securities depreciate by 30% a year, and the remaining 80% appreciate by 12% a year.

18-92. New drivers are required to pass written tests before they are given road driving test. These tests are usually administered in the city hall. Records at the City of Springdale show that the average number of written tests is 100 per 8-hr day. The average time needed to complete the test is about 30 minutes. However, the actual arrival of test takers and the time each spends on the test are totally random. Determine the following:

*(a) The average number of seats the test hall should provide.

*(b) The probability that the number of test takers will exceed the average number of seats provided in the test hall.

(c) The probability that no tests will be administered in any one day.

18-93. Demonstrate (by using excelPoissonQ.xls or TORA) that for small $\rho  = {.1}$ , the values of ${L}_{s},{L}_{q},{W}_{s},{W}_{q}$ , and ${p}_{n}$ for $c$ as small as 4 servers, the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model can be estimated reliably using the less cumbersome formulas of the $\left( {M/M/\infty }\right)  : \left( {{GD}/\infty /\infty }\right)$ model for $c$ as small as 4 servers.

18-94. Repeat Problem 18-93 for large $\rho  = 9$ , and show that the same conclusion holds except that the value of $c$ must be higher (at least 14). From the results of Problems 18-93 and 18-94, what general conclusion can be drawn regarding the use of $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ to estimate the results of the $\left( {M/M/c}\right)  : \left( {{GD}/\infty /\infty }\right)$ model?

18-95. In Example 18.6-8, do the following:

(a) Verify the values of ${\lambda }_{\text{ eff }}$ given in Figure 18.9.

*(b) Compute the expected number of idle repairpersons, given $R = 4$ .

(c) Compute the probability that all repairpersons are idle, given $R = 3$ .

*(d) Compute the probability that the majority (more than half) of repairpersons are idle, given $R = 3$ .

18-96. In Example 18.6-8, define and compute the productivity of the repairpersons for $R = 1,2,3$ , and 4 . Use this information in conjunction with the measure of machine productivity to decide on the number of repairpersons Toolco should hire.

18-97. In the computations in Figure 18.9, it may appear confusing that the average rate of machine breakdown in the shop, ${\lambda }_{\text{ eff }}$ , increases with the increase in $R$ . Explain why the increase in ${\lambda }_{\text{ eff }}$ should be expected.

*18-98. An operator attends five automatic machines. After each machine completes a batch run, the operator must reset it before a new batch is started. The time to complete a batch run is exponential with mean 45 minutes. The setup time is also exponential with mean 8 minutes.

(a) Determine the average number of machines that are awaiting setup or are being set up.

(b) Compute the probability that all machines are working.

(c) Determine the average time a machine is down.

18-99. Kleen All is a service company that performs a variety of odd jobs, such as yard work, tree pruning, and house painting. The company's four employees leave the office with the first assignment of the day. After completing an assignment, the employee calls the office requesting instruction for the next job to be performed. The time to complete an assignment is exponential, with a mean of 35 minutes. The travel time between jobs is also exponential, with a mean of 30 minutes.

(a) Determine the average number of employees who are traveling between jobs.

(b) Compute the probability that no employee is on the road.

*18-100. After a long wait, the Newborns were rewarded with quintuplets, two boys and three girls, thanks to the wonders of new medical advances. During the first 5 months, the babies' life consisted of two states: awake (and mostly crying) and asleep. According to the Newborns, the babies' "awake-asleep" activities never coincide. Instead, the whole affair is totally random. In fact, Mrs. Newborn, a statistician by profession, believes that the length of time each baby cries is exponential, with a mean of 30 minutes. The amount of sleep each baby gets also happens to be exponential, with a mean of 2 hrs. Determine the following:

(a) The average number of babies who are awake at any one time.

(b) The probability that all babies are asleep.

(c) The probability that the Newborns will not be happy because more babies are awake (and crying) than are asleep.

18-101. Verify the expression for ${p}_{n}$ for the $\left( {M/M/R}\right)  : \left( {{GD}/K/K}\right)$ model.

18-102. Show that the rate of breakdown in the shop can be computed from the formula

$$
{\lambda }_{\text{ eff }} = \mu \bar{R}
$$

where $\bar{R}$ is the average number of busy repairpersons.

18-103. Verify the following results for the special case of one repairperson $\left( {R = 1}\right)$ :

$$
{p}_{n} = \frac{K!{\rho }^{n}}{\left( {K - n}\right) !}{p}_{0}
$$

$$
{p}_{0} = {\left( 1 + \mathop{\sum }\limits_{{n = 1}}^{R}\frac{K!{\rho }^{n}}{\left( K - n\right) }\right) }^{-1}
$$

$$
{L}_{s} = K - \frac{\left( 1 - {p}_{0}\right) }{\rho }
$$

18-104. In Example 18.7-1, compute the percentage of time the facility is idle.

18-105. Solve Example 18.7-1, assuming that the service-time distribution is given as follows:

*(a) Uniform between 8 and 20 minutes.

(b) Normal with $\mu  = {10}$ minutes and $\sigma  = 3$ minutes.

(c) Discrete with values equal to 4,8, and 12 minutes and probabilities .1, .6, and .3, respectively.

18-106. Layson Roofing Inc. installs shingle roofs on new and old homes in Arkansas. Prospective customers request the service randomly at the rate of 6 jobs per 30-day month and are placed on a waiting list to be processed on a FCFS basis. Homes sizes vary, but it is fairly reasonable to assume that the roof areas are uniformly distributed between 120 and 360 squares. The work crew can usually complete 60 squares a day. Determine the following:

(a) Layson's average backlog of roofing jobs.

(b) The average time a customer waits until a roofing job is completed.

(c) If the work crew is increased to the point where they can complete 100 squares a day, how will this affect the average time until a job is completed?

*18-107. Optica makes prescription glasses according to orders received from customers. Each worker is specialized in certain types of glasses. The company has been experiencing unusual delays in the processing of bifocal and trifocal prescriptions. The worker in charge receives 30 orders per 8-hr day. The time to complete a prescription is normally distributed, with a mean of 12 minutes and a standard deviation of 3 minutes. After spending between 2 and 4 minutes, uniformly distributed, to inspect the glasses, the worker can start on a new prescription. Determine the following:

(a) The percentage of time the worker is idle.

(b) The average backlog of bifocal and trifocal prescriptions in Optica.

(c) The average time until a prescription is filled.

18-108. A product arrives according to a Poisson distribution at the rate of one every 45 minutes. The product requires two tandem operations attended by one worker. The first operation uses a semiautomatic machine that completes its cycle in exactly 28 minutes. The second operation makes adjustments and minor changes, and its time depends on the condition of the product when it leaves operation 1. Specifically, the time of operation 2 is uniform between 3 and 6 minutes. Because each operation requires the complete attention of the worker, a new item cannot be loaded on the semiautomatic machine until the current item has cleared operation 2.

(a) Determine the number of items awaiting processing on the semiautomatic machine.

(b) What is the percentage of time the worker will be idle?

(c) How much time is needed, on the average, for an arriving item to clear operation 2?

18-109. $\left( {M/D/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ . Show that for the case where the service time is constant, the P-K formula reduces to

$$
{L}_{s} = \rho  + \frac{{\rho }^{2}}{2\left( {1 - \rho }\right) }
$$

where $\mu  = \frac{1}{E\{ t\} }$ and $\rho  = \frac{\lambda }{\mu } = {\lambda E}\{ t\}$ .

18-110. $\left( {M/{E}_{m}/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ . Given that the service time is Erlang with parameters $m$ and $\mu$ (i.e., $E\{ t\}  = \frac{m}{\mu }$ and $\operatorname{var}\{ t\}  = \frac{m}{{\mu }^{2}}$ ), show that the P-K formula reduces to

$$
{L}_{s} = {m\rho } + \frac{m\left( {1 + m}\right) {\rho }^{2}}{2\left( {1 - {m\rho }}\right) }
$$

18-111. Show that the P-K formula reduces to ${L}_{s}$ of the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ when the service time is exponential with a mean of $\frac{1}{\mu }$ time units.

18-112. In a service facility with $c$ parallel servers, suppose that customers arrive according to a Poisson distribution, with a mean rate of $\lambda$ . Arriving customers are assigned to servers (busy or free) on a strict rotational basis.

(a) Determine the probability distribution of the interarrival time.

(b) Suppose in part (a) that arriving customers are assigned randomly to the $c$ servers with probabilities ${\alpha }_{i},{\alpha }_{i} \geq  0, i = 1,2,\ldots , c$ , and ${\alpha }_{1} + {\alpha }_{2} + \cdots  + {\alpha }_{c} = 1$ . Determine the probability distribution of the interarrival time.

18-113. In Example 18.9-1, do the following:

(a) Verify the values of ${\mu }_{2},{\mu }_{3}$ , and ${\mu }_{4}$ given in the example.

(b) Suppose that the penalty of $\$ {48}$ per job per day is levied only on jobs that are not "in progress" at the end of the day. Which copier yields the lowest total cost per day?

*18-114. Metalco is in the process of hiring a repairperson for a 10-machine shop. Two candidates are under consideration. The first candidate can carry out repairs at the rate of 5 machines per hour and earns \$15 an hour. The second candidate, being more skilled, receives \$20 an hour and can repair 8 machines per hour. Metalco estimates that each broken machine will incur a cost of \$50 an hour because of lost production. Assuming that machines break down according to a Poisson distribution with a mean of 3 per hour and that repair time is exponential, which repairperson should be hired?

18-115. BB&K Groceries is opening a new store boasting "state-of-the-art" check-out scanners. Mr. Bih, one of the owners of B&K, has limited the choices to two scanners: scanner $A$ can process 15 items a minute, and the better-quality scanner $B$ can scan 20 items a minute. The daily (10 hours) cost of operating and maintaining the scanners are \$30 and \$50 for models $A$ and $B$ , respectively. Customers who finish shopping arrive at the cashier according to a Poisson distribution at the rate of 10 customers per hour. Each customer's cart carries between 25 and 35 items, uniformly distributed. Mr. Bih estimates the average cost per waiting customer per minute to be about 20 cents. Which scanner should B&K acquire? (Hint: The service time per customer is not exponential. It is uniformly distributed.)

18-116. H&I Industry produces a special machine with different production rates (pieces per hour) to meet customer specifications. A shop owner is considering buying one of these machines and wants to decide on the most economical speed (in pieces per hour) to be ordered. From past experience, the owner estimates that orders from customers arrive at the shop according to a Poisson distribution at the rate of three orders per hour. Each order averages about 500 pieces. Contracts between the owner and the customers specify a penalty of \$100 per late order per hour.

(a) Assuming that the actual production time per order is exponential, develop a general cost model as a function of the production rate, $\mu$ .

*(b) From the cost model in (a), determine an expression for the optimal production rate.

*(c) Using the data given in the problem, determine the optimal production rate the owner should request from H&I.

18-117. Jobs arrive at a machine shop according to a Poisson distribution at the rate of 80 jobs per week. An automatic machine represents the bottleneck in the shop. It is estimated that a unit increase in the production rate of the machine will cost \$250 per week. Delayed jobs normally result in lost business, which is estimated to be \$500 per job per week. Determine the optimum production rate for the automatic machine.

18-118. Pizza Unlimited sells two franchised restaurant models. Model $A$ has a capacity of 20 groups of customers, and model B can seat 30 groups. The monthly cost of operating model $A$ is \$12,000 and that of model $B$ is \$16,000. An investor wants to set up a buffet-style pizza restaurant and estimates that groups of customers, each occupying one table, arrive according to a Poisson distribution at a rate of 25 groups per hour. If all the tables are occupied, customers will go elsewhere. Model $A$ will serve 26 groups per hour, and model $B$ will serve 29 groups per hour. Because of the variation in group sizes and in the types of orders, the service time is exponential. The investor estimates that the average cost of lost business per customer group per hour is \$15. A delay in serving waiting customers is estimated to cost an average of \$10 per customer group per hour.

(a) Develop an appropriate cost mode.

(b) Assuming that the restaurant will be open for business 10 hrs a day, which model would you recommend for the investor?

18-119. Suppose in Problem 18-118 that the investor can choose any desired restaurant capacity based on a specific marginal cost for each additional capacity unit requested. Derive the associated general cost model, and define all its components and terms.

18-120. Second Time Around sells popular used items on consignment. Its operation can be viewed as an inventory problem in which the stock is replenished and depleted randomly according to Poisson distributions with rates $\lambda$ and $\mu$ items per day. Every time unit the item is out of stock, Second Time loses $\$ {C}_{1}$ because of lost opportunities, and every time unit an item is held in stock, a holding cost $\$ {C}_{2}$ is incurred.

(a) Develop an expression for the expected total cost per unit time.

(b) Determine the optimal value of $\rho  = \frac{\lambda }{\mu }$ . What condition must be imposed on the relative values of ${C}_{1}$ and ${C}_{2}$ in order for the solution to be consistent with the assumptions of the $\left( {M/M/1}\right)  : \left( {{GD}/\infty /\infty }\right)$ model?

18-121. Solve Example 18.9-2, assuming that ${C}_{1} = \$ {25}$ and ${C}_{2} = \$ {50}$ .

*18-122. Tasco Oil owns a pipeline booster unit that operates continuously. The time between breakdowns for each booster is exponential with a mean of ${20}\mathrm{{hrs}}$ . The repair time is exponential with mean 3 hrs. In a particular station, two repairpersons attend 10 boosters. The hourly wage for each repairperson is \$18. Pipeline losses are estimated to be \$30 per broken booster per hour. Tasco is studying the possibility of hiring an additional repairperson.

(a) Will there be any cost savings in hiring a third repairperson?

(b) What is the schedule loss in dollars per breakdown when the number of repairper-sons on duty is two? Three?

18-123. A company leases a wide-area telecommunications service (WATS) telephone line for \$2000 a month. The office is open 200 working hours per month. At all other times, the WATS line service is used for other purposes and is not available for company business. Access to the WATS line during business hours is extended to 100 salespersons, each of whom may need the line at any time but averages twice per 8-hr day with exponential time between calls. A salesperson will always wait for the WATS line if it is busy at an estimated inconvenience of 1 cent per minute of waiting. It is assumed that no additional needs for calls will arise while the salesperson waits for a given call. The normal cost of calls (not using the WATS line) averages about 50 cents per minute, and the duration of each call is exponential, with a mean of 6 mins. The company is considering leasing (at the same price) a second WATS line to improve service.

(a) Is the single WATS line saving the company money over a no-WATS system? How much is the company gaining or losing per month over the no-WATS system?

(b) Should the company lease a second WATS line? How much would it gain or lose over the single WATS case by leasing an additional line?

*18-124. A machine shop includes 20 machines and 3 repairpersons. A working machine breakdown down randomly according to a Poisson distribution. The repair time per machine is exponential with a mean of 6 minutes. A queuing analysis of the situation shows an average of 57.8 calls for repair per 8-hr day for the entire shop. Suppose that the production rate per machine is 25 units per hour and that each produced unit generates \$2 in revenue. Further, assume that a repairperson is paid at the rate of \$20 an hour. Compare the cost of hiring the repairpersons against the cost of lost revenue when machines are broken.

18-125. The necessary conditions for ${ETC}\left( c\right)$ (defined earlier) to assume a minimum value at $c = {c}^{ * }$ are

$$
\operatorname{ETC}\left( {{c}^{ * } - 1}\right)  \geq  \operatorname{ETC}\left( {c}^{ * }\right) \text{ and }\operatorname{ETC}\left( {{c}^{ * } + 1}\right)  \geq  \operatorname{ETC}\left( {c}^{ * }\right)
$$

Show that these conditions reduce to

$$
{L}_{s}\left( {c}^{ * }\right)  - {L}_{s}\left( {{c}^{ * } + 1}\right)  \leq  \frac{{C}_{1}}{{C}_{2}} \leq  {L}_{s}\left( {{c}^{ * } - 1}\right)  - {L}_{s}\left( {c}^{ * }\right)
$$

Apply the result to Example 18.9-2, and show that it yields ${c}^{ * } = 4$ .

*18-126. A shop uses 10 identical machines. Each machine breaks down once every 7 hrs on the average. It takes half an hour on the average to repair a broken machine. Both the breakdown and repair processes follow the Poisson distribution. Determine the following:

(a) The number of repairpersons needed such that the average number of broken machines is less than 1.

(b) The number of repairpersons needed so that the expected delay time until repair is started is less than 10 minutes.

18-127. In the cost model in Section 18.9.1, it is generally difficult to estimate the cost parameter ${C}_{2}$ (cost of waiting). As a result, it may be helpful to compute the cost ${C}_{2}$ implied by the aspiration levels. Using the aspiration level model to determine ${c}^{ * }$ , we can then estimate the implied ${C}_{2}$ by using the following inequality:

$$
{L}_{s}\left( {c}^{ * }\right)  - {L}_{s}\left( {{c}^{ * } + 1}\right)  \leq  \frac{{C}_{1}}{{C}_{2}} \leq  {L}_{s}\left( {{c}^{ * } - 1}\right)  - {L}_{s}\left( {c}^{ * }\right)
$$

((See Problem 18-125, for the derivation.) Apply the procedure to the problem in Example 18.9-2, assuming ${c}^{ * } = 3$ and ${C}_{1} = \$ {15.00}$ .

This page intentionally left blank