# Electro
Репозиторий посвящен занятиям по электронике

## Мигание светодиода
```c++
void setup() {
  pinMode(8, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  digitalWrite(8, HIGH);
  delay(3000);
  digitalWrite(8, LOW);
  delay(3000);
}
```

## Работа с фоторезистором
```c++
int threshold = 900;

void setup() {
  pinMode(8, OUTPUT);
  pinMode(A0, INPUT);
  Serial.begin(9600);
}

void loop() {
  int photo = analogRead(A0);

  if (photo > threshold) {
    digitalWrite(8, HIGH);
  }
  else {
    digitalWrite(8, LOW);
  }

  Serial.println(photo);
}
```

## Добавили в цепь резистор с переменным сопротивлением 
```c++
void setup() {
  pinMode(8, OUTPUT);
  pinMode(A0, INPUT);
  Serial.begin(9600);
}

void loop() {
  int photo = analogRead(A0);
  int threshold = analogRead(A2);
  if (photo > threshold) {
    digitalWrite(8, HIGH);
  }
  else {
    digitalWrite(8, LOW);
  }

  Serial.println(threshold);
}
```

## С помощью резистора контролируем два режима (мигание диода, выкл)
```c++
void setup() {
  pinMode(8, OUTPUT);
  pinMode(A0, INPUT);
  Serial.begin(9600);
}

void loop() {
  int photo = analogRead(A0);
  int ptr = analogRead(A2);
  if (ptr > 512) {
    digitalWrite(8, HIGH);
    delay(3000);
    digitalWrite(8, LOW);
    delay(3000);
  }
  else digitalWrite(8, LOW);
  Serial.println(ptr);
}
```

## С помощью функции millis() заменили функцию delay
```c++
#define LED_PIN 9
#define LED_PIN_2 8
#define PTR_PIN A0

unsigned long prev = 0;
unsigned long prev_2 = 0;
int ledState = 0;
int ledState_2 = 0;

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(PTR_PIN, INPUT);
  Serial.begin(9600);
}

void loop() {
  unsigned long current = millis();

  if (current - prev > 30000) {
    ledState = !ledState;
    digitalWrite(LED_PIN, ledState);
    prev = current;
  }

  if (current - prev_2 > 3000) {
    ledState_2 = !ledState_2;
    digitalWrite(LED_PIN_2, ledState_2);
    prev_2 = current;
  }

  int ptr = analogRead(PTR_PIN);
  Serial.println(ptr);
  Serial.println(ledState);
}
```
  
## Подключили пищалку и написали небольшую мелодию для нее через массив
```c++
#define LED_PIN 9
#define LED_PIN_2 8
#define PTR_PIN A0
#define BUZZER 10

unsigned long prev = 0;
unsigned long prev_2 = 0;
int ledState = 0;
int ledState_2 = 0;
int melody[3] = {261, 293, 329}; 

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  pinMode(PTR_PIN, INPUT);
  Serial.begin(9600);
}

void loop() {
  unsigned long current = millis();

  if (current - prev > 30000) {
    ledState = !ledState;
    digitalWrite(LED_PIN, ledState);
    prev = current;
  }

  if (current - prev_2 > 3000) {
    ledState_2 = !ledState_2;
    digitalWrite(LED_PIN_2, ledState_2);
    for (int i = 0; i < sizeof(melody); i++) {
      tone(BUZZER, melody[i], 500);
      delay(100);
    }
    
    prev_2 = current;
  }

  int ptr = analogRead(PTR_PIN);
  Serial.println(ptr);
  Serial.println(ledState);
}
```

## Подключили датчик, который считывает влажность почвы
```c++
#define LED_PIN 9
#define LED_PIN_2 8
#define PTR_PIN A0
#define BUZZER 10
#define SOIL A1

unsigned long prev = 0;
unsigned long prev_2 = 0;
int ledState = 0;
int ledState_2 = 0;
int melody[3] = {261, 293, 329}; 

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  pinMode(PTR_PIN, INPUT);
  pinMode(SOIL, INPUT);
  Serial.begin(9600);
}

void loop() {
  int soilState = analogRead(SOIL);
  unsigned long current = millis();

  if (current - prev > 30000) {
    ledState = !ledState;
    digitalWrite(LED_PIN, ledState);
    prev = current;
  }

  if (current - prev_2 > 3000) {
    ledState_2 = !ledState_2;
    digitalWrite(LED_PIN_2, ledState_2);
    for (int i = 0; i < sizeof(melody); i++) {
      tone(BUZZER, melody[i], 500);
      delay(100);
    }
    
    prev_2 = current;
  }

  int ptr = analogRead(PTR_PIN);
  Serial.println(soilState);

}
```

## Подключили датчик температуры вместе с библиотекой
```c++
#include <TroykaThermometer.h>

#define LED_PIN 9
#define LED_PIN_2 8
#define PTR_PIN A0
#define BUZZER 10
#define SOIL A1

unsigned long prev = 0;
unsigned long prev_2 = 0;
int ledState = 0;
int ledState_2 = 0;
int melody[] = {392, 330, 330, 349, 294, 294, 262, 294, 330, 349, 392, 392, 392};
TroykaThermometer thermometer(A4);

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(LED_PIN_2, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  pinMode(PTR_PIN, INPUT);
  pinMode(SOIL, INPUT);
  Serial.begin(9600);
}

void loop() {
  int soilState = analogRead(SOIL);
  unsigned long current = millis();

  thermometer.read();
  Serial.print("Temperature is ");
  Serial.print(thermometer.getTemperatureC());
  Serial.println(" C");

  if (current - prev > 30000) {
    ledState = !ledState;
    digitalWrite(LED_PIN, ledState);
    prev = current;
  }

  if (current - prev_2 > 3000) {
    ledState_2 = !ledState_2;
    digitalWrite(LED_PIN_2, ledState_2);
    for (int i = 0; i < sizeof(melody); i++) {
      tone(BUZZER, melody[i], 700);
      delay(200);
    }
    
    prev_2 = current;
  }

  int ptr = analogRead(PTR_PIN);
  Serial.println(soilState);

}
```

## Наброски программы для ухода за цветком с сенсорами (связали Arduino и p5.js)
```c++
#define PTR A0
#define PHOTO A2
#define LED 9

int p5data, p5ptr;

void setup() {
  Serial.begin(9600);
  pinMode(PTR, INPUT);
  pinMode(PHOTO, INPUT);
  pinMode(LED, OUTPUT);
}

void loop() {
  int val = analogRead(PTR);
  int photo = analogRead(PHOTO);
  Serial.println(String(val) + ";" + String(photo));

  if (Serial.available() > 0) {
    p5data = Serial.read();
    p5ptr = Serial.read();

    if (p5data == 1) {
      analogWrite(LED, PTR);
      delay(100);
    }
    else digitalWrite(LED, LOW);
  }
}
```
