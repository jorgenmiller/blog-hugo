+++
date = "2017-06-21"
title = "Lego Offroad Vehicle with BrickPi"

+++

![A Lego Car](/blog_imgs/offroad_vehicle.jpg)

This Lego car is controlled by a Raspberry Pi with a BrickPi attached. It drives like a tank using joystick input from a USB logitech F310 gamepad. The wheels are directly connected to the Lego NXT motors. It also has 'suspension' because the plastic axles bend a bit. It can drive well on surfaces like gravel because the wheels need to slip as it turns since it drives like a tank.

![Oforad Vehicle in action](/blog_imgs/offroad_vehicle.gif)

The program uses threading to read input from the gamepad and drive the motors at the same time.

~~~~python
from inputs import get_gamepad
from BrickPi import *
import threading

BrickPiSetup()
BrickPi.MotorEnable[PORT_A] = 1
BrickPi.MotorEnable[PORT_B] = 1
BrickPi.MotorEnable[PORT_C] = 1
BrickPi.MotorEnable[PORT_D] = 1

quitting = False

def gamepad():
    while True:
        for event in get_gamepad():
            if event.code == "ABS_Y":
                BrickPi.MotorSpeed[PORT_A] = event.state / -128
                BrickPi.MotorSpeed[PORT_B] = event.state / 128
            elif event.code == "ABS_RY":
                BrickPi.MotorSpeed[PORT_C] = event.state / 128
                BrickPi.MotorSpeed[PORT_D] = event.state / -128
            elif event.code == "BTN_MODE":
                global quitting
                quitting = True
                return

gamepad = threading.Thread(target = gamepad)
gamepad.start()

while True:
    BrickPiUpdateValues()
    if quitting == True:
        sys.exit()
~~~~
