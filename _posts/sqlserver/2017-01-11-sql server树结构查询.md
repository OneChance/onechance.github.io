---
layout: post
comments: true
categories: sqlserver
---

![image](http://images.cnitblog.com/blog/347600/201306/25104716-b63ee4c14f3e45e4a131176bdaed9bbf.jpg)


```
WITH COL_CTE(Id,Name,ParentId,tLevel )
AS
(
    --基本语句
    SELECT Id,Name,ParentId,0 AS tLevel FROM Col
    WHERE ParentId = 0
    UNION ALL
    --递归语句
    SELECT c.Id,c.Name,c.ParentId,ce.tLevel+1 AS tLevel FROM COL as c 
    INNER JOIN COL_CTE AS ce 　　--递归调用
    ON c.ParentId = ce.Id
)

SELECT * FROM COL_CTE
```
![image](http://images.cnitblog.com/blog/347600/201306/25104945-111099a632634c26805bf41ea6416218.jpg)


```
SELECT * FROM COL_CTE
OPTION(MAXRECURSION 2)　　--指定最大递归次数为2
```

![image](http://images.cnitblog.com/blog/347600/201306/25105613-0a6d25e8baab41458e4746d4aaf4cda9.jpg)