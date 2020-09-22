---
layout: post
title:  "Data is everywhere!"
subtitle: "Uh, where again?"
tags: ["machine learning"]
date:   2020-09-13
summary: Last night I was on a data science career panel (of awesome ladies!) as part the Vancouver Datajam 2020 and I promised (as I've been meaning to do for a while...) to post a list of data resources. 

---

Last night I was on a data science career panel (of awesome ladies!) as part the [Vancouver Datajam 2020](https://www.vancouverdatajam.ca/) and I promised (as I've been meaning to do for a while...) to post a list of data resources. The hardest part of finding data isn't finding such a list but finding such a list that is up-to-date! To that end, this list was **last verified September 13, 2020**.

A very well maintained, corporately sponsored, [model and dataset](https://www.tensorflow.org/resources/models-datasets) resource is offered by Google. Many of the datasets below are built into [tensorflow datasets](https://blog.tensorflow.org/2019/02/introducing-tensorflow-datasets.html).

### Ok, but how to divvy up the data types?

Ultimately I have a taxonomy problem: divide the data by datatype, domain or best-suited algorithm type? Finally, I'll do a mixture of all three. This is how my mind divides them; this is how I ultimately search among them; this is hopefully how such a list will be most useful.

## Curated Datasets

A breed all their own: they're uniform, tidy, split into training/validation/test sets, (over-)used to pit algorithms against each other (some curated and shared for that purpose but aren't adopted as readily). Older benchmarks are good for starting out or for hard variants of the problem statement (eg. one-shot!). In no particular order:

### Images

* [MNIST](http://yann.lecun.com/exdb/mnist/),[CIFAR-10](http://www.cs.toronto.edu/~kriz/cifar.html), and [Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist) all have ~60k images split among 10 classes
* [CIFAR-100](https://www.cs.toronto.edu/~kriz/cifar.html) 100 classes 500+100 images/class
* [ciFAIR](https://cvjena.github.io/cifair/) duplicate free versions of CIFAR-10/100
* [ImageNet](http://www.image-net.org/) is large with bigger images a decent subset annotated with bounding boxes
* [Plant Disease](https://www.kaggle.com/emmarex/plantdisease) is the [most widely used](https://arxiv.org/abs/2009.04365) in agriculture studies
* [Unsplash](https://unsplash.com/data) lite and Full (must request; some evidence they don't answer non-edu emails?)

### Segmentation & Captioning

* [Street View House Numbers (SVHN)](http://ufldl.stanford.edu/housenumbers/)
* [COCO](https://cocodataset.org/#home) is a large-scale object detection, segmentation, and captioning dataset
* [Open Images](https://storage.googleapis.com/openimages/web/index.html) image labels, bounding boxes, segmentation, relations, and narratives
* [VisualQA (VQA)](https://visualqa.org/) open-ended questions about images requiring an understanding of vision, language and commonsense knowledge to answer

### NLP 

* [Large Movie Review Dataset](http://ai.stanford.edu/~amaas/data/sentiment/) and [Sentiment140](http://help.sentiment140.com/for-students/) for sentiment analysis[^senti]
* [Twenty Newsgroups](https://archive.ics.uci.edu/ml/datasets/Twenty+Newsgroups) for text classification
* currated [Wikipedia Corpus](https://nlp.cs.nyu.edu/wikipedia-data/) or dumps from [Wikipedia](https://en.wikipedia.org/wiki/Wikipedia:Database_download) itself
* [Blog Authorship Corpus](http://u.cs.biu.ac.il/~koppel/BlogCorpus.htm) many blogs of many bloggers
* [Machine Translation](http://statmt.org/wmt18/index.html) ~15GB within various "tasks"
* [Yelp Open Dataset](https://www.yelp.com/dataset) mixes NLP with images, interaction timelines, coordinates
* [One Billion Words](https://opensource.google/projects/lm-benchmark)  a standard corpus of reasonable size (0.8 billion words)
* [PG-19](https://github.com/deepmind/pg19) extracted from Gutenberg;
* [Snowden archive](https://www.cjfe.org/snowden)
* [3m Russian Troll tweets](https://github.com/fivethirtyeight/russian-troll-tweets/) from FiveThirtyEight
* many in [torchnlp](https://pytorchnlp.readthedocs.io/en/latest/source/torchnlp.datasets.html)

For benchmarking:

* [SQuAD 1-2 datasets](https://rajpurkar.github.io/SQuAD-explorer/)
* [GLUE](https://gluebenchmark.com/) and [SuperGlue](https://super.gluebenchmark.com/)
* [*Measuring Massive Multitask Language Understanding*](https://github.com/hendrycks/test) bigger, harder to test GPT-3

[^senti]: [SentiWordNet](https://github.com/aesuli/SentiWordNet) ("assigns to each synset of WordNet three sentiment scores: positivity, negativity, objectivity") may be interesting to compare against in sentiment analysis from supervised datasets.

### Recommenders

* [MS Learning to Rank](https://www.microsoft.com/en-us/research/project/mslr/) dataset
* [MovieLens](https://grouplens.org/datasets/movielens/) 25m ratings for ~60k movies of ~160k users
* [Spotify Recsys Challenge 2018](https://github.com/tmscarla/spotify-recsys-challenge) assembled by MSc students independent of Spotify who no longer host it
* [Goodbooks-10k](https://github.com/zygmuntz/goodbooks-10k) scraped from GoodReads
* [Netflix Prize](https://www.kaggle.com/netflix-inc/netflix-prize-data), a classic
* [GroupLens](https://grouplens.org/datasets/) links to various (Book-Crossing is gone?)


### Various

* [Penn ML Benchmarks](https://epistasislab.github.io/penn-ml-benchmarks/) for supervised learning algorithms
* [AutoML/AutoDL](https://automl.chalearn.org/) competitions datasets dating back to 2016; Springer has [open access to the book](https://www.automl.org/book/) with a chapter reviewing the challenge
* [NIPS 2003 workshop on feature extraction](http://clopinet.com/isabelle/Projects/NIPS2003/) (in case you want to compare against 11.9 in the Elements)
* [OKCupid dataset](https://openpsych.net/forum/showthread.php?tid=279) N=68,371, 2,620 variables from the dating site OKCupid
* [Common Crawl](https://commoncrawl.org/the-data/) with over 8yrs of web
* [GDELT Project](https://www.gdeltproject.org/) "watching our world unfold", or (less creepy) "the GDELT Project monitors the world's broadcast, print, and web news from nearly every corner of every country in over 100 languages and identifies the people, locations, organizations, themes, sources, emotions, counts, quotes, images and events driving our global society every second of every day, creating a free open platform for computing on the entire world."
* [CS bibliography](https://dblp.uni-trier.de/) has >5m publications, use as a graph, for NLP/topics, for time series analysis


### Outlier/Anomaly/Event Detection 

* *On the Evaluation of Unsupervised Outlier Detection* [data](https://www.dbs.ifi.lmu.de/research/outlier-evaluation/DAMI/)
* [Outlier Detection Datasets (ODDS)](http://odds.cs.stonybrook.edu/)
* *Unsupervised Anomaly Detection Benchmark* [data](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/OPQMVF)
* *Anomaly Detection Meta-Analysis Benchmarks* [data](https://ir.library.oregonstate.edu/concern/datasets/47429f155)
* [Turing Change Point Dataset](https://github.com/alan-turing-institute/TCPD)
* [Geoparse Benchmark](https://revealproject.eu/geoparse-benchmark-open-dataset/) 1000s of tweets during 4 diff natural disasters
* *[MAVEN: A massive general domain event detection dataset](https://arxiv.org/abs/2004.13590)*, coming soon but apparently you can write the authors for early access.


### One/Few Shot
* miniImageNet was introduced in *Matching Networks for One Shot Learning*; *Meta-Transfer Learning for Few-Shot Learning* added tieredImageNet and Fewshot-CIFAR10 both available to [downloaded directly](https://mtl.yyliu.net/download/); also see mini on [Kaggle](https://www.kaggle.com/c/hw2-few-shot-learning/) 
* [Meta-Dataset](https://github.com/google-research/meta-dataset) assembles various datasets into one benchmark
* [Chollet's ARC dataset](https://github.com/fchollet/ARC") this one is akin to searching for patterns in [$\pi$](https://en.wikipedia.org/wiki/Pi_(film))


### Graphs
* [Stanford Large Network Dataset Collection](https://snap.stanford.edu/data/) for social graphs, roads, communication networks and more
* [Open Graph Benchmark (OGB)](https://ogb.stanford.edu/) for "a collection of realistic, large-scale, and diverse benchmark datasets"
* [OpenStreetMap](https://planet.openstreetmap.org/planet/full-history/)
* [SketchGraphs](https://github.com/PrincetonLIPS/SketchGraphs) "A Large-Scale Dataset for Modeling Relational Geometry in Computer-Aided Design"
* [Data for STREETS](https://databank.illinois.edu/datasets/IDB-3671567)
* [2013 NYC Taxi Trip Data](https://chriswhong.com/open-data/foil_nyc_taxi/)

### Symbolic Regression

Both from the universe of Max Tegmark:
* [AI Feynman](https://space.mit.edu/home/tegmark/aifeynman.html) all eqns from the Feynman lectures, includes bonus eqns
* [AI Physicist](https://space.mit.edu/home/tegmark/aiphysicist.html) considers different forces per region of space;

### Audio
* [Free Spoken Digit Dataset](https://github.com/Jakobovski/free-spoken-digit-dataset) = spoken MNIST
* [Speech Command Dataset](https://ai.googleblog.com/2017/08/launching-speech-commands-dataset.html) with 65k 1s utterances of 30 short spoken commands like "Yes", "No", "Stop", "Go"
* [Free Music Archive](https://github.com/mdeff/fma) ~900GB/343 days of Creative-Commons-licensed audio from 106,574 tracks from 16,341 artists and 14,854 albums, arranged in a hierarchical taxonomy of 161 genres
* [Million Song Dataset](https://labrosa.ee.columbia.edu/millionsong/) audio features and metadata of ~1m popular music tracks
* [LibriSpeech](http://www.openslr.org/12/) ~1k hrs of audiobooks from LibriVox
* [VoxCeleb](http://www.robots.ox.ac.uk/~vgg/data/voxceleb/) ~1m utterances by ~7k celebrities, >2k hrs
* Spotify [OpenMic](https://github.com/cosmir/openmic-2018) and [TREC](https://podcastsdataset.byspotify.com/)

and **Video**: [AViD](https://github.com/piergiaj/AViD) collected videos with a creative-commons license shared as a static dataset


## Data in the Wild

### Time Series
* [S&P 500](https://finance.yahoo.com/quote/%5EGSPC/history/)
* Spotify [Sequential Skip Prediction Challenge](https://www.aicrowd.com/challenges/spotify-sequential-skip-prediction-challenge) but this has pages of User Agreements to scroll+click through
* [CompEngine](https://comp-engine.org/) a self-organizing db of time-series data

### Climate data
* [Global climate data](https://en.tutiempo.net/climate)
* [NOAA](https://www.ncdc.noaa.gov/data-access/quick-links)
* [www.data.gov/climate](https://www.data.gov/climate)
* [AI for Earth](https://www.microsoft.com/en-us/ai/ai-for-earth-tech-resources#primaryR10)
* [Catalyst Cooperative](https://catalyst.coop/)

 Recommended by [Amanda Giang](https://mech.ubc.ca/amanda-giang/) during the discussion: 
 * [Pangeo](http://pangeo.io/) and [their github](https://github.com/pangeo-data/WeatherBench)
 * [Zenodo](https://zenodo.org/)
 * [Google Earth Engine](https://earthengine.google.com/)

### Sports stats
* [NHL](http://www.nhl.com/stats/skaters)
* [Formula-1](https://www.sportsvizsunday.com/formula-1)
* [baseball](http://www.seanlahman.com/baseball-archive/statistics/)
* [athletes](https://www.bbc.com/news/special/2012/newsspec_3734/athletes_data.txt)

## An Aggregate of Other Aggregators

* [UCI ML Repository](https://archive.ics.uci.edu/ml/index.php) "currently maintain 557 data sets as a service to the machine learning community"

* [Kaggle](https://www.kaggle.com/datasets) including such gems as the [arXiv](https://www.kaggle.com/Cornell-University/arxiv) and [avocado prices](https://www.kaggle.com/neuromusic/avocado-prices)

* [Google Public Data](https://www.google.com/publicdata/directory) is curating datasets; they also have a [Dataset Search](https://datasetsearch.research.google.com/)

* [OpenSpending](https://openspending.org/): "search over 3,446 data packages from 83 countries with over 159,706,407 fiscal records"

* [Harvard Dataverse](https://dataverse.harvard.edu/) is a repository for research data (and code!).

* [FiveThirtyEight](https://data.fivethirtyeight.com/) posts all the data to back the articles

* [Tableau Public](https://public.tableau.com/s/resources?qt-overview_resources=1#qt-overview_resources) hosted datasets

* [StatCan Data](https://www150.statcan.gc.ca/n1/en/type/data); [DataBC](https://data.gov.bc.ca/); [Vancouver Open Data](https://opendata.vancouver.ca/pages/home/); [US Data.gov](https://www.data.gov/); [NYC OpenData](https://opendata.cityofnewyork.us/); [Seattle Open Data](https://data.seattle.gov/); [Switzerland's data](http://www.dataseries.org/); etc...

* Appen hosts some [Open Source Datasets](https://appen.com/resources/datasets/)

* [KDnuggets](https://www.kdnuggets.com/datasets/index.html) has datasets galore and also aggregates yet more aggregators. Alas, some links are out of date.




