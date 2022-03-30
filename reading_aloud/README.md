# Reading aloud

This example is implements the Reading Aloud network of Plaut et al. (1996),
as discussed in chapter 8 of:

McLeod, P., Plunkett, K. and Rolls, E. T. (1998). Introduction to
Connectionist Modelling of Cognitive Processes. Oxford University Press.

## Understanding the network and its representations

First, load `plaut.mesh` in Mesh and use the commands `groups` and
`projections` to study the architecture of the network (note that this is
not the attractor model). 

\noindent Next, study the input and output representations (use `items` to
list items). The command `showItem` takes an item number or name. By default
Mesh will show you a graphical representation of the binary vectors for this
network (you can disable this with the `togglePrettyPrinting` command). The
`Name:` field of each item denotes a given word, and the `Meta:` field
a string of phonemes. Note that Plaut does not tell us exactly how the
orthography groups (onset, vowel, coda) are encoded in the binary input
representations, but you can get a general idea.

## Training the model

We can now train the model to learn to read aloud! Type `train` to train the
model for `300` epochs.  erify the network has learned, using the commands
`test` and `similarityStats` (which informs you about how similar each
output pattern is to its target, as well as for what fraction of items the
produced output is more similar to its intended target than to any other
target) to inspect global performance, as well as by using `testItem}` to
examine by-item performance.

## Generalization

The set `test` contains two previously seen words HAVE and SAVE and the
non-word MAVE. Make this set the active set by typing `changeSet test` (this
should change the prompt). Compare the the network's performance on these
words. How does it behave?

Try altering the training regime, by editing `plaut.mesh`, to qualitatively
change the behavior of the model. What did you do and what changed? (free
inspiration: try setting the random seed to `15` and train the model for
`600` epochs).
