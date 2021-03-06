# @SuppressWarnings

코드 컴파일시 컴파일 경고를 하지 않도록 하는 어노테이션 설정





예제코드

```java
@SuppressWarnings("unchecked")
public void TestClass {
  //...
}
```





## 속성

| 속성                       | 설명                                       |
| ------------------------ | ---------------------------------------- |
| **all**                  | 모든 경고를 무시                                |
| boxing                   | boxing/unboxing 오퍼레이션과 관련된 경고를 무시        |
| dep-ann                  | 권장하지 않는 어노테이션과 관련된 경고 무시                 |
| deprecation              | 권장되지 않는 기능과 관련된 경고 무시                    |
| fallthrough              | switch문에서 누락된 break문과 관련된 경고 무시          |
| **finally**              | 리턴되지 않는 마지막 블록과 관련된 경고 무시                |
| hiding                   | 변수를 숨기는 로컬과 관련된 경고 무시                    |
| incomplete-switch        | switch문에서 누락된 항목과 관련된 경고 무시              |
| javadoc                  | javadoc 경고와 관련된 경고 무시                    |
| nls                      | 비nls 문자열 리터럴과 관련된 경고 무시                  |
| **null**                 | null분석과 관련된 경고 무시                        |
| rawtypes                 | 원시 유형 사용법과 관련된 경고 무시                     |
| resource                 | closable 유형의 자원 사용에 관련된 경고 무시            |
| restriction              | 올바르지 않거나 금지된 참조 사용법과 관련된 경고 무시           |
| **serial**               | 직렬화 가능 클래스에 대한 누락된 serialVersionUID필드와 관련된 경고 무시 |
| static-access            | 잘못된 정적 액세스와 관련된 경고 무시                    |
| static-method            | static으로 선언될 수 있는 메소드와 관련된 경고 무시         |
| super                    | 부모 클래스 호출을 사용하지 않는 메소드 오버라이딩과 관련된 경고 무시  |
| synthetic-access         | 내부 클래스로부터의 최적화 되지 않는 액세스와 관련된 경고 무시      |
| sync-override            | 동기화된 메소드를 오버라이드하는 경우 누락된 동기화로 인한 경고 무시   |
| **unchecked**            | 미확인 오퍼레이션과 관련된 경고 무시                     |
| unqualified-field-access | 규정되지 않은 필드 액세스와 관련된 경고 무시                |
| **unused**               | 사용하지 않는 코드 및 불필요한 코드와 관련된 경고 무시          |
| **cast**                 | 캐스트 오퍼레이션과 관련된 경고 무시                     |







# 템플릿 메소드 패턴



상위 클래스에서 처리의 흐름을 제어하며, 하위 클래스의 처리 내용을 구체화한다.

여러 클래스의 공통적인 부분을 상위 추상 클래스에서 구현하고, 각각의 상세구분은 하위 클래스에서 구현한다.

코드의 중복을 줄일 수 있고, 상속을 통한 확장 개발 방법으로 전략 패턴(Strategy Pattern)과 함께 가장 많이 사용되는 패턴이다.



## 고려사항

- 멤버 함수들의 접근 범위 지정을 명확히 해야한다.
- 상위 추상 클래스에서 구현 할지, 하위 클래스에서 구현하게 할지를 결정해야 한다.
- 추상 메서드(abstract method)의 수를 줄이는 것이 중요하다. (virtual table 확장에 따른 perfomance 문제 발생)



## 용어

- 추상 메소드(Abstract Method)
  - 추상 메서드(abstract method)로 정의한 메소드
  - 상위 추상 클래스를 상속받은 하위 클래스들은 해당 메소드를 반드시 구현해야 한다.
  - 각 하위 클래스마다 다른 작업을 하게되는 부분


- 훅 메소드 (Hook Method)
  - 상위 추상 클래스에 구현된 메소드
  - 해당 상위 추상 클래스를 상속받은 하위 클래스들에 공통적으로 적용되는 메소드이다.
  - 모든 하위 클래스가 같은 작업을 하게되는 부분





# DBCP

DBCP(DataBase Connection Pool)



데이터베이스와 연결된 커넥션을 미리 만들어 놓고 풀(Pool) 속에 저장해 두고 있다가 필요할 때 커넥션을 풀에서 꺼내 쓰고 다시 풀에 반납하는 기법을 말한다. 웹 프로그램에서 데이터베이스의 환경설정과 연결 관리 등을 따로 속성파일로 관리를 하고 이렇게 설정된 정보를 이용하여 커넥션을 획득하는 방법이다.



## 설명

- 웹 어플리케이션이 실행되면 미리 커넥션 객체를 생성하여 풀에 담아둔다.
- DB와 연결된 커넥션을 미리 생성하여 풀 속에 저장해두고 있다가 필요할 때 가져다 쓴다.
- 미리 생성해두었기 때문에 데이터베이스에 부하를 줄이고 유동적으로 연결을 관리할 수 있다.






## 종류

- Commons DBCP
- Tomcat-JDBC
- BoneCP
- HikaraCP





## 설정



DBCP 기준 옵션 설명



| 옵션          | 설명                            | 예제            |
| ----------- | ----------------------------- | ------------- |
| initialSize | 최초 설정되는 커넥션 수                 | initialSize=5 |
| maxActive   | 동시에 사용할 수 있는 최대 커넥션 수         | maxActive=15  |
| maxIdle     | 커넥션 풀에 대기로 있을 수 있는 최대 커넥션 수   | maxIdle=10    |
| minIdle     | 커넥션 풀에 대기로 있을 수 있는 최소 커넥션 수   | minIdle=5     |
| maxWait     | 모든 커넥션이 사용 중인 경우 커넥션을 기다리는 시간 | maxWait=1000  |



**[예제 설명]**

위의 옵션대로 설정한 경우

- initialSize : 최초 웹 어플리케이션을 실행 했을 때 커넥션 풀에 5개의 커넥션이 생성된다.
- maxActive : 웹 어플리케이션 실행 중 동시에 최대로 사용할 수 있는 커넥션의 수
  - 최초에 5개의 커넥션이 생성되는데 부족한 경우 추가로 10개까지 더 생성할 수 있다.
- maxIdle : 커넥션을 모두 사용한 후에 풀에 대기상태로 있을 수 있는 최대 커넥션 수
  - 15개를 사용하다가 5개는 반납하고 10개의 유휴 커넥션을 풀에 유지한다.
- minIdle : 커넥션을 모두 사용한 후에 풀에 대기상태로 있을 수 있는 최소 커넥션 수
  - 5 ~ 10개의 커넥션을 풀에 유지할 수 있다.
- maxWait : 커넥션이 모두 사용중인 경우 다음 커넥션을 사용할 수 있을 때까지 기다리는 시간
  - 최대 1초동안 기다리고 반납되지 않으면 time out이 발생
  - Millisecond 단위로 설정 (1000 = 1초)