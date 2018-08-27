---
layout: post
author: danny Kim
title: "letsencrypt 갱신 주의사항"
category: "web"
tags: letsencrypt ssl
---

letsencrypt는 90일의 유효기간이 있기 때문에 갱신을 해주어야 한다.
이번에 갱신 시점이 되어서 작업을 하다가
잘 안되는 점이 있었기에 기록을 남긴다.
최초에 letsencrypt 인증서를 만들때는 80포트를 이용했는데
갱신시에는 443 포트를 사용한다.
이 때문에 허송시간을 낭비하게 되었다.