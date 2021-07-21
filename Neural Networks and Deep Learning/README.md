# Neural Networks and Deep Learning (Course 1):

Some of the cases that are briefly mentioned, it turns out that if you have a linear activation function here and a sigmoid function here, then this model is no more expressive than standard logistic regression without any hidden layer. So I won't bother to prove that, but you could try to do so if you want. But the take home is that a linear hidden layer is more or less useless because the composition of two linear functions is itself a linear function.

So unless you throw a non-linear activation function in there, then you're not computing more interesting functions even as you go deeper in the network.  

ReLU actuvation is better most of the times.
Leaky RelU:
g(z) = max(0.001z,z)

We don't need to take derivatives with respect to the input x, since input x for supervised learning w.r.t x. We're not trying to optimize x, so we won't bother to take derivatives, at least for supervised learning with respect to x.

For a variable foo, 
foo & dfoo have the same dimensions.