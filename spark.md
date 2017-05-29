# Spark 기본

## Spark

### 설치

**TODO : 정리할 예정임**



### 설정





### spark context 만들기

Spark Context를 생성하기 위해선 마스터 정보와 어플리케이션 이름을 반드시 지정해야 한다. 



#### 마스터정보

스파크가 동작할 클러스터의 마스터 서버를 의미한다.

로컬 모드에서는 local 또는 local[3], local[*]과 같이 사용한다.

이때 []이 안의 값은 사용할 스레드의 개수로 local은 단일 스레드, '*'는 가용한 CPU의 코어 수 만큼의 스레드를 의미한다.



#### 어플리케이션 이름

어플리케이션을 구분하기 위한 이름



#### 예제코드

#####  Scala

```Scala
// val conf = new SparkConf().setMaster([마스터정보]).setAppName([어플리케이션 이름])
val conf = new SparkConf().setMaster("local[*]").setAppName("RDDCreateSample")
val sc = new SparkContext(conf)
```



#####  Java

```java
// SparkConf conf = new SparkConf().setMaster([마스터정보]).setAppName([어플리케이션 이름]);
SparkConf conf = new SparkConf().setMaster("local[*]").setAppName("RDDCreateSample");
JavaSparkContext sc = new JavaSparkContext(conf);
```



##### Python

```python
# sc = SparkContext(master=[마스터정보], appName=[어플리케이션 이름], conf=conf)
# sc = SparkContext([마스터정보], [어플리케이션 이름], conf)
sc = SparkContext(master="local", appName="RDDCreateTest", conf=conf)
```



**주의사항**





### RDD 생성

#### 예제 코드

```

```

