
<div align="center" id="top">
<img height="270px" width="270px" src="./logo.png"><br>
  <h1>📃개념 및 궁금증 정리</h1>
</div>

***
- 이클립스 Spring Tool Suite(STS) 설치 (Legacy Project 등 이전 버전의 부가기능을 사용하고자 할 때)
  - pring Tools 3 Add-On for Spring Tools 4 3.9.14(Spring framework 설치)
---

## DB에서의 데이터 암호화 - ex)주민번호, 비밀번호...
#### <암호화>
```
CREATE OR REPLACE FUNCTION f_Encrypt (p_Input_str  in varchar2) RETURN VARCHAR2
AS
 v_Input_len number := ROUND(LENGTH(p_Input_str)/8+0.5)*8;
 v_Encrypted_str varchar2(2000) := null;
 v_Key varchar2(16) := 'abcdefgh12345678';
BEGIN
   DBMS_OBFUSCATION_TOOLKIT.DESENcrypt(input_string => RPAD(p_Input_str,
                                       v_Input_len),
                                       key_string => v_Key,
                                       encrypted_string =>v_Encrypted_str);

   RETURN v_Encrypted_str;
END;
/
```

#### <복호화>
```
CREATE OR REPLACE FUNCTION f_Decrypt (p_Encrypted_str in varchar2) RETURN VARCHAR2
AS
 v_Key varchar2(16) := 'abcdefgh12345678';
 v_Decrypted_str varchar2(2000);
BEGIN
   DBMS_OBFUSCATION_TOOLKIT.DESDecrypt(input_string => p_Encrypted_str, 
                                     key_string => v_Key,
                                     decrypted_string => v_Decrypted_str);

   RETURN trim(v_Decrypted_str);
END;
/
```

```
//암호화로 데이터 입력
insert into imsi(id, password) values('AAA', f_Encrypt('1234'));
//그냥 조회시 암호화 되어있다
select id, password from imsi;
//복호화로 변화 조회시 실제 값이 보인다
select id, f_Decrypt(password) from imsi;
```

***

## SELECT 해서 INSERT하기
```
INSERT INTO emp (empno, ename, job, mgr, hiredate)
SELECT 8001
     , 'GENT'
     , a.job
     , a.mgr
     , TO_DATE('2021-05-03', 'YYYY-MM-DD')
  FROM emp a
 WHERE empno = 7698
```

## 글자or숫자 길이에 따른 조회(SELECT)
- ex) 계좌번호가 13자리 이하인 대상의 급여테이블 정보를 출력하시오.
```
select *
from ex1_salgrade
where length(act_no) <=13;
```

## 특정 문자가 포함된 데이터 조회(SELECT)
- ex) 사원이름에 'A'가 포함된 사원의 사원이름을 출력하시오.
```
select ename
from ex1_emp
where ename like '%A%';
```
