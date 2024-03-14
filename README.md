# Probabilistic Spiking Neurons (Research CS760)
S-NN's is a well defined research area that attempts to incorporate more "biological" like features into the model neuron. Rather than reading tricky whitepapers on this - the following should summarise this area neatly;

---

Instead of each neuron holding a continuous activation function, feeding these floating output values forward - we restrict each neuron to the binary output space 0 & 1. Neurons only firing when it's inputs have hit, for example, some threshold.

This can lead to destructive pathways though, an early 0 firing neuron will negatively impact further neurons to fire, for that reason we introduce a time dimension...

## Time dimension
Think of `steps`, where a network at each `step` can be evaluated. The same neurons firing at `step` may not be firing at `step` + 1... but this accommodates another idea, where neurons themselves can have state! Rather than being functional, it can "remember" it's previous input state, and add to it current input state - simulating a build up of "voltage" for example (pulling analogy of the biological neuron) and as this eventually goes above a threshold, boom, it fires!

### Observation Window
Because we are now looking at this time temporal point of view - we need to redefine what it means for a NN to express itself given an input. So we say that our NN can evaluate an input **given a time period**, say 300 steps. This is a hyper-parameter, we'll keep it constant for training and testing times.

#### Input Embedding
So with an image, say MNIST dataset, series of 28x28 grayscale images. You can traditionally imagine them as a 28x28 matrix, each cell being a value of pixel intensity. One one end you have the colour white, other side you have black.

That won't work in S-NN's, as you you again have destructive behaviours going down the NN, you need to encode this somehow in spikes.

##### Rate Encoding
So the same flattening can happen, but instead, we encode intensity of a pixel by the rate of the input neuron firing. Say we define a very intense pixel to be firing each `step`, where a devoid pixel can be represented as not firing at all during the entire observation window.

## Output Interpretation
For classification like above, say you have `N` classes... hence `N` output neurons. You could look for;

- The first of these that fires?
- During the observation period, which of these neurons fires the most.
- ... others ofcourse.
