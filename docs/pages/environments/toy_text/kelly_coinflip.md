---
AUTOGENERATED: DO NOT EDIT FILE DIRECTLY
layout: env
title: Kelly Coinflip
grid:
   - Action Space: Discrete(25000)
   - Observation Space: Tuple(Box([0.], [250.], (1,), float32), Discrete(301))
   - Import: <code>gym.make("KellyCoinflip-v0")</code>
---
The Kelly coinflip game is a simple gambling introduced by Haghani & Dewey 2016's
'Rational Decision-Making Under Uncertainty: Observed Betting Patterns on a Biased
Coin' (https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2856963), to test human
decision-making in a setting like that of the stock market: positive expected value
but highly stochastic; they found many subjects performed badly, often going broke,
even though optimal play would reach the maximum with ~95% probability. In the
coinflip game, the player starts with $25.00 to gamble over 300 rounds; each round,
they can bet anywhere up to their net worth (in penny increments), and then a coin is
flipped; with P=0.6, the player wins twice what they bet, otherwise, they lose it.
$250 is the maximum players are allowed to have. At the end of the 300 rounds, they
keep whatever they have. The human subjects earned an average of $91; a simple use of
the Kelly criterion (https://en.wikipedia.org/wiki/Kelly_criterion), giving a
strategy of betting 20% until the cap is hit, would earn $240; a decision tree
analysis shows that optimal play earns $246 (https://www.gwern.net/Coin-flip).

The game short-circuits when either wealth = $0 (since one can never recover) or
wealth = cap (trivial optimal play: one simply bets nothing thereafter).

In this implementation, we default to the paper settings of $25, 60% odds, wealth cap
of $250, and 300 rounds. To specify the action space in advance, we multiply the
wealth cap (in dollars) by 100 (to allow for all penny bets); should one attempt to
bet more money than one has, it is rounded down to one's net worth. (Alternately, a
mistaken bet could end the episode immediately; it's not clear to me which version
would be better.) For a harder version which randomizes the 3 key parameters, see the
Generalized Kelly coinflip game.