## CHAPTER 20 Classical Optimization Theory

### 20.1 UNCONSTRAINED PROBLEMS

An extreme point of a function $f\left( \mathbf{X}\right)$ defines either a maximum or a minimum of the function. Mathematically, a point ${\mathbf{X}}_{0} = \left( {{x}_{1}^{0},\ldots ,{x}_{j}^{0},\ldots ,{x}_{n}^{0}}\right)$ is a maximum if

$$
f\left( {{\mathbf{X}}_{0} + \mathbf{h}}\right)  \leq  f\left( {\mathbf{X}}_{0}\right)
$$

for all $\mathbf{h} = \left( {{h}_{1},\ldots ,{h}_{j},\ldots ,{h}_{n}}\right)$ , where $\left| {h}_{j}\right|$ is sufficiently small for all $j$ . In a similar manner, ${\mathbf{X}}_{0}$ is a minimum if

$$
f\left( {{\mathbf{X}}_{0} + \mathbf{h}}\right)  \geq  f\left( {\mathbf{X}}_{0}\right)
$$

Figure 20.1 illustrates the maxima and minima of a single-variable function $f\left( x\right)$ defined in the range $a \leq  x \leq  b$ . The points ${x}_{1},{x}_{2},{x}_{3},{x}_{4}$ , and ${x}_{6}$ are all extrema of $f\left( x\right)$ , with ${x}_{1},{x}_{3}$ , and ${x}_{6}$ as maxima and ${x}_{2}$ and ${x}_{4}$ as minima. The value $f\left( {x}_{6}\right)  = \; \max \left\{  {f\left( {x}_{1}\right) , f\left( {x}_{3}\right) , f\left( {x}_{6}\right) }\right\}$ is a global or absolute maximum, and $f\left( {x}_{1}\right)$ and $f\left( {x}_{3}\right)$ are local or relative maxima. Similarly, $f\left( {x}_{4}\right)$ is a local minimum and $f\left( {x}_{2}\right)$ is a global minimum.

Although ${x}_{1}$ (in Figure 20.1) is a (local) maximum point, it differs from remaining local maxima in that the value of $f$ corresponding to at least one point in the neighborhood of ${x}_{1}$ equals $f\left( {x}_{1}\right)$ . In this respect, ${x}_{1}$ is a weak maximum, whereas ${x}_{3}$ and ${x}_{6}$ are strong maxima. In general, for $\mathbf{h}$ as defined earlier, ${\mathbf{X}}_{0}$ is a weak maximum if $f\left( {{\mathbf{X}}_{0} + \mathbf{h}}\right)  \leq  f\left( {\mathbf{X}}_{0}\right)$ and a strong maximum if $f\left( {{\mathbf{X}}_{0} + \mathbf{h}}\right)  < f\left( {\mathbf{X}}_{0}\right)$ .

In Figure 20.1, the first derivative (slope) of $f$ equals zero at all extrema. This property is also satisfied at inflection and saddle points, such as ${x}_{5}$ . If a point with zero slope (gradient) is not an extremum (maximum or minimum), then it must be an inflection or a saddle point.

![bo_d56m5obef24c73bhe6ag_1_376_201_1114_679_0.jpg](bo_d56m5obef24c73bhe6ag_1_376_201_1114_679_0.jpg)

FIGURE 20.1

Examples of extreme points for a single-variable function

#### 20.1.1 Necessary and Sufficient Conditions

This section develops the necessary and sufficient conditions for an $n$ -variable function $f\left( \mathbf{X}\right)$ to have extrema. It is assumed that the first and second partial derivatives of $f\left( \mathbf{X}\right)$ are continuous for all $\mathbf{X}$ .

Theorem 20.1-1. A necessary condition for ${\mathbf{X}}_{0}$ to be an extreme point of $f\left( \mathbf{X}\right)$ is that

$$
\nabla f\left( {\mathbf{X}}_{0}\right)  = 0
$$

Because the necessary condition is also satisfied at inflection and saddle points, it is more appropriate to refer to the points obtained from the solution of $\nabla f\left( {\mathbf{X}}_{0}\right)  = \mathbf{0}$ as stationary points. The next theorem establishes the sufficiency conditions for ${\mathbf{X}}_{0}$ to be an extreme point.

Theorem 20.1-2. A sufficient condition for a stationary point ${\mathbf{X}}_{0}$ to be an extremum is that the Hessian matrix $\mathbf{H}$ evaluated at ${\mathbf{X}}_{0}$ satisfy the following conditions:

(i) $\mathbf{H}$ is positive definite if ${\mathbf{X}}_{0}$ is a minimum point.

(ii) $\mathbf{H}$ is negative definite if ${\mathbf{X}}_{0}$ is a maximum point.

Example 20.1-1

---

Consider the function

$$
f\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = {x}_{1} + 2{x}_{3} + {x}_{2}{x}_{3} - {x}_{1}^{2} - {x}_{2}^{2} - {x}_{3}^{2}
$$

---

The necessary condition $\nabla f\left( {\mathbf{X}}_{0}\right)  = 0$ gives

$$
\frac{\partial f}{\partial {x}_{1}} = 1 - 2{x}_{1} = 0
$$

$$
\frac{\partial f}{\partial {x}_{2}} = {x}_{3} - 2{x}_{2} = 0
$$

$$
\frac{\partial f}{\partial {x}_{3}} = 2 + {x}_{2} - 2{x}_{3} = 0
$$

The solution of these simultaneous equations is

$$
{\mathbf{X}}_{0} = \left( {\frac{1}{2},\frac{2}{3},\frac{4}{3}}\right)
$$

To determine the type of the stationary point, consider

$$
{\left| \mathbf{H}\right| }_{{\mathbf{X}}_{0}} = {\left( \begin{matrix} \frac{{\partial }^{2}f}{\partial {x}_{1}^{2}} & \frac{{\partial }^{2}f}{\partial {x}_{1}\partial {x}_{2}} & \frac{{\partial }^{2}f}{\partial {x}_{1}\partial {x}_{3}} \\  \frac{{\partial }^{2}f}{\partial {x}_{2}\partial {x}_{1}} & \frac{{\partial }^{2}f}{\partial {x}_{2}^{2}} & \frac{{\partial }^{2}f}{\partial {x}_{2}\partial {x}_{3}} \\  \frac{{\partial }^{2}f}{\partial {x}_{3}\partial {x}_{1}} & \frac{{\partial }^{2}f}{\partial {x}_{3}\partial {x}_{2}} & \frac{{\partial }^{2}f}{\partial {x}_{2}^{2}} \end{matrix}\right) }_{{\mathbf{X}}_{0}} = \left( \begin{array}{rrr}  - 2 & 0 & 0 \\  0 &  - 2 & 1 \\  0 & 1 &  - 2 \end{array}\right)
$$

The principal minor determinants of ${\left| \mathbf{H}\right| }_{{\mathbf{X}}_{0}}$ have the values -2,4, and -6, respectively. Thus, as shown in Section D.3, Appendix D on the website, ${\left| \mathbf{H}\right| }_{{\mathbf{X}}_{0}}$ is negative-definite, and ${\mathbf{X}}_{0} = \left( {\frac{1}{2},\frac{2}{3},\frac{4}{3}}\right)$ represents a maximum point.

In general, if ${\left| \mathbf{H}\right| }_{{\mathbf{X}}_{0}}$ is indefinite, ${\mathbf{X}}_{0}$ must be a saddle point. For nonconclusive cases, ${\mathbf{X}}_{0}$ may or may not be an extremum, and the sufficiency condition becomes rather involved, because higher-order terms in Taylor's expansion must be considered.

The sufficiency condition established by Theorem 20.1-2 applies to single-variable functions as follows. Given that ${y}_{0}$ is a stationary point, then

(i) ${y}_{0}$ is a maximum if ${f}^{\prime \prime }\left( {y}_{0}\right)  < 0$ .

(ii) ${y}_{0}$ is a minimum if ${f}^{\prime \prime }\left( {y}_{0}\right)  < 0$ .

If ${f}^{\prime \prime }\left( {y}_{0}\right)  = 0$ , higher-order derivatives must be investigated as the following theorem requires.

Theorem 20.1-3. Given ${y}_{0}$ , a stationary point of $f\left( y\right)$ , if the first $\left( {n - 1}\right)$ derivatives are zero and ${f}^{\left( n\right) }\left( {y}_{0}\right)  \neq  0$ , then

(i) If $n$ is odd, ${y}_{0}$ is an inflection point.

