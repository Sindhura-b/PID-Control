# PID Control for path tracking

In this project PID controller has been implemented to manuever the vehicle around the lake race track in the simulator. The simulator provides cross track error (CTE) and the velocity (mph) in order to compute the appropriate steering angle required to manuever safely. 

[//]: # (Image References)
[image1]: ./simulation.png

---

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## PID Control

PID control involves chosing optimal gains K_p, K_i and K_d such that a system follows desired trajectory.

## Parameter tuning

<img src="./simulation.png" width="450" height="350"> 

All parameters are tuned manually. Although there are alogirthms like twiddle and SGD that could tune the parameters automatically, manual tuning is chosen here to get a better understanding of the behavior of controller for different gain values. 

The tuning is done by initially chosing a non-zero value for K_p, with K_i and K_d set to zero. K_p is tuned till car follows the track for atleast 4 sec, beyond which it oscillates. Only P-Controller could not achieve better results as it is prone to over-shooting and never quite reaches the reference trajectory, instead oscillates around it. Hence, the oscillations in the system are reduced by increasing K_d. In case where the response of the car is slow, K_d is reduced or K_p is increased. It was observed that increasing K_i made the car go off the track. So, it was kept as low as possible. Even after tweaking the gains several times, car seemed to go off-track at curves. This could be because the car is steering with increasing speed. So, i implemented another P-Controller to maintain constant speed instead of maintaining constant throttle. The gains are tweaked several times till the car drove around the track safely. Final values of gains for steering controller are K_p = 0.2, K_i = 0.0001, K_d = 1.0 and the gains for speed controller are K_p = 0.005 ,K_i = 0.0 and K_d = 0.0.

