## 5. 다형성

// **제일 중요, 객체지향은 다형성까지 계속 복습!!, 이해해야 추상 클래스, 인터페이스 이해 가능**

- 사전 정의: 여러 가지 형태를 가질 수 있는 능력
- **조상 타입 참조 변수로 자손 타입 객체**를 다루는 것!

```java
ex)
class Tv{ .....
     }

class smartTv extends Tv{
....
      }

원래 Tv t = new Tv(); 
//이렇게 타입 일치하는 것으로 인스턴스를 만들었다. 
// 하지만 다형성은 Tv t = new Smart Tv(); 같이 
// 타입 불일치여도 ok 한다는 뜻이다. 
// tv 리모콘으로 스마트 tv를 다룬다. (타입 불일치)
// 다만 t로 smartTV만의 멤버는 사용 불가! 공통되는 것만!

==> 조상 Tv 타입 참조변수 t로 자손 타입 smartTv 객체를 다룬다.
```

![다형성.    타입의 일치와 불일치의 차이](https://blog.kakaocdn.net/dn/bFFty5/btrdJ4hJZUj/qdzV8dXe57rOBRxcA0xmIK/img.png)

다형성.    타입의 일치와 불일치의 차이

- 설명
    - 참조변수가 조상 vs 자손 타입의 차이
        
         - 참조변수로 사용할 수 있는 멤버의 개수 상이 
        
        // 1번의 경우 7개 기능을 모두 사용 가능. 2번은 tv 리모콘에 정의된 5개의 멤버밖에 사용 못한다. 실제 멤버가 7개여도 그중에 일부만 사용할 수 있는 것
        
    - 자손 타입의 참조변수로 조상 타입의 객체를 가리킬 수는 없다. Smart Tv s = new Tv(); 불가
        
        // 버튼이 7개인데, 기능은 5개. 버튼을 눌렀는데 없으니까, **없는 것을 호출해서 에러** 발생.  멤버 개수가 많은데 조금 사용은 ok, 그 반대는 안 된다.
        
    

- 타입의 불일치로 인한 두 가지 장점이 있다(이는 객체에서 굉장한 유연함을 준다)

## 5.2 참조변수의 형변환

- (조상, 자손끼리만 가능!) # 객체, 주소 모두 그대로이다.
- 결론: 사용할 수 있는 멤버의 개수를 조절하는 것
    
    ex) 기본형 형변환은 float 3.6 -> int 3처럼 값이 바뀐다. 그런데 참조변수의 형변환은 주소 값이나 객체 이런 거 바뀌지 않고 멤버 개수만 달라진다. 기본형처럼 값이 달라지는 게 아니다.
    
- **조상 자손 관계의 참조변수는 서로 형변환 가능**(형제끼리 x)
    
    - 대입 연산자 시, 양변이 타입이 맞지않을  (타입) 적어준다. 
    
    - 생략 가능, 불가능은 신경쓰지말자. 그냥 써주자.
    

![참조변수의 형변환. car c = (car) f; 를 하면 f의 주소가 c에 복사되고, c는 f처럼 같은 객체를 가리킨다. 다만, c타입은 멤버가 4개이기에 5개 중 4개만 다룰 수 있게된다.](https://blog.kakaocdn.net/dn/xOem1/btrdFm4Y0vt/B0cGbIO7Y2326kF4nSuMuK/img.png)

참조변수의 형변환. car c = (car) f; 를 하면 f의 주소가 c에 복사되고, c는 f처럼 같은 객체를 가리킨다. 다만, c타입은 멤버가 4개이기에 5개 중 4개만 다룰 수 있게된다.

- 설명
    
    - f2 에서는 다시 c의 주소를 복사하고, 멤버도 다시 5개로 바뀐다. (**리모컨의 변화**로 객체에서 사용할 수 있는 멤버를 줄였다 늘렸다 하는 것이다)
    
    - Car c = null; 이면 주소값이 null
    
    - 5개 멤버를 가진 객체를 4개 멤버를 가진 타입으로 형변환하면 멤버는 5개이나 1개를 못 쓰는 것이지, 5개로 형변환하면 다시 사용가능한 것! -> 조상에서 자손타입으로 형변환 할 때는 형변환 생략 불가(불안전한 형변환)
    
    - 자손, 조상 모두 객체 없이 null 이여도 서로 형변환 가능. 다만, 멤버 메서드 실행 시 에러.
    

- 형변환할 때 중요한 것은 **실제 인스턴스가 뭔지** 알아야한다. (멤버가 몇 개인지, 사용가능 멤버는 몇 개인지)
    
    - 객체의 멤버 개수를 넘으면 안 된다. 이것만 넘지 않고 줄이고 늘리는 것은 괜춘. 조상->자손 에러 여부는 실체 객체가 결정한다.
    

ex)

