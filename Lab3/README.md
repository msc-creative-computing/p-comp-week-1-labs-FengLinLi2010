## Knob machine arm
## How to use
Turn the knob, servo will rotate to the appropriate Angle
 ![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Lab3/servo.png)
## Code
```
#include <Servo.h>

Servo myservo; 

int potpin = 0;  // analog pin used to connect the potentiometer
int val;    

void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
}

void loop() {
  val = analogRead(potpin);            // reads the value of the potentiometer (value between 0 and 1023)
  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  myservo.write(val);                  // sets the servo position according to the scaled value
  delay(15);                           // waits for the servo to get there
}