(ii) If $n$ is even, then ${y}_{0}$ is a minimum if ${f}^{\left( n\right) }\left( {y}_{0}\right)  > 0$ and a maximum if ${f}^{\left( n\right) }\left( {y}_{0}\right)  < 0$ .

![bo_d56m5obef24c73bhe6ag_3_429_206_605_272_0.jpg](bo_d56m5obef24c73bhe6ag_3_429_206_605_272_0.jpg)

FIGURE 20.2

Extreme points of $f\left( y\right)  = {y}^{4}$ and $g\left( y\right)  = {y}^{3}$

Example 20.1-2

Figure 20.2 graphs the following two functions:

$$
f\left( y\right)  = {y}^{4}
$$

$$
g\left( y\right)  = {y}^{3}
$$

For $f\left( y\right)  = {y}^{4},{f}^{\prime }\left( y\right)  = 4{y}^{3} = 0$ , which yields the stationary point ${y}_{0} = 0$ . Now

$$
{f}^{\prime }\left( 0\right)  = {f}^{\prime \prime }\left( 0\right)  = {f}^{\left( 3\right) }\left( 0\right)  = 0,{f}^{\left( 4\right) }\left( 0\right)  = {24} > 0
$$

Hence, ${y}_{0} = 0$ is a minimum point (see Figure 20.2).

For $g\left( y\right)  = {y}^{3},{g}^{\prime }\left( y\right)  = 3{y}^{2} = 0$ , which yields ${y}_{0} = 0$ as a stationary point. Also

$$
{g}^{\prime }\left( 0\right)  = {g}^{\prime \prime }\left( 0\right) ,{g}^{\left( 3\right) }\left( 0\right)  = 6 \neq  0
$$

Thus, ${y}_{0} = 0$ is an inflection point.

#### 20.1.2 The Newton-Raphson Method

In general, the necessary condition $\nabla f\left( \mathbf{X}\right)  = \mathbf{0}$ may be highly nonlinear and, hence, difficult to solve. The Newton-Raphson method is an iterative algorithm for solving simultaneous nonlinear equations.

Consider the simultaneous equations

$$
{f}_{i}\left( \mathbf{X}\right)  = 0, i = 1,2,\ldots , m
$$

Let ${\mathbf{X}}^{k}$ be a given point. Then by Taylor’s expansion

$$
{f}_{i}\left( \mathbf{X}\right)  \approx  {f}_{i}\left( {\mathbf{X}}_{k}\right)  + \nabla {f}_{i}\left( {\mathbf{X}}_{k}\right) \left( {\mathbf{X} - {\mathbf{X}}_{k}}\right) , i = 1,2,\ldots , m
$$

Thus, the original equations, ${f}_{i}\left( \mathbf{X}\right)  = 0, i = 1,2,\ldots , m$ , may be approximated as

$$
{f}_{i}\left( {\mathbf{X}}_{k}\right)  + \nabla {f}_{i}\left( {\mathbf{X}}_{k}\right) \left( {\mathbf{X} - {\mathbf{X}}_{k}}\right)  = 0, i = 1,2,\ldots , m
$$

These equations may be written in matrix notation as

$$
{\mathbf{A}}_{k} + {\mathbf{B}}_{k}\left( {\mathbf{X} - {\mathbf{X}}_{k}}\right)  = \mathbf{0}
$$

If ${\mathbf{B}}_{k}$ is nonsingular, then

$$
\mathbf{X} = {\mathbf{X}}_{k} - {\mathbf{B}}_{k}^{-1}{\mathbf{A}}_{k}
$$

The idea of the method is to start from an initial point ${\mathbf{X}}_{0}$ , and then use the equation above to determine a new point. The process may or may not converge depending on the selection of the starting point. Convergence occurs when two successive points, ${\mathbf{X}}_{k}$ and ${\mathbf{X}}_{k + 1}$ , are approximately equal (within specified acceptable tolerance).

A geometric interpretation of the method is illustrated by a single-variable function in Figure 20.3. The relationship between ${x}_{k}$ and ${x}_{k + 1}$ for a single-variable function $f\left( x\right)$ reduces to

$$
{x}_{k + 1} = {x}_{k} - \frac{f\left( {x}_{k}\right) }{{f}^{\prime }\left( {x}_{k}\right) }
$$

The terms may be arranged as ${f}^{\prime }\left( {x}_{k}\right)  = \frac{f\left( {x}_{k}\right) }{{x}_{k} - {x}_{k + 1}}$ -meaning that ${x}_{k + 1}$ is determined from the slope of $f\left( x\right)$ at ${x}_{k}$ , where tan $\theta  = {f}^{\prime }\left( {x}_{k}\right)$ , as the figure shows.

Figure 20.3 demonstrates that convergence is not always possible. If the initial point is $a$ , the method will diverge. In general, it may be necessary to attempt a number of initial points before convergence is achieved.

FIGURE 20.3

Illustration of the iterative process in the Newton-Raphson method

![bo_d56m5obef24c73bhe6ag_4_433_1204_1095_932_0.jpg](bo_d56m5obef24c73bhe6ag_4_433_1204_1095_932_0.jpg)

Example 20.1-3

To demonstrate the use of the Newton-Raphson method, consider the function

$$
g\left( x\right)  = {\left( 3x - 2\right) }^{2}{\left( 2x - 3\right) }^{2}
$$

To determine the stationary points of $g\left( x\right)$ , we need to solve

$$
f\left( x\right)  \equiv  {g}^{\prime }\left( x\right)  = {72}{x}^{3} - {234}{x}^{2} + {241x} - {78} = 0
$$

Thus, for the Newton-Raphson method, we have

$$
{f}^{\prime }\left( x\right)  = {216}{x}^{2} - {468x} + {241}
$$

$$
{x}_{k + 1} = {x}_{k} - \frac{{72}{x}^{3} - {234}{x}^{2} + {241x} - {78}}{{216}{x}^{2} - {468x} + {24}}
$$

Starting with ${x}_{0} = {10}$ , the following table provides the successive iterations:

<table><tr><td>$k$</td><td>${x}_{k}$</td><td>$f\left( {x}_{k}\right)$ <br> ${f}^{\prime }\left( {x}_{k}\right)$</td><td>${x}_{k + 1}$</td></tr><tr><td>0</td><td>10.000000</td><td>2.978923</td><td>7.032108</td></tr><tr><td>1</td><td>7.032108</td><td>1.976429</td><td>5.055679</td></tr><tr><td>2</td><td>5.055679</td><td>1.314367</td><td>3.741312</td></tr><tr><td>3</td><td>3.741312</td><td>0.871358</td><td>2.869995</td></tr><tr><td>4</td><td>2.869995</td><td>0.573547</td><td>2.296405</td></tr><tr><td>5</td><td>2.296405</td><td>0.371252</td><td>1.925154</td></tr><tr><td>6</td><td>1.925154</td><td>0.230702</td><td>1.694452</td></tr><tr><td>7</td><td>1.694452</td><td>0.128999</td><td>1.565453</td></tr><tr><td>8</td><td>1.565453</td><td>0.054156</td><td>1.511296</td></tr><tr><td>9</td><td>1.511296</td><td>0.010864</td><td>1.500432</td></tr><tr><td>10</td><td>1.500432</td><td>0.000431</td><td>1.500001</td></tr></table>

The method converges to $x = {1.5}$ . Actually, $f\left( x\right)$ has three stationary points at $x = \frac{2}{3}$ , $x = \frac{13}{12}$ , and $x = \frac{3}{2}$ . The remaining two points can be found by attempting different values for initial ${x}_{0}$ . In fact, ${x}_{0} = {.5}$ and ${x}_{0} = 1$ should yield the missing stationary points (try it!).

## Excel Moment

Template excelNewtonRaphson.xls can be used to solve any single-variable equation. It requires entering $\frac{f\left( x\right) }{{f}^{\prime }\left( x\right) }$ in cell C3. For Example 20.1-3, we enter

---

$$
= \left( {{72} * {A3}^{ \land  }3 - {234} * {A3}^{ \land  }2 + {241} * {A3} - {78}}\right) /\left( {{216} * {A3}^{ \land  }2 - {468} * {A3} + {241}}\right)
$$

---

The variable $x$ is replaced with A3. The template allows setting a tolerance limit $\Delta$ , which specifies the allowable difference between ${x}_{k}$ and ${x}_{k + 1}$ that signals the termination of the iterations. You are encouraged to use different initial points, ${x}_{0}$ , to get a feel of how the method works.

