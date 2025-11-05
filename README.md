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
```
int threshold = 600;

void setup() {
  pinMode(8, OUTPUT);
  pinMode(A0, OUTPUT);
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
