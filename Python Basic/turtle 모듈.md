## Turtle Graphic
---
2차원 화면에 로봇 거북이가 있다고 가정하고, 이 거북이에게 명령을 내려서 그림을 그리는 기능으로 우리가 화면에서 거북이를 움직이면
 거북이의 움직임에 따라 그림이 그려진다.
 ```
 import turtle # turtle 모듈을 사용하기 위해 준비
 t=turtle.Turtle() # turtle 모듈에 있는 Turtle 클래스 객체를 t로 생성
 t.shape("turtle") # Turtle 클래스 객체인 t의 모양을 거북이 모양으로 설정
 
 t.forward(100) # 거북이를 전진시키는 명령어, 100pixel 만큼 이동
 t.left(90) # 거북이를 왼쪽으로 90도 회전시키는 명령어
 
 t.circle(반지름) # '반지름'을 반지름으로 하는 원을 그리는 명령어
 ```
