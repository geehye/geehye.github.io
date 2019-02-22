---
title: How to solve the problem when you create trigger in MariaDB
date: 2017-08-11
layout:
categories: issues
---

mariaDB에서 create trigger시 발생하는 에러 처리
<br>
#### error message

<pre>
SQL 오류 (1064): You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use </pre>
<br><br>
#### input sql code

<pre>
CREATE TRIGGER trg_triggerTest_update
BEFORE UPDATE ON TriggerTest
FOR EACH ROW
BEGIN
SET new.modifyDate = current_timestamp;
END;
</pre>
<br><br>
#### solution
code 앞에 <code>DELIMITER $$</code> 추가해준다.<br>
다음 줄에서 ctrl+Enter 를 이용해 한 줄 실행 시 위에 에러 코드 다시 나옴… (단, ctrl+F9는 잘 먹힘)<br>
DELIMITER는 명령 구분자를 바꿔주는 기능이다. 따라서 $$이거 하면, ‘;’ 이거 입력 시에 구분을 못 해서 단축키가 안 먹힌 것임.<br>
그리고 프로시저 만들 때는 DELIMITER가 반드시 필요하고 (+다시 <code>DELIMITER ;</code> 를 실행해주어야 다음부터 단축키 먹힘), 어떤 것으로 지정해주어도 무관하다. (트리거도 마찬가지 일 듯)
