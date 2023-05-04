Download Link: https://assignmentchef.com/product/solved-csci-561-foundations-of-artificial-intelligence-homework-2
<br>
<strong>Project description</strong>

In this project, we will play the game of <strong><em>Checkers</em></strong>, the classic strategy board game. It is a version of the game <em>draughts</em> and is also called <strong>American checkers</strong> or <strong>straight checkers</strong>. It uses an 8×8 checkered gameboard. Each player starts with 12 game pieces placed on the dark squares of the side of the gameboard closest to them, as can be seen in the figure above. The side with the darker colored pieces is usually called ‘Black’ and the side with the lighter color is ‘White’. Black opens the game. The pieces move diagonally forward and can capture opponent’s pieces by jumping over them. Whenever a piece reaches the opposite side of the board, it is crowned <strong><em>king</em></strong> and gains the ability to move/capture both forward and backward. The game ends when one side wins or a draw condition applies.

One side wins when the opponent cannot make a move, which can happen in two ways: 1) All the opponent’s pieces have been captured. 2) All the opponent’s pieces are blocked in some way. A draw also applies in two cases: 1) Over 50 consecutive turns, there has been no material change on the board (no pieces were captured or crowned), or 2) The same exact position on the board has been reached 3 times (i.e., all pieces of the two players combined have been in the exact same places 3 times).

More details on the game can be found at <u>https://en.wikipedia.org/wiki/English_draughts</u> and we will also go over the gameplay for you below. Beware that many variants of this game exist, so please adhere to the rules described in this homework carefully.

<strong>This 8×8 variant of checkers is <em>solved</em></strong>. Which means that when both players play a perfect game, the game comes to a draw. If you’re interested, you can check out the paper at the following link: <u>https://www.researchgate.net/publication/231216842_Checkers_Is_Solved</u>

This also means that checkers doesn’t have a first or second player advantage, and it will always lead to a draw with perfect play. Note that we do not expect your program to play perfectly, nor will this be necessary to succeed at this assignment, but we wanted to note this so that you know that there is no advantage to the player that gets the first move.




<strong><u>Setup of the game</u></strong>:




The setup of the game is as follows:

<ul>

 <li>Simple wooden pawn-style playing pieces, sometimes called ‘<em>men</em>’.</li>

 <li>The board consists of an 8×8 grid of squares.</li>

 <li>Players’ sides are situated across the board from each other.</li>

 <li>The first row of squares on each player’s side is usually called the ‘<em>king’s row</em>’. When an opponent’s piece reaches this row, it will be crowned ‘<em>king</em>’.</li>

 <li>Each player has a set of 12 pieces in a distinct color, which are placed on the 12 closest dark squares on their side of the board.</li>

</ul>




Here’s the visualization of this setup, as we will use in this homework:










<strong><u>Play sequence:</u> </strong>




We first describe the typical play for humans. We will then describe some minor modifications for how we will play this game with artificial agents.




<ul>

 <li>Create the initial board setup according to the above description.</li>

 <li>Players randomly determine who will play black/or the darker color. Black will play first.</li>

 <li>Pieces can move only diagonally. Regular pieces can only move forward. Pieces that have previously been crowned ‘king’ by reaching the king’s row of their opponent can move diagonally both forward and backward.</li>

 <li>Each player’s turn consists of moving a single piece of one’s own color in one of the following plays:

  <ul>

   <li><u>A simple move:</u>

    <ul>

     <li>Move the piece to any diagonally forward adjacent empty square. (King pieces can also move to one of the adjacent backward diagonals.) <strong>(Note: In this kind of play, the pieces can move only one square.) </strong></li>

     <li>This move ends this player’s turn, even if the move results in a position that makes one or more subsequent jumps possible (see below for jumps).</li>

    </ul></li>

   <li><u>One or more jumps, capturing one or more of the opponent’s pieces <strong>(Note: If a</strong></u><strong> <u>jump is possible at any point in the turn, it is mandatory)</u></strong><u>:</u>

    <ul>

     <li>An adjacent piece of the opponent in any of the allowed diagonal directions, i.e., forward-left and forward-right (and also backward-left and backward-right for king pieces) can be jumped over if there is an empty square on the other side of that piece.</li>

     <li>After the jump, the piece that was jumped over is “captured” (eliminated from the game).</li>

     <li>Place the piece in the empty square on the opposite side of the jumped piece.</li>

     <li>All jumping moves are compulsory. Every opportunity to jump must be taken. In the case where there are different jump sequences available, the player may choose which sequence to make, whether it results in the most pieces being taken or not. (This means that a player is not allowed to make a sequence of one or more jumps whose end result would still allow her/him/it to jump some more.)</li>

    </ul></li>

   <li>If a piece has reached the opposing king’s row, it is crowned ‘king’ and can now also move backwards in following turns.</li>

   <li>If the current play results in a board where the opponent has no pieces left or cannot move any of their remaining pieces, the acting player wins. Otherwise, play proceeds to the other player.</li>

  </ul></li>

