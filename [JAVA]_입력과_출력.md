# 입력과 출력

> Java 입·출력에 대해서 알아본다





## hasNextInt()

> true or false 값 반환



```java
public class MainInput {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        while (!sc.hasNextInt()) {
        // 사용자가 입력한 값이 정수(int)가 아니면 while문 진행

            sc.next();	// 기존에 입력된 값을 초기화
            
            
            System.err.println("다시 입력하세요");
            // 정수가 입력되지 않은 것을 사용자에게 err로 확인

        }
        
        int i = sc.nextInt();
        System.out.println(i * 10);

        sc.close();

    }
}
```

- `new`연산자를 통해 생성한 **Scanner 객체를 sc라는 변수에 대응**시킴으로써 `hasNextInt()` , `nextInt()`와 같은 메서드를 실행할 수 있다.

  

![image-20200321145719710](https://user-images.githubusercontent.com/58682321/77256779-a025d080-6cb3-11ea-8f01-9f633053c6a5.png)







## Buffer

> 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 임시 메모리 영역



- **BufferedReader** , **BufferedWriter** 는 **Buffer**에 있는 IO  클래스
- **Buffer flush** : **Buffer**에 남아 있는 데이터를 출력(**버퍼를 비우는 동작**)
- **특징** : 입력된 데이터가 바로 전달되지 않고, 중간에 버퍼링 된 후에 전달



![Untitled Diagram](https://user-images.githubusercontent.com/58682321/77256807-cea3ab80-6cb3-11ea-959f-99acd0add99a.png)



#### 버퍼(buffer)가 빠른 이유는?

​	: **버퍼를 사용하지 않는 입력**에 비해 **한 단계를 더 거치는데,** 왜 더 빠를까?  하드 뿐만 아니라 키보드 모니터와 같은 **외부 장치와의 데이터 입·출력은 시간이 많이 소요**된다. 따라서 **중간에 메모리를 두어 데이터를 한데 묶어서 이동시키는 것이 효율적이며, 그 속도 또한 빠르다.**





### BufferedReader

---



- **특징 :** **`Enter`(개행 문자)**만 경계로 인식하며, **데이터가 `String`으로 고정**된다. **Scanner**에 비해 다소 사용하기 불편하나, 많은 양의 데이터를 입력 받을 경우 **BufferedReader**를 통해 받는 것이 효율적이며, 속도 또한 빠르다.

  - Scanner : `Space`(띄어 쓰기) , `Enter`(개행 문자) 모두 경계로 인식

  

#### BufferedReader 사용법

- **한 줄씩 읽기** - `readLine()`

```java
import java.io.*;


class BufferedReaderEx1 {
    public static void main(String[] args) /*throw IOException*/ {
        try { // 예외 처리는 필수
            // try {} catch{} or throws IOExcption 으로 예외 처리가 가능하다

//			 [콘솔에서 입력 받는 경우]
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

			//리턴값 String으로 고정, 입력 받은 값 형변환 필수!
            int num = Integer.parseInt(br.readLine());
            br.close(); // 입출력 끝난 후 닫아준다
            
//           [파일에서 입력 받는 경우]
            
            // 입력 스트림 생성
            FileReader fr = new FileReader("abc.txt");
            // 입력 버퍼 생성
            BufferedReader br_f = new BufferedReader(fr);

            // 파일을 한줄 씩 읽어서 출력하는 방법
            String line = "";
            for (int i = 1; (line = br_f.readLine()) != null; i++) {
                System.out.println(line);
            }
            br_f.close();
            
            /* while ((line=br_f.readLine()) != null) {
            	System.out.println(line);
        } */


        } catch (IOException e) {
            e.printStackTrace();
            System.out.println(e.getMessage());
        }

    }
}
```

- `FileReader`의 경우 `IdeaProjects>[디렉터리 명]`에 위치해 있는 파일을 읽는다. 
  - `File file = new File("abc.txt")` 처럼 객체를 생성해서 `FileReader(file)` 에 대입해도 같은 결과를 가져온다.
- **예외 처리**: `readLine()` 사용 시 필수 이며, `throw IOException` 혹은 `try & catch`를 이용할 수 있다.

- **for & while 문의 존재** :`readLine()` : 파일의 끝이 **null** 값이 될 때 까지, 파일을 한줄 씩 읽는다.





### StringTokenizer

---

> Read한 데이터 가공

- 읽어 들인 데이터는 **줄 단위**로만 읽기 때문에, **공백 단위**로 데이터를 가공하기 위해 사용한다.



#### StringTokenizer 사용법

```java
import java.io.*;
import java.util.StringTokenizer;

public class MainInput {
    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());

        while (st.hasMoreTokens()) {	
            int x = Integer.parseInt(st.nextToken());
            System.out.print(x + " ");
        }
    }

}
```

- `nextToken()` : 다음 토큰을 리턴한다. 이전 토큰은 제거
- `hasMoreTokens()` : 리턴할 다음 토큰이 있으면 **true** 없으면 **false** 리턴

![image-20200323024602845](https://user-images.githubusercontent.com/58682321/77256821-e3803f00-6cb3-11ea-95c0-5d5ace54e824.png)





### BufferedWriter

---



- `System.out.print("");`와 동일하게 사용 가능한 함수. **Buffer**를 이용하기 때문에 성능면에서 더 뛰어나다. 즉, 많은 양의 출력이 필요한 경우 효율적이다.



#### BufferedWriter 사용법

```java
import java.io.*;
import java.util.StringTokenizer;

public class MainInput {
    public static void main(String[] args) throws IOException {

        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));
        bw.write("Hello");
        bw.newLine();   // 개행 역할
        bw.write("World!");
        bw.flush(); // 남아 있는 데이터 모두 출력        
        bw.close();
    }

}
```

- **줄 바꿈(개행)**: `write()` 내에 **"\n"**을 넣어 주거나, `newLine()` 을 이용하면 된다.
- `flush()` : **Buffer**를 이용하는 것이기 때문에, 이를 다 쓴 후에는 이 함수를 통해 버퍼에 남아있는 데이터를 출력한다.

![image-20200323030144017](https://user-images.githubusercontent.com/58682321/77256824-e713c600-6cb3-11ea-9c6d-217a985a695e.png)









**※ 참조)**

https://coding-factory.tistory.com/251

https://jhnyang.tistory.com/92

https://reakwon.tistory.com/50

https://jeong-pro.tistory.com/69