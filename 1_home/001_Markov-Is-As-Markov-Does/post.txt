Title: Markov is as Markov does
----
Date: February 7, 2008 
---- 
Author: Karthik 
---- 
Tags: all algorithms douglas-adams perl stochastic-processes
----
Text:  

> *“Oddly enough, you’re in the envelope had in the bedside table. The hall was filled. The drum sounded three times, twisting his heels heavily in the business with the hubbub of white gristle.”* -Douglas Adams, on Markov Generators  


Alright, so Douglas Adams (link: https://en.wikiquote.org/wiki/Douglas_Adams text: didn’t actually say popup: yes) as much. But it seems fairly likely that had he been asked, his answer would have been just as (deliberately) inane, and perhaps a touch warping and self-referential.
This little expository piece hopes to introduce in some detail, the process of confounding the sane readership of a piece of text by rearranging the insides to make it seem like a dozen startlingly grammar-aware monkeys have had a go at a word processor. I should probably elaborate, lest you think that a dozen grammar-aware primates have had a go at this piece.
At the epicenter of the semantic catastrophe in the opening statement above is a Markov Generator (MG); a simple (and as we shall see, dumb) algorithm that I encountered recently while attempting a semi-serious study of Perl(link: http://www.greenteapress.com/perl/ text: [1] popup: yes), a high-level computer language that excels at (among other things) text processing.
The MG mixes up words in a piece of text, with results that look like this:

> “Perhaps you would allow me to floor”, but eventually the pause got too long and cruel whip.

> “The rabbit brought his affairs to a private hospital in the morning Kate demanded and got a name to ask the next-door neighbour, the pregnancy of the same moment in the first landing, and looked her up and hurled it this short distance there.”

> Other things you made happen so I’d be afraid of him with any voluntary additional token of his eye, caught sight of Dirk’s mind that it wasn’t actually anything to do it. Odin says, 'Do this,' and I wish you to come and pick up for very long in the morning? Forget it. Dirk had. With his mind entirely taken up with something like hay, a window in her had subsided and he invariably ended up where I was in Wales.”

(Originals from The Long Dark Tea Time Of The Soul by Douglas Adams. The book, by the way, features spontaneous explosions at Heathrow airport, the ever bizarre Svlad Cjelli, and a cameo by the Norse god Thor and his (link: https://en.wikipedia.org/wiki/Mjolnir text: Mjolnir popup: yes). (Go read it!) So with all due respect, the original text made just as much sense; I don’t think anyone will mind the creative plagiarism just yet.)

To be more precise, the MG mixes-and-matches, with the shuffle possessing the following properties:

(1) The frequency with which a word appears is retained.
(2) The punctuation remains immaculate, assuming it was so in the original.
(3) Grammar is ostensibly preserved. (This is a weak assertion, yes.)

Ideally, we would want a fourth assertion, considering especially that monkeys are involved.
(4) The results are eye-gougingly slapstick and amusing.

Alas, things don’t quite work this way. Not yet.

So, postponing (4) until the end, what of objectives (1) through (3)? (1) is simple enough. We read through the original text, keeping count of how many times each word appears in the text. With novels, prepositions usually take the top spots, followed meekly by character names and adjectives. (2) is trivial if we substitute words that involve similar punctuation characters for each other. (3) is nearly impossible, unless we lay down explicit rules for grammar. Given that the algorithm must work on any source text irrespective of voice, tone, and other idiosyncrasies we have no intention of pursuing, writing down a complete set of grammatical constructs is likely to be a herculean effort. This is not quite true(link: https://en.wikipedia.org/wiki/Recursive_transition_network text: [2] popup: yes), but trying to do so will defile the moniker of ‘Markov’ in the MG. Instead, we employ a cheap trick.
The key to “preserving” grammar, in the sense that the output of the MG checks out as reasonably veracious, is to realize that if an arbitrary sentence possesses correct “short range” grammar, it’s probably okay in the “long range” as well. Errors in grammar originate (rather obviously) not from words, but from their combinations. Here’s what I mean:

> “The rabbit brought his affairs to a private hospital in the morning Kate demanded and got a name to ask the next-door neighbour, the pregnancy of the same moment in the first landing, and looked her up and hurled it this short distance there.”

Reading words (1,2 and 3), (2,3 and 4) and so on in the above sentence gives.

The rabbit brought
rabbit brought his
brought his affairs
his affairs to
affairs to a
to a private
a private hospital
…
morning Kate demanded
… and so on.

Each of these structures are grammatically “sound” (even though the line is fairly suspect), in the sense that a large number of grammatically correct sentences can involve them. Intuitively, “The rabbit brought” lends itself extremely well to insertion in an arbitrary English sentence, “morning Kate demanded” less so. Nevertheless, a large number of statements exist where any of the above triads would hold good.

So, a recipe for the MG: (about half of which is ripped shamelessly from [1])

> (i) Read in the entire original text, three consecutive words at a time ("actually anything to"). For the first two predecessors("actually anything") that we will call a prefix, write down the third word that follows these two("to"). We call this word the suffix. There might be other suffixes from elsewhere in the text that also follow the two predecessors, leading to a one-many mapping: (actually anything -> "to","dear","like","wise")

> (ii) Repeat the process for the next set of three consecutive words ("anything to do"). This leads to another map, of the kind (anything to -> "do", "eat", "look","do"). Note that there may be more than one instance of "anything to do" in the text.

> (iii) Once the entire document has been mapped in this manner, choose a random prefix ("anything to"). From the list of suffixes that it is succeeded by in the document ("do", "eat", "look"), choose one at random ("look". This is where we bring in the monkeys.) Our new text reads ("anything to look"), which actually appears somewhere in the original text.

> (iv) Form the next prefix with the latter two words ("to look"), and look up the list of successors ("at","for","in","in,"). Words are read in with their accompanying punctuations, hence the "in,".Choose one at random("in,"), and repeat this step with the new pattern ("to look in,"). Keep at it until you run out of words.

Part of the result of steps (i) through (iv) could be, for instance:

> “There wasn’t actually anything to look in, the grind was.”

Which is a perfectly nonsensical line. The grammar holds up too, for the reasons described earlier. (Unless you want to nitpick.) Also, based on the nature of the mapping defined above, conditions (1) and (2) from earlier are trivially satisfied.

In passing, we see that the grammar is likely to be skewered lesser still if we read 4 consecutive words at a time, and even more so if we read 5,6,…, until we read the entire line at a time in all its self-contained grammatical glory. For each assurance of higher grammatical veracity, however, we lose several potential substitutions for each (now longer) prefix. If we read in the entire line as a prefix, the output of the Markov Generator is very likely to be the original text itself.

The recipe for the MG reveals why the algorithm is called so. ((link: https://en.wikipedia.org/wiki/Andrey_Markov text: Andrey Markov popup: yes), a Russian mathematician, worked extensively on stochastic processes; his research is now known as Markov Chains.) Every new word added to the output is a discrete random variable, its values spanning the present set of suffixes. Moreover, the choice of this word depends only on the previous two suffixes (or alternatively, the current prefix), which is the hallmark of a Markov chain. The recipe also illustrates why the MG is ‘dumb’. It doesn’t understand the nature, structure or meaning of the sentence being read in. Instead, it exploits multiple occurances of similar phrases in a single piece of text. As it turns out, the primates of yore are not at all grammar aware. They’re just lexically competent and have good associative memories. (On second thought, those are highly desirable qualities in humans these days.)

Perl isn’t called the (link: http://acronyms.thefreedictionary.com/Pathologically+Eclectic+Rubbish+Lister+:-%29 text: pathologically eclectic rubbish lister popup: yes) for nothing- For those interested in trying it themselves, here’s the _COMING SOON_ script. (tar.gz, instructions inside) The script doesn’t ‘massage’ the text quite yet- no paragraph or line breaks, but I’m working on it. Among other things, I can now play deserving pranks on the folks in the other class comprehending the postmodern (and arguably inane) works of (link: https://en.wikipedia.org/wiki/Samuel_Beckett text: Samuel Beckett popup: yes). I’d say the odds that the Markov shuffled and original versions of their text are indistinguishable are just about equal. (Proof soon.)

Not being the kind to miss any opportunity for self-referential prose, here’s an excerpt from the output of the Markov Generator, applied to everything in this post, up to and including this line.

> If we read 4 consecutive words at a word appears in the morning Kate demanded … and so on in the document ("do", "eat", "look"), choose one at random("in,"), and repeat this step with the hubbub of white gristle.

> Among other things, I can now play deserving pranks on the folks in the MG. Instead, we employ a cheap trick. The key to "preserving" grammar, in the business with the shuffle possessing the following properties:

> 1. The frequency with which a word processor.

> This leads to another map, of the semantic catastrophe in the opening statement above is a discrete random variable, its values spanning the present set of grammatical constructs is likely to be a herculean effort.

Markov Generators: Lowering information entropy, one shuffle at a time :)

[1] (link: http://www.greenteapress.com/perl/ text: Learning Perl The Hard Way, Chapter 3 popup: yes)

[2] (link: https://en.wikipedia.org/wiki/Recursive_transition_network text: Recursive Transition Networks popup: yes)

*PS: I take back my reservations about (4). “The semantic catastrophe in the opening statement above is a discrete random variable, its values spanning the present set of grammatical constructs”- Moderately funny, and frighteningly open to interpretation!*

* * * * *

## Old comments from the w0rdpress days

**Dileep V. Reddy said:**
*9 February, 2008 at 9:29 am*
Testing.... (Ahem) testing.....

**Antaeus said:**
*10 February, 2008 at 12:31 pm*
Very interesting.
'twill be a good experiment to find the number of words in a prefix that will cause a majority of average length sentences to have consistent long-range grammar.
Then chart the values for various languages.
The one with the smallest prefix count shall be adopted as the official terran dialect someday ^_,^

**Antaeus said:**
*11 February, 2008 at 7:41 am*
I got an idea. How would MGs’ work on a piece of music?
Would it just generate (link: https://en.wikipedia.org/wiki/Pink_noise text: pink noise popup: yes)?

**Polar said:**
*11 march, 2008 at 8:51 am*
By music,
1. If you mean the (mono-frequent) notes of a verse or canon, the MG is likely to produce **very** interesting results. (Each note would correspond to a word, so this is expected.)
2. If you mean a song in general, I don’t know what will happen, because I don’t understand how a sampled fourier-transformed piece is stored in an uncompressed wav file. Not that I didn’t try- I locked up my pc when I did.
