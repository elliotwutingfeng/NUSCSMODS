---
layout: post
published: true
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
![CS3230-5-1.PNG]({{site.baseurl}}/img/CS3230-5-1.PNG)

![CS3230-5-2.PNG]({{site.baseurl}}/img/CS3230-5-2.PNG)


- Back trcking is to costly, there are n! permutation
- Dynamic programming does not help because we cannot find a small number of subproblems leading to the given problem.
- Guess the solution with initution that Lp(n) > Lp(1)

## Algorithm
- Sort the records in increasing length

## Prooving (Local swap for minimisation problem)
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

![CS3230-5-3.PNG]({{site.baseurl}}/img/CS3230-5-3.PNG)

Let greedy algo produce a permutation p such that 
![CS3230-5-4.PNG]({{site.baseurl}}/img/CS3230-5-4.PNG)

> Observed that dist(q) = 0 if and only if p = q... why?
> 
> 


##### Why does this proof work?
Let O be optimum solution such that dist(O) is as small as possible.
Since O is different from G, dist(O) > 0

- if F(O*) < f(O), then we have found a solution better than optimum which contradicts
- if f(O*) = f(O) and dist(O*) < dist(O) then this contradicts that dist(O) is the smallest among all possible optimal solution


### Generalisation
Assuming the frequency of accessing file ith is Fi

So if we reorder the files using the permutation q then the cost of the function now becomes:
![CS3230-5-5.PNG]({{site.baseurl}}/img/CS3230-5-5.PNG)

So intuitvely, we need Li to be in increasing order and Fi to be in decreasing order

- To help figure out the correct greedy choice, we can try a similiar local swap as the prev algo to help us
- Let q* be the permutation obtain by swapping q(i) and q(i+1)

![CS3230-5-6.PNG]({{site.baseurl}}/img/CS3230-5-6.PNG)

- This consistent with what we expect
- We again make the simplifying assumption that Li/Fi are distinct
- The proof of correctness of this greedy algorithm is almost identical to the prev one. The LOCAL SWAP is already there on the previous slide.



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
> - Convince urself that dist(S) = 0 if and only if S = G and that dist takes only finitely many values (There is no need to prove this)
> - Given O, prove that there exists an O* that satisfies the desired property

# Scheduling Classes
- Suppose you are given two ararys S and F of size n listing the start and finishing times of each class
- Choose the largest possible subset X of 1..n so that for any pair i,j in X.. either S[i] >= F[j] or S[j] >= F[i]

![CS3230-5-7.PNG]({{site.baseurl}}/img/CS3230-5-7.PNG)


## Theory

- Think of how to make the first greedy choice
- DO we want to include the class that is the shortest
- Do we want to include class that begin first
- Do we want to include the class that ends first

For each of the strategies above, think of a counter example for which it will not a part of the solution or try to reason why it should be a valid strategy


- If we pick the shortest one, might overlap with anotehr class with the starting time in between the S and F
- IF we pick class that start first, it might go on forever and conflict with every other class
- If pick the class that ends first, seems like it has minimal conflict and scheduling it might be good idea

> Pick the class that finish first and recurse over all classes that start after this one finishes

![CS3230-5-8.PNG]({{site.baseurl}}/img/CS3230-5-8.PNG)

## PsueudoCode
- Sort the finishing time of all class from first to last
- Add Class 1 to schedule, Curr = F[1]
- For i =2 to n
	- if S[i] >= Curr, then
    	- Add class i to the schedule
        - Curr = F[i]

Time complexity: O(nlogn) for sort and O(n) for others


## Proof
- Suppose optimal schedule O has class {o1..om}, f(O) = m
- Suppose greedy schedule G has classes {g1..gk}, f{G} = k
- We assume that the classes in both are sorted according to finish times
- We want to swap the first class where o differes from G
- Define dist(O) to be m-i where i+1 is the smallest index such that
				O'i+1' != g'i+1'


![CS3230-5-9.PNG]({{site.baseurl}}/img/CS3230-5-9.PNG)

# Graphs
![CS3230-5-11.PNG]({{site.baseurl}}/img/CS3230-5-11.PNG)

![CS3230-5-10.PNG]({{site.baseurl}}/img/CS3230-5-10.PNG)

## Minimum spanning tree
![CS3230-5-12.PNG]({{site.baseurl}}/img/CS3230-5-12.PNG)

Onegraph:
- n = number of vertices
- m = number of edges

![CS3230-5-13.PNG]({{site.baseurl}}/img/CS3230-5-13.PNG)

## Generic greedy algo
Consider greedy algo for finding an MST of G = (V,E) that finds a spanning tree as follows

- Initilised F = (V,E') where E' is empty
- For i = 1 to n-1
	- Let C1 .. Ck be the connected components of F
    - Arbituarily chooe j in {1..k} and pick an edge e in E with minimum weight among edges with exactly endpoint in Cj
    - Add e to E'

> Graph F is a forest

### Theory

![CS3230-5-14.PNG]({{site.baseurl}}/img/CS3230-5-14.PNG)
![CS3230-5-15.PNG]({{site.baseurl}}/img/CS3230-5-15.PNG)


> Check it if the path e is e'

### Prims algo
There is only one non trivial component C which is a tree. Every other component contains one vertex.

![CS3230-5-16.PNG]({{site.baseurl}}/img/CS3230-5-16.PNG)

- Choose one random vertice
- Check out going edges and select the one with least cost
- See 2040s

### Time complexity
- Keep all the edges adjacent to C in a pq Q implemented using a min heap
- At each step, extract the min weight edge (u,v) in Q
	- if both vertices are in tree do nothing
    - If only one, say u, is in the component C then we insert v into C and all edges from v into Q
- Each edge (u,v) can be inserted into Q at most twice.
	- Adding edges from u
    -　Adding edges from v
- The size of Q is at most M hence insertion is logm time

- Time complexity O(mLogn)

## Kruskal algorithm
![CS3230-5-17.PNG]({{site.baseurl}}/img/CS3230-5-17.PNG)

Scan all edges in increasing order of weight and add the edge if both endpoints are in different components

![CS3230-5-18.PNG]({{site.baseurl}}/img/CS3230-5-18.PNG)

