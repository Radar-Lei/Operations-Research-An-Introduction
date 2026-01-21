## CHAPTER 1 What Is Operations Research? ^chapter

```markmap
---
markmap:
  height: 643
---
# [[#^chapter|CHAPTER 1: What Is Operations Research (OR)?]]

## [[#^wwii|Origins & Purpose]]
### [[#^wwii|Started in WWII Britain: scientific allocation of war resources]]
### [[#^postwar|Post-war: adapted to improve civilian efficiency & productivity]]
### [[#^scienceart|OR as a decision-making discipline: science + art]]

## [[#^terminology|Core Terminology]]
### [[#^terminology|Mathematical modeling]]
### [[#^terminology|Decision variables & alternatives]]
### [[#^constraintscomponent|Constraints]]
### [[#^objectivecriterion|Objective (maximize/minimize)]]
### [[#^definitions|Feasible vs optimal solutions]]
### [[#^algorithms|Iterative/algorithmic computation]]

## [[#^introduction|1.1 Introduction: Key Messages]]
### [[#^problemdefinition|Correct problem definition is hardest and most important]]
### [[#^unquantifiable|Models are essential, but unquantifiable factors (human behavior) matter]]
### [[#^learningcases|Learning via solved examples, problems, and case analyses]]

## [[#^models|1.2 Operations Research Models]]

### [[#^modelcomponents|OR model components]]
#### [[#^alternatives|Alternatives (choices)]]
#### [[#^objectivecriterion|Objective criterion (what “best” means)]]
#### [[#^constraintscomponent|Constraints (restrictions)]]

### [[#^airtickets|Example A: Airline tickets (finite alternatives)]]
#### [[#^airtickets|Setup]]
#### [[#^airtickets|Costs]]
##### [[#^airtickets|Regular roundtrip]]
##### [[#^airtickets|Weekend-spanning roundtrip]]
##### [[#^airtickets|One-way]]
#### [[#^airtickets|Alternatives & costs (compare totals)]]
##### [[#^airtickets|Alt 1: 5 regular roundtrips]]
##### [[#^airtickets|Alt 2: mix of one-ways + weekend trips]]
##### [[#^airtickets|Alt 3: all weekend-spanning roundtrips]]

### [[#^gardenfencing|Example B: Garden fencing (continuous alternatives)]]
#### [[#^gardenfencing|Fence length]]
#### [[#^definevariables|Variables]]
#### [[#^perimeterconstraint|Constraint (perimeter)]]
#### [[#^maximizearea|Objective]]
#### [[#^qwer|Eliminate variable]]
##### $w = \frac{L}{2} - h$
##### $z(h) = \left(\frac{L}{2}-h\right)h = \frac{Lh}{2} - h^2$
#### [[#^bestsolution|Best solution (via calculus)]]

### [[#^generaltemplate|General model template]]
#### [[#^generaltemplate|Maximize / minimize objective function]]
#### [[#^generaltemplate|subject to constraints]]

### [[#^definitions|Definitions]]
#### [[#^definitions|Feasible: satisfies all constraints]]
#### [[#^definitions|Optimal: feasible + best objective value]]

### [[#^modelcompleteness|Model completeness matters]]
#### [[#^modelcompleteness|“Optimal” is only optimal relative to modeled alternatives & assumptions]]
#### [[#^modelcompleteness|Missing key alternatives can make solutions suboptimal in reality]]

## [[#^solving|1.3 Solving the OR Model]]
### [[#^nosinglemethod|No single universal method; depends on model type/complexity]]
### [[#^techniques|Major technique families]]
#### Linear programming (linear objective/constraints)
#### Integer programming (integer variables)
#### Dynamic programming (decomposable subproblems)
#### Network programming (graph/network structure)
#### Nonlinear programming (nonlinear functions)
### [[#^algorithms|Algorithms & iteration]]
#### [[#^algorithms|Solutions often not closed-form]]
#### [[#^algorithms|Use iterative algorithms; computers handle large/tedious computations]]
### [[#^heuristics|When optimization is too hard]]
#### [[#^heuristics|Use heuristics/metaheuristics for good (not necessarily optimal) solutions]]

## [[#^queuing|1.4 Queuing and Simulation Models]]
### [[#^waitinglines|Focus: waiting lines (performance measurement, not optimization)]]
#### Average waiting time in queue
#### Average service waiting time
#### Utilization of service facilities
### [[#^queuingsimulation|Queuing vs simulation]]
#### Queuing: mathematical/probabilistic, assumption-limited
#### Simulation: imitates system behavior; flexible for many scenarios
### [[#^simulationdrawback|Simulation drawback]]
#### [[#^simulationdrawback|Costly to build; slow to run even on fast computers]]

## [[#^ada|Aha! Moment: Ada Lovelace & Algorithms]]
### [[#^ada|“Algorithm” roots linked to Al-Khwarizmi (origin of the term)]]
### [[#^ada|Ada Lovelace wrote a pioneering algorithm (Bernoulli numbers)]]
### [[#^ada|Babbage’s Engines (Difference/Analytical) anticipated modern components]]
### [[#^ada|Legacy: Ada language; Ada Lovelace Day (STEM celebration)]]

## [[#^artofmodeling|1.5 Art of Modeling (Abstraction)]]
### [[#^approximations|Exact models are rare; most are approximations]]
### [[#^approximations|Model development as abstraction layers]]
#### Real world → assumed real world (dominant variables)
#### Assumed real world → mathematical model (amenable functions)
### [[#^tyko|Tyko Manufacturing example]]
#### Many interacting variables across departments
#### Simplify to dominant parameters: production rate & consumption rate
#### Build inventory cost model (excess vs shortage) → minimize total cost

## [[#^morethanmath|1.6 More Than Just Mathematics (Human Factors)]]
### [[#^psychology|Start with simplest approaches; psychology often decisive]]
### [[#^psychology|Illustrations]]
#### [[#^orion|UPS ORION: “Beat the Computer” framing improved adoption]]
#### [[#^houston|Houston airport: longer walk reduced baggage complaints]]
#### [[#^britishairport|British airport: cultural norms broke a mathematically sound queue policy]]
#### [[#^steelmill|Steel mill: simple charts revealed shift behavior; schedule leveling fixed it]]
#### [[#^elevator|Elevator: mirrors reduced perceived waiting]]
#### [[#^trucks|Shared trucks: visibility/communication solved “lack of trucks” complaint]]
### [[#^conclusions|Four conclusions]]
#### [[#^differentideas|Use different ideas; include social science/psychology]]
#### [[#^birdseye|Take a bird’s-eye view to find nontechnical root causes]]
#### [[#^nobias|Don’t bias toward a favorite tool (e.g., LP) without justification]]
#### [[#^peopleculture|Solutions must fit people/culture, not just technology]]

## [[#^phases|1.7 Phases of an OR Study]]
### [[#^teamwork|Teamwork: analysts + client collaborate]]
### [[#^scienceart|OR as science (methods) + art (creativity, judgment, communication)]]
### [[#^fivephases|Five phases]]
#### [[#^defineproblem|1) Define the problem (alternatives, objective, limitations)]]
#### [[#^constructmodel|2) Construct the model (relationships; may simplify)]]
#### [[#^solvemodel|3) Solve the model (algorithms)]]
##### [[#^sensitivity|Sensitivity analysis: robustness to parameter changes]]
#### [[#^validatemodel|4) Validate the model (sanity checks + compare to historical data)]]
#### [[#^implementsolution|5) Implement the solution (operational instructions & adoption)]]

## [[#^aboutbook|1.8 About This Book]]
### [[#^teachingmodels|Teaching models ≠ teaching modeling (emphasis on realistic cases)]]
### [[#^teachingmodels|Computation & software tools]]
#### [[#^teachingmodels|Commercial packages (Excel/Solver, AMPL) + tutorial tools (e.g., TORA)]]
### [[#^practicalcases|Learning by practical cases]]
#### [[#^practicalcases|End-of-chapter case analyses + many real-world cases (including online)]]
#### [[#^practicalcases|Interfaces (INFORMS) as a rich OR application source]]

```


