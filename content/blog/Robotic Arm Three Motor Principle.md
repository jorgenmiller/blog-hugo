+++
date = "2017-04-05"
title = "Robotic Arm Three Motor Principle"

+++

Robotic Arms are fun to build and can complete many different tasks. For a full three dimensional movement, six controlled joints are required. Usually, they are arranged some what like this.

![Six motor control of a robotic arm](/blog_imgs/sixmotorarmcontrol.jpg)

Six servos can be a lot of motors to control. Sometimes it is excessive. In my [Science Fair project in 2017](https://jorgenmiller.github.io/blog/science-fair-2017/), there was not a need to move upwards. Also, NXT can only support three motors (without brick-to-brick communication). I made a design that requires only three motors to move the end of the arm in a two dimensional plane.

This Lego arm is controlled by only three motors. This design functions when the arm makes a triangle where
- Two side lengths stay the same, but not necessarily equivalent
- the two base angles are free to rotate
- the top angle is controlled by a servo

In this triangle, when the top angle is changed, the bottom side of the triangle decreases or increase and the two base angles will also change. The amount that the bottom side changes depends on the lengths of the sides.

In a robotic Arm, it would look like this.

![Three motor control of a robotic arm](/blog_imgs/threemotorarmcontrol.jpg)

In total, the arm would rotate its base with one motor, extend the end of the arm with another motor, and complete a task (like grabbing an object) with another motor. The arm only uses three motors to move around its area and activate the end effector.


Here is a Lego Arm that I built that functions using this principle.

![Three motors in a Lego arm](/blog_imgs/threemotorarm.jpg)
