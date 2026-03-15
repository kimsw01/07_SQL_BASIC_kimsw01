# SQL_BASIC 2주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_2nd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**2주차 과제**는 1주차 과제처럼 SQL의 필요성이나 느낀점 위주가 아닌, **실제 강의 내용을 바탕으로 개념을 정리하고 학습한 내용을 집중적으로 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요. 

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_2nd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

### 2-4. SELECT 연습문제

### 2-5. 집계 (Group By + Having + Sum/Count)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | 🍽️         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리 

## 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE의 핵심 문법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

# 포켓몬 데이터셋으로 이해하는 DB

- 포켓몬의 종류 (row), 포켓몬 이름, 공격력 높은 포켓몬, 타입 (column)

# SQL 쿼리 구조

-> 빅쿼리 -> 구글 SQL

SQL 쿼리문은 아래와 같은 문법으로 작성 (SELECT, FROM, WHERE)

# SELECT : 테이블의 어떤 컬럼을 선택(출력)할 것인가?

Col1 AS(바꾸겠다) new_name(별칭),

Col2,

Col3

# FROM
Dataset.Table : 어떤 테이블에서 데이터를 확인할 것인가?

# WHERE : 만약 원하는 조건이 있다면 어떤 조건인가?

Col1 = 1 : 조건문

# 타입이 불인 포켓몬 찾는 쿼리

~~~
SELECT
 *
FROM basic.pokemon
WHERE
 type1 = "Fire"
~~~

별 : 모든 컬럼을 출력하겠다
(SELECT
 별 EXCEPT(제외할 컬럼)
이런 형태도 가능)

# 집합처럼 생각해보기

특정 Table에 있는 데이터를 추출 (SELECT col FROM Table A, B, C, ...)

# 데이터가 여러 장소에 저장되어 있는 경우

특정 Table에 있는 데이터를 각각 추출 후, 연결하기 (추후에 배울 JOIN)

# 실습

~~~
SELECT
 # EXCEPT(eng_name) 제외하는 컬럼
 id AS pokemon_id, # AS는 별칭을 지어줄 때 사용한다.
 id AS "pokemon_id", # 컬럼 이름에 따옴표를 넣는 경우 : 자주하는 실수 => 따옴표 없이 기록
 type1
 # 여러 컬럼 추가 가능
FROM basic.pokemon
WHERE
 type1 = "Fire" ; # ;(세미콜론은 하나의 쿼리가 끝났다는 것을 의미함, 이후 다음 컬럼 바로 작성 가능)

# kimsw01-bigquery : 프로젝트 id
# basic : dataset
# pokemon : table
# '<프로젝트 id>.<데이터셋>.<테이블>'
# 프로젝트 id는 꼭 명시할 필요는 없을 수도 있음 (프로젝트가 단일이라면!)
# 프로젝트를 여러개 사용한다면 명시하는 것이 좋음 => 쿼리를 실행할 때 어떤 프로젝트인지 확인하는 과정이 존재
# 프로젝트 명시 => 불편
# 프로젝트를 제외하고 사용해도 괜찮긴 함 (여러 프로젝트를 쓸 때는 명시해야 한다.)
# 프로젝트 id를 제외하고 작성할 때는 ' 없어도 괜찮음
# 데이터를 활용하고 싶은 목적이 있어야, 어떤 컬럼을 선택할지 알 수 있게 됨

# 가독성 있는 쿼리
# 쿼리를 잘 읽을 수 있으려면 잘 작성해야 함 => 협업할 때 중요함
~~~

# SQL 문법 핵심 정리

- FROM : 데이터를 확인할 Table 명시,

이름이 너무 길다면 AS "별칭"으로 별칭 지정 가능

FROM Table1 AS t1

- WHERE : FROM에 명시된 Table에 저장된 데이터를 필터링 (조건 설정)

Table에 있는 컬럼을 조건 설정

- SELECT : Table에 저장되어 있는 컬럼 선택

여러 컬럼 명시 가능

col1 AS "별칭"으로 컬럼의 이름도 별칭 지정 가능

# SQL 쿼리 구조

~~~
SELECT
컬럼1,
컬럼2,
컬럼3
FROM 테이블
WHERE
 <조건문>

이 순서를 꼭 기억하기! (SELECT - FROM - WHERE)
* SELECT WHERE FROM 불가능
~~~


## 2-5. 집계 (Group By / HAVING / SUM,COUNT)

~~~
✅ 학습 목표 :
* 데이터를 집계하고 그룹화하는 방법을 설명할 수 있다.
* GROUP BY, HAVING, ORDER BY, 집계함수(SUM/COUNT 등)을 활용하는 방법을 설명할 수 있다.
* having과 where의 차이에 대해서 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

# 집계 (GROUP BY)

집계 => 데이터를 요약하는 과정

집계하다 (모을 집, 계산할 계) => 모아서 계산하다

계산

- 더하기, 빼기
- 최대값, 최소값
- 평균
- 갯수 세기

GROUP BY : 같은 값끼리 모아서 그룹화한다.

EX. 색상 기준으로 모은다 => GROUP BY

특정 컬럼을 기준으로 모으면서 다른 컬럼에서는 집계 가능 (합, 평균, MAX, MIN 등)

EX2. 타입을 기준으로 그룹하해서 "평균 공격력" 집계하기

+ 타입을 기준으로 그룹화해서 "타입 별 포켓몬 수" 집계하기

=> 평균 공격력이 제일 높은 타입이 궁금한 경우
- 평균 공격력 내림차순 (큰 것부터 작은 것으로 내려감)으로 정렬 (ORDER BY)

