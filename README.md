# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Preface
In the project **m**odel **p**redicitve **c**ontrol (MPC) the goal is to implement a controller which can safely drive the car around the test track. The two variable which are used to manipulate the trajectory of the host vehicle are acceleration/throttle and steering. One benefit of MPC over PID-controllers is, that MPC can anticipate future events and can take control actions accordingly (https://en.wikipedia.org/wiki/Model_predictive_control)
A path which is basically the center of the road is given. Based on the upcoming part of the path - which is represented by a third order polynomial, multiple trajectories are calculated and evaluated. Evaluation considers the **c**ross **t**rack **e**rror (cte), orientation error and additional cost factors for using of actuator and change between sequential actuations. The best (local) trajectory based on these metrics is chosen. Between control commands and the actuation, there is a 100 millisecond latency. 
A lot of ideas and even code from the lesson *20: Model Predictive Control* can be applied. In comparison to the *Mind the Line* quiz, the planned trajectory is now a third order polynomial.

## Project Rubric

### Student describes their model in detail. This includes the state, actuators and update equations.
The formula describing the kinematic model follows.

<img src="simple.svg" width="480" alt="Formulas" />

Host vehicle's position is given by *x* and *y*. Orientation of the host vehicle is *psi*. Velocity is *v*. The cross track error (defined by reference position and actual position laterally) is *cte* and psi error (error in orientation of host vehicle and reference) is *epsi*.

The actuator variables are acceleration *a* and steering *delta*.

The differntial equation describe how the current state is transformed into the next state at time t+1 given only the state at time t and input (which is control input: a and delta)

### Student discusses the reasoning behind the chosen N (timestep length) and dt (elapsed duration between timesteps) values. Additionally the student details the previous values tried.

Clearly it is important that the prediction horizon is the product of N and dt. For example if N=12 and dt=0.1s then the predicition horizon is 1.2s. The computational cost increases when N increases. The prediction horizon shouldn't be too short and not too long. Extremes would be taking into acount only the next 10ms or even minutes, which absolutely makes no sense. Stability of the controller is highly influences by the parameters N and dt. I see stable behaviour if I vary N from 10 to 25 and keeping dt at 100ms. I chose N=12 because it worked fine for me and I like 12 :-)

### If the student preprocesses waypoints, the vehicle state, and/or actuators prior to the MPC procedure it is described.
The waypoints are in a global coordinate system. I transform them into the host vehicle's coordinate system by the usual inverse matrix operation. (translation and rotation)

## The student implements Model Predictive Control that handles a 100 millisecond latency. Student provides details on how they deal with latency.
The kinematic equations depend upon the actuations from timestep t-1, but with a delay of 100ms (which is exactly the chosen timestep interval dt) the actuations are applied another timestep later t-2. The equations have been altered to account for this (MPC.cpp lines 119-122). 
I did not find the solution for latency myself. My tutor Eren pointed out that there is a solution present https://github.com/jeremy-shannon/CarND-MPC-Project/blob/master/src/MPC.cpp which I adapted.




