---
layout: post
comments: true
categories: sqlserver
---

# 表结构
id    value  
----- ------   
1     aa  
1     bb  
2     aaa  
2     bbb  
2     ccc  

{% highlight java %}
/*stuff(param1, startIndex, length, param2)
说明：将param1中自startIndex(SQL中都是从1开始，而非0)起，删除length个字符，然后用param2替换删掉的字符。*/

SELECT id,value = stuff((SELECT ',' + value FROM tb AS t WHERE t .id = tb.id FOR xml path('')), 1, 1, '') FROM tb GROUP BY id
{% endhighlight %}