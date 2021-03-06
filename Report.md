# DeepRL-Continuous Control
Project 2 "Continuous Control" of the Deep Reinforcement Learning nanodegree.

Given the uncertainities for this project to be reviewed by the same reviewer, I am describing my background again. Basically, I am a civil engineer from Bangladesh who doesn't know civil engineering much let alone RL. RL is like Hebrew, not only RL the whole CS things seem like Hebrew to me- top to bottom I don't understand anything. I did only a Python course in my undergrad. That's it. Yet I tried this Nanodegree. Why? Firstly, I got one month free access to Udacity which I cannot afford otherwise. Secondly, I got an admission in an Erasmus Joint Master Degree Program of Hydroinformatics in Europe. My program arranges a conference named 'Symhydro'. The accepted papers of that conference get published in collarboration with Springer Water in a journal namely 'Advances in Hydroinformatics'. I read one of the papers from there- 'Large Markov Decision Processes Based Management Strategy of Inland Waterways in Uncertain Context.' I read the paper and didn't understand anything. That's how I got interest in RL and took the resolution to decode RL, though in reality I didn't understand many things while reading and doing so.

Thanks to the solution notebooks by Udacity and also the alumni of this Nanodegree. The solution codes I use here are managed through visiting their GitHub Repositories. Now, if I pass this nanodegree and get the certificate, I will be the happiest man in the world.


## Learning Algorithm
This Project 2 goes beyond DQN. Because it includes new Deep RL techniques:
- **Actor-critic method** in which the actor computes policies to act and the critic helps to correct the policies based on its Q-values;
- **Deep Deterministic Policy Gradients (DDPG)**, which is similar to actor-critic methods but it differs because the actor produces a deterministic policy instead of stochastic policies; the critic evaluates such deterministic policy; and the actor is trained by using the deterministic policy gradient algorithm;
- **Two sets of Target and Local Networks**, which is a way to implement the double buffer technique in order to avoid oscillations caused by overestimated values;
- **Soft Updates** instead of hard updates so that the values of the local networks are slowly transferred to the target networks;
- **Replay Buffer** in order to keep training the DDPG Agent with past experiences;
- **Ornstein-Uhlenbeck(O-U) Noise** which is introduced at training in order to make the network learn in a more robust and more complete way.

Moreover, the DDPG Agent uses 2 deep neural networks to represent complex continuous states. 1 neural network for the actor and 1 neural network for the critic.

The neural network for the actor has:
- A linear fully-connected layer of dimensions state_size=33 and fc1_units=128;
- The ReLu function;
- Batch normalization;
- A linear fully-connected layer of dimensions fc1_units=128 and fc2_units=128;
- The ReLu function;
- A linear fully-connected layer of dimensions fc2_units=128 and action_size=4;
- The tanh function.

The neural network for the critic has:
- A linear fully-connected layer of dimensions state_size=33 and fcs1_units=128;
- The ReLu function;
- Batch normalization;
- A linear fully-connected layer of dimensions fcs1_units=128 + 4 and fc2_units=128;
- The ReLu function;
- A linear fully-connected layer of dimensions fc2_units=128 and output_size=1;

This implementation has the following metaparameters:

```
# replay buffer size (a very big database of SARS tuples)
BUFFER_SIZE = int(1e5)  

# minibatch size (the number of experience tuples per training iteration)
BATCH_SIZE = 128        

# discount factor (the Q-Network is aware of the intermediate future, but not the far future)
GAMMA = 0.99            

# for soft update of target parameters 
TAU = 1e-3           

# learning rate of the actor 
LR_ACTOR = 2e-4         

# learning rate of the critic 
LR_CRITIC = 2e-4        

# L2 weight decay
WEIGHT_DECAY = 0        
```

## Plot of Rewards

The DDPG Agent was trained for `168` episodes. In each episode, the agent is trained from the begining to the end of the simulation. Some episodes are larger and some episodes are shorter, depending when the ending condition of each episode appears. Each episode has many iterations. In each iteration, the DDPG Agent is trained with `BATCH_SIZE=128` experience tuples (SARS).

```
Episode 100	Average Score: 8.74
Episode 168	Average Score: 30.01
Environment solved in 168 episodes!	Average Score: 30.01
```

The rubric asks to obtain an average score of 30 for 100 episodes. The best model was saved. In the graph, the blue lines connect the scores in each episode. Whereas the red lines connect the average scores in each episode.

![Plot of rewards (training)](/images/plot-of-rewards-training.png)

After training, the saved model was loaded and tested for 20 episodes. Here are the results of such testing. You can see that, on average, the scores are greater than 30. 

```
Episode 1	Score: 38.63
Episode 2	Score: 36.70
Episode 3	Score: 39.03
Episode 4	Score: 34.90
Episode 5	Score: 38.80
Episode 6	Score: 39.48
Episode 7	Score: 35.97
Episode 8	Score: 36.33
Episode 9	Score: 35.88
Episode 10	Score: 34.23
Episode 11	Score: 35.06
Episode 12	Score: 37.35
Episode 13	Score: 34.50
Episode 14	Score: 33.27
Episode 15	Score: 38.15
Episode 16	Score: 33.54
Episode 17	Score: 15.25
Episode 18	Score: 32.18
Episode 19	Score: 31.91
Episode 20	Score: 36.68
```

In the graph, the blue lines connect the scores in each episode. There is only 1 error at episode `17` in which the score drops to `15.25`. All the other scores are greater than `30`.

![Plot of rewards (testing)](/images/plot-of-rewards-testing.png)

## Ideas for Future Work

There could be a better set of hyperparameters. Therefore, there is room for improvement.

So far, this implementation has only `5` techniques: 
- Deep Deterministic Policy Gradients (DDPG);
- Two sets of Target and Local Networks;
- Soft Updates;
- Replay Buffer;
- Ornstein-Uhlenbeck(O-U) Noise.

Future implementations can be improved by applying the following techniques:
- **Prioritized** experience replay;
- Distributed learning with multiple independent agents (TRPO, PPO, A3C, and A2C);
- Q-prop algorithm, which combines both off-policy and on-policy learning.
