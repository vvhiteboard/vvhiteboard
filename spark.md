# Spark 기본

**참고서적** : 빅데이터 분석을 위한 스파크2 프로그래밍 - 위키북스



## Spark

### 설치

**TODO : 정리할 예정임**



### 설정

#### python

1. python path를 지정한다.

   - .bashrc에 PYTHONPATH 환경변수 설정
      ```shell
       export PYTHONPATH=$SPARK_HOME/python:$SPARK_HOME/python/build:$SPARK_HOME/python/lib/py4j-버전-src.zip
      ```

   - py4j를 추가하지 않으면 SparkContext 모듈 사용시 아래의 에러가 발생할 수 있다.

     ```shell
     hduser@main:~/spark/python$ python test.py
     Traceback (most recent call last):
       File "test.py", line 1, in <module>
         from pyspark import SparkContext
       File "/home/hduser/apps/spark/python/pyspark/__init__.py", line 44, in <module>
         from pyspark.context import SparkContext
       File "/home/hduser/apps/spark/python/pyspark/context.py", line 29, in <module>
         from py4j.protocol import Py4JError
     ImportError: No module named py4j.protocol
     ```







### spark context 생성

Spark Context를 생성하기 위해선 마스터 정보와 어플리케이션 이름을 반드시 지정해야 한다. 



#### 마스터정보

스파크가 동작할 클러스터의 마스터 서버를 의미한다.

로컬 모드에서는 local 또는 local[n], local[*]과 같이 사용한다.

이때 []이 안의 값은 사용할 스레드의 개수로 local은 단일 스레드, '*'는 CPU의 코어 수 만큼의 스레드를 의미한다.



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





### RDD 연산



RDD 연산은 크게 RDD 트랜스포메이션(Transformation)과 RDD 액션(Action)으로 나뉜다.

RDD 연산은 각 명령어가 실행될 때 실행하지 않고 **RDD 액션을 실행할 때** 실행합니다. 다시 말하면 트랜스포메이션 연산은 즉시 실행하는 것이 아니고 그런 연산이 이루어 질 것이라고 **명시**하는 것이고 실제 실행은 액션 명령어가 실행 될 때 순차적으로 실행하도록 되어 있습니다. 이를 **실행 지연(Lazy)** 이라고 한다.

실행 지연의 장점은 최적의 **실행계획**을 세울 수 있다는 것이다. 즉 실행하기 전에 실행해야하는 항목을 정리하고 한꺼번에 실행하기 때문에 최적의 수행 방법을 세우고 실행하는 것이 가능하다는 것이다. 따라서 RDD 연산을 작성할 때는 이것을 염두해서 적절한 실행 계획을 세울 수 있도록 작성하는 것이 중요하다.



#### RDD 트랜스포메이션(Transformation)

RDD를 연산하여 새로운 RDD를 생성하는 연산을 의미한다.

이는 RDD에 어떤 연산(사직연산 등)을 하여 새로운 RDD를 생성할 수도 있고 RDD 2개를 연산하여 새로운 RDD를 생성할 수도 있고 아니면 특정 데이터(객체나 파일)를 이용하여 새로운 RDD를 생성할 수도 있다.

일반적으로는 이 3가지 경우의 연산을 **트랜스포메이션 연산**이라고 한다.



연산의 종류는 크게 6가지로 분류할 수 있다. 간단하게 어떤 메소드들이 있는지만 정리하려고 한다.

- 맵(Map) 연산 : 요소간의 사상(Mapping)을 정의한 함수를 RDD에 속하는 모든 요소에 적용해 새로운 RDD 생성
  - map, flatMap
  - mapPartitions, mapPartitionsWithIndex
  - mapValues, flatMapValues
- 그룹화 연산 : 특정 조건에 따라 요소를 그룹화하거나 특정 함수를 적용
  - zip, zipPartitions
  - groupBy, groupByKey
- 집합 연산 : RDD에 포함된 요소를 집합으로 간주하여 합집합, 교집합등을 계산한다.
  - distinct
  - cartesian
  - subtract, subtractByKey
  - union
  - intersection
  - join, leftOuterJoin, rightOuterJoin
- 집계 연산 : RDD 요소에서 집계 RDD를 생성하는 연산
  - reduceByKey
  - foldByKey
  - combineByKey
  - aggregateByKey
- 파티션 연산 : RDD의 파티션 개수를 조정
  - pipe
  - coalesce, repartition, repartitionAndSortWithinPartitions
  - partitionBy
- 필터와 정렬 연산 : 특정 조건을 만족하는 요소만 선택하거나 각 요소를 정해진 기준으로 정렬
  - filter
  - sortByKey
  - keys, values
  - sample



#### RDD 액션(Action)

RDD를 이용하여 어떤 데이터를 추출하는 연산을 의미한다.

RDD에서 어떤 결과를 구해낼 때 사용하기 때문에 실제 실행이 될 필요가 있다. 따라서 앞에서 설명했듯이 이 액션 연산이 실행 될 때 앞에서 지정해둔 RDD 트랜스포메이션 명령어가 실행되고 액션을 실행해 결과를 얻는다.



- 출력 연산
  - first
  - take, takeSample
  - collect, count, countByValue
  - reduce
  - fold
  - aggregate
  - sum
  - foreach, foreachPartition
  - toDebugString
  - cache, persist, unpersist
  - partitions



#### RDD 데이터 저장/불러오기

**TODO : 정리 예정**

- 텍스트파일
- 오브젝트 파일
- 시퀀스 파일 (in Hadoop)



#### 클러스터 환경에서의 공유 변수

**TODO : 정리 예정**