---
layout: post
author: danny Kim
title: "Visual Studio 디버깅 시 오류 발생할 때"
category: "visual studio"
tags:  vcpkg "visual studio" debug error
---
빌드는 되는데 디버깅시작(F5) 하면 웹 서버에서 디버깅을 시작할 수 없습니다 라고 메세지가 뜹니다.

잘되던 프로그램이 갑자기 디버깅이 안된다.

어떤걸 했었는지 생각해보면 금방 찾았겠지만

삽질끝에

디버깅 설정에서

디버깅 경로가 잘못되어서 발생하는 문제

경로 값을 잘못 입력했거나 공백이면 이 문제가 발생한다.