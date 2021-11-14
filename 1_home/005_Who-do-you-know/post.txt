Title: Who do you know?
----
Author: Karthik
----
Date: March 10th, 2008
----
Tags: all orkut sociology statistics
----
Text:

So my college batch embarks on a most distressing adventure, one of creating an yearbook with expository information on everyone in the two hundred thirty strong ensemble. The venture is distressing because the few volunteers who’re organizing the data collection, formatting and printing process have had little time to sleep in the past few weeks.

The yearbook itself is likely to prove a nostalgic trigger for the part of our noggins that engages in such frippery, but at the moment, it comes across as a self-proclamation along the lines of “We are _so_ awesome!”; a process of collective unrestricted self-aggrandizement. But this is besides the point.

The prime feature of the yearbook is a section dedicated to a description of each person by his/her peers, listing out why their world would have been markedly incomplete without the company of said individual. These were collected through comments on Orkut, and because everyone is uninhibitedly mopey on Orkut, some rather unlikely testimonials poured out, and poured out freely. The result was a large amount of objective data on _one_ social community conveniently hoarded at _one_ location online, a treasure trove for people looking to study social interaction quantitatively.

This is where I step in.

Below the fold: some surprisingly incoherent trends, a few non-funny disclaimers, and a categorical surrender by me to the statistics gods that be. And graphs! Because everything is more authentic with graphs.  
<span id="more-32"></span>

_EDIT: The images are shrunk, and have shriveled to unreadable proportions. Go clicky-clicky on them._

The disclaimers first:

1.  I _abhor_ social networking. I was badgered into signing up for Orkut for the yearbook, and intend to quit as soon as the funny business ends. If you send me a ‘friend-request’, I will **burn your house** **down**. (On the other hand, Emails I like. Send me a few.)
2.  I have no contempt, despite pretenses, for the activity. It’s proved to be a fascinating experiment, and in due time, I’d like to engage in some reminiscing from behind the veneer of nostalgia as well.

Right, then. The experiment:

Each person had a thread where anyone could write about him/her, two hundred and thirty threads in all. A _post_ is an entry made on a thread by someone who knew the individual the thread was created for. Threads belonging to the popular folk had the most posts, for obvious reasons. In all, anywhere between 0 and 60 posts were made _for_ each person (in each thread), resulting in a total of ~5320 posts. (The average person was written about by 5320/230 ~ 23 people.)

Far more interesting, though, is the distribution of posts: How many threads f(**n**) had a given number of posts **n**? Alternatively, what is the probability distribution of the random variable **n**, where **n** is the number of posts?

(image: orkut1_1.png)

