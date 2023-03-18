SOLID 원칙
-----------

### SOLID 원칙이란?

* SOLID 원칙이란 5가지 객체지향 설계 원칙을 의미한다.
* S(Single responsibility principle)
    * 클래스는 단 한개의 책임을 가져야 하며 클래스를 변경하는 이유는 단 하나여야 한다.
    * 하나의 클래스가 너무 많은 역할과 책임을 가지면 유지보수와 확장성이 떨어진다.
    * SRP 원칙을 따르면 코드의 응집도가 높아지고 결합도가 낮아진다.

```java
  // SRP를 위반한 예시
class Employee {
    public void calculateSalary() {
        // 급여 계산 로직
    }

    public void saveEmployee() {
        // DB에 저장하는 로직
    }
}
// SRP를 따르는 예시

class Employee {
    public void calculateSalary() {
        // 급여 계산 로직
    }
}

class EmployeeRepository {
    public void saveEmployee(Employee employee) {
        // DB에 저장하는 로직
    }
}
```

* O(Open-close principle)
    * 확장에는 열려있어야 하고, 변경에는 닫혀 있어야 한다.
    * 기존 코드를 변경하지 않고서도 모듈의 기능을 하나 수정하거나 추가해야 한다.
    * OCP은 추상화와 다형성 등을 통해서 유연성, 재사용성, 유지보수성을 얻을수 있다.

```java
// OCP를 위반한 예시

class Employee {
    private final String name;
    private final double salary;
    private final String type;

    public Employee(String name, double salary, String type) {
        this.name = name;
        this.salary = salary;
        this.type = type;
    }

    public double calculateBonus() {
        if (type.equals("Manager")) {
            return salary * 0.2;
        } else {
            return salary * 0.1;
        }
    }
}

// OCP를 따르는 예시

interface Employee {
    double calculateBonus();
}

class Manager implements Employee {
    private final String name;
    private final double salary;

    public Manager(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double calculateBonus() {
        return salary * 0.2;
    }
}

class Engineer implements Employee {
    private final String name;
    private final double salary;

    public Engineer(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double calculateBonus() {
        return salary * 0.1;
    }
}
```

* L(Liskov substitution principle)
    * 하위 타입의 객체는 상위 타입 객체에서 가능한 행위를 수행할 수 있어야 한다.
    * 상위 타입 객체를 하위 타입 객체로 치환해도 정상적으로 동작해야 한다.
    * 상속 관걔가 안인 클래스들을 상속관계로 설정하면 LSP 위배된다.

```java
// LSP를 위반한 예시

class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int area() {
        return width * height;
    }
}

class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        super.setWidth(width);
        super.setHeight(width);
    }

    @Override
    public void setHeight(int height) {
        super.setHeight(height);
        super.setWidth(height);
    }
}

// LSP를 따르는 예시

interface Shape {
    int area();
}

class Rectangle implements Shape {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int area() {
        return width * height;
    }
}

class Square implements Shape {
    private final int side;

    public Square(int side) {
        this.side = side;
    }

    public int area() {
        return side * side;
    }
}


```

* I(Interface segregation principle)
    * 클라이언트는 자신이 사용하는 메서드에만 의존해야 한다.
    * 만약 사용하지 않는 메서드가 있는 인터페이스는 세분화하여 더 작은 단위의 인터페이스로 분리한다.

```java
// ISP를 위반한 예시

interface Employee {
    void work();

    void eat();

    void sleep();
}

class Manager implements Employee {
    public void work() {
        System.out.println("Manager is working");
    }

    public void eat() {
        System.out.println("Manager is eating");
    }

    public void sleep() {
        System.out.println("Manager is sleeping");
    }
}

class Engineer implements Employee {
    public void work() {
        System.out.println("Engineer is working");
    }

    public void eat() {
        System.out.println("Engineer is eating");
    }

    public void sleep() {
        System.out.println("Engineer is sleeping");
    }
}

// ISP를 따르는 예시

interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

interface Sleepable {
    void sleep();
}

class Manager implements Workable, Eatable, Sleepable {
    public void work() {
        System.out.println("Manager is working");
    }

    public void eat() {
        System.out.println("Manager is eating");
    }

    public void sleep() {
        System.out.println("Manager is sleeping");
    }
}

class Engineer implements Workable {
    public void work() {
        System.out.println("Engineer is working");
    }
}
```

* D(Dependency Inversion principle)
    * 구체화된 클래스에 의존하기 보다는 추상 클래스나 인터페이스에 의존해야 한다.

```java
// DIP를 위반한 예시

class Switch {
    private final Light light;

    public Switch() {
        this.light = new Light();
    }

    public void turnOn() {
        light.turnOn();
    }

    public void turnOff() {
        light.turnOff();
    }
}

class Light {
    public void turnOn() {
        System.out.println("Light is on");
    }

    public void turnOff() {
        System.out.println("Light is off");
    }
}

// DIP를 따른 예시

interface Switchable {
    void turnOn();

    void turnOff();
}

class Switch {
    private final Switchable device;

    public Switch(Switchable device) {
        this.device = device;
    }

    public void turnOn() {
        device.turnOn();
    }

    public void turnOff() {
        device.turnOff();
    }
}

class Light implements Switchable {
    public void turnOn() {
        System.out.println("Light is on");
    }

    public void turnOff() {
        System.out.println("Light is off");
    }
}
```
