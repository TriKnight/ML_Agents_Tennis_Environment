# ML_Agents_Tennis_Environment
![Tennis](misc/Tennis_envi.gif)
## 1. Setup Environment and Install Requirements 
The Project use the MLAngents version 0.4.0 so we need to do some following steps
### 1.1 Install Anaconda & Create virtual environment using conda
Install Anaconda following link bellow

https://www.anaconda.com/products/individual

Create virtual environment

```
# Create the virtual env DQN
conda create -n DQN_navigation python=3.6
# activate environment
source activate DQN_navigation
```
### 1.2 Install all dependence
```

# clone the udacity repo
git clone https://github.com/udacity/deep-reinforcement-learning.git

# go to the python folder of the repo
cd deep-reinforcement-learning/python

# install the unityagents package from this folder
pip install -e .

# git clone DQN_Navigation_Project
cd ..
https://github.com/TriKnight/ML_Agents_Tennis_Environment

# install the requirements from our package
cd ML_Agents_Tennis_Environment
pip install -r requirements.txt

```
### 1.3 Create and Adding Kernel to Jupyter notebook
```
conda install -c anaconda ipykernel
python -m ipykernel install  --user --name=DQN_navigation
```
1. Open Jupyter notebok. 
```
jupyter notebook
```
2. Open Reacher_Continuous_Control


3. Change the Kernel ```Kernel/Change Kernel/DQN_navigation```


## 2. Unity Tennis Enviroment


In this environment, two agents control rackets to bounce a ball over a net. If an agent hits the ball over the net, it receives a reward of +0.1. If an agent lets a ball hit the ground or hits the ball out of bounds, it receives a reward of -0.01. Thus, the goal of each agent is to keep the ball in play.

The observation space consists of 8 variables corresponding to the position and velocity of the ball and racket. Each agent receives its own, local observation. Two continuous actions are available, corresponding to movement toward (or away from) the net, and jumping.

The task is episodic, and in order to solve the environment, your agents must get an average score of +0.5 (over 100 consecutive episodes, after taking the maximum over both agents). Specifically,

- After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 2 (potentially different) scores. We then take the maximum of these 2 scores.

- This yields a single **score** for each episode.

The environment is considered solved, when **the average (over 100 episodes) of those scores is at least +0.5**.

### Download the Unity environment with the Agents  

Download the environment from one of the links below and decompress the file into your project folder.  
You need only select the environment that matches your operating system:

- Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Linux.zip)
- Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis.app.zip)
- Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Windows_x86.zip)
- Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P3/Tennis/Tennis_Windows_x86_64.zip)
    
## 3. Multi-Agent Deep Deterministic Policy Gradient (MADDPG)
The environment contains 2 agents who are playing tennis.  The MADDPG Algorithms is a framework of centralized training with decentralized execution. The MADDPG allow multi-agents can learn to compete and collaborate each other. 

![MADDPG Algorithms](https://github.com/TriKnight/ML_Agents_Tennis_Environment/blob/master/misc/MADDPG.png)

In the diagram show the Overview of our multi-agent decentralized actor, centralized critic approach. Each Agent in the MADDPG is an “actor” and each actor get advice from a “crittic” that help “actor” decide the actions during the training time. All the agents do not need to access the central critic at the test time, they action based on their observation combined with their predictions of other agents behaviors.

**Decentralized execution** is when each Agent has its own private Actor network and takes actions when observing the environment.

**Central Learning** is each agent's own private Critic Network, the Critic Network of each Agent has full visibility on the environment. It not only takes action and observation of a particular agent, it also takes all the observations and actions of all other agents.  The output of the Critic Network is still the Q value estimated given a full observation input (all agents) and a full action input(all agents).  The Critic Network is only active in the training time and disable in the running time.

**Experience Storage** is storing all states, actions, reward, next states, collected during interaction of environment.

**Explorations and noise decay** I use the  Ornstein–Uhlenbeck  seems to be the best algorithm to add noise. However,  the common failure mode of the DDPG is the learner to overestimate Q-value then the policy breaking, the scores result get good at the beginning but at the end, this will reduce dramatically. Because it exploits the errors in the Q-function.So, That means, I add noise decay to the target action and make the agent hard to exploit the error in the Q-function  by smoothing out Q along changes action.

## 4. References
- [Multi-Agent Actor-Critic for Mixed Cooperative-Competitive Environments](https://arxiv.org/pdf/1706.02275.pdf)
- [Open AI](https://openai.com/blog/learning-to-cooperate-compete-and-communicate/)
- [Medium Markus Buchholz](https://medium.com/@markus.x.buchholz/deep-reinforcement-learning-deep-deterministic-policy-gradient-ddpg-algoritm-5a823da91b43)
- [Silviomori Blog](https://github.com/silviomori/udacity-deep-reinforcement-learning-p3-collab-compet/blob/master/Report.md)

