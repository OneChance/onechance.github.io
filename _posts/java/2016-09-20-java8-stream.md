---
layout: post
comments: true
categories: java
---

# 内部迭代

```
shapes.foreach(s -> s.setColor(RED));
```

```
shapes.stream()
      .filter(s -> s.getColor() == BLUE)
      .forEach(s -> s.setColor(RED));
```
###### 在Collection上调用stream()会生成该集合元素的流，接下来filter()操作会产生只包含蓝色形状的流，最后，这些蓝色形状会被forEach操作设为红色

###### 如果我们想把蓝色的形状提取到新的List里，则可以
```
List<Shape> blue = shapes.stream()
                          .filter(s -> s.getColor() == BLUE)
                          .collect(Collectors.toList());
```
###### collect()操作会把其接收的元素聚集到一起（这里是List），collect()方法的参数则被用来指定如何进行聚集操作。在这里我们使用toList()以把元素输出到List中

###### 如果每个形状都被保存在Box里，然后我们想知道哪个盒子至少包含一个蓝色形状，我们可以这么写

```
Set<Box> hasBlueShape = shapes.stream()
                               .filter(s -> s.getColor() == BLUE)
                              .map(s -> s.getContainingBox())
                              .collect(Collectors.toSet());
```
###### map()操作通过映射函数（这里的映射函数接收一个形状，然后返回包含它的盒子）对输入流里面的元素进行依次转换，然后产生新流

###### 如果我们需要得到蓝色物体的总重量，我们可以这样表达
```
int sum = shapes.stream()
                .filter(s -> s.getColor() == BLUE)
                .mapToInt(s -> s.getWeight())
                .sum();
```
###### 这里的filter()和map()都是惰性的，这就意味着在调用sum()之前不会从数据源中提取任何元素。在sum()操作之后才会把filter()、map()和sum()放在对数据源一次遍历中。这样可以大大减少维持中间结果所带来的开销