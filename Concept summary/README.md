
<div align="center" id="top">
<img height="270px" width="270px" src="./logo.png"><br>
  <h1>๐๊ฐ๋ ๋ฐ ๊ถ๊ธ์ฆ ์ ๋ฆฌ</h1>
</div>

***
- ์ดํด๋ฆฝ์ค Spring Tool Suite(STS) ์ค์น (Legacy Project ๋ฑ ์ด์  ๋ฒ์ ์ ๋ถ๊ฐ๊ธฐ๋ฅ์ ์ฌ์ฉํ๊ณ ์ ํ  ๋)
  - pring Tools 3 Add-On for Spring Tools 4 3.9.14(Spring framework ์ค์น)
---

<div align="center">
<h1>ORACLE</h1>
</div>

## DB์์์ ๋ฐ์ดํฐ ์ํธํ - ex)์ฃผ๋ฏผ๋ฒํธ, ๋น๋ฐ๋ฒํธ...
#### <์ํธํ>
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

#### <๋ณตํธํ>
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
//์ํธํ๋ก ๋ฐ์ดํฐ ์๋ ฅ
insert into imsi(id, password) values('AAA', f_Encrypt('1234'));
//๊ทธ๋ฅ ์กฐํ์ ์ํธํ ๋์ด์๋ค
select id, password from imsi;
//๋ณตํธํ๋ก ๋ณํ ์กฐํ์ ์ค์  ๊ฐ์ด ๋ณด์ธ๋ค
select id, f_Decrypt(password) from imsi;
```

***

## SELECT ํด์ INSERTํ๊ธฐ
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

## ์ค์นผ๋ผ ์๋ธ์ฟผ๋ฆฌ
- SELECT ์ ์ ์ฌ์ฉํ๋ ์๋ธ์ฟผ๋ฆฌ๋ก์จ ๋จ์ํ JOIN์ ๋์ฒดํ  ๋ชฉ์ ์ผ๋ก ์ฌ์ฉ๋๋ ๊ฒฝ์ฐ๊ฐ ๋ง๋ค.
๋ค๋ง ํ ์ค์บ ๋ฑ์ ์ ๋ฐํ๋ ๋ฑ JOIN์ ๋นํด์ ์๊ณ ๋ฆฌ์ฆ์  ์ฑ๋ฅ๋ฉด์์ ๋ค์ ๋จ์ด์ง๊ธฐ ๋๋ฌธ์ JOIN์
ํ  ์ ์๋ ๊ฒฝ์ฐ๋ JOIN์ ํ๋๊ฒ ์ข๋ค.

- ๋ํ ์๋ธ์ฟผ๋ฆฌ์ ์กฐ๊ฑด์ ๋ฐ๋ผ ๋ฐ๋์ ํ๋์ ๊ฐ์ ์ถ๋ ฅํ๊ฒ ๋๋ฉฐ(๋จ ํ๊ฐ์ ํ์ ์ถ๋ ฅํ๋ค๋ ์๋ฏธ๊ฐ ์๋),
๋ง์ฝ์ ์๋ธ ์ฟผ๋ฆฌ์ ๊ฒฐ๊ณผ ๋ฐ์ดํฐ๊ฐ ์์ ๊ฒฝ์ฐ NULL๊ฐ์ ๋ฆฌํดํ๋ค. OUTERJOIN๊ณผ ๋ค์ ๋น์ทํ ์ญํ ์ ํ๋ค.
```
SELECT ename
        ,(SELECT dname
         FROM dept d
         WHERE d.deptno = e.deptno) dname
        ,job
FROM emp e
WHERE job = 'MANAGER';
===========================================================================================
ENAME    DNAME        JOB
JONES    RESEARCH     MANAGER
BLAKE    SALES        MANAGER
CLARK    ACCOUNTING   MANAGER
```



## ๊ธ์or์ซ์ ๊ธธ์ด์ ๋ฐ๋ฅธ ์กฐํ(SELECT)
- ex) ๊ณ์ข๋ฒํธ๊ฐ 13์๋ฆฌ ์ดํ์ธ ๋์์ ๊ธ์ฌํ์ด๋ธ ์ ๋ณด๋ฅผ ์ถ๋ ฅํ์์ค.
```
select *
from ex1_salgrade
where length(act_no) <=13;
```

## ํน์  ๋ฌธ์๊ฐ ํฌํจ๋ ๋ฐ์ดํฐ ์กฐํ(SELECT)
- ex) ์ฌ์์ด๋ฆ์ 'A'๊ฐ ํฌํจ๋ ์ฌ์์ ์ฌ์์ด๋ฆ์ ์ถ๋ ฅํ์์ค.
```
select ename
from ex1_emp
where ename like '%A%';
```


<div align="center">
<h1>MySQL</h1>
</div>

### <> -> !=(๊ฐ์ง์๋ค)

