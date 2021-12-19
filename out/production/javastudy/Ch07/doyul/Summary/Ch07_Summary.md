# Ch07. 객체지향 프로그래밍 II
-----------------
## 1. 상속(inheritance) 
### 1.1 상속의 정의와 장점      // 그림 도 그릴 수 있어야함
* 기존의 클래스로 새로운 클래스를 작성(코드의 재사용)
* 두 클래스를 부모와 자식으로 관계를 맺어주는 것
* 자손은 조상의 모든 멤버를 상속 받는다.(생성자, 초기화 블럭 제외)
* 자손의 멤버 개수는 조상보다 적을 수 없다.(같거나 많다)
* 자손의 변경은 조상에 영향을 미치지 않는다.
```java
    class Parent {                  //부모클래스 : 멤버 1개
        int age;                    
    }                               //상속 관계
    class Child extends Parent {    //자식클래스 : 멤버 2개
        void play() {               //자신의 멤버 1 개
            System.out.println("Let's play~!")
        }                                
                                    //상속받은 멤버 1개
    }   
```
### 1.2 클래스간의 관계 - 포함관계
* 클래스의 멤버로 참조변수를 선언하는 것
* 작은 단위의 클래스를 만들고, 이 들을 조합해서 클래스를 만든다.
* 저장 공간은 같으나 구조적 차이 발생 // * 그림 추가하기
### 1.3 클래스 간의 관계 결정하기
* 대부분 포함으로 진행
* 상속관계 : '~은 ~이다.(is - a)'
  - 원은 점이다.
* 포함관계 : '~은 ~을 가지고 있다.(has -a)'
  - 원은 점을 가지고 있다. 더 자연스러움.
   