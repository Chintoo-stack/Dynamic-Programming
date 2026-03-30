# Dynamic-Programming
Pattern 1: Problems on grid
The Problem: You are at the top-left cell (0, 0) of a grid. You want to reach the bottom-right
cell (m, n) . You can only move Down or Right. Find the path with the Minimum Cost.

Step 1: Think Recursively (Backward)

. Stand at the Goal: I am at the bottom-right cell (i, j) .

. Look Back: How did I get here? Since I can only move Down or Right to get here, I must
have arrived from:

1. The cell Above me (i-1, j) (I moved Down).

2. The cell to the Left of me (i, j-1) (I moved Right).

. The Logic: To minimize the cost to reach (i, j) , I should pick the minimum of the two
paths leading to me, and add my own cost.

Step 2: Recurrence relation (maths);
cost(i,j) = grid[i][j]+min(grid[i-1][j],grid[i][j-1])
Base Case: If I am at (0,0) , the cost is just grid[0][0].

Out of Bounds: If i < 0 or j < 0, return Infinity (so this path is never chosen).

Step 3: Pattern Identification
· How to Identify:

. Input is a 2D Matrix or Grid.
· Movement is restricted (e.g., "only right and down").
. Objective involves "Minimum cost", "Maximum gold", or "Number of ways" to reach a
corner.

. Typical Questions:
. Minimum Path Sum: Find the path with the lowest sum.

. Unique Paths: How many distinct paths exist from start to finish?

. Dungeon Game: Find minimum health needed to survive a grid of threats.

. Maximal Square: Find the largest square of 1s in a binary matrix.



class Solution {
// Memoization table to store results we've already calculated
// dp[i][j] will store the min cost to reach cell (i, j)
int[][] memo;

public int minPathSum(int[][] grid) {
int m = grid. length;
int n = grid[0].length;
memo = new int[m][n];

// Initialize memo with -1 to indicate "not calculated yet"
for(int[] row : memo) java.util.Arrays.fill(row, -1);

// Start the recursive thought process from the END (bottom-right)
return solve(grid, m - 1, n -1);

// The Recursive Function
private int solve(int[][] grid, int i, int j) {
// Base Case: We are at the start (top-left)
if (i == 0 && j == 0) return grid[0][0];

// Boundary Check: If we go off the grid (up or left), return Infinity
// so this path is ignored by the Math.min function
if (i < 0 | | j < 0) return Integer.MAX_VALUE;

// DP Check: If we already solved this subproblem, return the answer
if (memo[i][j] != -1) return memo[i][j];

// RECURSIVE LINE:
// Calculate cost coming from Above (up)
int up = solve(grid, i -1, j);

// Calculate cost coming from Left
int left = solve(grid, i, j -1);

// The Logic: Current cost + min(path from up, path from left)
memo[i][j] = grid[i][j]+ Math.min(up, left);

return memo[i][j];

Why this works: The code looks exactly like our thought process. We ask for the
answer at the end, and the computer recursively digs back to the start, solves the
base case, and bubbles the answers back up, saving them in memo along the way.
