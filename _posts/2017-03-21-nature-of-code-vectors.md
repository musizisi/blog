---
layout: post
title: Chapter 1. Vecoters
---

"Roger, Roger. What's our vector, Victor?"
  - Captain Oveur (Airplane)

유클리디(그리스의 수학자) 벡터 또는 기하 벡터 : 크기와 방향을 가지는 객체

## 1.1 백터 기본

위치 : 변수 x, y

속도 : 변수 xspeed, yspeed

*예제 1-1* 벡터를 사용하지 않고 구현한 튕기는 공 (Bouncing Ball, no vectors)
```java
// 위치와 속도를 나타내는 변수
float x = 100;
float y = 100;
float xspeed = 2.5;
float yspeed = 2;

// setup() 함수는 프로그램이 시작하기 전에 한 번 실행됩니다.
// 반면에 draw() 함수는 프로그램이 종료되기 전까지 계속 반복해서 실행됩니다.
void setup() {
  size(800, 200);
  smooth();
}

void draw() {
  background(255);

  // 속도만큼 위치를 이동시킵니다.
  x = x + xspeed;
  y = y + yspeed;

  // 화면을 벗어나는지 검사하고 공을 튕깁니다.
  if ((x > width) || (x < 0)) {
    xspeed = xspeed * -1;
  }
  if ((y > height) || (y < 0)) {
    yspeed = yspeed * -1;
  }

  // x, y 위치에 원을 그립니다.
  stroke(0);
  strokeWeight(2);
  fill(127);
  ellipse(x, y, 48, 48);
}
```


## 1.2 프로세싱 프로그래밍과 벡터

[다음 위치] = [현재 위치] + [속도]

```java
class PVector {
  float x;
  float y;
  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }
}
```

## 1.3 벡터 덧셈

```java
class PVector {

  float x;
  float y;

  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }

  void add(PVector v) {
    y = y + v.y;
    x = x + v.x;
  }
}

```

*예제 1-2* PVector 클래스를 활용한 튕기는 공 (Bouncing Ball, with PVector!)

```java
// float 변수를 쓸데없이 많이 만들지 말고, PVector 객체를 2개 만들어줍니다.
PVector location;
PVector velocity;

void setup() {
  size(200,200);
  background(255);
  location = new PVector(100,100);
  velocity = new PVector(2.5,5);
}

void draw() {
  noStroke();
  fill(255,10);
  rect(0,0,width,height);

  // PVector 객체의 요소를 사용하고 싶을 때는
  // location.x 와 location.y 형태로 . 기호를 사용합니다.
  location.add(velocity);

  if ((location.x > width) || (location.x < 0)) {
    velocity.x = velocity.x * -1;
  }
  if ((location.y > height) || (location.y < 0)) {
    velocity.y = velocity.y * -1;
  }

  // x, y 에 원을 그려줍니다.
  stroke(0);
  fill(175);
  ellipse(location.x,location.y,16,16);
}
```
연습문제 1-1

연습문제 1-2

연습문제 1-3


## 1.4 벡터와 관련된 수학

- add() : 벡터 덧셈 연산 (add vectors)
- sub() : 벡터 뺄셈 연산 (subtract vectors)
- mult() : 벡터 곱셈 연산 (scale the vector with multiplication)
- div() : 벡터 나눗셈 연산 (scale the vector with division)
- mag() : 벡터의 크기를 구함 (calculate the magnitude of a vector)
- setMag() : 벡터의 크기 지정 (set the magnitude of a vector)
- normalize() : 방향이 같고 단위 길이가 1인 벡터로 설정 (normalize the vector to a unit length of 1)
- limit() : 백터의 크기가 매개변수로 넣은 최댓값을 넘을 때 줄임 (limit the magnitude of a vector)
- heading() : 2차원 벡터의 회전 각도를 구함 (the 2D heading of a vector expressed as an angle)
- rotate() : 2차원 벡터를 특정 각도만큼 화전 (rotate a 2D vector by an angle)
- lerp() : 선형 보간법을 사용 (linear interpolate to another vector)
- dist() : 두 벡터(점)의 유클리드 거리를 구함 (the Euclidean distance between two vectors (considered as points))
- angleBetween() : 두 벡터의 각도를 구함 (find the angle between two vectors)
- dot() : 두 벡터를 내적 연산 (the dot product of two vectors)
- cross() : 두 벡터를 외적 연산 3차원 관련 (the cross product of two vectors (only relevant in three dimensions))
- random2D() : 임의의 2차원 벡터 생성 (make a random 2D vector)
- random3D() : 임의의 3차원 벡터 생성 (make a random 3D vector)


### 1.4.1 벡터 뺄셈

```java
class PVector {

  float x;
  float y;

  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }

  void add(PVector v) {
    y = y + v.y;
    x = x + v.x;
  }

  void sub(PVector v) {
    x = x - v.x;
    y = y - v.y;
  }
}

```

