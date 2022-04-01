# Learning the English past tense

This example implements the English Past Tense network of Plunkett and
Marchman (1991), as discussed in chapter 9 of:

McLeod, P., Plunkett, K. and Rolls, E. T. (1998). Introduction to
Connectionist Modelling of Cognitive Processes. Oxford University Press.

## Understanding the network and its representations

Load `phone.mesh` in Mesh and use the commands `groups` and `projections` to
study the architecture of the network.

The input an output representations of this model are vectors of `20` bits,
each vector corresponding to a sequence of `3` phonemes plus a suffix. Each
phoneme is encoded by `6` bits that represent different phonological
features: *consonant/vowel*, *voiced/unvoiced*, *manner and position*. Each
suffix is represented by `2` bits, the `4` possible states of which
correspond to either the absence of a suffix (`00`) or to each of the three
allomorphs of the suffix *-ed*: `01 -> d`, `10 -> t`, and `11 -> ed`. Hence,
putting everything together the input and output representations are
structured as follows:

| Phoneme #1 | Phoneme #2 | Phoneme #3 | Suffix   |
| :---       | :---       | :---       | :---     |
| (6 bits)   | (6 bits)   | (6 bits)   | (2 bits) |

Use the commands `items` and `showItem` to look at some of the input-output
pairs (note that they represent artificial, but possible English strings).
The suffix mappings are: `W -> 00` (absence), `X -> 10` (`t`), `Y -> 01`
(`d`), and `Z -> 11` (`ed`). Why do you think suffixes are not coded using
phonological features? Explain the difference between the input and output
representations.

## Training the network

Train the network with the default settings (`learning rate = 0.3`,
`momentum = 0.8`), and evaluate its global performance using `test` and
`similarityStats`. Can you improve performance by tweaking these (and/or
other) parameters?

## Analysis of network performance

Examine and report the performance of the network on irregular verbs. In the
training data, the first two items are arbitrary past tense forms, then come
`410` regular, `20` no-change, and `68` vowel change verbs. Why does the
network have difficulty learning irregular verbs? Study the output
representations the model produces for irregulars. What is it doing?

Compare the performance of the network on regulars versus irregulars. Can
you identify any systematicity in the errors that the network makes?

The set `test` contains `211` verb stems that the network has not been
trained on. Make this set the active set using the `changeSet test` command,
and examine how well the model generalizes to unseen data.

Increase the token frequency of the arbitrary verbs in the `phone_train.set`
file (by copying the first two item blocks a number of times). Why should an
increase in token frequency of irregular verb stems lead to an improved
overall performance of the network?