### 20.2 CONSTRAINED PROBLEMS

This section deals with the optimization of constrained continuous functions. Section 20.2.1 introduces the case of equality constraints, and Section 20.2.2 deals with inequality constraints. The presentation in Section 20.2.1 is covered for the most part in Beightler and Associates (1979, pp. 45-55).

#### 20.2.1 Equality Constraints

This section presents two methods: the Jacobian and the Lagrangean. The Lagrangean method can be developed logically from the Jacobian. This relationship provides an interesting economic interpretation of the Lagrangean method.

Constrained derivatives (Jacobian) method. Consider the problem

$$
\text{ Minimize }z = f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

where

$$
\mathbf{X} = \left( {{x}_{1},{x}_{2},\ldots ,{x}_{n}}\right)
$$

$$
\mathbf{g} = {\left( {g}_{1},{g}_{2},\ldots ,{g}_{m}\right) }^{T}
$$

The functions $f\left( \mathbf{X}\right)$ and $g\left( \mathbf{X}\right) , i = 1,2,\ldots , m$ , are twice continuously differentiable.

The idea of using constrained derivatives is to develop a closed-form expression for the first partial derivatives of $f\left( \mathbf{X}\right)$ at all points satisfying $g\left( \mathbf{X}\right)  = \mathbf{0}$ . The corresponding stationary points are identified as the points at which these partial derivatives vanish. The sufficiency conditions introduced in Section 20.1 can then be used to check the identity of stationary points.

To clarify the proposed concept, consider $f\left( {{x}_{1},{x}_{2}}\right)$ illustrated in Figure 20.4. This function is to be minimized subject to the constraint

$$
{g}_{1}\left( {{x}_{1},{x}_{2}}\right)  = {x}_{2} - b = 0
$$

where $b$ is a constant. From Figure 20.4, the curve designated by the three points $A$ , $B$ , and $C$ represents the values of $f\left( {{x}_{1},{x}_{2}}\right)$ satisfying the given constraint. The constrained derivatives method defines the gradient of $f\left( {{x}_{1},{x}_{2}}\right)$ at any point on the curve ${ABC}$ . Point $B$ at which the constrained derivative vanishes is a stationary point for the constrained problem.

The method is now developed mathematically. By Taylor’s theorem, for $\mathbf{X} + \Delta \mathbf{X}$ in the feasible neighborhood of $\mathbf{X}$ , we have

$$
f\left( {\mathbf{X} + \Delta \mathbf{X}}\right)  - f\left( \mathbf{X}\right)  = \nabla f\left( \mathbf{X}\right) \Delta \mathbf{X} + O\left( {\Delta {x}_{j}^{2}}\right)
$$

and

$$
\mathbf{g}\left( {\mathbf{X} + \Delta \mathbf{X}}\right)  - \mathbf{g}\left( \mathbf{X}\right)  = \nabla \mathbf{g}\left( \mathbf{X}\right) \Delta \mathbf{X} + O\left( {\Delta {x}_{j}^{2}}\right)
$$

As $\Delta {x}_{j} \rightarrow  0$ , the equations reduce to

$$
\partial f\left( \mathbf{X}\right)  = \nabla f\left( \mathbf{X}\right) \partial \mathbf{X}
$$

and

$$
\partial \mathbf{g}\left( \mathbf{X}\right)  = \nabla \mathbf{g}\left( \mathbf{X}\right) \partial \mathbf{X}
$$

![bo_d56m5obef24c73bhe6ag_7_286_191_849_1078_0.jpg](bo_d56m5obef24c73bhe6ag_7_286_191_849_1078_0.jpg)

FIGURE 20.4

Demonstration of the idea of the Jacobian method

For feasibility, we must have $\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0},\partial \mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}$ . Hence

$$
\partial f\left( \mathbf{X}\right)  - \nabla f\left( \mathbf{X}\right) \partial \mathbf{X} = 0
$$

$$
\nabla \mathbf{g}\left( \mathbf{X}\right) \partial \mathbf{X} = \mathbf{0}
$$

This gives $\left( {m + 1}\right)$ equations in $\left( {n + 1}\right)$ unknowns, $\partial f\left( \mathbf{X}\right)$ and $\partial \mathbf{X}$ . Note that $\partial f\left( \mathbf{X}\right)$ is a dependent variable whose value is determined once $\partial \mathbf{X}$ is known. This means that, in effect, we have $m$ equations in $n$ unknowns.

If $m > n$ , at least $\left( {m - n}\right)$ equations are redundant. Eliminating redundancy, the system reduces to $m \leq  n$ . If $m = n$ , the solution is $\partial \mathbf{X} = \mathbf{0}$ , and $\mathbf{X}$ has no feasible neighborhood, which means that the solution space consists of one point only. The remaining case $\left( {m < n}\right)$ requires further elaboration.

Define

$$
\mathbf{X} = \left( {\mathbf{Y},\mathbf{Z}}\right)
$$

such that

$$
\mathbf{Y} = \left( {{y}_{1},{y}_{2},\ldots ,{y}_{m}}\right) ,\mathbf{Z} = \left( {{z}_{1},{z}_{2},\ldots ,{z}_{n - m}}\right)
$$

The vectors $\mathbf{Y}$ and $\mathbf{Z}$ represent the dependent and independent variables, respectively. Rewriting the gradient vectors of $f$ and $g$ in terms of $\mathbf{Y}$ and $\mathbf{Z}$ , we get

$$
\nabla f\left( {\mathbf{Y},\mathbf{Z}}\right)  = \left( {{\nabla }_{\mathbf{Y}}f,{\nabla }_{\mathbf{Z}}f}\right)
$$

$$
\nabla g\left( {\mathbf{Y},\mathbf{Z}}\right)  = \left( {{\nabla }_{\mathbf{Y}}\mathbf{g},{\nabla }_{\mathbf{Z}}\mathbf{g}}\right)
$$

Define

$$
\mathbf{J} = {\nabla }_{\mathbf{Y}}\mathbf{g} = \left( \begin{matrix} {\nabla }_{\mathbf{Y}}{g}_{1} \\  \vdots \\  {\nabla }_{\mathbf{Y}}{g}_{m} \end{matrix}\right)
$$

$$
\mathbf{C} = {\nabla }_{\mathbf{Z}}\mathbf{g} = \left( \begin{matrix} {\nabla }_{\mathbf{Z}}{g}_{1} \\  \vdots \\  {\nabla }_{\mathbf{Z}}{g}_{m} \end{matrix}\right)
$$

${\mathbf{J}}_{m \times  m}$ is called the Jacobian matrix and ${\mathbf{C}}_{m \times  n - m}$ the control matrix. The Jacobian $\mathbf{J}$ is assumed nonsingular. This is always possible because the given $m$ equations are independent by definition. The components of the vector $\mathbf{Y}$ must thus be selected such that $\mathbf{J}$ is nonsingular.

The original set of equations in $\partial f\left( \mathbf{X}\right)$ and $\partial \mathbf{X}$ may be written as

$$
\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)  = {\nabla }_{\mathbf{Y}}f\partial \mathbf{Y} + {\nabla }_{\mathbf{Z}}f\partial \mathbf{Z}
$$

and

$$
\mathbf{J}\partial \mathbf{Y} =  - \mathbf{C}\partial \mathbf{Z}
$$

Given $\mathbf{J}$ is nonsingular, it follows that

$$
\partial \mathbf{Y} =  - {\mathbf{J}}^{-1}\mathbf{C}\partial \mathbf{Z}
$$

Substituting for $\partial \mathbf{Y}$ in the equation for $\partial f\left( \mathbf{X}\right)$ gives $\partial f$ as a function of $\partial \mathbf{Z} -$ that is,

$$
\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)  = \left( {{\nabla }_{\mathbf{Z}}f - {\nabla }_{\mathbf{Y}}f{\mathbf{J}}^{-1}\mathbf{C}}\right) \partial \mathbf{Z}
$$

From this equation, the constrained derivative with respect to the independent vector $\mathbf{Z}$ is given by

$$
{\nabla }_{c}f = \frac{{\partial }_{c}f\left( {\mathbf{Y},\mathbf{Z}}\right) }{{\partial }_{c}\mathbf{Z}} = {\nabla }_{\mathbf{z}}f - {\nabla }_{\mathbf{Y}}f{\mathbf{J}}^{-1}\mathbf{C}
$$

