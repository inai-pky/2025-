# 2025-동두천중 아두이노 경진대회/

## 개요
### 목표 : 감응형 신호등 만들기
### 시간 : 1 ~ 4 교시
### 세부내용
### 기본동작 1, 기본동작 2, 응용동작 1, 응용동작 2로 총 4단계로 구분되며 응용동작 2까지 구현을 목표로 하며 각 동작의 구현 유무와 구현까지 걸린 시간을 기준으로 순위를 매기며 상위 3명만 상을 수여함

## 동작설명
### 기본동작 1
### 주어진 코드를 확인하고 필요 부품을 연결하고 코드를 업로드 하여 RGB LED가 정상 작동 하도록 하시오

```C++
// RGB LED 각 핀에 연결된 아두이노 핀 번호를 정의합니다.
// PWM 기능을 지원하는 핀을 사용해야 합니다 (보통 ~ 표시가 있는 핀).
const int redPin = 9;    // 빨간색 LED 핀
const int greenPin = 10; // 초록색 LED 핀
const int bluePin = 11;  // 파란색 LED 핀


struct Color {
  int r, g, b;
};

const Color WHITE = {255, 255, 255};
const Color OFF = {0, 0, 0};

void setup() {

  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  Serial.begin(9600);
}

void setColor(Color color) {
  analogWrite(redPin, color.r);
  analogWrite(greenPin, color.g);
  analogWrite(bluePin, color.b);

  Serial.print("R: ");
  Serial.print(color.r);
  Serial.print(" G: ");
  Serial.print(color.g);
  Serial.print(" B: ");
  Serial.println(color.b);
}

void loop() {

  setColor(WHITE);
  delay(1000);

  setColor(OFF);
  delay(1000);
}

```
<br />
### 기본동작 2
### 초록 3초 -> 주황 1초 -> 빨강 3초 
### RGB LED가 위 순서대로 계속 반복하여 켜지도록 코드를 작성하고 업로드 하시오
<br />
<br />
### 응용동작 1
### 주어진 코드를 참고하여 초음파 센서를 연결하고 센싱값을 시리얼 모니터로 확인하시오

```C++
// HC-SR04 초음파 센서 핀 설정
const int trigPin = 9; // Trig 핀을 디지털 9번에 연결
const int echoPin = 10; // Echo 핀을 디지털 10번에 연결

void setup() {
  // 시리얼 통신 시작 (속도: 9600)
  Serial.begin(9600); 
  
  // 핀 모드 설정
  pinMode(trigPin, OUTPUT); // Trig 핀은 출력용
  pinMode(echoPin, INPUT);  // Echo 핀은 입력용
}

void loop() {
  long duration, distance;

  // 1. Trig 핀으로 초음파 발사 신호 보내기
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10); // 10마이크로초 동안 HIGH 신호 유지
  digitalWrite(trigPin, LOW);

  // 2. Echo 핀으로 초음파가 돌아오는 시간(duration) 측정
  // pulseIn() 함수는 핀이 HIGH 상태를 유지하는 시간을 마이크로초 단위로 반환합니다.
  duration = pulseIn(echoPin, HIGH); 
  
  // 3. 측정된 시간을 거리(cm)로 변환
  // 소리의 속도(340m/s)와 왕복 시간을 고려한 계산식
  distance = duration * 0.034 / 2;

  // 4. 시리얼 모니터에 결과 출력
  Serial.print("거리: ");
  Serial.print(distance);
  Serial.println(" cm");

  delay(500); // 0.5초 간격으로 측정
}
```
<br />
### 응용동작 2 
### 초음파 센서를 활용하여 초음파 센서가 10cm 이하의 값을 센싱하면 아래의 순서도에 따라 신호등을 제어하시오
### 빨강 -> 센싱후 2초 후 초록으로 전환 -> 초록 3초 -> 빨강
