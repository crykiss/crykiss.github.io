---
layout: post
author: danny Kim
title: "jetty embedded 디렉토리목록 표시금지"
category: "jetty"
tags: jetty
---

jetty embedded 에서 URL 끝에 / 로 접근 시 디렉토리 목록이 표시되는데
금지하려면 아래 셋팅을 하면 된다.
```
WebAppContext webContext = new WebAppContext();
webContext.setInitParameter("org.eclipse.jetty.servlet.Default.dirAllowed", "false");
```
