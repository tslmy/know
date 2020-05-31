---
description: >-
  Based on Explainable Deep Learning: A Field Guide for the Uninitiated
  (https://arxiv.org/abs/2004.14545)
---

# Explainable Deep Learning



![](../.gitbook/assets/image%20%2816%29.png)

## Explainable DNN

### Traits of an explanation

#### Confidence: DNN should think like a user

#### Trust: no need to validate how DNN think

* How to build up trust for a DNN
  * Satisfactory testing: test score sufficiently approaches training score
  * Experience: If too trivial, can trust without proving
* How to evaluate trustworthiness
  * Don’t rely on test
  * Best: “system evaluations”
    * during forward pass: Look at how neurons get activated
    * During backprop: Look at how weights get updated

#### Safety: because DNN affects humans, it should be safe.

* Consistently operate as expected
  * See "trust"
* Don’t make choices that could harm human
* Robust to changes in environment
* Feedback how environment affects decisions -- enables assessment

#### Ethics: Don’t violate human moral principles

* e.g., “Is it morally OK to use facial recognition to deter jaywalking?”
* Field of its own; no definitive answer yet; differ by culture

### Topics associated with explainability

#### Learning mechanism: How do params evolve during training?

* Methods related to _semantics_ -- associates params to concepts
  * Zhou et al. \(2014\)
    * How: plot out saliency maps; try to recognize what real-world obj they look like.
      * This association is _weak_
    * Side-discovery: Classifiers for _scenes_ has internal filters that work like _Object_ Detectors
  * Kim et al. \(2018a\) -- TCAV
    * Multiple linear classifiers
    * measures the proportion of examples that belong to a given class that are positively influenced by a given concept.
* Methods that finds patterns when a DNN _converges_ \(i.e., weight stabilizes\)
  * e.g. of such patterns
    * How each individual layer evolves \(i.e., have their weights updated\)
    * When different layers converge \(i.e., becomes similar\)
    * What/How/When they learn about concepts -- Generalization + memorization
  * methods
    * SVCCA
      * Finding: First layers converge earlier. Implications:
        * Can freeze first layers after short while of training to save computation
        * First layers capture primitive features/concepts
    * Systematic experimentation
      * Finding: more randomized training data, less adaptive to test data.
      * Hypothesis:
        * Explicit regularization may improve generalization
        * Stochastic gradient descent could act as regularizer
          * only hypothesized for linear models
    * Arpit et al. \(2017\)
      * finding: DNN memorizes common patterns instead of real data
        * Comment: this might be trivial nowadays, but compare with “prototype learning".
    * Bahri et al. \(2020\) -- statistical mechanics
      * A theoretical proof of DNN

#### Model debugging: uses a “probe”

* Model assertions / boolean functions
  * operate on a recent history of the model input and output
  * applications
    * Correct wrong outputs
    * Provide more samples -- active learning
* ModelTracker, a GUI for debugging
  * Primarily to solve problems in the training data
* Use linear functions to make sense of intermediate layers
  * Finding: Representations learnt by _later_ layers have more predictive power
    * Implication: More refined/intricate/high-level/complex features, more predictive power.
* Neural stethoscopes
  * How: Trains a simpler model along with training the main DNN
  * Compare with linear classifier: uses different training data
    * input: representation from a layer of interest
    * Output Labels to learn: some complementary info about the dataset
  * 3 modes
    * analytic
    * auxiliary
    * Adversarial

#### Adversarial attack & defense

* Adversarial attack
  * Breaks encapsulation? \(Has access to model params / intermediate gradients?\)
    * Black-box attack
    * White-box attack
  * Attacks by perturbing input data
    * Adding noise imperceptible to human
      * C&W attack
      * Projected Gradient Descent \(PGD\) attack
      * Fast Gradient Sign Method \(FGSM\)
    * Adding physical perturbations
      * “Wear a t-shirt printed with 500 human faces and you’re invisible to DNNs.”
* Adversarial defense
  * Adversarial training
    * e.g. Integrates the PGD attack into the training
      * Minimize classification loss
      * Maximize adversarial attack loss
  * Removal perturbations
    * e.g. Use GAN to “sanitize” input images

#### Fairness & Bias

* aspects
  * Group fairness
  * Individual fairness
  * Equalized odds and equal opportunity
  * Disparate mistreatment
* How to be fair
  * Pre-processing methods: revise input data
  * In-processing methods: add constraints to training process
  * Post-processing methods: adjust model predictions

### Future Directions

#### To enhance

* Enhance User-friendliness
  * model explanations would inevitably be mandatory
* Enhance efficiency
  * “DNN should be quick to infer, and explanations should also be quick to generate.”

#### To make

* Develop a systematic general theory
* Develop methods for Debugging DNNs
* Develop methods for trustworthiness
* Develop evaluation principles/procedures for explanation methods
  * human-friendly
  * complex
  * accurate
  * Complete: covers enough info from the DNN s.t. it’s reproducible
  * generalizable \(similar to human-friendly\): an explanation should be high-level enough to map to real-world concepts
  * persuasive
    * how well human comprehend the explanations

### Designing Explanations for Users

#### Who is the end user?

* Types of users
  * Expert users
    * want
      * Low-level, technical
      * debuggable
    * Can present explanations in the forms of
      * Input _features influence_ analytics
      * Hidden states interaction + viz
    * Demand for trust is not as strong, because experts can often debug the DNN themselves
  * Normal users
    * want
      * High-level
      * Can be operated upon / can inform decisions
    * Can present explanations in the forms of
      * Extracted reasoning logic
      * Input clues
    * Demand more trust to the model, otherwise outputs can be denied
* Can also vary by domain

#### How practically impactful are the decisions of the DNN?

* types
  * Time-critical scenarios
    * Don’t require extra human effort for verification -&gt; demands high reliability
    * Don’t be computationally intense
  * Decision-critical scenario
    * Demands ability to deeply inspect a decision 

#### How extendable is an explanation?

* aspects
  * modularity
    * See DNN as: Composition of interconnected functional units
    * Emphasizes on: ease of adaptation w/ modification
  * reusability
    * See DNN as: Complete DNN systems
    * Emphasizes on: ease of adaptation w/o modi.
* Explanation methods can be categorized according to extendability
  * Model-agnostic methods
  * Methods that are very specific to the model

### Methods for Explaining DNNs

#### Visualization methods: plot out characteristics of input that strongly influence the output

* Back-propagation/gradient based
  * Two major categories
    * \(Simonyan et al., 2013; Springenberg et al., 2014\)
      * visualizes the partial derivative of the network output w.r.t. each input feature
      * Input features are scaled by their values
    * Zeiler & Fergus, 2014; Bach et al., 2015; Montavon et al., 2017; Shrikumar et al., 2017\)
      * visualizes the partial derivative of the intermediate representations at a specific layer w.r.t. an output
  * Activation maximization
    * Optimize the input X s.t. the activation of a chosen unit I in a layer j is maximized
    * i.e., instead of updating weights according to gradient, update the _input_.
    * Stop training after a certain number of steps, not by checking a “target function”. \(At least in this paper\)
  * deconvolution
    * For CNNs only
    * DeCNN makes these replacements
      * Conv layers -&gt; decent layers
      * Max-pooling layers -&gt; unspooling layers
        * unpooling: all pixels in a patch is set to the given value \(which is supposed to be the max value from the patch during a max-pooling\)
  * CAM and Grad-CAM
    * CAM: + global average pooling to last conv layer
      * Creates a “relevance score map" for each output class
      * structure: GAP\(Conv\) → FC → softmax
      * Only for CNNs that were Conv → FC → softmax
    * Grad-CAM: uses the _gradients_
      * Only requiring the final activation function to be differentiable
      * Does not use weight $w\_{k,c}$ at all in its formula
  * Layer-Wise Relevance Propagation \(LRP\)
    * relevance of each input feature to the output of the network
    * Most generic type of LRP: Deep Taylor Decomposition
      * Exploits the fact that f is differentiable and hence can be approximated by a Taylor expansion
      * the relevance score of the later layers can be backprop’d to generate that of former layers
  * Deep Learning Important FeaTures \(DeepLIFT\)
  * Integrated Gradients
