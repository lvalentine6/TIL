일급 컬렉션
---------------

### 일급 컬렉션이란?
* 일급 컬렉션은 컬렉션을 래핑하면서, 그 외 다른 필드가 없는 상태를 말한다.
```java
    Map<String, String> map = new HashMap<>();
    map.put("1", "A");
    map.put("2", "B");
    map.put("3", "C");
``` 
* 위의 자료구조를 아래와 같이 래핑
```java
public class GameRanking {

    private Map<String, String> ranks;

    public GameRanking(Map<String, String> ranks) {
        this.ranks = ranks;
    }
}
```
* 일급 컬렉션을 사용했을때의 이점
  * 비즈니스에 종속적인 자료구조
    * List<String> 와 같은 자료구조를 사용하는 모든 장소에서는 데이터 검증 로직이 들어가야한다.
    * 어디에서 이러한 자료구조가 사용되는지 어떤 로직으로 돌아가는지 전부 파악해야만 한다.
    * 일급 컬렉션을 이용하면 이러한 검증 로직이 자료구조 내에서 이루어져 문제를 최소화 할 수 있다.
  * 불변성 보장
    * 자바에서 final은 재할당만 금지한다. 따라서 값이 변경될 수 있다.
    * 일급 컬렉션을 이용하면 setter 와 같이 값을 변경할 수 있는 방법이 없어 불변성이 보장된다.
  * 상태와 행위를 한곳에서 관리
    * pays라는 컬렉션과 계산로직은 서로 관계가 있다. pay 타입의 상태에 따라 지정된 메서드에서만 계산해야 하는데 강제할수 없는 문제가 있다.
    * 이 때문에 파생되는 문제로 똑같은 기능을 하는 메서드를 중복 생성할 수 있고, 계산 메서드를 누락할 수 있다.
    * 일급 컬렉션을 이용하여 필요한 메서드를 강제할 수 있고 상태와 로직이 한곳에서 관리된다.
    ```java
    public class PayGroups {
    private List<Pay> pays;

    public PayGroups(List<Pay> pays) {
        this.pays = pays;
    }

    public Long getNaverPaySum() {
        return getFilteredPays(pay -> PayType.isNaverPay(pay.getPayType()));
    }

    public Long getKakaoPaySum() {
        return getFilteredPays(pay -> PayType.isKakaoPay(pay.getPayType()));
    }

    private Long getFilteredPays(Predicate<Pay> predicate) {
        return pays.stream()
                .filter(predicate)
                .mapToLong(Pay::getAmount)
                .sum();
        }
    }
    ``` 
  * 이름이 있는 컬렉션
    * 각 그룹별 데이터가 필요할 때 변수명을 다르게 하는것은 검색이 어렵고, 명확한 표현이 불가능 하다는 단점이 있다.
    * 그룹 각각의 일급 컬렉션을 만들어서 컬렉션을 기반으로 용어 사용과 검색을 할 수 있다.
    ```java
        List<Pays> naverPays = new createNaverPays();
        List<Pays> kakaoPays = new createakakaoPays();
    
        -> NaverPays naverPays = new NaverPays(createNaverPays());
        -> KakaoPays kakaoPays = new KakaoPays(createkakaoPays());
    ```     

* 비즈니스 로직과 비즈니스 프로세스
* 비즈니스 로직 : DB와 상호작용하며, 데이터의 CRUD 작업을 수행하는 로직
  * 은행애플리케이션에서의 비즈니스 로직
  * 계좌 생성
  * 입금
  * 출금
* 비즈니스 프로세스 : 비즈니스 로직의 집합이며 애플리케이션의 핵심 기능을 수행하는 모듈인 서비스 클래스에서 구현된다.
  * 비즈니스 프로세스 단계
    * 요청 분석: 비즈니스 프로세스가 시작될 때, 먼저 요청을 분석하고 요청에 필요한 데이터를 수집합니다. 이를 통해 프로세스가 요청을 처리하기 위해 필요한 정보를 파악합니다.
    * 데이터 검증: 수집된 데이터는 유효한 값인지 검증합니다. 데이터의 형식, 범위, 무결성 등을 검사하여 잘못된 데이터가 없는지 확인합니다.
    * 데이터 처리: 유효한 데이터를 기반으로 비즈니스 로직을 수행하여 요청을 처리합니다. 이를 통해 요청에 대한 응답을 생성합니다.
    * 응답 생성: 요청 처리가 완료되면, 처리 결과에 따른 응답을 생성합니다. 응답은 보통 클라이언트에 반환되며, JSON, XML 등의 형식으로 표현됩니다. 
    * 로깅 및 모니터링: 비즈니스 프로세스의 수행 과정에서 발생하는 이벤트를 기록하고 모니터링합니다. 이를 통해 애플리케이션의 문제점을 파악하고 개선할 수 있습니다.

* 참조 : [일급 컬렉션의 소개와 써야할 이유](https://jojoldu.tistory.com/412)
