+++
date = "2017-06-15"
title = "The BrickPi and Motor Control"

+++

Here is a python program that I made for the BrickPi. The purpose is to get input from the right joystick and give output with the motors. The speed of motor B is controlled by the x position of the right joystick and the speed of motor c is controlled by the y position of the right joystick. The joysticks give values between 0 and 32,500 It also has the ability to quit the program if the mode button is pressed. On my logitech F310 gamepad, that is the center button labeled logitech.

The program uses inputs 0.1 to read the gamepad. Use `pip install inputs` to get it. Once installed, `get_gamepad()` may work properly, but you may need to edit it. you can find the name of your gamepad by looking in `/dev/input`.

The main difficulty I had when trying to make this program was reading the gamepad and instructing the BrickPi simultaneously. The gamepad uses a loop where it waits for an input, but the BrickPi needs to loop to run the motors. The gamepad loop normally blocks the BrickPi, but this program uses threading to do both.

~~~~python
from inputs import get_gamepad
from BrickPi import *
import threading

BrickPiSetup()
BrickPi.MotorEnable[PORT_B] = 1   #uses motors B and C
BrickPi.MotorEnable[PORT_C] = 1

quitting = False

def gamepad():    #make a thread for the gamepad
    while True:   #stay in the thread
        for event in get_gamepad():   #wait for user input in list of inputs
            if event.code == "ABS_RX":    #right joystick moved (x axis)
                BrickPi.MotorSpeed[PORT_B] = event.state / 128  #B moves 0-255
            elif event.code == "ABS_RY":    #right joystick moved (y axis)
                BrickPi.MotorSpeed[PORT_C] = event.state / 128  #motor C moves
            elif event.code == "BTN_MODE":    #quit pressed
                print "quitting"    
                global quitting   #a global variable
                quitting = True
                return    #exit thread

gamepad = threading.Thread(target = gamepad)    #simplify name
gamepad.start()   #start thread

while True:   #BrickPi loop is in main thread
    BrickPiUpdateValues()   #update to run motors
    if quitting == True:
        sys.exit()    #quit
~~~~
