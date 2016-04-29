---
layout: note
title: Artificial Intelligence A Modern Approach Chap 3
date: 2016-04-19 12:29:12 -0700
categories: ai
---

# Chapter 3 : Solving Problems by Searching

- Goal formulation: first step in problem Solving
  - create goal based on the current situation and the agent's performance measure
- Problem formulation: process of deciding what actions and states to consider, given a goal
- search : examining different possible sequence of actions that lead to the known value, and the choosing the best sequence
- search strategy : how the choice of which state to expand is chosen
- it is possible to have repeats and loops on a tree
- often implemented as a queue because it is computationally cheaper

Algorithm's performance measure:
  - Completeness : is it guaranteed to find a solution if possible?
  - Optimality : Does the strategy find the optimal solution?
  - Time complexity : How long does it take to find a solution?
  - Space complexity : How much memory is needed to perform the search?

complexity is expressed in 3 terms:
  - __b__ (branching factor) : maximum number of successors of any node
  - __d__ : depth of the shallowest goal node
  - __m__ : maximum length of any path in the state Space

breadth-first search : expand each level of successors before beginning the next
  - FIFO (queue)

depth-first search  : expands the deepest node
  - LIFO (stack)

depth-limited search : expands the deepest node to a given limit

iterative-deepening search : continuously increases the depth limit

- In general, iterative deepening is the preferred uninformed search method when
  there is large search space and the depth of the solution is not known

- sensorless problems: there are no sensors at all to detect the current state
- contingency problems: the environment is partially observable and actions provide
                       new information about the environment
- exploration problems : when the states and actions of the environment are unknown
                         and the agent must act to discover them.
