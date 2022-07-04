# Next word prediction

We will train a model to predict the next word of a sentence. This model
will be trained on the sentences used in:

[Venhuizen, N. J., Crocker, M. W., and Brouwer, H. (2019). Expectation-based
Comprehension: Modeling the Interaction of World Knowledge and Linguistic
Experience. *Discourse Processes, 56*:3,
229-255.](https://www.tandfonline.com/doi/full/10.1080/0163853X.2018.1448677)

which are derived from the following grammar:

| Head           | Body                                                          |
| :--:           | :--:                                                          |
| S              | NP*person* VP*v*=[*order*/*eat*/*drink*/*menu*/*pay*/*leave*] |
| S              | NP*person* VP*v*=[*enter*/*menu*/*pay*] CoordVP*v*            |
| NP*person*     | beth / dave / thom                                            |
| NP*place*      | the cinema / the restaurant                                   |
| NP*food*       | dinner / popcorn                                              |
| NP*drink*      | champagne / cola / water                                      |
| VP*enter*      | entered NP*place*                                             |
| VP*menu*       | asked for the menu                                            |
| VP*order*      | ordered NP*food* / ordered NP*drink*                          |
| VP*eat*        | ate NP*food*                                                  |
| VP*drink*      | drank NP*drink*                                               |
| VP*pay*        | paid                                                          |
| VP*leave*      | left                                                          |
| CoordVP*enter* | and VP*menu* / and VP*order* / and VP*leave*                  |
| CoordVP*menu*  | and VP*order* / VP*leave*                                     |
| CoordVP*pay*   | and VP*order* / VP*leave*                                     |

This grammar combines 21 words into a total of 117 different sentences. Not
all sentences are, however, equally frequent in the training set. More
specifically, there are:

* **Highly frequent sentences:** (x9): "NP*person* ordered dinner",
  "NP*person* ate popcorn", "NP*person* ordered champagne", "NP*person*
  drank water"; 
 
* **Relatively frequent sentences:** (x5): "NP*person* ordered cola",
  "NP*person* drank cola";

* **Sentences that occur only once:** (x1): All other sentences.

The total training set consists of 237 sentences. 

## Understanding the model and its representations

First, load `next_word.mesh` in `mesh` and use the commands `groups` and
`projections` to study the architecture of the network. What type of
architecture does the model have? The activation function at the output
layer is the [softmax](https://en.wikipedia.org/wiki/Softmax_function)
activation function. Can you think of why this activation function is used?

Next, study the input and output representations, using the command `items`,
as well as the command `showItem`, which takes an item number or name. The
meta field should help you interpret the input and output bits. How are the
training sentences coded?

## Training the model

We can now train the model to predict the next word of a sentence. Type
`train` to train the model, and study its performance once training is
completed. Use `test` and `similarityStats` to inspect global performance,
and `testItem` to examine by-item performance. Does the network behave as
expected? Explain what the model is doing.

## Quantifying word expectations

The activation values at the output layer can be interepreted as the
conditional probability of each potential next word, given the sentence thus
far (use `togglePrettyPrinting` to see the actual values). Indeed, if we
take the negative logarithm of the conditional probability of a word W*t+1*
we obtain its surprisal: 

surprisal(W*t+1*) = -log P(W*t+1*|W*1*...W*t*) 

Given "beth ordered", compute the surprisal of "dinner" and "popcorn". Do
these values make sense?

Because the entire training set is known, we actually know the exact
*offline* surprisal values. The command `dssWordInfo` takes two arguments:
a set of sentences, and the name or number of a sentence in that set, e.g.,
`dssWordInfo train "beth ordered dinner"` or `dssWordInfo train 190`. This
will output different surprisal and entropy metrics, but for now you only
need to be concerned with `Ssyn` which gives the offline surprisal for each
word. How do the offline surprisal values compare to those derived from the
model?

As a final exercise, type `set MaxEpochs 20` followed by `init`, and retrain
the network using `train`. How do the network derived surprisal estimates
now compare to the offline values? Type `train` to train for another 20
epochs. How do the estimates change?
