# SQL_BASIC 5주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_5th_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**5주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **3 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 4문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 



## SQL_BASIC_5th

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

### 4-5. 시간 데이터 연습문제 1~2번

### 4-5. 시간 데이터 연습문제 3~5번

### 4-6. 조건문 (CASE WHEN, IF)

### 4-7. 조건문 연습 문제

### 4-8. 정리

### 4-9. BigQuery 공식 문서 확인하는 법

(강의에서 연습문제가 많아서 따로 프로그래머스 문제 과제는 없습니다.)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | ✅         |
| 5주차 | 섹션 **4-4** ~ **4-9** | ✅         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>



<!-- 여기까진 그대로 둬 주세요-->

---

# 4-4. 날짜 및 시간 데이터 이해하기(2) (EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME)

~~~
✅ 학습 목표 :
* 날짜 및 시간 데이터에 대해서 더 자세히 설명할 수 있다. 
* CURRENT_TIME, EXTRACT, DATETIME_TRUNC, PARSE_DATETIME, FROMAT_DATETIME 을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

## CURRENT_DATETIME

CURRENT_DATETIME([time_zone])
 : 현재 DATETIME 출력

```SQL
SELECT
 CURRENT_DATE() AS current_date, #현재날짜
 CURRENT_DATE("Asia/Seoul") AS asia_date, #현재날짜
 CURRENT_DATETIME() AS current_datetime, #현재날짜 + 현재시각(UTC)
 CURRENT_DATETIME("Asia/Seoul") AS current_datetime_asia; #현재날짜 + 현재시각(KST)
```

## DATETIME 함수

### EXTRACT

: DATETIME에서 특정 부분만 추출하고 싶은 경우

ex) `EXTRACT(시간단위 FROM DATETIME "시간") AS 시간단위.`

### DATETIME_TRUNC

: 일정 부분만 남기고 싶은 경우

ex) `DATETIME_TRUNC(datetime_expression, datetime_part)`



### PARSE_DATETIME

: 문자열로 저장된 DATETIM을 DATETIME 타입으로 변경

ex) `PARSE_DATETIME('문자열의 형태', 'DATETIME 문자열')`

```sql
PARSE_DATETIME('%Y-%m-%d %H:%M:%S', '2024-01-01 12:35:35')
```


### FORMAT_DATETIME
: DATETIME 타입 데이터를 특정형태의 문자열 데이터로 변환

ex) `PARSE_DATETIME('%c', 'DATETIME')`


### LAST_DAY

: 마지막 날을 알고싶은 경우, 월의 마지막 값을 반환

ex) LAST_DAY(DATETIME)`

### DATETIME_DIFF

: 두 DATETIME의 차이를 알고 싶은 경우  

ex) `DATETIME_DIFF(첫 DATETIME, 두번째 DATETIME, 궁금한 차이)`

```sql
SELECT
   DATETIME_DIFF(first_datetime, second_datetime, DAY), 
   DATETIME_DIFF(second_datetime, first_datetime, DAY),
   DATETIME_DIFF(first_datetime, second_datetime, MONTH),
   DATETIME_DIFF(first_datetime, second_datetime, WEEK),
FROM (SELECT
      DATETIME "2024-04-02 10:20:00" AS first_datetime,
      DATETIME "2021-01-01 15")
```
 

# 4-6. 조건문(CASE WHEN, IF)

~~~
✅ 학습 목표 :
* 조건문 함수의 기능을 이해하고, 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

## 조건문

: 만약 특정 조건이 충족되면, 어떤 행동을 하자

-> 특정 조건이 참일 때 A, 아니면 B (조건에 따른 분기 처리가 필요할 경우)
& 조건에 따라 다른 값을 표시하고 싶을 때 사용

### 사용 이유

: 데이터 분석을 하다보면, 특정 카테고리를 하나로 합치는 전처리가 필요할 수 있음.

-> 발생 이유?

- 데이터를 저장하는 쪽과 데이터를 분석하는 쪽이 나뉘고 (팀 등으로),
- 분석할 때 필요한 부분에서 조건 설정에서 변경하는 것이 더 유용.
- 저장할 때부터 특정 카테고리를 합쳐서 저장하면, 쪼개서 보고싶을 때 볼 수 없음.

## CASE WHEN
~~~
SELECT
 CASE
  WHEN 조건1 THEN 조건1이 참일 경우 결과
  WHEN 조건2 THEN 조건2가 참일 경우 결과
  ELSE 그 외 조건일 경우 결과
END AS 새로운 컬럼 이름
~~~
- 조건1, 조건2에 둘 다 해당하면 앞선 순서울 따름.
- 문자열 함수(특정 단어 추출)에서 이슈가 바로 발생

### 1) CASE WHEN 예시
~~~
SELECT
 new_type1,
 COUNT(DISTINCT id) AS cnt
 CASE
  WHEN (type1 IN("Rock","Ground") OR type2 IN ("Rock","Ground")) THEN "Rock&Ground"
 ELSE type1
 END AS new_type1 
FROM basic.pokemon
)
GROUP BY
 new_type1
~~~

## IF
: 단일 조건일 경우 유용

ex) `IF(조건문, True일 때의 값, False일 떄의 값) AS 새로운_컬럼_이름`

## 정리

- CASE WHEN: 여러 조건이 있을 경우 사용, 조건의 순서에 주의
- IF: 단일 조건일 경우 사용


 # 4-5. 시간 데이터 연습문제 & 4-7. 조건문 연습 문제

~~~
✅ 학습 목표 :
* 4-5, 4-7 각각에서 두 문제 이상 (최소 4문제) 푼 내용 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

## 시간 데이터 1번 문제

: 트레이너가 포켓몬을 포획한 날짜(catch_date)를 기준으로, 2023년 1월에 포획한 포켓몬의 수를 계산해주세요.

```sql
SELECT
  COUNT(DISTINCT id) AS cnt
