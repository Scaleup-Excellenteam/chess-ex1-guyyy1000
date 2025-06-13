# Best Move Selection Algorithm
This project includes a simple move evaluation algorithm that suggests the best move in a given turn. The idea is to evaluate all legal moves for the current player, score them, and return the top 5.

## How It Works
**1. Legal Moves**
\
For each piece of the current player, we generate all legal moves.

**2. Scoring**
\
Each move is scored based on:

- Capturing an opponent's piece (higher score for more valuable pieces).

- Threatening a stronger enemy piece.
- Being threatened by a weaker piece.
- Delivering check.

**3. Lookahead**
\
If a depth > 0 is provided, the algorithm simulates the opponent's best response (and optionally our next move), using a naive minimax approach:
- For depth 1: we subtract the opponent's best move score.
- For depth 2: we add back our best reply, and so on.

**4. Top Moves**
\
All moves are stored in a custom PriorityQueue, and the top 3 are printed before the player moves.

## Complexity
- At depth 0: roughly O(N×M), where N is number of pieces, and M is average moves per piece.

- At depth D: time complexity grows exponentially like O((N×M)^D), similar to basic minimax.