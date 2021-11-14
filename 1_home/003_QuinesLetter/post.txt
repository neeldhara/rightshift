Title: Quine's Letter
----
Author: Karthik
----
Date: February 22nd, 2008
----
Tags: all math puzzles
----
Text:

Willard Van Orman Quine was a mathematician and philosopher at Harvard known, apparently, for his wit, charm, and openness of mind. In [Quine’s obituary](http://www.wvquine.org/wvq-obit4.html#PPMW), Morton White (a Professor Emeritus at the Institute of Advanced Study, Princeton) tells of the time when he (White) moved from Cambridge to Princeton, and his son Steve was missing multiplication in his Princeton school.  
 In a letter of 1953, Quine wrote to him saying:

> “Since Stevie misses multiplication, he may enjoy gorging on this one. Well, so you have these two numbers, see, and you want to multiply one of them by the other. 0\. K., so you write them down more or less side by side, as potential headings of two potentially parallel potential columns, roughly thus:
> 
> 19 27
> 
> Then you go to work on the left one, cutting it in half. Write the half underneath. No fractions, though. If it was odd, just forget the fraction. If it was <tt>58 .. 537</tt>, just put down <tt>29 .. 268</tt> as its half. That’s near enough. Then, under that in turn, put its half (ignoring, again, the fraction if any); and so on, until you get down to <tt>1</tt>. That completes your left-hand column.
> 
> 19 27
> 
> 9
> 
> 4
> 
> 2
> 
> 1
> 
> Then go to work on the right-hand number, making a column under it by exactly the opposite method: doubling each time. This could go on forever, but don’t let it. Keep your right-hand column lined up with your left-hand column, entry by entry, and stop as soon as you are opposite the bottom of your left-hand column.
> 
> 19 27
> 
> 9 54
> 
> 4 108
> 
> 2 216
> 
> 1 432
> 
> 0\. K., so now you have the two columns side by side. The next thing to do is to start in on the right-hand column and cross out a lot of it. Cross out all the entries which have even numbers opposite them in the left-hand column. Keep only those entries in the right-hand column which have odd numbers opposite them in the left-hand column. All right, now add up the right-hand column, what’s left of it after all the crossing out. The result, unless I have made a mistake somewhere, is the answer to your original multiplication problem.
> 
> 19 27
> 
> 9 54
> 
> 4 ~~108~~
> 
> 2 ~~216~~
> 
> 1 432
> 
> —–
> 
> 513 [19 * 27 = 513]
> 
> It may be that this information reaches Stevie a bit too late to be altogether useful. If I had tipped him off earlier, he would never had had to learn the multiplication table.”

How does this work?

I first saw this a while ago at the [Freakonomics blog](http://freakonomics.blogs.nytimes.com/2007/09/05/a-little-math-puzzle-to-ponder/)- the comments section of the post was filled with solutions within a day. It’s not a hard puzzle to solve; shortly after I figured it out myself, I posed it to three of my hostel-mates. All of them figured it out in less than fifteen minutes.

Wikipedia has an explanation for this “[Ancient Egyptian Multiplication](http://en.wikipedia.org/wiki/Ancient_Egyptian_multiplication)“, but I’m going to document here the way I understand it, if only because I think my solution is elegant (albeit visibly equivalent to the others), and because I did it all-by-myself. Now would be a good time to stop reading and go figure it out yourself.

Details below the fold.  
 <span id="more-30"></span>I’m describing the chain of thought I followed originally. Onward Ho.

I notice a few peculiar things about the operations in this method:

1\. Division and multiplication are carried out with the number 2\. In binary terms, the multiplication corresponds to a very simple operation- _left-shifting_

2\. The reminder at each division step is neglected. With this assurance, the division operation also corresponds to a simple binary operation- _right-shifting_.

3\. Even numbers have binary representations ending in 0.

(Bit-shifting is the operation of moving all bits in a binary number to the left/right, adding zeros/ removing bits as we move along. For instance, 27: 11011 left-shifted would be 110110: 54\. Similarly, 19: 10011 right-shifted would be 1001: 9)

To multiply the numbers 27 and 19 in binary, I would do:

<address>11011</address>

<address>X 10011</address>

<address>————–</address>

<address>11011</address>

<address>110110</address>

<address>0000000</address>

<address>00000000</address>

<address>110110000</address>

<address>——————–</address>

<address>1000000001</address>

Which is the standard way to multiply two numbers- use the fact that multiplication is distributive over addition.

<address>11011 X 10011</address>

<address>= (11011 X 1) + (11011 X 10) + (11011 X 000) + (11011 X 0000) + (11011 X 10000)</address>

<address>= (11011 X 1) + (110110 X 1) + (1101100 X 0) + (11011000 X 0) + (110110000 X 1)</address>


And that’s all there is to it. The first number in each pair of parentheses is a successively left shifted 11011- a 27 successively multiplied by two. The second number is a 0 or a 1, depending on whether the successively right-shifted 10011 (19) is even or odd. A 0 doesn’t count towards the total, for obvious reasons, so we scratch out the rows where the right-shifted number is even. When the right-shifted number is odd, we’re multiplying by 1, so we might as well simply add the left-shifted numbers in the intact rows.

<address>1 X 11011 19 27</address>

<address>1 X 110110 9 54</address>

<address><del>0 X 1101100</del> 4 <del>108</del></address>

<address><del>0 X 11011000</del> 2 <del>216</del></address>

<address>1 X 110110000 1 432</address>

<address>————————————————</address>

<address>1000000001 513</address>

Pretty neat.

* * * * *

## Old comments from the w0rdpress days

**Traums said:**
*23 February, 2008 at 12:58 pm*

Very cute.
But all that left-shift right-shift jargon makes it look like a (link: https://en.wikipedia.org/wiki/Shift_register text: shift-register popup: yes) based Hardware Multiplier implementation manual. Allow me to attempt a simplification. 19 in binary form is written as

10011

It’s an elaborate way of saying :

19 = 1 * 2^4 + 0 * 2^3 + 0 * 2^2 + 1 * 2^1 + 1 * 2^0
= 2^4 + 2^1 + 2^0

So 19 times 27 is really:

27 * 2^4 + 27 * 2^1 + 27 * 2^0

Which are exactly the terms you’ve retained in the second column (the second column lists 27 times 2^i, ‘i’ being position in column).

So the left-column contains the binary form of 19, starting with the LSB (least significant bit) on the top. Every even number corresponds to a ‘1′ bit, and every odd number to a ‘0′ bit.

The ‘1’s at every order (position) in the binary form compensate for the difference between the number and it’s nearest power of two (which is lesser than itself). If that difference is odd, we have a ‘1′ in that order, else a ‘0′.

For example, 16 is the nearest power of 2 to 19 (16 = 2^4).

19 - 16 = 3 is odd.

16 in binary is 10000. The extra offset required is 3.

3 - 2 = 1 is odd.

2 in binary is 10. Extra offset is 1.

1 in binary is 1.

Thus, 19 in binary is 10011.

Every time we hit an even number in the left column, we’ve stumbled upon the power of 2 nearest to (and lesser than) the offset.

This could in principle be done with a base other than 2. Say 3. But one would have to keep track of the exact fraction being neglected in the left-column. Remember, for every factor of 3, there are two non-factors of 3, unlike the binary “even or odd” case.

Nice post Polar. This should psyche my brother out.
