---
layout: post
author: danny Kim
title: "javascript 문자열 다중 라인으로 입력"
category: "web"
tags: web 2019 javascript string 자바스크립트
---

javascript 사용하다 보면 문자열을 입력할 때 다중 라인으로 입력 해 주고 싶을 때가 있다.
그럴 땐 \ (원표시) 를 끝에 붙여주면 간단히 사용 할 수 있다.

{% highlight javascript %}
var a = '처음 라인\
 그 다음 라인\
	그그 다음 라인';
{% endhighlight %}

```
마지막에는 \ 를 붙여서는 안된다.
" 를 표시 할 때는 \" 를 써야한다.
```
