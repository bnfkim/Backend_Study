# 1️⃣ 정보 요구 사항

### **SQL 문장들의 종류**

- 데이터 조작어 (DML : Data Manipulation Language)
    - SELECT, INSERT, UPDATE, DELETE
- 데이터 정의어 (DDL : Data Definition Language)
    - CREATE, ALTER, DROP, RENAME
- 데이터 제어어 (DCL : Data Control Language)
    - GRANT, REVOKE
- 트랜잭션 제어어 (TCL : Transaction Control Language)
    - COMMIT, ROLLBACK

# 2️⃣ DDL

테이블, 뷰, 인덱스, 시퀀스, 동의어 등 객체를 생성-삭제-수정 하는데 사용

**CREATE** : 객체 생성

**DROP**: 객체 삭제

**ALTER**:  객체 변경

**RENAME** : 객체 이름 변경

**TRUNCATE TABLE** : 테이블 내의 데이터 전부 삭제[복구 불가]

## CREATE TABLE

- 칼럼에 대한 제약 조건 → `CONSTRAINT`를 이용해 추가 가능
- 기본키를 지정할 때는 `’칼럼명' '테이터타입' **PRIMARY KEY**`를 입력
- 다른 테이블을 참조할 때
    
    ```sql
    참조할칼럼명 데이터타입 **REFERENCES** 현테이블명(칼럼명) **ON** 조건절
    ```
    
    - `ON DELETE CASCADE` → 참조한 모든 데이터 삭제
    - `ON DELETE SET NULL` → 참조한 칼럼의 값이 NULL값
- SELECT 문을 활용한 테이블 생성[CTAS: Create Table ~ As Select ~ FROM ~]
    - 기존 테이블을 이용 → 칼럼 별 데이터 유형 재정의 불필요
    - 기존 테이블의 제약조건 중에 `NOT NULL`만 새로운 복제 테이블에 적용
    - 기본키, 고유키, 외래키, CHECK 등의 다른 제약 조건 미적용
    - 제약조건을 추가하기 위해서는 ALTER TABLE 기능을 사용

### CONSTRAINT

- `PK` : 중복 불가 + NULL 불가 + 테이블 당 하나
- `FK` : 중복 가능 + NULL 가능 + 참조 무결성 제약 옵션 선택 가능
- `UNIQUE` : 중복 불가 + 여러 개의 NULL 가능
- `NOT NULL` : 명시적으로 널 값 방지
- `CHECK` : 데이터의 무결성 유지하기위해 특정 컬럼에 설정

### **테이블명 생성시 주의사항**

1. 객체를 의미할 수있는 적절한 이름 사용

2. 가능한 단수형을 사용

3. 다른 테이블의 이름과 중복 불가

4. 한 테이블 내에서는 칼럼명이 중복되게 지정 불가

5. 테이블명과 칼럼명은 **반드시 문자로 시작**

6. 사전에 정의한 예약어 사용 불가

7. A~Z, a~z, 0-9, _, $, #만 사용 가능 [특수문자 사용 불가]

※ 기본적으로 테이블명이나 칼럼명은 대문자로 만들어짐

### FK 참조 무결성 제약조건

- DELETE ACTION
    - `ON DELETE CASCADE` : 참조한 child 테이블의 데이터까지 자동으로 삭제
    - `ON DELETE SET NULL` : 참조한 child 테이블 데이터가 NULL 값으로 변경
- INSERT
    - `AUTOMATIC` : PK 없는 경우, PK 생성 후 child 테이블 데이터 입력
    - `DEPENDENT` : PK가 있을 때만 child 테이블 데이터 입력 허용

## ALTER TABLE

