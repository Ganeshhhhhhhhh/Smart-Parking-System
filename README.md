#include <Servo.h> //includes the servo library

Servo myservo1;
Servo myservo2;


#define ir_enter 0
#define ir_exit  1

#define ir_car1 2
#define ir_car2 4
#define ir_car3 6
#define ir_car4 7

#define led_redE 8
#define led_red1 9
#define led_red2 10
#define led_red3 11
#define led_red 12

#define led_greenE A5
#define led_green1 A0
#define led_green2 A1
#define led_green3 A2
#define led_green A3

int S1=0, S2=0, S3=0,S4=0;
int slot = 4;  
void setup()
{
pinMode(ir_car1, INPUT);
pinMode(ir_car2, INPUT);
pinMode(ir_car3, INPUT);
pinMode(ir_car4, INPUT);
pinMode(led_redE,OUTPUT);
pinMode(led_greenE,OUTPUT);
pinMode(led_red1,OUTPUT);
pinMode(led_green1,OUTPUT);
pinMode(led_red2,OUTPUT);
pinMode(led_green2,OUTPUT);
pinMode(led_red3,OUTPUT);
pinMode(led_green3,OUTPUT);
pinMode(led_red,OUTPUT);
pinMode(led_green,OUTPUT);
pinMode(ir_enter, INPUT);
pinMode(ir_exit, INPUT);
myservo1.attach(3);
myservo2.attach(5);
myservo1.write(0);
myservo2.write(0);

int S1=digitalRead(ir_car1);
int S2=digitalRead(ir_car2);
int S3=digitalRead(ir_car3);
int S4=digitalRead(ir_car4);
int total = S1+S2+S3+S4;
slot = slot-total; 
}
void loop()
{

if(slot>0)
{
analogWrite(led_green,255);
digitalWrite(led_red,HIGH);
}
else
{
digitalWrite(led_red,HIGH);

}


if(S1==1)
{
analogWrite(led_green1,255);
digitalWrite(led_red1,LOW);
}
else
{
analogWrite(led_green2,0);
digitalWrite(led_red2,HIGH);
}

if(S2==1)
{
analogWrite(led_green2,255);
digitalWrite(led_red2,LOW);
}
else
{
analogWrite(led_green2,0);
digitalWrite(led_red2,HIGH);
}

if(S3==1)
{
analogWrite(led_green3,255);
digitalWrite(led_red3,LOW);
}
else
{
analogWrite(led_green3,0);
digitalWrite(led_red3,HIGH);
}

if(S4==1)
{
analogWrite(led_green3,255);
digitalWrite(led_red3,LOW);
}
else
{
analogWrite(led_green3,0);
digitalWrite(led_red3,HIGH);
}


if(digitalRead (ir_enter) == 1)
{
if(slot>0)
{
  myservo1.write(90); 
  slot = slot-1;
  delay(3000);
  analogWrite(led_greenE,255);
  digitalWrite(led_redE,LOW);
    
 }
}
else
{
  analogWrite(led_greenE,0);
  digitalWrite(led_redE,HIGH);
}   

if(digitalRead (ir_exit) == 1)
{
  
  myservo2.write(90); 
  slot = slot+1;
  delay(3000);
}
}
