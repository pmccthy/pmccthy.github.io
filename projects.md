---
layout: page
title: Projects
permalink: /projects/
---

Here's a brief overview of some of my research projects.

---

## **Project 1: Reverse engineering neural representations in dmFC with RNNs**

**Duration:** 2026 – Present  
**Status:** Ongoing

In this project, I aim to uncover the neural representations that enable value-based decision-making in the dorsomedial prefrontal cortex (dmFC), using a combination of neural data analysis and neural network-based modelling. I analyse calcium imaging recordings from the dmFC of mice performing a visual Pavlovian reversal learning task, in which reward contingencies periodically switch, to identify how the brain encodes variables such as stimulus identity, value, and task context (i.e., which reversal phase the animal is in).

I take several complementary approaches: targeted dimensionality reduction to find task-relevant neural subspaces, selectivity-based analysis to define functional subpopulations of neurons, and decoding to ask which variables are represented and whether these representations are conserved across reversals in reward contingency.

I then train recurrent neural networks (RNNs) to perform an analogous task and analyse their resulting representations. I am particularly interested in how different learning rules shape these representations, and whether aligning model representations to experimental data can reveal something about how learning occurs in dmFC. To investigate this, I train RNN variants whose hidden representations are shaped by reinforcement learning, self-supervised learning, or a combination of both, and compare the resulting representations to the experimental data using statistical goodness-of-fit tests and representational similarity analysis (RSA).


![data_rnn_project_summary_figure](/assets/images/projects/data_rnn_project_summary_figure.png)

*Three RNN variants, example TDR projections and RSA matrices to be compared with experimental equivalents (unpublished so cannot show experimental data here).*

This project is ongoing. I am currently focused on a retrospective form of self-supervised learning within this simplified task. In the next stages, I plan to extend this to predictive self-supervised learning across a wider range of tasks, including those that require learning a state-transition model to successfully obtain reward.

**Technologies/Methods:** RNNs; reinforcement learning; self-supervised learning; linear decoding; dynamical systems analysis; steering; ablations.

---

## **Project 2: Designer waveforms for optogenetic stimulation**

**Duration:** 2026 - Present  
**Status:** Ongoing

Typical optogenetic stimulation protocols do not produce the same population-level activity as natural sensory input, partly because they rely on strong, synchronous stimulation of all neurons at once. In this project, I am developing tools to find stimulation waveforms that evoke more naturalistic neural activity.

Given a target average population response, the tool searches the space of parametric waveforms to find the stimulus shape that drives a neural population model toward that target. On each optimisation step, the candidate waveform is fed as input to a spiking neural network model of a representative population of V1 neurons expressing an opsin. The model is currently compatible with the ChRmine and C1V1 opsins. The resulting simulated population activity is compared to the target, and the error is computed as a scalar objective function. The waveform parameters are then updated to reduce this error, and the process is repeated until a convergence criterion is reached.

We have used this to optimise a simple 5-parameter waveform to match natural stimulus responses taken from the Allen Institute's Visual Coding Neuropixels dataset. These optimised waveforms are being tested in a stimulus detection task involving both natural and artificial (optogenetically driven) stimuli. We are using this task to ask a simple question: without the privilege of full control over individual neurons in the population (as we would get from holographic stimulation), but only a single shared waveform delivered to the entire population, can shaping that waveform still evoke behavioural report rates closer to those seen with natural images, compared to standard square-pulse stimulation?


![designer_waveform_schematic](/assets/images/projects/designer_waveform_schematic.png)

*Schematic of the optimisation loop. A candidate waveform drives a spiking network model of opsin-expressing V1 neurons; the population-averaged response is compared to the target, and the waveform parameters are updated until the mismatch falls below a threshold, yielding the optimised waveform.*

![waveforms_and_responses](/assets/images/projects/waveforms_and_responses.png)