```sql
ALTER TABLE 테이블명 ADD 추가할칼럼명 데이터유형;
ALTER TABLE 테이블명 ADD CONSTRAINT 제약조건명 제약조건 (칼럼명);
ALTER TABLE 테이블명 MODIFY (칼럼명 새로운데이터타입/길이 제약조건);
ALTER TABLE 테이블명 DROP COLUMN 칼럼명;
ALTER TABLE 테이블명 RENAME 새로운테이블명;
ALTER TABLE 테이블명 RENAME COLUMN 칼럼명 TO 새로운칼럼명;
```

- `CONSTRAINT` ‘PK이름’ `PRIMARY KEY` (’PK로 지정할 칼럼명’)
- 여러개의 컬럼을 동시에 수정하는 구문은 지원하지 않음

## DROP TABLE

```sql
DROP TABLE 테이블명;
DROP TABLE 테이블명 CASCADE CONSTRAINT;
TRUNCATE TABLE 테이블명;
```

- `CASCADE CONSTRAINT`를 함께 사용하면 해당 테이블의 데이터를 외래키로 **참조된 제약사항도 모두 삭제**
- `TRUNCATE TABLE`을 사용하면 해당 테이블에 들어있던 값들만 제거
    - 저장공간 재사용 가능
    - 테이블 구조를 완전히 삭제하기 위해서는 DROP TABLE 사용

| DELETE FROM | TRUNCATE | DROP |
| --- | --- | --- |
| DML | DDL(일부 DML 성격을 가짐) | DDL |
| Commit이전 ROLLBACK 가능 | ROLLBACK 불가능 | ROLLBACK불가능 |
| 사용자 Commit | Auto Commit | Auto Commit |
| 데이터만 삭제로그 기록 남음테이블 구조 유지 | 데이터 삭제로그 기록 삭제[용량 초기화]테이블 구조 유지 | 데이터 삭제로그 기록 삭제테이블 구조 삭제 |

### VIEW

- 테이블로부터 유도된 가상의 테이블
- 실제 데이터를 가지고 있지 않음
- 한번 생성된 뷰는 변경 불가 - ALTER 문 사용불가
    - CREATE VIEW : 뷰 생성
    - DROP VIEW : 뷰 삭제
- 뷰에 대한 입력, 수정, 삭제할 때 제약 존재

# 3️⃣ DML

- 사용자가 무슨 데이터 (what)를 원하는지 명세
    - 어떻게 데이터를 접근해야하는지 명세하는 것 → 절차적 언어(PL/SQL, T-SQL)
- 호스트 프로그램 속에 삽입되어 사용되는 DML 명령어들을 `데이터 부속어`라고 한다.

### SELECT

```sql
SELECT 칼럼명 FROM 테이블명 WHERE 원하는데이터의 조건 GROUP BY 칼람명 HAVING 조건 ORDER BY 칼람명;
```

- 정렬을 회피하고 싶을 경우 → INDEX 사용
    
    ```sql
    SELECT /*+ INDEX_DESC(A) */
    ```
    
- 중복된 데이터 한번만 조회
    
    ```sql
    SELECT **DISTINCT** 칼럼명 FROM 테이블명
    ```
    
- 사용자가 원하는 순서대로 정렬하고 싶을 경우
    
    ```sql
    CASE WHEN 조건 THEN 결과
    ```
    
- 실행 순서
    - `FROM` > `WEHRE` > `GROUP BY` > `HAVING` > `SELECT` > `ORDER BY`

### INSERT

### DELETE

**DELETE 와 FROM사이에 다른 문법이 들어가면 안됨**
!

| DELETE FROM | TRUNCATE | DROP |
| --- | --- | --- |
| DML | DDL(일부 DML 성격을 가짐) | DDL |
| Commit이전 ROLLBACK 가능 | ROLLBACK 불가능 | ROLLBACK불가능 |
| 사용자 Commit | Auto Commit | Auto Commit |
| 데이터만 삭제로그 기록 남음테이블 구조 유지 | 데이터 삭제로그 기록 삭제[용량 초기화]테이블 구조 유지 | 데이터 삭제로그 기록 삭제테이블 구조 삭제 |

### UPDATE
