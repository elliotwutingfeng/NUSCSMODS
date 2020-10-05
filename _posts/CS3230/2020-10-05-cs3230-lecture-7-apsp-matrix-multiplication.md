---
layout: post
published: true
title: 'CS3230 - Lecture 7 : APSP, Matrix multiplication'
---
# All Pair shortest path
Problem: A graph = (V,E), with a weight function w:E-> R. For every u,v in V, find the path of minimum total weight from u to v.

Obvious algorthims: Run single source algo on all v in V


## Reweighting
Negative edges slow us down signifiantly. Can we rid them?
Johnson idea: We want to reweight the graph in a way that the total weight of any path from s to t changes by the same amount.

Idea:
- Suppose for for function f: V -> R, we change the weight of the edge x->y as follows:
	(nsert ur img>

> Current weight of e (x->y)

- Such that, for any path, the value is just sum the edges w(k->m)
- for each w'(k->m), substitute with the above formula
- We realised that we are cancelling out the repeats:


- It is not clear whether there exist a function f such that w'(x->y) is not negative for all x and y
- Notice that f(x) = dist(x), where dist(x) is the distance from some source s satisfies this. (If nt, we shld be able to relax the edge x->y)
- The graph might not have a vertex s from which every vertex is reachable
- we don't want to subtract infinity

### How? (Ghost node)
- Add vertex s to graph and add edges s->v to all v in V, with w(s->v)=0
- Every vertex is reachable frm S
- For any u, v in V, we dont create a new path since there are no incoming edges to s. Thus dist(u,v) remains unchanged.

### Algo


### Time complexity
- One call to bellman ford
- n calls to dijkstra
- Reweighting takes O(m) time
- Total time O(mn + nm + n^2logn + m)


# Alternative simpler dynamic programming
- Modify bellman ford 
- dist(u,v,i) = shortest distance from u to v via a path with at most i edges


Complex: O(n^2m)
> Shortest path from u to v is dist(u,v,n)

## Divide and conqure speed up
- Speed up by having x as the middle element in the path from u to v.

Recurrance:


Base:


- Finding the minimum value of the dist from u to x and x to v
- shortest path by using k = logn (base 2)

# Matrix multiplcation
Consider two n*n matrix A and B such that C  = AB. 

Cij = Ai1*B1j + Ai2*B2j + .. Ain*Bnj


Now, let M be an n*n edge weight matrix for a graph G = (V,E) i.e.

[insert]

where 1<= i, j<=n are indices corresponding to the n vertices. Consider the following expressing:

M . M : = min(mil + M1j, Mi2 + M2j, .. Min + Mnj)

## Min plus product of matrices

M . M : = min(mil + M1j, Mi2 + M2j, .. Min + Mnj)

Reprsents the shortest path from i to j of length at most 2.


Notice:
- Resemblance to the matrix produce MM with
- Multiplcation replace with addition
- Addtion replace by minimum


## Solving APSP
--- Define : MINPLUSPRODUCE(M, n-1) = M. M.M..M n-1 times


For solving APSP notice that it is a sufficient to compute MINPLUSPRODUCE(M, n-1)

Time: O(n^3)

## Speeding up

- Let A, B be n*n matrices and we want to compute the n*n matrix C such that C = AB using divide and conquer. 

[Insert2]


> Recursive algo for computing C with 8 multiplcation of M*M matrices where m = n/2

Time complexity: T(n) = 8T(n/2) + O(n^2) = O(n^3)

## Straseen idea - karatsuba style


## Improving APSP
- No
- Strassen algo use subtraction - there is unfortunately no similiar inverse for min
- It is an open question whether APSP can be improve to O(n^2.99) It is widely believe that this impossible



# Flyod-Warshall
- Make O(1) recursive call
- Let the vertices in the graph be numberred 1,..n
- We define dist(u,v,r) to be the shortest path from u to v that only goes through vertices numbered 1..r

## Recurance relation 
[Img]

## algo 





