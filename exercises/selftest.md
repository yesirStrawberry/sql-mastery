잘 숙지 못한 개념들

- 단순 속성 vs 복합 속성
  -  다중 속성?

- index는 설계임 파생임/
  - 설계상 이점이 있어서 설계일 거 같긴 함
>> INDEX는 속성이 아님 ㅇㅇ, 문제에서 물어본 건 통계 속성같은 거라 파생이 답이었음

- 도메인?
  - 속성에 입력할 수 있는 값의 범위임
  - check로 입력값 검사? -> 이건 모르겠음
  - not null constraint로 입력값 검사 -> 암튼 속성에 입력할 수 있는 값의 범위임 
  - 하나의 relation 과 다른 relation과의 fk constiraint?
      - 이게 뭘 의미하는 지를 모르겠음

no.12
  - 이거 걍 ㄹㅇ 모르겠음
  ALTER TABLE TAB2 ADD FOREIGN KEY(CLASS_NO) REFERENCES TAB1(NO) ON DELETE SET NULL;
  DELETE FROM TAB1 WHERE NAME = 'C';
  - referance 가 tab1에 걸려있음
  - ON 조건이 delete 하라는 거 같긴 해서 4번 고르겠음
>> ON DELETE SET NULL은 INSTANCE 삭제가 아니라 ATTRIBUTE만 삭제함
    
no.22 TOP-N 쿼리? 
  1. rownum 으로 하는 거 있음
  2. TOP(2) -> TOP이라는 함수가 있음??
     - 진짜 모름...
  3. FETCH? 이건 또 뭐임



SELECT NO, 
       RANK() OVER(ORDER BY JUMSU DESC) AS RANK1, 
       DENSE_RANK() OVER(ORDER BY JUMSU DESC) AS RANK2, 
       ROW_NUMBER() OVER(ORDER BY JUMSU DESC) AS RANK3 
FROM STUDENT;


no.26
  SELECT COUNT(COL1), 
         COUNT(COL2) 
  FROM ( 
    SELECT DISTINCT COL1, COL2 
    FROM TEST40 
  );
  <img width="261" height="135" alt="image" src="https://github.com/user-attachments/assets/88fc4afb-0171-4bd7-891d-0d77bbb5ea52" />
  - 위 함수의 결과가 어떻게 될까?
  - 일단 distinct는 select에 해당하는 모든 colnume에 적용되는 게 맞을 거임
  - 그럼 조조와 다른 값은 일단 하나 말고는 없음
  - 근데 이 논리면 1,1 이 나와야하는데 보기에 없음
    - 그니깐 최대한 많은 칼럼을 살려야 함
    - 적어도 두 보기의 개수는 NULL이 없음으로 똑같음

  
SELECT COUNT(*) AS RESULT 
FROM TAB1 
WHERE COL1 = 200 
GROUP BY COL1; 
>> 0

SELECT SUM(COL2) AS RESULT 
FROM TAB1 
WHERE COL1 = 100; 
>> 0

SELECT COUNT(COL1) AS RESULT 
FROM TAB1 
WHERE COL3 = 400;
>> 0


<조건> 
DEPT_ID라는 정수형 컬럼을 새로 추가해야 한다. 
SALARY 컬럼은 NULL을 허용하지 않도록 수정해야 한다. 
EMAIL 컬럼은 삭제하려고 한다. 
DEPT_ID 컬럼에 외래키 제약조건(FK_EMP_DEPT)을 부여하려 한다.

ALTER TABLE EMP 
  ADD DEPT_ID NUMBER CONSTRAINT FK_EMP_DEPT FOREIGN KEY(DEPT_ID)
  DROP COLUMN EAMIL
  MODIFY COLUMN SALATY ADD CONSTRAINT 

NO.30
- DDL 많이 써보자..
  - 뭐부터 써야할 지 모르겠닭


NO. 31 아래 4개중에 고르기
  - WHERE 절이랑 SELECT 절에서 출연료 칼럼 똑같은 거로 답 고름
  - 이게 두 개의 칼럼이 똑같아야 되는 지는 잘 모르겠음
  - 2번은 AND 조건에서 그냥 영화번호 해버리면 어느 엔티티인지 몰라서 답 아님

SELECT 영화.영화명, 
       배우.배우명, 
       출연료 
FROM 배우, 영화, 출연 
WHERE 출연료 >= 8888 
      AND 출연.영화번호 = 영화.영화번호 
      AND 출연.배우번호 = 배우.배우번호;

 SELECT 영화명, 
        배우명, 
        출연료 
FROM 배우, 영화, 출연 
WHERE 출연료 >= 8888 
      AND 영화번호 = 영화.영화번호 
      AND 배우번호 = 배우.배우번호;

 SELECT 영화.영화명, 
        배우.배우명,
        출연료 
FROM 영화, 배우, 출연 
WHERE 출연.출연료〉8888 
      AND 출연.영화번호 = 영화.영화번호 
      AND 영화.영화번호 = 배우. 배우번호;

 SELECT 출연.영화명, 
        영화.배우명, 
        출연.출연료 
FROM 배우, 영화, 출연 
WHERE 출연료〉= 8888 
      AND 출연.영화번호 = 영화.영화번호 
      AND 출연.배우번호 = 배우.배우번호;


