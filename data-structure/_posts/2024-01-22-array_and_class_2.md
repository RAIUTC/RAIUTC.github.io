---
layout: post
title: Array & Class(2)
description: |
  이 글에서는 "Array & Class(2)"라는 제목으로, 클래스 문법(정의 방법, 멤버십, 생성자 및 소멸자, 상속 및 다형성)에 대한 내용과 STL에서의 Vector (Vector의 개념과 사용법)에 대해 다룹니다. 이를 통해 자료구조와 객체지향 프로그래밍의 핵심 원리를 손쉽게 이해할 수 있습니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Array & Class(2)

## 객체와 구조체

- **하나의 객체는 상태와 행위로 구성**

<p align="center">
<img src="/assets/img/blog/object_state_and_behavior.png">
</p>

- **절차 지향적 프로그래밍으로 객체를 구성한다면?**
  - 상태: 구조체, 행위: 함수 (데이터와 함수가 분리되어 있음)

<p align="center">
<img src="/assets/img/blog/object_made_by_procedural_programming.png">
</p>

## 객체와 클래스

- **클래스를 이용해 객체 지향적으로 객체 구성**
  - 속성: <span style="color:blue">멤버 변수</span>(member variable) 또는 필드(field)
  - 행위: <span style="color:red">멤버 함수</span>(member function) 또는 메소드(method)
  - 데이터와 함수를 묶음(encapsulation)

<p align="center">
<img src="/assets/img/blog/object_and_class.png">
</p>

## 클래스의 선언과 활용

- **클래스 선언: <span style="color:blue">class</span> 또는 <span style="color:blue">struct</span>**
  - 멤버 변수와 멤버 함수를 클래스 블록에 포함
  - 멤버 선언 위치에 상관없이 사용 가능

~~~cpp
class 클래스명 { // 새로운 클래스를 선언
  private:    // 멤버 접근 지정자(public, private, protected)
    멤버 변수1; // 멤버 변수는 객체의 속성을 나타냄
    멤버 변수2;
    ...
  public:     // 멤버에 대한 접근 지정자
    멤버 함수1; // 멤버 함수는 객체의 동작을 나타냄
    멤버 함수2;
    ...
};          // 세미콜론(';')을 잊지 말아야 함.
~~~

- **class, struct 기본 접근 지정자가 다름**
  - <span style="color:red">class:</span> 전용(private)
  - <span style="color:red">struct:</span> 공용(public)

~~~cpp
struct Complex {
  // public body
};

class Complex {
  public:
    // public body
};

class Complex {
  // private body
};
~~~

## 객체의 생성과 멤버 접근

- 복소수 클래스의 선언과 멤버 접근 예시 ($$a+bi$$)

<p align="center">
<img src="/assets/img/blog/object_generation_and_member_access.png">
</p>

## 생성자 & 소멸자

<p align="center">
<img src="/assets/img/blog/generator_and_destructor.png">
</p>

## 상속 & 다형성

<p align="center">
<img src="/assets/img/blog/inheritence_and_polymorphism.png">
</p>

## 사례: Complex의 다양한 변신

- **Complex v1: 구조체와 일반 함수로 구현한 복소수**

- **Complex v2: 복소수를 클래스로 전환(데이터 + 함수)**

- **Complex v3: 멤버 이름의 단순화**

- **Complex v4: 모든 멤버 함수를 내부 구현**

## Complex v1: 구조체와 함수

- Complex.h

~~~cpp
struct Complex {
  double real;
  double imag;
};
void setComplex(Complex &c, double r, double i){
  c.real = r;
  c.imag = i;
}
extern Complex readComplex();
extern void printComplex(Complex c);
extern Complex addComplex(Complex a, Complex b);
~~~

- Complex.cpp

~~~cpp
#include "Complex.h"
Complex readComplex(){
  Complex c;
  scanf("%lf %lf", &c.real, &c.imag);
  return c;
}
void printComplex(Complex c){
  printf("%4.1f + %4.1fi\n", c.real, c.imag);
}
Complex addComplex(Complex a, Complex b){
  Complex c;
  c.real = a.real + b.real;
  c.imag = a.imag + b.imag;
  return c;
}
~~~

- main.cpp

~~~cpp
#include "Complex.h"

