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
