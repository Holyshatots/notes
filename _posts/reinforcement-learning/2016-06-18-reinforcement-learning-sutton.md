---
layout: note
title: Reinforcement Learning : An Introduction
date: 2016-06-17 12:29:12 -0700
categories: reinforcement-learning
---

# Reinforcement Learning : An Introduction by Richard S. Sutton and Andrew G. Barto

## Chapter 1 : The Problem

- Reinforcement learning: learning what to do to maximize a numerical reward signal
- Separate from supervised learning because there is no knowledgeable supervisor
that provides examples.
- Exploration and exploitation need to be balanced in RL and are directly at odds with
each other.


Four main subelements of  a reinforcement learning system:
  - policy : defines the learning agent's way of behaving at a given time
  - reward function : defines the goal in a reinforcement learning problem
  - value function : defines what is good in the long run
  - model (optional) : something that mimics the behavior of the environment

## Chapter 2 : Evaluative Feedback

- Reinforcement learning is distinct because it provides training information that
__evaluates__ the results of an action instead of giving instructions of the
correct action.
- n-armed bandit problem : Being repeatedly faced with a choice amount n different options.
After each selection a numerical reward for the action is returned and your job is
to maximize this numerical reward.
- greedy action : choosing the action whose estimated value is the greatest. Exploiting the existing
knowledge about the situation.
