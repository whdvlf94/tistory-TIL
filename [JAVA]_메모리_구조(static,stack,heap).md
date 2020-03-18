# 메모리 구조 - static/stack/heap



## static (data 영역)

- JAVA 파일은 크게 **필드(Field), 생성자(Constructor), 메서드(Method)로 구성**되어 있다. 이 때, `static` 키워드가 붙은 **필드(Field) 부분에서 선언된 변수(전역 변수)**  또는 **메서드**는 **정적(static) 멤버** 이며, **data 영역**에 저장된다.
- **data 영역**에 저장되어 있는 데이터는 **프로그램 종료 시 까지 메모리에 남아있다.**



```java
package test4;

public class Static {

    static int Count;   // 정적 필드
    int a;  // 인스턴스 필드

    public Static() {
        this.Count ++;
        this.a ++;
        System.out.printf("Count : %s\t", this.Count);
        System.out.printf("a : %s\n", this.a);

    }

    public int display() {
       return a;
    }

    public static int getCount() {
        return Count;
    }


    public static void main (String[] args) {
        System.out.println(Count);
        // Static 클래스 정적(field) 필드 사용 가능
        // System.out.println(a);  Static 클래스 인스턴스 필드 사용 불가능
        Static st1 = new Static();
        Static st2 = new Static();

        st1.display();
        // 인스턴스 멤버 필요 시 인스턴스 생성 후 호출 가능

        System.out.println(Static.getCount());
        // Static 클래스 정적 메서드 사용 가능

        // System.out.println(Static.display());    Static 클래스 인스턴스 메서드 사용 불가능
    }
}

-------------------------------------------
0
Count : 1    a : 1
Count : 2    a : 1
2
```

**- 정적 멤버는 클래스명으로 바로 사용이 가능하다.**

ex) Static.Count , Static.GetCount()

**- 정적 메서드에서는 정적 멤버만 사용 가능하다.**

ex) this 키워드, 메서드 오버라이딩 사용 불가능

**- 인스턴스 멤버 필요시 인스턴스 생성 후 호출 가능**




## stack (stack 영역)

- **메서드 내**에서 정의하는 **지역 변수**와 **매개 변수**가 저장되는 공간이 **stack 영역**이다.
- **stack 영역**에 저장되어 있는 데이터는 메서드가 호출될 때 메모리에 할당되고, **종료 시 메모리가 소멸된다.**



- **stack 영역**은 **LIFO(Last In First Out)** 구조이다. 즉, 새로운 데이터는 stack의 최상위에 위치하게 되고, 데이터 추출 시, 가장 최근에 삽입된 데이터만(최상위) 접근이 가능하다.

```java
public class Stack {
    public static void main(String[] args) {
        int a=5; a=4; a=3;
        System.out.println(a);	// 마지막 값인 3만 출력

        for(int i=0;i<5;i++) {	
            // 매개 변수 i, 메서드 혹은 함수에서 입력 값을 받을 때 사용되는 변수
            // 매개 변수도 메서드 내에서 선언된 것으로 간주되므로 지역 변수 이다.
            
            int j=i;
            // 지역 변수 j, 메서드 내에 선언되며 메서드 호출 시 생성되고, 종료 시 소멸된다.
           
        }
        System.out.println(i); // 컴파일 에러
       // 변수 i는 메서드 밖 공간에서는 종료되기 때문에 그 메모리는 소멸된다. 따라서 컴파일 에러 발생
    }
}

```





## heap (heap 영역)

- **참조형(Reference Type)의 데이터 타입을 갖는 객체(인스턴스), 배열 등은 heap 영역**에 데이터가 저장된다.

- **객체, 객체 변수, 참조 변수**는 **stack 영역**에서 실제 데이터가 저장된 **heap 영역의 참조값**을 **new 연산자**를 통해 **return** 받는다. 

  - **new 연산자** : **클래스 타입**의 **인스턴스(객체)를 생성해주는 역할**

    ```java
    클래스		  객체변수		=		  new				클래스();
    
    자료형		참조값 저장			메모리(heap) 할당	   생성자 호출
        	 (인스턴스 핸들)			인스턴스 생성,
    							 참조값 return(→객체)
    ```

    ※ **new 연산자**를 통해 **heap 영역에 데이터 저장 공간 할당 및 인스턴스를 생성**한다. 이 후, 그 공간의 **참조값을 객체에게 반환하고 생성자를 호출**한다.

    

  **(※ 실제 데이터를 가지고 있는 heap 영역의 참조 값을 stack 영역의 객체가 가지고 있다.)**



```java
public class Heap {
    public static void main(String[] args) {
        int[] a= null;
        System.out.println(a); // null

        a = new int[3];	
        // new 연산자를 통해 heap 영역에 데이터 저장 공간을 할당하고, 인스턴스를 생성
        // 이 후, heap 영역의 참조값을 객체(a)에게 반환
        
        System.out.println(a);	// [I@723279cf(참조값)

   		a = new int[3];
        System.out.println(a);	// [I@10f87f48(참조값)
        
        // 두 객체의 참조값이 다른 것을 확인할 수 있다.
        
        
}
}
```

**※ new 연산자를 이용해서 생성하게 되면, 같은 값을 가진 객체이더라도 서로 다른 참조값을 리턴 받는 것을 확인 할 수 있다.**



_추가 개념 )  heap에 저장된 데이터가 더 이상 사용이 불필요하게 될 경우, 메모리 관리를 위해 JVM(Java 가상 머신)에 의해 자동으로 소멸된다._

