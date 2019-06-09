// Utilizes a Trinket M0 with a RGB LED, potentiometer and the on-board dotstar. For best results use a linear pot.

#include <Adafruit_DotStar.h>

#define NUMPIXELS 1 

//internal dotstar pins on the trinket m0
#define DATAPIN    7
#define CLOCKPIN   8

Adafruit_DotStar px(NUMPIXELS, DATAPIN, CLOCKPIN, DOTSTAR_BRG);

const int pwmMin = 0;
const int pwmMax = 255;

int r = 0; //pins for rgb led on trinket m0
int g = 2;
int b = 3;

void setup() {
  px.begin();
  px.show();  // dotstar initialization

  pinMode(r, OUTPUT);
  pinMode(g, OUTPUT);
  pinMode(b, OUTPUT);
}

void loop() {
  int pot = analogRead(A0);
  int range = map(pot, 0, 1023, pwmMin, pwmMax); //mapping full analog value to pwm value
  int rgbRange = map(range, pwmMin, pwmMax, 0, 6); //allows for pot to trigger the different cases

  int gUp = map(range, 0, 42, pwmMin, pwmMax); //0 - green value full range rise mapped to 0-42 on pot
  int rDown = map(range, 43, 84, pwmMax, pwmMin); //1 - red value full range rise mapped to 43-84 on pot
  int bUp = map(range, 85, 127, pwmMin, pwmMax); //2 - blue value full range rise mapped to 85-127 on pot
  int gDown = map(range, 128, 169, pwmMax, pwmMin); //3 - green value full range fall mapped to 128-169 on pot
  int rUp = map(range, 170, 212, pwmMin, pwmMax); //4 - red value full range fall mapped to 170-212 on pot
  int bDown = map(range, 213, 255, pwmMax, pwmMin); //5 - blue value full range fall mapped to 213-255 on pot

  switch (rgbRange) {
    case 0:    
      px.setPixelColor(0, gUp, 255, 0); //dotstar mimics rgb led
      px.show();
      analogWrite(g, gUp);
      digitalWrite(r, HIGH); //for full low &/or high just using digitalWrite rather than storing analog value
      digitalWrite(b, LOW);
      break;
    case 1:    
      px.setPixelColor(0, 255, rDown, 0);
      px.show();
      analogWrite(r, rDown);
      digitalWrite(g, HIGH);
      digitalWrite(b, LOW);
      break;
    case 2:    
      px.setPixelColor(0, 255, 0, bUp);
      px.show();
      analogWrite(b, bUp);
      digitalWrite(g, HIGH);
      digitalWrite(r, LOW);
      break;
    case 3:    
      px.setPixelColor(0, gDown, 0, 255);
      px.show();
      analogWrite(g, gDown);
      digitalWrite(b, HIGH);
      digitalWrite(r, LOW);
      break;
    case 4:
      px.setPixelColor(0, 0, rUp, 255);
      px.show();
      analogWrite(r, rUp);
      digitalWrite(b, HIGH);
      digitalWrite(g, LOW);
      break;
    case 5:
      px.setPixelColor(0, 0, 255, bDown);
      px.show();
      analogWrite(b, bDown);
      digitalWrite(r, HIGH);
      digitalWrite(g, LOW);
      break;
  }
  delay(1);
}
