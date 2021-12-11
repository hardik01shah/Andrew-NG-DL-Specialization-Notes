# Tuning of Hyperparameters:

## Split into data sets:
Typically 60/20/20 into train/dev/test
But if you have large data say like 1,000,000 then even 98/1/1 can work.

## Bias and Variance:
Underfitting -> High Bias
High train and dev set error
To fix introduce more layers, more input features, more neurons

Overfitting -> High Variance
Very low train set error and some dev set error
To fix more data

## Regularization:
We mostly don't include the bias term in regularization because that is just one parameter compared to the other large number of weights. So, regularizing one parameter doesn't make much of a difference.

Regularization parameter(lambda) is a hyperparameter that needs to be decided using the dev set.

For logistic regression: L2 Norm
For neural network: Frobenius norm (similar to L2 norm but for a matrix)
This sum of squares of all elements of a matrix

L2 regularization also called 'Weight Decay' as in every regularization step, the weights decrease.

## Methods to prevent overfitting:
1. Regularization
	1. L2
	2. Drop Out (inverted drop out)
2. Data Augmentation
3. Early Stopping

## Normalization:
Use same mu and sigma to scale the train and dev sets. Do not scale the sets differently.

## Vanishing and Exploding Gradients:
The activations will increase or decrease exponentially as a function of L(number of layers), and a similar argument can be used to show that the derivatives or the gradients the computer is going to send will also increase exponentially or decrease exponentially as a function of the number of layers. Hence, learning rate can increase or decrease exponentially as the gradient descent can take very small steps or large steps and this can make training difficult.

## Gradient Checking:
When trying to check gradients with dropu-out regularization, use keep-prob = 1.0 and then check.

## MiniBatch Gradient Descent:
For e.g. training examples = 5,000,000
mini-batch size = 1000
In each epoch, the algotrithm takes 5000 gradient descent steps, in contrast to the batch gradient descent that takes a single step in each epoch.
In minibatch, each minibatch is used to update the weights and biases but in batch all examples are used together to update.

mini-batch size = m -> batch gradient descent
mini-batch size = 1 -> stochastic gradient descent

Stochastic gradient descent will never converge. Oscillates around the minimum.

## Adam Optimization:
Exponentially Weighted Moving Averages (EWMA)
Combination of RMSprop and Gradient descent with momentum

## Hyperparams for adam:
alpha -> needs to be tuned
beta1 -> 0.9
beta2 -> 0.999
epsilon -> 10e-8

## Important Hyperparams:
1. learning_rate
2. beta, hidden units, mini batch size
3. number of layers, learning_rate decay
4. (beta1, beta2, epsilon for adam) -> rarely required to tune, take as default

## Batch Norm:
Gamma and beta ensure that the Z~ does not lie only between (0,1) as this could affect the activations if an activation function like sigmoid is used. Gamma and beta can be used to set the mean and variance of Z~ as required by the activation function.

There is no point in having biases (b) as a parameter in batch norm, since calculation of Znorm will cancel the effect of biases on Z.

Increasing the mini-batch size reduces the regularization effect of batch norm.

## Softmax classification:
Decision Boundary identified by a softmax classifier(without hidden layers) will be linear.
The sum of activations after softmax will be 1. The activations typically give the probability of each class. 

## Note:
If there is a huge gap between the dev set error and the test set error, it implies that the nn is overfitting the dev set. To solve, add more examples/data to the dev set so that the model generalizes well on the test set.