*예제 1-3* 백터 뺄셈 (Vector subtraction)
```java
void setup() {
  size(640,360);
}

void draw() {
  background(255);

  // 마우스 좌표를 나타내는 벡터를 생성합니다.
  PVector mouse = new PVector(mouseX,mouseY);
  // 화면 중심 좌표를 나타내는 벡터를 생성합니다.
  PVector center = new PVector(width/2,height/2);
  // 벡터 뺄셈 연산
  mouse.sub(center);

  // 뺄셈 연산된 벡터를 그려줍니다.
  translate(width/2,height/2);
  strokeWeight(2);
  stroke(0);
  line(0,0,mouse.x,mouse.y);

}
```

### 1.4.2 벡터 곱셉

```java
class PVector {

  float x;
  float y;

  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }

  void add(PVector v) {
    y = y + v.y;
    x = x + v.x;
  }

  void sub(PVector v) {
    x = x - v.x;
    y = y - v.y;
  }

  void mult(float n) {
    x = x * n;
    y = y * n;
 }
}

```

*예제 1-4* 벡터 곱셈 (Multiplying a vector)
```java

void setup() {
  size(640,360);
  smooth();
}

void draw() {
  background(255);

  PVector mouse = new PVector(mouseX,mouseY);
  PVector center = new PVector(width/2,height/2);
  mouse.sub(center);

  // 벡터 곱셈 연산입니다. 벡터에 0.5를 곱해 크기가 절반이 됩니다.
  mouse.mult(0.5);  

  translate(width/2,height/2);
  strokeWeight(2);
  stroke(0);
  line(0,0,mouse.x,mouse.y);
}
```

## 1.5 벡터 크기

```java
class PVector {

  float x;
  float y;

  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }

  void add(PVector v) {
    y = y + v.y;
    x = x + v.x;
  }

  void sub(PVector v) {
    x = x - v.x;
    y = y - v.y;
  }

  void mult(float n) {
    x = x * n;
    y = y * n;
  }

  float mag() {
    return sqrt(x*x + y*y);
  }

}

```

*예제 1-5* 벡터의 크기 (Vector magnitude)
```java

void setup() {
  size(640,360);
}

void draw() {
  background(255);

  PVector mouse = new PVector(mouseX,mouseY);
  PVector center = new PVector(width/2,height/2);
  mouse.sub(center);

  // 벡터의 크기(또는 길이)는 mag() 함수로 구할 수 있습니다.
  // 구해진 벡터의 길이로 화면 왼쪽 위에 벡터를 그려줍니다.
  float m = mouse.mag();
  fill(0);
  noStroke();
  rect(0,0,m,10);

  translate(width/2,height/2);
  stroke(0);
  strokeWeight(2);
  line(0,0,mouse.x,mouse.y);

}

```

## 1.6 벡터 정규화

```java
class PVector {

  float x;
  float y;

  PVector(float x_, float y_) {
    x = x_;
    y = y_;
  }

  void add(PVector v) {
    y = y + v.y;
    x = x + v.x;
  }

  void sub(PVector v) {
    x = x - v.x;
    y = y - v.y;
  }

  void mult(float n) {
    x = x * n;
    y = y * n;
  }

  float mag() {
    return sqrt(x*x + y*y);
  }

  void normalize() {
    float m = mag();
    if (m != 0) {
      div(m);
    }
  }

}

```

*예제 1-6* 벡터의 정규화 (Normalizing a vector)

```java

// Normalizing a vector sets its length to 1.
void setup() {
  size(640,360);
}

void draw() {
  background(255);

    // A vector that points to the mouse location
    PVector mouse = new PVector(mouseX,mouseY);
    // A vector that points to the center of the window
    PVector center = new PVector(width/2,height/2);
    // Subtract center from mouse which results in a vector
    // that points from center to mouse
    mouse.sub(center);

    // Normalize the vector
    mouse.normalize();

    // 벡터를 정규화하고 50을 곱해주는데요. 길이가 1이면 화면에서 잘 보이지
    // 않으므로 50을 곱한 것입니다. 어쨌거나 마우스를 어떤 위치에 놓아도
    // 벡터의 길이가 유지된다는 것을 확인해주세요.

    // Multiply its length by 50
    mouse.mult(150);

    translate(width/2,height/2);
    // Draw the resulting vector
    stroke(0);
    strokeWeight(2);
    line(0,0,mouse.x,mouse.y);

}
```


## 1.7 속도와 벡터를 활용한 이동