</ul>




In the image below, we show examples of valid moves (in green) and invalid moves (in red) for a regular and a king piece, as well as the different jump scenarios for a given toy scenario. A regular piece can only move in forward diagonals while a ‘king’ (with the crown symbol on it) can also move backward.




For the simple jump scenario given on the right, the blue piece has to choose between two different jump scenarios. After jumping over red piece 1, it can either continue jumping right and capture red piece 3 or choose to go left instead and capture red piece 2. Therefore, it is possible for the blue piece to switch directions as it fulfils a jump sequence during a play. Note that, the blue piece cannot stop after making the jump over red piece 1 since, if a jump is possible at any point in the play, it has to be made.










<strong><u>Playing with agents</u> </strong>




In this homework, your agent will play against another agent, either implemented by the TAs, or by another student in the class. For grading, we will use two scenarios:

<ul>

 <li><strong>Single move:</strong> Your agent will be given in input.txt a board configuration, a color to play, and some number of seconds of allowed time to play one move. Your agent should return in output.txt the chosen move(s), before the given play time has expired. Play time is measured as total CPU time used by your agent on all CPU threads it may spawn (so, parallelizing your agent will not get you any free time). Your agent will play 10 single moves, each worth one point. If your agent returns an illegal move, a badly formatted output.txt, or does not return before its time is up, it will lose the point for that move.</li>

 <li><strong>Play against reference agent:</strong> Your agent will then play 9 full games against a simple minimax agent with no alpha-beta pruning, implemented by the TAs. There will be a limited total amount of play time available to your agent for the whole game (e.g., 100 seconds), so you should think about how to best use it throughout the game. This total amount of time will vary from game to game. Your agent must play correctly (no illegal moves, etc.) and beat the reference minimax agent to receive 10 points per game. Your agent will be given the first move on 5 of the 9 games. In case of a draw, the agent with more remaining play time wins.</li>

</ul>

<strong><u>Draw condition:</u></strong> The game will be called a draw if for 50 consecutive turns: 1) The number of pieces on the board haven’t changed, and 2) The status of the pieces on the board haven’t changed (i.e., none has been crowned king). A draw will also be called if the same exact position on the board has been reached 3 times.




Note that we make a difference between single moves and playing full games because in single moves it is advisable to use all remaining play time for that move. While playing games, however, you should think about how to divide your remaining play time across possibly many moves throughout the game.




In addition to grading, we will run a competition where your agent plays against agents created by the other students in the class. This will not affect your grade. The top agents will be referred to a contact at Google for an informal introduction. There will also be a prize for the grand winner.




<strong><u>Agent vs agent games:</u> </strong>




Playing against another agent will be organized as follows (both when your agent plays against the reference minimax agent, or against another student’s agent):




A master game playing agent will be implemented by the grading team. This agent will:

