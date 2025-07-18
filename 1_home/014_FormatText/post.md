Title: Format:Text
----
Author: Karthik
----
Date: October 17th, 2009
----
Tags: all data-formats fringe-concerns regexes text
----
Text:

The following is an essay I wrote elaborating upon the power of plain text as a digital medium. I love text based data formats; I work with plain text for nearly everything. I love working at a shell- GUIs frustrate me. I am not an authority on the subjects of GUIs and data formats—I am an end user. Paul Graham says in his inspiring [essay on essays](http://www.paulgraham.com/essay.html):

> An essay is something you write to try to figure something out.

> Figure out what? You don't know yet. And so you can't begin with a thesis, because you don't have one, and may never have one. An essay doesn't begin with a statement, but with a question.

And that explains (in retrospect) why I sat down one evening and hammered out a few thousand words about _text_, of all things. I was trying to figure out why I liked text so.

He continues:

> ...if you want to write essays, you need two ingredients: a few topics you've thought about a lot, and some ability to ferret out the unexpected.

I certainly pass the first requirement, not so much the second! As a technical discourse, this essay will often be in error, and go nowhere on the whole. Read as a whimsical opinion piece about my fascination with all things plain text, however, it makes a smidgen more sense.

### Verbiage

Nested firmly between screen and seat, I take stock of how much of what I see is words. I write this in a text editor, with a browser and a music player open in the background. The browser is best navigated with a mouse; nevertheless, the primary interaction with it involves typing in a URL. A text editor is (by definition) all text—but in addition, I ask things of it, and I ask by typing in commands. The music player lets me click on text naming songs, and on buttons for issuing play commands, but it is not long before I have to recourse to the keyboard to search for a song.

A remarkably large chunk of our method of instructing our personal computers is done with pointing devices, and we like seeing large friendly buttons and boxes telling us where to click. Nevertheless, one finds that many actions involve the typing of text by design, perhaps because there is no other way to design these applications to do something for you. As anyone who's been at a computer for more than a few minutes realizes, this need is marked by that annoying phase of reaching over to the keyboard from the mouse.

The frequent fallback to the keyboard is often accepted, especially by us later generations of users brought up on "intuitive" GUIs, as a remaining vestige of the days when text was the only means of interaction with a computer. Surely this need will be dispensed with in time?

This is a one-sided view of a larger set of tradeoffs we make in our use of computers everyday: automation vs control, obfuscation vs complexity, ease of use vs power and GUIs vs text interfaces—the one that intrigues me the most.

Neal Stephenson's [In The Beginning Was The Command Line](http://www.cryptonomicon.com/beginning.html) is a _brilliant,_ meandering discourse on user interfaces, among other things. If you haven't read it yet, you ought to stop reading this and go take a look<sup>[1](#fn.1)</sup>. (Like, right now).

Operating systems like to present us with clever visual metaphors. Nearly everyone who's used a computer for a while realizes that there is no micro-benchpress compressing a folder when you're shown an animation of the same, and that pages don't fly over across folders when you issue a move command. Of course, in reality these metaphors are multi-layered; multiple levels of abstraction, each progressively twisting and distorting our view of the innards of frighteningly complex hardware carrying out equally frightening terrible processes.

In principle, the user is free to choose one of these realms of abstraction to "reside on", to accept a comfortable level of benign deceit. In practice, most of us have had this choice made for us by others; in most cases without our awareness or consent. (Perhaps this is a good thing. Choice scares us.) This essay peels back just half a layer—a limited under-the-hood tour of how nearly everything comes down to (plain) text at some point in our interaction with computers.

### A Wordy Net

Around the winter of 2004, I spent about four hours in the vicinity of a person deeply absorbed in manipulating lots of gibberish on his terminal. I asked him what it was that was forcing him to sort through bales of noise. "They're email headers!", he said.

"Email _what_?"

"Headers. It's a bunch of text part of every email.

I responded that it was strange, then, that I'd never seen one of those. There is a lot of text (often gibberish, but text nevertheless) associated with email, text that identified the sender, subject and recipient, time stamps, and every automated agent that was involved in the transfer of the email. A one line email is accompanied by more than ten times as much of (meta)information about the email! Mail services and clients go to great lengths to hide the header from the user<sup>[2](#fn.2)</sup>; this exchange of headers is a machination of the æther, designed by humans but not meant for them.

I realized in the following years that it was not just email—many of the invisible exchanges on the Internet are padded with snippets of text; snippets that, if you read carefully, appear to tell the story of their origin. At the lowest level, every data packet sent over the Internet possesses a header stating IP addresses and the format of the data—although we do not need to sniff that low.

Nearly all services offered on the Internet are composed of easily readable text. For instance, here is a snippet of the RSS feed of the site where this is published<sup>[3](#fn.3)</sup>:

> <pre class="example"> http://rightshift.blog Bionic Raptors ate this taglir:...
>     Sun, 07 Jun 2009 11:46:00 +0000 http://backend.userland.com/rss092
>     en Blink, Morse In the novel *Cryptonomicon*, one of the lead
>     characters finds himself implicated in a (comical) drug bust, and
>     is placed in a jail cell under the watchful (electronic) eyes of
>     hi-tech eavesdroppers. It's a scene out of a spy novel (although
>     *Cryptonomicon* isn't quite that), minus the secret agents, plus
>     ... http://rightshift.blog/starterkit/home/Why-are-you-producing-
>     so-few-red-blood-cells-today \u201cWhy are you producing so
>     few red blood cells today?\u201d An interesting note from six
>     months ago that I never got around to posting. 'tis a bit vague,
>     but then so is the source. Besides, I like to think that
>     nebulousness has its share of merits- trickster makes this world,
>     after all.
> </pre>

(For the uninitiated, an RSS feed is a service (and protocol) that offers the content of a website to users. Primarily, it obviates the need to visit a website to access updated content.)

There's plenty of crud in there, but if I stare at it long enough, easily identifiable patterns emerge. I see timestamps, URLs and sample content from previous posts, arranged in order—and just like that, I begin to understand how a feed reader (aggregator) works. Retreiving content from this website, filtering out bits not meant for our eyes, and printing it to a window involves exchange of text at several levels, and little else.

Most Internet thoroughfare works the same way. HTML (and its cousins) are text-based "markup" languages, and sure enough, they begin a document with an explanatory header. Images and audio files come with text snippets attached. Who makes up these rules?

[These guys](http://www.ietf.org) do. In particular, they release abstrusely named documents called Request(s) For Comments. That is where the rules of the æther are made up. And it's all text. For instance, here is the [RFC for email messages](http://tools.ietf.org/html/rfc2822)<sup>[4](#fn.4)</sup>.

Why are things this way? My first thought is: _How else could things be?_ But it is not too hard to imagine an Internet where all services talk with bits of binary data. Indeed, plain text has low information content per character, so using binary padding might conserve bandwidth. I reckon the architects stuck with text because the machinations in the æther will truly be lost to us otherwise—plain text is the most _natural_ format for the transfer of information, albeit not the most efficient Thankfully, manageability was chosen over efficiency when the Internet was being realized.<sup>[5](#fn.5)</sup>

### Plain Old Text

_Text is the spine of the Internet._

What of it? The point is that text is a fantastic medium for information exchange _between humans_.

When you edit a configuration file in /etc in Linux, you're not so much instructing the operating system as you are the person who set up the configuration in the first place. You tell him what you want your OS to do for you, in plain English, and he spells it out—he already has—in computerese. It's the same with text and the Internet.

But all of that is just half the story.

At this point, it would be germane to elaborate upon the difference between text and plain text—at least as I use these terms in this essay.

By text, I mean any combination of ASCII (or its supersets, such as UTF-8) characters. The only common feature of entities in this category is that every character is human-readable. This would include all source code, markup code, email (and other) headers, and text like that found on this page.

Plain text refers to text written in English (or any other language, for that matter) with no characters to be interpreted specially ("escaped"). By extension, a plain text file is one that contains plain text and nothing else. Traditionally, this corresponds to the contents of .txt files.

The only type of file we've left out is the [binary file](http://en.wikipedia.org/wiki/Binary_files)—which can be conveniently slotted away as a file whose contents do not satisfy the above criteria. (A Microsoft Word document is a binary file, even though under the right conditions you can read plain text off of it.)

Plain text (and text in general) is a very powerful medium for storing and retreiving information. It's the best we have today, for a number of reasons. In the light of the tradeoffs in usage mentioned earlier, the place of plain text is a very important one: Form (word processors) vs Content (text editors).

Plain text is highly portable. It doesn't matter what OS you're on. It doesn't matter what software you have installed. It doesn't matter what kind of display you use. You can read it on your phone and your ebook reader. In fact, if you can see a blinking cursor in a forty year old teletype, you can use it to read text. You could read it off a mainframe forty years ago. And when I think about it, it is quite likely that this is the only existing format we will be able to read off whatever device we use forty years from now.

It's stable. A corrupt binary file is a nightmare to recover. By virtue of being human readable, handling a corrupt text file is a relatively pleasant prospect. As a bonus, plain text documents work the best with [version control](http://en.wikipedia.org/wiki/Version_control) systems. In short, that means a text file is the easiest kind of file to track changes in and back up.

Text is easy to compose. There is no learning curve<sup>[6](#fn.6)</sup> because you've been doing it all your life. Plain (unformatted) text is often easier on the eyes when you read, as well.

In a plain text document, the focus is on the content, not bling. Agreeably, there are situations when it is prudent to chose form over content, but most often (for essays such as this, say) this is not the case.

With very simple tools, plain text (and text in general) is very malleable. In the hands of a texpert<sup>[7](#fn.7)</sup>, plain text is amazingly efficient. No other data format comes close when it comes to manipulability.

The above reads like a checklist of reasons not to use Word, but the intended message is general in nature.<sup>[8](#fn.8)</sup> For sheer power, no format I have ever used matches up. (But then I'm not a programmer, and there are several binary formats I haven't tried.)

What plain text files are not: They aren't good containers for large files. There is a parsing overhead involved in reading text files, and random access to some part of the file without having to read the whole thing is hard.<sup>[9](#fn.9)</sup> They don't handle associations well- text files don't make for good spreadsheets. Of course, better ways to deal with large files also involve text, just not plain text.

For storing and exchanging information, text is the format of the Internet and the format of the OS. In retrospect, this is not as surprising—text is, after all, the natural format for exchanging information between us humans, and we built all of that.

### M-x butterfly

All of which implies that we require means of generating and modifying this information in the first place. Enter the text editor—considered to be one of the pillars of a usable operating system. [This description](https://web.archive.org/web/20090607080644/http://www.computerworld.com/action/article.do?command=printArticleBasic&taxonomyName=Operating+Systems&articleId=9133570&taxonomyId=89) illustrates:

> In August 1969, Ken Thompson, a programmer at AT&T subsidiary Bell Laboratories, saw the month-long departure of his wife and young son as an opportunity to put his ideas for a new operating system into practice. He wrote the first version of Unix in assembly language for a wimpy Digital Equipment Corp. (DEC) PDP-7 minicomputer, spending one week each on the operating system, a shell, an editor and an assembler.

Among programmers, text editors are revered pieces of software, used and proselytised about with religious fervour. Or so the Internet suggests. I'm not a programmer<sup>[10](#fn.10)</sup> <sup>[11](#fn.11)</sup>, but I still spend an inordinate amount of time hammering away in a text editor, so I understand what the fuss is about, somewhat. Plain text is much more powerful than most people give it credit for. How efficiently it works for you depends on the editor you use, with Notepad (the one bundled with Windows) at the bottom of the utility ladder and several contenders fighting for the top spot.

Neal Stephenson is commonly quoted on his statement about text editors<sup>[12](#fn.12)</sup>, from his above mentioned essay:

> In the GNU/Linux world there are two major text editing programs: the minimalist vi (known in some implementations as elvis) and the maximalist emacs. I use emacs, which might be thought of as a thermonuclear word processor. It was created by Richard Stallman; enough said. It is written in Lisp, which is the only computer language that is beautiful. It is colossal, and yet it only edits straight ASCII text files, which is to say, no fonts, no boldface, no underlining. In other words, the engineer-hours that, in the case of Microsoft Word, were devoted to features like mail merge, and the ability to embed feature-length motion pictures in corporate memoranda, were, in the case of emacs, focused with maniacal intensity on the deceptively simple-seeming problem of editing text. If you are a professional writer—i.e., if someone else is getting paid to worry about how your words are formatted and printed—emacs outshines all other editing software in approximately the same way that the noonday sun does the stars. It is not just bigger and brighter; it simply makes everything else vanish.

Emacs is indeed comparable to Microsoft Word in scope (and little else, thankfully). If you've ever traversed the depths of the sub-menus in Microsoft Word and taken stock of the things you can do, you must wonder what functionality emacs could provide in handling plain text alone that compares.<sup>[13](#fn.13)</sup> Rephrased, that question reads:

"How much can a text editor do with plain text anyway?"

It's a valid question, deserving of an example-laden tour around emacs-town<sup>[14](#fn.14)</sup>, but it would be an unwelcome digression here. In short, a powerful text editor makes it a pleasure to compose text by encouraging economy of motion, automating repetitive tasks, and making it easy to (re-)configure its behaviour to suit your needs.

The best text editors are comparable to sheets of surgical steel. You can't do much with it at first—you'll cut your fingers on the edges if you try too hard. It needs to be tempered, beaten into shape, ground, polished and sharpened until you can use it as a scalpel. But it is, by then, _your_ scalpel and yours alone—it fits in your palm like it belongs there (and it does). Because you spent time training with it even as you forged the instrument, you can now use the scalpel to execute deft maneuvers, to do in seconds what took minutes with the blunt knife you were using before. It will take years to test every cut the scalpel can make, but you will already have achieved a level of proficiency with it that will make you wonder how you ever managed without it.

The other powerful tool when handling text is a language for matching strings (of characters) of interest, known as regular expressions. Regular expressions let you specify a pattern of characters that you are interested in by stating _rules_ to be followed by the expression processor. This is a much more powerful way of searching text compared to specifying a string itself—it is very nearly<sup>[15](#fn.15)</sup> like setting an assistant on the job of, say, finding every sentence in this essay that contains exactly fourteen nonconsecutive e's but no reference to a footnote.

[Whimsical examples](http://xkcd.com/208/) aside, regular expressions are used everyday to separate valuable information from torrents of raw text, but they are often stated to be a [double edged sword](http://regex.info/blog/2006-09-15/247). I love them, though. It helps that all self-respecting text editors have built-in support for regular expression syntax.

My morbid fascination with all things text is tied intricately to the tools I use to handle it. And there is no dearth of tools for handling plain text—on a standard install of the Linux operating system, there are dozens of programs (Unix shell utilities) that operate on text, and they can all be made to talk to each other, stringing together tasks to carry out complex transformations of the input. If this corpus of little tools prove insufficient, any of several programming languages (Perl, Python—also usually included) allows for writing scripts that process text in complicated (and inane) ways quite easily.

This stringing together (piping) of tools is an extremely useful idea. At a command line, programs act on strings of text passed to them as arguments—so one could, for instance, rename a thousand files at once by constructing a regular expression for the kind of filename to be renamed and the string to be renamed to, and giving the old and new names to the Unix rename-file command. As a consequence of the operating system's text based interface, easily manipulated text corresponds to an easily controlled operating system!

This is an unexpected revelation. Every advantage that plain text enjoys is an advantage for systems that incorporate them into their control structure as well. It's a subtle idea at first for those of us inundated with visual metaphors for using a computer. Once you begin poking under the hood, however, there's no turning back.

### Word

No one believes they lack perspective until they've acquired some of it. I did not realize how fractured my view of technology was until a professor at college casually mentioned that the map is one of the most underrated technologies in the history of man; it made conquest (and imperialism) possible. One is used to thinking of cartography as an art, maybe, and definitely a skill, but not technology.

At some point, thinking about what counts as technology becomes a game of semantics- but a few (somewhat) startling observations can be made. Here is an excerpt from Wikipedia's [article on writing](http://en.wikipedia.org/wiki/Writing%20):

> In Eurasia writing began as a consequence of the burgeoning needs of accounting. Around the 4th millennium BC, the complexity of trade and administration outgrew the power of memory, and writing became a more dependable method of recording and presenting transactions in a permanent form (Robinson, 2003, p. 36). In Mesoamerica writing may have evolved through calendrics and a political necessity for recording historical events.

When the process of instructing digital computers became a complex, enervating task, the engineers in charge instructed computers to understand words instead of numeric addresses. They constructed the first of many levels of abstraction to follow, but all of them since have been based on words. It is not surprising that this should be so—text is a mature technology in itself, all of six thousand years old.

Our primary means of interaction with programmable machines is still text, but the innards of the system are slowly being obscured by ever more intuitive and interactive graphical displays. The older, text based abstractions will stick around, though—and hopefully plain text will remain as gleeful an encoding to work with for quite some time.

After all, the recorded word is the ultimate technology.

* * *

##### Footnotes:

[1.](#fnr.1) Incidentally, _In The Beginning..._ is only available as a text file, which says something about the author's preferences.

[2.](#fnr.2) But provide them if you ask politely.

[3.](#fnr.3) This is likely a moot exercise. Anyone familiar with RSS feeds will also know what they're made of, so it conveys nothing to its intended audience and is irrelevant to the remaining.

[4.](#fnr.4) Good luck with reading that.

[5.](#fnr.5) On the other hand, text compresses better than binary data. There is doubtless [more to this argument](http://www.stuartcheshire.org/rants/Latency.html) than what I could think of—I have not studied the history of the Internet.

[6.](#fnr.6) If you want to get really good at writing text, this statement is patently false. A good text editor possesses as much of a learning curve as a document processor.

[7.](#fnr.7) Yeah, I made that up. TeXpert is often used to describe a person proficient with TeX, but The TeXbook suggests that because of the way TeX is pronounced, TeXperts ought to be called TeXnicians instead.

[8.](#fnr.8) That said, I fervently hope the day does not arise when I will be forced to use Word.

[9.](#fnr.9) But not impossible, [apparently](http://www.jwz.org/doc/mailsum.html).

[10.](#fnr.10) And this essay isn't aimed at programmers either. If you're one, you already know all of this.

[11.](#fnr.11) I did implement an AVL tree in C once. Phew! That was when I knew programming was not my thing. I do enjoy a little scripting every now and then, though.

[12.](#fnr.12) Not all of it is accurate today. Emacs now displays italicized and bold text, for instance. But I think it remains true in spirit.

[13.](#fnr.13) If you're an emacs user, you're probably wondering the opposite.

[14.](#fnr.14) Or Vi(m) town, for that matter. I'm fairly ecumenical when it comes to the two behemoths, preferring them both for different tasks. For writing a long essay, however, emacs blows away all competition.

[15.](#fnr.15) Very nearly, because regular expressions are written in a formal language, and so there are things it can't do. No expression can be written to match a palindrome of arbitrary length, for instance.

##### Further Reading

*   [In The Beginning Was The Command Line](http://www.cryptonomicon.com/beginning.html)
*   [Welcome To The Universe Of Fancy Colored Paper!](http://www.cs.cornell.edu/Info/People/raman/publications/colored-paper.html)

    > An amusing metaphorical look at the world of proprietary data formats.

*   Jamie Zawinski's [mail summary files](http://www.jwz.org/doc/mailsum.html)

    > To see how he set up a blazing fast way of accessing text files.

*   [The Power of Plain Text](http://c2.com/cgi/wiki/wiki?PowerOfPlainText)

    > A long Wiki discussion of the merits (and demerits) of plain text.

*   Demonstrations of what Emacs or Vim can do with plain text are surprisingly hard to find. The best way to see what the fuss is about would be to play around with them- but [here's](http://nubyonrails.com/articles/emacs-emacs) a five minute screencast showcasing some of emacs' more advanced features.
*   [Regular expressions](http://zez.org/article/articleview/11/) explained. Also, [here's](http://www.seeingwithc.org/topic7html.html) a step-by-step build of an elementary regular expression matching engine.


* * * * *

## Old comments from the w0rdpress days

**KVM said:**
*12 December, 2009 at 4:48 am*

Wow, very, very nice read! There’s a kind of pleasure in reading something that is not written with a word-limit in mind.

The first thing I thought of when you mentioned GUIs and text was this essay by David ‘Quine-God’ Madore about how GUI’s are restrictive. [Link to Google’s Cache](74.125.155.132/search?q=cache:TvoRJwqwJUgJ:www.madore.org/~david/computers/antims.html+madore+graphical&cd=2&hl=en&ct=clnk&gl=us)

Paul Graham’s quote is very interesting. I’ve always felt that that a necessary and sufficient condition for writing is to have conversations with oneself. And for _good_ writing, _natural_ conversations with oneself. Why should one even put pen to paper (or finger to keyboard) if one is not grappling with a thought that is shouting to be expressed, or a question that must be answered just for its own sake?

I’m actually priming myself for an experiment - I only have a very superficial understanding of Emacs or Vim; just enough to understand (and sometimes make) jokes about them :-) I still use Crimson Editor or TextWrangler for almost all my emails, blogs, and essentially everything I write. I’ll find the right muhurta and switch over to E or V, let’s see what my eigeneditor will turn out to be. In doing so, I want to fully explore the effect of Graham’s Blub paradox on myself. Right now I don’t feel I miss anything, but later on I want to able to say, “Wow, I was really in the stone age back then!”. That will also provide a lot of fuel to a blog I want to write about the Blub paradox; Graham’s own treatment of that fantastic idea is step-motherly at best. There’s goldmine there.

Regexes to match arbitrary-length palindromes - for a moment there, my heart was racing in hope that that was a Turing-unsolvable problem. A few seconds on Google deflated it though, it just is a quirk of the Regex format :( I think I understood Gödel’s theorem a few days ago, and am utterly disappointed. The _only_ examples I have found of it having troubled Mathematics in any way is via self-referential statements. I’ve been searching high and low for a _bonafide_ example of Gödel’s theorem: a simple statement of number theory that is true but is unprovable. I’ve had some luck with Goodstein’s theorem, but I still haven’t been able to find a proof for that. My hunch is that Gödel’s theorem has nothing to do with it, though. I hope to God (Göd?) the Incompleteness theorem has more to it than just self-reference being cute. Even other things that I hitherto have thought to be amazing - the halting problem, for instance - become just some self-referential silliness if that’s true. It was in this vein that I was hopeful that the palindrome search was hard, but no luck :(

The last bit on writing reminded me of Shreevatsa’s post on ‘Reading Aloud’ - Writing is so common, and yet so amazing!

Perhaps that only thing that is painful about text is that it’s so hard to read on a computer. For example, this blog on paper would an absolute pleasure - a few pages, and I can thumb back and forth and write and doodle and do all sorts of stuff. But in my browser, the footnotes are really hard to jump between and there’s a kind of restricted linearity that I don’t like. Even if I don’t read non-linearly, I want to have the ability to do so - somewhat like a zero-force member being in a truss just to take care of the possibility that a load is imbalanced :) It’s a bit paradoxical, though. I love to _write_ on a computer; I find it far more comfortable to type than to write. But to _read_, nothing comes close to paper!

**Karthik said:**
*13 December, 2009 at 7:10 am*

I never thought anyone would read through the wall of text above. :)

David Madore’s essay seems representative of the prevalent mood among the Old Ones circa 1998. The sysadmins and hackers were seeing a torrent of GUI based development piggybacking on Windows, and a considerable fraction of this demographic couldn’t help expressing a knee-jerk reaction as its inescapable shackles came down on the average user:

“Am I suggesting that the average user, say anybody’s mother, should learn the complexities of the command prompt? Yes!”

The above is probably a manipulative misquote. He does temper this statement rather well later in the essay, but even accounting for the 1998ness of it all, I can’t help but be turned off by the smattering of “micro$oft”s and “Windoze”.
I believe his list showcasing the efficacy of CLIs is a sermon to the wrong choir. I think the idea of a GUI is not empowerment, it’s outreach. And it works!

Why am I arguing orthogonally to the thrust of the mountain of prose above?
Because Paul Graham was right, and because I figured out something.
CLI and GUI interaction share the same atoms, primitive basis vectors that let you do sufficiently low level and (usually) orthogonal tasks. CLI atoms are either either atoms or simple linear combinations of them. nl is a linear combination of cat and wc; you could “express” any one in terms of the other two. find is (functionally) a combination of ls and grep, but this relation is not invertible. Perl is a smorgasbord of atoms- a veritable subspace of the set of atoms available at the CLI. The dimension of this space is limited only by the capabilities of the hardware, so it’s effectively infinite dimensional. The simplest GUI apps are also simple combinations, scalar-multiplied with system libraries- Xpad is just cat and some tk, Phatch is just imagemagick and some Python. But bigger applications and GUI interfaces are something else entirely. They’re linear combinations of so many library-multiplied-atoms that it takes large companies months to form useful ones. They are fantastic beasts that can do crazy stuff- but unlike atoms, are no longer orthogonal to each other, and combining these mammoth vectors to do anything meaningful is impossible. If CLI tools are Legendre polynomials, a GUI app is an infinite series that approximates ln(Gamma(J_bessel(x))); good for computing itself and a few variants, but not much else. This explains why people who familiarize themselves with the atoms never look back, except perhaps when they need to calculate the above monster series in a jiffy. It also explains the joy of tinkering around on the shell- combining atoms is like playing with Lego; you cannot make a corvette, but who knows, you might just make a [Reprap](http://reprap.org/). GUIs and GUI apps will never be as versatile as text because they’re not simple, orthogonal basis vectors.
Highly specific needs allow monster GUI apps to exist. GUIs have less to do with intuitiveness than they do with meeting specific needs- Which is why I think the point of GUIs is outreach. The vector space analogy is no isomorphism, granted, but it did shed some light, even if the field was reasonably lit to begin with. :)

“I’ve always felt that that a necessary and sufficient condition for writing is to have conversations with oneself.”

I didn’t always feel this way, but the more I read, the more I tend to agree with this. Any opinion piece that does not read like the author was having an interesting conversation with himself indeed feels like he was just going through the motions.

On Emacs, Vim and jokes: Oh, don’t get me started! (But I will, anyway.) I was introduced to Vim five years ago by the resident Linux guru who said a better text editor had not been written. A few years of Vim and Emacs later, I think text editors are more trouble than they are worth. The problem with something like Emacs is that it is self-consuming. It edits itself best! In the above analogy, it’s the mother of all subspaces of CLI atoms- it’s the (effectively) infinite dimensional mumspace. For instance, the muse-el prose and wiki writing extension to Emacs is used extensively and exclusively to [proselytize itself](http://mwolson.org/static/dist/muse/QuickStart.html) on the Internet.
I don’t know if you’ll see other editors as blub if you switch. Text Wrangler appears to be a very capable editor.

Regexes to match arbitrary length palindromes: Turing-unsolvable is exactly what I thought at first!
Perl 5 did add recursive regexes- I think it should now be possible to search for Palindromes, but [I’m not sure](https://rxfl.wordpress.com/2008/08/18/recursive-regexes/).
I completely understand what you mean about self-reference becoming just a gimmick! I would love to find a situation where it’s an actual crippling blow to a proof other than a proof of itself. Gee, that got confusing real quick, eh?

Reading text on a screen: There’s really [no argument](http://www.penny-arcade.com/comic/2009/03/09), even when compared to reading with specially prepared formats on specially prepared devices.

“It’s a bit paradoxical, though. I love to _write_ on a computer; I find it far more comfortable to type than to write. But to _read_, nothing comes close to paper!”
There is [a solution](https://en.wikipedia.org/wiki/Typewriter). :P 
