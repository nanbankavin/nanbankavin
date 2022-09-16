#include <Servo.h>

int TEMP = 0;

int GAS = 0;

int MOTION = 0;

Servo servo_2;

void setup()
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode(6, INPUT);
  Serial.begin(9600);
  pinMode(4, OUTPUT);
  servo_2.attach(2, 500, 2500);
}

void loop()
{
  TEMP = (-40 + 0.488155 * (analogRead(A0) - 20));
  GAS = analogRead(A1);
  MOTION = digitalRead(6);
  if (TEMP > 80 && GAS > 150) {
    Serial.println("FIRE ALERT !!!!!!!!!!!!!!!!!");
    digitalWrite(4, HIGH);
    if (MOTION == 1) {
      Serial.println("DOOR OPEN >>>>>");
      servo_2.write(90);
    } else {
      servo_2.write(0);
    }
  } else {
    digitalWrite(4, LOW);
    servo_2.write(0);
  }
  delay(10);
}
