---
layout: post
title: "vcpkg에서 static으로 링크하도록 visual studio 설정하기"
date: 2018-06-11 14:12:00
author: danny Kim
category: visual studio
tags: vcpkg "visual studio" static link
---

vcpkg 로 install한 lib는 기본적으로 share 로 컴파일 되는데 static으로 컴파일 시키기 위해서는 설정이 필요하다.

'Visual Studio'의 프로젝트 파일(.vcxproj)을 열어보면 아래와 같이 'Globlas'설정이 있다.
{% highlight xml %}
  <PropertyGroup Label="Globals">
    <SccProjectName />
    <SccLocalPath />
    <Keyword>MFCProj</Keyword>
    <ProjectGuid>{5D97BAA1-7C7D-CCFB-DD38-0F63F576B143}</ProjectGuid>
    <WindowsTargetPlatformVersion>10.0.17134.0</WindowsTargetPlatformVersion>
    <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
    <VcpkgEnabled>true</VcpkgEnabled>
  </PropertyGroup>
{% endhighlight %}

아래 내용을 추가하면 static으로 링크가 된다.
```
    <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
    <VcpkgEnabled>true</VcpkgEnabled>
```

그전에 `vcpkg`에서 static으로 설치하는 것을 잊으면 안된다.
```
vcpkg install xxx:x86-windows-static
```
