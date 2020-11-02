---
layout: post
published: false
title: 'CS3230 - Lecture 11 : Amortized Analysis'
---
Not tested in finals

# Incrementing a binary counter
The input B is an infinite array of bits where B[i] iff 2^i appears in the sum.

The first k bits are 1 and the next bit is 0, the incrememnt takes time O(K)

# Counting from 0 to n
- SUppose we call increment n times
- Starting with zero counter
- How long from 0 to n
- If can use worst case running time for each inc, we get upper bound of O(nlgn) on total running time. 

# Amortized cost
- Avg cost
- There is no prob involve
- Avg oiver a seq of operation
- Not the possible running times of a single operation

# Taxation method
- Method to derive amortized bounds

- Instead of paying for each bit flip when it happen, increment revenue service charges a two dolloar increment tax whenever we want to set a bit from zero to one
- One of those dollars is spent changing the bit form zero to one; the other is stored away as credit until wse need to reset the same bit to zero
- The key point here is that we always have enough credit saved up to pay for the next increment
- THe amortized cost of an increment is the total tax it incurs which is exactly 2 dollars since each increment changes jus one bit from 0 to 1

- Certain steps in algo charge tax
- Total cost incurred is never more than the total tax paid
- AMoritzied cost of operation is the overall tax charged during that operation


# Potential method
- Powerful method
- Represent prepaid worl as potential that can be spent in later operation
- Potential is function of the entiry data struct


> Define a potential function for the data structure that is init equal to zero and is always non negative. The amortized cost of an operation is its actual cost plus the change in potential


## Example: Increment and decrement
- Suppose we want a bin counter that both inc and dec efficiently
- Standard wont work
- If we alt between 2^k and 2^k - 1, every operation is O(K) time

Nice alt:
- Represent each interger as a pair (P,N) of bit strings, subject to the invariant P && N = 0
- FOr every index i, at most if the bits P[i] and N[i] is 1

If we interpret P and N as bin numbers, the actual value of the counter is P-N


## Example: Multipop stack
Goal: Support operation on a set of elemeents
- Push
- POp
- Multipop: Remove and retun the k most recently added elements

Total cost: Naive
- Starting from empty stack, anyu intermix seq of n PUSH, POP< Multipop operation takes O(N^2) time


## Summation method
- Starting from an empty stack, any intermixed seq of n Push, POp, Multipop operation takes O(n) time

Proof:
- an element is pop at most once for eerytime its psuh
- There is at most n push operation
- Thuis there are at most n pop operation (Including those mad wihtin Mulitpop)


## Tac method
- Charge 2 dolar everytime an element x is push
	- use 1 dollar top pay for the push operation
    - Save 1 dollar to be use for oppping x sat some time in the future
- Pop operation charges 0 dolalrs
	- totla cost is always less than the tax paid
    - Ammortized is at most 2n

## Potential method
- Definet he potential to be the number oif elenments on teh stack

