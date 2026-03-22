# SQL_BASIC 3주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_3rd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**3주차 과제는 문제 풀이를 중심으로**, 강의에서 제시된 예제 문제 중 **7 문제 이상을 선택하여 직접 풀어본 뒤**, 강의 영상의 풀이와 비교해 **틀린 부분, 맞은 부분, 새롭게 배운 개념**을 구체적으로 정리해주세요. (적어도 3문제는 정리해야 합니다.) 완성된 과제는 Gihub에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_3rd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-6. 연습문제 1~3번

### 2-6. 연습문제 7~9번

### 2-6. 연습문제 10~12번

### 2-6. 연습문제 13~17번

### 2-7. 정리 

### 2-8. 새로운 집계함수



## 섹션 4. 쿼리 잘 작성하기, 쿼리 작성 템플릿 및 오류를 잘 디버깅하기

### 3-1. INTRO

### 3-2. SQL 쿼리 작성하는 흐름

### 3-3. 쿼리 작성 템플릿과 생산성 도구 



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | ✅         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리

## 2-6. 연습문제

~~~
✅ 학습 목표 :
* 연습문제(7문제 이상) 푼 것들 정리하기
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### 1번 문제
포켓몬 중에 type2가 없는 포켓몬의 수를 작성하는 쿼리를 작성해주세요.

~~~
답변 :

SELECT
*
FROM basic.pokemon
WHERE
type2 IS NULL

(정답)

# 새롭게 배운 개념 : IS NULL 연산자. null 값은 직접 비교가 불가능해서
type2 = NULL 이 아니라 IS NULL로 사용해줘야 한다. 
반대로 IS NOT NULL도 가능.

WHERE 절에서 여러 조건을 연결하고 싶은 경우 AND 조건을 사용,
OR 조건은 () OR ()로 사용해주어야 한다.
~~~

### 2번 문제
type2가 없는 포켓몬의 type1과 type1의 포켓몬 수를 알려주는 쿼리를 작성해주세요.

단, type1의 포켓몬 수가 큰 순으로 정렬해주세요.

~~~
답변 :

SELECT
 type1, COUNT(id) AS cnt
FROM basic.pokemon
WHERE
type2 IS NULL

(오답)

# 틀린 개념 : type1의 포켓몬 수가 큰 순으로 정렬 => ORDER BY, 큰 순으로
=> 내림차순 (DESC) => ORDER BY cnt DESC

COUNT(집계함수)는 GROUP BY와 함께 다님. 집계하는 기준 (컬럼)이 없으면 COUNT만 쓸 수 있으나, 집계하는 기준이 있다면 그 기준 컬럼을 GROUP BY에 써줘야 한다. => GROUP BY type1

(모범 답안)
SELECT
 type1, COUNT(id) AS cnt
FROM basic.pokemon
WHERE
 type2 IS NULL
GROUP BY
 type1
ORDER BY cnt DESC
~~~

### 4번 문제

전설 여부에 따른 포켓몬 수를 알 수 있는 쿼리를 작성해주세요.

~~~
답변 :

SELECT
 COUNT(id) AS cnt
FROM basic.pokemon
WHERE
is_legendary = TRUE

(오답)

# 틀린 개념 : COUNT(집계함수)인데 GROUP BY 가 아닌 WHERE 을 사용함.
SELECT에 전설 컬럼이 들어가지 않았다.
GROUP BY 는 모든 값을 묶기 때문에 굳이 TRUE를 작성하지 않아도 된다.

(모범 답안)
SELECT
is_legendary, COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
is_legendary
~~~

### 7번 문제

trainer 테이블에서 "Iris", "Whitney", "Cynthia" 트레이너의 정보를 알 수 있는 쿼리를 작성해주세요.

~~~
답변 : 

SELECT
 *
FROM basic.trainer
WHERE
(name = "Iris")
OR (name = "Whitney")
OR (name = "Cynthia")

