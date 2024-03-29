---
layout: post
use_math: false
use_carousel: true
title:  "Embeddings"
subtitle: "They aren’t just for text"
tags: ["machine learning"]
date:   2023-07-12
summary: Some introductory notes on embeddings are pre-reading for our data science paper reading group.

---


> “The representation perspective of deep learning is a powerful view that seems to answer why deep neural networks are so effective. Beyond that, I think there’s something extremely beautiful about it: why are neural networks effective? Because better ways of representing data can pop out of optimizing layered models.”
> 
> from [Deep Learning, NLP, and Representations](https://colah.github.io/posts/2014-07-NLP-RNNs-Representations)

In machine learning, an embedding is a technique for converting data objects (such as words or images), potentially sparse, into low-dimensional vectors where each vector represents its corresponding object. This conversion process allows us to use these vectors to perform various tasks such as classification or regression. Embeddings are used widely in many areas of machine learning, including natural language processing, computer vision, and graph analysis.

Outside of textual data, for example, there are image embeddings, audio embeddings, and graph embeddings. For example, in image recognition tasks, CNNs learn image embeddings that capture visual patterns at different scales that can then be used for image classification, retrieval, or segmentation tasks.  In audio, recall in the VALL-E paper that they used a neural audio codec model trained to compress and decompress digital audio files. The intermediate encoding is an audio embedding.

In graph analytics, node and edge features can be combined to create graph embeddings that encode information about the structure and connectivity of the graph. These embeddings can be useful for solving problems like link prediction, community detection, or clustering. See [node2Vec](https://arxiv.org/abs/1607.00653) and [GraphSAGE](https://arxiv.org/abs/1706.02216). 

![GraphSage](/assets/images/embeddings/graphsage.png)

<p class="caption">The “unrolled” equivalent neural network of <a href="https://github.com/dsgiitr/graph_nets/blob/master/GraphSAGE/GraphSAGE_Code%2BBlog.ipynb">GraphSAGE</a></p>

In [recommender systems](https://eugeneyan.com/writing/system-design-for-discovery/), item embeddings reduce the dimensionality of the item catalog and allow for fast vector-search retrieval. New items can be cast into the item embedding space using similarity metrics based on item features before users have interacted with them at all. User embeddings alleviate the cold start problem in the same way.


![Movie Embeddings in a Recommender](/assets/images/embeddings/movie_embeddings.svg)

<p class="caption">A sample DNN architecture for learning movie embeddings from collaborative filtering data. From Google crash course on <a href="https://developers.google.com/machine-learning/crash-course/embeddings/obtaining-embeddings">embeddings</a></p>

Embeddings may finally allow neural network approaches to beat gradient boosted trees in tabular datasets:

![Tabular embeddings that finally compete with tree algorithms](/assets/images/embeddings/tabular-embeddings.png)

<p class="caption">First, continuous features are expanded into quantile bins to create higher dimensional sparse features; then, learned embeddings of these features allow the neural network to outperform CatBoost in a synthetic GBDT-friendly task. <a href="https://arxiv.org/abs/2203.05556">https://arxiv.org/abs/2203.05556</a></p>


## Learning Embeddings

Much like the original [word2vec](https://www.tensorflow.org/tutorials/text/word2vec) or more modern language models, a surrogate task can be used to train embeddings: for sequences, predicting masked items (as in a [MLM](https://huggingface.co/docs/transformers/main/tasks/masked_language_modeling) like BERT) or predicting next items (as in a [causal language model](https://huggingface.co/docs/transformers/main/tasks/language_modeling) like the GPT family); for tabular data, the surrogate task can be the prediction of one column based on the others; for image data, predicting the category of image is a common task. In a recommender task, predicting the rating a user will assign an item is a good task if such labels are available; predicting an implicit signal such as if they’ll choose an item from the selection or how long they’ll watch a video once they start it. Often, items selected can form a sequence and many of methods from language modelling can be used, eg. [BERT4Rec](https://arxiv.org/abs/1904.06690).

The surrogate task doesn’t have to be the task you want the embeddings for; it should however depend on factors/features that are important for your downstream task. Eg. for the [chairs dataset](https://www.di.ens.fr/willow/research/seeing3Dchairs/), if your surrogate model classifies the chair orientation, the resulting embeddings would do poorly to predict the chair style. 

Furthermore, if you finetune your general purpose embeddings to a specific task, don’t expect them to still be useful for other tasks, see [here](https://itnext.io/changes-of-embeddings-during-fine-tuning-c22aa1615921) as an example.


## Vectors Properties of Embeddings

The famous example popularized in the [word2vec paper](https://arxiv.org/abs/1301.3781) (but first appearing in [Linguistic Regularities in Continuous Space Word Representations](https://aclanthology.org/N13-1090/))

<p style="text-align: center;">King - Man + Woman = Queen</p>

(though apparently, that expression requires [tweaking](https://blog.esciencecenter.nl/king-man-woman-king-9a7fd2935a85)). Why would the embeddings lie in a vector space? Frankly, the better question is: why wouldn’t they?

Since the underlying models are overwhelmingly linear and frequently shallow (word2vec has a single hidden layer; GloVe embeddings approximate the full word co-occurrence matrix by a low rank decomposition), we should expect embeddings to lie in a vector space where similar items will be close. 


> “Representing features as different directions may allow _non-local generalization_ in models with linear transformations (such as the weights of neural nets), increasing their statistical efficiency relative to models which can only locally generalize.”
> 
> from [Toy Models of Superposition](https://transformer-circuits.pub/2022/toy_model/index.html)[^1], they refer to a [paper by Bengio](https://arxiv.org/abs/1206.5538) and a [blog post](https://colah.github.io/posts/2014-07-NLP-RNNs-Representations)

This linearity will only be broken when there are interactions among features. In natural language, words can combine to form an altogether different meaning: eg. “[wentelteefje](https://www.thedutchtable.com/2014/02/wentelteefjes.html)”; “to fast”; or idioms such as “to break the ice”, “to let the cat out of the bag” or “to table an issue”. But these examples are a minority, and overwhelmingly most writing (on the internet) is simple and “additive”. 


## References

[Representation Learning Without Labels](https://icml.cc/virtual/2020/tutorial/5751), excellent tutorial series at ICML 2020. 


<!-- Footnotes themselves at the bottom. -->
## Notes

[^1]:
     This post is excellent and I highly recommend reading!
