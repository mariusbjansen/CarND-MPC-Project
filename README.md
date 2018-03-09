# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Preface
In the project **m**odel **p**redicitve **c**ontrol (MPC) the goal is to implement a controller which can safely drive the car around the test track. The two variable which are used to manipulate the trajectory of the host vehicle are acceleration/throttle and steering. One benefit of MPC over PID-controllers is, that MPC can anticipate future events and can take control actions accordingly (https://en.wikipedia.org/wiki/Model_predictive_control)
A path which is basically the center of the road is given. Based on the upcoming part of the path - which is represented by a third order polynomial, multiple trajectories are calculated and evaluated. Evaluation considers the **c**ross **t**rack **e**rror (cte), orientation error and additional cost factors for using of actuator and change between sequential actuations. The best (local) trajectory based on these metrics is chosen. Between control commands and the actuation, there is a 100 millisecond latency. 
A lot of ideas and even code from the lesson *20: Model Predictive Control* can be applied. In comparison to the *Mind the Line* quiz, the planned trajectory is now a third order polynomial.

## Project Rubric

### Student describes their model in detail. This includes the state, actuators and update equations.

![simple](./simple.svg =640x)