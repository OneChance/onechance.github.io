---
layout: post
comments: true
categories: java
---

# Lambda表达式

```
(int x, int y) -> x + y                      //接收x和y两个整形参数并返回他们的和
() -> 66                                     //不接收任何参数直接返回66
(String name) -> {System.out.println(name);} //接收一个字符串然后打印出来
(View view) -> {view.setText("lalala");}     //接收一个View对象并调用setText方法
```

## 概念

###### Java中大多数回调接口都只有一个方法：比如Runnable和Comparator；这些只拥有一个方法的接口称之为函数式接口

## 目标类型

```
Runnable runnable = () -> doSomething();  //这个表达式是Runnable类型的
Callback callback = () -> doSomething();  //这个表达式是Callback类型的
```

###### lambda表达式在不同的上下文里有不同的类型

###### 编译器利用lambda表达式所在的上下文所期待的类型来推导表达式的类型，这个被期待的类型被称为目标类型。lambda表达式只能出现在目标类型为函数式接口的上下文中

```
//编译器可以推导出s1和s2是String类型
Comparator<String> c = (s1, s2) -> s1.compareTo(s2);
//当表达式的参数只有一个时括号也是可以省略的
button.setOnClickListener(v -> v.setText("lalala"));
```

## 作用域

###### lambda表达式的语义就十分简单，作为内部类时，它不会从父类中继承任何变量，也不用引入新的作用域，this代表的就是外部类

## 变量捕获（内部类中引用的外部变量）

```
Runnable getRunnable(String name){
    String hello = "hello";
    return () -> System.out.println(hello+","+name);
}
```

###### Java8中放宽限制--对于lambda表达式和内部类，允许在其中捕获那些符合有效只读的局部变量（如果一个局部变量在初始化后从未被修改过，那么它就是有效只读）

###### 不过尽管Java8放宽了对捕获变量的语法限制，但试图修改捕获变量的行为是被禁止的，比如下面这个例子就是非法的

```
int sum  = 0;
list.forEach(i -> {sum += i;});
```

### 注意：

###### java中一个非静态内部类会默认持有外部类实例的强引用，这往往会造成内存泄露。而在lambda表达式中如果没有捕获外部类成员则不会保留对外部类实例的引用

## 方法引用

```
Comparator<User> comparator = Comparator.comparing(u -> u.getUserName());
```

###### 可以写成

```
Comparator<User> comparator = Comparator.comparing(User::getUserName);
```

#### 静态方法引用：ClassName::methodName

#### 实例上的实例方法引用：instanceReference::methodName

#### 超类上的实例方法引用：super::methodName

#### 类型上的实例方法引用：ClassName::methodName

#### 构造方法引用：Class::new

#### 数组构造方法引用：TypeName[]::new