### 1.1 INTRODUCTION ^introduction

The first formal activities of Operations Research (OR) were initiated in England during World War II, when a team of British scientists set out to assess the best utilization of war materiel based on scientific principles rather than on ad hoc rules. ^wwii

After the war, the ideas advanced in military operations were adapted to improve efficiency and productivity in the civilian sector. ^postwar

This chapter introduces the basic terminology of OR, including mathematical modeling, feasible solutions, optimization, and iterative algorithmic computations. ^terminology

It stresses that defining the problem correctly is the most important (and most difficult) phase of practicing OR. ^problemdefinition

The chapter also emphasizes that, while mathematical modeling is a cornerstone of OR, unquantifiable factors (such as human behavior) must be accounted for in the final decision. ^unquantifiable

The book presents a variety of applications using solved examples and chapter problems. In particular, the book includes end-of-chapter fully developed case analyses. ^learningcases

### 1.2 OPERATIONS RESEARCH MODELS ^models

Consider the following tickets purchasing problem. A businessperson has a 5-week commitment traveling between Fayetteville (FYV) and Denver (DEN). Weekly departure from Fayetteville occurs on Mondays for return on Wednesdays. A regular roundtrip ticket costs \$400, but a 20% discount is granted if the roundtrip dates span a weekend. A one-way ticket in either direction costs 75% of the regular price. How should the tickets be bought for the 5-week period? ^airtickets

We can look at the situation as a decision-making problem whose solution requires answering three questions: ^modelcomponents

1. What are the decision alternatives?

2. Under what restrictions is the decision made?

3. What is an appropriate objective criterion for evaluating the alternatives?