*Left: model-optimised waveform and control square stimulation waveforms. Right: Model responses to these three waveforms.*

The code for this project can be found at [designer-waveform](https://github.com/pmccthy/designer-waveform).

This project is a work in progress. We are currently testing the first model-optimised waveforms in vivo. In the next stages, we will explore strategies for optimising parameters for holographic two-photon stimulation, in which we have control over individual neurons and will optimise for a target activity vector rather than stimulating the whole population simultaneously.

**Technologies/Methods:** Spiking neural networks; gradient-free optimisation; electrophysiological data analysis.

---

## **Project 3: Hierarchical feature binding in a spiking model of the ventral pathway**

**Duration:** 2021 – 2026
**Status:** Published in *PLOS Computational Biology* (2026)

How does the brain know which visual features belong to which objects, and how those features fit together? This is the *feature binding problem*, and it is still unsolved in neuroscience. Most existing theories are either not biologically realistic or do not capture the *hierarchical* relationships between features, for example that a vertical bar is part of the letter "T". In this project, we tested a hypothesis called *binding by polychrony*. The idea is that these part–whole relationships are encoded in precisely timed, repeating patterns of spikes across groups of neurons, known as polychronous neuronal groups.

To test this, we built a spiking neural network of conductance-based leaky integrate-and-fire neurons, in Brian2, that mirrors the primate ventral visual pathway. Gabor-filtered images, mimicking V1 simple cells, drive a Poisson input layer. This feeds four layers modelled on V2, V4, TEO and TE, which are connected by bottom-up, top-down and lateral synapses with axonal conduction delays. The network learns without supervision through spike-timing-dependent plasticity (STDP) and competition between neurons.

![feature_binding_model_schematic](/assets/images/projects/feature_binding_model_schematic.png){: width="60%" style="display:block; margin:0 auto;"}

*Schematic of the spiking model of the primate ventral visual pathway. Gabor-filtered input images drive a Poisson input layer, which feeds four layers of excitatory and inhibitory neurons modelled on V2, V4, TEO and TE, with bottom-up, top-down and lateral connections.*

After training on datasets of related 2D shapes, neurons became selective for boundary-contour features of the shapes, and higher layers represented larger-scale combinations of those features. Repeating, precisely timed spike patterns also emerged in the higher layers. Some of these formed hierarchical feature binding circuits: three-neuron motifs in which a "binding neuron" fires only when spikes from a lower-level feature neuron and a higher-level feature neuron arrive at the same time.

![feature_binding_circuit](/assets/images/projects/feature_binding_circuit.png){: width="40%" style="display:block; margin:0 auto;"}

*Schematic of a three-neuron hierarchical feature binding circuit. The binding neuron (3) fires only if spikes from the lower-level feature neuron (1) and the higher-level feature neuron (2) arrive at the same time, signalling that feature 1 is part of feature 2.*

These binding circuits stayed robust even when the timing of input spikes was randomised. This suggests that binding by polychrony is a plausible mechanism for representing hierarchical visual structure in the brain. It also points to what experimentalists could look for in real recordings, and it could help make computer vision systems more robust.

I developed the original model and found the first hierarchical feature binding circuits emerging in it. Brian Gardner and other co-authors then took the project further. They scaled up the analysis, used SPADE to detect polychronous groups systematically, and showed that the circuits are robust to randomised input timing.

The paper, *Hierarchical feature binding in a spiking neural network model of the primate ventral visual pathway* (Gardner, **McCarthy**, Chrol-Cannon, Goodman, Schultz, Lo Iacono & Stringer, 2026), is available [here](https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1014752). The original model I developed can be found at [spiking-PVVS-model](https://github.com/pmccthy/spiking-PVVS-model), and the code for the extended study and published analyses is at [feature_binding](https://github.com/BCGardner/feature_binding).

**Technologies/Methods:** Spiking neural networks (Brian2); spike-timing-dependent plasticity; unsupervised learning.