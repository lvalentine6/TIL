일급 객체
---------------

### 일급 객체의 정의

* 일급 객체는 다음의 3가지 조건을 만족한 객체를 말한다.
* 그러나 자바에서는 일급 객체를 사용하지 못했다.
    * 일급 객체는 변수나 데이터에 담을수 있어야 한다.
  ```java
    public class Main {

    public static void hello(){
            System.out.println("Hello World");
        }

    public static void main(String[] args) {
            Object a = hello; // !! 메서드를 변수에 할당 불가능
        }
    }
  ```
  ```js
    const hello = function() {
        console.log("Hello World");
    }
  ```
    * 일급 객체는 함수의 파라미터로 전달 할 수 있어야 한다.
    ```java
    public class Main {
    
      public static void hello() {
        System.out.println("Hello World");
      }
    
      public static void print(Object func) {
        func();
      }
    
      public static void main(String[] args) {
        print((Object) hello) // !! static 메서드를 함수 매개변수로 전달 불가능
      }
    }
    ```
    ```js
    const hello = function() {
        console.log("Hello World");
    }
    
    function print(func) {
        func();
    }
    
    print(hello);
    ```
    * 일급 객체는 함수의 리턴값으로 사용할 수 있어야 한다.
  ```js
    const hello = function() {
        console.log("Hello World");
        return function() {
            console.log("Hello World 22");
        }
    }
  
    const hello2 = hello();
    hello2();
  ```

* 람다와 익명클래스를 이용해서 자바에서도 일급 객체를 사용할 수 있게 되었다.
    * 일급 객체는 변수나 데이터에 담을수 있어야 한다.
  ```java
  import java.util.function.Consumer;
  
  public class Main {
  public static void main(String[] args) {
  Consumer<String> c = (t) -> System.out.println(t); // 람다식을 인터페이스 타입 변수에 할당
  c.accept("Hello World");
      }
  }
  ```
    * 일급 객체는 변수나 데이터에 담을수 있어야 한다.
  ```java
  import java.util.function.Consumer;

  public class Main {
  // 메소드 매개변수로 람다 함수를 전달
  public static void print(Consumer<String> c, String str) {
  c.accept(str);
  }

    public static void main(String[] args) {
        print((t) -> System.out.println(t) ,"Hello World");
    }
  }
  ```
    * 일급 객체는 변수나 데이터에 담을수 있어야 한다.
  ```java
  import java.util.function.Consumer;

  public class Main {
  public static Consumer<String> hello() {
  // 람다 함수 자체를 리턴함
  return (t) -> {
  System.out.println(t);
    };
  }

  public static void main(String[] args) {
  Consumer<String> c = hello();
  c.accept("Hello World");
    }
  }
  ```
