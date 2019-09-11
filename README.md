# lab3 7-segment

# GROUP of 2

# Lab equipment
	raspberry pi 	1
	resistor 1k	7
	NPN Transistor	7
	7-segment 	1

# Theory of operation
Let’s start by understanding how a single 7-segment display works. 7-segmentThe 7-segment display, as its name implies, is comprised of 7 individually lightable LEDs, labeled A, B, C, D, E, F, and G. There is also a decimal point labeled DP. Each segment is an LED. Recall that an LED has an anode and a cathode. The polarity matters for an LED; the anode voltage must be positive relative to the cathode for the LED to be lit. If the cathode is positive with respect to the anode, the segment is not lit.
[http://cs107e.github.io/labs/lab2/]

On the 7-segment displays we are using, the cathodes (ground) are connected to NPN transistor which are controlled by GPIO and more 4 GPIO to select digit for display. If all four digit pin have power at the dame time, all 7-segment will have the same display. In other to display different, you need to select the specific digit.

# Wire up display breadboard

## NPN Transistor 2N3904
NPN Transistor act like a switch. If it has the high signal on the base pin, it will allow some current to flow through between collector and emitter pin.
![npn](https://user-images.githubusercontent.com/40221875/64620838-cf0ee000-d40e-11e9-8b3c-69cbe5ed92da.jpg)

## 4-digits 7-segment common anode  
![7s](https://user-images.githubusercontent.com/40221875/64621239-89064c00-d40f-11e9-9a00-dd89c79a2a18.PNG)

## Schcematic 
![circuit](https://user-images.githubusercontent.com/40221875/64620110-7db22100-d40d-11e9-8fb6-bd7f741f76a7.PNG)

# Example 
```
import RPi.GPIO as GPIO
import time
a = 19
b = 21
c = 23 
d = 29
e = 31
f = 33
g = 35
led_pin = 	[a, b, c, d, e, f, g]
dig_pin = 	[ 32, 36, 38, 40] 
segment = {
	0: [a, b, c, d, e, f], 
	1: [b, c], 
	2: [a, b, g, e, d], 
	3: [a, b, g, c, d],
	4: [f, b, g, c],
	5: [a, f, g, c, d]
}
GPIO.setmode(GPIO.BOARD)
for pin in dig_pin:
	GPIO.setup(pin, GPIO.OUT)
	GPIO.output(pin, False)
for pin in led_pin:
	GPIO.setup(pin, GPIO.OUT)
	GPIO.output(pin, False)

num = 3
try:
	while True:
		for digi in dig_pin[::-1]:
			for pin in dig_pin:
				GPIO.output(pin, False)
			GPIO.output(digi, True)
				
			for pin in led_pin:
				GPIO.output(pin, False)
			for on in segment[num]:
				GPIO.output(on, True)
			time.sleep(0.5)
except KeyboardInterrupt:
        GPIO.cleanup()
```

**Exercise**
1. Show number 9876, all four digits at the same time.
![20190910_211332](https://user-images.githubusercontent.com/40221875/64621546-0f229280-d410-11e9-9672-5d0287bd9e23.jpg)

