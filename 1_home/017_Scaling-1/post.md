Title: Scaling (I)
----
Author: Karthik
----
Date: January 12th, 2010 
----
Tags: all 
----
Text:

There are presumably many clever, interesting and useful tools and ideas in science and math modeling. The concept of scaling, though, is the most powerful one I've seen in that it makes _very_ nontrivial predictions with just small helpings of information.

Let's start at the top. To _scale_ an object means to multiply its every linear dimension by the same factor. It's what you would expect: a geometric shrinking or enlarging, like under a microscope<sup>[1](#fn.1)</sup>.

Now, attributes of this object scale in different ways. If every linear dimension of the object is multiplied by a factor n, then the surface area and volume of the object go up by factors of $n^2$ and $n^3$ respectively. Depending on how we physically accomplish the scaling, either the mass of the object scales as $n^3$ or its density scales as $1/n^3$. (Stretching the original object preserves the mass but lowers the density by the above factor; creating a scaled-up replica retains the density but increases the mass by the above factor.)<sup>[2](#fn.2)</sup>

Forces scale in different ways:

1\. Let's say you have two hot metal plates identical in shape with a ratio of surface areas of $n^2$. The force of gravity on the larger of the scaled objects is $n^3$ times that on the smaller one.

2\. If the two metal plates were tenderly rested on the surface of water, the force of surface tension on the larger one would be n times that on the smaller one, because surface tension is proportional to the length in contact with the liquid. This explains why you can't float a steel knitting rod on the surface of water, but you can [float a steel pin](http://www.youtube.com/watch?v=YX2s79yyqXc). The surface tension holding the steel pin up is smaller by a factor of about 10, but the pin is lighter by a factor of about 1000.

3\. The force you need to break the larger plate by tugging along its length is $n^2$ times that needed to break the smaller one in the same way.

4\. If you were to pull these plates through molasses, the forces of drag on the plates due to the molasses do _not_ scale in an elementary way- but to a first approximation, the drag force is proportional to the surface area. This means the drag is higher on the larger plate by a factor of (approximately) $n^2$.

And rates of processes scale too. The bigger one would lose heat that much faster. This does not mean that it cools faster! If they are at the same temperature to begin with, the larger plate would lose heat at a rate $n^2$ higher than the smaller one, because this rate is proportional to its surface area. The amount of heat it needs to lose for its temperature to go down by a degree, however, is $n^3$ times higher than the amount the smaller plate does, because this quantity is proportional to its mass. This means it takes the larger plate about $n^3/n^2 = n$ times longer to cool down by the same degree.

The above scaling relations hold because of the simple physics that applies. Actually, when the physics gets complicated, scaling rules still hold; it's just that geometric similarity is not a fruitful pursuit anymore. There are more abstract ways of using scales to work with the system- a bit more on this towards the end.

This is where things get really interesting. Everything, including living things, are subject to the above rules, and we can make some remarkable observations about the design of insects and animals:

The ant is known to carry several times its own weight. Why can't we do this?

First, let's see how an ant would fare if it were about the size of a human. Much of the ant is strong tubes filled with mushy insides. (Insects have exoskeletons, like the ants' chitin.) If you were to breed a six foot tall ant, the weight of the ant would scale as $10^9$, and the load bearing cross-section of the chitin in its legs would go up by a factor of $10^6$.

This means the stress in its legs would go up by a factor of $10^9/10^6 = 1000$. The super-ant would break its legs just by standing!<sup>[3](#fn.3)</sup>

How about load-bearing capacity? The forces its muscles could exert would scale as the square of the linear dimension. (The force a muscle can exert is proportional to its cross sectional area). In this case, the square of (2 m/ 2 mm), which is about $10^6$. A regular ant can lift at least twenty times its own weight; if the super-ant were to try this, the stress on its muscles would be $10^9/10^6 = 1000$ times that of the regular ant.<sup>[4](#fn.4)</sup> Its muscles would rip.

Not so super now, eh?

Conversely, it follows that since you can stand on our legs without collapsing, you will be at least as strong as the ant when you're shrunk to its size. You can do the calculations; the general idea is that the capacity of a muscle-driven creature to bear it's own body weight (or any multiple of it) goes as 1/length of the creature.

The scaling rules tell us that everything will be different when we're shrunk by a factor of a thousand. From the example of the floating steel pin above, it follows that you should be able to walk on water, so long as it's relatively calm. You don't need a pitcher to carry around water; you can hold it in your hand like you would a football. It would take no effort at all to drink it- the super-powerful capillary effect would force it down your throat if you brought your mouth close to it. And yeah, you can hold your own against insects. You would be the iron man (or woman) of the insect world.

It's not all rosy, though. From the cooling example above, it follows that your body would cool a factor of 1000 faster. (Surface area/Body mass = $1/1000$) You would probably die of hypothermia unless you were consuming food _all_ the time. Not only can you lift many times your body weight, you'd have to eat many times your body weight in a day!<sup>[5](#fn.5)</sup>

On the other hand, if you were scaled up by a factor of 80 (say) you would suffer the same fate as the super-ant. Your legs can only bear a load 5-6 times more than they already do when you run or jump- and the stress in your bones would be a factor of 80 higher even when mega-you were just standing still! Your knees would buckle and shatter, smashing every bone in your body as you hit the ground. Your muscles will have torn, and the hydrostatic pressure of the blood in your body acting over a height of 100 m would have forced it down your arteries before rupturing them and causing hemorrhaging. For the same reasons whales do, however, you would survive rather well in the water!

While we're being squeamish:

> As J.B.S. Haldane put it in his classic essay, “[On Being the Right Size](http://irl.cs.ucla.edu/papers/right-size.html),” “You can drop a mouse down a thousand-yard mine shaft; and, on arriving on the bottom, it gets a slight shock and walks away….A rat is killed, a man broken, a horse splashes.” Haldane was being quite literal.
> 
> These facts were known to our ancestors, who used this aspect of scaling to gruesome effect—a common strategy during medieval sieges was to take a carcass of a horse, let it ripen for a few days in the sun, and then catapult it over the walls of the besieged town. On impact, the carcass would indeed splash, spreading contagion throughout the city.<sup>[6](#fn.6)</sup>

Wow!

The above is an extract from a [wonderful article about scaling](http://fathom.lib.uchicago.edu/2/21701757/) in biology that goes into much greater detail of hypothetical changes of scale- highly recommended!

This short foray into design in biology tells us two things: Evolution is, like physics, [imagination in a straightjacket](http://www.google.com/url?sa=t&source=web&ct=res&cd=10&ved=0CCcQFDAJ&url=http%3A%2F%2Fbooks.google.com%2Fbooks%3Fid%3D1HxzLaPYo2IC%26pg%3DPA98%26lpg%3DPA98%26dq%3Drichard%2Bfeynman%2Bimagination%2Bin%2Ba%2Bstraightjacket%26source%3Dbl%26ots%3DqUue3ROPqv%26sig%3DNPsWU8vAjgmaPSNSNTrNr9HIMhE%26hl%3Den%26ei%3DLHccS6HqB5LenAe-2M3QAw%26sa%3DX%26oi%3Dbook_result%26ct%3Dresult%26resnum%3D10%26ved%3D0CCgQ6AEwCQ&ei=LHccS6HqB5LenAe-2M3QAw&usg=AFQjCNH8h0aSbDJPmvW749fG_oSHpXd3VA). Worse, it's a straightjacket within other straightjackets, with additional constraints and intense competition to boot. Nature is the mother of all optimization engines! Second, biological design is _very_ parsimonious; the body of an ant is strong enough to carry the crazy amounts of food its colony needs, but no stronger than it need be.<sup>[7](#fn.7)</sup>

There is _so_ much scope for some hard science fiction here. In fact, a consideration of the physics of scaling is one of the things distinguishing hard and soft science fiction.<sup>[8](#fn.8)</sup>

The above was just one window into the concept of scaling- we saw how the properties of real world objects varied in interesting ways at different sizes. A different set of observations can be made by _looking_ at the _same_ object at different scales: it leads us to all kinds of interesting ideas, like fractals and universality. Perhaps the most amazing use of scaling is a technique that involves looking not at an object (real-world or abstract), but at a mathematical model for a system at different scales. This process, called the renormalization group, is touted as the most impressive use of abstraction in science. It is quite hard to segue into these other uses of scaling here; they're fodder for Scaling II!

* * *

##### Footnotes:

[1.](#fnr.1) Strictly speaking, a traditional microscope does not scale an object geometrically, because of the nonuniform optical properties of the lenses. I don't know of any system of lenses that magnifies correctly along the viewer's line of sight- the depth- of the inspected object.

[2.](#fnr.2) Of course, the above are special cases. You can vary the mass (and thus the density) by whatever factor you want so long as you're scaling it up in your head. We're talking about magnifying the size while retaining as much of the material's inner structure as possible: so if we wanted to scale up a clay pyramid, we would use the same kind of clay to construct a bigger pyramid, and its mass would scale like its volume does, as the cube of the linear dimension.

[3.](#fnr.3) If you are trying to imagine this, pick up a thin tube of plastic- or a straw, and push on both ends of it. It kinks and buckles; this is the usual mode of failure for a slender beam or tube, like the ant's chitinous appendages.

[4.](#fnr.4) This is essentially the same calculation as in the paragraph before it.

[5.](#fnr.5) This tells us something apparently paradoxical: The larger you are, the lesser you ought to eat! While this sounds like good health advice, it is of course an incomplete picture. We don't burn all our energy as heat, we spend a large chunk of it in locomotion, a lot in circulating blood and nutrients around (and in other body maintenance tasks) and a fair bit in thinking.

[6.](#fnr.6) Talk about biological warfare!

[7.](#fnr.7) Because of the way natural selection works, it's not really surprising that this is the case. If the ant couldn't carry several times its own weight, there would be no ant colonies and no ants as we know them, right? It's the antropic principle at work.

[8.](#fnr.8) The other physics most works of sci-fi violate are, of course, conservation laws, like that of momentum and energy. [There are workarounds](http://www.qwantz.com/fanart/superman.pdf), mind you. (PDF)

* * * * *

## Old comments from the w0rdpress days


**Kushal said:**
*14 January, 2010 at 3:55 pm*

By the way, a few days back, I attended a lecture on computational methods in evolutionary studies, and came to know that evolutionary biologists no longer consider nature (evolution) to be a good optimizer:

http://www.nature.com/nature/journal/v326/n6108/pdf/326010a0.pdf

**KVM said:**
*21 January, 2010 at 1:18 pm*

Very nice, especially the Flatland-esque description. The little details like eating and drinking we take for granted - wow! Reminds me of this old joke: an old fish passes by two young ones in the opposite direction and greets, “Howdy boys, how’s the water?”. The young ones smile, and after the old one goes by, one asks the other: “What the heck is water?”

The linked article about scaling in bug movies was wonderful. One of those instant-epics that have far too much good stuff to pick one to quote! In spite of that fact, the one thing that left me completely amazed was the bit about nature conserving safety factors - wow! That’s almost a fundamental law there. Why could that be? I like the level of abstractness of the law - it can’t be explained by just plain-vanilla “Nature strives to improve ‘fitness’”, because one might as well argue that nature might as well chosen another local optimum of having a different form and a higher safety factor with an equal ‘fitness’. We know nature is trying to optimize, but why _this_ local optimum?

Haldane’s article was brilliant too. You can’t resist something that begins, ” In a large textbook of zoology before me I find no indication that the eagle is larger than the sparrow, or the hippopotamus bigger than the hare, though some grudging admissions are made in the case of the mouse and the whale.”
:D

Straitjacket reminds me - I should reply to your comments on Osmosis Jones, and the previous one on Text. Apologies for the delay, will do so soon.

I’m very eagerly awaiting part II on renormalization. It’s one of those topics I have attempted to grok, but the amount of knowledge needed to see the beauty of the method is quite a bit higher than what I have - the learning curve is a bit too steep. Allow me to construct one of my intolerable analogies: topics like these are like step functions in knowledge, or dirac deltas in those most valuable ‘Ah!’ moments (*). The slope is a bit too high for me, but posts like this serve as excellent [mollifiers](https://en.wikipedia.org/wiki/Mollifier), in both the literal sense of easing the pain, and the technical sense of approximating spiky functions (hard math) via a sequence of smooth functions (nice blogs), using [ooh] convolutions (anecdotes) ;-)

A note on footnotes: do check out the tooltip-like popups in [this blog](http://anilmenon.com/blog/) (they are the little green daggers, ctrl+f for ‘†’ ). I find these just excellent for wry remarks.

(*) - The word ‘aascharya’ literally means ‘That which much be ‘ah’ed at’ or ” ‘Ah’-able” :-) 
