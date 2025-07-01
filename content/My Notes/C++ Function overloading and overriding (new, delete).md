---
title: C++ Function overloading and overriding (new, delete)
draft: false
tags:
  - cpp
aliases:
  - Function overloading and overriding (new, delete)
---
## 메모리 관리의 필요성
**스택(Stack) vs 힙(Heap)**
- **스택**: 컴파일 시에 크기가 결정되는 메모리 영역. 컴파일러가 자동으로 관리해주어 안전하지만, 크기가 제한적이고 유연성이 떨어짐.
- **힙**: 프로그램 실행 중에 동적으로 할당/해제할 수 있는 메모리 영역. 유연하지만 개발자가 직접 관리해야 하므로 책임이 따름.
## C vs C++의 메모리 할당 방식
**C언어**
```c
int* ptr = malloc(sizeof(int));  // 메모리 할당
*ptr = 10;
free(ptr);                       // 메모리 해제
```

**C++**
```cpp
int* ptr = new int;     // 메모리 할당
*ptr = 10;
delete ptr;             // 메모리 해제

// 또는 초기값과 함께
int* ptr = new int(10); // 10으로 초기화하며 할당
delete ptr;
```

## new와 delete의 장점
1. **타입 안전성**: new는 할당하는 타입을 알고 있어서 적절한 크기를 자동 계산
2. **생성자/소멸자 호출**: 객체를 생성할 때 생성자가, 삭제할 때 소멸자가 자동 호출
3. **문법의 간결성**: malloc보다 사용하기 편리

## 배열 할당
```cpp
int* arr = new int[10];    // 10개 정수 배열 할당
delete[] arr;              // 배열 메모리 해제 ([]에 주의!)
```

---
## Reference
[모두의 코드. ch3. C++의 세계로 오신 것을 환영합니다. (new, delete)](https://modoocode.com/169)

## Next
[[]]