```java
car 가 멤버 4개, fireeninge 5개(자손)

car c = new Car();
FireEngine fe = (FireEngine) c; 
//컴파일이 아니라 형변환 실행 에러 (classcastexception)
fe.water(); 
//컴파일 오케이 why? 형변환 타입만 잘 쓰면 객체 상관없이 통과된다. +리모컨 버튼에 있으니까

=> 그래서 실제 객체가 중요하다.
```

## 5.3 instanceof 연산자

(형변화 하기 전에 무조건 거쳐야한다)

- 참조변수의 형변환 가능여부 확인에 사용, 가능하면 true 반환
- 참조변수가 참조하고있는 인스턴스의 실제 타입을 파악하기위해
- 형변환 전에 반드시 이 연산자로 확인
    
    // 형변환 이유: **인스턴스의 원래 기능을 모두 사용**하려고!
    

 - **참조변수 instanceof B타입** 은 A가 B를 가리키냐고 생각할 수도 있는데, 조상인 경우도 true로 반환된다.

![instanceof 연산자 사용 예제, 조상에 해당되어도 instanceof 연산자 true 나온다. (주의) FireEngine 클래스는 Object, Car클래스의 자손 클래스여서 인스턴스 포함!!!](https://blog.kakaocdn.net/dn/cEB0nt/btrdInCk199/mPKWtwMQQuzKvBC3RjnDc1/img.png)

instanceof 연산자 사용 예제, 조상에 해당되어도 instanceof 연산자 true 나온다. (주의) FireEngine 클래스는 Object, Car클래스의 자손 클래스여서 인스턴스 포함!!!

==> **true가 나오면, B 타입으로 형변환 가능하다는 소리**이다. 

ex) Object obj = (Object) fe / Car c = (Car) fe

- 참조변수와 인스턴스의 연결

 - 조상 타입으로 자손 객체 참조, 자손 타입으로 자손객체 참조를 할 때, 같은 이름으로 정의된 메서드는 실제 참조된 메서드(오버라이딩된 메서드)가 호출되지만, 조상과 자손에서 같은 이름으로 정의된 변수는 결과가 다르다! ⇒ 조상→자손 참조의 경우, 조상 변수가 나온다!!!

## 5.5 매개변수의 다형성

- 다형성의 장점
    
     1. 다형적 매개변수 
    
     2. 하나의 배열로 여러 종류 객체 다루기
    

