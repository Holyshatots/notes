---
layout: note
title: Artificial Intelligence A Modern Approach Chap 2
date: 2016-04-19 12:29:12 -0700
categories: ai
---

### 2.4 The Structure of Agents

agent = architechture + program

agent program: takes the current percept as input

agent function: Takes the entire percept history

Four basic agent programs:

  - Simple Reflex Agents
  - Model-based reflex agents
  - Goal-based agents
  - Utility-based agents

Simple Reflex agent: select actions based on the current percept

condition-action rule:
  __if__ car-in-front-is-braking __then__ initiate-braking

Model-based agent: holds an internal state which is a model of all past percepts to base decisions off of
  - Can handle partial observability

Goal-based agents: A model-based agent that also has a goal and looks at potential states to choose an action that is most likely to reach the goal

Utility-based agents: A goal-based agent that tries to maximize a utility function

Utility function: "maps a state (or sequence of states) onto a real nubmer that describes the
                   associated degree of happiness"

 - Can have multiple goals and will try to optimize based on the influence of these

learning element: responsible for making improvements
performance element: responsible for selecting external actions
