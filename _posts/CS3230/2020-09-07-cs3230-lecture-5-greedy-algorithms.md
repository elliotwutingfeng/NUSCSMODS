---
layout: post
published: false
title: 'CS3230 - Lecture 5 : Greedy Algorithms'
---
Motivation: To figure out which of the option is the best and pick that wihtout making all recursive calls

# Storing files on a tape (Minimisation)
- Consider n files we want to store on a magnetic tape
- They have lengths given by L1.. Ln,
- Make a simple assumption that all lengths are distint
- On magnetic tape, reading the kth file requries going through all previous files
- If the files are arranged from 1 to n in the given order then
	- cost(k) = L1 + l2 + l3 ... Lk

Problem: Reaarange the files to minimize the avg cost

## Theory


- Back trcking is to costly, there are n! permutation
- Guess the solution with initution that Lp(n) > Lp(1)

## Algorithm
- Sort the records in increasing length

## Prooving
- Suppose we are given a problem where we are required to find an optimum solution O where f(O) is minimum
- Suppose greedy algo produce solution G
- We want to prove that for any optimum solution O That minimises f,
					f(G) = f(O)
- Approach: Slowly change any optimum solution O to eventually get the greedy solution G without increasing f in any step


Steps:
1. Define distance measure dist from any possible solution to a positive number that indicated the distance from greedy solution
	- For any solution S, dist(S) = 0 if and only if S = G
	- dist takes finitely many possible values for any valid solution
2. Given any optimum solution O, different from G, find another solution O* such that 
	- Either f(O*) < f(O)
    - or f(O*) = f(O) and dist(O*) < dist(O)

##### Why does this proof work?
Let O be optimum solution such that dist(O) is as small as possible.
Since O is different from G, dist(O) > 0

- if F(O*) < f(O), then we have found a solution better than optimum which contradicts
- if f(O*) = f(O) and dist(O*) < dist(O) then this contradicts that dist(O) is the smallest among all possible optimal solution


### Generalisation


# Local swap for maximiation problem
We are given a problem where we are required to find an optimum solution O such that f(O) is max
- Suppose greedy algo produce solution G
- We want to prove that for any optimum solution O That minimises f,
					f(G) = f(O)
- Approach: Slowly change any optimum solution O to eventually get the greedy solution G without decreasing f in any step

Steps:
1. Define distance measure dist from any possible solution to a positive number that indicated the distance from greedy solution
	- For any solution S, dist(S) = 0 if and only if S = G
	- dist takes finitely many possible values for any valid solution
2. Given any optimum solution O, different from G, find another solution O* such that 
	- Either f(O*) > f(O)
    - or f(O*) = f(O) and dist(O*) < dist(O)

> For exam
> - Define approporaite dist function
> - Convince urself that dist(S) = 0 if and only if S = G and that dist takes only finitely many values
> - Given O, prove that there exists an O* that satisfies the desired property

# Scheduling Classes
- Suppose you are given two ararys S and F of size n listing the start and finishing times of each class
- Choose the largest possible subset X of 1..n so that for any pair i,j in X.. either S[i] >= F[j] or S[j] >= F[i]

## Theory


