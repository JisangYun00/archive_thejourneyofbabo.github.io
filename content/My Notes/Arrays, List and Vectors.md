---
title: Arrays, List and Vectors
draft: false
tags: 
aliases:
---
## Basic of Array and List
### Array(배열) - array[ ]
메모리의 연속 공간에 값이 채워져 있는 형태의 자료구조. 인덱스를 통해 참조 가능.
선언한 자료형의 값만 저장 할 수 있다.
### 배열의 특징
- 인덱스를 사용해 값에 바로 접근할 수 있다.
- 새로운 값을 삽입하거나 특정 인덱스에 있는 값을 삭제하기 어려움.  
  삽입 혹은 삭제하려면 주변 값을 이동시키는 과정 필요
- 배열의 크기는 선언할 때 지정. 한번 선언 후 늘리거나 줄일 수 없다.
- 구조가 간단
### List
값과 포인터를 묶은 노드라는 것을 포인터로 연결한 자료구조
### List의 특징
- 인덱스가 없으므로 값에 접근하려면 Head 포인터 부터 순서대로 접근해야함.  
  접근 속도 느림.
- 포인터로 연결 -> 데이터 삽입 삭제 연산 속도 빠름
- 선언 시 별도 크기 지정안해도 됨. 크기가 변하기 쉬운 데이터 다룰 때 적절
- 포인터를 저장할 공간 필요 -> 배열보다 구조 복잡

## Vector!!
**기존의 배열과 같은 특징을 가지면서 배열의 단점을 보완한 동적 배열의 형태**  
### Vector의 특징
**사용하기 편리하고, 쉬움**
- 동적으로 원소를 추가할 수 있다. 크기가 자동으로 늘어남
- 맨 마지막 위치에 데이터를 삽입하거나 삭제할 때 문제 X.   
  중간 삽입 삭제는 배열과 같은 메커니즘으로 동작.
- 배열과 마찬가지로 인덱스를 이용해 각 데이터에 접근.
### Vector example code
```c++
#include <iostream>
#include <ostream>
#include <vector>
using namespace std;
int main() {
  vector<int> A;
  A.push_back(10);
  A.push_back(30);
  A.push_back(5);
  A.push_back(8);
  A.push_back(8);

  A.push_back(1);
  A.insert(A.begin(), 7);
  A.insert(A.begin() + 2, 10);

  A[4] = -5;

  A.pop_back();
  A.erase(A.begin() + 3);

  cout << A.size() << endl;
  cout << A.front() << endl;
  cout << A.back() << endl;
  cout << A[3] << endl;
  cout << A.at(5) << endl;
}
```
