# CircuitPython
This repository will actually serve as an aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_LCD](#CircuitPython_LCD)
  * [Photointerrupter](#Photointerrupter)
* [Motor Control](#Motor_control)
 * [Hangar](#Hangar)
 * [Swing_Arm](#Swing_Arm)


## Hello_CircuitPython

### Description & Code
This code made a small LED light up and change colors.
Here's how you make code look like code:

```python
# SPDX-FileCopyrightText: 2022 ladyada for Adafruit Industries
# SPDX-License-Identifier: MIT

import time
import board
from rainbowio import colorwheel
import neopixel

NUMPIXELS = 1 # Update this to match the number of LEDs.
SPEED = 0.01  # Increase to slow down the rainbow. Decrease to speed it up.
BRIGHTNESS = 0.5  # A number between 0.0 and 1.0, where 0.0 is off, and 1.0 is max.
PIN = board.NEOPIXEL  # This is the default pin on the 5x5 NeoPixel Grid BFF.

pixels = neopixel.NeoPixel(PIN, NUMPIXELS, brightness=BRIGHTNESS, auto_write=False)


def rainbow_cycle(wait):
    for color in range(255):
        for pixel in range(len(pixels)):  # pylint: disable=consider-using-enumerate
            pixel_index = (pixel * 256 // len(pixels)) + color * 5
            pixels[pixel] = colorwheel(pixel_index & 255)
        pixels.show()
        time.sleep(wait)


while True:
    rainbow_cycle(SPEED)
```


### Evidence


<img src="https://learn.adafruit.com/system/assets/assets/000/029/993/original/adafruit_products_2945limorgif_BIG.gif?1453742429" style="width:200px;">



Image credit goes to Martin Ku



### Wiring
![Capture](https://github.com/ldengel3718/Engr3/assets/143533539/26ac5589-7d16-4440-88b8-915730de3213)

### Reflection
This assignment wasn't very hard. The wireing was quite simple, but I did need a little help getting back in the groove with the coding.



## CircuitPython_Servo

### Description & Code
This assignment was about getting a servo to work with circuit python. We used code to move the motor and then included buttons.
```python
# # SPDX-FileCopyrightText: 2018 Kattni Rembor for Adafruit Industries
#
# SPDX-License-Identifier: MIT

"""CircuitPython Essentials Servo standard servo example"""
import time
import board
import pwmio
from adafruit_motor import servo
from digitalio import DigitalInOut, Direction, Pull


# create a PWMOut object on Pin A2.


pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

button = DigitalInOut(board.D2)
button.direction = Direction.INPUT
button.pull = Pull.DOWN

button2 = DigitalInOut(board.D5)
button2.direction = Direction.INPUT
button2.pull = Pull.DOWN


current_angle = 90  # Initialize the angle
my_servo.angle=current_angle

while True:
    if button.value:  # Button is pressed (remember, we're assuming it's pull-down)
        print(current_angle)
        current_angle = current_angle + 10
        current_angle = max(0, min(180, current_angle))
        my_servo.angle = current_angle  # Set the new angle

    if button2.value:  # Button is pressed (remember, we're assuming it's pull-down)
        print(current_angle)
        current_angle = current_angle - 10
        current_angle = max(0, min(180, current_angle))
        my_servo.angle = current_angle  # Set the new angle
    time.sleep(.
    01)  # Small delay to avoid excessive checking
```

### Evidence
Pictures / Gifs of your work should go here.  You need to communicate what your thing does.
Remember you can insert pictures using Markdown or HTML



![servo-sweeping](https://github.com/ldengel3718/Engr3/assets/143533539/e7bc0941-81fa-479f-aa34-4f226bd29ee9)
Image credit goes to adafruit.com
### Wiring
![buttonServo](https://github.com/ldengel3718/Engr3/assets/143533539/d74164fb-1572-4266-9665-93b52ee7c56f)

### Reflection

This assignment was a fun and challenging way. I had trouble starting, but I got some help from Josh, Ryan and Mr. Helmstetter. This helped me figure out some things and finish the assignment.





## CircuitPython_Distance

### Description & Code
This assignment told us how far away something was from the Ultrasonic distance sensor. it also lit up the Neopixel under the board.
```python
import time
import board
import adafruit_hcsr04
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6)
cm = 0
while True:
    try:
        cm = sonar.distance
        print((cm))
    except RuntimeError:
        print("Not in range")
    time.sleep(0.1)
```

### Evidence

Pictures / GIFs of your work should go here.  You need to communicate what your thing does.
![image](https://github.com/ldengel3718/Engr3/assets/143533539/216b327e-39dd-4b89-bef3-953974935521)
Image credit goes to the Adafruit Website

### Wiring
![Screenshot 2023-09-25 112807](https://github.com/ldengel3718/Engr3/assets/143533539/96bc16a5-da41-4627-8d6f-72ba9ffcd1f3)
### Reflection

This wasn't an easy assignment at all, I had trouble starting this assignment and struggled with the code. I didn't have too many problems with the wiring though.



## Motor Contol

### Description & Code
This assignment made the motor roatate using a potentiometer. 
```python
import time 
import board
from analogio import AnalogIn
import pwmio
from digitalio import DigitalInOut

#pins
potentiometerpin = AnalogIn(board.A0)
motorpin = pwmio.PWMOut(board.D3)

#prints the potentiometer value then writes it to the motor
while True:
    print(potentiometerpin.value)
    time.sleep(0.1)
    motorpin.duty_cycle = potentiometerpin.value
```

### Evidence
![nema17_rpi_demo](https://github.com/ldengel3718/Engr3/assets/143533539/8dcf4d22-53ac-4ae0-8cab-4c5e88654c56)
Image credit goes to Joshua Hrisco

### Wiring
![image](https://github.com/ldengel3718/Engr3/assets/143533539/df1de06d-90dc-4c47-94f2-5af0c8fdef59)

### Reflection
This assignment was not very hard and there wasnt too much code. The wiring was simple and I liked this assignment more than the previous.

## Photointerrupter

### Description & Code
This assignment told us how many times something had interrupted the photo interrupter in 4 seconds.
```python
from digitalio import DigitalInOut, Direction, Pull
import time
import board

interrupter = DigitalInOut(board.D7)
interrupter.direction = Direction.INPUT
interrupter.pull = Pull.UP

counter = 0

photo = False
state = False

max = 4
start = time.time()
while True:
    photo = interrupter.value
    if photo and not state:
            counter += 1
    state = photo

    remaining = max - time.time()

    if remaining <= 0:
        print("Interrupts:", str(counter))
        max = time.time() + 4
        counter = 0
```

### Evidence
![image](https://github.com/ldengel3718/Engr3/assets/143533539/519fabad-df20-4061-bdf9-82165b8a7542)
Image credit goes to Adafruit.com

### Wiring
![image](https://github.com/ldengel3718/Engr3/assets/143533539/29f96111-8f25-44a9-afae-369c6c195797)

### Reflection
This assignment was a little bit more challenging, but it was cool to use a photo interrupter. The wiring was very easy, but the code was a little harder.
## Hangar

### Assignment Description

We had to make a hangar based on a few photos with dimensions given to us.
### Evidence

![image](https://github.com/ldengel3718/Engr3/assets/143533539/57d98ecd-977b-41cd-9e8b-1afc9d87cfaf)
![Hangar](https://github.com/ldengel3718/Engr3/assets/143533539/f24c3fa0-4cf2-433a-81ee-a835c5fe1b37)
![Fronnt](https://github.com/ldengel3718/Engr3/assets/143533539/a852f46e-9c06-410c-a71b-c71d12b22513)

### Part Link 

[[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. ](https://cvilleschools.onshape.com/documents/caa6fd0b434cff95e6afe1d0/w/0b41de6fe5d46a783dfeba24/e/8b3b7df5f44e32f7ea277424)
### Reflection

This was a simple start to Onshape for this year which was nice. It was also cool to use sketch fillets for the first time.
&nbsp;

## Swing_Arm 

### Assignment Description

We were tasked to create a swing arm based on an image. Then we had to change the dimensions around which changed the look of the entire thing.
### Evidence

![image](https://github.com/ldengel3718/Engr3/assets/143533539/ee66d738-7639-41cd-a8f9-216b9382be3c)
![image](https://github.com/ldengel3718/Engr3/assets/143533539/56791c59-4843-447b-ad3c-5bc2f4e364e6)
![image](https://github.com/ldengel3718/Engr3/assets/143533539/f327fe2d-9164-4009-90ad-8c230e0d605a)

### Part Link 

[Create a link to your Onshape document]([https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021](https://cvilleschools.onshape.com/documents/5046251d5ea4d5ca425fbe3f/w/f0030bb96375f589834cb015/e/84b4033fe2b67420fd258d65)). Don't forget to turn on link sharing in your Onshape document so that others can see it. 

### Reflection

The first part of this project was not too bad but changing the dimensions led to many problems for me. It created a few errors with the fillets and somehow created new parts. After getting this fixed up it looked great.
&nbsp;
