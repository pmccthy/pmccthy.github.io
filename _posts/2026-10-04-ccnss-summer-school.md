---
layout: post
title: "Metalearning, Manifolds and Mandarin"
date: 2026-09-04
---

Earlier this summer I was lucky enough to attend the [Computational & Cognitive Neuroscience Summer School (CCNSS)](https://www.csh-asia.org/?content/3046) in Suzhou, China! This three-week intensive course was hosted by Cold Spring Harbor Asia and covered a broad set of topics on the computational neuroscience of cognition at all scales, from synaptic plasticity rules all the way to whole-brain modelling.

<img class="fig-center" style="width: 100%;" src="/assets/images/posts/china/csha_group_picture_web.jpg" alt="Group photo of the CCNSS 2026 participants at Cold Spring Harbor Asia">

*The CCNSS 2026 cohort at Cold Spring Harbor Asia.*

### **Highlights**

Over the 3 weeks we had around 30 lectures, which is a lot of information to absorb! Given this, I thought I'd take some time to take stock of what I learnt. It's obviously not possible to cover it all here, but I thought I'd summarised a couple of things that left the biggest impression on me.

**Nao Uchida - Metalearning**

Nao Uchida gave two great lectures covering reinforcement learning (RL) theory and the history of testing RL implementation in the brain. But the highlight of his lectures for me was when he talked about some work his lab has done on testing meta-reinforcement learning (metaRL) in the brain.

MetaRL is one of my favourite topics and possibly the coolest idea I've come across in computational neuroscience. The idea behind metaRL is that, by training an RNN through RL, it can learn to implement a second RL algorithm in its dynamics (updating value without any need for plasticity). For a given task with some latent structure, such an RNN can infer the latent variable and store it in its recurrent dynamics. A prerequisite for metalearning RNNs to work is that, as well as receiving the current state observation as input, they also receive the previous reward and action. By integrating these over time, they can infer hidden variables. For example, in a reversal learning task with uncued reversals, the hidden variable is the reward "context". A metalearning RNN learns to represent this context variable and can therefore switch its behaviour when it has accumulated enough evidence that the context has changed. As mentioned above, because it relies on recurrent dynamics, it does this without plasticity. So you can switch off plasticity in the network and the model can still switch its behaviour! In metaRL, rather than learning a set of stimulus-value associations, the slow plasticity-based learning sets the network up to perform a second kind of fast, dynamics-based learning. In other words, the network has learned to learn (hence "meta" learning).

MetaRL was first introduced in two papers which came out around the same time in 2016, one from OpenAI ([Duan *et al.* 2016](https://arxiv.org/abs/1611.02779)) and one from DeepMind ([Wang *et al.* 2016](https://arxiv.org/abs/1611.05763)).[^1] It was quickly applied to neuroscience in a follow-up paper from the same team at DeepMind ([Wang *et al.* 2018](https://www.nature.com/articles/s41593-018-0147-8)), which proposed it as a core function of the PFC and showed that it could replicate a number of findings from neuroscience experiments. However, since then, there hasn't been much work directly testing it in real neural circuits.[^2] In his lecture, Nao Uchida presented work from his lab ([Lee *et al.* 2025](https://www.biorxiv.org/content/10.64898/2025.11.30.691382v3)) in which they actually test metaRL models in the mouse basolateral amygdala (BLA).[^3]

They trained mice on an odour-reward task where the contingencies either stayed fixed or reversed every session (the "stable" and "dynamic" tasks, respectively). Mice in the dynamic task got faster at updating value, but they also became much more forgetful. Their value memory dropped to chance after a one-day break, or even a five-minute pause, whereas stable-task mice remembered for over a week. That's exactly what you'd expect if value is being held in activity rather than stored in synapses.

<img class="fig-center" style="width: 216px;" src="/assets/images/posts/china/uchida_iti_effect.png" alt="Effect of ITI length on value discrimination in the stable versus dynamic tasks">

*Illustration of the effect of ITI length on value discrimination in the stable versus dynamic tasks. Adapted from [Lee et al. 2025](https://www.biorxiv.org/content/10.64898/2025.11.30.691382v3)*

They then actually blocked plasticity in the BLA with a CaMKII inhibitor. Mice in the stable version were impaired, but mice trained on reversals were unaffected: they could still reverse their behaviour without BLA plasticity. Recordings showed BLA neurons tracking the current reward context between trials, just like the hidden units of a metaRL network.

I thought this work was really cool, and a beautiful example of testing computational ideas in real neural circuits. It left me wondering how widespread this is: if the BLA can switch from plasticity to dynamics, how many other circuits we think of as "learning through synapses" are actually doing something more like inference?

**Byron Yu - BCIs for basic neuroscience**

This was one of the most inspiring lectures for me, as BCIs are a major interest of mine. If you follow the field, you'll know it's a very exciting time. In the last few years, BCIs have been used to decode inner speech ([Kunz *et al.* 2025](https://doi.org/10.1016/j.cell.2025.06.015)), let people with paralysis walk again ([Lorach *et al.* 2023](https://www.nature.com/articles/s41586-023-06094-5)) and control robotic arms ([Natraj *et al.* 2025](https://doi.org/10.1016/j.cell.2025.02.001)), and several companies now have large-scale clinical trials underway.

However, Byron Yu's lecture focused on a different side of BCIs: not as medical devices, but as tools for basic science, arguing that they provide a powerful way to investigating basic questions about neural circuit function. This is because, unlike in behavioural tasks, in BCI tasks the experimenter controls the mapping between neural activity and output, and can change this mapping at will.

To illustrate this point he presented a paper from his lab ([Golub *et al.* 2018](https://doi.org/10.1038/s41593-018-0095-3)) where they take this approach to ask a fundamental question about learning. In this work, they trained rhesus monkeys with a Utah array in primary motor cortex to perform a BCI centre-out cursor task, allowing them to learn an "intuitive mapping". They then perturbed the mapping within the manifold and asked how the population activity changed to learn the new mapping. They hypothesised that this could happen in one of three ways:

1. **Realignment.** The population produces new activity patterns tailored to the new mapping.
2. **Rescaling.** Each neuron keeps its tuning but changes how strongly it modulates, like turning volume knobs up or down.
3. **Reassociation.** The population keeps the same repertoire of activity patterns it already had, but reassigns which pattern is used for which intended movement.

<img class="fig-center" style="width: 85%;" src="/assets/images/posts/china/yu_learning_fig.png" alt="The three hypotheses for how population activity could change during learning">

*From Fig. 2 of Golub et al. 2018.*

They found that reassociation explained the data best. The repertoire of population activity stayed essentially fixed, and the monkeys learned by repurposing existing patterns for new targets rather than producing new ones.

As someone who is interested in BCIs and basic neuroscience, I found this work really inspiring.

### Mini-project: geometry of value in low-rank RNNs

During the last week of the course, we had the opportunity to complete a mini-project. For mine, I decided to investigate how constraining the rank of the recurrent weight matrix of RNNs affects the resulting neural geometry in a context-dependent value learning task.

To do so, I first built a "toy" model of neural representations which I could control by specifying the covariance matrix for task variables. This allowed me to enumerate all the possible geometries that could exist whilst having full control over what is encoded. A key question I wanted to answer was whether value was encoded in a factorised or context-dependent manner, and to measure this I planned to use cross-context decoding generalisation (introduced in [Bernardi *et al.* 2020](https://doi.org/10.1016/j.cell.2020.09.031)). However, to use this metric, I needed to make sure I had the right task conditions to avoid confounds, and ensure that my metric function produced different values for these two different geometries. Having these toy models of geometry allowed me to check this and verify all the analysis code was working before I actually trained any models. Once I had done this, I trained low-rank RNNs to perform my task and then measured the value factorisation as a function of recurrent rank.

To my surprise, the value representation was factorised in all models, from rank-1 to full rank. However, once I began to think about it, I quickly realised why. I had modelled the task in such a way that the only information that needed to be carried forward in recurrent activity to solve the task was the stimulus on the current trial, which was a one-dimensional variable. Therefore, constraining the recurrent rank had no impact on the code for value.

My naïve assumption was that full-rank models would learn a conjunctive code, where orthogonal value subspaces emerged for different contexts, and low-rank or rank-1 models would be forced to learn a factorised code. However, this didn't happen, and I realised that the recurrent rank doesn't determine the value code, nor completely determine the dimensionality of a representation (since it can be expanded by inputs) anyway. The recurrent rank simply constrains the dimensionality of the information that can be carried forward in time through the recurrent weights. The way I modelled the task, this was just the stimulus identity for the current trial, which was 1D. For the rank to have an impact, a >1D variable would have to be carried forward to solve the task (e.g. reward history, such as in uncued reversal learning tasks).[^4]

Despite this negative result, the project gave me the opportunity to explore some ideas I'm interested in using some tools I learned about during the course, and I'm definitely wiser for having tried it.

### Thoughts on the school

Overall I thought the summer school was great! The lectures covered a broad set of topics and were of high quality in general. It was nice to have the chance to talk with the lecturers about their work in a way that you may not have the chance to do, say, if they gave a talk at a large conference (where you might be less inclined to ask questions and there will be less opportunity to catch speakers to discuss work with). Interesting conversations often extended into lunch time following the lectures. In fact, after a week or two you naturally start coming up with new ideas for things to try as you talk with each other, which feels really fun. I think one of the best things about it is that it gives you a break from your own project and creates space to focus on learning new things and think about ideas without the pressure of producing any results right now (with the exception of the mini-project).

Aside from this, I made some great friends and had a lot of fun exploring China. It was my first time there so naturally I found it fascinating to experience for myself a country that I had heard so much about but yet knew very little about. Suzhou itself is a beautiful city famous for its classical gardens (a UNESCO World Heritage Site that includes two of China's four most celebrated gardens), old canals, and lots of great restaurants. CSHA is located a little outside of the city on Dushu Lake, a beautiful location where people are usually paddle boardng. The course itself kept us pretty busy but we still found time for plenty of hotpot, drinking plum wine, and swimming in Dushu Lake at sunset. It was really cool to meet people from all over the world and compare our PhD experiences. Suzhou is very close by train to other major cities like Shanghai, Hangzhou and Nanjing, so it's very easy to explore more of China if you get the chance to stick around. I went to Shanghai for a few days and then up to Beijing for the rest of my trip.

In summary, I'd highly recommend it to anyone doing a PhD in computational neuroscience who wants the chance to explore outside of their topic and spend a few weeks exploring China!

<img class="fig-center" style="width: 100%;" src="/assets/images/posts/china/dushu_lake_sunset.jpg" alt="Sunset over Dushu Lake, Suzhou, with the city skyline on the horizon">

*Sunset at Dushu Lake.*

---

[^1]: The concept of metalearning generally dates back further and there has been interesting discussion about attribution of credit for it. For a good discussion on this, see [this blog post from Lilian Weng](https://lilianweng.github.io/posts/2019-06-23-meta-rl/).

[^2]: One notable exception is [Hattori *et al.* 2023](https://www.nature.com/articles/s41593-023-01485-3) from Takaki Komiyama's lab. They used a light-activated CaMKII inhibitor to block plasticity in mouse OFC, and found that it slowed down metalearning of a reversal task, but had no effect on reversal behaviour once mice were experts. Silencing OFC activity, on the other hand, did impair expert behaviour, just as metaRL predicts.

[^3]: The basolateral amygdala (BLA) is a classic site of plasticity-based value learning: synapses there strengthen during both reward and fear conditioning, and BLA activity tracks conditioned responses.

[^4]: However, even in such tasks, constraining the recurrent rank would probably simply make the model unable to learn the task, rather than constraining the dimensionality of the value representation. A setting that could be interesting to explore would be one where it is necessary to keep track of the reward history of N options in order to choose between them, so there are N value variables to keep track of. A full-rank model could keep track of all of these reward histories, but a model with rank <N may be forced to learn a different solution. In this sense, the dimensionality of the value code could be constrained.