Three plausible alternatives come to mind: ^alternatives

1. Buy five regular FYV-DEN-FYV for departure on Monday and return on Wednesday of the same week.

2. Buy one FYV-DEN, four DEN-FYV-DEN that span weekends, and one DEN-FYV.

3. Buy one FYV-DEN-FYV to cover Monday of the first week and Wednesday of the last week and four DEN-FYV-DEN to cover the remaining legs. All tickets in this alternative span at least one weekend.

The restriction on these options is that the businessperson should be able to leave FYV on Monday and return on Wednesday of the same week. ^constraintscomponent

An obvious objective criterion for evaluating the proposed alternatives is the price of the tickets. The alternative that yields the smallest cost is the best. Specifically, we have: ^objectivecriterion

Alternative 1 cost $= 5 \times  \$ {400} = \$ {2000}$

Alternative 2 cost $= {.75} \times  \$ {400} + 4 \times  \left( {{.8} \times  \$ {400}}\right)  + {.75} \times  \$ {400} = \$ {1880}$

Alternative 3 cost $= 5 \times  \left( {{.8} \times  \$ {400}}\right)  = \$ \mathbf{{1600}}$

Alternative 3 is the cheapest.

Though the preceding example illustrates the three main components of an OR model - alternatives, objective criterion, and constraints - situations differ in the details of how each component is developed, and how the resulting model is solved. To illustrate this point, consider the following garden problem: A home owner is in the process of starting a backyard vegetable garden. The garden must take on a rectangular shape to facilitate row irrigation. To keep critters out, the garden must be fenced. The owner has enough material to build a fence of length $L = {100}\mathrm{{ft}}$ . The goal is to fence the largest possible rectangular area. ^gardenfencing

In contrast with the tickets example, where the number of alternatives is finite, the number of alternatives in the present example is infinite; that is, the width and height of the rectangle can each assume (theoretically) infinity of values between 0 and $L$ . In this case, the width and the height are continuous variables. ^continuousalternatives

Because the variables of the problem are continuous, it is impossible to find the solution by exhaustive enumeration. However, we can sense the trend toward the best value of the garden area by fielding increasing values of width (and hence decreasing values of height). For example, for $L = {100}\mathrm{{ft}}$ , the combinations (width, height) $= ({10}$ , 40), (20, 30), (25, 25), (30, 20), and (40, 10) respectively yield (area) = (400, 600, 625, 600, and 400), which demonstrates, but not proves, that the largest area occurs when width $=$ height $= L/4 = {25}\mathrm{{ft}}$ . Clearly, this is no way to compute the optimum, particularly for situations with several decision variables. For this reason, it is important to express the problem mathematically in terms of its unknowns, in which case the best solution is found by applying appropriate solution methods.

To demonstrate how the garden problem is expressed mathematically in terms of its two unknowns, width and height, define ^definevariables

$$
w = \text{ width of the rectangle in feet }
$$

$$
h = \text{ height of the rectangle in feet }
$$

Based on these definitions, the restrictions of the situation can be expressed verbally as ^perimeterconstraint

1. Width of rectangle + Height of rectangle = Half the length of the garden fence

2. Width and height cannot be negative

These restrictions are translated algebraically as

1. $2\left( {w + h}\right)  = L$

2. $w \geq  0, h \geq  0$

The only remaining component now is the objective of the problem; namely, maximization of the area of the rectangle. Let $z$ be the area of the rectangle, then the complete model becomes ^maximizearea

$$
\text{ Maximize }z = {wh}
$$

subject to

$$
2\left( {w + h}\right)  = L
$$

$$
w, h \geq  0
$$

Actually, this model can be simplified further by eliminating one of the variables in the objective function using the constraint equation; that is, ^qwer

$$
w = \frac{L}{2} - h
$$

The result is

$$
z = {wh} = \left( {\frac{L}{2} - h}\right) h = \frac{Lh}{2} - {h}^{2}
$$

The maximization of $z$ is achieved by using differential calculus (Chapter 20), which yields the best solution as $h = \frac{L}{4} = {25}\mathrm{{ft}}$ . Back substitution in the constraint equation then yields $w = \frac{L}{4} = {25}\mathrm{{ft}}$ . Thus the solution calls for constructing a square-shaped garden. ^bestsolution

Based on the preceding two examples, the general OR model can be organized in the following general format: ^generaltemplate

Maximize or minimize Objective Function

subject to

Constraints

**A solution is feasible if it satisfies all the constraints. It is optimal if, in addition to being feasible, it yields the best (maximum or minimum) value of the objective function.** In the ticket purchasing problem, the problem considers three feasible alternatives, with the third alternative being optimal. In the garden problem, a feasible alternative must satisfy the condition $w + h = \frac{L}{2}$ , with $w$ and $h \geq  0$ , that is, nonnegative variables. This definition leads to an infinite number of feasible solutions and, unlike the ticket purchasing problem, which uses simple price comparisons, the optimum solution is determined using differential calculus. ^definitions

