#Liars Dice
People have vices. One of those is gambling. Whether it's a poker night, a super bowl bet, or picking investments, everyone gambles. This isn't anything new either, people have been gambling for thousands of years [1]. In recent years, as compute power has gotten more accessable, incredible bodies of analysis have been produced to better understand the games we wager on (or just play for fun). Given how much we like to gamble, this is hardly suprising- and we're not even considering the quantity of money involved. Poker, fantasy football, and the stock market are all great examples of games that are saturated with near-infinite technical anaysis available. While it might not all be of the highest quality, there is no lack of Poker strategy books, blogs spouting stock market tips, or insider fantasy scoops. Quality models for popular games such as poker were created by people who are certainly much smarter than you or I. While i'm confident there's more innvation to occur in a game like poker, i'll go out on a limb and speculate that it is unlikely I will be the one doing it. What might be possible however, is using existing knowledge of popular games to guide discoveries about games outside the spotlight. That's what i'll be writing about today, with my game of choice being Liars Dice. 

My goal is to gain a practical advantage while i'm playing. Liars dice is a game I play with my friends: I dont need a series of equations to model liars dice. I need strategies to win games, or atleast to help. I'm not a mathmatician, nor an expert poker player. But I dont think I need to be, in order to gain some small advantages, that will hopefully compound across an entire game. This writing attempts to document my trail of learning, for a game that's isn't as discovered as Go or Chess. 

# Rules of the Game

You can play with any number of players, but i'm going to keep my focus to a heads-up game of liars dice with only a single other oppenent. Each player starts with 6 dice, and lose dice as the game goes on. Each round begins with all players rolling their dice in secret (usually covered by a cup). The players alternate making "bids" about the total dice pool that has been rolled. For example, I would begin the round by bidding "two 2's", claiming that I beleive there to be atleast two 2's in the 12 total dice rolled (My 6 which I can see, plus my oppenents 6, which are hidden.). My hypothetical oppenent, can either increment the face count up (eg. two 3's, or two 5's), or increment the dice count (three 2's), or both (four 6's). If the dice count gets incremented, the face count can be lowered- 3 six's -> 4 one's, but not vice versa. This leads to a dynamic where the bid's are growing higher and higher, until they start to get unreasonable. At any point, a player may call bullshit on the previous bid. When this happens, all player reveal their dice, verifying the bid, and the player who was incorrect must discard a die. Each die that is lost is information lost for previous rounds, which makes mounting combacks quite difficult.  

# Strategy

The simple gameplay of liars dice invites complex strategy, due to the ever changing information dynamics. In game theory, Liars Dice would be labeled an asymetric game. Similar to poker, oppenents have differing amounts, and quality, of information at any given time. Unlike a game like chess, where all game state is visible to all players, the decisions made in Liars Dice require making guesses about hidden information.

As you might have been able to pick up from the name, Liars Dice requires some amount of bluffing. If you only bid representing the dice in your hand, you'll be able to rope in rounds when your oppoenent invevitably calles you- but after multiple hands against a diligent oppenent they will take note, and become more and more unlikely to call you. On the flip side, if you only ever lie about the dice you hold, you will quickly start to get called often. This isn't just a broad strategy note, it applies to indiviudal hands as well. If you always bluff 6's with low rolls, you gifting your oppenent an unnecesary edge. All of these strategys would be considered a "Pure Strategy", and in a game like liars dice, are open to exploitation.

Now, if any rounders are reading this, they've surely started to recognize Liar's Dices' parallels to Poker. A lovely coincidence given the ammount of Poker knowledge we can tap into.  

# GTO

The holy grail of Texas Hold'em play is a mathmatically derived Mixed Strategy dubbed "Game Theory Optimal", or GTO. "GTO Poker" describes a theoretial strategy that when played perfectly, is mathmatically unexploitable- Over infinite hands, you could never lose money, no matter how adaptable your opponent is to your strategy.  In practice, GTO play can be thought of as playing though a function: Input the table state, output a list of actions, some of which are likely than others. Generalizing GTO into a more general game philosphy: In order to play defencively against your opponent, multiple actions must be considered. The "ideal" decision cannot get choosen every time, it must be balanced by some frequency of suboptimal plays. 