*예제 1-7* 속도를 활용한 기본적인 움직임 (Motion 101 (velocity))
```java

// Mover 클래스의 변수를 선언합니다.
Mover mover;

void setup() {
  size(640,360);

  // Mover 클래스로 객체를 생성합니다.
  mover = new Mover();
}

void draw() {
  background(255);

  // Mover 객체의 함수를 호출합니다.
  mover.update();
  mover.checkEdges();
  mover.display();
}

class Mover {

  // Mover 클래스는 위치(location)와 속도(velocity)라는 2개의 속성을 갖습니다.
  PVector location;
  PVector velocity;

  Mover() {
    location = new PVector(random(width), random(height));
    velocity = new PVector(random(-2, 2), random(-2, 2));
  }

  void update() {
    // 가장 중요한 부분입니다. 속도로 위치를 변경합니다.
    location.add(velocity);
  }

  void display() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    ellipse(location.x, location.y, 48, 48);
  }

  void checkEdges() {

    if (location.x > width) {
      location.x = 0;
    }
    else if (location.x < 0) {
      location.x = width;
    }

    if (location.y > height) {
      location.y = 0;
    }
    else if (location.y < 0) {
      location.y = height;
    }
  }
}

```

## 1.8 가속도와 벡터를 사용한 이동

가속도`acceleration`는 속도가 변화하는 비율을 의미합니다.

### 1.8.1 가속도 활용

1. 변하지 않는 값을 가속도로 사용
2. 랜덤한 값을 가속도로 사용
3. 마우스를 향하는 가속도를 사용

**연습문제 1-4**
```java

  void limit(float max) {
    if (magSq() > max*max) {
      normalize();
      mult(max);
    }
  }
````

*예제 1-8* 변하지 않는 값을 가속도로 사용한 움직임 (Motion 101 (velocity and constant acceleration))
```java

Mover mover;

void setup() {
  size(640,360);
  mover = new Mover();
}

void draw() {
  background(255);

  mover.update();
  mover.checkEdges();
  mover.display();
}  


class Mover {

  PVector location;
  PVector velocity;

  // 가속도가 이번 예제의 핵심입니다.
  PVector acceleration;

  // 속도의 최대값을 나타내는 변수입니다.
  float topspeed;

  Mover() {
    location = new PVector(width/2, height/2);
    velocity = new PVector(0, 0);
    acceleration = new PVector(-0.001, 0.01);
    topspeed = 10;
  }

  void update() {
    // 가속도로 속도를 변경합니다. 그리고 topspeed 벼수로 속도를 제한합니다.
    velocity.add(acceleration);
    velocity.limit(topspeed);
    location.add(velocity);
  }

  // display() 함수는 이전과 같습니다.
  void display() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    ellipse(location.x, location.y, 48, 48);
  }

  // checkEdges() 함수는 이전과 같습니다.
  void checkEdges() {

    if (location.x > width) {
      location.x = 0;
    }
    else if (location.x < 0) {
      location.x = width;
    }

    if (location.y > height) {
      location.y = 0;
    }
    else if (location.y < 0) {
      location.y = height;
    }
  }
}


```

**연습문제 1-5**
```java

Mover mover;

int flag = 2;

void setup() {
  size(500,500);
  background(255,255,255);
  mover = new Mover();
}

void draw() {
  background(255,255,255);

  if(flag == 0) {
    mover.update();
  }else if(flag == 1) {
    mover.update2();
  }else if(flag == 2) {
    mover.update3();
  }
  mover.checkEdges();
  mover.display();
}

void keyPressed() {
  if (key == CODED) {
    if(keyCode == RIGHT) {
      flag = 0;
    }else if(keyCode == LEFT) {
      flag = 1;
    }
  }
}

void keyReleased() {
  if (key == CODED) {
    if(keyCode == RIGHT) {
      flag = 2;
    }else if(keyCode == LEFT) {
      flag = 2;
    }
  }
}


//class
class Mover {
  PVector location, velocity, acceleration;
  float topspeed;

  Mover() {
    location = new PVector(width/2,height/2);
    velocity = new PVector(0,0);
    acceleration = new PVector(0.1, 0);
    topspeed = 100;
  }


  void update() {
    velocity.add(acceleration);
    velocity.limit(topspeed);
    location.add(velocity);
  }

  void update2() {
    velocity.sub(acceleration);
    velocity.limit(topspeed);
    location.add(velocity);
  }

  void update3() {  
    location.add(velocity);
  }

  void display() {   
    stroke(0);
    fill(0,0,0);
    ellipse(location.x,location.y,10,10);
  }

  void checkEdges() {
     if (location.x > width) {
      location.x = 0;
    } else if (location.x < 0) {
      location.x = width;
    }
    if (location.y > height) {
      location.y = 0;
    } else if (location.y < 0) {
      location.y = height;
    }

  }

}

```


*예제 1-9* 임의 값을 가속도로 사용한 움직임 (Motion 101 (velocity and random acceleration))
```java

Mover mover;

void setup() {
  size(640,360);
  mover = new Mover();
}

