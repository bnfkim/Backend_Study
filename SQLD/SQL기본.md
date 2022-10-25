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

#### 참조 무결성에 의한 DELETE ACTION 참조동작
1) cascade : 부모 삭제 시 자식도 같이 삭제
2) set null : 부모 삭제 시 자식 해당 필드 null
3) set default : 부모 삭제 시 자식 해당 필드 디폴트 값으로 설정
4) restrict : 자식 테이블에 PK 값이 없는 경우에만 부모 삭제 허용
5) no action : 참조 무결성을 위반하는 삭제/수정 액션을 취하지 않음

### 참조무결성에 의한 INSERT ACTION 참조동작
1) Automatic : 부모 테이블에 PK가 없는 경우 부모 PK를 생성 후 자식 입력
2) Set Null : 부모 테이블에 PK가 없는 경우 자식 외부키를 null 값으로 처리
3) Set Default : 부모 테이블에 PK가 없는 경우 자식 외부키를 지정된 기본 값으로 입력
4) Dependent : 부모 테이블에 PK가 존재할 때만 자식 입력 허용
5) No Action : 참조 무결성을 위반하는 입력 액션을 취하지 않음

### 테이블 이름 변경하는 방법
- RENAME '기존 테이블 명' TO '바꿀 테이블 명'

### 삭제와 로그
- TRUNCATE TABLE
  - 로그 안 남김 (롤백 불가)
  - 특정 테이블의 모든 데이터 삭제
  - 디스크 사용량 초기화 (테이블을 최초 생성된 초기화 상태로 만듬)
  - 자동 커밋
- DROP TABLE
  - 로그 안 남김 (롤백 불가)
  - 테이블의 데이터 모두 삭제
  - 디스크 사용량 초기화 가능하지만 테이블의 스키마 정의도 함께 삭제 (테이블 정의 자체를 완전히 삭제)
  - 자동커밋
- DELETE FROM
  - 로그 남김 (커밋 이전 롤백 가능)
  - 테이블의 데이터 모두 삭제하지만 디스크 사용량을 초기화 하지는 않음
  - 사용자 커밋

### DISTINCT
- 데이터의 중복을 제거하는 명령어
- GROUP BY문을 사용하여 중복을 제거할 수도 있음

### 데이터베이스 트랜잭션 4가지 특성
1) 원자성 : 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아있어야 한다
2) 일관성 : 트랜잭션이 실행 되기 전의 데이터베이스 내용이 잘못되어 있지 않아면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안 된다
3) 고립성 : 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어져서는 안 된다
4) 지속성 : 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다

### 트랜잭션에 대한 격리성이 낮은 경우 발생할 수 있는 문제점 4가지
- Dirty Read
  - 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터를 읽는 것을 말한다
- Non-Repeatable Read
  - 한 트랜잭션 내에서 같은 쿼리를 두 번 수행했는데, 그 사이에 다른 트랜잭션이 값을 수정 또는 삭제하는 바람에 두 쿼리 결과가 다르게 나타나는 형상
- Phantom Read
  - 한 트랜잭션 내에서 같은 쿼리를 두 번 수행했는데, 첫번째 쿼리에서 없던 유령 레코드가 두번째 쿼리에서 나타나는 형상

### 롤백(Rollback)
- 커밋 이전에는 변경 사항을 취소할 수 있다
- 데이터 변경 사항이 취소되어 데이터의 이전 상태로 복구되며 관련된 행에 대한 잠금이 풀리고 다른 사용자들이 데이터 변경을 할 수 있게 된다
- 

### ORACLE, SQL Server
- ORACLE에서 DDL 문장의 수행은 내부적으로 트랜잭션을 종료시키므로
- ORACLE 에서는 DDL 문장 수행 후 자동으로 COMMIT을 수행
- SQL Server에서는 DDL 문장 수행 후 자동으로 COMMIT 수행하지 않는다
- SQL Server에서는 CREATE TABLE 문장도 TRANSACTION의 범주에 포함된다.


