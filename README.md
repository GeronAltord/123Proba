#include <Arduino.h>
int VCC1 = 1;
int VCC0 = 0;
uint8_t sensor0_value = 0;
uint8_t sensor1_value = 0;
int motorPin = 9;
#include <LiquidCrystal.h>  // Лобавляем необходимую библиотеку
LiquidCrystal lcd(7, 6, 5, 4, 3, 2); // (RS, E, DB4, DB5, DB6, DB7)
void setup() {
  Serial.begin(9600);
  lcd.begin(20, 2);
  lcd.setCursor(0, 0);              // Устанавливаем курсор в начало 1 строки
  lcd.print("Hello, world!");       // Выводим текст
  pinMode(VCC1, INPUT);
  pinMode(VCC0, INPUT);
  pinMode (motorPin, OUTPUT );
  }
void loop() {
sensor0_value = (255-analogRead(VCC0)/4);
Serial.print(sensor0_value);
Serial.println(" null");
sensor1_value = (255-analogRead(VCC1)/4);
Serial.println(sensor1_value);
if ((sensor1_value >= 200) && (sensor0_value > sensor1_value)){
  digitalWrite (motorPin, HIGH);
  delay(3000);
  digitalWrite (motorPin, LOW );
  delay(100);
}
else{
  digitalWrite (motorPin, HIGH);
  delay(1000);
  digitalWrite (motorPin, LOW );
  delay(1000);
}
lcd.setCursor(0, 1);              // Устанавливаем курсор в начало 2 строки
lcd.print(sensor1_value);
delay(1000);
}
