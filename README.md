# omnomcat
omnomcat is an automated cat feeder controlled by an arduino

//set a timer to call the timerIsr function every 8 seconds and every 10 times timerIsr is called, it will turn the degree of servo to 5 degrees. 
#include <Servo.h>
//#include <TimerOne.h>
#include <MsTimer2.h>

Servo myServo;
int const potPin=A0;
int potVal;
int angle;
int counter=0;

void setup() {
  // put your setup code here, to run once:

 angle=0;
 myServo.attach(3);
 Serial.begin(9600);
 myServo.write(0);
delay(15);
//  Timer1.initialize(1000000);
//Timer1.attachInterrupt( timerIsr);
  MsTimer2::set(8000, timerIsr); 
  MsTimer2::start();
}

void loop() {
  // put your main code here, to run repeatedly:
 //Timer1.initialize(8000000);
 //Timer1.attachInterrupt( timerIsr );
//potVal=analogRead(potPin);
//Serial.print("potVal: ");
//Serial.print(potVal);
//angle=map(potVal,0,1023,0,179);
//Serial.print(", angle: ");
//Serial.print(angle);
//myServo.write(angle);
//delay(15);
  /*
  int potPin;
  potPin=500;
  potPin=-potPin;
potVal=analogRead(potPin);
Serial.print("potVal: ");
Serial.print(potVal);
angle=map(potVal,0,1023,0,179);
Serial.print(", angle: ");
Serial.print(angle);
myServo.write(angle);
*/

}
void timerIsr()
{
  
  counter=counter+1;
  
  if(counter % 10 ==0){
  
angle=angle+5;

if(angle >= 180)
  angle = 0;
Serial.print(", angle: ");

Serial.print(angle);
//angle=angle+5;
myServo.write(angle);
//delay(15);
    //myServo.attach(9);
    //Serial.begin(9600);
  }
}
