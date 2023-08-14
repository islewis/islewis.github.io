#Liars Dice
Liars dice is an intiguing dice game that's oddly similar to poker. The rules are similar,...

The simple gameplay of liars dice invites complex strategy, due to the ever changing information dynamics. In game theory, Liars Dice would be labeled an asymetric game. Similar to poker, oppenents have differing amounts, and quality, of information at any given time. Unlike a game like chess, where all game state is visible to all players, the decisions made in Liars Dice require making guesses about hidden information.

As you might have been able to pick up from the name, Liars Dice requires some amount of bluffing. If only bid aggresively representing the dice in your hand, you'll be able to rope in rounds when your oppoenent invevitably calles you- but after multiple hands against a diligent oppenent they will take note, and become more and more unlikely to call you. On the flip side, if you only ever lie about the dice you hold, you will quickly start to get called often. This isn't just a broad strategy note, it applies to indiviudal hands as well. If you always bluff 6's with low rolls, you gifting your oppenent an unnecesary edge. All of these strategys would be considered a "Pure Strategy", and in a game like liars dice, are open to exploitation.

In order to play defencively against your opponent, multiple actions must be considered. The "ideal" decision cannot get choosen every time, it must be balanced by some frequency of suboptimal plays. This is what game theory calles a "Mixed Strategy". A mixed strategy dictates probabilities to act on a range of actions, for any given state. Compared to a Pure Strategy, where with a given input a player will always have a discrete output, a mixed strategy often won't gaurentee a specific output for any given input.  
# GTO
The holy grail of Texas Hold'em play is a mathmatically derived Mixed Strategy dubbed "Game Theory Optimal", or GTO. "GTO Poker" describes a theoretial strategy that when played perfectly, is mathmatically unexploitable- Over infinite hands, you could never lose money, no matter how adaptable your opponent is to your strategy.  In practice, GTO play can be thought of as playing though a function: "Input" the table state, "output" a list of actions, some of which are likely than others. Now, im sure you're wondering: If you can't lose money playing GTO, why doesn't everyone play GTO? Well, going back to the "Theoretical" designation  I gave GTO, it's pretty fucking hard to always play. Playing perfect GTO is no different than always knowing the perfect chess move. Even for the great Magnus, this is a pretty steep feat. While always sticking to GTO is impossible, we can still adapt concepts into our play.

So.... how? In order to keep this article light, we can look at positions with a smaller number of variables. In poker, this most tanslates to pre-flop strategy, which represents your first action after looking at your 2 hole cards. A good preflop player can boil the table state into 3 variables: Cards, Position, and incoming action, and act accordingly. For example, being 1st to act (Also called Under The Gun), with a suited K8, we'd raise 87.5% of the time, and fold the other 12.5% of the time. If we we're sitting in cuttoff, which has a later action, we would raise that hand 100% of the time! In fact, even if we got dealt K3 suited (A noticably worse hand), we would still raise 100% of the time in that position! Model this function across every possible hand you could be dealt, and you end up with a GTO preflop strategy. Visualized, it looks something like this.  

If we can model this in a game like Poker, could we do something similar in Liars Dice?
# Nash Equilibrium
If we look at GTO in terms of broader game theory, we could classify two players each playing GTO as a Nash Equilibirum. Nash Equilibrium's occur in games when opponents know each other's strategies, and still have nothing to gain from changing their own strategy. Boiling it down, even assuming your oppenent completely understands your strategy, there exists no strategy to take advantage of you; Leaving them with... the exact same strategy. Now, using Nash Equilibriums to describe poker, it formalizes my previous explaination of GTO being "Unexploitable". Even if your oppenent knows you play perfect GTO, their best option is to do the exact same thing, in which case you will come out dramatically even (thus, the "equilibrium" part). However, i'll again emphasize that this is theory in a vacuum. At the casino, nobody plays perfect GTO. We gain our advantage by aiming to be unexploitable, while exploiting our opponents. While conceptual poker can be solved to an equilibrium, an actual game of poker is very far from it.

Understanding these concepts can lead to advantages in poker, but what about Liars Dice? More specifically, does Liars Dice even have a Nash Equilibrium? 

It has too. John Nash proved that for any finite game, there exists atleast one Nash Equilibrium. This was published in his 1950's paper "Non-Cooperative Games", and unsupringly, is why the equilibrium is named after him. 

# Back to Liars Dice.
While a traditional game of liars dice consists of two players playing multiple rounds until a player loses all of their dice, we can discect the game into "minigames". Instead of thinking of "Liars Dice" as one game, we can think of it as a set of individual games, where the outcome of the previous dictates the start of the next. The first round can be defined as a 6-Dice vs 6-Dice game, the next a 6v5, and the next either a 6v4, or a 5v5 depending on the winner of the previous. This chunking of the dice state allows us to easily analyze the impacts of the constantly changing information dynamics. Each minigame will have it's own Nash Equilibirum, with the overall Nash Equilibrium being the set of respective minigame Equilibriums.

Luckily, 