where ${\nabla }_{c}f$ is the constrained gradient vector of $f$ with respect to $\mathbf{Z}$ . Thus, ${\nabla }_{c}f\left( {\mathbf{Y},\mathbf{Z}}\right)$ must be null at the stationary points.

The sufficiency conditions are similar to those developed in Section 20.1. The (constrained) Hessian matrix corresponds to the independent vector $\mathbf{Z}$ , and the elements of the Hessian matrix must be the constrained second derivatives.

Example 20.2-1

Consider the following problem:

$$
f\left( \mathbf{X}\right)  = {x}_{1}^{2} + 3{x}_{2}^{2} + 5{x}_{1}{x}_{3}^{2}
$$

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1}{x}_{3} + 2{x}_{2} + {x}_{2}^{2} - {11} = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = {x}_{1}^{2} + 2{x}_{1}{x}_{2} + {x}_{3}^{2} - {14} = 0
$$

Given the feasible point ${\mathbf{X}}^{0} = \left( {1,2,3}\right)$ , we wish to study the variation in $f\left( { = {\partial }_{c}f}\right)$ in the feasible neighborhood of ${\mathbf{X}}^{0}$ .

Let

$$
\mathbf{Y} = \left( {{x}_{1},{x}_{3}}\right) \text{ and }\mathbf{Z} = {x}_{2}
$$

Thus,

$$
{\nabla }_{\mathbf{Y}}f = \left( {\frac{\partial f}{\partial {x}_{1}},\frac{\partial f}{\partial {x}_{3}}}\right)  = \left( {2{x}_{1} + 5{x}_{3}^{2},{10}{x}_{1}{x}_{3}}\right)
$$

$$
{\nabla }_{\mathbf{Z}}f = \frac{\partial f}{\partial {x}_{2}} = 6{x}_{2}
$$

$$
\mathbf{J} = \left( \begin{array}{ll} \frac{\partial {g}_{1}}{\partial {x}_{1}} & \frac{\partial {g}_{1}}{\partial {x}_{3}} \\  \frac{\partial {g}_{2}}{\partial {x}_{1}} & \frac{\partial {g}_{2}}{\partial {x}_{3}} \end{array}\right) \left( \begin{array}{ll} {x}_{3} & {x}_{1} \\  2{x}_{1} + 2{x}_{2} & 2{x}_{3} \end{array}\right)
$$

$$
\mathbf{C} = \left( \begin{array}{l} \frac{\partial {g}_{1}}{\partial {x}_{2}} \\  \frac{\partial {g}_{2}}{\partial {x}_{2}} \end{array}\right)  = \left( \begin{matrix} 2{x}_{2} + 2 \\  2{x}_{1} \end{matrix}\right)
$$

Suppose that we need to estimate ${\partial }_{c}f$ in the feasible neighborhood of the feasible point ${\mathbf{X}}_{0} = \left( {1,2,3}\right)$ , given a small change $\partial {x}_{2} = {.01}$ in the independent variable ${x}_{2}$ . We have

$$
{\mathbf{J}}^{-1}\mathbf{C} = {\left( \begin{array}{ll} 3 & 1 \\  6 & 6 \end{array}\right) }^{-1}\left( \begin{array}{l} 6 \\  2 \end{array}\right)  = \left( \begin{array}{rr} \frac{6}{12} &  - \frac{1}{12} \\   - \frac{6}{12} & \frac{3}{12} \end{array}\right) \left( \begin{array}{l} 6 \\  2 \end{array}\right)  \approx  \left( \begin{array}{r} {2.83} \\   - {2.50} \end{array}\right)
$$

Hence, the incremental value of constrained $f$ is given as

$$
{\partial }_{c}f = \left( {{\nabla }_{\mathbf{Z}}f - {\nabla }_{\mathbf{Y}}f{\mathbf{J}}^{-1}\mathbf{C}}\right) \partial \mathbf{Z} = \left( {6\left( 2\right)  - \left( {{47},{30}}\right) \left( \begin{array}{r} {2.83} \\   - {2.50} \end{array}\right) }\right) \partial {x}_{2} =  - {46.01}\partial {x}_{2}
$$

By specifying the value of $\partial {x}_{2}$ for the independent variable ${x}_{2}$ , feasible values of $\partial {x}_{1}$ and $\partial {x}_{2}$ are determined for the dependent variables ${x}_{1}$ and ${x}_{3}$ using the formula

$$
\partial \mathbf{Y} =  - {\mathbf{J}}^{-1}\mathbf{C}\partial \mathbf{Z}
$$

Thus, for $\partial {x}_{2} = {.01}$ ,

$$
\left( \begin{array}{l} \partial {x}_{1} \\  \partial {x}_{3} \end{array}\right)  =  - {\mathbf{J}}^{-1}\mathbf{C}\partial {x}_{2} = \left( \begin{array}{r}  - {.0283} \\  {.0250} \end{array}\right)
$$

We now compare the value of ${\partial }_{c}f$ as computed above with the difference $f\left( {{\mathbf{X}}_{0} + \partial \mathbf{X}}\right)  - f\left( {\mathbf{X}}_{0}\right)$ , given $\partial {x}_{2} = {.01}$ .

$$
{\mathbf{X}}_{0} + \partial \mathbf{X} = \left( {1 - {.0283},2 + {.01},3 + {.025}}\right)  = \left( {{.9717},{2.01},{3.025}}\right)
$$

This yields

$$
f\left( {\mathbf{X}}_{0}\right)  = {58}, f\left( {{\mathbf{X}}_{0} + \partial \mathbf{X}}\right)  = {57.523}
$$

or

$$
f\left( {{\mathbf{X}}_{0} + \partial \mathbf{X}}\right)  - f\left( {\mathbf{X}}_{0}\right)  =  - {.477}
$$

The amount -.477 compares favorably with ${\partial }_{c}f =  - {46.01}\partial {x}_{2} =  - {.4601}$ . The difference between the two values is the result of the linear approximation in computing ${\partial }_{c}f$ at ${\mathbf{X}}_{0}$ .

## Example 20.2-2

This example illustrates the use of constrained derivatives. Consider the problem

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = {x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1} + {x}_{2} + 3{x}_{3} - 2 = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = 5{x}_{1} + 2{x}_{2} + {x}_{3} - 5 = 0
$$

We determine the constrained extreme points as follows. Let

$$
\mathbf{Y} = \left( {{x}_{1},{x}_{2}}\right) \text{ and }\mathbf{Z} = {x}_{3}
$$

Thus,

$$
{\nabla }_{\mathbf{Y}}f = \left( {\frac{\partial f}{\partial {x}_{1}},\frac{\partial f}{\partial {x}_{2}}}\right)  = \left( {2{x}_{1},2{x}_{2}}\right) ,{\nabla }_{\mathbf{Z}}f = \frac{\partial f}{\partial {x}_{3}} = 2{x}_{3}
$$

$$
\mathbf{J} = \left( \begin{array}{ll} 1 & 1 \\  5 & 2 \end{array}\right) ,{\mathbf{J}}^{-1} = \left( \begin{array}{rr}  - \frac{2}{3} & \frac{1}{3} \\  \frac{5}{3} &  - \frac{1}{3} \end{array}\right) ,\mathbf{C} = \left( \begin{array}{l} 3 \\  1 \end{array}\right)
$$

Hence,

$$
{\nabla }_{c}f = \frac{{\partial }_{c}f}{{\partial }_{c}{x}_{3}} = 2{x}_{3} - \left( {2{x}_{1},2{x}_{2}}\right) \left( \begin{array}{rr}  - \frac{2}{3} & \frac{1}{3} \\  \frac{5}{3} &  - \frac{1}{3} \end{array}\right) \left( \begin{array}{l} 3 \\  1 \end{array}\right)
$$

$$
= \frac{10}{3}{x}_{1} - \frac{28}{3}{x}_{2} + 2{x}_{3}
$$

The equations for determining the stationary points are thus given as

$$
{\nabla }_{c}f = 0
$$

$$
{g}_{1}\left( \mathbf{X}\right)  = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = 0
$$

or

$$
\left( \begin{array}{rrr} {10} &  - {28} & 6 \\  1 & 1 & 3 \\  5 & 2 & 1 \end{array}\right) \left( \begin{array}{l} {x}_{1} \\  {x}_{2} \\  {x}_{3} \end{array}\right)  = \left( \begin{array}{l} 0 \\  2 \\  5 \end{array}\right)
$$

The solution is

$$
{\mathbf{X}}_{0} \approx  \left( {{.81},{.35},{.28}}\right)
$$

