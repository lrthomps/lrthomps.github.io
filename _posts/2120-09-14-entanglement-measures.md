---
layout: post
use_math: true
title:  "A Quantum Evaluation of Disentangled Representations"
tags: ["physics", "machine learning", "representation"]
date:   2120-09-14
summary:  "Some representations are easier to learn from than others. How can we assure that the representations are most useful for many and any downstream tasks?"

---

> Friend: what does "disentangle" mean in this context?
>
> Me: e.g. a representation for a robot of a scene shouldn't mix the encoding of space with texture or colour. the physics notion carries over: the subspaces should be factored subsets
>
> Friend: so in a dumbed down sense, it's a measure of how linearly independent the subspaces are?
>
> Me: yes, but drop the word 'linear'

Some representations are easier to learn from than others. Consider chess: in the abstracted representation of named pieces at various board positions with enumerated legal actions is far simpler than the real world chess board on a table in a room in front of a robot.

* For classification, the input data is abstracted further with each layer and the representation is disentangling the output among the prediction classes  
* Autoencoder or encoder-decoder networks are shaped explicitly to learn embeddings, e.g. [word2vec](https://arxiv.org/abs/1310.4546)
* [Cambridge Analytica](https://www.theguardian.com/news/series/cambridge-analytica-files) used online personality tests to cast users into a [five-dimensional embedding](https://en.wikipedia.org/wiki/Big_Five_personality_traits)
* Generative adversarial networks (GANs) learn to transform an input "noise" variable into samples indistinguishable from the real data, e.g. from the same distribution

Whereas in the supervised setting evaluating the quality of a representation is simple because the task is known and trained for directly. In the unsupervised setting, the downstream tasks are various and not (entirely) known at training time. The reconstruction error does not seem to correlate well with performance on (certain) downstream tasks[^beta-VAE] and, for generative algorithms, at best, we are left with visual inspection.

[^beta-VAE]: Irina Higgins, Loic Matthey, Arka Pal, Christopher Burgess, Xavier Glorot, Matthew Botvinick, Shakir Mohamed, and Alexander Lerchner. [β-VAE: Learning basic Visual Concepts with a Constrained Variational Framework](https://openreview.net/forum?id=Sy2fzU9gl). In 5th International Conference on Learning Representations, 2017.

How can we assure that the representations are most useful for many and any downstream tasks? There must be a trade-off in the compression vs expressiveness of the representation but, also, in which *generative factors* are preserved and what data is lost. Just like some coordinate systems are more natural for certain problems, some representations may be more suitable to certain downstream paths. This is not only a problem in unsupervised learning: even in the supervised setting, we want to assure that the learned representation *generalizes* from the training set to the real world[^adversarial][^texture][^shortcut].

[^adversarial]: Andrew Ilyas, Shibani Santurkar, Dimitris Tsipras, Logan Engstrom, Brandon Tran, Aleksander Madry. [Adversarial Examples Are Not Bugs, They Are Features](https://arxiv.org/abs/1905.02175), 2019.
[^texture]: Robert Geirhos, Patricia Rubisch, Claudio Michaelis, Matthias Bethge, Felix A. Wichmann, Wieland Brendel. [ImageNet-trained CNNs are biased towards texture; increasing shape bias improves accuracy and robustness](https://openreview.net/forum?id=Bygh9j09KX), In 7th International Conference on Learning Representations, 2019.
[^shortcut]: Robert Geirhos, Jörn-Henrik Jacobsen, Claudio Michaelis, Richard Zemel, Wieland Brendel, Matthias Bethge, Felix A. Wichmann. [Shortcut Learning in Deep Neural Networks](https://arxiv.org/abs/2004.07780), 2020.

A recurring theme since the 1990s (at least) is the notion that a factored[^schmid92], disentangled, (statistically or even causally) independent representation would ease downstream learning tasks. Various disentanglement metrics have been proposed[^metrics]; various schemes have been devised to encourage a disentangled representation, mostly adaptations to variational autoencoders (VAEs)[^VAEs]. Unfortunately, as recent literature makes clear, the various metrics do not agree; the learning algorithms do not disentangle robustly.

While the current metrics consider statistical, causal, re-predictability or algebraic (as subgroups) approaches, none has considered the very general framework long known to the condensed matter physicist (aka, me). Hopefully something useful will come out of this. 

[^schmid92]:  Jurgen Schmidhuber. Learning factorial codes by predictability minimization,1992.
[^metrics]: First linear, then statistical, then algebraic (as subgroups), then causal, at least 6 of them
[^VAEs]: another 6 maybe?





## A Quantum Entanglement

Why are quantum computers so hard to make in practice? Decoherence! The quantum bits, or qubits, must maintain coherence among themselves and not interact with the environment. If they do, the qubits become entangled with the environment as well; but the environment has oodles of degrees of freedom and is essentially an infinite pit of random chaos! Their brief entanglement is quickly averaged over that chaotic environment, decohering the quantum state. 

Just like the quantum computer, in training representations we likewise do not want  entanglement between independent generating subspaces. 

[^group]:  give a convincing proposal 

This can be formulated mathematically using density matrices, but first, some notation. 

### A Quantum Introduction

The quantum state of an isolated system can be written as a (complex) superposition of basis states, $\left\vert\phi_i\right>$,
$$
\left\vert\Phi\right> = \sum_{i=0}^N \alpha_i \left\vert\phi_i\right>
$$

where the $\alpha_i$ are complex coefficients that satisfy 

$$
\sum_{i=0}^N \alpha_i \alpha_i^\star = 1
$$

This is analogous to the familiar $\sum_i p_i = 1$ for probabilities of various outcomes; indeed, $\alpha_i \alpha_i^\star$ is the probability of finding the system in state $i$. The strange angled brackets are *kets*, angled the opposite way they are *bras* as in two halves of a [*bra-ket*](https://en.wikipedia.org/wiki/Bra%E2%80%93ket_notation), also known as the Dirac notation: think of them as row, or complex transpose, (bra) and column (ket) vectors.

These states are enumerable or *quantized* and determined by the Hamiltonian of the system. Assuming this system is finite, there will be a finite number of basis states, $N$. The noisy environment has its own quantum states but since it's an infinite system there will normally be an infinity of them: for simplicity, let's pretend there are only $M$ degrees of freedom.

The combined basis is the tensor product of the two bases, $\left\vert\phi_{ij}\right> = \left\vert\phi_i\right> \otimes \left\vert\psi_i\right>$, where the tensor product symbol is already implied by the chained *kets*, and a general quantum state that has interacted with the environment can be expressed as

$$
\left\vert\Phi\right> = \sum_{i=0}^N \sum_{j=o}^M \alpha_{ij} \left\vert\phi_i\right> \left\vert\psi_j\right>
$$

where the number of indices allow for overloading our notation. It is both easier to write and easier to read (after some getting used to) so I will drop the summations &mdash; where indices repeat one upper, one lower, a sum is implied[^E-notatn]. The previous equation becomes simply $\left\vert\Phi\right> =  \alpha^{ij} \left\vert\phi_i\right> \left\vert\psi_j\right>$.

[^E-notatn]: Upper indices represent components of column (contravariant) vectors; lower indices represent of their complex transposed row (covariant) vectors. See more about the [Einstein notation](https://en.wikipedia.org/wiki/Einstein_notation) and [covariance and contravariance of vectors](https://en.wikipedia.org/wiki/Covariance_and_contravariance_of_vectors).

A disentangled, or factored, state has coefficients that factor, $\alpha^{ij} =  \alpha^i  \beta^j $. In comparison, the two-qubit Einstein-Podolsky-Rosen (EPR)[^EPR] or Bell states 
$\left\vert \Phi^\pm \right> = {1\over \sqrt{2}} (\left\vert \uparrow \right>_A \left\vert \uparrow \right>_B \pm \left\vert \downarrow \right>_A \left\vert \downarrow \right>_B )$ 
are *perfectly entangled* states and the subsystem $A$ is in a *completely mixed* state. Density matrices let us describe these mixed states mathematically.

[^EPR]: Originally posed as the [EPR paradox](https://en.wikipedia.org/wiki/EPR_paradox) intended to illustrate the incompleteness of quantum theory; experiments have since confirmed that the so-called paradox happens in reality.

### Density Matrix

The density matrix of a quantum state $\left\vert\Phi\right> = \alpha^i \left\vert\phi_i\right>$ is

$$
\rho = \left\vert\Phi \right>\left< \Phi \right\vert =  \left\vert \phi_i \right> \rho^i_j \left< \phi_j \right\vert
$$

This is an outer product of vectors; the matrix elements of $\rho$ in this case are $\rho^i_j = \alpha^i \alpha_j^\star$. In terms of our coupled spaces, we could imagine a flattened index, $(i, j) \to m$, but prefer to explicitly index the density matrix with all *four* components: $\rho^{ij}_{kl}$. 

The washing out of the environment variables is equivalent to tracing out those degrees of freedom; the reduced density matrix becomes

$$
\rho' = \rho^{ij}_{kj} = \alpha^{ij} \alpha_{kj} = \alpha \alpha^T
$$

where $\alpha$ is the matrix with entries $\alpha^{ij}$. For disentangled subsystems, 

$$
\rho' = \beta^j \beta_j^\star \alpha^i \alpha_k^\star = \alpha^i \alpha_k^\star
$$

using the normalization condition on the $\beta_j$. But this is just the density matrix of the quantum state $\left\vert\Phi\right> =  \alpha_i \left\vert\phi_i\right>$. Now consider the density matrix of the Bell state

$$
\rho_{ent} = {1 \over 2} \left( \left\vert \uparrow \right>_A \left\vert \uparrow \right>_B \pm \left\vert \downarrow \right>_A \left\vert \downarrow \right>_B \right)\left( \left< \uparrow \right\vert_A \left< \uparrow \right\vert_B \pm \left< \downarrow \right\vert_A \left< \downarrow \right\vert_B \right)
$$

In matrix form, this becomes

$$
\rho_{EPR} = {1\over 2} \left( \begin{array}{cccc} 
1&0&0&\pm1 \\0 & 0 & 0 & 0\\ 0 & 0 & 0 & 0 \\ \pm1 &0&0& 1
\end{array}\right)
$$

where the implied basis here is the $(\uparrow\uparrow, \uparrow\downarrow, \downarrow\uparrow, \downarrow\downarrow)$. When we trace out the $B$ qubit (this picks out entries for which the $B$ in and out states match), 

$$
\rho_A = {1 \over 2} \left( \begin{array}{cc}
1 & 0 \\ 0 & 1
\end{array} \right)
$$

There is no pure quantum state that gives this density matrix; in fact, it is an entirely mixed "classical" state where $A$ is found with 50/50 probability in either the $\uparrow$ or $\downarrow$ state. Rather than having to convince ourselves through brute force, a few properties of density matrices will help!

1. The density matrix is Hermitian, that is, $\rho = \rho^\dagger$. This follows directly from the definition.
2. The trace of a density matrix is 1. In all the preceding examples, this was true, but it's also easy to see in general using the normalization condition (repeatedly for each subspace).
3. As a direct consequence of these, the eigenvalues of the density matrix are [all real](https://en.wikipedia.org/wiki/Hermitian_matrix#Spectral_properties), non-negative (because they correspond to [probabilities](https://inst.eecs.berkeley.edu/~cs191/fa09/lectures/lecture13_fa09.pdf)) and [sum to 1](https://en.wikipedia.org/wiki/Trace_(linear_algebra)#Trace_equals_sum_of_eigenvalues). 

Let's explore the eigenvalues further. A Hermitian matrix can always be diagonalized via a unitary transformation; for our density matrix that means

$$
\rho = U\Lambda U^H
$$

where $UU^H = I$ and $\Lambda$ has the real eigenvalues of $\rho$ along its diagonal. $U$ defines a (possibly rotated) basis for the system any *one* of which defines a pure quantum state; for multiple non-zero eigenvalues, $\lambda_i$, the state is a mixture with probabilities  $\lambda_i$.

Adding this to the list of properties,

4. A pure state has a single non-zero eigenvalue equal to 1; alternatively, in a pure state, $\textrm{tr}(\rho^2) = 1$, whereas in a mixed state $\textrm{tr}(\rho^2) < 1$.

To get a measure of the mixing fraction, consider the von Neumann entropy

$$
S(\rho) = -\textrm{tr}(\rho \log_2 \rho) = -p^i \log_2 p_i
$$

For a pure state, a single $p_i=1$ giving $S = 0$. For a totally mixed state, $p_i = 1/N$ and $S = \log_2 N$, the highest possible entropy in an $N$ state system. For partially mixed states, $0 < S < \log_2 N$. A measure of *dis*entanglement (small for entangled; 1 for fully disentangled) is
$$
metric = 1 -S / log_2N
$$
Even though the computational cost of $\textrm{tr}(\rho^2)$ is similar to finding the eigenvalues of $\rho$, it will be interesting to test how useful the trace is as a metric. 

### Adapting to Representations

The qubit system resembles a binary encoding directly, but to develop a density matrix for a data set with representations $\in \Bbb{R}^d$ would need quantum field theory only to turn around and require Dirac deltas at sampled data points then "integrated" (summed) over. Another alternative is to pick a parametric distribution to fit with real data: but make Gaussian or similar assumptions is not realistic. We can also discretize the representation. A float is already a discrete encoding, but without going into floating point implementations, lets consider histograms. 

A binary encoding would be a Heaviside function of each dimension; choosing a threshold of 0 wlog and negative numbers are cast to 0, positive to 1. 

If we expect a ~normal distribution of values, we could split bins using quantiles of the normal distribution. 

A measure of how entangled a given dimension $m$ is with another dimension $n$ involves the reduced density matrix 
$$
\rho^{ij}_{kj} = \alpha^{ij} \alpha_{kj}
$$
where we drop complex conjugates since all values can be assumed real. The coefficients $\alpha_{ij} = \sqrt{p_{ij}}$ where the probabilities $p_{ij}$ are approximated the scaled 2-d histogram of data representations in the two dimensions $m$ and $n$. 

First, some sanity checks. A very basic implementation of the entropy involves histograms with equispaced bins: it captures correlations very well and orders pairs properly according to their subjective entanglement. But it requires a lot of data to ensure enough bins can cover the range of embedding values without too many gaps. A better option involves a kernel density estimation of the embedding distribution: Gaussian kernels decay too slowly; instead I use a [bump function](https://en.wikipedia.org/wiki/Bump_function), commonly used as a limiting [representation of the Dirac delta function](https://en.wikipedia.org/wiki/Dirac_delta_function#Representations_of_the_delta_function). 

```python
from scipy.spatial.distance import cdist

def get_softhist(embeddings, i=0, j=1, n=20):
    x, y = embeddings[:, [i,j]].transpose()
    x = (x - np.mean(x))/np.std(x)
    y = (y - np.mean(y))/np.std(y)
    
    u, v = np.meshgrid(np.linspace(np.min(x), np.max(x), n),
                       np.linspace(np.min(y), np.max(y), n))
    uv = np.column_stack([u.reshape(-1),v.reshape(-1)])
    
    d = cdist(np.column_stack([x,y]), uv)*(n**0.5)/2
    spread = (np.abs(d) < 1) * np.exp(-1/(1-(d*(np.abs(d) < 1))**2))
    
    h = np.sum(spread, axis=0).reshape((-1, n))
    return np.sqrt(h / np.sum(h))

def entropy(embeddings):
    a = get_softhist(embeddings)
    rho_i = np.matmul(a, a.transpose())
    p = np.linalg.eig(rho_i)[0]
    return -np.dot(p, np.log2(np.maximum(1e-6, p))) / np.log2(a.shape[0])
```

Baseline: show entropy on dim0 = dim1; dim0, dim1 totally random; a few familiar forms with 0 correlation (sin-cos, x-x^2).

There incompatible objectives in such a sampling strategy. Simultaneously:

* equal embedding dimensions should have very high entanglement; the reduced density matrix has non-zero entries only along its diagonal and requires very little, if any spread of the data points. Note that the entropy is not maximal unless the diagonal entries are furthermore all equal. But these entries correspond to the histogram of the isolated embedding dimension, so that maximum entropy entails a uniform distribution of embedding values.
* completely independently random embedding dimensions should have zero entanglement; the reduced density matrix has rank 1. But as the diagonals are the histogram of the isolated embedding dimension, to have rank 1 as many off diagonal entries are required (if a given diagonal is zero, that row/column is all zeros). In the limit of a uniform distribution of this embedding dimension, since the density matrix is always symmetric, all entries must be equal (to $1/n$). Intuitively, this means that all values occur in the traced out dimension for a given value in the isolated dimension: these *off-diagonal* correlations are easy to miss with finite sampling over too fine a grid.

## Datasets $\bigotimes$ Models

### The Swiss Roll

The [swiss roll](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.make_swiss_roll.html) is a classic that appears in any comparison of dimensionality reduction algorithms. Since the ideal embedding is two dimensional it will serve well to examine the embeddings directly and compare with the entanglement measure. UMAP (or tsne? whichever does better!) embedding will be considered alongside an regular autoencoder, a VAE and beta-VAE.

### dSprites

We next consider the [dSprites](https://github.com/deepmind/dsprites-dataset/) dataset of 32x32 images of with a white square, ellipse or heart with a random choice of scale, orientation, and x and y position. 

### And all the others...

Thanks to the [disentanglement lib](https://github.com/google-research/disentanglement_lib), full of datasets and pretrained models, I can apply my entanglement measure of them all. 