- 다형적 매개변수: 참조형 매개변수는 **메서드 호출시, 자신과 같은 타입 또는 자손타입의 인스턴스를** 매개변수로 넘겨줄 수 있다.
- ex)
    
    ```java
    class Product {
        int price; //제품의 가격
        int bonusPoint; //제품 구매시 제공하는 보너스 점수
    
        Product(int price) {
             this.price = price;
             bonusPoing = (int)(price/10.0);
    				// 보너스 점수는 제품가격의 10%
         }
    }
    
    class Tv1 extends Product {
          Tv1() {
                super(100);
           }
          // object클래스의 toString()을 오버라이딩한다.
          public String toString() { reutrn "Tv"}
    }
    
    class Computer extends Product{
           Computer() {
    						super(200);
    			}
           public String toString() { return "Computer";}
    } // sop를 할 때, 출력되는 것
    
    class Buyer { //고객, 물건을 사는 사람
          int money =1000;
          int bonusPoint = 0;
    
          void buy(Product p){
                if(money < p.price) {
                sop("잔액 부족“);
                return;
           }
    
          money -= p.price;
          bonusPoint += p.bonusPoint;
          sop(p.toString()+ "을 구입“);
    
    class Ex7_8
       public static void main(String args[]) {
            Buyer b = new Buyer();
    
            b.buy(new Tv1());
    // => 이제, buy 매개변수에 Tv1을 넣으면, Tv가격은 100만원(super 100 이기에). 조상 클래스의 Product 메서드 호출! 
    // 그러면 Tv 인스턴스의 price는 100, bonuspoint는 10 이 되는 것. 그리고 다시 void 메서드로 가게되면 잔액, 보너스포인트, 구입했다가 나온다.
    // b.buy(new Tv1()); 은 **Product p = new Tv1(); 과 b.buy(p);**를 한 줄로 만든 것과 같다. 
    // 대신 차이점은, 참조변수가 없기에 메인메서드 안에서는 사용 못하나, buy 메서드 안에서는 사용 가능 
    
            b.buy(new Computer());
    
            sop("현재 남은 돈은“ + b.money + "만원입니다”);
            sop("현재 보너스점수는“ + b.bonusPoint + "점입니다.”);
         }
    }
    ```
    

// public String toString() {} 은 p 혹은 p.toString() 으로 표현하여 호출할 수 있다.

- print 메서드는 매개변수에 toString()을 호출하여 문자열을 얻어 출력한다.

```java
public void print(Object obj) {
	write(String.valueOf(obj)); // valueOf() 가 반환한 문자열 출력
}

public static String valueOf(Object obj){
	return (obj == null) ? "null" : obj.toString(); //문자열 반환
}
```

## 5.6 여러 종류의 객체를 배열로 다루기

- 다형성의 두 번째 장점
    
     - 조상타입의 배열에 자손들의 객체를 담을 수 있다. 보통 배열은 하나의 타입만 되는데..
    

