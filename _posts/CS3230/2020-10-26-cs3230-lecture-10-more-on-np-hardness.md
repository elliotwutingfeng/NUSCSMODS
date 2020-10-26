---
layout: post
published: false
title: 'CS3230 - Lecture 10: More on NP-hardness'
---
# Subset Sum
Problem: Given a set X of n numbers, and a target T, decide whether there exist a subset of X that adds to T.
- There is a dp solution
> We can show NP-hardness

1. Reduce from vertex cover
	- Given G = (V,E) and a number k
2. Produce a set X and number T such that
    - The graph has vertex cover of k 
    - This implies that the set X has a subset that adds to T
    - There is a subset of X that adds to T implies that the graph has a vertex cover of size k

## Reduction
- Number the edges arbitrarily from 0 to E-1
- Our set X contains the integer bi := 4^i for each edge i and the integer:

for each vertex c where the sum of v is the set of edges that have v has an endpoint
- Why does NP hardness proof not imply that P=NP
	- T is not polynomial in the size of our input

# Partition problem
Problem: Given a set X of n numbers, find a partitioning of X into X1 and X2 such that the sum of elements in X1 and X2 is the same

- Theory: NP-hard
- Reduce from subset-sum

> Given a set of numbers X such that the sum of all elements in X is S, we want to add two large numbers P and Q to the set S such that X union {P,Q} can be divded into two sets with equal sum iff X can be divided into two parts that add to T and S-T


# Hamiltonian Cycle problem
- A hamilitonian cycle in a directed graph is a cycle that visit every vertex in the graph exactly once

Problem: Given a directed graph G = (V,E), does there exist a hamiltonian cycle

## Reduction
- Reduce from 3-SAT or from vertex cover to show NP-hardness
- Reduction is tricky
- Use NP hardness of HC to talk about other problems

> All NP-complete problems are polynomial time reducible to each other. Not all reductions are easy to find
Sometimes it is easier to reduce from A to B and then B to C instead of A to C directly

# Hamiltonian Path Problem
- HP from s to t in a directed graph is a path that begind with s and ends at t and visit every vertx in the graph exactly once

Problem: Given a **directed** graph G = (V,E) such that does there exist a Hamilitonian path from s to t

Theorem: It is NP-hard

- Reduce it from hamiltonian cycle
- Given G = (V.E) choose arbitrary vertex v in G
- Replace v by two vertices s and t and add (s to u) for every edge (v to u) in G and add (u to v).

# Undirected Hamilitonian Cycle Problem
Problem: Given an undirected graph G = (V,E) does there exist a Hamilitonian cycle

## Reduce
- Reduce it from Directed Hamilitonaian Path
- For each vertex v, we add tree vertices uin, umid, uout
- For every edge, (u to v), we add the following edges

Claim: The original undirected graph was a HamCycle iff the new undirected graph has a HamCycle

# Traveling Salesman problem
Problem: Given a list of cities and the distance between each pair of cities, what is the shortest possible route that visit each city and returns to origin city

> This is similar to the Undirected Hamiltonian cycle problem, except that it is on a weighted graph

Theorem: TSP is NP-Hard

> reduce it from undirected Hamiltonian Cycle

## NP hardness of search Optimisation problem
- If a known NP-hard problem can be efficiently reduce to A (which is a search/optimisation problem) then this shows that A is NP-hard
- A search/optimsation cannot be NP complete. For A to be NP-complete, it should be in NP which is only well defined for decision problems

# Approximation Algorithm
- we dont know how to solve them
- Approximate the solution
	- Say find an assignment of a 3 SAT instance that satisfies 90 percent of the clauses
    - Or find a path for a traveling salesman that is 110 percent of the best path
- This is good enough for most application

# TSP is NP hard to approximate
- Consider edge weighted undirected graph G. Let the minimum length of a tour of the graph G starting with vertex v and ending with vertex v is M

Problem: c-approximate TSP: Our task is to find a tour starting and ending with vertex v and total length cM for some c>1

Theorem: c-approximate TSP is NP-hard
- reduce from undirected Hamilitonian cycle problem

- Create a new complete G' = (V,E') with edge weight defined as w(x,y) = 1 if (x,y) is in E and w(x,y) = cn +1 otherwise
- G has a hamiltonian cycle iff G' has a cycle with total weight n iff G' has a cycle of total weight at most cn



# Euclidean TSP problem
Problem: This is the TSP problem with the additional restriction that for any three vertices x,y,z, w(x,y) + w(y,z) >= w(x,z) ie the distance from x to z is at msot distance of going from x to y and then going from y to z

## Efficient Algorithm for 2 approximate EuclideanTSP
To approximate the smallest tour P starting with vertex v.
- Let T be the minimum spanning tree for G. Consider T as a tree rooted at v.
- TSP(T,v)
	- Add v to P
    - For each child u of v
    	- TSP(T,u)
        - Add v to P
- Remove all repeated appearance of any vertex in P

## Why does it work
Show the following observation that lead to the proof
- The min spanning tree is the smallest connected graph spanning all vertices. So the total weight is less than the total tour weight of the travelling salesman
- Our algo visit every edge of the tree exactly twice withut the last step
- By removing repeated appearance of vertices in the last step, we only decrease the total weight of the tour (This uses the Euclidean property)

## 2 Approximation Algo for vertex cover
Problem: Given an undirected graph G = (V,E) find a subset of vertices V' that covers each edge in G and is at most twice the size of the smallest vertex cover
- While there exist an edge (u to v) not covered by V'
	- Add u,v to V'
- Correctness is immediate from the fact that for any vertex cover V'', and for any pair of vertices u,v added to V' in any single step at least one of u, v must be in V''














