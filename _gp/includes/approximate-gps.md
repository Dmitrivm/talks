### Approximate Gaussian Processes


\include{../../_gp/includes/low_rank_motivation.md}
\include{../../_gp/includes/gp_variational_complexity.md}
\include{../../_gp/includes/bottleneck.md}

### Information capture {data-transition="None"}

-   Everything we want to do with a GP involves marginalising
$\mappingFunctionVector$

    -   Predictions

    -   Marginal likelihood

    -   Estimating covariance parameters

-   The posterior of $\mappingFunctionVector$ is the central object. This
means inverting $\Kff$.

\include{../../_gp/includes/nystrom.md}
\include{../../_gp/includes/inducing_notation.md}
\include{../../_gp/includes/inducing_introduction.md}

### The alternative posterior

[Instead of doing]{}
$$p(\mappingFunctionVector\given\dataVector,\inputMatrix) = \frac{p(\dataVector\given\mappingFunctionVector)p(\mappingFunctionVector\given\inputMatrix)}{\int p(\dataVector\given\mappingFunctionVector)p(\mappingFunctionVector\given\inputMatrix){\text{d}\mappingFunctionVector}}$$
[We’ll do]{}
$$p(\inducingVector\given\dataVector,\inducingInputMatrix) = \frac{p(\dataVector\given\inducingVector)p(\inducingVector\given\inducingInputMatrix)}{\int p(\dataVector\given\inducingVector)p(\inducingVector\given\inducingInputMatrix){\text{d}\inducingVector}}$$
\pause
\centering\alert{but $p(\dataVector\given\inducingVector)$ involves inverting $\Kff$}

<!--Flexible Parametric Approximation-->

\include{../../_gp/includes/larger_graph_intro.md}
\include{../../_gp/includes/larger_variational.md}
\include{../../_gp/includes/larger_factorize.md}

### Inducing Variables

* Choose to go a different way.

* Introduce a set of auxiliary variables, $\inducingVector$, which are $m$ in length.

* They are like "artificial data".

* Used to *induce* a distribution: $q(\inducingVector|\dataVector)$

### Making Parameters non-Parametric

* Introduce variable set which is *finite* dimensional.
$$
p(\dataVector^*|\dataVector) \approx \int p(\dataVector^*|\inducingVector) q(\inducingVector|\dataVector) \text{d}\inducingVector
$$

* But dimensionality of $\inducingVector$ can be changed to improve approximation.

### Variational Compression {.slide: data-transition="none"}

* Model for our data, $\dataVector$

$$p(\dataVector)$$
<br><object type="image/svg+xml" data="./diagrams/py.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

* Prior density over $\mappingFunctionVector$. Likelihood relates data, $\dataVector$, to $\mappingFunctionVector$.

$$p(\dataVector)=\int p(\dataVector|\mappingFunctionVector)p(\mappingFunctionVector)\text{d}\mappingFunctionVector$$<br>
<object type="image/svg+xml" data="./diagrams/pygfpf.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

* Prior density over $\mappingFunctionVector$. Likelihood relates data, $\dataVector$, to $\mappingFunctionVector$.

$$p(\dataVector)=\int p(\dataVector|\mappingFunctionVector)p(\inducingVector|\mappingFunctionVector)p(\mappingFunctionVector)\text{d}\mappingFunctionVector\text{d}\inducingVector$$<br>
<object type="image/svg+xml" data="./diagrams/pygfpugfpf.svg">
</object></td></tr>
</table>

### Variational Compression {.slide: data-transition="none"}

$$p(\dataVector)=\int \int p(\dataVector|\mappingFunctionVector)p(\mappingFunctionVector|\inducingVector)\text{d}\mappingFunctionVectorp(\inducingVector)\text{d}\inducingVector$$
<br><object type="image/svg+xml" data="./diagrams/pygfpfgupu.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

$$p(\dataVector)=\int \int p(\dataVector|\mappingFunctionVector)p(\mappingFunctionVector|\inducingVector)\text{d}\mappingFunctionVectorp(\inducingVector)\text{d}\inducingVector$$<br>
<object type="image/svg+xml" data="./diagrams/pygfpfgupu2.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

$$p(\dataVector|\inducingVector)=\int p(\dataVector|\mappingFunctionVector)p(\mappingFunctionVector|\inducingVector)\text{d}\mappingFunctionVector$$<br>
<object type="image/svg+xml" data="./diagrams/pygfpfgu.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

$$p(\dataVector|\inducingVector)$$<br>
<object type="image/svg+xml" data="./diagrams/pygu.svg">
</object>

### Variational Compression {.slide: data-transition="none"}

$$p(\dataVector|\paramVector)$$<br>
<object type="image/svg+xml" data="./diagrams/pygtheta.svg">
</object>

### Compression

* Replace true $p(\inducingVector|\dataVector)$ with approximation $q(\inducingVector|\dataVector)$.

* Minimize KL divergence between approximation and truth.

* This is similar to the Bayesian posterior distribution.

* But it's placed over a set of 'pseudo-observations'.


###

\LARGE$$\mappingFunctionVector, \inducingVector \sim \gaussianSamp{\mathbf{0}}{\begin{bmatrix}\Kff & \Kfu\\\Kuf & \Kuu\end{bmatrix}}$$
$$\dataVector|\mappingFunctionVector = \prod_{i} \gaussianSamp{\mappingFunction}{\dataStd^2}$$

<!--Variational Compression-->

\include{../../_gp/includes/variational_compression.md}
\include{../../_gp/includes/low_rank_variational.md}
\include{../../_gplvm/includes/bayes_gplvm_intro.md}
\include{../../_gplvm/includes/variational_bayes_gplvm_long.md}
\include{../../_gplvm/includes/nested_variational_compression.md}
\include{../../_gp/includes/larger_gaussian.md}

### Efficient Computation

* Thang and Turner paper

### Other Limitations 

* Joint Gaussianity is analytic, but not flexible.


