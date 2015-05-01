
//notice should download the MsTimer2 library from arduino website
#include <Servo.h>

#include <MsTimer2.h>

Servo myServo;
int const potPin=A0;
int potVal;
int angle;
int counter=0;
int pos = 0;
bool moving = false;

void setup() {
  

 angle=0;
 myServo.attach(9);
 Serial.begin(9600);
 myServo.write(0);
delay(15);


  MsTimer2::set(8000, timerIsr); 
  MsTimer2::start();
}

void loop() {
  

  angle = myServo.read();
  delay(15);
  if(angle == 180)  {
    myServo.write(0);
    Serial.println("Set to 0");
  }
  
  if(moving) {
    for(pos = 0; pos <= 180; pos += 5) // goes from 0 degrees to 180 degrees 
      {                                  // in steps of 1 degree 
          Serial.print(", angle: ");
      Serial.print(pos);
        myServo.write(pos);              // tell servo to go to position in variable 'pos' 
        delay(15);                       // waits 15ms for the servo to reach the position 
      } 
      for(pos = 180; pos>=0; pos-=5)     // goes from 180 degrees to 0 degrees 
      { 
      Serial.print(", angle: ");
      Serial.print(pos);      
        myServo.write(pos);              // tell servo to go to position in variable 'pos' 
        delay(15);                       // waits 15ms for the servo to reach the position 
      } 
      moving = false;
  }

}
void timerIsr()
{
  
  counter=counter+1;
  
  if(counter % 10 ==0){



    moving = true;

  }

}
