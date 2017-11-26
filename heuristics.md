# Heuristic Analysis

> Trying to figure out which 🤔 strategy wins the game 🎯

_Note:_ During the development of these heuristics it showed that the sample size of **10** matches for the _random_ player results in up to `40%` difference between different tournaments when running the same heuristic. Final decision on best strategy should be performed on a way larger set of games.
In a tournament where the same strategy was applied twice the results were: (`wins1 : wins2` of the same strategy) `7:10`, `5:6`, `8:6`, `7:8`, `4:6`, `5: 3`, `4:6`.

## Overview

This table provides an overview of 3 tournaments with the heuristics described below. Multiple tournaments were run to average out the above mentioned randomness due to low sample size.

Columns for the stragies are provided as `Wins:Losses`

| Match  | Opponent  | AB_Improved  | Strategy 1  | Strategy 2  | Strategy 3  |
|---|---|---|---|---|---|
| 1  | Random       |  19:11 | 25:5  | 24:6  | **27:3**  |
| 2  | MM_Open      | 19:11  | 20:10  | 20:10  | **22:8**  |
| 3  | MM_Center    | **24:6**  | 21:9  | 21:9  | 23:7  |
| 4  | MM_Improved  | 15:15  | 18:12  | **20:10**  | 18:12  |
| 5  | AB_Open      | 20:10  | 16:14  | **18:12**  | 16:14  |
| 6  | AB_Center    | 16:14  | **17:13**  | 16:14  | **17:13**  |
| 7  | AB_Improved  | 16:14  | **17:13**  | 11:19  | 14:16  |
|   |   |   |   |   |   |
| Win Rate  |   |  61.4% | 63.8%  | 61.9%  | 65.2%  |

> Overall the third strategy seems to perform the best.

## Strategy 1

`moves(player) - moves(opponent)`

Starting with a _classic_ to have a baseline for performance. This heuristic tries to make sure the player always has more available moves than the adversary.

## Strategy 2

`0.5 * (moves(player) - moves(opponent)) + uniqe_moves(player)`

This one tries to implicitly bring the player to generate a barrier between itself and the adversary. By boosting the score of moves that only the player can take any actions that lead to unique moves will be preferred. I imagine this would be especially relevant near the end of the game. In the beginning players might not share moves at all because of different starting points. For that reason the _Strategy 1_ is implemented as a baseline as well with a lower weight.

## Strategy 3

`uniqe_moves(player) / moves(opponent)`

Trying to further push _Strategy 2_. The agent should behave way more aggressive with this stance. Putting the opponents move in the denominator will reward moves that lock the opponent in. This in turn results in more unique moves for the agent and further increase the score.