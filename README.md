# Prediction Phase in the trajectory generation of cars
 
To understand what the prediction does, imagine at T-shaped intersection. You are a self-driving car that has just pulled up to the stop sign. You want to turn left but your sensors notice another vehicle coming from the left. At this point, you as a human probably know the green vehicle will do one of two things,
* Either it will go straight 
* Or it will go right.


 <p align="right"> <img src="./img/3.png" style="right;" alt=" the green vehicle will do one of two things" width="600" height="400"> </p> 
 
Let's say that at this point, the green vehicle starts slowing down and moving right in the lane.Well, you probably know that they are turning right which means it is safe for you to go left. By making a successful prediction, you were able to make a decision that got you to your destination safely and efficiently and what makes prediction interesting but also challenging is that it is inherently multi-modal. 


A good way of thinking about what that means is to think of how you would answer the question "Where is the green car likely to be in five seconds?" If we try to come up with the probability distribution, we would see that it has multiple peaks or moats. If the car is going straight, then the car is likely to be somewhere here (see gif) but if the car turns right, then it's more likely to be here(see gif).
 
 <p align="right"> <img src="./img/1.gif" style="right;" alt=" Where is the green car likely to be in five seconds" width="600" height="400"> </p> 

In general, the way we think about handling multi-modal uncertainty is by maintaining some beliefs about how probable each potential mode is. Initially, if we just see this green car coming from far away, those beliefs could be initialized using some prior knowledge about this intersection (see geif at time step 0).
In this case, let's say that car generally goes straight at this intersection.But as we continue watching the car we may notice that it is slowing down. Since this behavior is more consistent with turning right, the probability of turning right increases. And then, at the next timestep, we might notice that the car has already started turning right which again increases the probability of turning right.
And as we keep observing, we continue updating our belief based on new evidence until eventually we can predict with high certainty that the vehicle is turning right at this intersection.

 
 <p align="right"> <img src="./img/2.gif" style="right;" alt=" multi-modal uncertainty" width="600" height="400"> </p> 