NO. 35
  
  SELECT 
    ADD_MONTHS(
      TO_DATE('2024/08/24 10:00:00', 'YYYY/MM/DD HH24:MI:SS') - 10, -3
    ) + 10/24/60 FROM DUAL;

  - 일단 DATE TYPE 의 산술 연산 결과가 뭔지 헷갈림
    - 그래도 일단 10시간이 빠진다고 해보자
  - ADD MONTH의 결과는 3개 빠지니깐 5월임
  - 그럼 거기다 + 10/24/60 해주면
  - 2024/5/24 10:24:60 인데 이럼 2024/5/25 11:01:00 아닌가?
  - 일단 보기에 없음




no.36 
- 아래 선지 중에 오류를 뱉는 거를 모르겠음


 SELECT 메뉴ID, 
        사용유형코드, 
        AVG(COUNT(*)) AS AVGCNT 
FROM 시스템사용이력 
GROUP BY 메뉴ID, 사용유형코드;

SELECT 메뉴ID, 
       사용유형코드, 
       COUNT(*) AS CNT 
FROM 시스템사용이력 
WHERE 사용일시 BETWEEN SYSDATE - 1 AND SYSDATE 
GROUP BY 메뉴ID, 사용유형코드 
HAVING 메뉴ID = 3 AND 사용유형코드 = 100；

 SELECT SUM(주문금액) AS 합계 FROM 주문 HAVING AVG(주문금액) > 100；

- HASH JOIN
  - 걍 뭔지 모르겠음
    
NO.38

사원 500명, 
대리 100명, 
과장 30명, 
차장 10명, 
부장 5명, 
직급이 정해지지 않은(NULL) 사람 25명
결과 건수를 순서대로 나열한 것은?

아니 sql1은 결과건수가 1 아닌가;; 645는 결과고 ㅇㅇ 
- GROUP BY가 NULL을 제외하고 묶는가 아닌가.. 일단 나는 같이 묶는다에 한 표를 건다

SQL1) SELECT COUNT(GRADE) FROM EMP; >>  645
SQL2) SELECT GRADE FROM EMP WHERE GRADE IN('차장', '부장', '널'); >> 15  
SQL3) SELECT GRADE, COUNT(*) FROM EMP GROUP BY GRADE; >>



NO. 39 
  - ORDER BY 에 CASE 가 섞인 경우
  
  SELECT ID 
  FROM TAB1 
  ORDER BY CASE WHEN ID > 'B' THEN 'A' ELSE ID END, 
           ID;
  
  - ID가 'B' 보다 커야 됨
  - 문자끼리 대소비교.. -> 동일개수 문자면 아스키코드 비교할 텐데
  -> 일단 사전식으로 비교해서 사전의 뒷부분에 있으면 큰 걸로 ㄱㄱ
  만약에 같으면 ID있으니깐 오름차순 사전식 ㄱㄱ

  - > 'B' -> BI, BAA, 
  AA, ABC, B
>> BAA BI AA ABC B


NO.43 이거 답 뭔지 모르겠음
  - 일단 MINUS 기준이 뭔지 모르겠어서 걍 MINUS 때렸는데 맞는지는 모르겠음
 (
 SELECT TO_CHAR(EMPNO) AS EMPNO, 
         ENAME, 
         SAL 
 FROM EMP 
 UNION 
 SELECT EMPLOYEE_ID AS EMPNO, 
        NAME, 
        SALARY 
FROM EMPLOYEES
) 
ORDER BY EMPNO;


 (
SELECT TO_CHAR(EMPNO) AS EMPNO, 
        ENAME, 
        SAL 
FROM EMP 
UNION 
SELECT EMPLOYEE_ID AS EMPNO, 
       NAME, 
       SALARY 
FROM EMPLOYEES
) 
ORDER BY EMPNO;

SELECT ENAME, SAL FROM EMP 
MINUS 
SELECT NAME, SALARY FROM EMPLOYEES;

SELECT DEPTNO, 
       SUM(SAL) AS SUM_SAL 
FROM EMP 
GROUP BY DEPTNO 
UNION ALL 
SELECT DEPARTMENT_ID, 
       SUM(SALARY) 
FROM EMPLOYEES 
GROUP BY DEPARTMENT_ID;



NO.46
SELECT REGEXP_SUBSTR(
        'ORA-00600 Oracle SQL-Server 50', '[^0-9]+') "REGEXPR_SUBSTR" FROM DUAL;

- 이럼 "0","-","9" 뻬고 찾는거임 아님 숫자 빼고 찾는 거임?


NO.47

SELECT 사원번호, 이름, LEVEL 
FROM 사원 
WHERE 지역 = '경기' 
START WITH 상위관리자코드 IS NULL 
CONNECT BY 상위관리자코드 = PRIOR 사원번호;
- 이럼 지역 = '경기' 부터 찾는 건지 아님 먼저 계층구조 만들고 지역 = '경기' 찾는 건지 모름
- 근데 조건절로 걸러내고 트리만들면, 계층구조가 아에 무너져서 안보이는 인스턴스가 너무 많이 생김

둘 다 ㄱㄱ

NO.49 
<img width="645" height="679" alt="image" src="https://github.com/user-attachments/assets/7184f3b3-baf5-4d5e-a98e-35ec4a076ec8" />
  - 연도 월 일 이 /인지 -인지 모르겠다







