---
title: "Notes on RL for AWS DeepRacer"
date: 2019-09-23
tags: [ML&AI]
excerpt: "Basics of Reinforcement Learning for AWS DeepRacer"
mathjax: "True"
---



# REINFORCEMENT LEARNING

## AWS DeepRacer Notes

### What is Reinforcement Learning?

Reinforcement Learning (RL) is a type of Machine Learning in which an *agent* explores an *environment*  to learn how to perform desired tasks by taking actions with good outcomes and avoiding actions with bad outcomes. 

An RL model will learn from its experience and over time-- will be able to identify which actions lead to the best results.

Other types of Machine Learning:


*   Supervised Learning -- example-driven learning, with labeled data of known outputs for given inputs, where a model is trained to predict outcomes from new inputs.
*   Unsupervised Learning -- inference-based training, with unlabeled data without known outputs, where a model is trained to identify related structures or similar patterns within the input data.

### How does AWS DeepRacer learn how to drive by itself?

In RL the agent interacts with an environment with the objective to maximize its total reward. 
The agent takes an *action*  based on the environment *state* and the environment returns the reward and the next state. The agent learns from trial and error, initially taking random actions and over time identifying the actions that lead to long-term rewards. 

### AGENT
The *agent* simulates the AWS DeepRacer vehicle in the simulation for the training. More especifically, it embodies the neural network that controls the vehicle, taking inputs and deciding actions.

### ENVIRONMENT
The *environment* contains a track that defines where the agent can go and what state it can be in. The agent explores the environment to collect data to train the underlying neural network.

### STATE 
A *state* represents a snapshot of the environment the agent is in at a point in time. For AWS DeepRacer, a state is an image captured by the front-facing camera of the vehicle. 

### ACTION
An *action* is a move made by the agent in the current state. For the AWS DeepRacer, an action represents a move at a particular speed and steering angle.

### REWARD
A *reward* is the score given as feedback to the agent when it takes an action in a given state. In training the AWS DeepRacer model, the reward is returned by a *reward function*. In general, you decide or supply a reward function to specify what is desirable or undesirable action for the agent to take in a given state. 

## TRAINING AN RL MODEL
Training is an iterative process. In a simulator, the agent explores the environment and builds up experience. The experiences collected are used to update the neural network periodically and the updated models are used to create more experiences. 
With AWS DeepRacer, we are training a vehicle to drive itslef. Let's explore this concept with a simplified example.

### A Simplified Environment
In this example, we want the vehicle to travel from point A to point B following the shortest path. Let's pretend we have a grid of squares and that each square represents an individual state and we will allow the vehicle to move up or down while facing the direction of the goal.

### Scores
We can assign a score to each square in the grid to decide wich behavior to incentivize. We can designate the squares on the edge of the track as 'stop states' which will tell the vehicle that it has gone off the track and failed. 
Since we want to incentivize the vehicle to learn to drive down the center of the track, we assign a high reward for the squares on the center line and a low reward elsewhere.

### An Episode
In RL training, the vehicle will start by exploring the grid until it moves out of bounds or reaches its destination.
As it drives around, the vehicle accumulates rewards from the scores we defined. This process is called an *episode*.

### Iteration
RL algorithms are trained by repeated optimization of cumulative rewards. 
The model will learn which action (and subsequent actions) will result in the highest cummulative reward on the way to the goal.
Learning does not just happen on the first go, it takes some iteration. First, the agent needs to explore the environment and see where it can get the highests rewards, before it can exploit that knowledge. 

### Exploration
As the agent gains more and more experience, it learns to stay on the central squares to get higher rewards.
If we plot the results from each episode , we can see how the model performs and improves over time.

### Exploitation and Convergence

With more experience, the agent gets better and it is able to get to the destination reliably. Depending on the exploration-exploitation strategy, the vehicle may still have a small probability of taking random actions to explore the environment. 

## Parameters of Reward Functions 

### Reward function parameter for AWS DeepRacer

In AWS DeepRacer, the reward function is a Python function which is given certain parameters that describe the current state and returns a numeric reward value.
The parameters passed to the reward function describe various aspects of the state of the vehicle, such as its position and orientation on the track, observed speed, stearing angle and more. 
We will explore some of these parameters and how they describe the vehicle as it drives around the track:


*   Position on the track
*   Heading
*   Waypoints
*   Track width
*   Distance from center line
*   All wheels on track
*   Speed
*    Steering angle

### 1- Position on the track

The parameters ```x``` and ```y``` describe the position of the vehicle in meters, measured from the lower-left corner of the environment. 

### 2- Heading

The ```heading``` parameter describes the orientation of the vehicle in degrees, measured counter-clockwise from the X-axis of the coordinate system. 

### 3- Waypoints

The ```waypoints``` parameter is an ordered list of milestones placed along the track center. 
Each waypoint in ```waypoints``` is a pair ```[x, y]``` of coordinates in meters, measured in the same coordinate system as the car's position. 

### 4- Track Width

The ```track_width``` parameter is the width of the track in meters.

### 5- Distance from the center line