The identity of this stationary point is checked using the sufficiency condition. Given that ${x}_{3}$ is the independent variable, it follows from ${\nabla }_{c}f$ that

$$
\frac{{\partial }_{c}^{2}f}{{\partial }_{c}{x}_{3}^{2}} = \frac{10}{3}\left( \frac{d{x}_{1}}{d{x}_{3}}\right)  - \frac{28}{3}\left( \frac{d{x}_{2}}{d{x}_{3}}\right)  + 2 = \left( {\frac{10}{3}, - \frac{28}{3}}\right) \left( \frac{\frac{d{x}_{1}}{d{x}_{3}}}{\frac{d{x}_{2}}{d{x}_{3}}}\right)  + 2
$$

From the Jacobian method,

$$
\left( \begin{array}{l} \frac{d{x}_{1}}{d{x}_{3}} \\  \frac{d{x}_{2}}{d{x}_{3}} \end{array}\right)  =  - {\mathbf{J}}^{-1}\mathbf{C} = \left( \begin{array}{r} \frac{5}{3} \\   - \frac{14}{3} \end{array}\right)
$$

Substitution gives $\frac{{\partial }_{c}^{2}f}{{\partial }_{c}{x}_{3}^{2}} = \frac{460}{9} > 0$ . Hence, ${\mathbf{X}}_{0}$ is the minimum point.

Sensitivity analysis in the Jacobian method. The Jacobian method can be used to study the effect of small changes in the right-hand side of the constraints on the optimal value of $f$ . Specifically, what is the effect of changing ${g}_{i}\left( \mathbf{X}\right)  = 0$ to ${g}_{i}\left( \mathbf{X}\right)  = \partial {g}_{i}$ on the optimal value of $f$ ? This type of investigation is called sensitivity analysis and is similar to that carried out in linear programming (see Chapters 3 and 4). However, sensitivity analysis in nonlinear programming is valid only in the small neighborhood of the extreme point. The development will be helpful in studying the Lagrangean method.

We have shown previously that

$$
\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)  = {\nabla }_{\mathbf{Y}}f\partial \mathbf{Y} + {\nabla }_{\mathbf{Z}}f\partial \mathbf{Z}
$$

$$
\partial \mathbf{g} = \mathbf{J}\partial \mathbf{Y} + \mathbf{C}\partial \mathbf{Z}
$$

Given $\partial \mathbf{g} \neq  0$ , then

$$
\partial \mathbf{Y} = {\mathbf{J}}^{-1}\partial \mathbf{g} - {\mathbf{J}}^{-1}\mathbf{C}\partial \mathbf{Z}
$$

Substituting in the equation for $\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)$ gives

$$
\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)  = {\nabla }_{\mathbf{Y}}f{\mathbf{J}}^{-1}\partial \mathbf{g} + {\nabla }_{c}f\partial \mathbf{Z}
$$

where

$$
{\nabla }_{c}f = {\nabla }_{\mathbf{Z}}f - {\nabla }_{\mathbf{Y}}f{\mathbf{J}}^{-1}\mathbf{C}
$$

as defined previously. The expression for $\partial f\left( {\mathbf{Y},\mathbf{Z}}\right)$ can be used to study variation in $f$ in the feasible neighborhood of a feasible point ${\mathbf{X}}_{0}$ resulting from small changes $\partial \mathbf{g}$ and $\partial \mathbf{Z}$ .

At the extreme (indeed, any stationary) point ${\mathbf{X}}_{0} = \left( {{\mathbf{Y}}_{0},{\mathbf{Z}}_{0}}\right)$ , the constrained gradient ${\nabla }_{c}f$ must vanish. Thus

$$
\partial f\left( {{\mathbf{Y}}_{0},{\mathbf{Z}}_{0}}\right)  = {\nabla }_{{\mathbf{Y}}_{0}}f{\mathbf{J}}^{-1}\partial \mathbf{g}\left( {{\mathbf{Y}}_{0},{\mathbf{Z}}_{0}}\right)
$$

or

$$
\frac{\partial f}{\partial \mathbf{g}} = {\nabla }_{{\mathbf{Y}}_{0}}f{\mathbf{J}}^{-1}
$$

The effect of the small change $\partial \mathbf{g}$ on the optimum value of $f$ can be studied by evaluating the rate of change of $f$ with respect to $\mathbf{g}$ . These rates are usually referred to as sensitivity coefficients.

## Example 20.2-3

---

Consider the same problem of Example 20.2-2. The optimum point is given by ${\mathbf{X}}_{0} =$

$\left( {{x}_{01},{x}_{02},{x}_{03}}\right)  = \left( {{.81},{.35},{.28}}\right)$ . Given ${\mathbf{Y}}_{0} = \left( {{x}_{01},{x}_{02}}\right)$ , then

$$
{\nabla }_{{\mathbf{Y}}_{0}}f = \left( {\frac{\partial f}{\partial {x}_{1}},\frac{\partial f}{\partial {x}_{2}}}\right)  = \left( {2{x}_{01},2{x}_{02}}\right)  = \left( {{1.62},{.70}}\right)
$$

Consequently,

$$
\left( {\frac{\partial f}{\partial {g}_{1}},\frac{\partial f}{\partial {g}_{2}}}\right)  = {\nabla }_{{\mathbf{Y}}_{0}}f{\mathbf{J}}^{-1} = \left( {{1.62},{.7}}\right) \left( \begin{array}{rr}  - \frac{2}{3} & \frac{1}{3} \\  \frac{5}{3} &  - \frac{1}{3} \end{array}\right)  = \left( {{.0876},{.3067}}\right)
$$

This means that for $\partial {g}_{1} = 1, f$ will increase approximately by .0867. Similarly, for $\partial {g}_{2} = 1, f$ will

increase approximately by .3067.

---

Lagrangean method. In the Jacobian method, let the vector $\mathbf{\lambda }$ represent the sensitivity coefficients - that is

$$
\mathbf{\lambda } = {\nabla }_{{\mathbf{Y}}_{0}}{\mathbf{J}}^{-1} = \frac{\partial f}{\partial \mathbf{g}}
$$

Thus,

$$
\partial f - \lambda \partial \mathbf{g} = 0
$$

This equation satisfies the necessary conditions for stationary points because $\frac{\partial f}{\partial \mathbf{g}}$ is computed such that ${\nabla }_{c}f = \mathbf{0}$ . A more convenient form for presenting these equations is to take their partial derivatives with respect to all ${x}_{j}$ . This yields

$$
\frac{\partial }{\partial {x}_{j}}\left( {f - \lambda \mathbf{g}}\right)  = 0,\;j = 1,2,\ldots , n
$$

The resulting equations together with the constraint equations $\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}$ yield the feasible values of $\mathbf{X}$ and $\mathbf{\lambda }$ that satisfy the necessary conditions for stationary points.

The given procedure defines the Lagrangean method for identifying the stationary points of optimization problems with equality constraints. Let

$$
L\left( {\mathbf{X},\mathbf{\lambda }}\right)  = f\left( \mathbf{X}\right)  - \mathbf{{\lambda g}}\left( \mathbf{X}\right)
$$

The function $L$ is called the Lagrangean function and the elements of the vector $\mathbf{\lambda }$ constitute the Lagrange multipliers. By definition, these multipliers have the same interpretation as the sensitivity coefficients of the Jacobian method

The equations

$$
\frac{\partial L}{\partial \mathbf{\lambda }} = 0,\frac{\partial L}{\partial \mathbf{X}} = 0
$$

give the necessary conditions for determining stationary points of $f\left( \mathbf{X}\right)$ subject to $\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}$ . Sufficiency conditions for the Lagrangean method exist, but they are generally computationally difficult.

## Example 20.2-4

Consider the problem of Example 20.2-2. The Lagrangean function is

$$
L\left( {\mathbf{X},\mathbf{\lambda }}\right)  = {x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2} - {\lambda }_{1}\left( {{x}_{1} + {x}_{2} + 3{x}_{3} - 2}\right)  - {\lambda }_{2}\left( {5{x}_{1} + 2{x}_{2} + {x}_{3} - 5}\right)
$$

This yields the following necessary conditions:

$$
\frac{\partial L}{\partial {x}_{1}} = 2{x}_{1} - {\lambda }_{1} - 5{\lambda }_{2} = 0
$$

$$
\frac{\partial L}{\partial {x}_{2}} = 2{x}_{2} - {\lambda }_{1} - 2{\lambda }_{2} = 0
$$

