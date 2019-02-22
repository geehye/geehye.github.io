---
title: How to solve the problem when 'sudo' doesn't work
date: 2017-09-04
layout:
categories: issues
---

##### 1. problem
```$ sudo``` not work

<pre>
$ sudo yum install ~~~~
<em>...is not in the sudoers file. This incident will be reported.</em>
</pre>
<br>

##### 2. solution
register user into /etc/sudoers<br><pre>
$ su -
$ chmod u+w /etc/sudoers
$ vi /etc/sudoers
</pre>
<br><br>

[/etc/sudoers 하단에 다음을 추가]
<pre>
'USER_NAME' ALL=(ALL) ALL
</pre>

<pre>
$ chmod u-w /etc/sudoers
</pre>

<br><br>
done!!