(정답)

# 새로 배운 개념 : 컬럼 IN ("Iris", "Whitney", "Cynthia")
=> OR로 이어진 개념을 IN으로 한번에 처리할 수 있는 함수.
~~~

### 11번 문제 

type2가 있는 포켓몬 중에 제일 많은 type1은 무엇인가요?

~~~
답변 :

SELECT
 type1,
 COUNT(id) AS cnt
FROM basic.pokemon
GROUP BY
 type1
HAVING
 type 2 IS NOT NULL.
 
 (오답)

 # 틀린 개념 : 그룹화된 결과에 필터를 거는 것이 HAVING인데,
 지금 문제의 경우 먼저 조건 처리 후에 그룹화를 해야해서 WHERE을 사용하고 순서는 반대가 되어야 한다.
 또한 제일 많은 것이기에 ORDER BY cnt DESC 로 내림차순 정리를 해주고 하나의 행만 남기기 위해 LIMIT 1로 제한해준다.

 (모범 답안)

 SELECT
 type1,
 COUNT(id) AS cnt
FROM basic.pokemon
WHERE
 type 2 IS NOT NULL
GROUP BY
 type1
ORDER BY cnt DESC
LIMIT 1
~~~

### 13번 문제

포켓몬의 이름에 "파"가 들어가는 포켓몬은 어떤 포켓몬이 있을까요?

~~~
답변 :

SELECT
 kor_name
FROM basic.pokemon
WHERE
??(모르겠음)

(오답)

# 틀린, 새로 배운 개념 : 컬럼 LIKE "특정단어%"
이름 안에 특정단어가 들어간 것도 검색할 수 있다.
문자열 컬럼에서 특정 단어가 포함되어 있는지 알고 싶은 경우엔 LIKE를 사용하면 편하다.

"%파" : 파로 끝나는 단어, "파%" : 파로 시작하는 단어, 
"%파%" : 파가 들어가는 단어.

(모범 답안)

SELECT
 kor_name
FROM basic.pokemon
WHERE
 kor_name LIKE "%파%"
 ~~~

### 16번 문제

포켓몬을 제일 많이 풀어준 트레이너는 누구일까요?

~~~
답변 :

SELECT
 trainer_id,
 COUNT(pokemon_id) AS cnt_poke
FROM basic.trainer_pokemon
WHERE
 status = "Released"
GROUP BY
 trainer_id

(오답)

# 틀린 개념 : 제일 많이 풀어준 트레이너를 찾는 것이기 때문에,
내림차순 정렬 후 LIMIT 1로 하나만 남겨줘야 한다.

(모범 답안)
...
ORDER BY
 cnt_poke DESC
LIMIT 1
~~~

### 17번 문제

트레이너 별로 풀어준 포켓몬의 비율이 20%가 넘는 포켓몬 트레이너는 누구일까요?

- 풀어준 포켓몬의 비율 = (풀어준 포켓몬 수 / 전체 포켓몬 수)

~~~
답변 :

SELECT
 trainer_id,
 COUNT(pokemon_id) AS cnt
FROM basic.trainer_pokemon
WHERE
???(모르겠음)

(오답)

# 틀린, 새로 배운 개념 : COUNTIF(조건)
조건에 맞는 행만 걸러서 출력해준다.

(모범 답안)

SELECT
 trainer_id,
 COUNTIF(status = 'Released') AS released_cnt,
 COUNT(pokemon_id) AS cnt,
 COUNTIF(status = 'Released')/COUNT(pokemon_id) AS released_ratio
FROM basic.trainer_pokemon
GROUP BY
 trainer_id
HAVING
 released_ratio >= 0.2
 ~~~


## 2-8. 새로운 집계함수

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE을 활용하는 방법을 설명할 수 있다. 
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### GROUP BY ALL
- SELECT 에 작성했던 컬럼을 GROUP BY 에 작성해야 그룹화 할 수 있었음.