int main(){
  Complex a, b, c;
  a = readComplex();
  b = readComplex();
  c = addComplex(a, b);
  printComplex(a);
  printComplex(b);
  printComplex(c);
  return 0;
}
~~~

## Complex v2: 클래스로 변환

- Complex.h

~~~cpp
class Complex {
  private:
    double real; // 데이터는 private으로 선언
    double imag;
  public:
    void setComplex(double r, double i){
      real = r;     // 객체를 입력을 받을 필요가 없음
      imag = i;
    }
    void readComplex();
    void printComplex();
    void addComplex(Complex a, Complex b);
};
~~~

- Complex.cpp

~~~cpp
#include "Complex.h"

void Complex::readComplex(){
  scanf("%lf %lf", &real, &imag); // 범위 연산자(::)로 Complex 클래스의 멤버 함수임을 명시
}
void Complex::printComplex(){
  printf("%4.1f + %4.1fi\n", real, imag);
}
void Complex::addComplex(Complex a, Complex b){ // 반환형 void로 변경
  real = a.real + b.real;
  imag = a.imag + b.imag; // private의 접근 기준은 object가 아니라 class의 기준 따라서 Complex 클래스 내에서는 다른 object의 멤버 변수 직접 접근 가능!
}
~~~

- main.cpp

~~~cpp
#include "Complex.h"

int main(){
  Complex a, b, c;  // Complex 객체 생성
  a.readComplex();
  b.readComplex();
  c.addComplex(a, b); // c객체에 결과 저장
  a.printComplex();
  b.printComplex();
  c.printComplex();
  return 0;
}
~~~

## Complex v3: 이름 단순화

- Complex.h

~~~cpp
class Complex {
  private:
    double real;
    double imag;
  public:   // Complex의 연산이므로 각 멤버 함수 뒤에 Complex를 붙이지 않아도 의미 명확함
    void set(double r, double i){
      real = r;
      imag = i;
    }
    void read();
    void print();
    void add(Complex a, Complex b);
};
~~~

- Complex.cpp

~~~cpp
#include "Complex.h"

void Complex::read(){
  scanf("%lf %lf", &real, &imag);
}
void Complex::print(){
  printf("%4.1f + %4.1fi\n", real, imag);
}
void Complex::add(Complex a, Complex b){
  real = a.real + b.real;
  imag = a.imag + b.imag;
}
~~~

- main.cpp

~~~cpp
#include "Complex.h"

int main(){
  Complex a, b, c;

  // 가독성을 해하지 않으면서 코드가 간결하게 표현됨
  a.read();
  b.read();
  c.add(a, b);
  a.print();
  b.print();
  c.print();

  return 0;
}
~~~

## Complex v4: 내부 단순화

- Complex.h

~~~cpp
// Complex.cpp 내에 구현하지 않고 헤더 파일에 구현하는 것
class Complex {
  private:
    double real;
    double imag;
  public:
    void set(double r, double i){
      real = r;
      imag = i;
    }

    void read(){
      scanf("%lf %lf", &real, &imag);
    }

    void print(){
      printf("%4.1f + %4.1fi\n", real, imag);
    }

    void add(Complex a, Complex b){
      real = a.real + b.real;
      imag = a.imag + b.imag;
    }
};
~~~

- main.cpp

~~~cpp
#include "Complex.h"

int main(){
  Complex a, b, c;
  a.read();
  b.read();
  c.add(a, b);
  a.print();
  b.print();
  c.print();
  return 0;
}

// 실제 개발은 헤더파일(.h)과 본문파일 (.cpp)을 구분하는 게 바람직
~~~

## 배열 + 클래스 응용: 다항식 클래스

- **다항식의 일반적인 형태**

$$
p(x) = a_nx^n + a_{n-1}x^{n-1} + \cdots + a_1x + a_0
$$

  - 어떤 자료구조가 다항식의 연산을 편리하게 할까?

- **다항식을 위한 자료구조?**
  - <span style="color:blue">배열을 사용하는 방법</span>
    - 다항식의 모든 항을 배열에 저장
  - 연결 리스트를 사용하는 방법
    - 희소 다항식에 적합
      - <span style="color:blue">희소 다항식:</span> 다항식의 0이 아닌 항만을 배열에 저장

## 배열을 이용한 다항식 클래스

- **배열을 이용한 다항식 클래스**
  - 모든 차수에 대한 계수 값을 배열로 저장
  - 하나의 다항식을 하나의 배열로 표현