![부모타입 배열에 자손들의 객체 담기. 왼쪽 오른쪽 같지만 왼쪽은 변수를 개별적으로 쓴것, 오른쪽은 세 변수를 묶어놓은 product 배열. 다형성 때문에 타입이 달라도 자손들이 들어온다.](https://blog.kakaocdn.net/dn/c06rQa/btrdEjAJuG8/plQNXf40Ostbuyqpygf16k/img.png)

부모타입 배열에 자손들의 객체 담기. 왼쪽 오른쪽 같지만 왼쪽은 변수를 개별적으로 쓴것, 오른쪽은 세 변수를 묶어놓은 product 배열. 다형성 때문에 타입이 달라도 자손들이 들어온다.

![본격적으로 조상타입 배열이 만들어지고 자손 객체가 어떻게 연결되는지](https://blog.kakaocdn.net/dn/c5Tzpy/btrdK7SOAND/OYntDaDkPTxJuucLjzQmyK/img.png)

본격적으로 조상타입 배열이 만들어지고 자손 객체가 어떻게 연결되는지

// 처음에 cart (0x100 주소)로 10개 요소의 배열을 만든다. 

// 참조형 기본값은 null이니까, 각 요소는 null. 이후, p가 tv객체를 받을 때, p(0x200)이 주소값을 null인 요소에 넣게 되어 주소값 복사, tv객체를 가리키게된다.

// cart[i++] = p; // 배열에 차곡차곡 저장 ==> buy method안에 있다.

// p에 해당하는 게 인스턴스이니까 cart 배열에 인스턴스가 배열로!

- **Vector 클래스**
    - 가변 배열 기능을 갖고 있는 클래스. 이 클래스는 Object elementData[]; 과 같이 오브젝트 배열을 갖고 있어서 모든 종류의 객체를 저장할 수 있다.(최고 조상이기에)
    - 원래 배열의 길이를 우리가 직접 관리해줘야해서 크기가 부족하면 새로운 배열 만들고 복사해야하는데, 이 클래스는 다 알아서 해준다.

```java
void summary() { //구매한 물품에 대한 정보를 요약해서 보여준다.
       int sum = 0; // 구입한 물품의 가격합계
       String itemList = “”; //구입한 물품목록

//반복문을 이용해서 구입한 물품의 총 가격과 목록을 만든다.
	   for(int I=0; i<cart.length; I++) {
        if(cart[i] ==null) break; //물건이 안 들어가는 경우
        sum += cart[i].price
        itemList += cart[i]+“, ”; 
				// cart[i]는 cart[i].toString() 과 같다.
				// ex) Tv, Computer, .... 이런 식으로 나온다.
```

## 6. 추상클래스, 추상 메서드

<aside>
💡 추상메서드⇒ 조상클래스에서 **선언부만을 작성하고, 주석을 덧붙여 어떤 기능을 수행할 목적으로 작성되었는지 알려주고 실제 내용은 상속받는 클래스에서 구현**하도록 비워둔다.

</aside>

- 추상클래스: 미완성 설계도, 미완성 메서드를 갖고있는 클래스(멤버가 적거나, 그냥 단순히 미완성 메서드면 미완성 설계)
- 미완성 메서드(추상 메서드): 구현부가 없는..., **abstract**을 앞에 붙여준다. 그러면 에러가 안 난다.다른 클래스 **작성에 도움**을 주기 위한 것. **인스턴스 생성 불가.**

![추상클래스, 구현](https://blog.kakaocdn.net/dn/4sEPr/btrdJ3pB9DT/nxPmJuDJAU2e26AK1YVSSK/img.png)

추상클래스, 구현

- 구현: 추상 메서드의 몸통을 만들어주는 것. 상속받은 추상 클래스 멤버를 다 구현한 것이 아니라면 계속 abstract! (이는 상속받고나서 내가 이 설계도를 완성해야하는 구나를 강제한다)

<aside>
💡 **ap 타입을 Player로 적어도 된다(다형성, 조상타입이니까. 참조변수는 리모콘이라 버튼만 제공, 몸통 없어도 된다. 리모콘하고 연결된 객체가 기능을 다 갖고있으면 된다)**

</aside>

 → 그리고나서 이  player 참조변수로 player.play를 호출하면 아래 완성된 메서드가 호출된다.

// 추상클래스 타입인데, 괜찮나 싶지만 가능하다!!

- 추상메서드
    
     - 미완성 메서드, 구현부(몸통, {})가 없는 메서드 ⇒ **`일단 선언부를 잘 짜는 게 중요!`**
    
     - abstract(제어자 중 하나) 리턴타입 메서드이름(); (세미클론으로 끝나야한다)
    
    언제 쓰냐? 자손마다 다르게 구현될 것으로 예상되는 경우(굳이 몸통 구현 필요x)
    
    “자손한테 player 라면 이 재생하는 플레이, 스탑 기능이 있어야 돼 이런 뜻. 그러니까 너희들은 상속을 통해서 이걸 너희한테 맞게 구현을 해서 몸통을 만들어 줘야 돼”
    
    - 객체를 생성해서(완성되서) 객체 참조변수.play를 하게되면 play(currentPos) 호출하게 된다. (**실제 객체가 가지고있는 메서드가 호출된다.**)
    

- 추상 클래스의 작성
    - `**추상화(클래스 간의 공통점 찾아내서 공통 조상) vs 구체화(상속을 통해 클래스 구현,확장)**`
    - 추상클래스를 단계별로 만들어놓으면 용이하다!! (마치 깃의 브랜치 하는 것처럼)
    - 여러 클래스에 공통적으로 사용될 수 있는 추상클래스를 바로 작성하거나 기존클래스의 공통 부분을 뽑아서 추상클래스를 만든다. (공통의 조상을 만드는것)

![추상메서드 예제. 호출할 때는 선언부만 있어도 된다. play(currentPos)는 나중에 완성되면[객체 생성 후] 호출될 수 있다. 단지 이렇게 작성되도 에러는 아니라는 뜻. void play()는 매개변수 없을 때의 play메서드이고, abstract void play(int pos)는 후손 클래스에서 구현하라는 의미! play메서드 오버로딩!](https://blog.kakaocdn.net/dn/bHrj4n/btrdFnbNAt5/HKsbkTXGP4mAIKtYeVDHiK/img.png)

추상메서드 예제. 호출할 때는 선언부만 있어도 된다. play(currentPos)는 나중에 완성되면[객체 생성 후] 호출될 수 있다. 단지 이렇게 작성되도 에러는 아니라는 뜻. void play()는 매개변수 없을 때의 play메서드이고, abstract void play(int pos)는 후손 클래스에서 구현하라는 의미! play메서드 오버로딩!

- ex) 공통된 부분을 빼서 추상클래스 활용
    
    ![추상클래스 활용(공통된 부분만 빼서)](https://blog.kakaocdn.net/dn/ysDrj/btrdJjGemjv/ZGK8CO6VUl1EwPag0kwnw0/img.png)
    
    추상클래스 활용(공통된 부분만 빼서)
    
     -  코드 중복이 있는 왼쪽을 오른쪽처럼 코드를 작성할 수 있다는 의미
    
     -  해군과 탱크, 비행선. 이들의 **공통된 부분**을 뽑아서 unit 추상클래스를 만들었다. move는 각자 달라질 부분! ==> 몸통은 달라도 선언부는 같으니까... ==> 상속받은 자손들이 int x, int y;를 따로 작성할 필요 없어져 간결해졌다. (코드의 중복 제거, 이게 객체 언어의 장점이다) 
    
    - abstract 안 쓰고 {}을 만들 수도 있지만 구현되어있다고 생각하고 호출할 수도 있기에!!
    

- ex) 추상클래스와 여러 타입 배열 다루기
    
    ![추상클래스를 통해 응용. 추상메서드를 호출하는 것이라 객체에 있는 메서드를 호출하는 것을 이용](https://blog.kakaocdn.net/dn/cTL3jH/btrdK6l4oLz/pEWcinitjr5gV5KBDq1f9k/img.png)
    
    추상클래스를 통해 응용. 추상메서드를 호출하는 것이라 객체에 있는 메서드를 호출하는 것을 이용
    
     - group 리모컨에 x,y,move,stop 버튼이 생긴다. 이 그룹은 unit [] group 의 그룹을!
    
     -  다형성의 두 번째 장점인 하나의 배열에 여러 객체를 집어넣는 것
    
     -  for문에서 각자 객체의 모습으로 호출.
    
     - **group[0], group[1], group[2](참조변수, 리모콘이다)의 타입은 Unit 이다!!!**
    
     - 타입을 Object로 바꿔도 여러 타입을 하나의 배열로 다룰 수 있지만, object에 move 메서드가 없기에 group[i].move에서 에러가 난다.
    

 - unit[] group = new unit[3]; (참조변수를 묶은 객체배열) group[0] = new Marine(); group[1] = new Tank(); group[2] = new Dropship(); 은 unit [] group = { new Marine(), new Tank(), new Dropship() }으로 줄일 수 있다.

 -  int 와 int 배열은 다른 것이다. int는 기본형, int 배열은 참조형이다.

- 추상화의 장점 : 구체화된 코드보다 유연, 변경에 유리

ex) Calender cal = calender.getInstance(); 

추상클래스 참조변수일 때 다형성으로 인해 자손 객체 담을 수 있다. Calender가 추상클래스일 때, getinstance를 통해 어떤 객체를 반환할지 모른다. 즉, 완성될 추상클래스의 자손 객체를 반환하여 cal 참조변수에 저장하게된다. 구체화되었으면 자손 객체 무엇으로 반환할지 일일이 case를 다 적어야하는데.. ===>> 차차 이해 필요

## 7. 인터페이스

- 결론(자바에서 인터페이스를 어떻게 쓰는 지에 대한)
    
     - (프로그래밍 관점에서)  추상 메서드의 집합
    
     - static 메서드, 상수, 디폴트 메서드도 포함은 되지만 부수적인 것. 일단 추상 메서드 집합이 핵심이다. 구현된 것이 전혀 없는 설계도(모든 멤버가 public)
    

![인터페이스는 껍데기. 바깥으로 노출되어있는](https://blog.kakaocdn.net/dn/bMvR4E/btrdEjObopm/U5Kky66k3RNKTYHlNJlWS1/img.png)

인터페이스는 껍데기. 바깥으로 노출되어있는

 -  iv 변수데이터를 객체에서 접근하려고 할 때 메서드를 통해서만 접근 가능(캡슐화), 그리고 이 때 껍데기를 인터페이스라고 한다.

 - `추상클래스와의 차이점`:  추상클래스는 추상메서드도 갖고 있는 것이라면(일부 미완성), 인터페이스는 추상메서드만 갖고 있다. (완전 미완성) => iv, 생정자, 인스턴스 메서드를 가질 수 없다.

```java
interface 인터페이스 이름{
           public static final 타입 상수이름 = 값; // 상수
           public abstract 메서드이름(매개변수 목록); // 추상 메서드
}
```

// 인터페이스 선언. interface 내 멤버들은 public static(멤버변수)/public abstract(메서드) 여야한다. 다만 생략가능(일부만 생략도 가능)! 항상 이거니까

- 인터페이스의 상속
    
     - 인터페이스의 조상은 **인터페이스만 가능**(object가 최고 조상 아님)
    
     - 다중 상속이 가능(조상이 여러 개) ex) interface Fightable extends Movable, Attackable{}
    
    // 왜 가능하냐? 선언부가 같을 수 있어서 충돌 가능성 있는데, 인터페이스는 선언부가 같으면 그냥 같은거임. 혹은 조상-자손 관계거나... //다만 거의 안 쓴다. 되도록 하나는 상속 다른 건 포함!!
    
     - 상속과 구현을 동시에도 가능 ex) class Fighter extends Unit implements Fightable {}
    

- 인터페이스의 구현
    
     - 인터페이스에 정의된 추상 메서드를 완성하는 것(이를 구현이라 한다)
    
    ```java
    class 클래스이름 implements 인터페이스이름{
            // 인터페이스에 정의된 추상메서드를 모두 구현해야한다.
    }
    => “..클래스는 ..인터페이스를 구현했다.” 라고 한다.
    
    // 추상클래스는 상속받아서 구현하는디. implements 는 extend와 이름만 다르다. 추상메서드 작성은 같다.
    ```
    
     - 일부만 구현하는 경우, 클래스 앞에 abstract을 붙여야한다!!
    

### 인터페이스를 이용한 다형성

- 인터페이스 타입의 매개변수가 갖는 의미는 메서드 호출 시 해당 인터페이스를 구현한 클래스의 인스턴스를 매개변수로 제공해야한다는 것

 - 그리고 인터페이스 타입의 참조변수로도 Object 클래스에 정의된 메서드들을 호출할 수 있다!

- 또한 인터페이스 타입을 메서드의 리턴 타입으로 사용 가능(자손 인스턴스를 return해서)

<aside>
🔥 **리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환한다는 의미이다.**

</aside>

```java
Interface Fightable {---}
class Fighter implements Fightable{---}

Fightable f = (Fightable) new Fighter();
또는
Fightable f = new Fighter(); 가능

=> 그래서 다음과 같이 메서드의 매개변수의 타입으로 사용 가능
void attack(Fightable f) {
 //....
} // 여기서는 Fightable을 구현한 Fighter 인스턴스를 매개변수로 제공한다. 
  // = void attack(new Fighter());

FIghtable method() {
   --
	Fighter f= new Fighter();
	return f;
} // 이와 같이 메서드의 리턴타입으로 인터페이스의 타입을 지정하는 것도 가능
```

## 7.7 인터페이스의 장점

- 인터페이스의 개념: 두 대상(객체)간의 ‘연결, 대화, 소통’을 돕는 ‘중간 역할’을 한다.
    
    `1. 사람과 컴퓨터 사이에서 껍데기 역할.` 
    
    - 컴퓨터를 조작하는 것보다 사람이 사용하기 편한 껍데기! 사람과 컴퓨터가 소통하기 쉬워진다. 
    
    ex) 윈도우 GUI(Graphic user interface) // 우리가 윈도우를 보는 것도
    
    + 변경에 유리. 컴퓨터가 다른 컴퓨터로 교체된다고 하면 또 조작법을 배워야하는데, 이런 껍데기가 공통적인 양식이기에... 껍데기는 인터페이스, 실제구현 내용을 감싸고 있다.
    
    `2. 선언(설계)와 구현을 분리시킬 수 있게 한다.` 
    
    (**변경에 유리**한 유연한 설계가 가능하다. )
    
    ![인터페이스를 통해 선언부와 구현부 분리](https://blog.kakaocdn.net/dn/PC9tQ/btrdDKkppTz/2PtmKVRKj66r6BWBRiaHV1/img.png)
    
    인터페이스를 통해 선언부와 구현부 분리
    
    - A 유저가 B 클래스를 사용한다고 할 때(A가 B에 의존), 즉 A가 껍데기를 보기 때문에, 알맹이가 바뀌어도 껍데기가 그대로면 사용에 아무 지장 없다. (사용에 영향x)
        
        // 기존에 구현되어있는 일반 클래스의 메서드를 선언부와 구현부로 분리시킬 수 있다. => 변경에 유리, 유연한 코드 ==> 이러한 인터페이스 덕분에 B(컴퓨터)가 변경되어도 A(유저)는 안 바꿀 수 있게 된다.
        
        ex) 윈도우창
        
    
    ![인터페이스의 장점 선언부, 구현부 분리. 왼쪽으로 쓰게 되면 수정할 때 귀찮아진다. 그래서 인터페이스 타입의 매개변수 다형성을 사용하는 것. 그리고 설계와 구현을 분리하기에 편리](https://blog.kakaocdn.net/dn/q5wKa/btrdFnW8cfz/qPaUST3nso5FcPbiVlqcQ0/img.png)
    
    인터페이스의 장점 선언부, 구현부 분리. 왼쪽으로 쓰게 되면 수정할 때 귀찮아진다. 그래서 인터페이스 타입의 매개변수 다형성을 사용하는 것. 그리고 설계와 구현을 분리하기에 편리
    
    - `과정에 대한 설명`
        
        // 왼쪽 코드의 경우, 클래스 A가 클래스 B의 메서드를 호출하고 있는 것이다.(이를 A가 B에 의존한다고 한다) 그리고 실행하기 위해 A객체 만들고, B 객체를 만들어서(B b = new B(); ) 매개변수로 삼아서 메서드 호출. B클래스를 변경하게되면 A도 변경해야하는 문제..
        
        // 오른쪽 코드의 경우, 클래스 A를 인터페이스 I의 메서드를 호출하는 것[I를 구현한 것들만 들어와라]으로 바꾸면 A와 B는 관계가 없다. 그리고 B가 인터페이스를 구현할 것이고, 나중에 B를 C로 변경해도 A에서 변경할 게 없어지는 것
        
    
    `3. 개발 시간을 단축할 수 있다.`
    
    - A(user)는 B(provider)를 사용하려고 하는데, B가 완성될 때까지 기다려야한다. 하지만 껍데기 I를 사용한다면 추상메서드 호출하는 코드 작성 가능. 이후에 구현하면 된다.
    
    `4. 표준화가 가능하다.` 
    
    ex) 클라와 서버가 있을 때, 서버의 변동이 있는 경우 클라에 변동이 많이 필요한데, 이들 사이에 인터페이스를 둔다. (이러한 양식이 있다=추상 메서드 규칙) 그리고 클라는 이 인터페이스만 있으면 된다. (인터페이스의 변화가 없다면) 각 서버는 인터페이스 표준에 맞게 개발한다.
    
    `5. 서로 관계없는 클래스들을 관계 맺어줄 수 있다.`
    
    ![서로 관계없는 클래스들을 관계 맺는다.](https://blog.kakaocdn.net/dn/QozgI/btrdJ3wlTmg/rviR6uOTIW8UKI4r6JymX0/img.png)
    
    서로 관계없는 클래스들을 관계 맺는다.
    
    // 상속 관계로 맺어줄 수 없거나 같은 조상클래스가 아닌 SCV, Tank, Dropship을 관계 맺어준다.
    
    ⇒ implements Repairable 을 통해 같은 인터페이스를 구현했다는 공통점을 만들어 준다. 
    
    // 관계있는 것들 혹은 조상으로 관계를 맺으면 관계없는 건 배제되거나, 관계있지만 제외하고 싶어도 불가함. => 새로운 조상인 인터페이스 활용. 이를 통해 같은 메서드의 매개변수를 인터페이스 타입으로 사용 가능. 
    
    - 이후
    
    ```java
    void repair(Repairable r) { 
    //Repairable을 구현한 애들만 들어올 수 있다. Repairable은 interface이름.
          if (r instanceof Unit) { // Unit 타입의 자손만
               Unit u = (Unit) r; //변수 구분
               while(u.hitPoint ! = u.MAX_HP) {
                      u.hitPoint++;
          }
    }
    ```
    

- 같은 조상클래스를 갖고있으나, 일부에게만 적용되는 메서드를 추가하고자한다면?

 - 인터페이스 생성 → 구현한 A 클래스를 내부에 포함시켜서 추가된 메서드 호출 가능해진다!

 = > **`여러 클래스에 같은 내용의 코드를 작성할 필요없이 A클래스에서 관리`**할 수 있다!

- 기타

 - getInstance() 를 통해 인스턴스를 제공받을 수도 있다. 이 때도 다형성 사용 가능!!


## 7.9 디폴트 메서드와 static 메서드

 - 인터페이스에 디폴트 메서드, static 메서드 추가기능(JDK 1.8부터)

 - 인터페이스에 새로운 메서드(추상 메서드)를 추가하기 어려움. => 새로운 메서드를 추가하게 되면, 인터페이스에 이미 구현한 기존 클래스들이 이 새로운 메서드를 다 구현해야하는 문제...

## 해결책 => 디폴트 메서드: 인스턴스 메서드(인터페이스 원칙 위반. 예외사항)

// 새로운 추가한 메서드를 default 앞에 붙이고 추상메서드와 달리 {} 몸통 만들어준다. 그러면 이미 구현한 클래스들이 짐을 덜 수 있다.

- 디폴트 메서드가 기존의 메서드와 충돌할 때의 해결책 // 아리송....
    
    (1) 여러 인터페이스의 디폴트 메서드 간의 충돌: 구현한 클래스에서 디폴트 메서드를 오버라이딩
    
    (2) 디폴트 메서드와 조상 클래스의 메서드 간의 충돌: 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다.
    

## 8. 내부 클래스

 - 사용빈도가 높지않아서 그냥 내부 클래스의 기본 원리와 특징을 이해하는 정도까지만

- 내부 클래스: 클래스 내에 선언된 클래스(서로 긴밀한 관계에 있기에)
    
     - 두 클래스의 멤버들 간에 서로 쉽게 접근, 외부에 불필요한 클래스 감춤(캡슐화)
    


- 내부 클래스의 제어자와 접근성


- 인스턴스 멤버는 static 멤버에 접근 가능하나, 그 반대는 안된다.


- 내부클래스는 외부클래스와 달리, class 앞에 4가지 제어자 모두 사용 가능. 내부 클래스에는 변수는 안되고 상수만 가능.


- 익명 클래스

 - 이름이 없는 일회용 클래스, 정의와 생성을 동시에