$$
\frac{\partial L}{\partial {x}_{3}} = 2{x}_{3} - 3{\lambda }_{1} - {\lambda }_{2} = 0
$$

$$
\frac{\partial L}{\partial {\lambda }_{1}} =  - \left( {{x}_{1} + {x}_{2} + 3{x}_{3} - 2}\right)  = 0
$$

$$
\frac{\partial L}{\partial {\lambda }_{2}} =  - \left( {5{x}_{1} + 2{x}_{2} + {x}_{3} - 5}\right)  = 0
$$

The solution to these simultaneous equations yields

$$
{\mathbf{X}}_{0} = \left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = \left( {{.8043},{.3478},{.2826}}\right)
$$

$$
\mathbf{\lambda } = \left( {{\lambda }_{1},{\lambda }_{2}}\right)  = \left( {{.0870},{.3043}}\right)
$$

This solution combines the results of Examples 20.2-2 and 20.2-3. The values of the Lagrange multipliers, as given by the vector $\mathbf{\lambda }$ , equal the sensitivity coefficients obtained in Example 20.2-3. The result shows that these coefficients are independent of the specific choice of the dependent vector $\mathbf{Y}$ in the Jacobian method.

#### 20.2.2 Inequality Constraints—Karush-Kuhn-Tucker (KKT) Conditions ${}^{1}$

This section extends the Lagrangean method to problems with inequality constraints. The main contribution of the section is the development of the general Karush-Kuhn-Tucker (KKT) necessary conditions for determining the stationary points. These conditions are also sufficient under certain rules that will be stated later.

Consider the problem

$$
\text{ Maximize }z = f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}
$$

---

${}^{1}$ W. Karush was the first to develop the KKT conditions in 1939 as part of an M.S. thesis at the University of Chicago. The same conditions were developed independently in 1951 by W. Kuhn and A. Tucker.

---

The inequality constraints may be converted into equations by using nonnegative slack variables. Let ${S}_{i}^{2}\left( { \geq  0}\right)$ be the slack quantity added to the $i$ th constraint ${g}_{i}\left( \mathbf{X}\right)  \leq  0$ and define

$$
\mathbf{S} = {\left( {S}_{1},{S}_{2},\ldots ,{S}_{m}\right) }^{T},{\mathbf{S}}^{2} = {\left( {S}_{1}^{2},{S}_{2}^{2},\ldots ,{S}_{m}^{2}\right) }^{T}
$$

where $m$ is the total number of inequality constraints. The Lagrangean function is thus given by

$$
L\left( {\mathbf{X},\mathbf{S},\mathbf{\lambda }}\right)  = f\left( \mathbf{X}\right)  - \mathbf{\lambda }\left\lbrack  {\mathbf{g}\left( \mathbf{X}\right)  + {\mathbf{S}}^{2}}\right\rbrack
$$

Given the constraints $\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}$ , a necessary condition for optimality is that $\mathbf{\lambda }$ be nonnegative (nonpositive) for maximization (minimization) problems. This result is justified by noting that the vector $\mathbf{\lambda }$ measures the rate of variation of $f$ with respect to g-that is,

$$
\lambda  = \frac{\partial f}{\partial \mathbf{g}}
$$

In the maximization case, as the right-hand side of the constraint $\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}$ increases from0to the vector $\partial \mathbf{g}$ , the solution space becomes less constrained and hence $f$ cannot decrease, meaning that $\mathbf{\lambda } \geq  \mathbf{0}$ . Similarly for minimization, as the right-hand side of the constraints increases, $f$ cannot increase, which implies that $\mathbf{\lambda } \leq  \mathbf{0}$ . If the constraints are equalities, that is, $\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}$ , then $\mathbf{\lambda }$ becomes unrestricted in sign (see Problem 20-18).

The restrictions on $\mathbf{\lambda }$ hold as part of the KKT necessary conditions. The remaining conditions will now be developed.

Taking the partial derivatives of $L$ with respect to $\mathbf{X},\mathbf{S}$ , and $\mathbf{\lambda }$ , we obtain

$$
\frac{\partial L}{\partial \mathbf{X}} = \nabla f\left( \mathbf{X}\right)  - \mathbf{\lambda }\nabla \mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

$$
\frac{\partial L}{\partial {S}_{i}} =  - 2{\lambda }_{i}{S}_{i} = 0, i = 1,2,\ldots , m
$$

$$
\frac{\partial L}{\partial \mathbf{\lambda }} =  - \left( {\mathbf{g}\left( \mathbf{X}\right)  + {\mathbf{S}}^{2}}\right)  = \mathbf{0}
$$

The second set of equations reveals the following results:

1. If ${\lambda }_{i} \neq  0$ , then ${S}_{i}^{2} = 0$ . This result means that the corresponding resource is scarce (i.e., consumed completely).

2. If ${S}_{i}^{2} > 0$ , then ${\lambda }_{i} = 0$ . This means resource $i$ is not scarce and, hence, it has no effect on the value of $f$ (i.e., ${\lambda }_{i} = \frac{\partial f}{\partial {g}_{i}} = 0$ ).

From the second and third sets of equations, we obtain

$$
{\lambda }_{i}{g}_{i}\left( \mathbf{X}\right)  = 0, i = 1,2,\ldots , m
$$

This new condition essentially repeats the foregoing argument, because if ${\lambda }_{i} > 0$ , ${g}_{i}\left( \mathbf{X}\right)  = 0$ or ${S}_{i}^{2} = 0$ ; and if ${g}_{i}\left( \mathbf{X}\right)  < 0,{S}_{i}^{2} > 0$ , and ${\lambda }_{i} = 0$ .

TABLE 20.1 Sufficiency of the KKT Conditions

<table><tr><td rowspan="2">Sense of optimization</td><td colspan="2">Required conditions</td></tr><tr><td>Objective function</td><td>Solution space</td></tr><tr><td>Maximization Minimization</td><td>Concave <br> Convex</td><td>Convex set <br> Convex set</td></tr></table>

The KKT necessary conditions for maximization problem are summarized as follows:

$$
\lambda  \geq  0
$$

$$
\nabla f\left( \mathbf{X}\right)  - \lambda \nabla \mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

$$
{\lambda }_{i}{g}_{i}\left( \mathbf{X}\right)  = 0,\;i = 1,2,\ldots , m
$$

$$
\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}
$$

These conditions apply to the minimization case as well, except that $\mathbf{\lambda }$ must be nonpositive (verify!). In both maximization and minimization, the Lagrange multipliers corresponding to equality constraints are unrestricted in sign.

Sufficiency of the KKT conditions. The KKT necessary conditions are also sufficient if the objective function and the solution space satisfy the conditions in Table 20.1.

It is simpler to verify that a function is convex or concave than to prove that a solution space is a convex set. For this reason, we provide a subset of sufficiency conditions which, though not as general as the ones in Table 20.1, are easier to apply in practice. To provide these conditions, we define the generalized nonlinear problems as

$$
\text{ Maximize or minimize }z = f\left( \mathbf{X}\right)
$$

subject to

$$
{g}_{i}\left( \mathbf{X}\right)  \leq  0, i = 1,2,\ldots , r
$$

$$
{g}_{i}\left( \mathbf{X}\right)  \geq  0, i = r + 1,\ldots , p
$$

$$
{g}_{i}\left( \mathbf{X}\right)  = 0, i = p + 1,\ldots , m
$$

$$
L\left( {\mathbf{X},\mathbf{S},\mathbf{\lambda }}\right)  = f\left( \mathbf{X}\right)  - \mathop{\sum }\limits_{{i = 1}}^{r}{\lambda }_{i}\left\lbrack  {{g}_{i}\left( \mathbf{X}\right)  + {S}_{i}^{2}}\right\rbrack   - \mathop{\sum }\limits_{{i = r + 1}}^{p}{\lambda }_{i}\left\lbrack  {{g}_{i}\left( \mathbf{X}\right)  - {S}_{i}^{2}}\right\rbrack   - \mathop{\sum }\limits_{{i = p + 1}}^{m}{\lambda }_{i}{g}_{i}\left( \mathbf{X}\right)
$$

The parameter ${\lambda }_{i}$ is the Lagrange multiplier associated with constraint $i$ . The conditions for establishing the sufficiency of the KKT conditions are summarized in Table 20.2.

The conditions in Table 20.2 are a subset of the conditions in Table 20.1 because a solution space can be convex without satisfying the conditions in Table 20.2.

