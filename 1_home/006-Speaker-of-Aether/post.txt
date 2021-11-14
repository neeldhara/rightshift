Title: Speaker of Aether
----
Author: Dileep
----
Date: March 14, 2008
----
Tags: all experiment technology
----
Text:


So I’m sitting at my computer, immersed in a literature survey for my term project, listening to TOOL at full volume, when all of a sudden I hear a loud “dit-dit-dit-dit-deeeeet–ditditdit-dit—–dit——dit——dit”. Took me about three seconds to realize it’s coming from my speakers. So then I went, “ET!!! WOOHOOO- I KNEW IT!!!”

But, as some wise jack once said, “If wishes were horses, beggars would teleport”. I am of course referring to the [noise](https://www.freesound.org/people/RutgerMuller/sounds/50699/) certain old generation sound-systems tend to make when a nearby cellphone starts transmitting radio waves. Veterans will know that it’s a great way to predict phone calls before it actually rings. And some people have even attempted to make music with it. But one must wonder why it happens at all? A quick Google search will reveal a countless instances where the question has been addressed. Almost all of them appear in discussion forums, short, and insufficient and hand-wavy (to me at least). They all go, “Oh that’s just radio interference”. Even the Youtube video owner messes-up (”…an inch from your brain”?! :”Don’t try with headphones”?! What’s wrong with him!!!). Only a [couple](http://ask.slashdot.org/comments.pl?sid=182537&cid=15089579) [came](http://ask.slashdot.org/comments.pl?sid=182537&cid=15089200) close to helpful. But there are other things the speaker is trying to tell us. So this week, for my first post on RightShift, I’ve decided to listen closely.

The experiment involves recording and observation of sound patterns from a cellphone-speaker coupled system under various modes of operation, and an attempt to correlate to expected cellphone behavior. (You may skip to the comments section . . . now.)

THE APPARATUS:
1) My Cellphone
A SAMSUNG SGH-X160.
GSM phone with Dual Band (900/1800MHz).

2) My Speakers
Creative SBS 240, 20 KHz.

3) Standard issue aluminum foil.
Food wrapping variety. Unknown thickness. (The package didn’t say)

4) Sound-recording (Ubuntu sound recorder software, nameless chinese microphone), Imaging (GIMP) and track visualization tools (Snd 7.0).

LETS GET OUR HANDS DIRTY:
First, the basics. Let us identify all the modes of operation where one gets a response from the speakers.

1. Cellphone switched on.
2. Cellphone receives SMS or equivalent message.
3. Cellphone transmits SMS or equivalent message.
4. Cellphone gets call and cuts it while ringing.
5. Cellphone gets call and receives it, then closes it.
6. Cellphone gets call and the caller changes his/her mind while ringing.
7. Cellphone calls and cuts it while ringing.
8. Cellphone calls, connects and closes it.
9. Cellphone switches off.
10. Cellphone arbitrarily decides to interrupt TOOL when you least expect it.

The following image contains visual plots of the first 9 responses (click to enlarge, forgive the ambient noise).

(image: all_graphs1.jpg width: 1000)

