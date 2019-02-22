---
title: How to get or show original data from 'oracle.sql.clob' column
date: 2017-11-15
layout:
categories: issues
---

SELECT <b>dbms_lob.substr</b>(COLUNM_NAME)<br>
FROM TABLE_NAME
