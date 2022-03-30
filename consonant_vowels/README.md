# Consonant-vowel dependencies (ba dii guuu)

This example is taken from chapter 8 of:

Plunkett, K., and Elman, J. (1997). Exercises in rethinking innateness:
A Handbook for Connectionist Simulations. MIT Press.

The aim of this tutorial is to get familiar with the processing of sequences
over time, using Simple Recurrent Networks (SRNs).

## Understanding the network and its representations

Load `srn.mesh` in Mesh and use the commands `groups` and `projections` to
study the architecture of the network. Verify that the network is an SRN.

The input and output representations of this model are 4-bit vectors:

| Letter | Bit1  | Bit2  | Bit3  | Bit4  |
|  :---: | :---: | :---: | :---: | :---: |
|    b   |   1   |   1   |   0   |   0   |
|    d   |   1   |   0   |   1   |   0   |
|    g   |   1   |   0   |   0   |   1   |
|    a   |   0   |   1   |   0   |   0   |
|    i   |   0   |   0   |   1   |   0   |
|    u   |   0   |   0   |   0   |   1   |

In each of these vectors, the first bit represents the consonant feature,
while the other three bits are localist representations of each consonant
and vowel. The training patterns in the set `train` specifies a sequence of
these letters, and we are going to train the model on next letter
prediction. Take a look at the `items` to examine how the training data is
structured. What does each item encode?

## Training the network

Train the network with the default settings (`learning rate = 0.1`,
`momentum = 0.3`, `epochs = 70000`; `batch size = 1`), and evaluate its
performance using `test` and `similarityStats`. Why does the the error stay
relatively high? Note: take into account the development of the error over
training.

## Analysis of network performance

Activate the `test` set (`changeSet test`), and examine the items in this
set. What letter sequence is this set testing? Test the network using this
sequence. Examine the behaviour for each letter in the sequence.

How well has the network learned to predict the next element in the
sequence? Does it correctly predict the vowel following a consonant? Does it
correctly predict the number of vowels?

Does the network predict when a consonant will be the next item in the
sequence? Why do you think it has or has not?

Finally, we can examine the network's solution through a cluster analysis.
First, record the hidden unit activation patterns for each of the items (in
the active `test` set) by typing `recordUnits hidden hidden.txt`. Now quit
Mesh, start R, and type the following:

```
data <- read.csv("hidden.txt", head=T)
mtx <- data[,6:ncol(data)]
rownames(mtx) <- paste(data$ItemId, data$ItemName, data$ItemMeta)
str(as.dendrogram(hclust(dist(mtx))))
```

What does the dendogram tell about the solution of the network?
