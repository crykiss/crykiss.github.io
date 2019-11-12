---
layout: post
author: danny Kim
title: "Visual Studio 디버그 컴파일 시 vcpkg x86-windows 연결하기"
category: "visual studio"
tags:  vcpkg "visual studio" debug link
---
기존에는 vcpkg 를 사용 할 때 Global 로 static 을 지정해서 사용하고 있었다.
boost lib 를 사용하려 하는데 lib 충돌이 발생했다.

원인이 뭔지 찾아보니 debug 와 release lib 컴파일 차이로 인한 오류다.
release 컴파일 시에는 오류 없이 컴파일이 정상 완료 된다.

debug 로 컴파일 시 오류 제거를 위해서 따로 설정을 추가 했다.

{% highlight xml %}
<PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|Win32'" Label="Configuration">
    <ConfigurationType>Application</ConfigurationType>
    <UseDebugLibraries>true</UseDebugLibraries>
    <PlatformToolset>v141</PlatformToolset>
    <CharacterSet>Unicode</CharacterSet>
    <UseOfMfc>Dynamic</UseOfMfc>
	<VcpkgTriplet>x86-windows</VcpkgTriplet>
  </PropertyGroup>
{% endhighlight %}

추가적으로 `VcpkgTriplet 만 지정을 했다.
기존에 Global 은 static 설정에서 변경을 하지 않았다.

이 후 Debug로 정상 컴파일 확인했다.
