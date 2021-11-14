Title: On Free-Energies and “Higher-Learning”
----
Author: Dileep
----
Date: June 22nd, 2009
----
Tags: all free-energy higher-learning latex legendre-transform statistical-mechanics thermodynamics
----
Text:
_This tiny post was originally conceived to appear in  "**Really Cool Derivations**", the working title for an unpublished study companion meant to pain young upper middle-class students from semi-orthodox Indian families who weren't romantic enough to indulge in the arts and were consequently conscripted into training for entrance exams conducted by elite institutions of "higher-learning". It assumes that the reader  is already familiar with Thermodynamic terminology, and believes in the First Law, among other things._ 

Allow me to guide you through your technical "higher-learning" experience with the following example. You begin by realizing that an easy and efficient way to prepare for IIT-JEE is to memorize a set of equations such as: 

$$\Delta E = T \Delta S - P \Delta V + \mu \Delta N$$

Then, you memorize what name each variable is referred to as. ($ S = $ Entropy, $ \mu = $ Chemical Potential, and so on.) And then, you memorize the "conditions" under which the use of an equation is valid, such as "reversible processes for the above case". Then you look for the same key words in the question being posed, choose the correct equation, plug-in values, and compute some number. Presto, now you are in college, have met some intellectual lecturers and intelligent peers, have been exposed to the larger portion of the real world, have realized that you don't know jack, have a library, the internets, and accessible "consultants" at your disposal, and are suddenly faced with an abundance of free time. And then, you tend to grow a brain. You read somewhere about the First Law of Thermodynamics: 

$$ dQ = dU + dW $$

You learn that $ dU $ is a perfect (exact?) differential, which means that it is path independent. And since this was explicitly mentioned, the others are not (in general). So you painstakingly learn how to compute the others consistently so as not to violate the First Law for a toy problem involving cylinders, pistons and ideal gases. Then you once again encounter entropy and reversible processes, and are tempted to rewrite the First Law like so: 

$$ T dS = dE + P dV - \mu dN $$

This begins to look very familiar. 

Here you learn to define Intensive (or Field) variables and Extensive (or State) variables. You make an analogy to electrodynamics and solid mechanics, where $ \vec{E}, \vec{B} $ and stress would be Intensive and $ \vec{P}, \vec{\mu} $ and strain would be Extensive variables. Then you treat $ T, P, \mu $ as Field variables and $ S, V, N $ as State variables. 

Now you begin to view $ E $ as a sort of "Thermodynamic Potential", for a system in state $ (S,V,N) $. Then define Field variables as: 

$ T = ( {\partial E} / {\partial S} )_{V,N} $ 

$ P = - ( {\partial E} / {\partial V} )_{S,N} $ 

$ \mu = ( {\partial E} / {\partial N} )_{S,V} $ 

Then you cross check your intuitive definitions of the Field variables for consistency. Now you define a "regime of validity" where the state changes are such (slow?, reversible?) that $ E $  behaves as a homogeneous function of the extensive variables. You express the "Thermodynamic Potential" with a bunch of first-order derivative terms, and arrive at the Euler-relation: 

$ E = TS - PV + \mu N $ 

Now in a rather unrelated train of thought, you learn about Legendre transforms. You wiki it. You apply it in Lagrangian Mechanics. You transform a "Lagrangian" $ L(q,dq/dt) $ into a "Hamiltonian" $ H(q,p) $. You notice that the state variables have changed from $ (q,dq/dt) $ to $ (q,p) $. Now, armed with Legendre Transform technology, you begin ravaging the "Thermodynamic Potential" $ E(S,V,N) $ from earlier. You start to derive familiar relics from the past, such as 

Gibb's Free Energy: 

$ G(T,P,N) = E -TS +PV $ 

Helmholtz Free Energy: 

$ F(T,V,N) = E - TS $ 

Entropy: 

$ H(S,P,N) = E+PV $ 

Grand Potential: 

$ \Phi (T,V,\mu) = E - TS - \mu N = -PV $ 

And other strange beasts: 

$ \Phi\_{1}(S,V,\mu) = E - \mu N $ $ \Phi\_{2}(S,P,\mu) = E + PV - \mu N $ 

You revise your list of Field and State variables for each case, and derive their respective "regimes of validity". Suddenly, you realize that all your training has been mathematically consistent and you feel the need to write this down somewhere. And someday you graduate, at which point I stop ranting because I'm yet to experience what comes next. 

Many souls in this age are unfortunate enough to get inducted into over-accelerated education programs hellbent on flooding their minds with advanced sounding semantics and arbitrary logical rules of progression. It appears that "higher-learning" is composed of recursively unlearning and relearning "old" lessons. Its probably a good way to go about it, if each level is viewed as a layer of abstraction (as hinted by fellow co-blogger elsewhere), but one would wish that said fact of abstraction be stressed early enough in place of dogmatic rhetoric, to make the unlearning a little easier. 

@Neels: TeX support test #1, successful. Good job!

* * * * *

## Old comments from the w0rdpress days

**SG said:**
*27 June, 2009 at 12:28 pm*

Hi Dileep,

You can organise all these potentials in a neat fashion. Assign each potential to a face of an octahedron. Each edge connects two faces and represents the Legendre transform. Here is a trick question: there is a problem with one of the faces. Why?

When I write down the first law, I use dbar Q (dbhar is like \hbar which I define in LaTeX) and dbar W to denote that they are not exact differentials.

By the way, your post mirrors part of my lecture on thermodynamics that I given in the middle of my stat mech courses (also Physics III when it existed). You should add the bit on stability — this translates into convexity/concavity conditions on the potentials.

Loved the bit about “And then, you grow a brain”.

SG

**Kushal said:**
*28 June, 2009 at 5:08 am*

What happens after you graduate is that you choose one among the many equations you have mentioned in this blog and decide to spend the rest of your life brooding on it.. :-)

**KVM said:**
*19 September, 2009 at 6:12 pm*

I was about to write about the octahedron of potentials when I saw SG’s comment :) The L corner troubled us for sometime during the Stat Mech course here!

While on the topic, let me put in a shameless plug for some of my thoughts on math. After doing stat mech, I very very strongly think that real analysis and statistics *must* be taught with a stat mech background. Buy two, get one free! I had done the ‘math’ stats before, but the central limit theorem’s true power is restricted to some silly made-up textbook problem. Unleash it on a microcanonical ensemble, and presto! The world is magical again! And probability suddenly becomes infinitely clearer and more fun when you talk of molecules and ensembles instead of sodding card games and multinomial theorems.

And truly, ideas in real analysis like uniform convergence and varying degrees of infinity come out very nicely when you talk of millions of molecules, and then collections of such millions, and so on. And the real goal of any kind of Analysis, real or complex, is measurement. I haven’t come across any other topic where measurement is clearer than in stat mech. Apropos of measurement, here’s a very nice article by Tim Gowers on continuity: http://www.dpmms.cam.ac.uk/~wtg10/continuity.html

If we are taught _why_ epsilons and deltas are necessary and sufficient, and how they evolved from “without lifing pen from paper”, I suspect *everyone* would fall in love with analysis!

**Karthik said:**
*8 October, 2009 at 5:33 am*

Now I have to take a Stat Mech course.

Too many interests, too little time…
