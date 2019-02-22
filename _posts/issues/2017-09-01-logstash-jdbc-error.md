---
title: How to solve "out of memory error" when using Logstash JDBC input plugin
date: 2017-09-01
layout:
categories: issues
---

logstash input plugin 으로 JDBC 이용 시 문제 발생

<em>Exception when executing JDBC query {:exception=>#Sequel::DatabaseError: Java::JavaLang::OutOfMemoryError: Java heap space}
</em>
<br><br><br>

##### logstash.conf의 JDBC부분에 다음을 추가한다
<pre>
jdbc {
   jdbc_paging_enabled => true,
   jdbc_page_size => 200000
}
</pre>
