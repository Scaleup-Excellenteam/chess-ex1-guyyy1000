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


# Multithreading Support

1. **Thread Pool**
A custom ThreadPool class is implemented using std::thread, std::mutex, and std::condition_variable. When initialized, it spawns a configurable number of worker threads.

2. **Work Distribution**
When calculating move suggestions, we divide the current player's pieces across the available threads. Each thread evaluates the best move for one or more pieces and attempts to insert the result into a shared PriorityQueue.

3. **Synchronization**
Access to the PriorityQueue is protected using a std::mutex. Only the push operation is synchronized to minimize performance overhead.

### Benchmark Methodolog
yTo evaluate performance, the program was run with different thread counts (2, 4, and 8). For each configuration, i measured the time taken to compute the best move at each turn and then averaged the results over 8 moves. These average times are recorded in the table below.