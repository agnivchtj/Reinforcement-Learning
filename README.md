# Objective

The goal of the project is to program an agent to learn a route, through a maze, based on rewards. 
The target location is a rewarded location in that maze, and the agent will learn to navigate from a fixed start to this rewarded target via exploration and repetition. 

For this, the approach taken is based on Reinforcement Learning (RL). The aim is to implement a model-free off-policy version of RL called Q-Learning, using a tabular representation for `Q(s,a)`, i.e., a matrix with two dimensions S and A; S being all possible states (the locations in the maze), and A being all actions possible in each state (up, down, left, right).  
A value in the matrix at location `(s,a)` represents the `Q(s,a)` value, i.e., the value of an action a in state s.

Essentially, the problem to solve boils down to learning a `S x A` matrix of values with each value representing the utility of an s,a pair. 
Every step the agent takes updates one such value, namely the last visited `(s,a)` pair. As Q-learning is used, and Q-learning is off-policy (thus, updates are not based on actual actions chosen), we will update this value using the value of the best possible next action `Q(s',a.max)`. 

The full update rule is:

`Q(s,a).new = Q(s,a).old + a(r + yQ.max(s',a.max) - Q(s,a).old)` 

Where `Q.max(s',a.max)` is the Q-value of the best action so far in state `s'`.

The agent learns by taking random actions, and after each action updating `Q(s,a)`.  I will experiment with action selection (the policy) and it will be implemented with the `e`-Greedy algorithm. 
This method will take either a random action with a probability of `e` (exploration) or a greedy action with a probability of `1 - e` (exploitation). A random action is selected out of the 4 possible actions while a greedy action is an action with the highest predicted value so far, so it chooses the action with the highest `Q(s,a)` for the states we are now in.
Typically we find that with a high `e`-value, though the expected reward on a step might be lower, the total reward in the long-term is greater.