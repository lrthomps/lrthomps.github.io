---
title:  "There ain't no such thing as a free lunch"
categories: ["machine learning"]
date:   "2018-06-20"
description: Notes on the No Free Lunch Theorems for Optimization paper. 
page-layout: full
title-block-banner: true

---

[No Free Lunch Theorems for Optimization]<https://georgemaciunas.com/wp-content/uploads/2012/07/Wolpert_NLFoptimization-1.pdf>, D.H. Wolpert, W.G. Macready.

A bar offering a free lunch will likely charge more for drinks. If an algorithm performs well on a certain class of problems then it necessarily pays for that with degraded performance on the set of all remaining problems.

*Theorem 1* states that for any two algorithms the sum of the probability of a given sample over all loss functions is equal. Or:

**For any pair of algorithms, the average expected performance over all cost functions is equal.**

*"If an algorithm performs better than random search on some class of problems then in must perform worse than random search on the remaining problems. Thus comparisons reporting the performance of a particular algorithm with a particular parameter setting on a few sample problems are of limited utility. While such results do indicate behavior on the narrow range of problems considered, one should be very wary of trying to generalize those results to other problems."*

This allows still for problems to exist such that algorithm 1 fares much better than algorithm 2 where no problems exist in which 2 performs much better than 1; there must be many many problems for which 2 does (only) somewhat better than 1 for balance out.

#### Time dependence
*Theorem 2* extends this to time-varying loss functions replacing the sum over loss functions to a sum over time. I consider this version to understand NFL for machine learning problems: the set of examples can be imagined to grow with "time"; the training set is a minimization problem for a particular loss function, extending to more and more examples is effectively evolving loss function with those additions. 
#### Non-flat priors *P(f)*
If we're worried that a flat distribution over problems is unrealistic (not all problems are equally likely1), no worries because the proof extends to a variety of non-flat priors *P(f)*: this can be interpreted as averaging over classes of algorithms rather than all algorithms. The sum over *f* becomes weighted by the prior *P(f)*. This can be restated as an inner product in *f* space. Geometrically, an algorithm performs well for a given class of problems or is well *matched* if the vectors *P(f)* and *v(f) = P(d_m^y | f, m, a)* are co-linear. The authors show that the magnitude of *v(f)* is independent of algorithm *a*, so the *match* is detemined solely by the alignment of the algorithm to problem space. 

#### Stochastic algorithms
Can be extended also to stochastic algorithms.

#### Best algorithm for a fixed problem?
Suppose we test two algorithms on a subset to compare them. Should be chose the one with lower loss? the one with higher loss?

*Theorem 10*: There is no a priori justification for using any particular choosing procedure.

*"If one restricts [consideration] to only be over those algorithms that are a good match to the [current problem], then it is often the case that “stupid” choosing procedures (pick the worse performer on the subset) outperform “intelligent” ones (versus picking the better performer)."* 

Another paper is focused on supervised learning: *The Lack of A Priori Distinctions Between Learning Algorithms* by David H. Wolpert, Neural Computation **8**, 1341-1390 (1996). In this paper, the equivalent NFL is that "there are as many targets for which it is preferable to choose between two learning algorithms based on which has larger cross-validation error (“anti-cross- validation”) as based on which has smaller cross-validation error."

## Applications!
### Information Theory
*Theorem 3*: What fraction of problems yield the same sample losses?  (Independent of algorithm according to NFL!) this is related to the entropy of the distribution of sample losses. 

*Theorem 4*: Given a specific problem (actually, only the distribution of losses it gives), what fraction of algorithms will yield a particular sample loss distribution? This is related to the Kullback–Liebler distance between the distributions of the problem and the sample losses.

### Performance Metrics
*Theorem 7*: For a given problem with *m* oracle evaluations, the fraction of algorithms that find a minimum (wlog) > *eps* is a simple function of fraction of cost evaluations over the entire search domain that are > *eps*.

One can then compare an algorithm to all others (including random):
* given *m* oracle evaluations on a particular run, what fraction of algorithms would have found a larger minimum (done worse)?
* given *m* steps, how many further *k* steps until the algorithm finds a smaller minimum? how does this compare with the expected number of points searched at random? In particular, the expected random search takes *1/z(d) - 1* steps, where *z(d)* is the fraction of the remaining search space with a loss lower than the current loss.
* how does the algorithm compare with random throughout the entirety of its search? are there "hard/slow" parts?  

## Notation
*x* is a point in the search space 

*y* is the cost 

*f* is the loss function such that *f(x) = y*

The time-ordered "sample" of size *m* (that is, a search with *m* distinct visited points, wasteful duplication of oracle calls are ignored) is given by *{(d_m^x(0), d_m^y(0)), ... ((d_m^x(m), d_m^y(m))}*.  *d_m^x(i)* indicates the *X* value of the *i*th successive element in a sample of size *m* and *d_m^y(i)* is its associated cost or *Y* value.

*P(f)* is a prior distribution encoding what we know for a given class of problem about the behaviour of its cost function. 

*P(d_m^y | f, m, a)* is the probability of a given sample of size *m* for loss function *f* directed by algorithm *a*