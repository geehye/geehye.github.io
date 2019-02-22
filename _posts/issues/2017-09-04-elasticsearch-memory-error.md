---
title: How to solve "max virtual memory error" in Elasticsearch
date: 2017-09-04
layout:
categories: issues
---

##### 1. problem
after starting Elasticsearch, an error has occured.

<em>error : max virtual memory areas vm.max_map_count [4096] is too low,
increse to at least [65530]</em>
<br>

##### 2. solution

add into limits.conf
<pre>
$ sudo vim /etc/security/limits.conf

'USER_NAME' hard nofile 262144
'USER_NAME' soft nofile 262144
'USER_NAME' hard nproc 262144
'USER_NAME' soft nproc 262144
'USER_NAME' hard memlock unlimited
'USER_NAME' soft memlock unlimited
</pre>

<br>
add into sysctl.conf

<pre>
$ sudo vim /etc/sysctl.conf

vm.max_map_count=262144
</pre>

after rebooting, done!!
