# Warming up: Activation propagation

Consider the following network:

```

  ( O1 )  ( O2 )
   |  \    /  |
   |   \  /   |
   |    \/    |
.75| .25/\.5  |.25
   |   /  \   |
   |  /    \  |
  ( I1 )  ( I2 )

```

and the input (I1, I2) and target (T1, T2) patterns in the table below:

|  I1   |  I2   |  T1   |  T2   |  O1   |  O2   |
| :---: | :---: | :---: | :---: | :---: | :---: |
|   0   |   0   |   0   |   0   |       |       |
|   1   |   0   |   1   |   1   |       |       |
|   0   |   1   |   1   |   1   |       |       |
|   1   |   1   |   2   |   2   |       |       |

Assume a linear activation function on the output nodes (O1, O2), and
determine their activation levels, given input patterns in the table above.

## Activation propagation using Mesh

Now verify your solution using `Mesh`. Load the network by typing:

```
$ mesh net_input.mesh
Mesh, version 1.0.0: https://github.com/hbrouwer/mesh (`?` for help)
...
> Loaded file                    [ net_input.mesh ]
  [net_input:data>
```

Next, load the predefined weights using the `loadWeights net_input.weights`
command, and type `showMatrix weights input output` to see the effect. Do
the weights match those in the figure?

You can now propagate the activation using Mesh. The command `items` lists
all items in the current example set, and the command `testItem` either
takes the number (first column) or name (second column) of an item as
argument. Do the numbers match the ones you calculated by hand?

Explore the network some further, using the commands `groups` and
`projections` (and if you want even more information, try `inspect`). Which
group was omitted in the figure? Study the weights between this group and
its recipient. Was it legitimate to omit in the figure? Finally, type
`weightStats`. Do these numbers make sense?

## Training the network

Let us now try to improve the network. Type `init` to reset the weights, and
use `weightStats` to confirm. Now type `train`, and study the output. What
happens to the error? How many times has the network been exposed to each
example pattern?

Look at the different items. Has the network improved?

Run `train` again. And now? Repeat one more time. And now?
