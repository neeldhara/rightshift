Title: A Tryst with Card Counting
----
Author: Dileep
----
Date: November 2, 2015
----
Tags: all card counting blackjack 21 casino gambling advantage play statistics probability odds risk code coding simulation travel money geek nerd mob
----
Text:


(image: bellagio.jpg width: 800 caption: Bellagio musical fountain show. Photo credit: Wes Erickson)


So there's this movie called [21](http://www.imdb.com/title/tt0478087/), about a group of students from MIT who get recruited by a Math professor to learn how to count cards, and then hit the casinos in Vegas with a big wad of investor dough to see if they could make the wad a little bigger. Since some of the greatest ideas to come from MIT in the past few decades have involved [students doing their own thing in their spare time](https://en.wikipedia.org/wiki/Hackers:_Heroes_of_the_Computer_Revolution), this naturally piqued my noodle. Years later, I'd acquire a [book](http://www.book-info.com/isbn/1-4176-6563-7.htm) containing a fictionalized account of a real life MIT card counting team (which allegedly also inspired the movie). Reading said book cemented card counting into my bucket list. Eventually, in the fall of 2014, during a department hosted winter holiday party at the end of term, I asked my trusty fellow physicist [Wes](http://pages.uoregon.edu/wwe/index.html) if he'd be interested in investing some time and money into a most fickle summer project involving statistics, coding, travel, cloak&#45;and&#45;dagger pretense, Blackjack and money. And he was drunk enough to say "sure!" 

Thus began Project Deckard.


# What is Card Counting?

If you walk into a large enough Casino, and navigate through the maze of slot machines for long enough, you will run into areas consisting of tables, and chairs, and uniformed employees manning them. No, these aren't cafes. They are "pits," where "table games" are played. A particularly popular game played at these tables is called "[Blackjack](https://en.wikipedia.org/wiki/Blackjack)" (or "21"). It's a game that pits the players against the casino, instead of each other. The table consists of six locations where players can place their bets, a 'shoe' where several jokerless decks of shuffled cards are stored ready to be drawn, a place to discard used cards into, some seats, a tray full of color&#45;coded casino chips with numerical currency denominations printed on them, a 'dealer' who can be identified by his/her uniform, and the table's location inside the pit. The pit will also consist of a pitboss and other employees, and there is always a camera above every table called the 'eye in the sky' that records the entire game. The camera is used for dispute resolution, and by the security team to catch card counters. But more on that later.

(image: table.jpg caption: Blackjack table at Ceasar's Palace. Source: http://www.blackjackscience.com/)

The play starts with a clear table. The dealer waits for players to place their bets in the form of chips (which can be bought with cash at any table at any time) before the round can begin. The bet sizes have to respect the table minimum and maximum to be valid. Once the dealer makes the sign (hand gesture) for closing the bets, the round begins, and every player and the dealer is dealt two cards from the shoe. One of the dealer's cards is placed face&#45;up, and the other face down (called the hole card). And unless the table happens to be a single&#45;deck game, or a two&#45;deck game with some special house rule, all of the player's cards are dealt face up for everyone to see. Now the second phase of the game begins: The dealer addresses each player in turn, starting from her left, asking them to make a series of decisions. Every card in the deck has a number associated with it. The number cards represent their own numbers, and the face cards are worth 10. An ace can be counted as 1 or 11. The objective of the round is to ensure that the sum of all the cards' numbers of the player exceeds the dealer's total, without exceeding the value of 21. A total is "soft" if it is computed with an ace functioning as an 11. If either totals exceeds 21, then that person is said to have "busted" their hand. If the above mentioned victory condition is achieved, or if the dealer busts, the player wins back their original bet plus an equal amount from the casino. If the player and dealer totals equal each other, then the round is considered a "push," and the player is awarded the original bet back. If the dealer's total exceeds the player's without exceeding 21, or if the player busts, then the dealer confiscates the player's bet for the house. If the player gets a total of 21 with just the opening two cards (which is possible if one of them is an ace and the other a card of value 10), then the player is said to have gotten a Blackjack, and will win 1.5 times the original bet amount as payout (over the original bet). Blackjack payout is offered instantly, before the round reaches phase three.

Since the player's cards are face up, they (and everyone else) know their total, but only partial information about the dealer's hand is available. Based on this knowledge, the player is asked to make one of five decisions:

- **Hit:** The player asks for another card to be dealt from the shoe.
- **Double:** The player doubles his bet on the table in exchange for one (and only one) more card from the shoe.
- **Split:** When the two cards are of the same numerical value, the player may split the hand into two hands by matching his bet, and will be dealt two cards to create two pairs. The play proceeds with the player playing the two hands independently.
- **Stand:** where the player decides that the current number of cards is sufficient, and passes the play to the next player, or back to the dealer.
- **Surrender:** (If available) The player surrenders half of his bet amount to the casino in exchange for the other half being returned immediately, and exits the round.

Once all the players have had their turn for phase two decisions, the round enters phase three, where the dealer reveals her hole card. If the dealer's total is below 17, then the rules dictate that the dealer must hit (deal a card to self from the shoe). And so the dealer hits until the total reaches 17 or above. And then, based on the totals, all the bets are resolved, and the cards are stuffed into the discard pile before a new round can begin. All decisions during phase two are made using hand gestures, and verbal commands hold no sway. This is so the 'eye&#45;in&#45;the&#45;sky' can track the play, and be used for dispute resolution. Depending on the speed of the dealer and the players, a six player round can take about 30 to 60 seconds. And unless you are a highroller, most blackjack tables at non&#45;Vegas&#45;strip type casinos have a table minimum of $\$$5 or $\$$10 in the US. So unless some smart decisions are made, the game can very quickly drain your bank!

If the dealer's visible card is an ace, then the dealer asks if any player without a blackjack would like to avail themselves of insurance. Insurance involves placing half the original bet in the special zone on the table, which is basically betting that the dealer has a Blackjack. A player with a Blackjack is then asked if he would like to accept "even money" (i.e. receive regular victory payout instead of a Blackjack payout). After insurance is "closed," the dealer then looks at the hole card in secret (using a prism/mirror embedded in the table) to check for a dealer Blackjack. If the dealer indeed has a Blackjack, then the hole card is revealed. All players that claimed insurance will get to keep all of their money for that round. And players with Blackjacks who didn't accept even money now enter a "push" with the dealer, and only get their original bet back. It is generally advised to always accept even money, and never insure your bet.

(image: basic_strat_chart.jpg caption: Basic strategy chart for 4-to-8 deck shoes. Source: Wikipedia)

If you ask google for advice on how to play Blackjack without losing too much money too soon, you will very quickly run into decision charts such as these. This is known as basic strategy, and if adhered to along with a constant bet size, can in the long run, minimize the house edge (i.e. maximize player's edge). Basic strategy is extant knowledge, and everyone playing Blackjack is expected to know this. You can even ask the dealer for advice on what the optimum move is if you ever forget, and most places even allow players to bring a printed copy of the charts for reference during play. The casinos don't care because the house edge still remains positive (there would be no Blackjack tables otherwise!). The house edge at most tables is typically around 0.5% (i.e. per round, the player on average loses 0.5% of bet amount), with a variance of around 3%. On top of the standard game rules, casinos usually impose additional house rules, which can significantly affect the edge. Possible house rules variations are:

- An upper limit on the maximum number of recursively split hands playable.
- Blackjack payout (3 to 2, or 6 to 5).
- Whether surrender is allowed as an option.
- Whether the player is allowed to hit split aces (if not, then the player is simply dealt two cards, one for each ace of a split pair, and the hands are stood).
- Whether the player is allowed to double after a split.
- Whether a dealer is required to hit on a soft 17 (total).

Some set of house rules are more favorable than others. For example, the dealer standing on a soft 17 is a huge advantage to the player, and one must avoid playing at 6&#45;to&#45;5 blackjack payout tables on principle.

(image: datum1_zoom.png caption: Player edge vs. some house rules. Plot generated from our code: https://github.com/dileepvr/decks)

The basic strategy is computed based on the probability of the value of the next card drawn from a full shoe. Hence, the charts change a little with the size (number of decks) of the shoe. However, every round does not start with a full shoe. In the shoe of shuffled decks, there is a special blank&#45;colored card called the shuffle card. If the shuffle card is ever drawn during a round, then that will be the last round played before all the cards from the discard pile and those left over in the shoe are brought together, reshuffled, and restacked into the shoe. The depth at which the shuffle card is placed into the shoe is colloquially termed "penetration." And there is a reason why the penetration of a shoe is never 100% (its usually 80% for a six&#45;deck shoe, and 50% for a two&#45;deck or single&#45;deck shoe). This is because as more cards are drawn (and revealed) from a shoe, this gives the player increasing amounts of information about the content of the remaining cards in the shoe, including new odds for the values of future cards drawn. And as the number of cards in the shoe depletes, the possibility space also decreases, and the player will be able to predict future draws with increasing amounts of accuracy. This information can be used in decision&#45;making (both in phase two, as well as in the size of the bets) to turn the house edge negative (that is, to see net statistical positive gains). This act of tracking the values of drawn cards to infer information about the remaining shoe using only one's eyes, memory, and concentration is popularly called **Card Counting**.


# So, it has been a thing, apparentely ...

Card counting is not illegal under federal, state, and local laws in the United States as long as no external card counting device or person assists the player in counting cards. Casinos object to the practice, and try to prevent it by banning players believed to be counters. In their pursuit to identify card counters, casinos sometimes misidentify and ban players suspected of counting cards even if they do not. Atlantic City casinos in the state of New Jersey are forbidden from barring card counters as a result of a New Jersey Supreme Court decision. In 1979 Ken Uston, a Blackjack Hall of Fame inductee, filed a lawsuit against an Atlantic City casino, claiming that casinos did not have the right to ban skilled players. The New Jersey Supreme Court agreed, ruling that "the state's control of Atlantic City's casinos is so complete that only the New Jersey Casino Control Commission has the power to make rules to exclude skillful players." The Commission has made no regulation on card counting, so that Atlantic City casinos are not allowed to ban card counters. Being unable to ban counters even if detected, Atlantic City casinos increased countermeasures (see below).

(image: ken_uston.jpg caption: Ken Uston. Source: http://www.countingedge.com)

In the early 1990s, students at MIT, and friends and partners who had previously seen 100% returns on smaller investments, funded a $\$$1 million dollar company called Strategic Investments, which would train bright students to card count and gamble, and then unleash them on the unsuspecting casinos. People who passed the internal tests, and who could look the part, would be assigned to teams, and would be sent off to locations with team pool funds to make a profit. Pressure to perform was growing as more players started being spotted by the casinos and were barred from playing. A private detective had been employed to find them, who realised from the Boston addresses of many of those caught that this was a student team from MIT. He even obtained a yearbook including some of their photos.

They had 10, 20, or 30 people playing in five different casino locales, some in Las Vegas, some in New Orleans, some in Canada, and were keeping track of their play while trying to make sure no one was embezzling funds. The venture had had mixed success and the money earned wasn't as much as many had hoped, especially as it had to be split between so many players and investors. In the end, the increasing pressure meant Strategic Investments was dissolved in December 1993. By then the team had grown to around 80 players. Many went on to found their own teams.

Very few such teams last very long though. Longevity is unusual among Blackjack teams, which often fall apart due to discouragement or suspicion among team members during losing streaks. The MIT Blackjack team once made $\$$50,000 in a single night, which put them on the map. They inspired the book "Bringing Down the House" by Ben Mezrich, as well as the movie "21" starring Kevin Spacey.

The Blackjack Hall of Fame, launched in 2002, honors the greatest Blackjack experts, authors, and professional players in history. It is housed at the Barona Casino, in San Diego, California. The Barona Casino awards to each inductee a permanent lifetime comp for full room, food and beverage, in exchange for each member’s agreement never to play on Barona’s tables :P


# Okay. But you haven't explained what Counting is! And what did you actually do?

I have introduced the concept of player edge, and its dependence on house rules. Wes and I needed to thoroughly analyze the mathematics of the game before we risked actual money on our quixotic quest. Naturally, we put our programming caps on and went to work. All graphs on this page (plotted with gnuplot) are showing data generated from our simulation code, available at [https://github.com/dileepvr/decks](https://github.com/dileepvr/decks).

There are house rule (and shoe size) combinations that give the player a more negative edge, sometimes close to -2%. However, most tables we've seen play with rules that put the player edge closer to -0.5%. We suspect that players start avoiding tables that accrue a bad reputation. This makes Blackjack the casino game with the smallest house edge, provided one follows basic strategy and sticks to a constant bet size. The plot below shows a little more about how a typical round plays out.

(image: x01_ghist.png caption: Gains in a typical hand. Error bars are too small to show)

The histogram is roughly the same for two&#45;deck shoes. It illustrates how the number of times one loses a straight bet is slightly larger than when one wins a straight bet. But there are bars for winning or losing twice, thrice, or even larger factors of the basic bet size. These occur due to special decisions like splits, doubles, and their recursive combinations, as well as Blackjack payouts. Interestingly, the wins at factors of two and higher are slightly larger than the number of loses. Most of the gains are really made with these special plays.

But there is more going on in the game. And to understand this, I'll have to introduce the concept of a shoe **true count**. A "count" is basically a single number assigned to a shoe, that represents the prevalence of high cards versus low cards left in it. A shuffled full shoe starts with a count of zero. And the count updates every time a card is drawn from it and revealed. Counts are great because all one has to do is keep track of a single number and diligently update it as the play continues, instead of having to memorize every single card that has been dealt. And card counting relies on the count of the shoe for decision making. There are many card counting strategies that rely on different types of counts. The list from the wikipedia article reads thusly:

(image: hilo_counts.png)

Some strategies also involve keeping a side count for the number of aces left in the shoe. The difference in gains between the various strategies is miniscule. It is more important to train in the simplest strategy and not make mistakes. Overoptimization is often more troublesome than it's worth. And so we used the simplest possible count: the Hi&#45;Lo count, which occupies the first row in the above table. As mentioned, a freshly shuffled full shoe starts with a count of zero. Everytime a card of numeric value between 2 and 6 is drawn from the shoe, the Hi&#45;Lo count increases by 1. And everytime a card of value 10 or higher (ace) is drawn, the count decreases (hence -1). Cards 7, 8, and 9 do not affect the Hi&#45;Lo count. Clearly, the signs are chosen such that a shoe with a large count has more high cards than low cards left in it (as many low cards will have already been drawn from it to increase the count). Consequently, the probability of dealing a high card on the next draw would be high. The coverse is true by symmetry.

But shoes of different sizes have different limits on the maximum possible value of the count. So decision making has to take the number of decks in the shoe into account. Therefore, what one really needs to track is the **True Count**, which is the count divided by the approximate number of decks left in the shoe. This becomes easy to estimate visually through practice (one need only look at the size of the discard pile), and can safely be rounded off up to half a deck. If we reanalyze the simulation data for basic strategy for correlations of parameters with the true count, then we can see more structure within the game.

<!-- "If we reanalyze...": This sentence is not clear -->

(image: rs01_tchist1.png)

The above bar graph illustrates the occurrence of true count values during the betting phase of the round for a typical game for two different shoe sizes. The penetration for the six deck shoe was set at 80% and the two&#45;deck shoe at 50%. Well shuffled shoes will for the most part average around zero, but naturally there is a distribution of typical true counts encountered. And the variance of this distribution increases with a smaller shoe size. So, to economize one's time in card counting, sticking to smaller shoe tables is the way to go. However, the house rules can sometimes be too strict for small shoe tables. For example, in some single&#45;deck tables the players are dealt their cards face down, and aren't allowed to show them to other players unless special decisions (split, double) are made or outcomes (Blackjack, bust) encountered. Also, casinos are more wary of counters at small shoe tables. Six deck tables, while being more drawn out, do have a higher probability of reaching extreme true count values. But one has to play long hours to see the benefits of this.

And what are these benefits I speak of? A high true count favors the player, and a smaller (negative) true count favors the dealer. The graph below shows the inherent true count dependent player edge for basic strategy play for two different shoe sizes in a typical shoe game.

(image: rs01_tchist2.png)

The bars at the extreme ends are more error prone as those true count values weren't encounted often enough for good statistics. There are better ways to plot the above graph (like starting with a biased shoe for example), but the basic point is unambiguous. If we multiply the inherent player edge for a true count with the frequency of occurrence of said true count (and normalize the curve), we get the following actual&#45;gain versus true count plot.

(image: rs01_tchist3.png)

Again, this assumes that the player is following basic strategy and not varying bet size. The above graph illustrates all of Blackjack in a nutshell. The reason the house has an edge (and the reason the game is even offered at casinos) is because the area under the negative lobe of the curve exceeds the positive lobe. And there you have it. The entire game in a single graph.

While were were debugging and trying to get the code to spit out sane values, we were also practicing our basic strategy and our true count tracking abilities at home. The photographs below show Wes and me practicing with our mutual friend and fellow physicist [Gabe](http://pages.uoregon.edu/gbarello/), who joined us on some of our pre&#45;Vegas outings. Also in the frame is a screen shot of a javascript applet that Wes cooked up for practice in a browser. This was basically mimicing existing online trainers, such as [the blackjack trainer](http://www.blackjack-trainer.net/), with added counting functionality. We also relied on the [Wizard of Odds](http://wizardofodds.com/) site for more information for our prep.

(image: laughing.png)

Practicing in a homely environment doesn't quite emulate the noisy, smoky, distraction filled locale of a casino, but it really did help sharpen our game. For some in&#45;field real practice, we needed to visit some local casinos. Oregon, it turns out, has a whole bunch of casinos on Indian Reservation lands. And so, a map was drawn, and a list of all the ones to the west of Eugene was made, and a summer weekend roadtrip schedule took form.

(image: calendar1.png)


# Casinos in reservations are a thing, apparentely ...

Gambling on Oregonian reservation lands is not called Gambling. The correct term is: Indian Gaming.

(image: oregon_indians_hood.jpg)

The Indian Gaming Regulatory Act is a 1988 United States federal law (Reagan era) that establishes the jurisdictional framework governing Indian gaming. The act establishes three classes of games with a different regulatory scheme for each:

- **Class I:** Traditional Indian gaming, and social gaming.

- **Class II:** Bingo and non&#45;banked card games that are played against other players. Slot machines and electronic facsimiles are excluded explicitly.

- **Class III:** Everything else, including Blackjack.

Indian reservations have tribal sovereignty. States have limited ability to forbid gambling there, as codified by the Indian Gaming Regulatory Act of 1988. Tribes get to enter into "Tribe&#45;State Compacts" if they want to establish a casino on reservation lands. The Compacts are declared necessary for any Class III gaming on reservations under the Indian Gaming Regulatory Act of 1988 (IGRA). They were designed to allow tribal and state governments to come to a "business" agreement. A compact can be thought of as a "negotiated agreement between two political entities" that resolves questions of overlapping jurisdictional responsibilities. Compacts affect the delicate power balance between states, federal, and tribal governments. It is these forms that have been a major source of controversy surrounding Indian gaming.

Certain Indian tribes in Oregon have repeatedly attempted to get permits to build off&#45;reservation casinos in or near the lucrative Portland market, to no effect. Some public voices oppose the current practice of government. One reason for the opposition comes from the fact that the Bureau of Indian Affairs grants tax&#45;payer money to tribes for economic development purposes. Some tribes use that money to create casinos and other gaming establishments. Certain citizens reject the idea of using tax payer money to build tax&#45;exempt tribal casinos which generate tax&#45;exempt revenue. We, on the other hand, didn't mind all that much.

(image: oregon_travel1.png)

Driving to coastal towns in Oregon in the summer is a pleasant holiday experience. I'd recommend it to counters and non&#45;counters alike. Wes, Gabe, and I had a lot of fun admiring the mountainous terrain, visiting the local tourist attractions, and sampling the local foods (and wine (and beer)). Some places were visited twice, and still left things unexplored. If the weather cooperated, all of these places tended to be perfect Sunday getaways. And along the way, we encountered several omens and sigils alluding to our endeavor. The "Wizard of Odds" store in Florence, OR takes the prize for the best coincidental omen. And we spotted it on our first trip!

(image: oregon_travel2.png)

Most of the other gamblers we spotted on the Oregon trips were mostly old folk, who we presumed were rich and retired, and were throwing away their retirement savings. Some of them were really senile. There are few sights more depressing than a very old woman sitting hunched next to a slot machine and repeatedly banging on the one-armed bandit hoping for a jackpot. Speaking of the slot machines, casinos seem to be full of them. It is ridiculous how popular they are, and says a lot about the general population of the planet. On day one, Wes tried to slip $\$$10 into a slot machine before we had tried our first real-world game of Blackjack. He took a few spins on the machine, and right way, the true nature of the whole enterprise was laid bare in front of us. On every roll, the deduction in the total amount in the player's bank would happen instantly (these were electronic slot machines with an LCD screen, and sound effects). So Wes's bank amount would immediately decrease by a dollar in less than half a second. But he won 33 cents on a particular roll, and the slot machine lit up with bells and whistles and flashy animations. It incremented his bank slowly, one cent at a time, ringing a bell for every increment, drawing out the whole process to make it seem like he had won big. All casino games, including Blackjack are designed this way. They bleed your bank continuously while you are stuck in a compulsive action-loop, but when you do win on occasion, they give you the impression that you have won big. Your victories never quite compensate for your losses.

(image: oregon_travel3.png)

Almost all the tables we found had six&#45;deck shoes, and everyone shuffled by hand. The house rules weren't as favorable as they could have been (no surrenders, dealer hits soft&#45;17), but according to our calculations, some basic counting can give one a net positive, if tiny, edge. The Blackjack payouts were always 3&#45;to&#45;2, but you could not hit split aces. Penetrations varied between 80% and 85%. The minimum bet at most of these tables was $\$$5, although one joint bumped it up to $\$$10 after a particular hour in the evening. We are not sure how vigilant these reservation casinos are against counters. Once a dealer accused Gabe of counting in jest after he had won a big hand. And I did get heat (in the form of a strange look) at another joint when I stopped playing hands on a shoe with a large negative count (which is normal. People are superstitious enough to believe that a particular shoe/shuffle is just inherently unlucky for them, causing them to sit the game out until the next shuffle), but decided to opt in on a round as soon as the count recovered to zero before the shuffle card had been drawn. Luckily, that place was huge, and I just grabbed my chips and walked away (which is normal as well) to another pit. Some places are smokier than others. Refer to trip advisor websites for reviews of the place before venturing. Some pits don't open until a particular hour after lunch. The whole experience can be boring unless you learn to engage the other players and the dealer in casual conversation. The idea is to come off as a natural gambler. Perhaps even a spoiled trust&#45;fund kid. Some players, however, will be hyper-social, and will try to engage you in conversation just as you are trying to concentrate on all the cards on the table to update your count. Remember, if counting as a group, to sit at different tables if possible, pretend to not know each other, and enter/leave the casino at different times. Do not be intimidated by the speed of a fast experienced dealer. You can take as much time as you want with your decisions in phase two. Ignore the bullshit statistics advice other drunken players will try to give you, but humor them. Hop tables on occasion if the count gets too low. Tip the dealer only at the end of your play. And stay off the table-specific special side bets. They have huge payouts, but are sucker's bets, and will eat into your edge. Oh, and it is generally considered impolite to join a table mid&#45;shoe, as superstitious players tend to think that it affects their luck.

(image: oregon_travel4.png)

Casinos don't allow photography inside their premises. While we did manage to pose with the security staff in a couple of them (with the exit doors in the background), I'll resist putting those out on the internet. The Oregon Blackjack experience was, with all its ups and downs, well worth it. It helped cure our initial nervousness, and made us less sensitive to risking hundreds of dollars of hard&#45;earned money on stupid, geeky misadventures. It also helped us learn to behave like a robot that always follows the algorithm irrespective of how well or badly the game is progressing. Our first two runs were only meant to try out basic strategy. We started tracking counts on the third, and started making count based decisions from the fourth onwards. The plot above doesn't show the final run, as I seem to have lost data for that final day. But I did come out positive. (Gabe's numbers haven't been displayed, as he wasn't there for all of the trips.)

<!--  and I don't have his permission to release that information. -->


# How to exploit superior knowledge for profit

We've established that high true counts favor the player, as it increases the chances of high cards being drawn. This means that the dealer is more likely to bust if he/she needs to hit, and the player's first hand is more likely to total 20 or 21. If that doesn't occur, it can still be advantageous to double or split under certain conditions and expect a high total. But since the house controls the shuffle process, we cannot prime the shoe to give us a high true count. What is to be done then? An obvious solution is to play basic strategy with a constant bet size, but to leave a table when ever the true count gets below a particular threshold (or choose to sit the shoe out). The simulations do indeed indicate that table hopping will increase the players edge to positive values.

(image: sixdeck_twodeck_hopping_index.png)

However, table hopping isn't a viable strategy. Most places will not have free table spots with good house rules to jump into, especially during rush hours. And sitting a shoe out too often will cause frowns, as you are occupying a spot where someone else could have played and made the casino some money. And if we consider the gains made per hour, this will rapidly make Blackjack a wasteful proposition. So what are our other options?

Why, bet spreading of course! The basic idea is to bet big when the true count is high, and reduce bet back to the table minimum when the true count reaches zero or lower (This can be combined with sitting a bad shoe out). So then, how much to spread? And how fast? to answer this, I defined two parameters:

- The **bet spread** is the maximum factor of the minimum bet that we are willing to bet in a single round, say when the true count is 5.
- The **bet ramp** is the general speed with which we raise our bets (versus increases in true count). The figure below shows some curves for these.

(image: bet_ramp_definitions.png)

Using these two parameters, we can very quickly simulate the effective player edge using the said same code. And the results, shown below, are very encouraging.

(image: six_deck_ramps.png caption: Sigma has been divided by 10 in the above graph for visualization purposes)

The variance increases with larger bet spreads. But more interestingly, for smaller bet spreads (like 5), ramp one dominates, indicating that ramping fast and hard is the way to go. This is because true counts closer to zero occur more often, and it makes sense to exploit them early. But at larger bet spreads, the linear ramp (3) wins out. The is probably because even though larger true counts are rare, they are also more favorable. So reaching a higher spread at larger true counts can offset their rarity. I plot the histogram for the outcome of a typical hand for a bet spread of 1 (no bet spread) and of 5, below.

(image: rs01_two_deck_spread_ghist.png)

As expected, spreading bet size will increase variance. As far as winning or losing the table-minimum bet amount goes, the relative heights of the bars do not change, as this play is identical to basic strategy. However, there are more ways to win and lose big when spreading the bet. And due to inherent player favorability of high true counts, the gains from winning big just about compensate for and eclipse the loss from losing big. This occurs because of rare hands that allow recursive string-combos of special decisions such as splits and doubles.

<!--  "And due to inherent player favorability of high true counts." Do you mean "Due to the player favoring high true counts"? Right now it reads like the player is being favored, not favoring certain conditions. -->

(image: two_deck_tchist_spread.png)

We can repeat the actual-gain versus true count normalized plots for spreads of 1 and 20 (above), and clearly visualize where our gains are coming from. And this is counting in a nutshell. The above graph shows what we really want. A player edge of, say around 0.5% or 1%. Starting from good house rules and increasing bet spread is the name of the game.

# Vegas baby!

(youtube: https://www.youtube.com/watch?v=naDCCW5TSpU width: 600 height: 480)

As the summer was inevitably coming to an end, we had to rapidly plan our six-day Vegas trip. Buoyed by our Oregon experience, and eager to aim our momentum, Wes and I hashed out an itinerary and reserved flights, hotel and rental car in a single evening. Certain companies offer really cheap flights to and from Vegas, provided one reserves them in advance. Cheap hotels are a dime a dozen, but I would suggest trying to get a room closer to downtown, to save on the rental car.

(image: vegas_map.png)

The casinos in Vegas cluster around two regions: the strip and downtown. Downtown is where we spent most of our time. With the exception of Orleans and Monte Carlo, we played all our games downtown as well. That is where most of the locals (non-tourists) game, and so the table minimum bets are more reasonable ($\$$5 or $\$$10). Almost all of them used automatic shufflers. Our typical day involved waking up early and driving downtown for breakfast. Some casinos (like El Cortez, and the D) would open quite early. We would split up and play for about one to two hours at a single place before cashing out and playing elsewhere. We mostly limited our bet spread to 5 so as to not raise suspicion, and hopped casinos often to not alert the security staff behind the eye in the sky, since they have the luxury of observing our play for prolonged periods. We found several two-deck tables, and found them to be good for counting. Some places have the so called "party pits," which open late in the evenings and are manned by scantily clad pretty women. These must be avoided, as they tend to have shitty house rules.

(image: vegas_travel1.png)

In the evenings, we would either watch one of Vegas's shows, or we would try and walk through a whole series of casinos on the strip looking for small minimum bet tables with good rules, not finding any. It was disheartening to see most strip casinos changing over to 6&#45;to&#45;5 Blackjack payouts and transitioning to continous shuffling machines to replace their shoes. Most of the advice we had found online turned out to be severely out of date for the strip. By the evening of day 5, Wes had had a magnificent streak at the Orleans, and was very satisfied with his winnings. He was in no mood to play further and risk anymore. In essence, he was quiting while he was ahead. I on the other hand, was not doing so well. 5 days and four nights in Vegas, and I was still lounging around zero net gain. Through hours of mostly pointless scouting on the strip, I had identified two small corners at two casinos with favorable two-deck tables, but with a table minimum bet size of $\$$25. One was at Excalibur, the other at Monte Carlo. Since Wes wasn't playing anymore, I didn't want to return from my card counting escapade having not played on the strip. So on the fifth night at the witching hour, I walked into Monte Carlo, sat down at a $\$$25 minimum two-deck table with only one other player at it, and fully redeemed my self-esteem in under an hour. The adventure was a success.

(image: vegas_travel2.png)

And we didn't get kicked out even once!

# Lessons and Loose Ends

There are many things that we couldn't explore or cover. For example, there are a set of popular count&#45;based modifications to basic strategy (such as Illustrious 18, and the Fabulous 4 surrenders) that allegedly improve player edge over and above what bet spreading can deliver. Our [simulation code](https://github.com/dileepvr/decks) did not notice this effect, although that could simply be due to programming errors on our part (see if you can spot any). Also, the code currently does not simulate the existence of other players at the table with varied skill levels. The position of the chief player on that table is also of consequence, as the true count at the beginning of phase one and phase two will differ by more the further down the player chain one sits at. We also couldn't cover team&#45;based strategies, such as those employed by the MIT teams. In brief, Blackjack teams consist of two kinds of players. The **spotters** sit at a single table the entire night, always betting the safe table minimum and playing basic strategy, but keeping track of the count. And the **big spenders** dress up all fancy and keep walking around the casino floor behaving rich and drunk. When a spotter measures a high true count, she secretly signals the big spender to come over to the table and bet huge sums of money. The spotter signals the big spender to move away from the table once the true count decreases again. Naturally, these teams work with common pools of money and make prior agreements regarding delegation of responsibility for losses due to mistakes. Wes and I didn't want to bother with such complications.

Looking back on the experience, I am often baffled by the visions of dirt poor street artists sweating for alms in the neon glare of the obscene opulence that is the strip. I feel fortunate to have not only a life more comfortable, but also sufficient technical competence and disposable income to try something like this in my spare time, for mirth and merriment. Casinos exist to prey on hope and superstition. The only reason they exist is because of human weakness and the technical illiteracy of the general populace. It is a tax on the poor, the desperate and the dumb. But Blackjack allows for this curious form of reverse exploitation. It is not an easy lifestyle though. The edge gained is minute and the variance is huge. One would have to start with a large bank, and play for very long hours to see any substantial benefits. And until then, one has to endure wild huge swings in the bank without losing an overall sense of actual mathematical long term expected gain. And yet, there are people who do it, not just casually, but for subsistence. I, for one, am never stepping into a casino again. But I don't regret having tried this, if only to be able to say that I did.

(image: vegas_travel3.png)


Extra Reading:

- I stole a bunch of prose from [wikipedia](https://en.wikipedia.org/wiki/Main_Page) verbatim for some of the trivia presented here.
- I would also recommend checking out the [Wizard of Odds](http://wizardofodds.com/) site.
- [This](https://www.quora.com/Las-Vegas/How-do-casinos-identify-people-on-their-blacklist) forum post on Quora is informative.
- [This](http://www.blackjackforumonline.com/content/surveillancetalks.htm) interview of an anonymous casino surveillance director is sobering, and most enlightening.

