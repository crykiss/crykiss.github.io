---
layout: post
author: danny Kim
title: "크롬(chrome)에서 http에서 -> https 강제전환 해결"
category: "tip"
tags: web chrome browser http https
---

크롬으로 https 에 접속한 사이트는 이후 http로 접속하더라도 강제적으로 https 변경

## 해결방법

크롬 주소창에 `chrome://net-internals` 입력 후 HSHTS 도메인 관련 삭제 처리

`delete domain` 을 수행한다.

도메인 검색 시 전체 경로를 모두 입력하자
```
abc.cry.com
```