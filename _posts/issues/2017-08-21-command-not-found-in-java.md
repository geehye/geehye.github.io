---
title: How to solve "bash: javac: command not found"
date: 2017-08-21
layout:
categories: issues
---

`$ java -version` 은 확인이 가능한데, <code>$ javac -version</code> 은 <u>명령어를 찾을 수 없습니다</u>가 뜨는 경우 해결하기

> 분명 JAVA_HOME도 완벽히 설정했다면, jdk를 추가로 설치해야 하는 문제일 수 있다.

<br>

##### 1. 설치 가능 목록 확인
<pre>
$ sudo yum list java*jdk-devel<br>
Loaded plugins: fastestmirror, langpacks
Loading mirror speeds from cached hostfile
 * base: ftp.daumkakao.com
 * extras: ftp.daumkakao.com
 * updates: ftp.daumkakao.com
Available Packages
java-1.6.0-openjdk-devel.x86_64                                        1:1.6.0.41-1.13.13.1.el7_3                                         updates
java-1.7.0-openjdk-devel.x86_64                                        1:1.7.0.141-2.6.10.1.el7_3                                         updates
java-1.8.0-openjdk-devel.i686                                          1:1.8.0.141-1.b16.el7_3                                            updates
java-1.8.0-openjdk-devel.x86_64                                        1:1.8.0.141-1.b16.el7_3                                            updates
</pre>

<br>
##### 2. 본인 java 버전과 동일한 버전 설치
<pre>
$ sudo yum install java-1.8.0-openjdk-devel.x86_64
</pre>

<br>
##### 3. 설치 확인
<pre>
$ javac -version<br>
javac 1.8.0_141
</pre>
