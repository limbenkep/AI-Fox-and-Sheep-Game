# AI-Fox-and-Sheep-Game  
This project is in zip form because it include jar libraries.  

# FoxGame rules
The agents will send moves to each other by communicating through an intermediary server program called the monitor. The monitor allows us to watch the game in progress.

The Rules of the Game
Because this implementation of the game is inspired by the Swedish version, the two players control foxes and sheep. The goal of the fox player is to eat the sheep. The goal of the sheep player is to fill a pen, consisting of the top 9 positions on the board. The rules are described in much more detail below.

Board Layout
The board consists of a total of 33 positions, arranged to form a plus (+) sign consisting of 5 squares. When the game starts, the bottom 20 positions are occupied by sheep. The top two corners are occupied by foxes.

Starting board

Unit Movement
Any unit may only move to an empty position. In most cases, the destination must also be an adjacent position. Fox jumps (see below) are the only exceptions. Some positions allow movement up/down and left/right. Some positions also allow diagonal movement. The board indicates which positions are regarded as adjacent by drawing a line connecting the positions. Units may only move along these lines.

A fox may jump over a sheep in a straight line. The sheep must be directly adjacent to the fox. The fox will thus move a total of two positions with one jump. A contiguous sequence of any number of jumps is allowed. This means that a regular move is never allowed to follow any number of jumps.

Note that a sheep is removed as soon as a fox jumps over it. Hence it is impossible to jump over the same sheep twice.

A sheep may never move back again. Back, in this case, means downward, away from the pen. In other words, it can only move forward (toward the pen) or sideways.

With the exception of fox multi-jumps, a player may only perform one move per turn. The fox player gets to make the first move.

Fox jumping over a sheep

This shows a fox jumping over a sheep. The sheep will be removed (see unit elimination below).

Fox jumping over multiple sheep

This shows a fox performing multiple jumps in a sequence. All the sheep will be removed.

Fox trying to end a sequence of jumps with a regular move

Here the fox is trying to end a sequence of jumps with a regular move. This is illegal.

Unit Elimination
A sheep is removed from the game if, and only if, a fox jumps over it.

A fox is removed if, and only if, it has no valid moves to make.

Win conditions
There is one way for the foxes to win and two ways for the sheep to win.

Sheep win if:

(1) The pen is full, meaning that none of the nine positions are empty.
(2) There are no foxes left in the game.
Foxes win if:

(3) There are not enough sheep to fill the pen (by themselves*).
* Since foxes count when determining whether the pen is full, this means that the sheep could, in principle, still win if the number of sheep units plus the number of fox units is equal to or greater than 9. However, the win condition is satisfied whenever the number of sheep is too low for them to satisfy (1) by themselves.

In addition to these win conditions, a player can also win as a result of the opponent getting disqualified. A player is disqualified if it tries to perform an illegal move, if it does not generate a new move on time - meaning that it doesn't conform to the allotted time slice - or if it makes a move that causes a deadlock.

Note that draws are possible.

The goal positions for sheep

The top 9 positions (encircled in the picture) make up the pen. The goal for sheep is for each of the 9 positions to be occupied.

Deadlock
If the current board configuration is an element in the set of previous configurations for this instance of the game, then the player that caused this state has caused a deadlock. In other words, a particular board state may only occur at most once per match. If a player makes a move that produces a board state identical to a previous state, then that player is disqualified.

Timeslice
The monitor also imposes a time limit on the players. That is, they have some amount of time during which they are allowed to plan the next move. An agent is allowed to submit a move early. In that case, the extra time is discarded, and the opponent's turn starts earlier. Exceeding the time slice is illegal.

An agent is (of course) allowed to plan its next move while it is waiting for the opponent to move, but don't forget that the opponent might finish early.
