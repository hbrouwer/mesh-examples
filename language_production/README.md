# Exercise: Language production

We will here turn the comprehension model of:

[Venhuizen, N. J., Crocker, M. W., and Brouwer, H. (2019). Expectation-based
Comprehension: Modeling the Interaction of World Knowledge and Linguistic
Experience. *Discourse Processes, 56*:3,
229-255.](https://www.tandfonline.com/doi/full/10.1080/0163853X.2018.1448677)

into a model of language production. First, [refresh your
memory](https://github.com/hbrouwer/mesh-examples/tree/main/expectation_comprehension)
on this comprehension model.

## From comprehension to production

In order to turn the comprehension model into a model of production, we
should flip the inputs (from sequences of words to sentence meanings) and
target outputs (from sentence meanings to sequences of words) in the
training data. This has been done for you, and the resultant training
patterns can be found in `venhuizen_train_prod.set`.

Now copy the network specification `venhuizen.mesh` to
`venhuizen_prod.mesh`, and alter it to turn the comprehension model into
a production model. Some things to consider: 

* What should the architecture of the model look like?
* What are the appropriate layer dimensions?
* What activation functions should you use?
* What parameters should you use to train the model?
* How to evaluate model performance?
* ...
