# lab3

**Wire up display breadboard**
![alt text](https://github.com/SiWachirawich/lab3/issues/1#issue-491689194)

**Example**
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

