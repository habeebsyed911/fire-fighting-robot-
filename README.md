const int pingTrigPin = 12;
const int pingEchoPin = 13;
#include <Servo.h>
Servo myservo; int pos = 0;
void setup() {
38
pinMode(1, INPUT);
pinMode(2, INPUT);
pinMode(3, INPUT);
pinMode(6, OUTPUT);
pinMode(7, OUTPUT);
pinMode(8, OUTPUT);
pinMode(9, OUTPUT);
pinMode(10, OUTPUT);
myservo.attach(11);
myservo.write(90); }
void put_off_fire()
{
digitalWrite(10,HIGH
);
delay(500);
for (pos = 1; pos <= 90; pos += 1) {
myservo.write(pos);
delay(10);
}
for (pos = 90; pos >= 2; pos-=1) {
myservo.write(pos);
delay(10);
}
digitalWrite(10,LOW);
myservo.writ
e(90);
}
long microsecondsToCentimeters(long microseconds)
{
return microseconds / 29 / 2;
}
void loop()
{
long duration, cm;
39
pinMode(pingTrigPin, OUTPUT);
digitalWrite(pingTrigPin, LOW);
delayMicroseconds(2);
digitalWrite(pingTrigPin, HIGH);
delayMicroseconds(5);
digitalWrite(pingTrigPin, LOW);
pinMode(pingEchoPin, INPUT);
duration = pulseIn(pingEchoPin, HIGH);
cm = microsecondsToCentimeters(duration);
// int d= map(cm, 1, 100, 20, 2000);
if((cm>=20)&(cm<50))
{
digitalWrite(6,HIGH);
digitalWrite(7, LOW);
digitalWrite(8, LOW);
digitalWrite(9, HIGH);
delay(500);
digitalWrite(6, HIGH);
digitalWrite(7, LOW);
digitalWrite(8, HIGH);
digitalWrite(9, LOW);
}
if(digitalRead(1) ==1)
{
digitalWrite(6, LOW);
digitalWrite(7, LOW);
digitalWrite(8, LOW);
digitalWrite(9, LOW);
put_off_fire();
}
if(digitalRead(2) ==1) //RIGHT
{
digitalWrite(6,LOW);
digitalWrite(7, HIGH);
40
digitalWrite(8, HIGH);
digitalWrite(9, LOW);
delay(500);
digitalWrite(6, LOW);
digitalWrite(7, LOW);
digitalWrite(8, LOW);
digitalWrite(9, LOW);
}
if(digitalRead(3) ==1)
//LEFT
{
digitalWrite(6,HIGH);
digitalWrite(7, LOW);
digitalWrite(8, LOW);
digitalWrite(9, HIGH);
delay(500);
digitalWrite(6, LOW);
digitalWrite(7, LOW);
digitalWrite(8, LOW);
digitalWrite(9, LOW);
}
}
