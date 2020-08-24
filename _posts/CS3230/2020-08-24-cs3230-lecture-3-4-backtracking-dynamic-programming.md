---
layout: post
published: true
title: 'CS3230 - Lecture 3/4: Backtracking, Dynamic Programming'
subtitle: Lecture 3 and 4
---
# Backtracking
- Construct a solution to the problem one piece at a time
- Algo recursively evaluates all alrernatives and chooses the best one
- Algo exp amount of time in the recursion depth

#### Example: N queens problem
We want to put n queens on n*n chessboard such that no queens are in attacking position (row/column/diagonal)

![CS3230-3-1.PNG]({{site.baseurl}}/img/CS3230-3-1.PNG)

Algorthims:


Array of Q[1..n] where Q[i] represents the column position of the queen in the ith row

- if i = n + 1, output the value (finish)
- For k = 1 to n (Iterating the col)
	- Algo checks if Q[i] = k is valid with respect to Q[1..i-1]: Check if the row and col is valid with respect to the ones we have previously
    - if valid, sets and make recursive call with input i + 1 , and Q[1..i] (update)

> This explains why numb 3 in the image stops there because the next row cannot be input

Consider the following directed graph for the N queens problem
- The vertices are the states (i, Q[1..i-1]
- There is an edge from (i..Q[1..i+1]) to (i+1..Q[1..i]) if Q[i] is valid with respect to the previous values

One can construct the graph and run DFS on it with the source vertex s being (1, "EMPTY"). **If there is a vertex v at distance n, then the problem has a valid solution.** One can trace back the path from v to the source s to obtain the solution to the problem.

Backtracking algorthim doesnt build the graph in advance but does it on the fly.

#### Example: Game tree
Alice and bob play 2 player game
- Alice can move one piece east each step
- Bob can move one piece south each step
- Each player can only move one move at a time or jump one step over the other player

![CS3230-3-2.PNG]({{site.baseurl}}/img/CS3230-3-2.PNG)



# Dynamic Programming