void draw() {
  background(255);
  mover.update();
  mover.checkEdges();
  mover.display();
}


class Mover {

  PVector location;
  PVector velocity;
  PVector acceleration;
  float topspeed;

  Mover() {
    location = new PVector(width/2, height/2);
    velocity = new PVector(0, 0);
    topspeed = 6;
  }

  void update() {

    // PVector 클래스의 random2D() 함수를 사용하면
    // 임의의 방향을 가진, 길이가 1인 벡터를 얻을 수 있습니다.
    acceleration = PVector.random2D();
    acceleration.mult(random(2));

    velocity.add(acceleration);
    velocity.limit(topspeed);
    location.add(velocity);
  }

  void display() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    ellipse(location.x, location.y, 48, 48);
  }

  void checkEdges() {

    if (location.x > width) {
      location.x = 0;
    }
    else if (location.x < 0) {
      location.x = width;
    }

    if (location.y > height) {
      location.y = 0;
    }
    else if (location.y < 0) {
      location.y = height;
    }
  }
}


```

## 1.9 static 함수

연습문제 1-7
```java
PVector v = new PVector(1, 5);
PVector u = v.mult(2);
PVector w = PVector.sub(v, u);
PVector w = w.div(3);
```

## 1.10 가속도와 상호작용

*예제 1-10* 마우스를 향해 가속되는 객체 (Accelerating towards the mouse)
```java
// A Mover object
Mover mover;

void setup() {
  size(640,360);
  mover = new Mover();
}

void draw() {
  background(255);

  // Update the location
  mover.update();
  // Display the Mover
  mover.display();
}


class Mover {

  // The Mover tracks location, velocity, and acceleration
  PVector location;
  PVector velocity;
  PVector acceleration;
  // The Mover's maximum speed
  float topspeed;

  Mover() {
    // Start in the center
    location = new PVector(width/2,height/2);
    velocity = new PVector(0,0);
    topspeed = 5;
  }

  void update() {

    // 첫 번째 : 방향을 구합니다.
    PVector mouse = new PVector(mouseX,mouseY);
    PVector dir = PVector.sub(mouse,location);

    // 두 번째 : 벡터를 정규화합니다.
    dir.normalize();

    // 세 번째 : 크기를 조절합니다.
    dir.mult(0.5);

    // 네 번째 : 가속도를 설정합니다.
    acceleration = dir;

    // Velocity changes according to acceleration
    velocity.add(acceleration);
    // Limit the velocity by topspeed
    velocity.limit(topspeed);
    // Location changes by velocity
    location.add(velocity);
  }

  void display() {
    stroke(0);
    strokeWeight(2);
    fill(127);
    ellipse(location.x,location.y,48,48);
  }

}


```

연습문제 1-8


*예제 1-11* 마우스를 향해 가속되는 객체들 (Array of movers accelerating towards the mouse)
```java

// 객체들의 배열
Mover[] movers = new Mover[20];

void setup() {
  size(640,360);
  for (int i = 0; i < movers.length; i++) {
    // 배열을 초기화힙니다.
    movers[i] = new Mover();
  }
}

void draw() {

  background(255);

  for (int i = 0; i < movers.length; i++) {
    // 배열 안에 있는 객체의 함수를 호출합니다.
    movers[i].update();
    movers[i].checkEdges();
    movers[i].display();
  }
}


class Mover {

  // The Mover tracks location, velocity, and acceleration
  PVector location;
  PVector velocity;
  PVector acceleration;
  // The Mover's maximum speed
  float topspeed;

  Mover() {
    // Start in the center
    location = new PVector(random(width),random(height));
    velocity = new PVector(0,0);
    topspeed = 5;
  }

  // 가속도와 관련된 코드가 들어있는 함수
  void update() {

    // 마우스를 향하는 벡서를 생성합니다.
    PVector mouse = new PVector(mouseX,mouseY);
    PVector dir = PVector.sub(mouse,location);

    // 만들어진 벡터를 가속도로 설정합니다.
    acceleration = dir;

    // 벡터를 정규화합니다.
    acceleration.normalize();
    // 크기를 변경합니다.
    acceleration.mult(0.5);


    // 실제로 물체를 움직는 코드입니다.
    // 가속도로 속도를 변경합니다.
    velocity.add(acceleration);
    // 가속도를  topspeed까지 제한합니다.
    velocity.limit(topspeed);
    // 속도로 위치를 변경합니다.
    location.add(velocity);
  }

  void display() {
    stroke(0);
    fill(175);
    ellipse(location.x,location.y,16,16);
  }

  void checkEdges() {
    if (location.x > width) {
      location.x = 0;
    } else if (location.x < 0) {
      location.x = width;
    }

    if (location.y > height) {
      location.y = 0;
    } else if (location.y < 0) {
      location.y = height;
    }
  }

}

```