Though OR models are designed to optimize a specific objective criterion subject to a set of constraints, the quality of the resulting solution depends on the degree of completeness of the model in representing the real system. Take, for example, the ticket purchasing model. If all the dominant alternatives for purchasing the tickets are not identified, then the resulting solution is optimum only relative to the alternatives represented in the model. To be specific, if for some reason alternative 3 is left out of the model, the resulting "optimum" solution would call for purchasing the tickets for \$1880, which is a suboptimal solution. The conclusion is that "the" optimum solution of a model is best only for that model. If the model happens to represent the real system reasonably well, then its solution is optimum also for the real situation. ^modelcompleteness

### 1.3 SOLVING THE OR MODEL ^solving

In practice, OR does not offer a single general technique for solving all mathematical models. Instead, the type and complexity of the mathematical model dictate the nature of the solution method. For example, in Section 1.2 the solution of the tickets purchasing problem requires simple ranking of alternatives based on the total purchasing price, whereas the solution of the garden problem utilizes differential calculus to determine the maximum area. ^nosinglemethod

The most prominent OR technique is linear programming. It is designed for models with linear objective and constraint functions. Other techniques include integer programming (in which the variables assume integer values), dynamic programming (in which the original model can be decomposed into smaller more manageable subproblems), network programming (in which the problem can be modeled as a network), and nonlinear programming (in which functions of the model are nonlinear). These are only a few among many available OR tools. ^techniques

A peculiarity of most OR techniques is that solutions are not generally obtained in (formula-like) closed forms. Instead, they are determined by algorithms. An [[algorithm]] provides fixed computational rules that are applied repetitively to the problem, with each repetition (called iteration) attempting to move the solution closer to the optimum. Because the computations in each iteration are typically tedious and voluminous, it is imperative in practice to use the computer to carry out these algorithms. ^algorithms

Some mathematical models may be so complex that it becomes impossible to solve them by any of the available optimization algorithms. In such cases, it may be necessary to abandon the search for the optimal solution and simply seek a good solution using heuristics or metaheuristics, a collection of intelligent search rules of thumb that move the solution point advantageously toward the optimum. ^heuristics

### 1.4 QUEUING AND SIMULATION MODELS ^queuing

Queuing and simulation deal with the study of waiting lines. They are not optimization techniques; rather, they determine measures of performance of waiting lines, such as average waiting time in queue, average waiting time for service, and utilization of service facilities, among others. ^waitinglines

Queuing models utilize probability and stochastic models to analyze waiting lines, and simulation estimates the measures of performance by "imitating" the behavior of the real system. In a way, simulation may be regarded as the next best thing to observing a real system. The main difference between queuing and simulation is that queuing models are purely mathematical, and hence are subject to specific assumptions that limit their scope of application. Simulation, on the other hand, is flexible and can be used to analyze practically any queuing situation. ^queuingsimulation

---

## Aha! Moment: Ada Lovelace, the First-Ever Algorithm Programmer ^ada

Though the first conceptual development of an algorithm is attributed to the founder of algebra Muhammad Ibn-Musa Al-Khwarizmi (born c. 780 in Khuwarezm, Uzbekistan, died c. 850 in Baghdad, Iraq), ${}^{1}$ it was British Ada Lovelace (1815-1852) who developed the first computer algorithm. And when we speak of computers, we are referring to the mechanical Difference and Analytical Engines pioneered and designed by the famed British mathematician Charles Babbage (1791-1871).

