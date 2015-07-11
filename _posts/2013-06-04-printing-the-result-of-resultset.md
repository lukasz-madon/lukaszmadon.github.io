---
layout: post
title: Printing the result of ResultSet
date: 2013-06-04 20:26:32.000000000 +00:00
categories:
- Java
tags:
- java
- orm
- db
- api
---

Sample code for printing java.sql.ResultSet

```java
ResultSet rs = statement.executeQuery();
ResultSetMetaData rsmd = rs.getMetaData();
System.out.println("querying SELECT * FROM XXX");
int columnsNumber = rsmd.getColumnCount();
while (rs.next()) {
    for (int i = 1; i <= columnsNumber; i++) {
        if (i > 1) System.out.print(",  ");
        String columnValue = rs.getString(i);
        System.out.print(columnValue + " " + rsmd.getColumnName(i));
    }
    System.out.println("");
}
```
