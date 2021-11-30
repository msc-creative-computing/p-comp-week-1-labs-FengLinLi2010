## Knob machine arm
## How to use
Turn the knob, servo will rotate to the appropriate Angle
 ![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Lab3/servocircuit.png)
 ![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Lab3/servo.jpg)
## Code
```
#include <Servo.h>

Servo myservo; 

int val;    

void setup() {
  myservo.attach(9); 
}

void loop() {
  val = analogRead(A3);
  val = map(val, 0, 1023, 0, 180);   
  myservo.write(val);                
}
