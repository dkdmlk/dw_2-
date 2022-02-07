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