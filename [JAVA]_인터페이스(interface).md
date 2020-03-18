# 인터페이스(interface)





### 인터페이스란?

---

> 코드와 인스턴스를 연결하는 접점



![2275244E57B6DBEC16](https://user-images.githubusercontent.com/58682321/76967990-89a60f00-696b-11ea-8a27-4613a91b87f6.png)



- JAVA 에서의 인터페이스는 기본적으로 **추상(abstract) 메서드 모음**이라고 할 수 있다. 즉, **구현부가 존재하지 않는 메서드의 집합체**이다.

  ```java
  public interface Birds {
  
      public void fly();
      void run();
      ...
      
  }
  ```

  **※ 인터페이스의 기본 접근 제어자는 `public` 이다.**





### 인터페이스 구성 멤버

---

> 인터페이스는 기본적으로 **상수**와 **추상메서드**로 구성된다.

(※ JAVA 8 부터는 `default 메서드`와 `static 메서드` 또한 인터페이스의 멤버로 추가되었음)



```java
public interface Birds {	
// 접근제어자는 public 또는 default만 올 수 있다.
    
    String name;
    //[public static final] String name; 
    
    public void fly(); // [public abstract] void fly();
    
    void run();	// [public abstract] void run();
    
    public void move(int x); // [public abstract] void move(int x);
    
    
    
}
```

- **멤버 변수)** 
  - **상수 필드만 선언 가능**, 컴파일 과정에서 자동으로 **public static final**이 생성
- **추상 메서드)**
  -  **구현부**가 없고 **타입, 메서드명, 매개 변수**로만 정의된 메서드, 자동으로 **public abstract**  생략





### 인터페이스 구현

---



```java
class Eagle implements Birds {
    
   //...
 
   
   @Override
   public void fly() {
       System.out.println("I'm flying");
   }
    
   @Override
   public void run() {
       System.out.println("I'm running")  
   }
   
    @Override
    public void move(int x) {
        System.out.printf("최고 속력 : %s", x);
    }
  
}

public class Animal {
    public static void main(String[] args) {
        
        Eagle eagle = new Eagle();
        
        eagle.fly();
        eagle.move(100);
    }
    
}
```

- **인터페이스 자체**로는 **인스턴스를 생성할 수 없다.**

- **상속 받는 하위 클래스**에서는 반드시 인터페이스 내에 존재하는 **추상 메서드를 구현해야 한다.**

  - **중요)** 만약 **인터페이스 메서드 중 일부만 구현**한다면, **추상(abstract) 클래스로 선언**해야 한다.

  

- **인터페이스의 추상메서드**에는 `public`이 **생략**되어 있을 수도 있기 때문에 `@Override`을 할 때, `public`을 반드시 명시해야 한다.





### 인터페이스 특징

---



- **추상 클래스 내**에는 **구현부**가 있는 메서드가 존재할 수 있다.

```java
public abstract class AbstractEx01 {
    
    public abstract void display(); // 구현부가 존재하지 않는 추상 메서드
    
    void display() {
        System.out.println("Hello!") // 구현부가 존재하는 메서드
    }
}
```



- **인터페이스 간**에는 **다중 상속**이 가능하다.

```java
public interface Dog {
    void bark();
}

public interface Cat {
    void mew();
}

public interface Animal extends Dog, Cat {
    
    @Override
    public void bark() {
        //...
    }
    
    @Override
    public void mew() {
        //...
    }
    
}
```

**※ 클래스 간에는 단일 상속만 가능하다.**

