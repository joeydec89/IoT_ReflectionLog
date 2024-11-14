# IoT_ReflectionLog
Reflections for assignment sand labs


# LAB1 

import RPi.GPIO as GPIO # General Purpose Input/Output library
import time

## Set up the GPIO mode
GPIO.setmode(GPIO.BCM)

## Define the GPIO pins for each LED
led_pins = [2, 3, 4]

## Initialize GPIO pins as outputs
for pin in led_pins:
    GPIO.setup(pin, GPIO.OUT)

try:
    while True: # forever until CTRL-C
        # get the current time and seconds
        current_time = time.localtime()
        seconds = current_time.tm_sec

        countup = seconds % 8

        # convert seconds to binary string
        binary_seconds = format(seconds, '03b')

        # display each binary digit by turning LEDs on or off
        for i in range(3):
            GPIO.output(led_pins[i], int(binary_seconds[i]))

        # wait one second before resuming the program
        time.sleep(1)

finally: # when an error occurs, don't leave the try block without doing this
    # Clean up GPIO on program exit
    GPIO.cleanup()
