## Papers on Hierarchical RL

1. [Data-Efficient Hierarchical Reinforcement Learning](https://papers.nips.cc/paper/7591-data-efficient-hierarchical-reinforcement-learning.pdf), Nachum et al., *NeurIPS*, 2018. 
   * This paper proposes a two-level policy, the high level policy specifies a goal given a state of the environment. The low level policy takes an action given the state and the goal. The reward assigned by the high level policy to the low level policy is based on how close the new state is compared to the old state and the goal.
   * It works directly with the raw state, instead of learning a representation to specify goals. The authors mentions this is important as it eliminates the samples needed to learn representation and the low level policy can be provided with reward right away.
   * It uses off-policy correction to reuse past samples of the low level policy. The main problem is that the (state,goal,action,reward) tuples observed in the past cannot be used for learning by the low level policy under the current instantiation. The main idea is to relabel the goals so that the past samples are likely to be generated from the current policy.

2. [Feudal Networks for Hierarchical Reinforcement Learning](https://arxiv.org/pdf/1703.01161.pdf), Vezhnevets et al., *ICML*, 2017.
   * There are two networks -- the manager and the worker. The manager network specifies goals in a latent space. The worker uses the same latent space and try to learn policy that completes the proposed goal at a given state in the learned representation.
   * The two networks are trained independently. The reward for the manager network is extrinsic i.e. obtained from the environment. But the reward for the worker is a combination of intrinsic and extrinsic reward. The intrinsic reward measures the cosine similiarity between the goal and difference in state transition. Intuitively, this enforces taking actions in the same direction as the goal in the latent space.
   * The manager works at a lower temporal abstraction setting than the worker, and can probably avoid problems of sparse rewards.

3. [The Option Critic Architecture](https://arxiv.org/pdf/1609.05140.pdf), Bacon et al., *AAAI*, 2017. 
    * This paper proves two policy gradient theorems in the context of the options framework. The policy over options have two parameters, $\theta$ (intra-option policy parameters i.e. specifies the probability of taking an action at a state in the context of a policy) and $\nu$ (termination parameter i.e. specifies the probability of termination at a state given a policy).
    * These two theorems immediately lead to an actor-critic like algorithm, where the critic updates the Q values for a given state, option pair and the actor updates the parameters for intra-option policy and termination policy.
    * The architecture needs to specify the number of options but not the associated subgoals. Experiments suggest that the architecture is able to learn meaningful options (which complete interpretable subgoals) for several standard benchmarks.

4. [Learning Multi-Level Hierarchies with Hindsight](https://openreview.net/pdf?id=ryzECoAcY7), Levy et al., *ICLR*, 2019.
    * Existing algorithms do not efficiently learn multiple levels within a hierarchy in parallel.
    *