Table 20.2 is valid because the given conditions yield a concave Lagrangean function $L\left( {\mathbf{X},\mathbf{S},\mathbf{\lambda }}\right)$ in case of maximization and a convex $L\left( {\mathbf{X},\mathbf{S},\mathbf{\lambda }}\right)$ in case of minimization. This result is verified by noticing that if ${g}_{i}\left( x\right)$ is convex, then ${\lambda }_{i}{g}_{i}\left( x\right)$ is convex if ${\lambda }_{i} \geq  0$ and concave if ${\lambda }_{i} \leq  0$ . Similar interpretations can be established for all the remaining conditions. Observe that a linear function is both convex and concave. Also, if a function $f$ is concave, then $\left( {-f}\right)$ is convex, and vice versa.

TABLE 20.2 Subset of KKT Sufficient Conditions

<table><tr><td rowspan="2">Sense of optimization</td><td colspan="4">Required conditions</td></tr><tr><td>$f\left( \mathbf{X}\right)$</td><td>${g}_{i}\left( \mathbf{X}\right)$</td><td>${\lambda }_{i}$</td><td></td></tr><tr><td>Maximization</td><td>Concave</td><td></td><td>$\geq  0$ <br> $\leq  0$ <br> Unrestricted</td><td>$\left( {1 \leq  i \leq  r}\right)$ <br> $\left( {r + 1 \leq  i \leq  p}\right)$ <br> $\left( {p + 1 \leq  i \leq  m}\right)$</td></tr><tr><td>Minimization</td><td>Convex</td><td>$\left\{  \begin{array}{l} \text{ Convex } \\  \text{ Concave } \\  \text{ Linear } \end{array}\right.$</td><td>$\leq  0$ <br> $\geq  0$ <br> Unrestricted</td><td>$\left( {1 \leq  i \leq  r}\right)$ <br> $\left( {r + 1 \leq  i \leq  p}\right)$ <br> $\left( {p + 1 \leq  i \leq  m}\right)$</td></tr></table>

## Example 20.2-5

Consider the following minimization problem:

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = {x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = 2{x}_{1} + {x}_{2} - 5 \leq  0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = {x}_{1} + {x}_{3} - 2 \leq  0
$$

$$
{g}_{3}\left( \mathbf{X}\right)  = 1\; - {x}_{1}\; \leq  0
$$

$$
{g}_{4}\left( \mathbf{X}\right)  = 2\; - {x}_{2}\; \leq  0
$$

$$
{g}_{5}\left( \mathbf{X}\right)  = \; - {x}_{3}\; \leq  0
$$

This is a minimization problem, hence $\mathbf{\lambda } \leq  \mathbf{0}$ . The KKT conditions are thus given as

$$
\left( {{\lambda }_{1},{\lambda }_{2},{\lambda }_{3},{\lambda }_{4},{\lambda }_{5}}\right)  \leq  \mathbf{0}
$$

$$
\left( {2{x}_{1},2{x}_{2},2{x}_{3}}\right)  - \left( {{\lambda }_{1},{\lambda }_{2},{\lambda }_{3},{\lambda }_{4},{\lambda }_{5}}\right) \left( \begin{array}{rrr} 2 & 1 & 0 \\  1 & 0 & 1 \\   - 1 & 0 & 0 \\  0 &  - 1 & 0 \\  0 & 0 &  - 1 \end{array}\right)  = 0
$$

$$
{\lambda }_{1}{g}_{1} = {\lambda }_{2}{g}_{2} = \cdots  = {\lambda }_{5}{g}_{5} = 0
$$

$$
\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}
$$

These conditions reduce to

$$
{\lambda }_{1},{\lambda }_{2},{\lambda }_{3},{\lambda }_{4},{\lambda }_{5} \leq  0
$$

$$
2{x}_{1} - 2{\lambda }_{1} - {\lambda }_{2} + {\lambda }_{3} = 0
$$

$$
2{x}_{2} - {\lambda }_{1} + {\lambda }_{4} = 0
$$

$$
2{x}_{3} - {\lambda }_{2} + {\lambda }_{5} = 0
$$

$$
{\lambda }_{1}\left( {2{x}_{1} + {x}_{2} - 5}\right)  = 0
$$

$$
{\lambda }_{2}\left( {{x}_{1} + {x}_{3} - 2}\right)  = 0
$$

$$
{\lambda }_{3}\left( {1 - {x}_{1}}\right)  = 0
$$

$$
{\lambda }_{4}\left( {2 - {x}_{2}}\right)  = 0
$$

$$
{\lambda }_{5}{x}_{3} = 0
$$

$$
2{x}_{1} + {x}_{2} \leq  5
$$

$$
{x}_{1} + {x}_{3} \leq  2
$$

$$
{x}_{1} \geq  1,{x}_{2} \geq  2,{x}_{3} \geq  0
$$

The solution is ${x}_{1} = 1,{x}_{2} = 2,{x}_{3} = 0,{\lambda }_{1} = {\lambda }_{2} = {\lambda }_{5} = 0,{\lambda }_{3} =  - 2,{\lambda }_{4} =  - 4$ . Because both $f\left( \mathbf{X}\right)$ and the solution space $\mathbf{g}\left( \mathbf{X}\right)  \leq  \mathbf{0}$ are convex, $L\left( {\mathbf{X},\mathbf{S},\mathbf{\lambda }}\right)$ must be convex, and the resulting stationary point yields a global constrained minimum. The KKT conditions are central to the development of the nonlinear programming algorithms in Chapter 21.

## BIBLIOGRAPHY

Bazarra, M., H. Sherali, and C. Shetty, Nonlinear Programming Theory and Algorithms, 3rd ed., Wiley, New York, 2006.

Beightler, C., D. Phillips, and D. Wilde, Foundations of Optimization, 2nd ed., Prentice Hall, NJ, 1979.

Bertsekas, D., Nonlinear Programming, 2nd ed., Athena Scientific, NH, 1999.

Fletcher, R., Practical Methods of Optimization, 2nd ed., Wiley, New York, 2000.

Taha, H. and G. Curry, "Classical Derivation of the Necessary and Sufficient Conditions for Optimal Linear Programs," Operations Research, Vol. 19, No. 4, pp. 1045-1049, 1971.

## PROBLEMS

<table><tr><td>Section</td><td>Assigned Problems</td></tr><tr><td>20.1.1</td><td>20-1 to 20-4</td></tr><tr><td>20.1.2</td><td>20-5 to 20-6</td></tr><tr><td>20.2.1</td><td>20-7 to 20-16</td></tr><tr><td>20.2.2</td><td>20-17 to 20-21</td></tr></table>

20-1. Determine the extreme points of the following functions:

*(a) $f\left( x\right)  = {x}^{3} + x$

*(b) $f\left( x\right)  = {x}^{4} + {x}^{2}$

(c) $f\left( x\right)  = 4{x}^{4} - {x}^{2} + 5$

(d) $f\left( x\right)  = {\left( 3x - 2\right) }^{2}{\left( 2x - 3\right) }^{2}$

*(e) $f\left( x\right)  = 6{x}^{5} - 4{x}^{3} + {10}$

20-2. Determine the extreme points of the following functions:

(a) $f\left( \mathbf{X}\right)  = {x}_{1}^{3} + {x}_{2}^{3} - 3{x}_{1}{x}_{2}$

(b) $f\left( \mathbf{X}\right)  = 2{x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2} + 6\left( {{x}_{1} + {x}_{2} + {x}_{3}}\right)  + 2{x}_{1}{x}_{2}{x}_{3}$

20-3. Verify that the function

$$
f\left( {{x}_{1},{x}_{2},{x}_{3}}\right)  = 2{x}_{1}{x}_{2}{x}_{3} - 4{x}_{1}{x}_{3} - 2{x}_{2}{x}_{3} + {x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2} - 2{x}_{1} - 4{x}_{2} + 4{x}_{3}
$$

has the stationary points $\left( {0,3,1}\right) ,\left( {0,1, - 1}\right) ,\left( {1,2,0}\right) ,\left( {2,1,1}\right)$ , and $\left( {2,3, - 1}\right)$ . Use the sufficiency condition to identify the extreme points.

*20-4. Solve the following simultaneous equations by converting the system to a nonlinear objective function with no constraints:

$$
{x}_{2} - {x}_{1}^{2} = 0
$$

$$
{x}_{2} - {x}_{1} = 2
$$

[Hint: $\min {f}^{2}\left( {{x}_{1},{x}_{2}}\right)$ occurs at ${f}^{\prime }\left( {{x}_{1},{x}_{2}}\right)  = 0$ .]

20-5. Use NewtonRaphson.xls to solve Problem 20-1(c).

20-6. Solve Problem 20-2(b), by the Newton-Raphson method.

20-7. Consider Example 20.2-1.

(a) Compute ${\partial }_{c}f$ by the two methods presented in the example, using $\partial {x}_{2} = {.001}$ instead of $\partial {x}_{2} = {.01}$ . Does the effect of linear approximation become more negligible with the decrease in the value of $\partial {x}_{2}$ ?

*(b) Specify a relationship among the elements of $\partial \mathbf{X} = \left( {\partial {x}_{1},\partial {x}_{2},\partial {x}_{3}}\right)$ at the feasible point ${\mathbf{X}}_{0} = \left( {1,2,3}\right)$ that will keep the point ${\mathbf{X}}_{0} + \partial \mathbf{X}$ feasible.

(c) If $\mathbf{Y} = \left( {{x}_{2},{x}_{3}}\right)$ and $\mathbf{Z} = {x}_{1}$ , what is the value of $\partial {x}_{1}$ that will produce the same value of ${\partial }_{c}f$ given in the example?

20-8. Suppose that Example 20.2-2 is solved in the following manner. First, use the constraints to express ${x}_{1}$ and ${x}_{2}$ in terms of ${x}_{3}$ ; then use the resulting equations to express the objective function in terms of ${x}_{3}$ only. By taking the derivative of the new objective function with respect to ${x}_{3}$ , we can determine the points of maxima and minima.

(a) Would the derivative of the new objective function (expressed in terms of ${x}_{3}$ ) be different from that obtained by the Jacobian method?

(b) How does the suggested procedure differ from the Jacobian method?

20-9. Apply the Jacobian method to Example 20.2-1 by selecting $\mathbf{Y} = \left( {{x}_{2},{x}_{3}}\right)$ and $\mathbf{Z} = \left( {x}_{1}\right)$ .

*20-10. Solve by the Jacobian method:

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = \mathop{\sum }\limits_{{i = 1}}^{n}{x}_{i}^{2}
$$

subject to

$$
\mathop{\prod }\limits_{{i = 1}}^{n}{x}_{i} = C
$$

$C$ is a positive constant. Suppose that the right-hand side of the constraint is changed to $C + \delta$ , where $\delta$ is a small positive quantity. Find the corresponding change in the optimal value of $f$ .

20-11. Solve by the Jacobian method:

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = 5{x}_{1}^{2} + {x}_{2}^{2} + 2{x}_{1}{x}_{2}
$$

subject to

$$
g\left( \mathbf{X}\right)  = {x}_{1}{x}_{2} - {10} = 0
$$

(a) Find the change in the optimal value of $f\left( \mathbf{X}\right)$ if the constraint is replaced by ${x}_{1}{x}_{2} - {9.99} = 0.$

(b) Find the change in value of $f\left( \mathbf{X}\right)$ in the neighborhood of the feasible point $\left( {2,5}\right)$ , given that ${x}_{1}{x}_{2} = {9.99}$ and $\partial {x}_{1} = {.01}$ .

20-12. Consider the problem:

$$
\text{ Maximize }f\left( \mathbf{X}\right)  = {x}_{1}^{2} + 2{x}_{2}^{2} + {10}{x}_{3}^{2} + 5{x}_{1}{x}_{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1} + {x}_{2}^{2} + 3{x}_{2}{x}_{3} - 5 = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = {x}_{1}^{2} + 5{x}_{1}{x}_{2} + {x}_{3}^{2} - 7 = 0
$$

Apply the Jacobian method to find $\partial f\left( \mathbf{X}\right)$ in the neighborhood of the feasible point $\left( {1,1,1}\right)$ . Assume that this neighborhood is specified by $\partial {g}_{1} =  - {.01},\partial {g}_{2} = {.02}$ , and $\partial {x}_{1} = {.01}$

20-13. Consider the problem

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = {x}_{1}^{2} + {x}_{2}^{2} + {x}_{3}^{2} + {x}_{4}^{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1} + 2{x}_{2} + 3{x}_{3} + 5{x}_{4} - {10} = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = {x}_{1} + 2{x}_{2} + 5{x}_{3} + 6{x}_{4} - {15} = 0
$$

(a) Show that by selecting ${x}_{3}$ and ${x}_{4}$ as independent variables, the Jacobian method fails to provide a solution and state the reason.

*(b) Solve the problem using ${x}_{1}$ and ${x}_{3}$ as independent variables, and apply the sufficiency condition to determine the type of the resulting stationary point.

(c) Determine the sensitivity coefficients, given the solution in (b).

20-14. Solve the following linear programming problem by both the Jacobian and the Lagrangean methods:

$$
\text{ Maximize }f\left( \mathbf{X}\right)  = 5{x}_{1} + 3{x}_{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1} + 2{x}_{2} + {x}_{3}\; - 6 = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = 3{x}_{1} + {x}_{2}\; + {x}_{4} - 9 = 0
$$

$$
{x}_{1},{x}_{2},{x}_{3},{x}_{4} \geq  0
$$

*20-15. Find the optimal solution to the problem

$$
\text{ Minimize }f\left( \mathbf{X}\right)  = {x}_{1}^{2} + 2{x}_{2}^{2} + {10}{x}_{3}^{2}
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  = {x}_{1} + {x}_{2}^{2} + {x}_{3} - 5 = 0
$$

$$
{g}_{2}\left( \mathbf{X}\right)  = {x}_{1} + 5{x}_{2} + {x}_{3} - 7 = 0
$$

Suppose that ${g}_{1}\left( \mathbf{X}\right)  = {.01}$ and ${g}_{2}\left( \mathbf{X}\right)  = {.02}$ . Find the corresponding change in the optimal value of $f\left( \mathbf{X}\right)$ .

20-16. Solve Problem 20-13, by the Lagrangean method, and verify that the values of the Lagrange multipliers are the same as the sensitivity coefficients obtained in Problem 20-13.

20-17. Consider the problem:

$$
\text{ Maximize }f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  \geq  0
$$

Show that the KKT conditions are the same as in Section 20.2.2, except that $\mathbf{\lambda } \leq  \mathbf{0}$ .

20-18. Consider the following problem:

$$
\text{ Maximize }f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  = 0
$$

Show that the KKT conditions are

$$
\nabla f\left( \mathbf{X}\right)  - \mathbf{\lambda }\nabla \mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

$$
\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

λ unrestricted in sign

20-19. Write the KKT necessary conditions for the following problems:

(a) Maximize $f\left( \mathbf{X}\right)  = {x}_{1}^{3} - {x}_{2}^{2} + {x}_{1}{x}_{3}^{2}$ subject to

$$
{x}_{1} + {x}_{2}^{2} + {x}_{3} = 5
$$

$$
5{x}_{1}^{2} - {x}_{2}^{2} - {x}_{3} \geq  2
$$

$$
{x}_{1},{x}_{2},{x}_{3} \geq  0
$$

(b) Minimize $f\left( \mathbf{X}\right)  = {x}_{1}^{4} + {x}_{2}^{2} + 5{x}_{1}{x}_{2}{x}_{3}$

subject to

$$
{x}_{1}^{2} - {x}_{2}^{2} + {x}_{3}^{3} \leq  {10}
$$

$$
{x}_{1}^{3} + {x}_{2}^{2} + 4{x}_{3}^{2} \geq  {20}
$$

20-20. Consider the problem

$$
\text{ Maximize }f\left( \mathbf{X}\right)
$$

subject to

$$
\mathbf{g}\left( \mathbf{X}\right)  = \mathbf{0}
$$

Given $f\left( \mathbf{X}\right)$ is concave and ${g}_{i}\left( \mathbf{X}\right) \left( {i = 1,2,\ldots , m}\right)$ is a linear function, show that the KKT necessary conditions are also sufficient. Is this result true if ${g}_{i}\left( \mathbf{X}\right)$ is a convex nonlinear function for all $i$ ? Why?

20-21. Consider the problem

$$
\text{ Maximize }f\left( \mathbf{X}\right)
$$

subject to

$$
{g}_{1}\left( \mathbf{X}\right)  \geq  0,{g}_{2}\left( \mathbf{X}\right)  = 0,{g}_{3}\left( \mathbf{X}\right)  \leq  0
$$

Develop the KKT conditions, and give the stipulations under which the conditions are sufficient.