---
layout: note
title: Neural Networks and Deep Learning
date: 2015-05-17 20:14:44 -0600
categories: Deep-Learning
---

<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

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

w<sup>l</sup><sub>jk</sub> : Denotes the weight for the connection to the kth neuron in the (l - 1)th layer to the jth neuron in the lth layer.
![Shows on a neural network where the weight is](http://neuralnetworksanddeeplearning.com/images/tikz16.png)

b<sup>l</sup><sub>j</sub> : Denotes the bias of the jth neuron in the lth layer

a<sup>l</sup><sub>j</sub> : Denotes the activation for the jth neuron in the lth layer.

![Shows the bias and activation on a neural network](http://neuralnetworksanddeeplearning.com/images/tikz17.png)

Activations of neurons are related by the following equation:

a<sup>l</sup>=σ(w<sup>l</sup>a<sup>l</sup>−1+b<sup>l</sup>)

Note: The sigmoid function (σ) is applied element by element

- "The goal of backpropagation is to compute the partial derivatives ∂C/∂w and ∂C/∂b of the cost function C with respect to any weight w or bias b in the network"
- Assumptions that need to be made about the cost function so that backpropagation can be applied.
    - "The cost function can be written as an average C=1/n ∑<sub>x</sub>C<sub>x</sub> over cost functions C<sub>x</sub> for individual training examples, x."
    - The cost can be written as a function of the outputs from the neural network
- Hadamard / Schur product ( ⊙ ) : The elementwise product of two vectors

#### Four fundamental equations behind backpropagation

__1. An equation for the error in the output layer:__

\begin{eqnarray}
  \delta^L_j = \frac{\partial C}{\partial a^L_j} \sigma'(z^L_j).
\tag{BP1}\end{eqnarray}

\partial C / \partial a^L_j : Measures how fast the cost is changing as a function of the j<sup>th</sup> output activation.

\sigma'(z^L_j) : Measures how fast the activation function σ is changing at z<sup>L</sup><sub>j</sub>.



__2. An equation for the error in terms of the error in the next layer:__

\begin{eqnarray}
  \delta^l = ((w^{l+1})^T \delta^{l+1}) \odot \sigma'(z^l),
\tag{BP2}\end{eqnarray}


(w^{l+1})^T : The transpose of the weight matrix w<sup>l+1</sup> for the (l+1)th layer


__3. An equation for the rate of change of the cost with respect to any bias in the network:__

\begin{eqnarray}  \frac{\partial C}{\partial b^l_j} =
  \delta^l_j.
\tag{BP3}\end{eqnarray}

__4. An equation for the rate of change of the cost with respect to any weight in the network:__

\begin{eqnarray}

  \frac{\partial C}{\partial w^l_{jk}} = a^{l-1}_k \delta^l_j.
\tag{BP4}\end{eqnarray}