<ul>

 <li>Create the initial board setup according to the above description.</li>

 <li>Assign a player color (black or white) to your agent. The player who gets assigned black will have the first move.</li>

 <li>Then, in sequence, until the game is over:

  <ul>

   <li>The master game playing agent will create an input.txt file which lets your agent know the current board configuration, which color your agent should play, and how much total play time your agent has left. More details on the exact format of input.txt are given below.</li>

   <li>We will then run your agent. Your agent should read input.txt in the current directory, decide on a move, and create an output.txt file that describes the move (details below). Your time will be measured (total CPU time). If your agent does not return before your time is over, it will be killed and it loses the game.</li>

   <li>Your remaining playing time will be updated by subtracting the time taken by your agent on this move. If time left reaches zero or negative, your agent loses the game.</li>

   <li>The validity of your move will be checked. If the format of output.txt is incorrect or your move is invalid according to the rules of the game, your agent loses the game.</li>

   <li>Your move will be executed by the master game playing agent. This will update the game board to a new configuration. o The master game playing agent will check for a game-over condition. If one occurs, the winning agent or a draw will be declared accordingly.</li>

   <li>The master game playing agent will then present the updated board to the opposing agent and let that agent make one move (with the same rules as just described for your agent; the only difference is that the opponent plays the other color and has its own time counter).</li>

  </ul></li>

</ul>

<strong><u>Input and output file formats:</u> </strong>




<strong>Input:</strong> The file input.txt in the current directory of your program will be formatted as follows:




First line:  A string SINGLE or GAME to let you know whether you are playing a single move (and can use all of the available time for it) of playing a full game with potentially many moves (in which case you should strategically decide how to best allocate your time across moves).

Second line:  A string BLACK or WHITE indicating which color you play. Black will always start the play with its pieces placed at the top of the game board, with white on the bottom, as given in the above images.

Third line:  A strictly positive floating point number indicating the amount of play time remaining for your agent (in seconds).

Next 16 lines: Description of the game board, with 16 lines of 16 symbols each:

<ul>

 <li>w for a grid cell occupied by a white regular piece</li>

 <li>W for a grid cell occupied by a white king piece</li>

 <li>b for a grid cell occupied by a black regular piece</li>

 <li>B for a grid cell occupied by a black king piece</li>

 <li>. (a dot) for an empty grid cell</li>

</ul>




For example:

SINGLE

WHITE

100.0 .b.b.b.b b.b.b.b. .b…b.b ….b… ……..

w.w.w.w. .w.w.w.w w.w.w.w.

In this example, your agent plays a single move as white color and has 100.0 seconds. The board configuration is just the one from the start of the game, after black has made the first move.

<strong>Output: </strong>The format we will use for describing the square positions is borrowed from the algebraic notation used for chess, where every column is described by a letter and every row is described by a number. The position for a given square is given as the concatenation of these. Here’s a useful visualization on how we identify each square for the 8×8 checkers board:







Image from ichess.net

As an example, in the input sample given above, black has moved their piece from position d6 to e5. Note that for checkers, valid moves will always land in dark squares.




Using the above notation for the squares on our gameboard, the file output.txt which your program creates in the current directory should be formatted as follows:




1 or more lines: Describing your move(s). There are two possible types of moves (see above):




<strong>E FROM_POS TO_POS</strong> – Your agent moves one of your pieces from location FROM_POS to an adjacent empty location (on the diagonal) TO_POS. FROM_POS and TO_POS will be represented using the notations explained above, by a lowercase letter from a to h and a number from 1 to 8. As explained above, TO_POS should be adjacent to FROM_POS (on the diagonal) and should be empty. If you make such a move, you can only make one per turn.




<strong>J FROM_POS TO_POS</strong> – Your agent moves one of your pieces from location FROM_POS to empty location TO_POS by jumping over a piece in between. You should write out <strong>one jump per line</strong> in output.txt if your play results in more than one jumps.

For example, output.txt may contain:

E c3 b4

The resulting board would look like this, given the above input.txt:

.b.b.b.b b.b.b.b. .b…b.b ….b… .w……

w…w.w. .w.w.w.w w.w.w.w.

Let’s look at another example that consists of a jump sequence. Let’s say input.txt is as given below:




SINGLE

BLACK

100.0 .b…..b b…b.b. .b…b.b ..b.w… ……..

w…w… .w.w…w w…w.w.

<strong> </strong>

The file output.txt will contain the following, since all possible jumps have to be taken:

J f6 d4

J d4 f2

After which the board would look like:

.b…..b b…b.b. .b…..b ..b….. ……..

w……. .w.w.b.w w…w.w.

<strong> </strong>

<strong> </strong>

<strong>Notes and hints: </strong>




