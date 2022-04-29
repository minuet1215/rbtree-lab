# 중첩 구조체 (Nested Structure)

## 1. 중첩 구조체
- 이미 선언된 구조체를 또 다른 구조체의 멤버로 선언

```C
struct first
{ // first 구조체 선언
    int a;
    int b;
};
    
struct second { // second 구조체 선언
    struct first sa;  // first 구조체 변수를 멤버로 가지는 선언 
    struct first sb;
    // 변수 선언이 아닌 멤버 선언 (초기화가 불가능)
};
```

> 메인 함수에서 구조체 변수를 second ns와 같이 선언하면 나중에 선언한 second 구조체에는 먼저 선언한 first 구조체의 변수를 가지는 second 구조체 멤버가 생성됨
```C
int main() {
    second ns;
}
```

<hr>

## 2. 중첩 구조체 사용
### 중첩된 구조체 변수의 멤버 구성 요소
- 메인 함수에서 선언한 second ns는 변수 ns안에 sa가 들어 있고 sa 안에 a가 들어있는 구조체 변수의 멤버 구성 요소를 가직ㅁ
- 중첩된 구조체는 구조체 멤버가 또 다른 구조체 멤버를 포함하는 구조
- 중첩된 구조체 멤버에 접근하기 위해서는 구조체 연산자인 점(.)을 두 번 사용해야 함

```C
ns.sa.a = 10;
ns.sa.b = 20;
...
```
