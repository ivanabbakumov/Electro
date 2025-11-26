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
  

  Serial.println(ptr);
}
```
