# Singleton


- Singleton 클래스는 **생성자**와 **getInstance()** 의 메서드를 포함한 클래스이다. **하나의 해당 클래스에서 단 하나의 인스턴스만 만들도록 보장하는 방법을 싱글톤 패턴이라고 한다.**
- 간단한 예제를 통해 **Singleton 패턴**에 대해서 알아보도록 한다.



### Normal(singleton과 비교하기 위해 생성한 클래스)

> **생성자 함수, Default Constructor**

```java
package test1;

public class Normal {

    public Normal() {
        System.out.println("public");
    }
    
    
    // public Normal() {} : Default Constructor 자동 생성
    // 생성자 함수를 별도로 설정해두지 않으면 위와 같은 생성자가 default로 생성된다.
}
```




**- 사용자가 생성자 함수를 정의하게 되면, Default 생성자는 더 이상 자동으로 생성되지 않는다.**

**- 생성자는 반드시 클래스 이름과 같아야 하며, 앞에는 접근 제어자(public, private, protected.. )만 올 수 있다.** 

**- 생성자는 상속되지 않으므로 abstract, final 등의 수식어를 가질 수 없고, 객체 생성시에만 호출되기 때문에 static일 수 없다. 또한 메서드가 아니기 때문에 반환 값은 void 도 허용되지 않는다.**



### Singleton

> **private, static, getInstance()**

```java
package test1;

public class Singleton {

    private static Singleton singleton = new Singleton(); // 자신의 인스턴스 생성
    //private: 외부에서 생성자를 호출할 수 없도록 제한,  private로 생성된 생성자는 스스로 호출 가능
    //static을 통해 정적 필드를 선언하고, 자신의 인스턴스를 생성하여 초기화
    
    private Singleton() {
        System.out.println("Singleton");
    }
    // 외부 클래스에서 값을 변경하지 못하도록 생성자 호출 제한(private)

    public static Singleton getInstance() {
        return singleton;
        // 변수명을 static으로 설정하였기 때문에, static method에서 사용가능
        // 생성한 인스턴스 리턴
    }

}
```



\- **Private:** **Singleton** 클래스에서 생성자 함수를 **private**로 설정하였기 때문에, **Main** 클래스에서 **new**를 이용하여 객체를 생성할 수 없다. 




\- **Static: 인스턴스 생성**과 **getInstance() 메서드**에 **static**이 추가되었다.

- JAVA 파일의 **field 부분에서 선언된 변수(전역 변수)**와 **정적 멤버변수(static이 붙은 자료형)**를 **Static 영역에 데이터를 저장**한다. 또한 저장된 데이터는 프로그램이 종료될 때 까지 어디서든 사용이 가능하다.
  (※ 하나의 메모리 공간이 할당되어 어디에서 선언되더라도 그 클래스 내에서는 공유된다.)

- static 으로 선언한 메서드 내에서는 static으로 선언한 변수를 제외하고 접근이 불가능 하다.

  - 인스턴스 생성 시 **static 메서드**로 선언했기 때문에, **getInstance() 메서드**에서 return 가능
  
  

\- **getInstance(): 이 메서드**는 **public**으로 선언했기 때문에 이를 통해 **Singleton** 클래스에 접근이 가능하다. 

- 해당 클래스에서 **singleton 인스턴스**는 최초 실행 시 한번만 생성된다. 이 때, **getInstance() 메서드**는 그 인스턴스를 return 하기 때문에, 호출할 경우 또 다른 인스턴스를 생성하지 않고, **기존의 인스턴스를 반환**한다. 



### Main

> **생성자 호출**

```java
package test1;

public class Main {
    public static void main(String[] args) {

        Normal normal1 = new Normal(); // 인스턴스 생성 및 호출
        Normal normal2 = new Normal();


        Singleton singleton1 =  Singleton.getInstance();
        // 최초 호출 이 때, Singleton의 new 연산자를 통해 객체가 생성된다.
        Singleton singleton2 =  Singleton.getInstance();
        // 기존에 생성된 객체를 반환한다.

        if (normal1 == normal2) {
            System.out.println("normal1 == normal2");
        } else {
            System.out.println("normal1 != normal2");
        }

        if (singleton1 == singleton2) {
            System.out.println("singleton1 == singleton2");
        } else {
            System.out.println("singleton1 != singleton2");
        }
    }
}

------------------------------------------------------------------
public
public
Singleton
normal1 != normal2
singleton1 == singleton2
```

\- **Normal** 클래스는 **public** 으로 생성했기 때문에 **new** 연산자를 이용해 외부 클래스에서 생성할 수 있다. 또한 **static**으로 선언하지 않았기 때문에 서로 다른 메모리 주소 값을 가진 인스턴스가 생성된다.

\- 최초 **getInstance()** 가 호출되면, **Singleton**클래스 내에 있는 **new** 연산자에 의해 생성된 인스턴스(변수 명 : singleton)가 호출된다. **static 메서드**로 선언했기 때문에 같은 메모리 주소 값을 공유한다.





**Singleton 패턴의 장점?**

---

\- new 연산자를 통해 **인스턴스를 한 번만 생성(메모리 공간 공유)** 하기 때문에, 메모리의 낭비를 줄일 수 있다.

\- **공통된 객체를 사용해야하는 경우** 매번 객체를 생성하지 않아도 되기 때문에 성능면에서 좋다.