Lovelace had a keen interest in mathematics. As a teenager, she visited the Babbage home and was fascinated by his invention and its potential uses in doing more than just arithmetic operations. Collaborating with Babbage, she translated into English an article that provided the design details of the Analytical Engine. The article was based on lectures Babbage presented in Italy. In the translated article, Lovelace appended her own notes (which turned out to be longer than the original article and included some corrections of Babbage's design ideas). One of her notes detailed the first-ever algorithm, that of computing Bernoulli numbers on the yet-to-be-completed Analytical Engine. She even predicted that the Babbage machine had the potential to manipulate symbols (and not just numbers) and to create complex music scores. ${}^{2}$

Ada Lovelace died at the young age of 37. In her honor, the computer language Ada, developed for the United States Department of Defense, was named after her. The annual mid-October Ada Lovelace Day is an international celebration of women in science, technology, engineering, mathematics (STEM). And those of us who have visited St. James Square in London may recall the blue plaque that read "Ada Countess of Lovelace (1815-1852) Pioneer of Computing."

${}^{1}$ According to Dictionary.com, the word algorithm originates "from Medieval Latin algorismus, a mangled transliteration of Arabic al-Khwarizmi."

${}^{2}$ Lack of funding, among other factors, prevented Babbage from building fully working machines during his lifetime. It was only in 1991 that the London Science Museum built a complete Difference Engine No. 2 using the same materials and technology available to Babbage, thus vindicating his design ideas. There is currently an ongoing long-term effort to construct a fully working Analytical Engine funded entirely by public contributions. It is impressive that modern-day computers are based on the same principal components (memory, CPU, input, and output) advanced by Babbage 100 years earlier.

---

The use of simulation is not without drawbacks. The process of developing simulation models is costly in both time and resources. Moreover, the execution of simulation models, even on the fastest computer, is usually slow. ^simulationdrawback

### 1.5 ART OF MODELING ^artofmodeling

The illustrative models developed in Section 1.2 are exact representations of real situations. This is a rare occurrence in OR, as the majority of applications usually involve (varying degrees of) approximations. Figure 1.1 depicts the levels of abstraction that characterize the development of an OR model. We abstract the assumed real world from the real situation by concentrating on the dominant variables that control the behavior of the real system. The model expresses in an amenable manner the mathematical functions that represent the behavior of the assumed real world. ^approximations

To illustrate levels of abstraction in modeling, consider the Tyko Manufacturing Company, where a variety of plastic containers are produced. When a production order is issued to the production department, necessary raw materials are acquired from the company's stocks or purchased from outside sources. Once a production batch is completed, the sales department takes charge of distributing the product to retailers. ^tyko

A viable question in the analysis of Tyko's situation is the determination of the size of a production batch. How can this situation be represented by a model?

Looking at the overall system, a number of variables can bear directly on the level of production, including the following (partial) list categorized by department:

1. Production Department: Production capacity expressed in terms of available machine and labor hours, in-process inventory, and quality control standards.

2. Materials Department: Available stock of raw materials, delivery schedules from outside sources, and storage limitations.

3. Sales Department: Sales forecast, capacity of distribution facilities, effectiveness of the advertising campaign, and effect of competition.

FIGURE 1.1

Levels of abstraction in model development

![bo_d56m41n7aajc73800n1g_5_348_1687_1169_477_0.jpg](bo_d56m41n7aajc73800n1g_5_348_1687_1169_477_0.jpg)

Each of these variables affects the level of production at Tyko. Trying to establish explicit functional relationships between them and the level of production is a difficult task indeed.

A first level of abstraction requires defining the boundaries of the assumed real world. With some reflection, we can approximate the real system by two dominant parameters:

1. Production rate.

2. Consumption rate.

The production rate is determined using data such as production capacity, quality control standards, and availability of raw materials. The consumption rate is determined from the sales data. In essence, simplification from the real world to the assumed real world is achieved by "lumping" several real-world parameters into a single assumed-real-world parameter.

It is easier now to abstract a model from the assumed real world. From the production and consumption rates, measures of excess or shortage inventory can be established. The abstracted model may then be constructed to balance the conflicting costs of excess and shortage inventory-that is, to minimize the total cost of inventory.

### 1.6 MORE THAN JUST MATHEMATICS ^morethanmath

Because of the mathematical nature of OR models, one tends to think that an OR study is always rooted in mathematical analysis. Though mathematical modeling is a cornerstone of OR, simpler approaches should be explored first. In some cases, a "commonsense" solution may be reached through simple observations. Indeed, since the human element invariably affects most decision problems, a study of the psychology of people may be key to solving the problem. Six illustrations are presented here to demonstrate the validity of this argument. ^psychology

1. The stakes were high in 2004 when United Parcel Service (UPS) unrolled its ORION software (based on the sophisticated Traveling Salesman Algorithm-see Chapter 11) to provide its drivers with tailored daily delivery itineraries. The software generally proposed shorter routes than those presently taken by the drivers, with potential savings of millions of dollars a year. For their part, the drivers resented the notion that a machine could "best" them, given their long years of experience on the job. Faced with this human dilemma, ORION developers resolved the issue simply placing a visible banner on the itinerary sheets that read "Beat the Computer." At the same time, they kept ORION-generated routes intact. The drivers took the challenge to heart, with some actually beating the computer suggested route. ORION was no longer putting them down. Instead, they regarded the software as complementing their intuition and experience. ${}^{3}$ ^orion

2. Travelers arriving at the Intercontinental Airport in Houston, Texas, complained about the long wait for their baggage. Authorities increased the number of baggage handlers in hope of alleviating the problem, but the complaints persisted. In the end, the decision was made to simply move arrival gates farther away from baggage claim, forcing the passengers to walk longer before reaching the baggage area. The complaints disappeared because the extra walking allowed ample time for the luggage to be delivered to the carousel. ${}^{4}$ ^houston

---

${}^{3}$ http://www.fastcompany.com/3004319/brown-down-ups-drivers-vs-ups-algorithm.See also "At UPS, the Algorithm Is the Driver," Wall Street Journal, February 16, 2015.

---

3. In a study of the check-in counters at a large British airport, a U.S.-Canadian consulting team used queuing theory to investigate and analyze the situation. Part of the solution recommended the use of well-placed signs urging passengers within 20 mins of departure time to advance to the head of the queue and request priority service. The solution was not successful because the passengers, being mostly British, were "conditioned to very strict queuing behavior." Hence they were reluctant to move ahead of others waiting in the queue. ${}^{5}$ ^britishairport

4. In a steel mill in India, ingots were first produced from iron ore and then used in the manufacture of steel bars and beams. The manager noticed a long delay between the ingots production and their transfer to the next manufacturing phase (where end products were produced). Ideally, to reduce reheating cost, manufacturing should start soon after the ingots leave the furnaces. Initially, the problem could be perceived as a line-balancing situation, which could be resolved either by reducing the output of ingots or by increasing the capacity of manufacturing. Instead, the OR team used simple charts to summarize the output of the furnaces during the three shifts of the day. They discovered that during the third shift starting at 11:00 P.M., most of the ingots were produced between 2:00 and 7:00 A.M. Investigation revealed that third-shift operators preferred to get long periods of rest at the start of the shift and then make up for lost production during morning hours. Clearly, the third-shift operators have hours to spare to meet their quota. The problem was solved by "leveling out" both the number of operators and the production schedule of ingots throughout the shift. ^steelmill

5. In response to complaints of slow elevator service in a large office building, the OR team initially perceived the situation as a waiting-line problem that might require the use of mathematical queuing analysis or simulation. After studying the behavior of the people voicing the complaint, the psychologist on the team suggested installing full-length mirrors at the entrance to the elevators. The complaints disappeared, as people were kept occupied watching themselves and others while waiting for the elevator. ^elevator

6. A number of departments in a production facility share the use of three trucks to transport material. Requests initiated by a department are filled on a first-come-first-serve basis. Nevertheless, the departments complained of long wait for service, and demanded adding a fourth truck to the pool. Ensuing simple tallying of the usage of the trucks showed modest daily utilization, obviating a fourth truck. Further investigations revealed that the trucks were parked in an obscure parking lot out of the line of vision for the departments. A requesting supervisor, lacking visual sighting of the trucks, assumed that no trucks were available and hence did not initiate a request. The problem was solved simply by installing two-way radio communication between the truck lot and each department. ${}^{6}$ ^trucks

---

${}^{4}$ Stone, A.,"Why Waiting Is Torture," The New York Times, August 18,2012.

${}^{5}$ Lee, A., Applied Queuing Theory, St. Martin’s Press, New York,1966.

---

Four conclusions can be drawn from these illustrations: ^conclusions

1. The OR team should explore the possibility of using "different" ideas to resolve the situation. The (common-sense) solutions proposed for the UPS problem (using Beat the Computer banner to engage drivers), the Houston airport (moving arrival gates away from the baggage claim area), and the elevator problem (installing mirrors) are rooted in human psychology rather than in mathematical modeling. This is the reason OR teams may generally seek the expertise of individuals trained in social science and psychology, a point that was recognized and implemented by the first OR team in Britain during World War II. ^differentideas

2. Before jumping to the use of sophisticated mathematical modeling, a bird's eye view of the situation should be adopted to uncover possible nontechnical reasons that led to the problem in the first place. In the steel mill situation, this was achieved by using only simple charting of the ingots production to discover the imbalance in the third-shift operation. A similar simple observation in the case with the transport trucks situation also led to a simple solution of the problem. ^birdseye

3. An OR study should not start with a bias toward using a specific mathematical tool before the use of the tool is justified. For example, because linear programming (Chapter 2 and beyond) is a successful technique, there is a tendency to use it as the modeling tool of choice. Such an approach may lead to a mathematical model that is far removed from the real situation. It is thus imperative to analyze available data, using the simplest possible technique, to understand the essence of the problem. Once the problem is defined, a decision can be made regarding the most appropriate tool for the solution. In the steel mill problem, simple charting of the ingots production was all that was needed to clarify the situation. ^nobias

4. Solutions are rooted in people and not in technology. Any solution that does not take human behavior into consideration is apt to fail. Even though the solution of the British airport problem may have been mathematically sound, the fact that the consulting team was unaware of the cultural differences between the United States and Britain resulted in an unimplementable recommendation (Americans and Canadians tend to be less formal). The same viewpoint can, in a way, be expressed in the UPS case. ^peopleculture

### 1.7 PHASES OF AN OR STUDY ^phases

OR studies are rooted in teamwork, where the OR analysts and the client work side by side. The OR analysts' expertise in modeling is complemented by the experience and cooperation of the client for whom the study is being carried out. ^teamwork

---

${}^{6}$ G. P. Cosmetatos,"The Value of Queuing Theory-A Case Study," Interfaces, Vol. 9, No. 3, pp. 47-51,1979.

---

As a decision-making tool, OR is both a science and an art: It is a science by virtue of the mathematical techniques it embodies, and an art because the success of the phases leading to the solution of the mathematical model depends largely on the creativity and experience of the OR team. Willemain (1994) advises that "effective [OR] practice requires more than analytical competence: It also requires, among other attributes, technical judgment (e.g., when and how to use a given technique) and skills in communication and organizational survival." ^scienceart

It is difficult to prescribe specific courses of action (similar to those dictated by the precise theory of most mathematical models) for these intangible factors. We can, however, offer general guidelines for the implementation of OR in practice.

The principal phases for implementing OR in practice include the following: ^fivephases

1. Definition of the problem.

2. Construction of the model.

3. Solution of the model.

4. Validation of the model.

5. Implementation of the solution.

Phase 3, dealing with model solution, is the best defined and generally the easiest to implement in an OR study, because it deals mostly with well-defined mathematical models. Implementation of the remaining phases is more an art than a theory.

Problem definition involves delineating the scope of the problem under investigation. This function should be carried out by the entire OR team. The aim is to identify three principal elements of the decision problem: (1) description of the decision alternatives, (2) determination of the objective of the study, and (3) specification of the limitations under which the modeled system operates. ^defineproblem

Model construction entails an attempt to translate the problem definition into mathematical relationships. If the resulting model fits one of the standard mathematical models, such as linear programming, we can usually reach a solution by using available algorithms. Alternatively, if the mathematical relationships are too complex to allow the determination of an analytic solution, the OR team may opt to simplify the model and use a heuristic approach, or the team may consider the use of simulation, if appropriate. In some cases, mathematical, simulation, and heuristic models may be combined to solve the decision problem, as some of the end-of-chapter case analyses demonstrate. ^constructmodel

Model solution is by far the simplest of all OR phases because it entails the use of well-defined optimization algorithms. ^solvemodel

An important aspect of the model solution phase is [[sensitivity analysis]]. It deals with obtaining additional information about the behavior of the optimum solution when the model undergoes some parameter changes. Sensitivity analysis is particularly needed when the parameters of the model cannot be estimated accurately. In these cases, it is important to study the behavior of the optimum solution in the neighborhood of the parameters estimates. ^sensitivity

Model validity checks whether or not the proposed model does what it purports to do-that is, does it adequately predict the behavior of the system under study? Initially, the OR team should be convinced that the model's output does not include "surprises." In other words, does the solution make sense? Are the results intuitively acceptable? On the formal side, a common method for validating a model is to compare its output with historical output data. The model is valid if, under similar input conditions, it reasonably duplicates past performance. Generally, however, there is no guarantee that future performance will continue to duplicate past behavior. Also, because the model is usually based on examination of past data, the proposed comparison should usually be favorable. If the proposed model represents a new (non-existing) system, no historical data would be available. In some situations, simulation may be used as an independent tool for validating the output of the mathematical model. ^validatemodel

Implementation of the solution of a validated model involves the translation of the results into understandable operating instructions to be issued to the people who will administer the recommended system. The burden of this task lies primarily with the OR team. ^implementsolution

### 1.8 ABOUT THIS BOOK ^aboutbook

Morris (1967) states "the teaching of models is not equivalent to the teaching of modeling." I have taken note of this important statement during the preparation of this edition, making every effort to introduce the art of modeling in OR by including realistic models and case studies throughout the book. Because of the importance of computations in OR, the book discusses how the theoretical algorithms fit in commercial computer codes (see Section 3.7). It also presents extensive tools for carrying out the computational task, ranging from tutorial-oriented TORA to the commercial packages Excel, Excel Solver, and AMPL. ^teachingmodels

OR is both an art and a science - the art of describing and modeling the problem and the science of solving the model using (precise) mathematical algorithms. A first course in the subject should give the student an appreciation of the importance of both areas. This will provide OR users with the kind of confidence that normally would be lacking if training is dedicated solely to the art aspect of OR, under the guise that computers can relieve the user of the need to understand why the solution algorithms work. ^artscience

Modeling and computational capabilities can be enhanced by studying published practical cases. To assist you in this regard, fully developed end-of-chapter case analyses are included. The cases cover most of the OR models presented in this book. There are also some 50 cases that are based on real-life applications in Appendix E on the website that accompanies this book. Additional case studies are available in journals and publications. In particular, Interfaces (published by INFORMS) is a rich source of diverse OR applications. ^practicalcases

## BIBLIOGRAPHY

Altier, W., The Thinking Manager's Toolbox: Effective Processes for Problem Solving and Decision Making, Oxford University Press, New York, 1999.

Brown, S. I., Insight into Mathematical Thought, NCTM, Reston, VA, 2013.

Checkland, P., Systems Thinking, System Practice, Wiley, New York, 1999.

Evans, J., Creative Thinking in the Decision and Management Sciences, South-Western Publishing, Cincinnati, 1991.

Morris, W., "On the Art of Modeling," Management Science, Vol. 13, pp. B707-B717, 1967.

Paulos, J., Innumeracy: Mathematical Illiteracy and Its Consequences, Hill and Wang, New York, 1988.

Singh, S., Fermat's Enigma, Walker, New York, 1997.

Willemain, T., "Insights on Modeling from a Dozen Experts," Operations Research, Vol. 42, No. 2, pp. 213-222, 1994.

## PROBLEMS7

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>1.2</td><td>1-1 to 1-11</td></tr></table>

1-1. In the tickets example,

(a) Provide an infeasible alternative.

(b) Identify a fourth feasible alternative and determine its cost.

1-2. In the garden problem, identify three feasible solutions, and determine which one is better.

1-3. Determine the optimal solution of the garden problem. (Hint: Use the constraint to express the objective function in terms of one variable, then use differential calculus.)

*1-4. Amy, Jim, John, and Kelly are standing on the east bank of a river and wish to cross to the west side using a canoe. The canoe can hold at most two people at a time. Amy, being the most athletic, can row across the river in 1 minute. Jim, John, and Kelly would take 3, 6, and 9 minutes, respectively. If two people are in the canoe, the slower person dictates the crossing time. The objective is for all four people to be on the other side of the river in the shortest time possible.

(a) Define the criterion for evaluating the alternatives (remember, the canoe is the only mode of transportation, and it cannot be shuttled empty).

*(b) What is the shortest time for moving all four people to the other side of the river?

1-5. In a baseball game, Jim is the pitcher and Joe is the batter. Suppose that Jim can throw either a fast or a curve ball at random. If Joe correctly predicts a curve ball, he can maintain a .400 batting average, else, if Jim throws a curve ball and Joe prepares for a fast ball, his batting average is kept down to .200. On the other hand, if Joe correctly predicts a fast ball, he gets a .250 batting average, else, his batting average is only .125.

(a) Define the alternatives for this situation.

(b) Define the objective function for the problem and discuss how it differs from the familiar optimization (maximization or minimization) of a criterion.

---

chapter problems throughout the book.

---

1-6. During the construction of a house, six joists of 24 ft each must be trimmed to the correct length of 23 ft. The operations for cutting a joist involve the following sequence:

<table><tr><td>Operation</td><td>Time (seconds)</td></tr><tr><td>1. Place joist on saw horses</td><td>15</td></tr><tr><td>2. Measure correct length (23 ft)</td><td>5</td></tr><tr><td>3. Mark cutting line for circular saw</td><td>5</td></tr><tr><td>4. Trim joist to correct length</td><td>20</td></tr><tr><td>5. Stack trimmed joist in a designated area</td><td>20</td></tr></table>

Three persons are involved: Two loaders must work simultaneously on operations 1, 2, and 5, and one cutter handles operations 3 and 4. There are two pairs of saw horses on which untrimmed joists are placed in preparation for cutting, and each pair can hold up to three side-by-side joists. Suggest a good schedule for trimming the six joists.

1-7. An upright symmetrical triangle is divided into four layers: The bottom layer consists of four (equally-spaced) dots, designated as A, B, C, and D. The next layer includes dots E, F, and G, and the following layer has dots H and I. The top layer has dot J. You want to invert the triangle (bottom layer has one dot and top layer has four) by moving the dots around as necessary. ${}^{8}$

(a) Identify two feasible solutions.

(b) Determine the smallest number of moves needed to invert the triangle.

1-8. You have five chains, each consisting of four solid links. You need to make a bracelet by connecting all five chains. It costs 2 cents to break a link and 3 cents to re-solder it.

(a) Identify two feasible solutions and evaluate them.

(b) Determine the cheapest cost for making the bracelet.

1-9. The squares of a rectangular board of 11 rows and 9 columns are numbered sequentially 1 through 99 with a hidden monetary reward between 0 and 50 dollars assigned to each square. A game using the board requires the player to choose a square by selecting any two digits and then subtracting the sum of its two digits from the selected number. The player then receives the reward assigned the selected square. What monetary values should be assigned to the 99 squares to minimize the player's reward (regardless of how many times the game is repeated)? To make the game interesting, the assignment of \$0 to all the squares is not an option.

1-10. You have 10 identical cartons each holding 10 water bottles. All bottles weigh 10 oz. each, except for one defective carton in which each of the 10 bottles weighs on 9 oz. only. A scale is available for weighing.

(a) Suggest a method for locating the defective carton.

*(b) What is the smallest number of times the scale is used that guarantees finding the defective carton? (Hint: You will need to be creative in deciding what to weigh.)

*1-11. You are given two identical balls made of a tough alloy. The hardness test fails if a ball dropped from a floor of a 120-storey building is dented upon impact. A ball can be reused in fresh drops only if it has not been dented in a previous drop. Using only these two identical balls, what is the smallest number of ball drops that will determine the highest floor from which the ball can be dropped without being damaged?

---

${}^{8}$ Problems 1-7 and 1-8 are adapted from Bruce Goldstein, Cognitive Psychology: Mind, Research, and Everyday Experience, Wadsworth Publishing, 2005.

---

This page intentionally left blank
