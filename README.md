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

// 색상 값을 저장할 구조체를 정의합니다 (선택 사항이지만 관리가 용이합니다).
struct Color {
  int r, g, b;
};

// 주요 색상들을 미리 정의합니다.

const Color WHITE = {255, 255, 255};

void setup() {
  // 각 LED 핀을 출력으로 설정합니다.
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  // 시리얼 통신을 시작합니다 (선택 사항: 값 확인용).
  Serial.begin(9600);
}

// RGB 색상을 설정하는 함수 (Color 구조체 사용)
void setColor(Color color) {
  // analogWrite 함수를 사용하여 각 LED의 밝기를 PWM으로 제어합니다.
  // (예: analogWrite(redPin, 255 - color.r);)
  analogWrite(redPin, color.r);
  analogWrite(greenPin, color.g);
  analogWrite(bluePin, color.b);

  // 현재 색상 값을 시리얼 모니터에 출력합니다 (선택 사항).
  Serial.print("R: ");
  Serial.print(color.r);
  Serial.print(" G: ");
  Serial.print(color.g);
  Serial.print(" B: ");
  Serial.println(color.b);
}

void loop() {
  // 정의된 색상 변수를 사용하여 LED 색상을 변경합니다.

  // 빨간색 밝게
  setColor(WHITE);
  delay(1000);

  // LED 끄기
  setColor(OFF);
  delay(1000);
}

```
### 기본동작 2
### 초록 3초 -> 주황 1초 -> 빨강 3초 
### RGB LED가 위 순서대로 계속 반복하여 켜지도록 코드를 작성하고 업로드 하시오

### 응용동작 1
### 주어진 코드를 참고하여 초음파 센서를 연결하고 센싱값을 시리얼 모니터로 확인하시오

### 응용동작 2 
### 초음파 센서를 활용하여 초음파 센서가 10cm 이하의 값을 센싱하면 아래의 순서도에 따라 신호등을 제어하시오
### 빨강 -> 센싱후 2초 후 초록으로 전환 -> 초록 3초 -> 빨강
