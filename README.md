# Lunar_Lander



https://user-images.githubusercontent.com/103886856/168421118-d087fab0-ffdf-48b4-97ee-5246c2bdbbe2.mp4




The main objective of the OpenAI's LunarLander-v2 gym is to land safely between the two flags. To achieve this goal, we need to change the hyperparameters of the model to train our ship and let it learn what actions to take.

First of all, a pilot was run to serve as a baseline, setting the hyperparameters without a clear objective. As shown in the following graph, this strategy did not achieve a good result after several iterations.

 ![image](https://user-images.githubusercontent.com/103886856/168420751-8215638c-3c0f-4ce9-9909-5ec4ab8c3c1b.png)
 
 Pilot version’s total reward.
 
 
Later, a set of hyperparameters were change with the idea of accelerating the convergence of the model to a good solution, even though if it is not the global best. As Shen, K. (2018) states, “using smaller batch sizes have been empirically shown to have faster convergence to “good” solution”. In this sense, the batch size was set to 64. Furthermore, the entropy factor was kept with a small number, to encourage the agent to exploit known solutions rather than exploring new ones. Thus, the entropy factor was set to 0.001. Finally, the actor and critic learning rates were set 10 times higher than in the pilot version, with the objective of increasing the size of the learning steps and converge to a minimum in the loss function faster, even if it not a global minimum. The two parameters were set with values of 0.001 each.

Then, two strategies were tested, having the combination of hyperparameters previously explained. The first strategy was focus on the short-term rewards, and the second was focus on the long-term rewards. In the first one, to give more importance to the short-term rewards, the scale reward was decreased and set with the value 0.001. Moreover, to emphasize more in the current state, the discount was also decreased and set with the values 0.7, meanwhile the GAE lambda was also decreased and set to 0.7, reducing the bias of the model rather than the variance.

In the second strategy, the scale reward was increased and set with the value 0.1, giving more importance to the long-term rewards compared to the previous strategy. In the same way, the discount was increased and set to 0.99, to give more importance to the future states. And, finally, the GAE lambda was also increased and set to 0.99, to reduce the variance and make the model more stable (Trivedi, 2019).
As shown in the following graph, the long-term strategy (in blue) quickly outperformed the short-term strategy (in orange), achieving a very good result after several iterations. The short-term strategy was stopped since it did not show much potential, and the time of the assignment was limited.
 
![image](https://user-images.githubusercontent.com/103886856/168420806-b920a455-a89b-45d9-90d5-2b8bd450a23a.png)

Short-term and long-term strategies’ total reward.

# Hyperparameters

The best combination of hyperparameters was found with the second strategy, in the checkpoint 490, achieving a total reward of 264 in the test, with the following combination:

- SCALE_REWARD:         float = 0.1
- MIN_REWARD:           float = -1000.
- HIDDEN_SIZE:          float = 128
- BATCH_SIZE:           int   = 64
- DISCOUNT:             float = 0.99
- GAE_LAMBDA:           float = 0.99
- PPO_CLIP:             float = 0.2
- PPO_EPOCHS:           int   = 10
- MAX_GRAD_NORM:        float = 1.
- ENTROPY_FACTOR:       float = 0.001
- ACTOR_LEARNING_RATE:  float = 0.001
- CRITIC_LEARNING_RATE: float = 0.001
- RECURRENT_SEQ_LEN:    int = 8
- RECURRENT_LAYERS:     int = 1    
- ROLLOUT_STEPS:        int = 2048
- PARALLEL_ROLLOUTS:    int = 8
- PATIENCE:             int = 200
- TRAINABLE_STD_DEV:    bool = False 
- INIT_LOG_STD_DEV:     float = 0.0

# REFERENCES
- Foster, C. (2019). Entropy loss for reinforcement learning. From https://fosterelli.co/entropy-loss-for-reinforcement-learning
-	Schulman, et al. (2016). High-dimensional continuous control using generalized advantage estimation. From https://arxiv.org/pdf/1506.02438.pdf
-	Shen, K. (2018). Effect of batch size on training dynamics. From https://medium.com/mini-distill/effect-of-batch-size-on-training-dynamics-21c14f7a716e
-	Trivedi, C. (2019). Proximal Policy Optimization Tutorial (Part 2/2: GAE and PPO loss). From https://towardsdatascience.com/proximal-policy-optimization-tutorial-part-2-2-gae-and-ppo-loss-fe1b3c5549e8
- Valdarrama, S. (2019). OpenAI Gym's LunarLander-v2 Implementation. From https://github.com/svpino/lunar-lander/
-	Yoon, C. (2019). Understanding Actor Critic Methods and A2C. From https://towardsdatascience.com/understanding-actor-critic-methods-931b97b6df3f



