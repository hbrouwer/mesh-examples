# Expectation-based comprehension

This implements the Surprisal model of:

[Venhuizen, N. J., Crocker, M. W., and Brouwer, H. (2019). Expectation-based
Comprehension: Modeling the Interaction of World Knowledge and Linguistic
Experience. *Discourse Processes, 56*:3,
229-255.](https://www.tandfonline.com/doi/full/10.1080/0163853X.2018.1448677)

## Exploring the model

Load the model by typing `mesh venhuizen.mesh`, and explore it using the
commands: `groups`, `projections`, and `inspect`. Also take a look at the
training sentences, their corresponding semantics, and the input-output
vectors (using `items` and `showItem`). How are the input-target pairs for
a single sentence are structured?

This network is pre-trained. Examine its performance, using the commands
`test` and `similarityStats`. As the output vectors of the model are DSS
representations, its performance can also be evaluated in terms of the
by-item `comprehension(target,output)` score, using the command `dssTest`.
Identify for which type of sentence the performance of the model is the
worst. Can you think of why?

Also, compare the sentence `dave paid (#41)` with `dave paid and ordered
cola (#91)`. Can you explain the behavior of the model?

## Inferencing

One of the distinctive features of DSS representations is that they allow
for direct *world knowledge*-driven inference. For instance, we can study on
a word-by-word basis the degree to which the atomic propositions that
constitute a DSS space are inferred to be (or not to be) the case when
processing a given sentence.

The command `dssScores` allows one to do this. It takes two arguments: a set
of atomic propositions, and the name or number of a sentence in the active
set. The set `events` contains the atomic propositions for the present DSS
space. Hence, type `dssScores events "beth left"` or `dssScores events 43`.
Do you understand what is shown in the revelant rows and columns?

The command `dssInferences` makes exploring inferencing a little less
overwhelming (but also less awesome!). In addition to a set of atomic
propositions, and the name or number of a sentence in the active set, it
takes a threshold value for the (absolute) comprehension scores:
`dssInferences events "dave left" .3` or `dssInferences events 44 .3`.

## Comprehension-centric Surprisal

The command `dssWordInfo` takes two arguments, a set of sentences, and the
name or number of a sentence in that set, e.g., `dssWordInfo train "dave
paid"` or `dssWordInfo train 41`. This will output different offline
syntactic and semantic Surprisal metrics, as well as the DSS-derived online
metric of Surprisal, for each word in a sentence. The Surprisal metrics are
prefixed with a capital `S'. The metrics prefixed with `DH' are the entropy
reduction counterparts (see [Venhuizen, Crocker, Brouwer, 2019,
*Entropy*](https://www.mdpi.com/1099-4300/21/12/1159)).

Find a pair of sentences for which online Surprisal follows *linguistic
experience*. Which contrast did you pick? Try to explain how the different
Surprisal values arise.

Now find a pairs of sentences for which online Surprisal follows *world
knowledge*. Again, try to explain how the different Surprisal values arise.
