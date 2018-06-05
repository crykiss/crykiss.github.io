 sqlite3 를 cpp에 사용하기 위해서 검색을 하던 도중 [sqlite_modern_cpp](https://github.com/SqliteModernCpp/sqlite_modern_cpp) 프로젝트를 발견했다. c++14 스타일의 코드로 사용하기 좋아보였다. 페이지에 보니 vcpkg를 이용할 수 있도록 되어 있어서 vcpkg를 이용해서 바로 인스톨 하였다.
 
 vcpkg search sqlite
 vcpkg install sqlite-modern-cpp
 
 그런데 컴파일을 진행하려고 하니 오류가 발생되었다.
 
 오류는 매크로 문자열정의 에러인데
 
{% highlight html %}
{% raw %}{% highlight c++ %}    
 매크로A(
   매크로
   매크로
   매크로
   매크로
   )   
{% endhighlight %}{% endraw %}


 위와 같이 구성되어야 하는데
 
 {% raw %}{% highlight cpp %}    
 매크로A(
   매크로
 #ifdef A
   매크로1
 #endif
   매크로2
   )
{% endhighlight %}{% endraw %}
{% endhighlight %}
   
 소스가 위와 같이 되어 있다보니 매크로A 해석 중에 '#'을 만나서 발생하는 문제였다.
 물론 내가 작성한건 아니어서 처음에는 어떻게 해야 해결이 되나 찾아봤지만
 결국 sqlite-modern-cpp의 최신소스에서는 위와 같은 #ifdef 가 제거가 되어 있었다.
 
 vcpkg에 보면 늘상 버전이 조금씩 늦는 경향이 있는거 같다. openssl도 그렇고......
 vcpkg의 설치 폴더에 가보면 h 들이 쭉 있는데 (sqlite-modern-cpp는 h로만 구성된 lib)
 최신버전을 엎어치면 컴파일 오류가 사라진다.
