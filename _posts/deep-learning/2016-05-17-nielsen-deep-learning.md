---
layout: note
title: Neural Networks and Deep Learning
date: 2015-05-17 20:14:44 -0600
categories: Deep-Learning
---

[Source](http://neuralnetworksanddeeplearning.com/index.html)
[Code Samples](https://github.com/mnielsen/neural-networks-and-deep-learning)

## [Chapter 1 : Using neural nets to recognize handwritten digits](http://neuralnetworksanddeeplearning.com/chap1.html)

- A neural network can represent any computable function
- To make learning possible, the sigmoid function must be used for the perceptrons
so that small changes in weight/bias result in small changes in the output. Otherwise,
changes in different parts of the network could culminate and give an entirely different
result for similar inputs.
- The sigmoid function is defined by σ(w⋅x+b) where σ is the sigmoid function/logistic function.
- σ(z)≡1/1+e^(−z)
- feedforward network : all data only flows in one direction
- recurrent network : there are loops that let data return into the data flow
- cost / loss / objective function : how well the weights and biases approximates y(x) for all
training inputs x.
- Debugging a neural network can be very difficult but there are heuristics to
- Neural networks break down a complicated question into increasingly specific subproblems until the features are directly from the data.

## [Chapter 2 : How the backpropagation algorithm works](http://neuralnetworksanddeeplearning.com/chap2.html)

- Backpropagation : A fast algorithm for computing the gradient of the cost function.
- Defines how the weights and biases are set in the network

Notation:

w<sup>l</sup><sub>jk</sub>
