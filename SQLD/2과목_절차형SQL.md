# 절차형 SQL(PL/SQL, T-SQL)

---

### 절차형 SQL

- SQL문의 **연속적인 실행**이나 **조건에 따른 분기처리**를 이용해 특정 기능을 수행하는 저장 모듈을 생성할 수 있도록 하는 SQL
    - PL/SQL → oracle
    - T-SQL → SQL Server

### PL/SQL

- Block내 `DML`, `QUERY`, `IF`, `LOOP` 등을 사용 가능
    - Block 구조
        
        → 각 기능별로 모듈화 가능
        
        → Block 으로 묶어서 한번에 전부 서버로 보내므로 통신량을 줄일 수 있음
        
    - IF, LOOP 등의 절차형 언어
        
        → 절차적인 프로그램이 가능
        
- `변수`와 `상수` 등을 사용 가능
    - 일반 SQL문을 실행할 때 `Where` 절의 조건 등으로 대입 가능
    - 변수, 상수 등을 선언하여 SQL 문장 간 값을 **교환 가능**
- `Procedure`, `User Defined Function`, `Trigger` 객체를 PL/SQL 로 작성 가능
    - 작성자가 트랜잭션 분할 가능
    - `Procedure` 내에서 다른 `Procedure` 호출시, 호출 프로시저의 트랜잭션과는 별도로 자율 트랜잭션 처리 가능
        - PRAGMA AUTOMOUS_TRANSACTION
- DBMS 정의 에러나 사용자 정의 에러를 정의해 사용 가능
- Oracle 과 PL/SQL 을 지원하는 어떤 서버로도 프로그램 이동 가능

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b29da439-ecb3-4f1c-9af4-932f6555f56a/Untitled.png)

- DECLARE
    - BEGIN ~ END 에서 사용될 변수와 인수에 대한 정의 및 데이터 타입 선언부
- BEGIN ~ END
    - 처리하고자 하는 SQL, 비교문, 제어문을 이용해 필요한 로직을 처리하는 실행부
- EXCEPTION
    - BEGIN ~ END 에서 실행되는 SQL이 발생하는 에러를 어떻게 처리할 것인지 정의하는 예외 처리부

### T-SQL

- 변수 선언 가능
    - `@@` → 전역변수 : 이미 SQL에 내장된 변수 존재
    - `@` → 지역변수 : 사용자가 자신의 연결 시간동안만 사용하기위해 만들어지는 변수 존재
- 데이터 유형 제공
    - INT, FLOATE, VARCHAR
- 연산자 사용가능
    - 산술연산자, 비교연산자, 논리연산자 사용 가능
- 흐름 제어 기능
    - IF ~ ElSE, WHILE, CASE - THEN
- 주석 기능
    - 한줄 주석 : `--`
    - 여러 주석 : `/* */`

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/78568876-7f81-425e-81ab-ad4a1a207840/Untitled.png)

- `DECLARE`
    - BEGIN ~ END 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입을 선언하는 선언부
- `BEGIN ~ END`
    - 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용하여 필요한 로직을 처리하는 실행부
    - BEGIN, END 문을 반드시 사용해야하는 것은 아니지만 블록 단위로 처리하고자 할 때는 반드시 작성
- `ERROR`
    - BEGIN ~ END 절에서 실행되는 SQL문이 발생하는 에러를 어떻게 처리할 것이지를 정의하는 예외 처리부
