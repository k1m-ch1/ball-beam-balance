# Plan

So this is a typical ball beam balance system where you have a ball, some sort of distance sensor, and some sort of servo to adjust the tilt of the inclined plane, and the goal is to keep the ball a fixed distance (which will be our setpoint) from the sensor.

Although this may seem like a boring and useless task, I think it's good to study the simplest cases in control systems, because, it's quite rare that you can apply all these analytical methods to an actual control system (because it's hard to get an accurate model of your system in the first place).

So to begin with, we will try generic black box and empirical control schemes on this problem, that is:

- Generic bang bang control (the acceleration is going to be very high, so make sure to clamp the whole system down or something)
- Generic blackbox emprical PID (perhaps starting with P, then adding D, then adding I)
- Nichols-Ziegler for PID

We can then try to create an approximate mathematical model of the system. I have two ideas I want to try:

- analyzing the physics and creating a differential equation
- collecting a bunch of data points and then letting some algorithm do the systems identification for us.

After we have a model, we can then try more analytical methods:

- root locus method for PID
- LQR controller

# Modeling the system

We'll need to actually design the systems first before we can model it, but here's the rough idea that we're going to do:

- approximate the moment of inertia of the ball
- assume that the servo can control position instantly, so our control variable $\theta$ is instant (if it makes that big of a difference, we can model the lag too)
- assume no backlash
- assume no slip on the ball

Then I think for something like this, it's probably easiest if we use some sort of energy method to determine the acceleration of the ball given the angle of the inclined plane, while assuming that the change of angle of the inclined plane has negligible effects on the acceleration of the ball.

# Notes

## Ball 

We will use a ball, ranging from a marble to a ping pong ball, so the diameter ranges from 25mm to 40mm. We'll need to make sure there's enough clearance, and that the sensor can measure it well.

## Servos

We'll try to use SG90S servos for now, but if movements are too jerky, and the lag is too much, we can move to a bigger MG996R servo motor (so make sure everything is designed to fit well)

## Gears

We'll first need a way to attach the servos to the gears, and then we also need to mount everything rigidly to the base.

We'll need to think about how big the gears should be to be strong enough. Also, if we 3d print the shafts, we're going to need to think about clearance, and whether a loose gear to shaft fit will significantly impact our gearing.

## VL53L1X tof distance sensor

So, apparently, we can program the region of interest, so that we only capture the distance of the ball, so we can try to do something about that.

# TODO

## Mechanics

- [] design the base
- [] design the arm
- [] design the inclined plane
- [] design a way to mount the gears
- [] assemble everything

## Electronics and programming

- [] solder the perf board, connect the servos, connect the sensors, just control it one by one see if everything works
- [] format the project that's standard for platformio projects
- [] code the controller (ensuring that the format of the controller is modular, because we're planning on using different kinds of controllers)


