# FIRE.Extinguisher.robocar
Fire Extinguisher 
#include <SoftwareSerial.h>
#include <AFMotor.h>
int RELAY1 = 8;
int state1 = 0;
AF_DCMotor motor1(1);
AF_DCMotor motor4(3);
AF_DCMotor motor3(3);
char bt = 'S';
void setup()
{
  Serial.begin(9600);
  motor1.setSpeed(255);
  motor3.setSpeed(255);
  motor4.setSpeed(255);
  pinMode(RELAY1, OUTPUT);
  Stop();
}


void loop() {

  bt = Serial.read();

  if (bt == 'F')
  {
    forward();
  }

  if (bt == 'B')
  {
    backward();
  }

  if (bt == 'L')
  {
    left();
  }

  if (bt == 'R')
  {
    right();
  }

  if (bt == 'W')
  {
    Stop();
  }

  if (bt == 'M');
  {
    pump_ON();
  }
  if (bt == 'm');
  {
    pump_OFF();
  }
  if (bt == 'X')
  {
    left_base();
  }
  if (bt == 'Y')
  {
    right_base();
  }
}
void pump_ON()
{
  if (state1 == 0 && bt == 'M')
  {
    digitalWrite(RELAY1, HIGH);
    state1=1;
    bt=0;
  }
}
void pump_OFF()
{
  if (state1 == 1 && bt == 'm')
  {
    digitalWrite(RELAY1, LOW);
    state1=0;
    bt=0;
  }
}
void forward()
{
  motor1.run(FORWARD);
  motor3.run(FORWARD);
}



void backward()
{
  motor1.run(BACKWARD);
  motor3.run(BACKWARD);
}

void left()
{
  motor1.run(FORWARD);
  motor3.run(BACKWARD);
}
void right()
{
  motor1.run(BACKWARD);
  motor3.run(FORWARD);
}
void Stop()
{
  motor1.run(RELEASE);
  motor3.run(RELEASE);
  motor4.run(RELEASE);
}
void left_base()
{
  motor4.run(FORWARD);
}
void right_base()
{
  motor4.run(BACKWARD);
}
