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
    * This paper proves two policy gradient theorems in the context of the options framework. The policy over options have two parameters, (a) intra-option policy parameters i.e. specifies the probability of taking an action at a state in the context of a policy, and (b) termination parameter i.e. specifies the probability of termination at a state given a policy.
    * These two theorems immediately lead to an actor-critic like algorithm, where the critic updates the Q values for a given state, option pair and the actor updates the parameters for intra-option policy and termination policy.
    * The architecture needs to specify the number of options but not the associated subgoals. Experiments suggest that the architecture is able to learn meaningful options (which complete interpretable subgoals) for several standard benchmarks.

4. [Learning Multi-Level Hierarchies with Hindsight](https://openreview.net/pdf?id=ryzECoAcY7), Levy et al., *ICLR*, 2019.
    * Existing algorithms do not efficiently learn multiple levels within a hierarchy in parallel.
    
5. [Learning Abstract Options](https://papers.nips.cc/paper/8243-learning-abstract-options.pdf), Riemer et al., *NeurIPS*, 2018.
    * Presents general policy gradient theorems that can be applied to a hierarchy of options.
    * Given a state, the top level first chooses an option, say o_1. Then an option from the next level say o_2 is chosen according to the intra-option policy for o_1. This continues for N levels until a primitive action a is taken by the Nth level. The termination functions are invoked in a bottom-up fashion. An option at level k can terminate only if all the options at levels higher than k+1 have terminated. This enables the higher level options to be more temporally extended compared to
        the lower level options.
    * The gain from considering hierarchical options framework is not very impressive. I would have loved to see settings where rewards are really sparse.
6. [Learning Options end-to-end for Continuous Action Tasks](https://arxiv.org/pdf/1712.00004.pdf), Klissarov et al., *arXiv*, 2017.
    * Combines the option-critic architecture with the Proximal Policy Optimization (PPO) for environments with continuous actions.
    * Works well for environments that demonstrate compositionality.

7. [Finding Options that Minimize Planning Time](https://arxiv.org/pdf/1810.07311.pdf), Jinnai et al., *arXiv*, 2019.
    * This paper considers the problem of finding the smallest set of options so that planning converges in less than a maximum number of iterations of the planning algorithm.

8. [When Waiting is not an Option: Learning Options with a Deliberation Cost](https://arxiv.org/pdf/1709.04571.pdf), Harb et al., *arXiv*, 2017.
    * One of the main challenges in the options framework is to learn a good set of options. This paper proposes to define a good set of options as the ones that allow an agent to learn and plan faster.
    * Intuitively, the cost of continuing the execution of an option is less than the cost of switching to a different option. This is introduced in learning by introducing the concept of *deliberation cost* which defines the cost of switching to a different option.
    * The learning problem is maximize discounted sum of rewards subject to a bounded deliberation cost. The constrained optimization is difficult to solve in general. So the authors propose to optimize a lagrangian formulation where a regularization parameter \eta controls the importance given to the deliberation cost. 
    * The parameter \eta can also be interpreted as a margin parameter as it adds directly to the advantage function. Therefore, a higher value of \eta enforces changing policies only if the advantage of doing so is high.
    * The main motivation of the paper was to incorporate the framework of bounded rationality with the help of deliberation cost. However, the current formulation seems insufficient and needs to include other types of deliberation costs to truly reflect the notion of bounded rationality.
    
9. [Learning with Options that Terminate Off-Policy](https://arxiv.org/pdf/1711.03817.pdf), Harutyunyan et al., *AAAI*, 2018.

10. [Discovering Options for Exploration by Minimizing Cover Time](https://arxiv.org/pdf/1903.00606.pdf), Jinnai et al., *arXiv*, 2019.
    * This paper studies how to accelerate exploration in an environment with sparse reward.
    *
