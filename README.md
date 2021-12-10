
<H1 align="center"> SkimLit </H1>


The purpose of this notebook is to build an NLP model to make reading medical abstracts easier.

The paper we are replicating (the source of the dataset that we'll be using) is available here : https://arxiv.org/abs/1710.06071

If you want to find the ground truth for this notebook (with lots of diagrams and text annotations) see the GitHib: https://github.com/mrdbourke/tensorflow-deep-learning/blob/main/09_SkimLit_nlp_milestone_project_2.ipynb

This notebook is inspired from  [Daniel Bourke's version](https://github.com/mrdbourke/tensorflow-deep-learning/blob/main/09_SkimLit_nlp_milestone_project_2.ipynb)

The Model categorizes the Abstracts of the Pubmed Articles into the following
* Methods
* Results
* Conclusion
* Background
* Objective


<a href="https://github.com/clannoronha/SkimLit">
  <img src="img/Skimlit_img.png" alt="Logo">
</a>

## Building a tribrid embedding model

Below is the Architecture from which this model was built with the  help of :[Neural Networks for Joint Sentence Classification in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)
<p align="center">
<a href="https://github.com/clannoronha/SkimLit">
  <img src="img/Model Architecture.PNG" alt="Logo">
</a>
</p>

1. Create a token-level model (Passes tokenized sentences to a Universal Setence Encoder)
2. Create a character-level model (tokenizes characters and passes it through an embedding layer as well as a Bidirectional LSTM)
3. Create a "line_number" model (takes in one-hot-encoded "line_number" tensor and passes it through a non-linear layer)
4. Create a "total_lines" model (takes in one-hot-encoded "total_lines" tensor and passes it through a non-linear layer)
5. Combine (using layers.Concatenate) the outputs of 1 and 2 into a token-character-hybrid embedding and pass it series of output to Figure 1 and section 4.2 of [Neural Networks for Joint Sentence Classification in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)
6. Combine (using layers.Concatenate) the outputs of 3, 4 and 5 into a token-character-positional tribrid embedding
7. Create an output layer to accept the tribrid embedding and output predicted label probabilities
8. Combine the inputs of 1, 2, 3, 4 and outputs of 7 into a `tf.keras.Model`


## Acknowledgements
* [Daniel Bourke's version](https://github.com/mrdbourke/tensorflow-deep-learning/blob/main/09_SkimLit_nlp_milestone_project_2.ipynb)
* [TFHub Universal Sentence Encoder](https://tfhub.dev/google/universal-sentence-encoder/4)
* [PubMed 200k RCT: a Dataset for Sequential Sentence Classification in Medical Abstracts
](https://arxiv.org/abs/1710.06071)
* [Neural Networks for Joint Sentence Classification
in Medical Paper Abstracts](https://arxiv.org/pdf/1612.05251.pdf)





