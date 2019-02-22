---
title: How to include .jar files to compile .java file in CMD
date: 2017-11-08
layout:
categories: issues
---

<pre>
<b>> javac -cp ".;[PATH]/[JAR_FILE_NAME].jar;" [JAVA_FILE_NAME].java</b>
</pre>

ex) javac -cp ".;C:\Users\user\Desktop\test\test.jar;" test.java
