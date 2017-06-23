+++
date = "2017-06-14"
title = "The BrickPi"

+++

![The BrickPi](/blog_imgs/brickpi.jpg)

The BrickPi is an attachment from Dexter Industries for the Raspberry Pi that allows the Pi to easily use NXT motors and sensors. It can control four NXT motors and get input from four NXT sensors. It fits on top of a Pi and comes with a lego compatible case to protect it and the Pi. The BrickPi can be bought online at [DexterIndustries.com](https://www.dexterindustries.com/) and instructions to get the BrickPi SD card iamge can be found [here](https://www.dexterindustries.com/howto/install-raspbian-for-robots-image-on-an-sd-card/).

The BrickPi can be programmed in C, scratch, or python. I chose to use python. The SD card image comes with examples that you can use to learn the BrickPi commands, but here are some of the standard ones used in a program to run a motor.

~~~~python
from BrickPi import *   #use the BrickPi
BrickPiSetup()    #initiate the BrickPi

BrickPi.MotorEnable[PORT_A] = 1   #initiate motor A

BrickPi.MotorSpeed[PORT_A] = 255    #motor A state to max speed

while True:   #this needs to be repeated
  BrickPiUpdateValues()   #update states with the BrickPi
~~~~

The commands for sensors are similar. The examples on the SD card show each command and what kind of  input each sensor has.
