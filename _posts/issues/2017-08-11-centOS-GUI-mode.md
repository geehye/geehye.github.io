---
title: How to boot centsOS 7 graphical login (GUI mode)
date: 2017-08-11
layout:
categories: issues
---

VertualBox에서 CentOS 7 GUI 모드로 실행하기
<br><br>
#### 1. GNOME desktop 그룹 설치

```
$ sudo yum groups install "GNOME Desktop"
```
<br><br>
#### 2. boot 설정

```
$ sudo systemctl set-default graphical.target
```
<br><br>
#### 3. GUI 로그인 모드로 실행

```
$ sudo systemctl start graphical.target
```
OR
```
$ sudo shutdown -r now
```
