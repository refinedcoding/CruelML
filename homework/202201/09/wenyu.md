# RNN day 2 

## implementation 

- We can train an RNN-based character-level language model to generate text following the user-provided text prefix.
- A simple RNN language model consists of input encoding, RNN modeling, and output generation.
- RNN models need state initialization for training, though random sampling and sequential partitioning use different ways.
- When using sequential partitioning, we need to detach the gradient to reduce computational cost.
- A warm-up period allows a model to update itself (e.g., obtain a better hidden state than its initialized value) before making any prediction.
- Gradient clipping prevents gradient explosion, but it cannot fix vanishing gradients.

## vanishing gradients

- One of the problems with naive RNNs that they run into **vanishing gradient** problem.
- An RNN that processes a sequence data with the size of 10,000 time steps, has 10,000 deep layers which is very hard to optimize.
- Suppose we are working with language modeling problem and there are two sequences that model tries to learn:
    - "The **cat**, which already ate ..., **was** full"
    - "The **cats**, which already ate ..., **were** full"
    - Dots represent many words in between.
- What we need to learn here that "was" came with "cat" and that "were" came with "cats". The naive RNN is not very good at capturing very long-term dependencies like this.
- *Vanishing gradients* problem tends to be the bigger problem with RNNs than the *exploding gradients* problem. 
- Exploding gradients can be easily seen when your weight values become `NaN`. 
- So one of the ways solve exploding gradient is to apply **gradient clipping** means if your gradient is more than some threshold - re-scale some of your gradient vector so that is not too big. So there are cliped according to some maximum value.