* Perturbation based
  * Occlusion sensitivity
    * sweeps a grey patch across input image; see how output changes
  * Representation erasure
    * Like “Occlusion sensitivity”, but for text classification.
    * Removes words; find minimum textual changes that flips the output
  * Meaningful perturbation
    * types of perturbation
      * constant
      * noise
      * blur
    * Generates explanation specific to a given input image \(i.e., local to $x\_0$\)
  * Prediction difference analysis
    * original
      * delete info from an input; measure the influence -- more mathly proven
      * measures the importance of feature $x\_i$
    * Improved version
      * Sample patches instead of pixels
      * Removes patches instead of pixels
      * Also use this method for intermediate layers \(instead of input\)

#### Model Distillation: Make another \(inherently explainable\) model that mimic the I/O behavior of the main DNN

* Local approximation
  * types
    * LIME
    * Anchor-LIME
      * Use if-then rules \(think: decision trees\) instead of linear combinations
    * STREAK
      * Add time limit to func calls
      * Greedily solve a combinatorial maximization problem
  * similarities
    * Splits each input instance into semantically meaningful parts
    * Have to call the original DNN
    * local
* Model translation
  * Tree based
  * FSA based
    * For RNNs
    * Clustering methods explored
      * K-means++
      * K-means-x
    * Why FSA are more interpretable
      * FSA can be simulated by humans \(“by pen and paper”\)
      * the transitions between states in FSA have _real physical meanings_
  * Graph based
  * Rule based

#### Intrinsic methods

* Attention mechanisms
  * Single-modal weighting
  * Multi-modal interaction
* Joint training
  * Text explanation
  * Explanation association
  * Model prototype

