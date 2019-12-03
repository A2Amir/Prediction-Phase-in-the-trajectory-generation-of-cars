# Prediction Phase in the trajectory generation of cars
 
To understand what the prediction does, imagine at T-shaped intersection. You are a self-driving car that has just pulled up to the stop sign. You want to turn left but your sensors notice another vehicle coming from the left. At this point, you as a human probably know the green vehicle will do one of two things,
* Either it will go straight 
* Or it will go right.


 <p align="right"> <img src="./img/3.png" style="right;" alt=" the green vehicle will do one of two things" width="700" height="400"> </p> 
 
Let's say that at this point, the green vehicle starts slowing down and moving right in the lane.Well, you probably know that they are turning right which means it is safe for you to go left. By making a successful prediction, you were able to make a decision that got you to your destination safely and efficiently and what makes prediction interesting but also challenging is that it is inherently multi-modal. 


A good way of thinking about what that means is to think of how you would answer the question "Where is the green car likely to be in five seconds?" If we try to come up with the probability distribution, we would see that it has multiple peaks or moats. If the car is going straight, then the car is likely to be somewhere here (see gif) but if the car turns right, then it's more likely to be here(see gif).
 
 <p align="right"> <img src="./img/1.gif" style="right;" alt=" Where is the green car likely to be in five seconds" width="700" height="400"> </p> 

In general, the way we think about handling multi-modal uncertainty is by maintaining some beliefs about how probable each potential mode is. Initially, if we just see this green car coming from far away, those beliefs could be initialized using some prior knowledge about this intersection (see geif at time step 0).

In this case, let's say that car generally goes straight at this intersection.But as we continue watching the car we may notice that it is slowing down. Since this behavior is more consistent with turning right, the probability of turning right increases. And then, at the next timestep, we might notice that the car has already started turning right which again increases the probability of turning right.
And as we keep observing, we continue updating our belief based on new evidence until eventually we can predict with high certainty that the vehicle is turning right at this intersection.

 
 <p align="right"> <img src="./img/2.gif" style="right;" alt=" multi-modal uncertainty" width="700" height="400"> </p> 

The responsibility of the prediction module is to do the following: 

* We take as input a map of the world and data from sensor fusion
* As output we generate some predictions of the future state of all the vehicles and other moving objects in the vicinity of our vehicle.

Typically, these predictions are represented by a set of possible trajectories like that two dotted arrows emanating from the green car in this scenario and an associated probability for each trajectory.

 <p align="right"> <img src="./img/4.png" style="right;" alt="The responsibility of the prediction module " width="700" height="400"> </p> 

**Before we get into the details, let me explain what we are going to discuss in this repository.**

<b>
 
1. First, we'll go through a brief overview where you will learn a bit more about the inputs and outputs to prediction.

2. Next, we will talk about how prediction is actually done.

3. We will discuss the two main classes of prediction techniques:model-based approaches and data-driven approaches. Model-based approaches use mathematical models of motion to predict trajectories and data-driven approaches rely on machine learning and examples to learn from (trajectory clustering will be expalined).

4. Then, we will dig into model-based approaches where I will introduce process models as a mathematical technique for modelling various maneuvers like lane changes, vehicle following, etc and introduce multi-modal estimators as an effective technique for handling the uncertainty associated with prediction, namely, the uncertainty about which maneuver an object will do in a particular situation.

5. Finally, we will dive deep into hybrid approaches which use data and process models to predict motion through a cycle of intense classification where we try to figure out what a driver wants to do and trajectory generation where we try to figure out how they are likely to do it.

6. We will end by implementing an algorithm called Naive Bayes to predict the motion of a car at a T-shaped intersection like the one you just saw.

</b>


