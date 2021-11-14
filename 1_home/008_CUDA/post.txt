Title: CUDA
----
Author: Karthik
----
Date: June 23rd, 2008
----
Tags: all computing gaming
----
Text:
I have two primary uses for personal computers.

By uses, I don’t refer to tasks that involve using a hammer where an orthopaedists’ tongs will suffice; Most modern desktops are far too overpowered for (relative to those below) simple tasks like web surfing and listening to music. (With two primary exceptions: The PC must not run Windows Vista or [Firefox 2.0](http://lifehacker.com/software/ie7/ie7-vs-firefox-2--the-memory-usage-showdown-208908.php)!)

By uses, I mean tasks that tax the machine to its limits, give it a nosebleed while ensuring you’re getting all you can from your hardware. In no specific order, they are (i) Gaming and (ii) Simulation (or equivalently, scientific computation). There’s also media encoding and the like, but the above are most relevant to my case.

These activities (appropriately reserved for vacation and study months) are unfortunately at odds with each other, even though they’re both “computation intensive”. Both involve loads of floating point operations; although I’m sure they have more in common than just that. But simulations have traditionally been CPU intensive activities, while graphics computations are handled almost exclusively by dedicated processors (GPUs) on graphics cards. Physics computations in games are handled by the CPU (or dedicated physics cards), but the GPU is still in charge of pushing pixels to the screen, receiving a major workout in the process.

In short,

*   The GPU is “idling” when you’re not doing something graphics intensive, including times when (for instance) you’re running CFD code that has your CPU running at “full load”. It’s also drawing less power.
*   Your GPU is running hot when you’re playing the latest graphics intensive title, although your CPU might not be at full load.

A scheme of arrangements that is less then satisfactory when you consider this image doing the rounds of the Internet (Released by Nvidia):

(image: gpu_die.jpg)

That is a shot of the Nvidia GeForce GTX 280 (the latest in their series of GPUs as of June ‘08) next to a modern Intel dual core processor. The “Penryn” dual core processor has [just over 410 million transistors](http://www.digital-daily.com/cpu/intel_penryn/); the [GTX 280 has 1.4 billion](http://www.extremetech.com/article2/0,2845,2320089,00.asp)! Larger transistor count doesn’t translate directly to better performance, though- the two are dissimilar in their architecture, purpose and degree of accessibility to the average user. But the latest GPU is, without a doubt, the most advanced piece of hardware you can buy off a shelf right now. And the most powerful piece of hardware in your PC is also the most esoteric, the most specific and the most underutilized.

Which, if I may digress briefly, reminds me of the years I spent pining for a capable graphics card so I could play computer games all day. What kept me from splurging on one of these monsters (GPUs have  outstripped the CPU in transistor count for years now) was that they were too exclusive, too special-purpose to warrant pawning your soul for. And pawn your soul you must, for these things [don’t come cheap](http://www.anandtech.com/video/showdoc.aspx?i=3334$). Well, that and the fact that I was and am incumbent.

All this is set to change now.

<span id="more-61"></span>Except for the incumbent bit. That’s likely to remain for a while!

Nvidia recently released a Software Development Kit (the quaintly named [CUDA](http://www.nvidia.co.in/object/cuda_main_in.html)) that allows users to do general purpose computations on the GPU. The G-P-GPU idea’s been [floating around](http://en.wikipedia.org/wiki/GPGPU) for a while, but this is the first time a free (as-in-beer) toolkit has been released for developing C-programs that can run on the GPU. This implies that if you have a [recent GPU](http://www.nvidia.co.in/object/cuda_learn_products_in.html), you have a computing monster on board that is almost an [order-of-magnitude faster](http://www.ddj.com/cpp/207200659) than your processor. And that’s in addition to what they’re designed for; running games with [jaw-dropping levels](http://www.incrysis.com/downloadvideo.php?id=39) of detail.

(image: crysis_gen.jpg)

And so, both primary tasks I need a computer for are being off-loaded to the GPU. This is exciting indeed. In addition to letting me play [Crysis](http://www.gametrailers.com/game/2509.html) without reducing my display to a slideshow (well, almost), the GPU can now run [astrophysics simulations](http://media.hpcwire.com/documents/nbody_gems3_ch31%5B1%5D.pdf) [PDF] and solve [computational](http://www.biomedcentral.com/1471-2105/8/474) [biology](http://www.biomedcentral.com/1471-2105/9/S2/S10) problems, implying that a well stocked home computer is going to become a computation powerhouse. The toolkit is a combination of source files that can be modified freely and object code and art that are proprietary, which makes it a mixed bag. (It’s royalty free and free to use, though.) Unfortunately I’m no programmer, and it will be a while before (if at all) I train myself to use it for simulations. It would perhaps be better to wait until very high-level software- like plugins/libraries for MATLAB that can utilize the GPGPU- are made available before attempting pesky numerical simulations.

The introduction of the GPGPU might also have some interesting side-effects. The volume of the PC-gaming audience is quite large, but they’re the only ones buying top end graphics cards right now. With the addition to the list of a sizeable chunk of the scientific community interested in engaging miniature supercomputers for their problems, graphics cards are likely to get bigger, better and cheaper- at a rate faster than at present.

In an year or two, I will have to make fewer excuses for a new graphics card (which will hopefully be given a more fitting moniker, like “computation card”) when asking for one from those I am incumbent upon. Or just get one myself. We’ll see.

For now, though, I’ll stick to playing Crysis.

* * * * *

## Old comments from the w0rdpress days

**Traums said:**
*25 June, 2008 at 5:20 am*

Why shouldn’t a PC run Firefox 2?

I’ve been experiencing excessive I/O operations choking up my CPU usage while I run firefox 3 on Ubuntu.

What I’d like to see is even automated, and root tasks offloaded to the GPU without my consent. Perhaps I should be allowed to designate the GPU for “Graphics Processing Only” just before an intense Crysis session.

Now the pressure to make a post is mounting ...
