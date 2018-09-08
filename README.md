# AlphaZero-Deep-Reinforcement-Learning
A replica of the AlphaZero methodology in Python



To start the learning process, run the top two panels in the run.ipynb Jupyter notebook. Once it’s built up enough game positions to fill its memory the neural network will begin training. Through additional self-play and training, it will gradually get better at predicting the game value and next moves from any position, resulting in better decision making and smarter overall play.

We’ll now have a look at the code in more detail, and show some results that demonstrate the AI getting stronger over time.

N.B — This is my own understanding of how AlphaZero works based on the information available in the papers referenced above. If any of the below is incorrect, apologies and I’ll endeavour to correct it!

## Connect4
The game that our algorithm will learn to play is Connect4 (or Four In A Row). Not quite as complex as Go… but there are still 4,531,985,219,092 game positions in total.


## Connect4
The game rules are straightforward. Players take it in turns to enter a piece of their colour in the top of any available column. The first player to get four of their colour in a row — each vertically, horizontally or diagonally, wins. If the entire grid is filled without a four-in-a-row being created, the game is drawn.

Here’s a summary of the key files that make up the codebase:

### game.py
This file contains the game rules for Connect4.

Each squares is allocated a number from 0 to 41, as follows:


### Action squares for Connect4
The game.py file gives the logic behind moving from one game state to another, given a chosen action. For example, given the empty board and action 38, the takeAction method return a new game state, with the starting player’s piece at the bottom of the centre column.

You can replace the game.py file with any game file that conforms to the same API and the algorithm will in principal, learn strategy through self play, based on the rules you have given it.

### run.ipynb
This contains the code that starts the learning process. It loads the game rules and then iterates through the main loop of the algorithm, which consist of three stages:

### 1.Self-play
### 2.Retraining the Neural Network
### 3.Evaluating the Neural Network
### 4.There are two agents involved in this loop, the best_player and the current_player.

The best_player contains the best performing neural network and is used to generate the self play memories. The current_player then retrains its neural network on these memories and is then pitched against the best_player. If it wins, the neural network inside the best_player is switched for the neural network inside the current_player, and the loop starts again.
