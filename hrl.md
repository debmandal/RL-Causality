## Papers on Hierarchical RL

* [Data-Efficient Hierarchical Reinforcement Learning](https://papers.nips.cc/paper/7591-data-efficient-hierarchical-reinforcement-learning.pdf), Nachum et al., *NeurIPS*, 2018. 
   .. -- This paper proposes a two-level policy, the high level policy specifies a goal given a state of the environment. The low level policy takes an action given the state and the goal. The reward assigned by the high level policy to the low level policy is based on how close the new state is compared to the old state and the goal.
   .. -- It works directly with the raw state, instead of learning a representation to specify goals. The authors mentions this is important as it eliminates the samples needed to learn representation and the low level policy can be provided with reward right away.
   .. -- It uses off-policy correction to reuse past samples of the low level policy. The main problem is that the (state,goal,action,reward) tuples observed in the past cannot be used for learning by the low level policy under the current instantiation. The main idea is to relabel the goals so that the past samples are likely to be generated from the current policy.
