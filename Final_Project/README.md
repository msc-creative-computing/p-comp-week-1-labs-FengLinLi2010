# Social Media Simulator
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/fog.jpg)
## Background and main Idea
### Background research
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/95320b49fcede2d74fee4f727f71c3b.png)
### Inspiration from Cyborg manifesto
"It is certainly true that postmodernist strategies, like my cyborg myth, subvert myriad organic wholes (for example, the poem, the primitive culture, the biological organism).
-A Cyborg Manifesto"
The author's statement inspired me. In this state, is language also abandoned? Maybe you have a Cyborg way of communicating vague ideas that have no boundaries? Such as smoke
### Main idea
TO SIMULAT HOW PUBLIC OPINION PRODUCED WITH A HYBRID MEDIUM
## SPECIFIC CONCEPT
### Thinking of meduim
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/24565785544df1b809fb4fbf23e1e7e.png)
for this step, I research several way to be the medium of the installation
* bubble Different bubbles represent different ideas, and they react with each other in the container
* fog Using the colors of the fog to represent different ideas, they will merge in the container
* screen Make a video game to demonstrate this
Finally I decided to use fog as a medium. I think it would be really interesting to see how different colors of fog react to each other
### Sketch
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/bc8b018a56c399de4f35246e5530a94.png)
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/c6fbf6dd4bb8290ec1865aa949fd241.png)
It consists of an interactive interface and a reaction device,the interactive interface will read your motion state, color; A button that allows you to interact, and a screen that outputs information. The reactor consists of aerosols in three primary colours, which operate for a period of time determined by the value of the colour sensor, and then a small fan feeds the mist into the reactor.
## Development
# challenge
the development of my project has a long period, here is three challenge I had faced.
* color sensor I used color sensors once many years ago, but for a completely different purpose. I rewrote the code and tested it repeatedly, but the results were always inaccurate. Finally, I decided to use the method described in the Case of Arduino Project Book to make a color sensor with photosensitive resistance.
* atomizer I first used a 5V atomizer, but it produced very little fog. I had to give up the low-powered nebulizer in favor of the super-powered one. I need a 24V power supply for this. Also, I needed to find a way to control the 24V circuit. I first tried Lab15 in Arduino Project Book, but its effect was not good. So I bought the electromagnetic relay and tested it. Finally, the high-power nebulators and the electromagnetic relay worked very well.
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/pics_storage/atomizer.jpg)
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/test_vide%26pics/relay.png)
* screen This is a brand new area for me. I took a long time to understand the library document and how to use this screen. here is some test  code
```
#include "U8glib.h"

U8GLIB_SSD1306_128X32 u8g(U8G_I2C_OPT_NONE);

void setup(void) {
  u8g.setFont(u8g_font_8x13B);
  u8g.setFontRefHeightText();
  u8g.setFontPosTop();
}

void loop(void) {
  int i;
  for (i = 1000; i >=0; i--) {
    u8g.firstPage();
    do {
      u8g.setColorIndex(1);
      u8g.drawStr(0, 0, "Hello World!");
      u8g.setPrintPos(0, 17);
      u8g.print(i);
      delay(300);
      u8g.setColorIndex(0);
    } while ( u8g.nextPage() );
    
  }
}
```
There is more test document, you can find it in my github.
# circuit design
![pic](https://github.com/msc-creative-computing/p-comp-labs-FengLinLi2010/blob/main/Final_Project/final_project_circuit.png)
This is made by [Tinkercad](https://www.tinkercad.com/things/kjAPQdotJcB),but it can't works in Tinkercad,because Tinkercad don't have many element I use. So I suggest you treat  it as a skech of circuit.
# Coding
As mentioned earlier, the screen lights up when PIR detects someone. At this point, if you press the button, the photoresistor will record your RGB values and transmit them to the electromagnetic relay. The electromagnetic relay will first turn on the fan, and then the three-color nebulizer will operate according to RGB values.
```
#include "U8glib.h"
U8GLIB_SSD1306_128X32 u8g(U8G_I2C_OPT_NONE);

int redvalue = 0;//红色数值
int redlight =10;//红色装置

int greenvalue = 0;//绿色数值
int greenlight = 11;//绿色装置

int bluevalue = 0;//蓝色数值
int bluelight = 12;//蓝色装置

int fan = 13;//设置风扇引脚
int pir = 9;//pir传感器
int button = 2;//开关

int redtime = 0;//红灯灯亮持续时长
int greentime = 0;//绿灯灯亮时长
int bluetime = 0;//蓝灯灯亮持续时长

int led = 3; 
int pirstate = 0;
void setup() {
  Serial.begin(9600);//开始串行监视器
  pinMode(button,INPUT);//设置按钮输入
  pinMode(pir,INPUT);
  
  pinMode(led,OUTPUT);
  pinMode(redlight,OUTPUT);
  pinMode(greenlight,OUTPUT);
  pinMode(bluelight,OUTPUT);
  pinMode(fan,OUTPUT);
  
  u8g.setFont(u8g_font_8x13B);
  u8g.setFontRefHeightText();
  u8g.setFontPosTop();
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:
  pirstate = digitalRead(pir);
  
if(pirstate == HIGH){
  digitalWrite(led,HIGH);
   
   u8g.firstPage();
    do {
      u8g.drawStr(0, 0, "Society  Simulator");
      u8g.setPrintPos(0, 17);
      
    } while ( u8g.nextPage() );

    int buttonval = digitalRead(button);
    if (buttonval == HIGH){//按下按钮
    digitalWrite(fan,HIGH);//打开风扇
    int redvalue = analogRead(A0);//读取RGB数值并开启装置
    int greenvalue = analogRead(A1);
    int bluevalue = analogRead(A2);

    
    Serial.print("red");
    Serial.println(redvalue);
    Serial.print("green");
    Serial.println(greenvalue);
    Serial.print("blue");
    Serial.println(bluevalue);
    int redtime = 10*redvalue;
    digitalWrite(redlight, HIGH);
    delay(redtime); 
    digitalWrite(redlight,LOW);
    int greentime = 10*greenvalue;
    digitalWrite(greenlight,HIGH); 
    delay(greentime);
    digitalWrite(greenlight,LOW);
    int bluetime = 10*bluevalue;
    digitalWrite(bluelight,HIGH);
    delay(bluetime);
    digitalWrite(bluelight,LOW);
    digitalWrite(fan,LOW);//关闭
    }
  if (buttonval == LOW){
    digitalWrite(bluelight,LOW);
    digitalWrite(greenlight,LOW);
    digitalWrite(redlight,LOW);
    digitalWrite(fan,LOW);
    }
  
  delay(3000);
  digitalWrite(3,LOW);
  u8g.firstPage();
    do {
      u8g.drawStr(0, 0, "");
      u8g.setPrintPos(0, 17);
      
    } while ( u8g.nextPage() );
  }
}
```
# make appearence and solding circuit


