# Boolean functions

These examples are taken from chapter 3 of:

Plunkett, K., and Elman, J. (1997). Exercises in rethinking innateness:
A Handbook for Connectionist Simulations. MIT Press.

This tutorial investigates the training of networks to learn the boolean
functions: **AND**, **OR**, and **XOR**:

|  IN1  |  IN2  |  AND  |  OR   |  XOR  |
| :---: | :---: | :---: | :---: | :---: |
|   0   |   0   |   0   |   0   |   0   |
|   0   |   1   |   0   |   1   |   1   |
|   1   |   0   |   0   |   1   |   1   |
|   1   |   1   |   1   |   1   |   0   |

## Two-layer networks

### Learning AND

The `and.*` files specify a network for the **AND** function. Train the
network using the `train` command, and then type `test` to see the network's
performance on the entire training set:

```
Number of items:                 4
Total error:                     0.142309
Error per example:               0.035577
Root Mean Square (RMS) error:    0.266748
# Items reached threshold:       0 (0.00%)
```

Note that the error function that is minimized is the sum of squares
function defined as: `1/2 sum_j (y_j - d_j) ^ 2`.

You can now examine the output for each of the training items. Use `items`
to list all items, and use the `testItem` command to inspect individual
examples (by name or number). Has the network successfully learned the
**AND** function? What was your criterion for this decision?

Assume the following success criterion: activation `>0.6` corresponds to
`1`, and activation `<0.4` corresponds to `0`. We can factor this criterion
into the error function by typing `set ZeroErrorRadius 0.4`. Retrain the
network by typing `init` (which will reinitialize the weights) followed by
`train`, and inspect the global and by-item error. Has the network learned
the **AND** function in accordance with the success criterion? Now try again
with `set ZeroErrorRadius 0.1`. Do the global and by-item error make sense?
Has the network learned the function in accordance with the criterion? Type
`set MaxEpochs 10000`, and retrain the network. How about now?

### Learning OR

The `or.*` files specify a network for the **OR** function. Is the network
able to learn this function? Try experimenting with different parameters
(see those under `steepest` in the output of `help updating`). Does this
affect the network's performance?

### Learning XOR

The file `xor_2layers.mesh` specifies a network for the **XOR** function.
Try training this network using varying parameters and numbers of epochs.
Also, try varying the random seed using the `set RandomSeed <value>`
command. Can you make the network learn the **XOR** function? Why not?

## Three-layer networks

Now try again using the network specified in `xor_3layers.mesh`. Does this
network succeed in learning the **XOR** function? Can you tell this from the
global error?

Store the weights using `saveWeights weights.txt` and record the hidden
units using `recordUnits hidden hidden.txt`. Now study the resultant `.txt`
files. Do you understand why it works? Note: do not forget about the bias
units! What do the hidden units encode?

Alter `xor_3layers.mesh` such that the hidden layer contains `5` units.
Train this model, save the weights and record the hidden units. How does the
network use the additional units?
