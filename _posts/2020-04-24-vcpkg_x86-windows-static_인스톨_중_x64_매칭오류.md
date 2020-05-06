---
layout: post
author: danny Kim
title: "vcpkg x86-windows-static 인스톨 중 x64 모듈 충돌 발생"
category: "visual studio"
tags:  vcpkg "visual studio" insatll compile
---
vcpkg에서 특정 패키지를 x86-windows-static로 인스톨하는 중에 /MACHINE 설정이 없어서 기본으로 x64로 설정되어
모듈 충돌이 발생해서 install을 할 수 없었다.

![오류발생추적](https://github.com/crykiss/crykiss.github.io/blob/master/assets/images/KakaoTalk_20200424_102101299.png?raw=true)

log 파일을 통해서 원인 분석

![로그확인](https://github.com/crykiss/crykiss.github.io/blob/master/assets/images/KakaoTalk_20200424_102154809.png?raw=true)

기본값으로 x64가 지정되서 x86 과 충돌되는 모습

![원본소스경로](https://github.com/crykiss/crykiss.github.io/blob/master/assets/images/KakaoTalk_20200424_102239555.png?raw=true)

log 파일을 통해서 원인 분석

기본값으로 x64가 지정되서 x86 과 충돌되는 모습

vcpkg install 마다 소스를 복사해서 사용하므로 해당 소스 위치 확인

vs2017 cmd 창으로 통해서 직접 vcxproj 를 컴파일하면 정상적으로 컴파일이 되는 상황이라
x86 설정을 어떻게 주면 되지 않을까해서 찾아보게 되었다.

vcpkg 에서 수행하는 명령어는 로그상으로 확인해보면

MSBuild xxx.vcxproj 다.

그런데 xxx.vcxproj 를 직접 수정으로 컴파일을 하려고 했더니
> vcpkg install 을 실행 할때마다 새로 생성이 되었다.

어디선가 새로 생성하는 스크립트가 있을 것이라 생각하고 dngrep 프로그램을 활용하여 .vcxproj을 찾아가던 중
MSBuildProject.pm 파일 안에서 .vcxproj 가 만들어지는 것을 확인했다.

MSBuildProject.pm 안에 <PreferredToolArchitecture>x86</PreferredToolArchitecture> 값을 추가

```
  <PropertyGroup Label="Globals">
    <ProjectGuid>$self->{guid}</ProjectGuid>
    <PreferredToolArchitecture>x86</PreferredToolArchitecture>
```

이후 vcpkg 컴파일 수행하니 정상적으로 실행되었다.

.vcxproj 안에서 확인해보면 link 상에 분명 <TargetMachine>MachineX86</TargetMachine> 값이 있는데
x86 매칭을 하지 않는게 이상했는데
결국 모든 툴에 대한 설정값을 주는 PreferredToolArchitecture 설정을 통해서 해결 할 수 있었다.

기존에 poco 를 쓰고 있다가 vcpkg 업글과 함께 poco 고 업글하는 과정에서 이런 상황이 발생하였다.
물론 이건 poco의 문제가 아니라 vcpkg 안에서 poco 컴파일 스크립트의 문제라고 할 수 있겠다.