FROM basic.trainer_pokemon
WHERE
  EXTRACT(YEAR FROM DATETIME(catch_datetime, "Asia/Seoul")) = 2023
  AND EXTRACT(MONTH FROM DATETIME(catch_datetime, "Asia/Seoul")) = 1
```

### 배운 점

- 컬럼의 이름만 믿고 바로 쿼리를 작성하는 것이 아니라, 꼭 **데이터를 확인해야 한다.**

- date가 UTC인지 KST인지 잘 확인해야 한다. 

- != 는 같지 않다는 연산자

## 시간 데이터 2번 문제 

: 배틀이 일어난 시간(battle_datetime)을 기준으로, 오전 6에서 오후 6시 사이에 일어난 배틀의 수를 계산해주세요.

```sql
SELECT
  COUNT(DISTINCT id) AS battle_cnt
FROM basic.battle
WHERE
  EXTRACT(HOUR FROM battle_datetime) >=6
  AND EXTRACT(HOUR FROM battle_datetime) <= 18
```

### 배운 점
- EXTRACT도 상위 함수 사용 (섞기)

- 섞어서 EXTRACT(HOUR FROM battle_datetime) BETWEEN 6 and 18

- 6 이상 8 이하

## 조건문 1번 문제

: 포켓몬의 'Speed'가 70 이상이라면 '빠름', 그렇지 않으면 '느림'으로 표시하는 새로운 컬럼 'Speed_Category'를 만들어 주세요.

```sql
#1번 문제
SELECT
  id,
  kor_name,
  IF(speed>=70, "빠름", "느림") AS Speed_Category
FROM basic.pokemon
```

### 배운 점

- 조건 활성화.
- IF('조건', 값1, 값2)

## 조건문 2번 문제

: 포켓몬의 'type1'에 따라 'Water', 'Fire', 'Electric' 타입은 각각 '물', '불', '전기'로, 그 외의 타입은 '기타'로 분류하는 새로운 컬럼 'type_Korean 만들어 주세요.

```sql
SELECT
  id,
  kor_name,
  type1,
  CASE
    WHEN type1 = "Water" THEN "물"
    WHEN type1 = "Fire" THEN "불"
    WHEN type1 = "Electric" THEN "전기"
    ELSE "기타"
  END AS type1_Korean
FROM basic.pokemon
```
### 배운 점

- type 1을 사용해서 특정 조건을 만족하는 것은 값을 변경

- 타입이 여러가지가 있다.


# 확인문제

## 문제 1

> **🧚Q. 광윤이는 카페 주문 로그 데이터(order_log)를 분석하여, '오전(0시-11시)'과 '오후(12시-23시)'의 주문 건수를 집계하려고 합니다. 광윤이가 작성한 다음 SQL 쿼리 중 문법적으로 틀렸거나 의도한 결과가 나오지 않는 것을 모두 골라보세요. (복수 선택 가능)**

~~~sql
1. SELECT 
   IF(EXTRACT(HOUR FROM order_time) < 12, '오전', '오후') AS time_type,
   COUNT(*)
   FROM order_log
   GROUP BY time_type;

2. SELECT 
   DATETIME_TRUNC(order_time, HOUR) AS truncated_hour,
   COUNT(*)
   FROM order_log
   WHERE order_time BETWEEN '2021-01-01' AND '2021-12-31'
   GROUP BY order_time;

3. SELECT 
   FORMAT_DATETIME(order_time, '%H') AS order_hour,
   COUNT(*)
   FROM order_log
   GROUP BY 1;

4. SELECT 
    CASE 
      WHEN EXTRACT(HOUR FROM order_time) BETWEEN 0 AND 11 THEN '오전'
      ELSE '오후'
    AS time_group,
    COUNT(*)
   FROM order_log
   GROUP BY time_group;
~~~

<!-- 틀린쿼리에 대한 오류의 원인도 같이 작성해주세요. 문제에서 제공된 order_time 컬럼은 DATETIME type의 데이터를 가지고 있다고 가정합니다. -->

~~~
2번 - GROUP BY를 시간대 별로 묶어야 하는데 그렇게 하지 않음. (전체 시각으로 쪼개져서 보기 힘듦)

4번 - END 누락. CASE WHEN을 사용할 때에는 반드시 END를 사용해주야 함.
~~~



## 문제 2

> **🧚Q. 예운이는 포켓몬 타입에 따라 설명을 부여하는 쿼리를 작성했습니다. type 1 컬럼의 값에 따라 조건을 분기했으며, 다음 SQL 쿼리를 실행했습니다.**

~~~sql
SELECT name,
       CASE 
         WHEN type1 = 'Fire' THEN 'Hot'
         WHEN type1 = 'Water' THEN 'Cool'
         ELSE 'Normal'
       END AS type_description
FROM pokemon;
~~~

> **다음 중 type_description의 결과가 'Normal'로 출력될 포켓몬은?**

| **name**   | **type1** |
| ---------- | --------- |
| Pikachu    | Electric  |
| Charmander | Fire      |
| Squirtle   | Water     |
| Bulbasaur  | Grass     |

<!-- 근거와 함께 답을 작성해주세요 -->

~~~
Pikachu, Bulbasaur

나머지 둘은 Hot, Cool이라는 이름표를 받음. 피카츄와 이상해씨는 어디에도 속하지 않아 Normal로 이름표 변경.
~~~



<br>

### 🎉 수고하셨습니다.
