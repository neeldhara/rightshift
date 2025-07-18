Title: The Illegal Prime
----
Author: Karthik
----
Date: August 9th, 2010
----
Tags: all bash dmca primes regexes unix web resources
----
Text:

Hello, reader. An offering, for your perusal:

> It’s unbelievable today, but there was a time when the government classed crypto as a munition and made it illegal for anyone to export or use it on national security grounds. Get that? We used to have illegal math in this country.


> The National Security Agency were the real movers behind the ban. They had a crypto standard that they said was strong enough for bankers and their customers to use, but not so strong that the mafia would be able to keep its books secret from them. The standard, DES-56, was said to be practically unbreakable. Then one of EFF’s millionaire co-founders built a $250,000 DES-56 cracker that could break the cipher in two hours.

> Still the NSA argued that it should be able to keep American citizens from possessing secrets it couldn’t pry into. Then EFF dealt its death-blow. In 1995, they represented a Berkeley mathematics grad student called Dan Bernstein in court. Bernstein had written a crypto tutorial that contained computer code that could be used to make a cipher stronger than DES-56. Millions of times stronger. As far as the NSA was concerned, that made his article into a weapon, and therefore unpublishable.

> Well, it may be hard to get a judge to understand crypto and what it means, but it turned out that the average Appeals Court judge isn’t real enthusiastic about telling grad students what kind of articles they’re allowed to write. The crypto wars ended with a victory for the good guys when the 9th Circuit Appellate Division Court ruled that code was a form of expression protected under the First Amendment — “Congress shall make no law abridging the freedom of speech.” If you’ve ever bought something on the Internet, or sent a secret message, or checked your bank-balance, you used crypto that EFF legalized. Good thing, too: the NSA just isn’t that smart. Anything they know how to crack, you can be sure that terrorists and mobsters can get around too.


