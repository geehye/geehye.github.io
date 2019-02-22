---
title: How to install NPM
date: 2017-08-11
layout:
categories: issues
---

npm 설치 방법

<br><code>
$ sudo yum install epel-release<br>
$ sudo yum install npm nodejs<br>
$ sudo yum install npm
</code>


##### solve "Error: Package: 1:nodejs-6.11.1-1.el7.x86_64 (epel)" 

```
$ sudo rpm -ivh https://kojipkgs.fedoraproject.org//packages/http-parser/2.7.1/3.el7/x86_64/http-parser-2.7.1-3.el7.x86_64.rpm && yum -y install nodejs
```
