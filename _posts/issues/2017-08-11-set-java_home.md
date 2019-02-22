---
title: How to set $JAVA_HOME
date: 2017-08-11
layout:
categories: issues
---

JAVA_HOME 설정 하기

<br>
#### 1. Java의 경로를 확인한다.

<pre>
$ which javac
/usr/bin/javac

$ readlink -f /usr/bin/javac
/usr/lib/jvm/java-1.8.0/bin/javac
</pre>

<br><br>
#### 2. /etc/profile에 JAVA_HOME 경로를 추가한다.

<pre>
export JAVA_HOME=/usr/lib/jvm/java-1.8.0
</pre>

<pre>
$ echo $JAVA_HOME
/usr/lib/jvm/java-1.8.0
</pre>

<br><br>
#### 3. 재부팅 후 경로가 제대로 설정되었는지 확인한다.

```
$ sudo shutdown -r now
```
