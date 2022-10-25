### SQL 문장들의 종류
- 데이터 조작어 (DML : Data Manipulation Language)
  - SELECT (RETRIEVE)
    - 데이터베이스에 들어 있는 데이터를 조회하거나 검색하기 위한 명령어를 말하는 것 
  - INSERT, UPDATE, DELETE 
    - 테이블에 들어 있는 데이터에 변형을 가하는 종류의 명령어들
    - 데이터를 테이블에 새로운 행을 집어넣거나, 원하지 않는 데이터를 수정 혹은 삭제하는 명령어들
- 데이터 정의어 (DDL : Data Definition Language)
  - CREATE, ALTER, DROP, RENAME
    - 테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들
    - 그러한 구조를 생성하거나 변경하거나 삭제하거나 이름을 바꾸는 데이터 구조와 관련된 명령어들
- 데이터 제어어 (DCL : Data Control Language)
  - GRANT, REVOKE
    - 데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어
- 트랜잭션 제어어 (TCL : Transaction Control Language)
  - COMMIT, ROLLBACK
    - 논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위 별로 제어하는 명령어 

### 데이터 언어와 SQL 명령어
- 비절차적 데이터 조작어(DML)는 사용자가 무슨(what) 데이터를 원하는지만을 명세한다
- 절차적 데이터 조작어는 어떻게(how) 데이터를 접근해야 하는지 명세한다
- 절차적 데이터 조작어로는 PL/SQL (오라클), T-SQL(SQL Server)가 있다

### PK 설정 명령어
- CREATE TABLE PRODUCT ( CONSTRAINT PRODUCT_PK PRIMARY KEY (PROD_ID) );
- ALTER TABLE PRODUCT ADD CONSTRAINT PRODUCT_PK PRIMARY KEY (PROD_ID);
- ALTER TABLE \[테이블명] ADD CONSTRAINT \[pk 이름] PRIMARY KEY ( \[pk로 쓸 컬럼명])

### 테이블 칼럼에 대한 정의 변경
- 오라클 : ALTER TABLE '테이블 명' MODIFY ( '칼럼명' '데이터 유형' 'default 식' 'NOT NULL, '칼럼명2' ... )
- SQL Server : ALTER TABLE '테이블명' ALTER ( '칼럼명' '데이터 유형' 'default 식' 'NOT NULL, '칼럼명2' ... )

### NULL
- 모르는 값을 의미
- 값의 부재를 의미
- NULL과의 모든 비교는 알 수 없음으로 반환

### 옵션
- REFERENCES '참조할_테이블' '참조할_컬럼' \[ON DELETE CASCADE | ON DELETE SET NULL]
- ON DELETE CASCADE
  - 참조되는 부모 테이블의 행에 대한 DELETE를 허용한다.
  - 부모 테이블의 행이 지워지면 자식 테이블의 행도 같이 지워진다.
- ON DELETE SET NULL
  - 참조되는 부모 테이블의 행에 대한 DELETE를 허용한다.
  - 부모 테이블의 행이 지워지면 자식 테이블의 행은 NULL 값으로 설정된다.

### 제약조건의 종류 (Constraints)
- 데이이터 베이스에서 데이터의 무결성을 유지하기 위하여 테이블의 특정 컬럼에 설정하는 제약
- UNIQUE
  - 고유키, 테이블 내에서 중복되는 값이 없음, NULL 입력 가능
- PK
  - 주키로 테이블당 1개만 생성 가능
- FK
  - 외래키로 테이블 당 여러 개 생성 가능, NULL 입력 가능, 참조 무결성 제약을 받을 수 있음, 테이블 생성 시 설정할 수 있음
- NOT NULL
  - 명시적으로 NULL 입력 방지

### 테이블명과 칼럼명 규칙
- A-Z, a-z, 0-9, _ , $, # 만 허용

### 테이블의 불필요한 칼럼 삭제하는 명령어
- ALTER TABLE '테이블명' DROP COLUMN '삭제할 컬럼명'

