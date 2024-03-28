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
 We used the neopixel on the board along with the RGB led to get a rainbow pattern. I was able to do both of these and used the code from the library.
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





### Wiring
![Capture](https://github.com/ldengel3718/Engr3/assets/143533539/26ac5589-7d16-4440-88b8-915730de3213)

### Reflection
This assignment wasn't very hard. The wiring was quite simple, but I did need a little help getting back in the groove with the coding. I struggled with the while loop but got some help and figured it out. I learned how to write while loops and I also learned how to use git hub for documentation. I feel like Google Sites is easier for documentation and would advise that in the future.



## CircuitPython_Servo

### Description & Code
This assignment was about getting a servo to work with Circuit Python. We used code to move the motor and then included buttons. One button made the servo go the the right and the other to the left.
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


https://drive.google.com/file/d/19kU0gMM48Dn6-dehD8EDgt95eNHNegF_/view?usp=sharing


### Wiring
![buttonServo](https://github.com/ldengel3718/Engr3/assets/143533539/d74164fb-1572-4266-9665-93b52ee7c56f)

### Reflection

I had lots of trouble on starting this assignment and it took me a while to finish the code for the button. I learned to use angles for my servo and how to use a button. Something that would be helpful would be an outline for the code to get us started.




## CircuitPython_Distance

### Description & Code
This assignment told us how far away something was from the Ultrasonic distance sensor and it also lit up the Neopixel under the board. If there was nothing in range of the distance sensor it would print "not in range". The neopixel lit up different colors based on the distance of the object from the sensor.
```python
import time
import board
import adafruit_hcsr04
sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D5, echo_pin=board.D6) #Gets distance here
cm = 0
while True:
    try:
        cm = sonar.distance
        print((cm)) #variable printed here
    except RuntimeError:
        print("Not in range") #If it doesn't read anything, print "Not in Range"
    time.sleep(0.1)
```

### Evidence

https://drive.google.com/file/d/1aiwX1ZQLRiEpCKVNxv7e4bX0L4c7XX4-/view?usp=sharing

### Wiring
![Screenshot 2023-09-25 112807](https://github.com/ldengel3718/Engr3/assets/143533539/96bc16a5-da41-4627-8d6f-72ba9ffcd1f3)
### Reflection

This assignment was actually easier for me than the previous two. I had gotten back in the groove for coding and wiring. I did have some trouble with the wiring and I also didn't have matching pins. I learned how helpful importing things is and how it makes everything easier. I advise taking your time on this assignment and making sure your code is write, writing the code is the harder part.


## Motor Contol

### Description & Code
This assignment made the motor rotate using a potentiometer. We used batteries as well on this assignment and it took me a second to re-learn how to use them. This took me three classes and the code isn't too complicated.
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
https://drive.google.com/file/d/1tmlIlOe0C0YODo9KltpYBuVw_AmxRr4T/view?usp=sharing

### Wiring
![image](https://github.com/ldengel3718/Engr3/assets/143533539/df1de06d-90dc-4c47-94f2-5af0c8fdef59)

### Reflection
This assignment was fun as there wasn't too much code and I like using motors. I didn't really struggle with much but the potentiometer was definitely the hardest part. I learned how to mix the two components together and it was a fun assignment. I would advise starting with your wiring so you know which pins to use.
## Photointerrupter

### Description & Code
This assignment told us how many times something had interrupted the photo interrupter in 4 seconds. It would count how many times it was interrupted in the interval and print it. If nothing it would just print 0.
```python
from digitalio import DigitalInOut, Direction, Pull
import time
import board
#pins 
interrupter = DigitalInOut(board.D7)
interrupter.direction = Direction.INPUT
interrupter.pull = Pull.UP

counter = 0

photo = False #
state = False #   

max = 4 #sets the interval
start = time.time() 
while True:
    photo = interrupter.value
    if the photo and not state: #if not interrupted in the interval, increase the counter by 1
            counter += 1
    state = photo

    remaining = max - time.time()

    if remaining <= 0:
        print("Interrupts:", str(counter))
        max = time.time() + 4
        counter = 0
```

### Evidence

https://drive.google.com/file/d/1muSV-7Zl1t76_cL3m35tonO5IzkEUjEB/view?usp=sharing

### Wiring
![image](https://github.com/ldengel3718/Engr3/assets/143533539/29f96111-8f25-44a9-afae-369c6c195797)

### Reflection
This assignment was a lot harder than the previous few. I struggled with the counter and it took a while for me to understand it. I did also understand and know how to use it which should be helpful in the future. I would advise trying to understand what the code entails before trying to write it and make an outline. 
## Hangar

### Assignment Description

The goal of this assignment was to make a hangar based on a few photos with dimensions given to us. This was a very simple design and it incorporated skills we used from last year into this such as extruding.
### Evidence

![image](https://github.com/ldengel3718/Engr3/assets/143533539/57d98ecd-977b-41cd-9e8b-1afc9d87cfaf)
![Hangar](https://github.com/ldengel3718/Engr3/assets/143533539/f24c3fa0-4cf2-433a-81ee-a835c5fe1b37)
![Fronnt](https://github.com/ldengel3718/Engr3/assets/143533539/a852f46e-9c06-410c-a71b-c71d12b22513)

### Part Link 

[[Create a link to your Onshape document](https://cvilleschools.onshape.com/documents/003e413cee57f7ccccaa15c2/w/ea71050bb283bf3bf088c96c/e/c85ae532263d3b551e1795d0?renderMode=0&uiState=62d9b9d7883c4f335ec42021). Don't forget to turn on link sharing in your Onshape document so that others can see it. ](https://cvilleschools.onshape.com/documents/caa6fd0b434cff95e6afe1d0/w/0b41de6fe5d46a783dfeba24/e/8b3b7df5f44e32f7ea277424)
### Reflection

This was our first assignment of the year so it took a while for me to become comfortable with Onshape again which was challenging. I re-learned how to use Onshape and how to use sketch fillets as well. I don't have much advice on this one though. Maybe don't use sketch fillets since its honestly harder than a normal fillet.
&nbsp;

## Swing_Arm 

### Assignment Description

We were tasked to create a swing arm based on an image and then we had to change the dimensions around which changed the look of the entire thing. There were many different angles and sketches given to us and then we had to change the dimensions to change the entire look of it. If the initial sketch was off than your second wrong would end up horribly wrong.
### Evidence

![image](https://github.com/ldengel3718/Engr3/assets/143533539/ee66d738-7639-41cd-a8f9-216b9382be3c)
![image](https://github.com/ldengel3718/Engr3/assets/143533539/56791c59-4843-447b-ad3c-5bc2f4e364e6)
![image](https://github.com/ldengel3718/Engr3/assets/143533539/f327fe2d-9164-4009-90ad-8c230e0d605a)

### Part Link 

https://cvilleschools.onshape.com/documents/5046251d5ea4d5ca425fbe3f/w/f0030bb96375f589834cb015/e/84b4033fe2b67420fd258d65
### Reflection

The first part of this project was not too bad but changing the dimensions led to many problems for me. It created a few errors with the fillets and somehow created new parts. After getting this fixed up it looked great. I learned how to use the parallel tool. I would advise paying attention to your initial sketch as changing the dimensions really screwed mine up.
&nbsp;
## Onshape Certification Part 1  

### Assignment Description

This was the first part of our onshape certification to prep for the test. In this we were asked to make a design on Onshape using photos. 
### Evidence
![Screenshot 2024-03-28 110708](https://github.com/ldengel3718/Engr3/assets/143533539/12dd4f38-8313-405a-8e15-ea2908d5ff87)
![Screenshot 2024-03-28 110828](https://github.com/ldengel3718/Engr3/assets/143533539/44342171-b50a-432a-8558-1bf3657fd3d3)


### Part Link 
https://cvilleschools.onshape.com/documents/92b147b8d7ff3b9049249335/w/8a123f3111920f108ef0cdcc/e/900544e70849e1d97fae8455

### Reflection

This part was somewhat challenging but I got good help from Ryan and Mr. Miller. I struggled with cutting into the part at the end as it was definantly the hardest part of this project. I liked this project a lot as it was challenging but also fun and simple. nbsp;
