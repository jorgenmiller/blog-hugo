+++
date = "2017-09-16"
title = "Wifi Robots"

+++

The last robot I made was the [Offroad Vehicle](https://jorgenmiller.github.io/blog/lego-offroad-vehicle-with-brickpi/). The biggest problem it had was the way it was controlled. I was using a logitech gamepad that had a USB plug. The wired connection limited the usuability, range, and was just annoying. Wireless Logitech gamepads are available for purchase, but why buy something when you have a mobile device? A phone can communicate with a Raspberry Pi over wifi to be used as a controller. This allows a large range, customizable controls, and the option to include a camera to drive your robot without line-of-sight.

I used [Sockets](https://socket.io/) to communicate between my iPod and the BrickPi. It is traditionally used to send information between a client and server for things like chat rooms, so it will work great. For a robot and controller, the BrickPi Robot is the server. Whatever device controls it is the client. The client will use a website to send information to the BrickPi. I used [Surge](http://surge.sh/) to make a quick website.

On the website, a bit of html can make a button, and some javascript will send it to the BrickPi. The BrickPi can use python to receive commands and control motors.

For the front end, this should be included in the html.

~~~~html
<script src="https://cdnjs.cloudflare.com/ajax/libs/socket.io/1.7.3/socket.io.min.js"></script>
<script src="<js file>"></script>
~~~~

The javascript should specify what IP address it should send to, and what port.

~~~~javascript
var socket = io.connect("<IP address>:<port>")
~~~~

Using an IP address for local connections only will ensure that no one else can control your Pi. Next, a message on an event should be sent to the pi which can be understood easily.

~~~~javascript
socket.emit("button", "motor A", "200");
~~~~

This can be attached to a button to send when the button is clicked. The python will receive the message using `@SocketIO(app)`. Here is a full back end that can receive commands for any motor. It also has a message for when a client connects.

~~~~python
from flask import Flask, render_template
from flask_socketio import SocketIO
from BrickPi import *

BrickPiSetup()
BrickPi.MotorEnable[PORT_A] = 1
BrickPi.MotorEnable[PORT_B] = 1
BrickPi.MotorEnable[PORT_C] = 1
BrickPi.MotorEnable[PORT_D] = 1

app = Flask(__name__)
socketio = SocketIO(app)

@socketio.on("message")
def handle_message(message):
    print("received message: " + message)

@socketio.on("button")
def handle_button(motor, speed):
    print(str(motor) + ": " + str(speed))
    if motor == "motor A":
        BrickPi.MotorSpeed[PORT_A] = int(speed)
    elif motor == "motor B":
            BrickPi.MotorSpeed[PORT_B] = int(speed)
    elif motor == "motor C":
            BrickPi.MotorSpeed[PORT_C] = int(speed)
    elif motor == "motor D":
            BrickPi.MotorSpeed[PORT_D] = int(speed)
    BrickPiUpdateValues()
    BrickPiUpdateValues()

if __name__ == "__main__":
    socketio.run(app,host= "0.0.0.0")
~~~~

With a complete front end and back end, The pi can be controlled from a mobile device. It can actually be controlled from any device on your wifi.

Check out [socket.io](https://socket.io/) for more help and to learn how to use sockets to their full extent!
