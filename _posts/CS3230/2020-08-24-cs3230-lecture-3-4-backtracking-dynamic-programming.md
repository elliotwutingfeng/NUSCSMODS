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

## Example: N queens problem
We want to put n queens on n*n chessboard such that no queens are in attacking position (row/column/diagonal)

![CS3230-3-1.PNG]({{site.baseurl}}/img/CS3230-3-1.PNG)

-  For the first layer of the tree, we will only place the queens on the first row 
- subsequent children will try to put the next queen on the next row if it is possible
- Else it will backtrack till a possible path is allowed

Looking at the graph stucture, we will see that the order that the configuration are visited is similiar to [DFS](https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/). 

#### DFS:
- Subproblem = Vertices
- There is an edge from p1 to p2 if p1 makes a recusive call to p2


![CS3230-3-17.PNG]({{site.baseurl}}/img/CS3230-3-17.PNG)


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

## Example: Game tree
Alice and bob play 2 player game
- Alice can move one piece east each step
- Bob can move one piece south each step
- Each player can only move one move at a time or jump one step over the other player

![CS3230-3-2.PNG]({{site.baseurl}}/img/CS3230-3-2.PNG)

> The state is bad when the move player P makes results in the opponents next move state to be good

![CS3230-3-3.PNG]({{site.baseurl}}/img/CS3230-3-3.PNG)

## Example: Fibonacchi
![CS3230-3-4.PNG]({{site.baseurl}}/img/CS3230-3-4.PNG)

- F0 = 0 
- F1 = 1
- Fn = Fn-1 + Fn-2 for n>=2




BUT:
![CS3230-3-5.PNG]({{site.baseurl}}/img/CS3230-3-5.PNG)

SOLUTION:
- Use memorisation

![CS3230-3-6.PNG]({{site.baseurl}}/img/CS3230-3-6.PNG)


![CS3230-3-8.PNG]({{site.baseurl}}/img/CS3230-3-8.PNG)

We store the value into an array such that when we need it again, we just have to retreive it from the array. Thus we eliminate the need to recalculate the past.

#### Analyis of algorithm

We will classify the recusive calls:
![CS3230-3-18.PNG]({{site.baseurl}}/img/CS3230-3-18.PNG)

> - Memorised recusive calls takes O(1) time
> - Recusive calls executed for the first time executes only once
>		> This means that Fib(7) only calculates ones


Consider all possible recusive calls Fn, we know that it will all end up in the base case. Since we do not know which is recusive and which is memorise.. we will just analysis each of the recursive calls not counting the recursive calls that runs for the first time 

![CS3230-3-19.PNG]({{site.baseurl}}/img/CS3230-3-19.PNG)

> No time is taken for calling a recusion ie F(n-1)

![CS3230-3-20.PNG]({{site.baseurl}}/img/CS3230-3-20.PNG)


Proof by induction:
![CS3230-3-7.PNG]({{site.baseurl}}/img/CS3230-3-7.PNG)

#### Bottom Up version
Bottom up has the same time complexity for MEMODP up to a constant factor.

![CS3230-3-21.PNG]({{site.baseurl}}/img/CS3230-3-21.PNG)

> Bottom up is similiar to memo except that bottom up start from the leaf rather than the top and does not use recusion



> Question: Can all problems if is solvable top down means that it can be solve bottom up vice versa:
> Yes
>
> ![CS3230-3-22.PNG]({{site.baseurl}}/img/CS3230-3-22.PNG)






## Memorisation is DFS
- DFS doesn't re visit the old paths 
- Fibo:
	- For every i there is an edge from i to i-1 and from i to i-2
    - the vertices are 1..n
    - We can construct the graph with source vertex s being n. Before finishing a particulare vertex.. compute the FIB (Fi = Fi-1 +Fi-2)

Compare:
![CS3230-3-9.PNG]({{site.baseurl}}/img/CS3230-3-9.PNG)

# Dynamic Programming

## Bottom-up
- We can fill up the array iteratvely
![CS3230-3-10.PNG]({{site.baseurl}}/img/CS3230-3-10.PNG)

## Example: Subset sum
Given a sets of positive integer X and a number S. Determine if there exist a subset of X that sums to S

- If there exist a subset, return TRUE else FALSE

### Recurrence
![CS3230-3-11.PNG]({{site.baseurl}}/img/CS3230-3-11.PNG)

> We subtract the number from T each time we did the recusion
### Base case
- SubSUM(X,0,T) = 1 if T = 0 and 0 otherwise

We realised that we can immediately return if
- T = 0 for any i: Return true
- T < 0 for any i return 0

### Remark
We can treat X as an global variable so we can decrease the number of parameter

### Algorithm
- if T<0, return 0 //SUBTRACTION FAIL
- if T = 0, return 1 // T is exactly X[i]
- if i = 0 and T > 0 , return 0 // T is too big such that there is no values that can be added 
- Else return SubSUm(i-1,T) OR SubSum(i-1,T-X[i])

#### Analysis and remarks
- Correctness: Induction
- Complexity: T(n) = 2T(n-1) + C which solves to O(2^n)

### Algorithm with memorisation
- Initialise array SS[0..n][0..T] all to (False/NULL)

SubSum(i,T):
- IF T<0, return 0
- if T = 0, return SS[i][T] = 1
- If i = 0, and T > 0 , then SS[i][T] = 0
- If SS[i][T] is null then
	- SS[i][T] = Subsum{i-1, T) OR subSUM(i-1, T-X[i])
- Return SS[i][T]

#### Analysis and remarks
- The time is O(nS) 
- The analysis is the same as the fibonnachi sequence.

> It is dynamic programming because we are breaking the larger problem into a smaller problem before solving it


## Example: Longest Common Subsequence
A string of X is said to be a subsequence of another string if there exist some distint integers such that X[j] = Y[ij]
![CS3230-3-12.PNG]({{site.baseurl}}/img/CS3230-3-12.PNG)

For example:
- X = "ABSGED"
- Y = "AFERGDW"
> The subsequence is "AGD", Note that the position matters

### Recursive solution

Theorem:
- Let C[1..k] be an LCS of A[1..m] and B[1..n]
- If A[m] = B[n], then
	- C[k] = A[m] = B[n]
    - C[1..k-1] is an LCS of A[1..m-1] and B[1..n-1]
- If A[m] is not equal B[n]
	- C[k] != A[m] implies that C[1..k] is an LCS of A[1..m-1] and B[1..n]
    - C[k] != B[n] implies that C[1..k] is an LCS of A[1..m] and B[1..n-1]

#### Proof
- Proof by contradiction
![CS3230-3-13.PNG]({{site.baseurl}}/img/CS3230-3-13.PNG)

> Idont get this 

![CS3230-3-14.PNG]({{site.baseurl}}/img/CS3230-3-14.PNG)


#### Algorithm
- Let LCS(i,j) denote LCS of A[1..i] and B[1..j] where x||j denote the concat of string x and y

From the previous theorem we get recursive solution for LCS(i,j)
- LCS(i,j) = LCS(i-1, j-1) || A[j] if A[i] = B[j]
- LCS(i,j) is the longer of the LCS(i, j-1) and LCS(i-1, j) if A[i]!=B[j]

Recurrance:
![CS3230-3-15.PNG]({{site.baseurl}}/img/CS3230-3-15.PNG)

> Do not solve this complicated recurrance but rather use dynamic programming to solve

Bottom-up:
![CS3230-3-16.PNG]({{site.baseurl}}/img/CS3230-3-16.PNG)

> -  everytime we see that the characters are equal, we add them together
> - Set the current LCS to the greater of the previous answer

Running time: O(nm)