<ul>

 <li>Please name your program “<strong>xxx</strong>” where ‘xxx’ is the extension for the programming language you choose (“py” for python, “cpp” for C++, and “java” for Java). If you are using C++11, then the name of your file should be “homework11.cpp” and if you are using python3 then the name of your file should be “homework.py”. If you are using python2, even though it is now officially unsupported, you can name your file “homework2.py”.</li>

 <li>The board you will be given as input will always be valid and will have twelve or fewer w/W letters, twelve or fewer b/B letters, and the rest will be . (standing for empty cells).</li>

 <li>Likely (but not guaranteed), total play time will be 5 minutes (300.0 seconds) when playing against another agent, and 30.0 seconds for single moves.</li>

 <li>Play time used on each move is the total combined CPU time as measured by the Unix <strong>time</strong> This command measures pure computation time used by your agent, and discards time taken by the operating system, disk I/O, program loading, etc. Beware that it cumulates time spent in any threads spawned by your agent (so if you run 4 threads and use 400% CPU for 10 seconds, this will count as using 40 seconds of allocated time).</li>

 <li>If your agent runs for more than its given play time (in input.txt), it will be killed and will lose the single move or the game.</li>

 <li>You need to think and strategize how to best use your allocated time. In particular, you need to decide on how deep to carry your search, on each move. In some cases, your agent might be given only a very short amount of time (e.g., 5.2 seconds, or even 0.01 seconds), for example towards the end of a game. Your agent should be prepared for that and return a quick decision to avoid losing by running over time. The amount of play time that will be given in input.txt will always be &gt;0, but it could be very small if you are close to running out of time.</li>

 <li>To help you with figuring out the speed of the computer that your agent runs on, you are allowed to also provide a second program called <strong>xxx</strong> (same extension conventions as for homework.xxx). This is optional. If one is present, <strong>we will run your calibrate program once (and only once)</strong> before we run your agent for grading or against another agent. You can use calibrate to, e.g., measure how long it takes to expand some fixed number of search nodes, or to benchmark file I/O. You can then save this into a single file called <strong>calibration.txt</strong> in the current directory. When your agent runs during grading or during a game, it could then read calibration.txt in addition to reading input.txt, and use the data from calibration.txt to strategize about search depth or other factors.</li>

 <li>You need to think hard about how to design <strong>your eval function</strong> (which gives a value to a board when it is not game over yet).</li>

 <li>You are allowed to maintain persistent data across moves during a game, by writing such data to a single file called <strong>txt</strong> in the current directory. Before a new game starts, the master game playing agent will delete any playdata.txt file. So, on your first move, this file will not exist, and you should be prepared for that. Then, you can write some data to that file at the end of a move and read that file back at the beginning of the next move. – There is no first or second player advantage in this game for two agents with perfect play. In our case, when playing against the reference minimax agent we will give your agent the first move for 5 of the 9 games. In the competition, we will play two agents against each other for an even number of games, and advance both agents to the next round of the competition if they both win or draw on half of the games. If an agent loses more than half of the games, it will be eliminated and only the other agent will move to the next round of the competition. We may end up with several equivalent winners of the competition.</li>

</ul>



















<strong>Example 1: </strong>




For this input.txt:




SINGLE

BLACK

100.0

.b…b..

..b…b.

…..w.b ….w… .b……

w…w.w. …B…. ……w.




One possible correct output.txt is:




J d2 f4

J f4 d6




Here, black can only move backwards because the piece in d2 has been crowned king in a previous turn.

<strong> </strong>

<strong> </strong>

<strong> </strong>

<strong>Example 2: </strong>




SINGLE

WHITE

6.6 ……..

w…b.b. ……..

..w.b…

.w…b..

….b…

.w…..b ..w…w.




One possible correct output.txt is:




E a7 b8




Which results in a white piece reaching the king’s row of the opponent and getting crowned king.




<strong>Example 3: </strong>




For this input.txt:




SINGLE

WHITE

23.33

.b…b..

..b.b.b.

…b…b ..b….. …..w..

w.b.w.w. .w…..w w…w…




one possible correct output.txt is:




J b2 d4

J d4 b6

J b6 d8