<p align="center">
<img src="/assets/img/blog/polynomial_class_using_array.png">
</p>

## Polynomial 클래스 설계

- **다항식 클래스를 사용하는 코드의 예**

<p align="center">
<img src="/assets/img/blog/polynomial_class.png">
</p>

## Polynomial 구현 (C++)

~~~cpp
#define MAX_DEGREE 80 // 다항식의 처리 가능한 최대 차수 + 1
class Polynomial {
  int degree;             // 다항식의 최고 차수
  float coef[MAX_DEGREE]; // 각 항에 대한 계수
  public:
    Polynomial() {degree = 0;}    // 생성자: 최대 차수를 0으로 초기화

    // 다항식의 내용을 입력받는 함수
    void read() {
      printf("다항식의 최고 차수를 입력하시오: ");
      scanf("%d", &degree);
      printf("각 항의 계수를 입력하시오 (총 %d개): ", degree + 1);
      for (int i = 0; i <= degree; i++)   // 방법1로 계수 저장
        scanf("%f", &coef[i]);
    }

    // 다항식의 내용을 화면에 출력하는 함수
    void display(char *str = " Poly = ") {    // 디폴트 매개변수 사용
      printf("\t%s", str);
      for (int i = 0; i < degree; i++)
        printf("%5.1f x^%d + ", coef[i], degree - i);
      printf("%4.1f\n", coef[degree]);
    }
};
~~~

## Array 분석

- **Array 연산 및 시간 복잡도**
  - create(n): $$O(n)$$ (n개의 메모리 공간을 확보하고 초기화)
    - int A[10] = {0,1,2,3,4,5,6,7,8,9};
  - retrieve(i): $$O(1)$$
    - A[i]
  - store(i, item): $$O(1)$$
    - A[i] = 10;

- **단점**
  - Array는 크기가 고정되어 지정된 개수 이상의 원소를 가질 수 없음

## Vector in STL

- **Array의 클래스 버전**
  - 프로그램 실행 중에 크기가 달라 질 수 있음
  - 저장하려는 자료형을 지정할 수 있음(template)

- **vector의 주요 연산 (\#include \<vector\>)**
  - std::vector<span style="color:lime">\<data_type\></span> name;
  - std::vector<span style="color:lime">\<data_type\></span> name(size);
  - name.size()
    - 항목의 개수를 반환
  - name.empty()
    - vector가 비었으면 true, 아니면 false를 반환
  - name.push_back(item)
    - 입력 item을 vector의 제일 뒤에 push
    - $$O(1)$$ time in worst cases
  - Access: name[index]
    - name 이라는 vector의 index에 접근/값 반환
    - $$O(1)$$ time in worst cases
  - Insert: name.insert()
    - 지정된 위치에 item 삽입(지정된 위치 다음의 기존 item들은 뒤로 한 칸씩 밀림)
    - $$O(n)$$ time in worst cases
  - Delete: name.erase()
    - 지정된 위치의 item 삭제(지정된 우치 다음의 기존 item들은 앞으로 한 칸씩 댕겨짐)
    - $$O(n)$$ time in worst cases
  - API 문서
    - <a href="https://en.cppreference.com/w/cpp/container/vector">https://en.cppreference.com/w/cpp/container/vector</a>

## Vector 사용 예

~~~cpp
#include <vector>
using namespace std;

int main()
{
  vector<double> vec;
  vec.push_back(10.0);
  vec[0] = 20.0;
  printf("%f\n", vec[0]);

  return 0;
}

#include <vector>
using namespace std;

int main()
{
  vector< vector<double> > vec(10);
  for(int i = 0; i < 10; i++)
    vec[i] = vector<double>(10);

  for(int i = 0; i < 10; i++) {
    for (int j = 0; j < 10; j++)
      printf("%f ", vec[i][j]);
    printf("\n");
  }

  return 0;
}
~~~

## What You Need To Know

- **클래스 문법**
  - How to define? &rarr; use <span style="color:blue">class</span> keyword
  - Memberships &rarr; <span style="color:blue">public</span>, <span style="color:blue">private</span>, <span style="color:blue">protected</span>
  - Constructor & Destructor
  - Inheritance & Polymorphism

- **Vector in STL**
  - Vector의 개념과 사용법