(단점) => 컬럼이 많아지면 쿼리가 길어지고, 단순 작업이 추가됨.

- 그래서 GROUP BY 뒤에 ALL 이라는 함수로 모든 컬럼을 그룹화 시킬 수 있는 함수가 추가되었음.

~~~
예시:

(이전)
SELECT
 Firstname,
 Lastname
...
GROUP BY
 Firstname,
 Lastname

=======================
(이후)

SELECT
 Firstname,
 Lastname
...
GROUP BY ALL
~~~

## 3-2. 쿼리를 작성하는 흐름

~~~
✅ 학습 목표 :
* 쿼리를 작성하는 흐름을 설명할 수 있다.
~~~

<!-- 새롭게 배운 내용을 자유롭게 정리해주세요.-->

### 흐름 정리

1. 지표 고민 - 어떤 문제를 해결하기 위해 **데이터**가 필요한가? (문제 정의)

2. 지표 구체화 - 추상적이지 않고 구체적인 지표 명시 (분자, 분모 표시)

3. 지표 탐색 - 유사한 문제를 해결한 케이스가 있나 확인 (존재할 경우, 해당 쿼리 리뷰)

4. 없다면, 쿼리 작성 - 데이터가 있는 테이블 찾기 (1개일 경우 활용, 2개 이상일 경우 JOIN 등으로 연결 방법 고민)

5. 데이터 적합성 확인 - 예상한 결과와 동일한지 확인

6. 쿼리 가독성 - 나중을 위해 깔끔하게 쿼리 작성

7. 쿼리 저장 - 쿼리는 재사용되므로 문서로 저장


## 3-3. 쿼리 작성 템플릿과 생산성 도구

~~~
✅ 학습 목표 :
* 생산성 도구를 만들 수 있다.
~~~

### 쿼리 작성 템플릿

~~~
# 쿼리를 작성하는 목표, 확인할 지표 :
# 쿼리 계산 방법 :
# 데이터의 기간 :
# 사용할 테이블 :
# Join KEY :
# 데이터 특징 :

SELECT

FROM
WHERE
~~~

### 생산성 도구 : 템플릿 쉽게 사용하기

템플릿을 사용하자! 라고 제시하면 생기는 일

-> 템플릿 사용을 까먹음, 습관 형성이 되지 않음

-> 이 부분을 개선하기 위해 생산성 도구를 활용

<!-- 이어질 주차에서 생산성 도구를 활용한 실습이 있습니다.강의에 맞게 제작하여 화면을 캡쳐하여 이 주석을 지우고 올려주세요. -->



<br>
<br>

---

# 2️⃣ 학습 인증란

<!-- 이 글을 지우고, 여기에 학습한 것을 인증해주세요.-->



<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. Q. 포켓몬 연구에 흥미를 느낀 혜인은 각 타입(type1)별 평균 공격력(attack)을 비교해보고 싶었습니다.**
>
> 그래서 다음과 같은 필요한 정보를 미리 정리해보았습니다. 

~~~
조건 : attack이 50 이상인 포켓몬만 포함
보고 싶은 컬럼 : type1
집계 내용 : 각 type1 별 평균 공격력
정렬 기준 : 평균 공격력을 기준으로 내림차순 정렬
~~~

> **이 목표를 바탕으로 혜인은 아래와 같은 쿼리를 작성했지만, 일부 SQL 문법 요소를 빼먹었습니다. 비어 있는 부분인 ㄱ, ㄴ, ㄷ, ㄹ 에 들어갈 알맞은 SQL 구문을 채워보세요:**

~~~sql
SELECT type1, (ㄱ)
FROM pokemon
(ㄴ) attack >= 50
(ㄷ) type1
ORDER BY (ㄱ) (ㄹ);
~~~



~~~
여기에 답을 작성해주세요!
~~~



### 🎉 수고하셨습니다.
