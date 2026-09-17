---
layout: page
title: Projects
permalink: /projects/
---

Here's a brief overview of some of my ongoing research projects.

---

### **Project 1: Neural representations in dmFC and RNNs**

**Duration:** 2026 – Present  
**Status:** Ongoing

In this project, I aim to uncover the neural representations that enable value-based decision-making in the dorsomedial prefrontal cortex (dmPFC), using a combination of neural data analysis and neural network-based modelling. I analyse calcium imaging recordings from the dmPFC of mice performing a visual Pavlovian reversal learning task, in which reward contingencies periodically switch, to identify how the brain encodes variables such as stimulus identity, value, and task context (i.e., which reversal phase the animal is in).

I take several complementary approaches: targeted dimensionality reduction to find task-relevant neural subspaces, selectivity-based analysis to define functional subpopulations of neurons, and decoding to ask which variables are represented and whether these representations are conserved across reversals in reward contingency.

I then train recurrent neural networks (RNNs) to perform an analogous task and analyse their resulting representations. I am particularly interested in how different learning rules shape these representations, and whether aligning model representations to experimental data can reveal something about how learning occurs in dmPFC. To investigate this, I train RNN variants whose hidden representations are shaped by reinforcement learning, self-supervised learning, or a combination of both, and compare the resulting representations to the experimental data using statistical goodness-of-fit tests and representational similarity analysis (RSA).


![data_rnn_project_summary_figure](/assets/images/projects/data_rnn_project_summary_figure.png)

Three RNN variants, example TDR projections and RSA matrices to be compared with experimental equivalents (unpublished so cannot show experimental data here).

This project is ongoing. I am currently focused on a retrospective form of self-supervised learning within this simplified task. In the next stages, I plan to extend this to predictive self-supervised learning across a wider range of tasks, including those that require learning a state-transition model to successfully obtain reward.

**Technologies/Methods:** RNNs; reinforcement learning; linear decoding; dynamical systems analysis; activation steering; ablations; reinforcement learning; linear decoding; dynamical systems analysis; activation steering; ablations.

---

### **Project 2: Designer waveform**

**Duration:** 2026 - Present
**Status:** Ongoing

Typical optogenetic stimulation protocols do not produce the same population-level activity as natural sensory input, partly because they rely on strong, synchronous stimulation of all neurons at once. In this project, I am developing tools to find stimulation waveforms that evoke more naturalistic neural activity.

Given a target population response (e.g., a peristimulus time histogram, or PSTH, recorded during natural stimulation), the tool searches the space of parametric waveforms to find the stimulus shape that drives a neural population model toward that target. On each optimisation step, the candidate waveform is fed as input to a spiking neural network model of a representative population of V1 neurons (with multiple possible opsins, the light-sensitive proteins used to control neural activity). The resulting simulated population activity is compared to the target, and the error is computed as a scalar objective function. The waveform parameters are then updated to reduce this error, and the process is repeated until a convergence criterion is reached.

These optimised waveforms are being tested in a stimulus detection task involving both natural and artificial (optogenetically driven) stimuli. We are using this task to ask a simple question: without the privilege of full control over individual neurons in the population (as we would get from holographic stimulation), but only a single shared waveform delivered to the entire population, can shaping that waveform still evoke behavioural report rates closer to those seen with natural images, compared to standard square-pulse stimulation?


![increasing_l23_l23_optimised_waveform](/assets/images/projects/increasing_l23_l23_optimised_waveform.png)

*An example of a waveform optimised to fit Allen Visual Coding natural image responses for the ChRmine opsin.*

![waveforms_and_responses](/assets/images/projects/waveforms_and_responses.png)
*Left: model-optimised waveform and control square stimulation waveforms. Right: Model responses to these three waveforms.*

The code for this project can be found at [designer-waveform](https://github.com/pmccthy/designer-waveform).

This project is a work in progress. We are currently testing the first model-optimised waveforms _in vivo_. In the next stages, we will explore strategies for optimising parameters for holographic two-photon stimulation, in which we have control over individual neurons and will optimise for a target activity vector rather than stimulating the whole population simultaneously.

**Technologies/Methods:** Spiking neural networks; gradient-free optimisation; electrophysiological data analysis.