This is dubbed a "Mixed Strategy" in game theory. A mixed strategy dictates probabilities to act on a range of actions, for any given state. Compared to a Pure Strategy, where with a given input a player will always have a discrete output, a mixed strategy often won't gaurentee a specific output for any given input.  

In Texas Hold'em, one of the easier to understand GTO concepts is pre-flop strategy. Pre-flop represents your first action after looking at your 2 hole cards. A good preflop player can boil the table state into 3 variables: Cards, Position, and incoming action, and act accordingly. For example, being 1st to act (Also called Under The Gun), with a suited K8, we'd raise 87.5% of the time, and fold the other 12.5% of the time. If we we're sitting in cuttoff, which acts later, we would raise that hand 100% of the time! In fact, even if we got dealt K3 suited (A noticably worse hand), we would still raise 100% of the time in that position! Model this function across every possible hand you could be dealt, and you end up with a GTO preflop strategy. Visualized, it looks something like this: 

Now, the question is: If you can't lose money playing GTO, why doesn't everyone play GTO? Well, going back to the "Theoretical" designation I gave GTO, it's impossible to play perfect GTO poker. Playing perfect GTO is no different than always knowing the best chess move. Easier said than done. While always sticking to GTO is impossible, we can still aim to adapt GTO strategy into our play, making us slightly more unexploitable than our opponent. 

If we can model this in a game like Poker, could we do something similar in Liars Dice?

# Nash Equilibrium

Here, i'm going to ask you, the reader, to humor me for a second. 

Imagine two robots, Tim and Tom, sat at a table with chips and a deck of card. They're both infinitely smart, and are thus perfect poker players, able to execute GTO play to a T. Being infinitely smart, Tim knows Tom understands and plays GTO. He knows that GTO is defensive, and is mathmatically unexpolitable if played correctly. Tim knows Tom will play it correctly, so the best he can do it be unexploitable himself. Tom kknows that he's unexploitable, but he also knows Tim will play the same. Lets say we throw them the bone of infinite time, and where do we end up? Nowhere. They both play perfectly, and over infinite hands, neither wins a dime, unable to adapt their perfect strategy against their oppenents mirror strategy. 

In broader Game Theory terms, we can call this a Nash Equilibirum. Nash Equilibrium's occur in games when opponents know each other's strategies, and still have nothing to gain from changing their own strategy. Boiling it down, even assuming your oppenent completely understands your strategy, there exists no strategy to take advantage of you; Leaving them with... the exact same strategy. 

I'd like to again emphasize that this is theory in a vacuum. At the casino, nobody plays perfect GTO. In fact, most players don't even get close, and aren't really trying to.  We gain our advantage by aiming to be unexploitable, while exploiting our opponents. While conceptual poker can be solved to an equilibrium, an actual game of poker is very far from it.


Understanding these concepts can lead to advantages in poker, but what about Liars Dice? More specifically, does Liars Dice even have a Nash Equilibrium? 

It has too. John Nash proved that for any finite game, there exists atleast one Nash Equilibrium. This was published in his 1950's paper "Non-Cooperative Games", and unsupringly, is why the equilibrium is named after him. 

# Back to Liars Dice.
While a traditional game of liars dice consists of two players playing multiple rounds until a player loses all of their dice, we can discect the game into "minigames". Instead of thinking of "Liars Dice" as one game, we can think of it as a set of individual games, where the outcome of the previous dictates the start of the next. The first round can be defined as a 6-Dice vs 6-Dice game, the next a 6v5, and the next either a 6v4, or a 5v5 depending on the winner of the previous. This chunking of the dice state allows us to easily analyze the impacts of the constantly changing information dynamics. Each minigame will have it's own Nash Equilibirum, with the overall Nash Equilibrium being the set of respective minigame Equilibriums.

I lucked out here: someone else has already done it! THNG has an amazing blog post where he calculates the Equilibrium strategies for a 1v1 game, as well as 2v1 and 1v2. We can see the outputs below.

But what about the rest of the minigames? 3v1? 5v2? 6v2? As the dice count grow, the computational complexity needed to calculate the equilibrium grows exponentially. Even in a game as low as 2v1, we still are reaching the upper limit of what is amateurly calculatable, and we need to move into techniques that approximate the equilibrium strategy. 


[1] https://en.wikipedia.org/wiki/Gambling#History