The ```distance_from_center``` parameter measures the displacement of the vehicle from the center of the track.
The ```is_left-of_center``` parameter is a boolean describing whether the vehicle is to the left of the center of the track. 

### 6- All wheels on track 

The ```all_wheel_on_track``` parameter is a boolean (true/false) which is true if all four wheels of the vehicle are inside the track borders and false if any wheel is outside the track.

### 7- Speed

The ```speed``` parameter measures the observed speed of the vehicle, measured in meters per second. 

### 8- Steering angle

The ```steering_angle``` parameter measures the steering angle of the vehicle, measured in degrees. 
This value is negative if the vehicle is steering right and positive if the vehicle is steering left. 

## The Reward Function

### Putting all the pieces together

With all these parameters, we can define a reward function to incentivize whatever driving behavior we like.
The following are examples of reward functions:

### 1- Stay on Track

With this function, we give a high reward for when the car stays on the track and penalize if the car deviates from the track boundaries.
This examples uses the ```all_wheels-on_track```, ```distance_from_center``` and ```track_width``` parameters to determine whether the car is on the track and give a high reward if so. 

### 2- Follow Center Line

In this example, we measure how far the car is from the center of the track and give a higher reward if the car is close to the center line. 
This example uses ```track_width``` and ```distance_from_center``` parameters  and returns a decreasing reward the further the car is from the center of the track. 

### 3- No Incentive

An alternative strategy is to give a constant reward on each step regardless of how the car is driving. 
This example does not use any of the input parameters -- instead it returns a constant reward of ```1.0``` at each step. 
The agent's only incentive is to sucessfully finish the track and it has no incentive to drive faster or follow any particular path though it may behave erratically. 





## The Basic Reward Function

The basic reward function operates off of distance from the center lane using 'markers' at different percentages of the track width.