The speaker input jack was disconnected from the computer in all cases.
Sorry I didn’t normalize all the axes. The volume intensity is quite hard to predict. The time-axis unit is second. I couldn’t plot response #10 for obvious reasons. We’ll dissect further shortly.
I own a speaker pair, but only the “main” one with the power button and the volume knob seems to respond to strong microwave sources (So much for the exposed wire theory). Insulating the wires with aluminum foil didn’t change a thing. However, by completely wrapping the “main” speaker with foil, I was able to completely shield it from interference. My best guess; it’s the Power Control Circuitry inside. All (most?) AC appliances employ them. The rectifier diodes must have sufficient capacitive nature to act as low-pass filters.
Note that a cellphone transmits at frequencies around 900MHz (1800MHz in some countries), well beyond human hearing. But a [GSM](https://en.wikipedia.org/wiki/GSM) network is multiplexed in time (refer: [TDMA](https://en.wikipedia.org/wiki/Time_division_multiple_access)). Every base station operates at 124 carrier frequencies, and assigns each carrier to a maximum of 8 cellphones in its neighbouring [cells](http://www.privateline.com/mt_cellbasics/) (hence the term “Cellphone”). So at any given time, only 992 (124 times 8 ) cellphones can actively communicate in a given cell! Remember to resort to SMS only, in emergencies!!
So anyway once a cellphone is assigned its carrier frequency, it shares it with seven other hypothetical phones. They all take turns to transmit. So each phone has a time-slot duration of 0.577ms to use. A GSM phone would (after carrier channel assignment) transmit radio waves in short bursts of 0.577ms length, once every 4.616ms (0.577 times 8 ). So although the bursts themselves are at 900MHz, a Fourier transform of a typical transmission would yield coefficients of significant magnitude at around 216.68Hz (1/4.616) to account for the rapid changes in average amplitude, well within human hearing range. And this is what we hear. In contrast, a [CDMA](https://en.wikipedia.org/wiki/CDMA) phone transmits more or less continuously, and is less likely to be picked up.
I didn’t consider plotting the Fourier coefficients of the recorded responses. The graphs seems to have been sampled at 20kHz, but I wouldn’t trust it (cheap extrapolators and shady [WAV](https://en.wikipedia.org/wiki/WAV) compression standards).
So this effect would not be observed on laptop speakers (no power control circuit, centralized power unit, well shielded), or headphones (passive device, wires don’t do s**t, take that Youtube guy!). The next time you’re in a rock concert, this is one more wicked reason to want to be in the pit close to the sound machines (I take no responsibility for anything this blog post inspires it’s readers to do).
People claim that the reason we don’t hear constant chatter from the base station is because despite the high-power antenna, the signal attenuates as 1/r^3 (it’s actually closer to 1/r^4 in an obstacle filled urban environment) by the time it reaches the client. (Can you imagine how sensitive the receiving antenna must be?) The cellphone however transmits at about 1 Watt (a battery powered device can’t exceed much), and is close to the speaker.
By that hypothesis, a resident close to a base station would have gone deaf by the time he/she has reached this sentence. Remember, the base-station is transmitting continuously in all carrier channels and all time slots. So there won’t be any significant amplitude changes in its signals either, just like in the CDMA case.

# THE PLOTS SPEAK:

Now let’s consider the first plot in detail.

(image: 11.jpg width: 800)

We see two distinct regions of activity, marked red and blue. The red region has a peculiar structure. There is a pattern consisting of three short bursts, the first two about 0.1 seconds apart and the third 0.3 seconds ahead of the first; and this pattern seems to repeat itself about 5.5 times.
About two seconds later, the blue region begins with about three broad bands of transmissions followed by 3 short bursts separated by 0.125 seconds and 9 bursts separated by 0.25 seconds.
When a cellphone is switched on, it scans all the channels looking for the strongest one in the cell. After selecting a channel the phone then identifies itself. It sends its phone number, electronic serial number, and home system ID, among other things. After which the cell might need to synchronize with the base-station clock, so it can latch onto the beginning of a time-slot (the phone clock and the station clock are independent). To recognize an empty/available time-slot, it needs to decode the station transmissions and identify the busy/idle bit. Unfortunately, we are unable to capture the signals our phone receives. So we are restricted to guessing what the phone seems to be doing when it only transmits. The registration process is meant to happen every so often, just in case we move into a area where the old base station becomes too weak, or we change cells, et cetera. In fact, when I wrapped the cellphone in Al foil, it determined that the signal is too weak, and declared “Limited Service”. Upon removing the foil, it took about 15 seconds to recover full signal status (also accompanied by speaker noise).

Note that the patterns in the red and blue regions also appear in all the other plots (except the last one).

(image: all_graphs_small1.jpg width: 1000)

Note that the red region appears in the beginning of all nine cases. The repeating pattern maintains its time-duration but the number of repetitions vary. In all red cases, the cellphone is expected to communicate its identity to the base station and acknowledge some state or query; either just to let the station know it exists in this cell, or to let it know that it wishes to ‘make a call to’/’send a message to’, or has ‘received message from’/'call from and is ringing’, or that it’s signing off, and so forth.

The blue region appears at the end of the first eight cases (it deactivates in the ninth case). All of them consist of 9 bursts 0.25 seconds apart. But the prefixes have different number of denser bursts and broad transmissions. This is reminiscent of some kind of synchronization activity, as if the cellphone returns to idle state after each action, relatching onto “aether” clock. The number of broad streams is highest in the first case, where the cellphone has just been turned on, and is groping in the dark without a past reference.

# UNSOLVED STUFF:
The regions of the plot where a call is in progress look completely blocked out. The phone does need to continuously communicate, lest some part of the conversation is missed! However, a zoomed-in version reveals another repeating pattern about 1.2 seconds in length. This number doesn’t seem to fit any of the previous derivations.

(image: convo_zoom11.jpg width: 800)

Another level of zoom reveals more structure.

(image: convo_zoom21.jpg width: 800)

The reader may fire at will.

# AFTERTHOUGHT:
The reason I named the post “Speaker of Aether” was because to me, the speakers seem to reveal untold conversations machines involve in, not meant for us mortals, through a medium inaccessible to biological beings. There is symbolism here. Since the communication revolution and the cellphone boom (especially in this country), the cellphone has stood for the black-box gift of technology, which mankind was quick to embrace, but failed to appreciate, and took for granted. Can’t really blame them. When one reads of Richard Feynman fixing a noisy radio in his teens, one wonders if such a thing is even possible in today’s accelerated society. Every thing is bigger, more complicated, and smaller in scale. Everything is changing and evolving at an [enormous rate](https://en.wikipedia.org/wiki/Accelerating_change). We should be jealous of our generation-old professors, who in their time built AM radio receivers with mere LRC circuits. The layman today is easily alienated by the technosphere.
So this exercise, in some sense is profound in that it’s a phenomena not resulting by design, and yet involving so many cool mini-systems and processes any college student is exposed to. It’s easily reproducible from the comfort of a hostel room or residence. It’s these little things; HAM radio clubs, recreational programming, reverse engineering sessions, astronomy nights, and inter-hostel robotics contests, that help keep a student of technical studies motivated and in form.

# OTHER FUNKY THINGS TO TRY OUT:

* Dismantle speakers and use the foil to isolate the responsible components that pick-up microwaves. (I’m not nearly confident enough to try it with my only speakers! They’re still in working condition…)
* Map pick-up intensity to position and orientation of cellphone. The antenna is clearly anisotropic. Maybe one can guess its shape if one knew the radiation pattern.
* Repeat experiment on monitors (both CRT and TFT). The display on the CRT definitely responds to cellphone chatter.
* Connect speakers to microphone jack and use them to communicate verbally via GTalk or Ventrilo. Not the best substitute, but hey! There’s always Morse Code. ^_^
Update: For more on EM-radiation related technology, check out Ms. [Ouellette’s entry](http://twistedphysics.typepad.com/cocktail_party_physics/2008/10/repost-ghost-in.html).

*****

## Old comments from the w0rdpress days

**Polar said:**
*15 Mardh, 2008 at 3:29 pm*

Funky.

I reproduced the cellphone switching on and off patterns (hardly necessary- It happens so often I know them by heart now), and the red section matches up to the limit of my hearing. The blue’s a bit off, and the gap between the red and the blue when the phone switches on is a lot more than two seconds (about eight). I have no idea why syncing on to Æther clock (blue) takes longer. This is mountainous _and_ densely populated terrain, though.

Are the numbers (124 carrier frequencies, 8 phones per frequency, 0.577ms per phone etc) GSM standards? I have a sneaking feeling my local service provider’s bending the rules, taking more than it can service efficiently.

The “ingenuity gap” you mention really frightens me. There are an astonishing number of black-boxes around, and explanations like this one go a long way towards reassuring us that the world is not magic. (http://cosmicvariance.com/2005/10/10/the-world-is-not-magic/) Delve more often into aether speak- someone needs to.

As a side note, there appears to be enough variation in the patterns for me to apply the Huffman algorithm(http://en.wikipedia.org/wiki/Huffman_algorithm); but coolness aside, would anyone really use the cellnoise code?

I _love_ this blog.

**Traums said:**
*28 May, 2008 at 10:40 am*

The time delay before syncing is probably highly dependent on the make of your cellphone. Older makes might just be slow and newer java phones run such bad code it takes forever to boot, load applets, fire-up buffers, yada yada before it becomes aware its a cellphone.

I don’t know how good our cellphones are in adapting to an international change in standards. If all your phone conversations are noisy, then your suspicion might be justified.

**[The 1974 Revelation << Random Shit Stall](https://randomshitstall.wordpress.com/2009/04/13/the-1974-revelation/) said:**
*13 April, 2009 at 4:54 pm*

[...] the negative feedback screech from the bose speakers at CLT, creepy elevator music at the library, GSM cellphone signals picked-up by the computer speakers, ball-point pens scratching paper during quiz-hour, and waves dying at the [...]