From the amazing (and edifying!) (link: http://craphound.com/littlebrother/download/ text: Little Brother popup: yes), by Cory Doctorow. But no, this little burst of text isn’t about this (scary) modern day dystopian novel, or the EFF, or crypto, or security. It’s about a 1401 digit prime number that showed up in my feeds, via (link: http://www.everything2.com/ text: Everything2 popup: yes), a mystery in a puzzle in a mystery. It’s about Unix, and about peeling back layers. This prime number is illegal. I’m going to paste it anyway, then tell you why:

<pre><code>48565078965739782930984189469428613770744208735135792401965207366869<br/>85134010472374469687974399261175109737777010274475280490588313840375<br/>49709987909653955227011712157025974666993240226834596619606034851742<br/>49773584685188556745702571254749996482194184655710084119086259716947<br/>97079915200486670997592359606132072597379799361886063169144735883002<br/>45336972781813914797955513399949394882899846917836100182597890103160<br/>19618350343448956870538452085380458424156548248893338047475871128339<br/>59896852232544608408971119771276941207958624405471613210050064598201<br/>76961771809478113622002723448272249323259547234688002927776497906148<br/>12984042834572014634896854716908235473783566197218622496943162271666<br/>39390554302415647329248552489912257394665486271404821171381243882177<br/>17602984125524464744505583462814488335631902725319590439283873764073<br/>91689125792405501562088978716337599910788708490815909754801928576845<br/>19885963053238234905580920329996032344711407760198471635311617130785<br/>76084862236370283570104961259568184678596533310077017991614674472549<br/>27283348691600064758591746278121269007351830924153010630289329566584<br/>36620008004767789679843820907976198594936463093805863367214696959750<br/>27968771205724996666980561453382074120315933770309949152746918356593<br/>76210222006812679827344576093802030447912277498091795593838712100058<br/>87666892584487004707725524970604446521271304043211826101035911864766<br/>62963858495087448497373476861420880529443</code></pre>

What is it for?

When written in base 16 (hexadecimal), this 1401 digit prime number found by Phil Carmody forms a gzip file of the C-source code that decrypts the DVD Movie encryption scheme (DeCSS). This prime number is illegal in every country that the DMCA applies.

Wow.

If you’re like me, you’re firing up a terminal right now to unfurl the layers one after another, driven by burning curiosity to see what the seed contains. If you’re not… well, aren’t you a little curious? Of course your are.

Let’s get on a Unix shell and start peeling.

<hr>

# Getting the number

If you select all of the digits in the number above using your mouse, you’ll pull in a lot of newline (and/or carriage return) characters, even if you try copying the HTML source. If you’re going to deal with HTML source anyway, let’s make this easy on ourselves.

I read about it on Everything2, and you can use (link: http://everything2.com/title/Illegal+prime+number text: this URL popup: yes) to access the number from there, or you could use the (link: http://rightshift.blog/starterkit/home/The-Illegal-Prime text: URL to this page) itself.

Now we pull down the HTML so we can easily parse the number:

```
$ curl -s http://rightshift.blog/starterkit/home/The-Illegal-Prime
```

That should spew out the HTML containing this number. If ‘curl’ is not your thing, try wget to save to a file, or use the browser itself, and replace the above by ‘cat your filename’.

Next, let’s find this block of text. It’s preformatted with either a &lt;blockquote&gt; or &lt;pre&gt; tag, so we use that in a regular expression. There may be more than one preformatted section in the page, so we use a dirty hack in the pattern matching: Let’s put in the first few digits of the number in the pattern so the other blockquotes don’t match.

```
$ curl -s http://rightshift.blog/starterkit/home/The-Illegal-Prime | awk '/(<pre>|<blockquote>).*4856.+(<\/pre>|<\/blockquote>)/ {print}'
```

We could have used grep instead of awk, but we’ll get to that in a moment. If the command works, you should see the illegal prime on screen with a bunch of &lt;br&gt; and other tags mixed in. Let’s get rid of those, shall we?

```
$ curl -s http://rightshift.blog/starterkit/home/The-Illegal-Prime | awk '/(<pre>|<blockquote>).*4856.+(<\/pre>|<\/blockquote>)/ {gsub(/[^[:digit:]]/,""); print}' 
```

The gsub performs a global substitution on any character that is not a digit , **/[^[:digit:]]/**. This should print just the number on the screen. Things will get very unwieldy soon, so we’ll store this number (actually a string) into a variable. In Bash, the only way to do this is: 

```
$ prime=$(curl -s http://rightshift.blog/starterkit/home/The-Illegal-Prime | awk '/(<pre>|<blockquote>).*4856.+(<\/pre>|<\/blockquote>)/ \
{gsub(/[^[:digit:]]/,""); print}')
```

Note the ‘\’ followed by a newline, splitting the command onto two lines. If you were typing this, you don’t need to include either.

<hr>

# Converting it to hex

To see $prime in hex, we use **bc**, the handy command line calculator:

```
$ echo "obase=16; $prime" | bc
```

This should print out the number in Hex. Here are the first few bytes:

```
1F8B0808196C9A3A00036373732D6465736372616D626C652E6300ED56CD8E9B3010\
BEF314F412E140241B304B95984B1F618F164859205D2B4BB64AA65B56BB79F70EE1\
2736F1A1552F6DB51...
```

Oops. bc considered it appropriate to put end of line markers, \ splitting the text across multiple lines. Let’s get rid of them, using **tr**, the text replacement utility:

```
$ echo "obase=16; $prime" | bc | tr -d '\\\n'
```

There are three \’s in the text we’re deleting because one of them’s part of ‘\n’, one of them is a literal backslash that’s escaped by the shell, and the third one’s there to keep the second one from being escaped. Phew.

As a check, here’s what the (link: http://www.gzip.org/zlib/rfc-gzip.html#member-format text: gzip specification popup: yes) says about the header to any gzip file:

> The first two bytes have the fixed values ID1 = 31 (0×1f, 037), ID2 = 139 (0×8b, 213), to identify the file as being in gzip format.

1F8B, indeed. We’re almost there.

<hr>

# Dumping it into a binary file

The above stream can’t be unzipped! This sure bewildered for a few minutes. I suppose this is what happens when your mental model of the computer’s storage structure is as badly broken as mine.

Of course it can’t be unzipped. It’s an ascii stream of hex characters; still an ascii stream! We need to dump the above hex code into a binary file.

How do we do that? Sure, you can write some code in C to do it. (Scan as hex and use putchar().)
But you know what they say about Unix: If you need to do it, it’s been done. Hmm. Let’s search for a bit:

```
$ apropos --and hex dump
hd (1)               - ASCII, decimal, hexadecimal, octal dump
hexdump (1)          - ASCII, decimal, hexadecimal, octal dump
xxd (1)              - make a hexdump or do the reverse.
```

Slowly I realize how true this adage is. Enter xxd. Some thinking reveals that we need to do a reverse hex dump. A hex dump is where the contents of a binary file are printed out as a stream of ascii-encoded hex characters, we’re trying to do the opposite. After reading the man page, we construct the reverse hex dump:

```
$ echo "obase=16; $prime" | bc | tr -d '\\\n' | xxd -r -p
```

If all goes well, we shoud see a stream of unprintable characters (no, not that type) desperately trying to print themselves on the screen.

<hr>

# On to the source

The rest is trivial. We have the gzipped stream pouring through ‘xxd‘, so let’s redirect that:

```
$ echo "obase=16; $prime" | bc | tr -d '\\\n' | xxd -r -p | zcat
```

And that’s it. If **‘zcat‘** doesn’t work, for some reason, try **‘gunzip -c‘**.

The illegal source code hidden in the illegal prime should be floating on your screen now.

What, you thought I’d put it here? **_It’s illegal_**.

Probably more illegal than printing the number, anyway. If you skipped to the end hoping to glance at the code, here’s an unreadable composite command for you, instead. (Again, note the line breaking ‘\’ after awk’s first argument, added to keep this webpage from breaking.) Hide your eyes, they who fear line noise:

```
$ curl -s http://rightshift.blog/starterkit/home/The-Illegal-Prime | awk '/(<pre>|<blockquote>).*4856.*(<\/pre>|<\/blockquote>)/ \
{gsub(/[^[:digit:]]/,""); print "obase=16;" $0}' | bc | tr -d '\\\n' | xxd -r -p | zcat
```

Or, you know, you could just read the code on Wikipedia. I didn’t. I don’t know anything about crypto, but I expected a certain kind of joy in deciphering this simple code, something I could actually hope to do. I wasn’t disappointed.

# The wormhole

Now, the DMCA isn’t at odds with the opening excerpt: It’s all right to write code that does absolutely anything, and it may be all right to distribute it, but it’s illegal (by the DMCA) to use it to break copy-protection measures.

Except for one little thing, though. There is still illegal math.

A request, then: Someone explain that C source to me!

<hr>

Further reading:

- (link: http://craphound.com/littlebrother/download/ text: Little Brother popup: yes), as described by Cory Doctorow: “This book is meant to be part of the conversation about what an information society means: does it mean total control, or unheard-of liberty? It’s not just a noun, it’s a verb, it’s something you do.”
This book is licensed under Creative Commons, and is free to download. It’s also a cracker of a novel.

- (link: http://www.regular-expressions.info/tutorial.html text: Regular expressions popup: yes) are awesome. I cannot stress this enough. If you want to see a whimsical but fantastic use of regexes, (link: https://rxfl.wordpress.com/2008/11/15/regex-prime/ text: try this popup: yes).

- Phil Carmody’s (link: http://primes.utm.edu/bios/page.php?id=239 text: Titanic Primes popup: yes). See for yourself.

- The (link: http://www.gzip.org/zlib/rfc-gzip.html text: gzip specification popup: yes): Just to see what goes into making a standard. Why did they pick 1F8B as the gzip header, for instance?

- The Unix utilities **(link: www.gnu.org/software/gawk/manual/gawk.html text: awk popup: yes)**, **(link: https://www.gnu.org/software/bc/manual/html_mono/bc.html text: bc popup: yes)**, **tr** and **(link: http://curl.haxx.se/docs/manual.html text: curl popup: yes)**. The entire (link: https://www.gnu.org/software/coreutils/manual/coreutils.html text: GNU coreutils popup: yes) pack is awesome, more functionality than you can ever need in a terse, powerful set of commands.

- (link: https://www.gnu.org/software/coreutils/manual/coreutils.html text: Hex Dump Code Golf popup: yes), a game played by the Stack Overflow community where the objective is to write a reverse hex dump in the language of your choice in the fewest chars possible. Perl won.

* * * * *

## Old comments from the w0rdpress days

**Traums said:**
*9 August, 2010 at 3:14 am*

Insane…
Although I doubt there is much in the fact that that number happened to be a prime. zcat seemed to detect and ignore some ‘trailing garbage’. Besides, the number can be altered drastically by changing variable names and adding comments to the *.c file. I don’t know how ergodically that number can be made to vary, and whether it is ’sufficiently easy’ to touch other nearest primes. Does the decrease in prime-number density flatten after some big number? Must summon Neels in on this one.

There is a self-referential GEB-esque philosophy to illegality of math (or any string of symbols). The statement, ” If one prints out all the digits of \pi, one will eventually encounter the entire Windows 7 source code” might be as profound as it is profoundly useless. But I’d wager that with appropriate choice of block chaining or cypher feedback rules, one can make out the first n digits of \pi to be the Windows 7 source code.

Crypto munitions brought back memories of
http://www.cypherspace.org/adam/rsa/
and
http://www.cypherspace.org/rsa/spook.html

The decryption code itself demands another blogpost. But now we’ll have to buy a commercial DVD and break the law :)

**Tweets that mention >> RIGHTSHIFT >> The Illegal Prime -- Topsy.com said:**
*9 August, 2010 at 11:37 am*

[...] This post was mentioned on Twitter by Suresh Govindarajan, AlbinJames. AlbinJames said: RT @modularform: LOL >> RIGHTSHIFT » The Illegal Prime http://bit.ly/akNGDt [...]
