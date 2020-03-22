# Java SE, JVM, JRE, JDK



### Java SE

------

: **자바의 표준안**



-  자바라는 언어가 **어떠한 문법을 가져야 한다는 것이 Java SE(표준안)** 에 기술되어 있다.

  

- IBM, 오라클, Open JDK 등 다양한 주체가 자바 표준안에 기술된 자바의 문법과 규칙에 따라 자바를 실행할 수 있는 환경인 JVM을 만드는 것





### **JVM(Java Virtual Machine)**

------

**: 자바 소스 코드로 부터 만들어지는 바이너리 파일(.class)을 실행해 주는 가상 머신**





**※ 중요) 자바 파일은 `소스코드`이며, 이는 JVM이 이해할 수 있는 코드가 아니다. 즉, JVM이 이해할 수 있는 파일은 `바이트 코드`로 이루어진 `.class `파일이다.**

- **`javac [파일명.java]` : JVM이 이해할 수 있는 `바이트코드`로 구성된 `.class` 파일**(컴파일 작업)
- **`java [파일명]` : 자바 런처라고도 하며, JVM에 파일을 전달하는 역할**



즉, `자바 파일(.java)`의 **변동 사항**이 있을 시에는 `javac [파일명.java] `**(컴파일)** 을 실행한 후, `java [파일명]` **(자바 런처)**을 실행해야지만 **바뀐 결과를 적용**할 수 있다.





- **JVM은 플랫폼에 의존적이다.**
  
  - 리눅스 JVM , Windows의 JVM은 서로 다르다.
  - **JDK, JRE, JVM 모두 플랫폼에 의존적**이지만, **자바는 플랫폼에 독립적**

  
  
- **컴파일된 바이트코드**를 **JVM**을 이용해 실행하면 **어떤 운영체제나 하드웨어에서 실행하든 상관없이 코드의 동작을 보장**한다. 

| **소스 코드(자바 파일)**  - 어떠한 환경에서든 코드 동작 가능 |
| ------------------------------------------------------------ |
| **JVM**                                                      |
| **운영체제**                                                 |
| **컴퓨터 하드웨어**                                          |



- **JVM 수행 작업**
  - **Loads code :** 작성된 소스코드 **읽기**
  - **Verifies code :** 소스코드 **검증 및 확인**(문법에 올바른지 검증하여 정상적으로 동작하는지 확인)
  - **Executes code :** 소스코드 **실행**(실제 머신에서 소스코드를 실행해 프로그램 구동)
  - **Provides runtime environment :** **런타임 환경을 제공**(어떠한 장비에서건 구동이 되기 위해 기본 베이스 환경 구축)





### **JRE(Java Runtime Environment)**

------

: **소스 코드에 적힌대로 프로그램을 생성하는 역할**



- 자바 개발자 보다는 **일반 사용자를 위한 프로그램**



- **JVM**이 자바 프로그램을 동작시킬 때 필요한 **라이브러리 파일**들과 **기타 파일들**을 가지고 있다.

![jre](https://user-images.githubusercontent.com/58682321/77073242-4ebade80-6a32-11ea-80b2-020aa2debbaf.jpg)



### **JDK (Java Development Kit)**

------

**: 자바 소프트웨어를 개발하는 데 필요한 여러 가지 개발 도구**



- **JRE** 뿐만 아니라 **컴파일러, 디버거 등(개발 도구)** 자바를 실행할 수 있는 **자바 애플리케이션이 포함**되어 있다.



- **JDK**를 설치하면 **JRE**를 별도로 설치하지 않아도 된다.

![jdk](https://user-images.githubusercontent.com/58682321/77073237-4d89b180-6a32-11ea-8dd2-6e3c50f14962.jpg)