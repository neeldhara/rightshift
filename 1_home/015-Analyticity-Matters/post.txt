Title: Analyticity Matters
----
Author: Dileep
----
Date: November 2nd, 2009
----
Tags: all analytic balki complex contour differential equation integral math power-series rubel
----
Text:
Ever since [KVM posted his dissection of Rubel's UDE paper](http://mohankv.blogspot.com/2009/10/understanding-rubels-universal.html), I've been wanting to address this issue he raised:

> I'm still amazed and can't quite fully digest the fact that a perfectly smooth function can be non-analytic. I mean, consider the $\exp(-1/x)$ function. If you stand at the origin, you have no clue what happens as you step forward! All the meters in your car will read zero at the origin, and yet, somehow the function bootstraps itself into rising! This never happens with analytic functions!

The function he was talking about is not $\exp(-1/x)$ per se, but 


$$
f(x) =
\begin{cases}e^{\frac{-1}{x}} & \mbox{if}\quad x>0 \cr
0 & \mbox{if}\quad x\leq 0 \end{cases}
$$

He goes on to plot it as so: 

(image: plot.png width: 600)

At first sight, defining a function differently for negative and positive x, and then expecting civilised behaviour felt like cheating to me. After all, $\exp(-1/x)$ is singular as $x \rightarrow 0^{-}$. But that doesn't make his comment any less rich, as one is lead to believe that $C^{\infty}$-continuity is more sacred than that. While this post doesn't solve anything, it notices some interesting patterns and compiles them all in one place, and provides for a sweet link next time the reader is having to explain this to someone over the internet. So lets see how far we can get. 


**The Power Series Expansion:** 

I'll confine myself to basic high-school math, so the learning curve is analytic for all readers. 

For the uninitiated (I love that word), any function $f(x)$ that is said to be "analytic" (we'll get to that before this post ends), can be expanded as a power series in $x$, about a point $x\_{o}$ like so: 

$${f(x)} = {f(x\_{o})} + \sum\_{n=1}^{\infty}{{c\_{n}}{(x-x\_{o})}^{n}},$$ 

where $c\_{n} = \frac{f^{(n)}(x\_{o})}{n!}$, the $n^{th}$ derivative of the function at $x\_{o}$, scaled down by $n$ factorial. Since the same function can be translated along the x-axis, we'll stick to Taylor expansions about the origin for all our derivations. 

This has an interesting consequence. A general single-valued function with no strings attached, in order to be completely defined, will require us to specify the value of the function at an uncountably infinite number of points on the x-axis, no matter how small the domain (as long as it is not a collection of isolated points). However, analytical functions require only that we specify one set of countably infinite values (all derivatives at any one point within every simply connected part of the domain). This is a drastic reduction. No doubt, the compression of parameter space is stronger than what that mere $C^{\infty}$ continuity condition imposes. Apparently, for every function representable by a power series, uniformity of convergence ensures integrability and differentiability. If you've understood that, than stop reading further and do more productive things with your life. 

**Convergence and Analyticity:** 

Let us examine the importance of the word 'domain' with a few basic examples. Now, the KVM function involves stitching two separate domain definitions, so we'll start with simpler functions. Take for example, the infinite sum of the following geometric series: 

$${1}/{1-x} = 1 + x + {x^{2}} + {x^{3}} + {x^{4}} + .... $$

The right-hand side is the Taylor expansion about the origin, where the $n^{th}$ derivative of $\frac{1}{1-x}$ is $n!$. Clearly, a geometric series can only converge if the multiplicative factor $x$ is less than $1$ in magnitude. So this expansion diverges for $x \geq 1$ .This is no surprise, as the $\frac{1}{1-x}$ blows up at $x=1$, and one can expect the characteristics of functional derivatives on one side to have little effect on the other side of this singular point (probably why physicists can't define a "before the big-bang" universe). A good analogy is the vibration of a constrained string. A string held put at a point can only vibrate in modes which have a node at that point. But if we clamp down (up?) all the derivatives of the string at that point, then excitations from one side cannot travel to the other. If one were to expand $\frac{1}{1-x}$ as a power series about some other point greater than one, it would be valid for all $x>1$. So we seem to have arrived at some sort of definition for the boundary of a domain. After all, $\frac{1}{1-x}$ is merely $\frac{1}{x}$ shifted and flipped. But there is an anomaly. 

It turns out that this expansion also diverges for $x \leq -1$. Highly unexpected, as $\frac{1}{1-x}$ seems to have no bumps, kinks or black holes around $-1$. Funky behaviour on one side of the point of expansion seems to be affecting the symmetrically opposite point on the other side. The string has strings attached? Say we parity flip the function and expand again about the origin: 

$$\frac{1}{1+x} = 1 - x + {x^{2}} - {x^{3}} + {x^{4}} - ....$$ 

This again is singular at $x=-1$, but the expansion diverges for both $x \leq -1$, and $x \geq 1$. 

Note that the two expansions are interconvertible. One is generated by flipping the signs of all alternate terms in the other. Now we invoke the concept of conditional vs. absolute convergence of a power series. 

An infinite series $\sum\_{n=1}^{\infty}a\_{n}$ tends to converge to a finite value if successive terms $a\_{i}$ fall off fast enough as $i$ increases. Sometimes, the signs of the terms help the convergence by cancellation. But the series is said to be absolutely convergent (as opposed to conditionally convergent) if the fall off in successive term magnitude is so fast that $\sum\_{n=1}^{\infty}\vert a\_{n} \vert$ is convergent. Absolute convergence implies conditional convergence. But conditional convergence does not imply absolute convergence. Take for example the harmonic series $1 + {{1}/{2}} + {{1}/{3}} + {{1}/{4}} ....$. It is provably divergent. But if we flip the sign of every even term, the resulting series converges to $log(2)$. Series with alternating signs have added help at hand, as all they require is for the absolute values of successive terms $\vert a\_{i} \vert$ to tend monotonically to $0$. None of this helps our case. We are looking for conditional vs. absolute divergence relations. Take the series $\sum\_{n=1}^{\infty}a\_{n}$. Denote the positive terms by $p\_{1}, p\_{2}, p\_{3}, ....$, and the negative terms by $-q\_{1}, -q\_{2}, -q\_{3}, ....$. Then the absolute sum is $\sum\_{\nu = 1}^{\infty}p\_{\nu} + \sum\_{\nu = 1}^{\infty}q\_{\nu}$, and the conditional sum is $\sum\_{\nu = 1}^{\infty}p\_{\nu} - \sum\_{\nu = 1}^{\infty}q\_{\nu}$. For absolutely convergent series, both the sum of positive terms and the sum of negative terms need to be convergent. For conditional convergence, both have to be divergent. For our power series expansions, both positive term sums and negative term sums have to converge inside the domain. Only one of them needs to diverge outside the domain. As an aside, the sum of conditionally convergent series can be changed by suitable rearrangement of the terms of the series, and it can even be made to diverge. This is not possible for absolutely convergent series.

So, what is the biggest generalisation we can make thus far? If a power series in $x$ converges for a value $x = \xi$, it converges absolutely for every value x such that $\vert x \vert < \vert\xi\vert$, and the convergence is uniform in every interval $\vert x \vert \le \eta$, where $\eta$ is any positive number less than $\vert\xi\vert$. $\eta$ may lie as near $\vert\xi\vert$ as we please (in an $\epsilon,\delta$ sense). This magically implies that, If $\exists x = \xi$ such that the power series diverges, then it must diverge for every value of $x$ such that $\vert x \vert > \vert\xi\vert$. This defines an "interval of convergence", centered about the point of expansion for the power series. Since the KVM function $\exp(-1/x)$ has a singularity at $x \rightarrow {0^{-}}$, it's interval of convergence for an expansion about the origin has size zero. This still doesn't seem to demystify the stitched function weirdness. 

**So What Is All This Analyticity Stuff??** 

So why is analyticity a stronger constraint than $C^{\infty}$ continuity? What other conditions does it impose on the countably infinite derivatives required to completely specify the function? It is worthwhile to recall that in calculus, the differential element $dx$ of the independent variable is a linear term in x. Often in analysis and perturbation theory, we've neglected terms with higher-order powers and managed to retain accuracy of our results. So a power series expansion of a function about a point to a very good accuracy, can be approximated by a finite degree polynomial, in a neighbourhood about that point, whose size is dependent on the desired error tolerance. This means, for an ultra-small neighbourhood, the function is a straight line. In a slightly larger, say mega-small, neighbourhood, it is a parabola, and so on. If we differentiate a power series any number of times, we again end up with a power series. So this property is not only shared by the function, but also by all its other derivatives. Say a function $f(x)$ has a zero of order $r$ at $x=a$, ${{f^{(r)}}{(a)}} \ne 0$. Then the function may be expressed as ${f(x)} = {{(x-a)}^{r}}{g(x)}$, with ${g(a)} = {f^{(r)}{(a)}}/r!$. $g(x)$ cannot vanish in a suitably small neighbourhood of $x=a$, or, the zeros of $f(x)$ are "isolated", unless of course $f$ vanishes identically. The same is true for $f'(x)$. It follows that in a finite interval an analytical function (and all its derivatives) is (are) piecewise monotone(s), that is, it (they) cannot change its (their) character of monotonicity infinitely often. As a counter-example, consider the Taylor expansion of $sin({1}/{x})$. This tends to wildly oscillate as $x$ approaches $0$. It crosses the x-axis infinitely many times in any finite interval about the origin. So the zeros at the origin can't be said to be isolated. 


(image: sin1.jpg width: 800)

**Complexity Matters:** 

So far, we seemed to have managed quite well on the real number line. Here comes the bomb: Taylor expansions of:

$$\frac{1}{1+x^{2}} = 1 - x^{2} + x^{4} - x^{6} + ....$$

or

$${tan^{-1}(x)} = x - {\frac{x^{3}}{3}} + {\frac{x^{5}}{5}} - ....$$

These expansions also diverge for $\vert x \vert >1$, despite the functions themselves being well-behaved at $\vert x \vert=1$. ${WTF}^{\infty}$.

It turns out that complex domain is more natural than its real subset. We note that both $\frac{1}{1+x^{2}}$ and the expansion of $tan^{-1}(x)$ diverge at $x=\pm i$, where $i = \sqrt{-1}$. Note that the real part of the first function blows up, but for the second function, its the imaginary part that does so. If we are willing to extend the power series expansion to complex variables, then we'll have to upgrade our interval of convergence to circle of convergence. This would mean that if $f(x)$ is singular at complex point $z\_{1}$, then its power series expansion about the origin definitely diverges for points farther than $z\_{1}$ on the complex domain. Take the function $e^{{-1}/{x^{2}}}$, which is quite close to the KVM function. All its derivatives vanish at $x=0$. So we cannot expand it in a power series about the origin because $e^{{-1}/{(ix)^{2}}}$ diverges on the imaginary axis as it tends toward the origin.

(image: exp1.jpg width: 800)


An arbitrary point $z$ on the complex plane may be defined as $z=re^{i \theta}$. Then, ${z^{n}} = {r^{n}}{e^{i n \theta}} = {r^{n}}{\cos(n \theta)} + i {r^{n}}{\sin(n \theta)}$. A singularity at some point $z\_{1}$ affects the function expansion everywhere on the circle $\vert z \vert = \vert z\_{1}\vert$. The vibrating string has become a 2D membrane. And if all derivatives of the membrane are clamped at some point, then radial (and angular?) excitations from the origin cannot travel beyond the circle centred at the origin, with the clamped point on its circumference. [HSR](http://www.ee.iitm.ac.in/user/hsr/) once remarked that the EE department at IITM wrongfully exposes its students to Fourier and Laplace transforms before the concept of analytical functions has been taught. Electrical engineers who have studied filter design should recall all those conditions for "poles lying on the left half-plane" or "outside the unit circle", and reinterpret them in the present context.

(image: complex_plane.jpg width: 600)

This domain extension works wonders to our compression ratio discussion. It allows us to reduce the task of function definition from specifying two values at every point on a 2D region to specifying twice (hehe) countably infinite derivatives (real and imaginary) at any one point. There is a strange interplay between real and complex values of the power series expansion of any analytical function, that transcends the absolute vs. conditional convergence picture.

$${(-1)^{n}}{z^{n}} = {(-r)^{n}}{e^{i n \theta}} = {(-1)^{n}}{r^{n}}{\cos(n \theta)} + i {(-1)^{n}}{r^{n}}{\sin(n \theta)}$$
$${(z^{\ast})^{n}} = {r^{n}}{e^{-i n \theta}} = {r^{n}}{\cos(n \theta)} + i {(-1)^{n}}{r^{n}}{\sin(n \theta)}$$

The cosine and sine functions scale the magnitudes of the real and imaginary values and affect the signs of terms depending on $n \theta$. It might be worthwhile to see how a rotation transform affects power series expansions. It is interesting that complex analysis turned out to be so fundamental to our understanding of seemingly trivial math. The Euler exponential notation was more than a calculation and expression aid. And we didn't even need quantum mechanics! All of it has much to do with the fact that on a line, there are 2 sides to a point. There are two signs, + and -, as there are 2 kinds of electromagnetic charges. Hence the 2D domain. And a set of two harmonically conjugate solutions for the Laplacian. There cannot be a further extension of the complex domain to higher dimensions in quite the same way real was extended to complex (a la Algebraically closed fields). This was the triumph of 19th century mathematics, when rigour was born. The number 2 was found be holy. 

**Aside:** 

Parity is a discrete transformation. However, in relativistic quantum mechanics, while studying chiral symmetry of Dirac particles, a parity flip is modelled as a continuous transformation using the pseudo-scalar ${\gamma\_{5}}$ matrix as a generator of rotations on a complex plane. The wavefunction transforms as $\psi \rightarrow {e^{i \theta \gamma\_{5}}} \psi$, and an operator $\hat{H} \rightarrow {e^{i \theta \gamma\_{5}}} \hat{H} {e^{-i \theta \gamma\_{5}}}$. Also, in QED, in perturbative expansions of charge conjugation symmetric processes (like electron-positron annihilation), the observable cannot depend on sign of charge. So it is a power series in $e^{2}$, or $\alpha$, the fine structure constant. But in a universe where $\alpha < 0$, like charges will attract and opposite charges will repel. This is very unstable, as the only ground-state is two oppositely charged black-holes at infinite distance from eachother. So, if $\alpha$ could take values on a complex plane, then all negative real values are a no-no. So there is a branch cut on the complex plane all along the negative real axis, implying that the radius of convergence of a power series expansion in $\alpha$ about the origin is zero. So even though $\alpha$ is very small, the series don't converge. They just happen to be "asymptotic" series, which allows physicists to do some amount of close approximation to physics. Now you know why even theoretically computed physical values (like masses) have a computable error bound, and the number of significant digits keep increasing every year.

**The Search for Hidden Redundancies:** 

The definition of analytical functions on the complex plane is generally made using the Cauchy-Riemann differential equations. However, Weierstrass is said to have developed the theory of complex analysis from scratch from the point of view of power series expansions. That derivation seems lost to the pages of history written in European languages. Let us see how much further we can explore the compression ratio aspects and built-in redundancies in function definition by specification of parameters. So in a domain where a complex function is analytic (i.e. differentiable in an $\epsilon$-$\delta$ limit sense), integration along any closed contour vanishes. But what if we introduce a simple pole (singularity) in the function $f(t)$ at the point $z$ and compute the contour integral around it. We have,

$${f(z)} = {\frac{1}{(2\pi i)}}{\int\limits_{C}}{\frac{f(t)}{t-z}}{dt}= {\frac{1}{(2\pi)}}\int\limits_0^{2\pi}{f(z+re^{i\theta})}{d\theta}$$

In the region of analyticity, the value of a function is the average of its value in the neighbourhood of the point in question (see how this is true for real functions defined on the real line). Does this also imply that the solution to a Laplacian differential equation is unique if the boundary conditions are fixed? That is a reduction from specifying function values on a 2D domain to specifying on a 1D contour. And since it is analytic along the contour loop, it can be parameterised again by coefficients of angular basis functions, this reducing further into countably infinite space. Every analytical function can be expanded as a power series. If we introduce slightly sharper poles at points and compute contour integrals around them, we have:

$$\frac{f^{(\nu)}(z_{o})}{\nu !}= {\frac{1}{(2\pi i)}}\int\limits_C{\frac{f(z_o+t)}{t^{\nu+1}}}dt = \frac{1}{(2\pi)}\int\limits_0^{2\pi}\frac{f(z_o+re^{i\theta})}{r^{\nu+1}}e^{-i(\nu+1)\theta}d\theta$$

The contour integral seems to circle the point $( \nu +1)$ times clockwise, to yield the $ {\nu}^\text{th}$ derivative of the function. Note that in the power series expansion, the $n^\text{th}$ term (${z^{n}}={r^{n}}{e^{i n \theta}}$) also circles a closed contour n times (anti-clockwise, as if to unwind the derivative coefficient). The complex plane comes with strings attached, since every point has a build-in multiplicity (there are $n$ solutions to $z^{n}=\text{constant}$). Inverting a function converts poles to zeros and vice versa. Do you see how that affects regions of power series convergence? If $f(z)$ has an $n^{th}$ order zero at $z\_{o}$, then it is expressible as ${f(z)} = {(z-z\_{o})^{n}}{g(z)}$, where $g(z\_{o}) \ne 0$. The inverse function ${1}/{f(z)} = q(z) = {h(z)}/{(z-z\_{o})^{n}}$ ($h(z)$ is analytic in the neighbourhood of $z\_{o}$), can be expanded as,

$$q(z) = {c\_{-n}}{(z-z\_{o})^{-n}} + .... + {c\_{-1}}{(z-z\_{o})^{-1}} +{ c\_{0}} + {c\_{1}}{(z-z\_{o})} + ....$$

A contour integral of negative index terms of $q(z)$ around $z\_{o}$ gives $2 \pi {c\_{-1}}$, and the higher negative power terms vanish. The residue of a function at a pole is therefore $2 \pi {c\_{-1}}$. The theorem of residues, which best illustrates the information compression ratio, states that if a function $f(z)$ is analytic in the interior of a region R and on its boundary C except at a finite number of interior poles, the integral of the function taken around C in the positive sense is equal to the sum of the residues of the function at the poles enclosed by the boundary C. 

**So Why Power Series??** 

Consider the polynomial expression,

$${a\_{0}} + {a\_{1}}{z} + {a\_{2}}{z^{2}} + .... + {a\_{n}}{z^{n}} = {P(z)}$$

For some real parameter $t$, take the integral along any closed path C in the z-plane, which does not pass through any of the zeros of $P(z)$,

$$u(t) = \oint\limits_{C}{\frac{e^{tz}f(z)}{P(z)}{dz}}$$

Let $f(z)$ be a constant or any polynomial in z, of a degree we shall assume to be less than $n$, so that the integrand behaves well at infinity. The successive derivatives of $u(t)$ with respect to $t$ under the integral sign is equivalent to multiplication of the integrand by $z, {z^{2}}, {z^{3}}, ....$ as the case may be. If we now form the differential expression $L{[}{u}{]} = {a\_{0}}{u} + {a\_{1}}{{du}/dt} + {a\_{2}}{{{d}^{2}u}/{dt^{2}}} + .... + {a\_{n}}{{{d}^{n}u}/{dt^{n}}}$, or in symbolic operator notation, $P(D)u$, we have,

$$P(D)u = L{[}{u}{]} = \oint{C}{}{{e^{tz}}{f(z)}{dz}} = 0$$

So $u(t)$ is a solution for the differential equation $P(D)u = 0$, and the $n$ arbitrary constants from the polynomial $f(z)$ are the constants of integration. Most differential equations engineers and scientists study can be constructed out of polynomial type operators. If ${a\_{o}} \ne 0$,

$$\frac{1}{a_0 + a_1 t + a_2 t^2 + .... + a_n t^n} = b_0 + b_1 t + b_2 t^2 + ....$$

then the solution of

$$a_0 u + a_1 \frac{du}{dx} + a_2 \frac{d^2 u}{dx^2} + .... + a_n \frac{d^n u}{dx^n} = R(x)$$

is,

$$u(x) = b_0 R(x) + b_1 \frac{dR(x)}{dx} + b_2 \frac{d^2 R(x)}{dx^2} + ....$$

and if $a\_{0}=0$ but $a\_{1} \ne 0$,

$$\frac{1}{a_1 t + a_2 t^2 + .... + a_n t^n} = b t^{-1} + b_0 + b_1 t + b_2 t^2 + ....$$

and,

$$u(x) = b \int R(x)dx + b_0 R(x) + b_1 \frac{dR(x)}{dx} + b_2 \frac{d^2 R(x)}{dx^2} + ....$$

[Balki](https://www.iitm.ac.in/info/fac/vbalki) once claimed that if all of Calculus had to be summed up in one single useful sentence, it would read, "An exponential grows faster than a polynomial, which grows faster than a logarithm". The definition of a differential element as a linear increment of the independent variable, and the practice of solving polynomial operator type differential equations, has lead to the extensive use of power series in analysing mathematics, instead of other types of expansions. However, linear diffential operators of infinite order, like the time evolution operator in Quantum mechanics, and the generator formalism for infinitesimal transformations have been explored as well. As for the KVM function, every derivative at $x = 0^{+}$ vanishes because they are all products of a diverging polynomial factor and a converging (vanishing) exponential factor. If one were to blindly Taylor-expand the function about the origin, all the polynomial factors from all the terms will seem to add up to something formidable, even compared to the common vanishing exponential factor. The ${\infty}^\text{th}$ derivative does seem to be of order $ \infty $!, although understandably indecisive about its sign. 

**[BLINK] Plugin missing :(** 

We started by stating that analytical functions can be at worst specified uniquely by a countably infinite number of parameters. In the power series expansion notation, these parameters turned out to be successive derivatives of the function at a point. However, from early lessons in probability density function theory, one may recall a similar set of parameters which are defined by the integration operator. A function on the real number line could well be uniquely specified by its mean, variance, and all the higher moments $\int{}{}{{(x-x\_{o})^{n}}{f(x)}{dx}}$ about any point. I wonder how this would translate to the complex plane, since analyticity doesn't seem to play a role at first glance (but normalizability matters . . . . a lot . . . ). This might hint at the duality between differential equations and Lagrangian formalisms. Are the invariant constants dictated by Noether's theorem applied to the Lagrangian formalism directly related to the constants of integration arising from the differential equation formalism? Karthik's next post promises to enlighten us regarding some aspects of this. 

**Epistemology, and the possible non-futility of Modelling:** 

KVM's Rubel post was preceded by his disdain for all modelling. However, one must ask what it truly means to have understood a phenomena, as opposed to having merely "modelled" it. All our analysis seem to be restricted to analytical functions, but they are a small subset of all possible functions. Wiki claims that:

> In a measure-theoretic sense: when the space C([0, 1]; R) is equipped with classical Wiener measure $\gamma$, the collection of functions that are differentiable at even a single point of [0, 1] has $\gamma$-measure zero. The same is true even if one takes finite-dimensional "slices" of C([0, 1]; R): the nowhere-differentiable functions form a prevalent subset of C([0, 1]; R).

How curious, that most natural processes can be easily described by analytical functions alone? Or can they? Aren't singularities our greatest unconquered enemies? In my view, the non-rapid, piecewise monotonic behaviour appeals to an aesthetic sense of the human mind, which has evolved to expect small input changes to have small observable effects, at least in the short run. Are we then destined to know the universe only to a close approximation? Does a mere knowledge of a handful of parameters qualify as knowledge of a process? Is the definition of the class of functions of the solution important? At what point of generalisation does a predictive DE (as defined by KVM) become a shrink DE? Is it NOT amazing that group symmetries helped define previously unobserved fundamental particles in high-energy physics? Is "intuitive feel" all we have? Needless to say, $C^{\infty}$ continuity is yet to be demystified. But I hope I have motivated a domain for analysis. If this entire post is to be condensed into a single valuable sentence, it would read, "2 is a holy number". 

###References:- 

1> Richard Courant, Fritz john, "Introduction to Calculus and Analysis", Vol. I. and II. 

2> My class notes. 

3> Wikipedia 

###Other suggested reading:- 

1> [Balki's arguments for why 3 is a holy number.](http://www.physics.iitm.ac.in/~labs/dynamical/pedagogy/) 

2> Rubel's original paper: Rubel, L. A. **"A Universal Differential Equation."** _Bull. Amer. Math. Soc._ **4**, 345-349, 1981. 

3> [Weierstrass](http://www.gap-system.org/~history/Biographies/Weierstrass.html)'s original unpublished works, if you can find them.

*****

## Old comments from the w0rdpress days

**Kushal said:**
*2 November, 2009 at 7:35 am*

If you keep writing such articles regularly, you will end up publishing a book before you finish your PhD! :-)