![alt text](https://s3.amazonaws.com/video.udacity-data.com/topher/2019/June/5d116efd_l2-reward-function/l2-reward-function.png)

In the above image, we can see that there are different rewards based on how far the car is from the center line. 
Here's the code from the AWS console:

```python
def reward_function(params):
     '''
     Example of rewarding the agent to follow center line
     '''
     
     # Read input parameters
     
     track_width = params['track_width']
     distance_from_center = params['distance_from_center']
     
     # Calculate 3 markers that are varying distances away from the center line
     
     marker_1 = 0.1 * track_width
     marker_2 = 0.25 * track_width
     marker_3 = 0.5 * track_width
     
     # Give higher reward if the car is closer to center line and vice versa
     
     if distance_from_center <= marker_1:
         reward = 1.0
         
     elif distance_from_center <= marker_2:
         reward = 0.5
         
     elif distance_from_center <= marker_3:
         reward = 0.1
         
     else:
         reward = 1e-3 # likely crashed / close to off track
         
     return float(reward)

```

In this code, we first gather the parameters for track width and the distance from the center line. Then, we create three markers based off if the track width-- one at 10% of the track width, another at 25% width and the last at half of the track width.
From there, it's a simple if/else statement that gives different, decreasing rewards based on the vehicle being within a given marker or not. If its outside all three markers, notice that the reward is almost zero.


## Machine Learning Algorithms

*   Supervised Learning -- trains a model based on providing labels to each input, such as classifying between images of a dog and those that are not a bulldog.
*   Unsupervised learning can use techniques like clustering to find relationships between different points of data, such as in detecting new types of fraud.
*    Reinforcement Learning -- uses feedback from previous iterations, using trail and error the model.

More info on the above topics:

*    [Supervised vs. Unsupervised Learning](https://towardsdatascience.com/supervised-vs-unsupervised-learning-14f68e32ea8d)
*    [Intro to Machine Learning](https://www.udacity.com/course/intro-to-machine-learning--ud120)

### Hyperparameters

*   Discount factor -- determines the extent to which future rewards should contribute to the overall sum of expected rewards. At a factor of zero, this means that DeepRacer would only care about the very next action and its reward. With a factor of one, it pays attention to future rewards as well.
*    Policy -- this determines what action the agent takes given a particular state. Policies are split between stochastic and deterministic policies. Note that policy functions are often denoted by the symbol pi. 
     *   Stochastic -- determines a probability for choosing a given action in a particular state (e.g. and 80% chance the vehicle goes straight, 20% chance to turn left)
     *   Deterministic -- directly maps actions to states.
     
* Convolutional Neural Network (CNN) -- a neural network whose strength is determining some output from an image or set of images. In our case, it is used with the input image from the DeepRacer vehicle.

The training cycle --the agent chooses an action, moving to a new state in the environment and gaining some reward. 

![alt text](https://video.udacity-data.com/topher/2019/June/5d127901_l3g3/l3g3.png)



### Value Functions

*   Value Functions -- indicate which actions you should take to maximize rewards over the long-term (and expected rewards when starting from some given state). These are often represented with the capital letter 'V'
*   AWS DeepRacer uses the Proximal Policy Optimization (PPO) algorithm to help optimize the value function.
*   Policy network (aka actor network) decides which action to take given an input image
*   Value network (aka critic network) estimates the cummulative result given the input image. 

## Training Cycle

### Optimization
A highly iterative process used in order to find the best policies to follow in the environment.

### SageMaker
Used to train RL models.

### RoboMaker
Used to create the virtual space / environment used for training.

### S3
The storage bucket used to hold the model files.

### REDIS
All the training data gets stored in Redis. At a high level, we start with *episodes* which are runs around the track from the starting line to an end state (finish line, crashing off the track, etc.). Within each episode, the course is further divided up into steps or *segments*. Furthermore, these are subdivided into *experiences* which are the state, action , reward and the new state from a given point in time. 

![Training Process](https://video.udacity-data.com/topher/2019/June/5d13e296_l4g1/l4g1.png)

In Machine Learning, there are Parameters and Hyperparameters.

*   Parameters -- Internal to the model and can be learned from training. 
*   Hyperparameters -- External to the model and set by you before training. They cannot be estimated/inferred by the data. We cannot know what their best values are but we can approximate by trial and error.

### The Reward Function

In RL, the reward function is the primary code uded to incentivize optimal actions. It's a mechanism used by the environment to let the agent know how it's doing. The agent takes a particular action in a given state and receives either an immediate reward or a penalty. 
For AWS DeepRacer, the reward function is vital to optimizing the models and enhancing performance around the track. For instance, when using the AWS DeepRacer console to train a model with a supported framework, the reward function is the only application-specific piece and it depends on our input.
AWS DeepRacer includes various parameters that will help you optimize your reinforcement learning algorith. 
See above for parameters and descriptions.

![Examples of Parameters](https://video.udacity-data.com/topher/2019/June/5d13e2d5_l4-parameters/l4-parameters.png)

A great reward fucntions can help us better optimize our RL model. In AWS DeepRacer, the reward function is written in Python code and it uses different input parameters to help encourage good behavior and disincentivize poor behavior. There is no single right answer for which parameters to include in our reward function and our best reward function will likely require a lot of experimentation. This experimentation can often be done more easily and quickly in simulation.  

A best practice for iterating on rewad functions is just to update one thing at the time-- for instance: adding one additional parameter into the basic reward function. The other reward function in the AWS console-- adds a parameter to avoid steering too much so they car can travel faster by following a straight line rather than zig-zagging across the track. 

## Tuning Hyperparameters

As mentioned previously, we can set hyperparameters values prior to training our model. By changing these, we can make additional improvements to our model and get a faster racer. Also, remember that there is no one single best tunning of hyperparameters. We'll have to experiment and iterate to find the best values.

There are eight (8) hyperparameters associated with the DeepRacer algorithm--all these hyperparameters can be tuned before training our model:


1.   Batch Size -- defines how much of the data the model should work through before each new update. Typycally the batch size can be equal to or less than the entire size of the training data. For the AWS DeepRacer, batch size determines hows many images will be used for training. Batch size is a required hyperparameter and its value can be 32, 64, 128, 256, 512.
2.   Number of Epochs -- determines how many times the algorithm will pass through the batch dataset before updating the training weights. In general, we want to increase the number of epochs until the validation accuracy is minimized. Large number of epochs is acceptable when the batch size is large. Number of epochs is not a required hyperparameter and its value can range from 3-10. 
3.   Learning Rate -- controls de speed at which the algorithm learns. It determines the times between the weights updates. Too large of a learning rate would prevent weights from reaching an optimal solution. A small learning rate might result in the algorithm taking longer to learn.  
4.   Exploration -- gives a balance between exploitation and exploration. Exploitation is when the algorithm makes decision based on information it already has where as exploration is when the algorithm gathers additional information beyond what is already been collected. For instace -- exploration helps us find a high reward path that may not have been discovered before. Exploration can be categorical and epsilon. Categorical exploration has a discrete action space. Epsilon exploration has a continuous action space. Epsilon greedy -- will decrease the exploration value over time so that it explores a lot at first but later will perform actions more and more based on experience while still allowing for some random exploration.    
5.   Entropy -- controls the degree of randomness of an action that an agent/vehicle might take in a given situation. The larger the entropy the more random actions the agent will take fro exploration. We can use these hyperparameter to have the modle explore new options instead of performing the same actions  over and over again with sub-optimal results. 
6.   Discount Factor -- helps the model decide the extent to which future rewards should contribute to the overall sum of expected rewards. With a smaller discount factor the agent will only consider immediate rewards. This is not a required hyperparameter and its range is 0-1 with a default value of 0.999.
7.   Loss Type -- is an objective network function used to update the network weights. A good training algorithm should make incremental changes to the agent strategy so that it gradually transitions from taking random actions to taking strategic actions. There are two options for this hyperparameter: Huber Loss and Mean Squared Error Loss. The two behave similar for small updates but as the updates get larger Huber loss takes smaller increments compared to Mean Squared Error loss. Huber loss can be used when we have convergence problems whereas Mean Squared Error Loss can be used when we want the  model to train faster. 
8.   Episodes -- defines the number of tasks the algorithm will go through during training 