I was expecting _some_ [tendency to cluster](http://en.wikipedia.org/wiki/Central_tendency), but this was better than I had hoped for. Why is this interesting? Because the number of posts I write (one for each person) is strongly positively correlated with the number of people I know well, and the number of people I interact with on a daily basis. In particular, if I assume that the number of posts I write for someone is proportional (or better yet, equal) to the number of people in my social circle, then I can estimate the size of each person’s “sphere of interaction”.

Well, not quite. The data here is the number of posts written _for_ a person, not by him/her. Nevertheless, the argument holds since social relations are bijective: the number of people you know closely is the number of people who know you closely, and so the social circles we seek have been estimated.

Inspired in part by [this humorous article](http://en.nothingisreal.com/wiki/Why_I_Will_Never_Have_a_Girlfriend#_note-4), I lunged for my power tools* to test if the distribution of posts would be Gaussian- because, you know, These Things Are. A least squares fit** suggested nothing of the sort:

(image: orkut2_1.png)

My eyes bleed at the sight- that is the most ill-fitting Gaussian I’ve ever conjured, and sadly, that’s the best I can do. The histogram (and its Gaussian fit) is perplexing and illuminating in roughly equal measure:

*   The mean (or expectation value) of **n**, the number of posts per person is 23.052 ~ 23, in agreement with the earlier estimate. That is, an average of 23 people wrote about any one person, and by hypothesis, an average person knows 23 people closely in my batch of 230 people- about 10% of the total populace. Is this a local equivalent of [Dunham’s number](http://en.wikipedia.org/wiki/Dunbar's_number)?
*   The mean alone is an insufficient criterion. A better measure of how closely knit the community is would be the variance- what is the _range_ of the difference between extroverts and introverts? The standard deviation of the sample (_and_ the Gaussian fit, see **) is 9.4534, implying that the _average_ extrovert interacts with about 9 people more than the _average_ introvert does. Not bad for a community of 230 people, I’d say. <span style="text-decoration: underline;">How does your community fare?</span>
*   In going from 20 to 24 posts per person (**n**), there is a _steep_ fall and rise of the probability- from 0.058 to 0.03\. This might not seem like much, but in terms of the frequency with which 20-24 posts were made, this amounts to 230*p(**n**): a fall and rise from 13 to 7 to 13 posts. This is partly responsible for ruining my much loved Gaussian least squares fit***, as there is a steep fall where a maximum was expected, but the variation is simply too much (100%) for me to shrug off as statistical noise. Why do so many people know 20 and 24 others, while so few know 21-23? I sense a sociological [uncanny valley](http://en.wikipedia.org/wiki/Uncanny_valley).
*   This analysis ignores entirely the fact that the propensity to write testimonials varies from person to person, so that the “constant of proportionality” between the number of testimonials a person writes and the number of people he knows is different for different folks. Such doubts aside, we can estimate parameters of the “network” of social interactions:

(image: networkresized.png)

*   If each person is represented as a ‘node’ on a map and links between nodes Aldebaran and Bellatrix (see figure) means “Aldebaran knows Bellatrix (well enough)”- it follows that “Bellatrix knows Aldebaran (well enough)”, and the total number of links is simply one-half the total number of testimonials written: 5327/2 = 2664 social links between 230 people, at approximately 11.6 links per <span style="text-decoration: line-through;">celestial object</span> person.

*   The histogram isn’t symmetric. The gregarious folk skewer my precious distribution by garnering up to 60 posts when the average is a measly 23- as opposed to the introverts and generally-not-popular chaps, who are (i) many in number (in comparison to the outspoken extroverts), and (ii) closer together in the number of people they know well.

One of the purposes of conducting this analysis was to test the basis for assuming normal distributions in mathematical models in the [soft sciences](http://en.wikipedia.org/wiki/Soft_sciences) whenever a tendency to cluster is expected, such as in psychology or sociology. Of course, I had ready access to only one mound of data, and the results are disrespectfully dismissive of this notion.

The distribution of posts is certainly _not_ Gaussian, unless I’m missing something elementary. What then, is the rule that governs how people interact with other people (and how many people they interact with)? This ‘posterior’ analysis doesn’t help, so I’ll need to create a model from scratch (soon). As promised, I now fling my arms up in desperation and question the game the gods of statistics play with me- whatever they produce all those peaks for, I have no idea. Alternatively, perhaps the IIT Guwahati 2004 batch is a particularly pathological sample for mathematical analysis. The odds are rather high, I’d say!

Finally, in case you’re wondering: I fell comfortably in the ‘ambiverts’ zone, but then _I_ got to choose the introvert-ambivert boundary on the plot! :)

_PS: I hunger for more data so I can make sense of it all. Let me know if you know where I can find it._

* Power tools: That would be [Perl](http://en.wikipedia.org/wiki/Perl) and [Octave](http://en.wikipedia.org/wiki/GNU_Octave), respectively. Awesome combination, really.

* In fitting a given data sample to a normal distribution, the least squares Gaussian mean and variance [simply equal](http://en.wikipedia.org/wiki/Normal_distribution) the sample mean and variance, a most helpful simplification.

* Another reason why the normal distribution is such a poor approximation is because the discrete and the normal distribution are normalized differently: The normal distribution is a probability density, while the discrete distribution is not. The area under the latter curve certainly sums to greater than unity.