=> 타입 당 포켓몬 수가 10마리 이상인 데이터만 추출하고 싶은 경우 (HAVING)

# SQL로 표현해보기

~~~
SELECT
 집계할_컬럼1,
 집계함수(COUNT, MAX, MIN 등)
FROM TABLE
GROUP BY
 집계할_컬럼1

* 집계할 컬럼을 SELECT에 명시하고
GROUP BY 에 작성해줘야 함.
~~~

# 집계 함수 종류

AVG, COUNT, COUNTIF, MAX, MIN, SUM, ...

# DISTINCT : 고유값을 알고 싶은 경우

DISTINCT의 뜻 : 별개의 여러 값 중에 UNIQUE 한 것만 보고 싶은 경우 사용

EX) 1,2,3,3,4 -> 1,2,3,4 (중복을 제거하는 것)

~~~
SQL 쿼리

SELECT
 집계할 컬럼,
 COUNT(DISTINCT count할 컬럼)
FROM Table
GROUP BY
 집계할 컬럼
~~~

# 그룹화(집계) 활용 포인트

데이터 분석하다가 그룹화하는 경우
- 일자별 집계(원본 데이터는 특정 시간에 어떤 유저가 한 행동이 기록, 일자별로 집계)
- 연령대별 집계 (특정연령대에서 더 많이 구매했는가?)
- 특정 타입별 집계(특정 제품 타입을 많이 구매했는가?)
- 앱 화면별 집계(어떤 화면에 유저가 많이 접근했는가?)

...

# 조건을 설정하고 싶은 경우 : WHERE, HAVING

## WHERE - Table에 바로 조건을 설정하고 싶은 경우 사용

Raw Data인 테이블 데이터에서 조건 설정

~~~
SELECT
 컬럼1, 컬럼2
 COUNT(컬럼1) AS col1_count
FROM Table
WHERE
 컬럼1 >= 3
~~~

## HAVING - GROUP BY한 후 조건을 설정하고 싶은 경우 사용

~~~
SELECT
 컬럼1, 컬럼2,
 COUNT(컬럼1) AS col1_count
FROM Table
GROUP BY 컬럼1, 컬럼2
HAVING
 col1_count > 3
~~~

# 서브 쿼리

- SELECT 문 안에 존재하는 SELECT 쿼리
- FROM 절에 또 다른 SELECT 문을 넣을 수 있음
- 괄호로 묶어서 사용

서브 쿼리를 작성하고, 서브 쿼리 바깥에서 WHERE 조건 설정하는 것

= 서브 쿼리에서 HAVING으로 하는 것

# 정렬하기 : ORDER BY

~~~
SELECT
 col
FROM
ORDER BY <컬럼><순서>
~~~

- 순서 : DESC(내림차순), OSC(오름차순 - 보통 Default)

order by는 쿼리의 맨 마지막(아래)에 두고,

쿼리는 맨 마지막에만 작성하면 됨 (중간에 필요없음)

# 출력 개수 제한하기 : LIMIT

- 쿼리문의 결과 Row 수를 제한하고 싶은 경우 LIMIT 사용

### 쿼리문의 제일 마지막에 작성

~~~
SELECT
 col
FROM Table
LIMIT 1000
~~~

# 최종 정리

- 집계하고 싶은 경우 : GROUP BY + 집계 함수 (AVG, MAX 등)
- 고유값을 알고 싶은 경우 : DISTINCT
- 조건을 설정하고 싶은 경우 : WHERE, HAVING
- 정렬하고 싶은 경우 : ORDER BY
- 출력 개수를 제한하고 싶은 경우 : LIMIT
  

# 2️⃣ 학습 인증란





<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 마스터 진아는 포켓몬 데이터 조회하는 SQL문에 재미를 느껴서 혼자서 데이터를 조회하는 쿼리문을 짰습니다. 하지만 세 가지의 오류로 다음 코드가 실행이 안된다고 하는데, 각 오류의 위치와 이유를 설명하고, 올바른 쿼리문으로 수정해보세요.**

~~~sql
# 진아의 SQL Query문 
SELECT name. type
FROM pokemon;
WHERE type = Electric;
~~~



~~~
SELECT 부분에서는 name과 type을 구분하기 위해 쉼표를 사용해야 한다.
FROM 데이터를 하고 나서 세미콜론이 있으면 안된다. (세미콜론은 쿼리를 끝내는 구문)
WHERE 에서 type이 전기인 것을 추출하려고 하지만 Electric은 string 형식이기에 따옴표가 있어야 한다.

SELECT name, type
FROM pokemon
WHERE type = 'Electric';
~~~



## 문제 2

> **🧚Q. 앞서 SQL Query의 오류를 해결한 진아는 기분 좋게 이번에는 포켓몬 데이터에서 타입별 평균 공격력이 60 이상인 타입만 조회하려는 쿼리를 작성하려고 했습니다. 하지만 이번에도 실수를 하여 쿼리문이 실행되지 않거나 잘못된 결과가 나오고 있는데, 쿼리에서 잘못된 부분이 무엇인지 설명하고, 올바르게 수정한 쿼리를 작성해보세요.**

~~~sql
SELECT type, AVG(attack) AS avg_attack
FROM pokemon
WHERE AVG(attack) >= 60
GROUP BY type;
~~~



~~~
집계 후 조회하는 것이기 때문에, 집계하는 함수 GROUP BY가 FROM 다음으로 와야하고, WHERE이 아닌 HAVING 함수를 사용해야한다.

SELECT type, AVG(attack) AS avg_attack
FROM pokemon
GROUP BY type
HAVING AVG(attack) >= 60
~~~



### 🎉 수고하셨습니다.
