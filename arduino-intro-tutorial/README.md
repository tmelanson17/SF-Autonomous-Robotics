# Instructions for Moisture Sensing Robot, Part I

## Set up the Arduino

- Plug Arduino into computer using the USB cable (make sure to bring a converter if you have a MacBook)
- Open Arduino IDE
- File -> Examples -> 01. Basics -> Blink
- Tools -> Board -> Arduino Nano
- Tools -> Processor -> ATMega328P (Old Bootloader)
- Press “->” button to upload code
- Arduino Nano “L” LED should be blinking, on 1 second, off 1 second.

## Set up the Moisture Sensor:

- Using jumper cables, attach :
    - 5V Arduino -> VCC on sensor
    - GND Arduino -> GND on sensor
    - A0 Arduino -> A0 on sensor
- File -> Examples -> 01. Basics -> AnalogReadSerial
-  Make sure  “int sensorValue = analogRead(A0);” in loop (value in parentheses must correspond to pin you connected the A0 sensor pin to)
- Press “->” button to upload code
- Press the button with the magnifying glass on top right (known as the Serial Monitor) to open the print output
- You should see a continuous stream of numbers (likely 1023), one per line
    - If you don’t see anything, or you see random characters, it is likely the serial monitors “baud rate” (aka the communication frequency) is set incorrectly. Make sure it is at 9600 baud (see drop-down menu on the bottom right)
- If you clench the sensor with your fingers, you will see the number go down slightly
- Fill a glass with water and place the sensor (NOT the electronics side) in the water. You should see the count drop drastically

## Program Your First Robot!

- Take a look at the “Blink” code. You should see two sections, one labeled “setup” and “loop”. For those new to programming, these are *functions*, which are sections of code designed to do a specific and unique task.
    - In this case, “setup” is created to initialize, or set up, the variables used by the Arduino, and “loop” is the function that the Arduino calls repeatedly.
    - Additionally, within these functions, you will see “pinMode” in setup and “digitalWrite” and “delay” in loop. These are *calls* to other functions, defined in other accessible code files called *libraries*.
    - Functions have a specific syntax, usually either a lowercase first letter of the first word followed by uppercase first letter for each subsequent word (camelCase) or all lowercase with underscores in between (snake_case). It is up to you what you choose, as long as you are consistent both in your code and with code of people you are working with. 
    - Specifically, I will talk more about “pinMode” and “digitalWrite”. 
        - “pinMode” is designed to set up an Arduino pin for either input or output. The number of the pin, as well as whether the pin should be input or output, are supplied to the function in the form of *arguments* (the words within the parentheses). Generally speaking, arguments are provided inside the function parentheses and are separated by commas.
        - “digitalWrite” will write a digital value (or *signal*) to the pin number provided, with a value determining whether the signal is *high* (i.e. 1 or high voltage) or *low* (i.e. 0 or low voltage). 
        - You’ll notice that the arguments in these functions are not directly provided as numbers, but as words in capital letters. These words represent values and are called *variables*. Because these values are never changed over the course of the program, the variables are known as *constants*.
        - In this instance, the variables are just stand-ins that are replaced with numbers before the code even runs and are there for readability. These are known as *macros*, and are denoted by their all-uppercase format.
- Pull up the “AnalogReadSerial” window. Copy the “pinMode” call from the Blink code into the setup function of AnalogReadSerial
- Now we will create an “if” statement, which reads like this:
```
if (condition) {
// do something
} else {
// do something else
}
```
- This stands for “If condition is true, do something, otherwise do something else”.
	- Copy the above code into the “loop” function. Directly below “// do something”, write `digitalWrite(LED_BUILTIN, HIGH);`. Directly below “// do something else”, write `digitalWrite(LED_BUILTIN, LOW);`.
- The double slashes are what we call *comments*. These provide plain English descriptions of what a section of code does. 
        - To be more clear to readers of our code, we will change “do something” to “Turn on the LED” and “do something else” to “Turn off the LED”.
- Now we need to set the condition variable. This requires two things:
        - Declaring the type of the variable (in this case, `int`) before the variable name. Note this only happens ONCE for each variable.
        - Setting the value of the variable by using “=“, followed by a value
- In the line directly above the if statement, write `int threshold = <insert a good threshold here :)>;`. This threshold will determine the distinction between “moist” and “dry”.
- Replace “condition” with “sensorValue < threshold”. This means that `sensorValue` (declared earlier in the loop) must be *less than* the threshold variable for the condition to hold. For greater than, you would use “>” instead.
- Press the Upload button. The “L” LED should now turn off in the air, but turn on  when the sensor is dipped in a moist environment (i.e. water).
- Congrats, you built your first robot!

