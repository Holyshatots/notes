# (Neural Networks and Deep Learning)[http://neuralnetworksanddeeplearning.com/index.html] by Michael Nielsen

## (Chapter 1 : Using neural nets to recognize handwritten digits)[http://neuralnetworksanddeeplearning.com/chap1.html]

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
