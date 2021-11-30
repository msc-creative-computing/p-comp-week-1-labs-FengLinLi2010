# Night guard
## Background
 There is a hallway in my house, and every night when I go out of the study to my bedroom, it feels dark. So I wanted to make a lamp that would start working at night and light up automatically when someone walked by.
 The duels were also very varied. There are simple, casual rock-paper-scissors, and also pistols that would kill someone with the flick of the trigger.
## composition
 PIR sensor, an LED for testing whether it is running (when night comes), an LED for lighting
 ![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Week_02/Sketch%20night%20%20light.jpg)
 <img src="https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Week_02/Sketch%20night%20%20light.jpg" style="transform:rotate(90deg);">
## How to use
 You don't have to do anything, and the Night Guard automatically kicks in as night falls. When someone stealthily passes in front of it, it lights up its lamp to illuminate the intruder.
 ![pic](https://raw.githubusercontent.com/msc-creative-computing/p-comp-labs-FengLinLi2010/main/Week_02/1634125090(1).png)
 [Tinkercad Link](https://www.tinkercad.com/embed/gDwkeGMcnxk?editbtn=1)
##Code
```
int photocellVal = 0; 
int Minlight = 400;
int LED = 13;
int ledstate = 0;
int PIR = 2;
int pirState = LOW;
int val = 0;
int LIGHT = 12;
//天黑的时候，灯亮（13引脚），开启运动检测，如果有人，就开12号引脚的灯，没人就关掉。
void setup()
{
  Serial.begin(9600);
  pinMode(LED,OUTPUT);
  pinMode(LIGHT,OUTPUT);
  pinMode(PIR,INPUT);
}

void loop(){
	photocellVal = analogRead(A0);						//光敏电阻值获取
  if (photocellVal < Minlight){		//光敏电阻值小于Minlight 并且 Led状态关闭
		Serial.println("night is coming");  
		digitalWrite(LED, HIGH);
		if(ledstate == 0){
			ledstate = 1;	
		}
		val = digitalRead(PIR); 						
		if (val == 1) {            
			digitalWrite(LIGHT, HIGH); 
			if (pirState == LOW) {      
				Serial.println("Motion detected!");      
				pirState = HIGH;
			}
  
		} 
		else {
			digitalWrite(LIGHT, LOW); 
			if (pirState == HIGH){      
				Serial.println("Motion ended!");      
				pirState = LOW;
			}
		} 
	}
    
   
	if (photocellVal > Minlight)
	{
		Serial.println("night is gone");
		digitalWrite(LED, LOW);
		if(ledstate == 1)
		{
			ledstate = 0;	
		}
	}  
 //Serial.println(digitalRead(PIR));
 // Serial.println(photocellVal);
}
  
