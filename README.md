#include <DFRobotDFPlayerMini.h>
#include <Wire.h>
#include <SoftwareSerial.h>
int t =200;
int a;
static const uint8_t PIN_MP3_TX=10;
static const uint8_t PIN_MP3_RX=9;

SoftwareSerial softwareSerial (PIN_MP3_RX, PIN_MP3_TX);
DFRobotDFPlayerMini player;

int thumb;
int first_finger;
int second_finger;
int third_finger;
int fourth_finger;

void setup() {

  pinMode(A1,INPUT);
  pinMode(A2,INPUT);
  pinMode(A3,INPUT);
  pinMode(A4,INPUT);
  pinMode(A5,INPUT);
  Serial.begin(9600);

  softwareSerial.begin(9600);
  if(player.begin(softwareSerial)){
    Serial.println("Working");
    player.volume(30);
    //player.play(5);
  }else{
    Serial.println("Connecting to DFPlayer Mini Failed!");
  }
}

void loop() {
  
int thumb=analogRead(A1);
int first_finger=analogRead(A2);
int second_finger=analogRead(A3);
int third_finger=analogRead(A4);
int fourth_finger=analogRead(A5);

Serial.print (thumb);
Serial.print("/t");

Serial.print (first_finger);
Serial.print("/t");

Serial.print (second_finger);
Serial.print("/t");

Serial.print (third_finger);
Serial.print("/t");

Serial.print (fourth_finger);
Serial.println("/t");


if (thumb < 750){

  Serial.println("Thumb Up");
  //player.play(1);
  delay(1000);
}else if(thumb >= 750){

  Serial.println("Thumb Down");
  //player.play(1);
  delay(1000);
}

if (first_finger >= 780){
  Serial.println("Finger Down 1");
  //player.play(2);
  delay(t); 
}else if(first_finger < 780){
  Serial.println("Finger Up 1");
  //player.play(3);
  delay(t);
}
if (second_finger >= 731){

  Serial.println("Finger Down 2");
  //player.play(4);
  delay(t);
}else if (second_finger < 731){
  Serial.println("Finger Up 2");
 // player.play(5);
  delay(t);
}
if (third_finger >= 748){
  Serial.println ("Finger Down 3");
 // player.play(6);
  delay(t);
}else if (third_finger <748){
  Serial.println ("Finger Up 3");
  //player.play(8);
  delay(t);
}

if (fourth_finger >=789){
  Serial.println("Finger Down 4");
 // player.play(9);
  a = 0;
  delay(t);
}else if (fourth_finger <789){
  Serial.println("Finger Up 4");
 // player.play (10);
  a=1;
  delay(t);
}else{
  Serial.println("Nothing");
}

if (a == 1){
  Serial.println("Funciona");
  }


if (first_finger >= 780 & second_finger >= 731 & third_finger >= 748 & fourth_finger >= 789 & thumb >= 750){
 
  Serial.println ("o");
  player.play (1);
  delay (t);
}

if (first_finger >= 780 & second_finger >= 731 & third_finger >= 748 & fourth_finger < 789 & thumb >= 750){

  Serial.println ("i");
  player.play (2);
  delay (t);
}

if (first_finger >= 780 & second_finger >= 731 & third_finger >= 748 & fourth_finger < 789 & thumb < 750){

  Serial.println ("y");
  player.play (3);
  delay (t);
}

if (first_finger < 780 && second_finger < 731 && third_finger >= 748 && fourth_finger >= 789 && thumb >= 750){
 
  Serial.println ("v");
  player.play (4);
  delay (t);
}
}
