---
layout: page
title: Projects
permalink: /projects/
---

## **Research Projects**

Here's a selection of my research projects.

---

### **Project 1: Neural geometry of value representations in RNNs**

**Duration:** 2026 – Present  
**Status:** Ongoing

In this project, I train RNN models to perform simple cognitive tasks through reinforcement learning and then analyse the model representations to understand the computational mechanisms which arise. With these simple toy models, we can answer fundamental questions. I am interested in context-dependent value representations, where the same items can take different values across different contexts. In particular I am interested in two alternative computational mechanisms: conjunctive representations, in which a distinct subspace represents value across different contexts, and factorised representations, in which the same value subspace is reused across contexts. Each of these have advantages and disadvantages, and I am working to map out the space of tasks in which the optimal representation is one or the other. I have developed a value decoding generalisation test which can be used to measure which of these representations is present in the model. I then verify this using causal manipulations such as ablations and activation steering. My goal is to use my models to make experimentally testable predictions about value coding in the brain in a range of task conditions.

**Technologies/Methods:** Low-rank RNNs; reinforcement learning; linear decoding; dynamical systems analysis; activation steering; ablations.

---

### **Project 2: Neural representations underlying value-guided decision-making in the PFC**

**Duration:** 2025 – Present  
**Status:** Ongoing

In this project, I analyse calcium imaing recordings from dmPFC of mice performing a visual Pavlovian reversal learning task to identify the subspaces encoding variables such as stimulus indetity, value and context. Alongside this, I train neural network models to perform an analogous task and find the conditions which reproduce the experimental data. I am specifically interested in the extent to which representational similarity determines similarity of lick responses for different stimuli.

**Technologies/Methods:** Targeted dimensionality reduction; neural decoding; neural encoding; selectivity analysis; optophysiological data analysis.

---

### **Project 3: Designer waveform**

**Duration:** 2026 - Present
**Status:** Ongoing

Typical optogenetic stimulation protocols do not produce the same population-level activity as natural sensory input, partally due to strong synchronous stimulation. In this project, I am developing tools to find stimulation waveforms that evoke more naturalistic activity. Given a target population response (e.g. a PSTH recorded during natural stimulation), it searches the space of parametric waveforms to find the stimulus shape that drives a neural population model towards that target.

**Technologies/Methods:** Spiking neural networks; gradient-free optimisation; electrophysiological data analysis.
