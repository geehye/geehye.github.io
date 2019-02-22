---
title: How to dump MySQL in Linux
date: 2017-08-30
layout:
categories: issues
---

##### 1. dump

<pre>
$ [path/to/]mysqldump [database_name] -u[id] -p > [database_name].sql
</pre>

* '허가거부' 에러가 발생했었는데 'mysqldump'명령어가 있는 디렉토리에 쓰기 권한이 없기 때문이었다.
따라서 'home' 디렉토리 위치에서 전체 path를 적어 실행해주었다.

<br>

##### 2. 원격 data 전송
<pre>
$ scp [file_name] [user_name]@[ip_address]:[destiny_path] 
</pre>
<br>

##### 3. get dump

<pre>
$ mysql -u[user_name] -p [database_name]
</pre>
