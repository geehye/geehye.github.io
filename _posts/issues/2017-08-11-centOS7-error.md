---
title: How to solve "Cannot find a valid baseurl for repobase/7/x86_64"
date: 2017-08-11
layout:
categories: issues
---

yum 실행 시 발생하는 에러 처리
<br>
#### solution 1 : restart network interface

<pre>
$ ifconfig
enp0s3
</pre>

<pre>
$ ifdown ifcfg-enp0s3
$ ifup ifcfg-enp0s3
</pre>

<br><br>
#### solution 2

최초 centos 설치 시에 `ifconfig` command를 찾지 못 할 수 있다.
그럴 때 대신 해결할 수 있는 방법이다. 다음 command를 입력한 후 `$ sudo yum ~~~`를 진행하면 된다.

<pre>
$ dhclient
</pre>
