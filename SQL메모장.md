***서브쿼리가 가능한 곳
서브쿼리를 쓰기전에 한번 생각!.
정말필요한가?
1. ***SELECT
        a테이블(감기관련),
        b테이블(코로나 확진 관련),
        c테이블(오미클론 확진자 관련)
    조건: 교집합 데이터(칼럼)이 없음.
    실행. 서브쿼리가 먼저 실행된 후 외부쿼리 실행
        SELECT 
            COUNT(*) as 감기확진, //감기 확진 수
            (SELECT COUNT(*)FROM코로나 )as 코로나 확진,
            (SELECT COUNT(*)FROM 오미크론) as 오미크론 확진   
        FROM 날씨
2. ***FROM
    FROM 서브쿼리 :
    언제 데이터를 먼저 필터링 해야할 때
    ex) emp테이블에 (급여가 3000천 이하) 을 찾고싶을떄.
3. ***WHERE
    where 서브쿼리:
    -단일행
    SELECT * FROM emp
    WHERE ename = (SELECT ename FROM emp WHERE empno = 3000)
    -다중행
    in : 시제로 존재하는 데이터의 값을 비교
    데이터가 많아지면 많아질 수록 속도가 느려짐.
    SELECT * FROM emp
    WHERE ename in (SELECT ename FROM emp WHERE sal <> 3000)
---------------
sql
DML
- select

- insert : 데이터를 저장
    작성법 1.
    INSERT INTI 테이블 이름(컬럼이름 [ex)'name',sal,job])
    VALUES(컬럼에해당하는데이터 [ex)'홍길동',3000,'manager']) 
    주의 : 테이블에 NULLABLE 
        1. 테이블에 job컬럼이 not null이면, insert할떄 무저건 데이터를 넣어야 함. 
        2. 테이블에 기본키가 auto increment 가 아니라면, 기본키 데이터를 넣어야 함.
        3. commit 을해야  최종 insert가 됨. (디비버 같은 프로그램은 auto commit 으로 설정되어 있음.)
    작성법 2.
    해당 테이블에 데이터를 모두 넣으면, 테이블 뒤 괄호 생략
    INSERT INTI 테이블
    VALUES(컬럼에해당하는데이터 [ex)'홍길동',3000,'manager',...])

- delete : 데이터 삭제
    작성법
    DELETE FROM 테이블이름
    wHERE 컬럼 = 70
    주의 : 
        1. 해당 컬럼이 ON DELETE CASCADE 로 설정되어 있으면, 연관된 컬럼 모두 삭제됨.
    실제로는 데이터 삭제x
    삭제여부 컬럼을 만듬 ex) 컬럼이름 : 회원탈퇴 여부
                             데이터 : 'y' or 'n'
- update