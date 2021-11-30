# Battle in future 
## Story background
 Throughout human history, conflict between individuals has always been inevitable. When problem cannot be solved, people will duel with others.
 The way how people duel has developed with the development of technology.
 The duels were also very varied. There are simple, casual rock-paper-scissors, and also pistols that would kill someone with the flick of the trigger.
 ![pic](http://5b0988e595225.cdn.sohucs.com/images/20171101/cb094a823ed54df78069933c97444ca4.jpeg)
## How future people duel?
 In the coming decades, humanity will experience a new ice age due climate change. 
 After a  globally sharp drop of polulation, The rest of humanity kept flocking to cities of limited capacity.
 In order to save resources in the extreme cold, the city decided to duel to choose one of the two men for shelter.
 And in this particular case, temperature became the criterion for winning a duel, because people with high body temperatures have a better chance of surviving.
 
 ![pic](https://www.pockettactics.com/wp-content/uploads/2021/05/frostpunk-mobile-release-date-580x334.jpg)
## How to use
 The two duelers put their hands on the sensor, after the judge pressed the start switch, the colorful light of the side with higher temperature will lighted, which symbolized his victory.
 ![pic](https://raw.githubusercontent.com/msc-creative-computing/p-comp-labs-FengLinLi2010/main/Week_01/circuit.png)
 ## Code
```C++
  int Switchstate = 0;

  int Temperature1 = 0;

  int Temperature2 = 0;

  void setup()
{
  Serial.begin(9600);
  
  pinMode(2, INPUT);
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(13, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(12, OUTPUT);
}

void loop()
{
  Switchstate = digitalRead(2); 
  Temperature1 = analogRead(A0); // temperature of player1
  Temperature2 = analogRead(A1); //temperature of player2

  digitalWrite(13, HIGH); // This is led for check is the circuit work
  
  if (Switchstate == HIGH) {
    
    Serial.print(Temperature1);
    Serial.print(' ');
    Serial.println(Temperature2);
        if (Temperature1 > Temperature2) {
      digitalWrite(3, HIGH);
      delay(1000);
      digitalWrite(4, HIGH);
      delay(1000); 
      digitalWrite(5, HIGH);
      delay(1000); 
      digitalWrite(6, HIGH);
      delay(1000); 
      digitalWrite(7, HIGH);
      delay(1000); 
      digitalWrite(3, LOW);
      digitalWrite(4, LOW);
      digitalWrite(5, LOW);
      digitalWrite(6, LOW);
      digitalWrite(7, LOW);
    } 
    else {
      Serial.println(Temperature2);//Just check dose the else clause works
      digitalWrite(8, HIGH);
      delay(1000); 
      digitalWrite(9, HIGH);
      delay(1000); 
      digitalWrite(10, HIGH);
      delay(1000); 
      digitalWrite(11, HIGH);
      delay(1000); 
      digitalWrite(12, HIGH);
      delay(1000);
      digitalWrite(8, LOW);
      digitalWrite(9, LOW);
      digitalWrite(10, LOW);
      digitalWrite(11, LOW);
      digitalWrite(12, LOW);
    }
    }  
    }

