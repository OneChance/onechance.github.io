---
layout: post
comments: true
categories: front-end
---

###### 在给webpack2添加sass-loader后，发现使用@import嵌套的scss无法编译，在一番检查和试验后,发现原来import是这么写的：

```

@import url(./xxx.scss);

```

###### 虽然没有报错,不过无法编译,然后修改为：

```

@import './xxx.scss';

```

###### 之后，可以正常编译了.