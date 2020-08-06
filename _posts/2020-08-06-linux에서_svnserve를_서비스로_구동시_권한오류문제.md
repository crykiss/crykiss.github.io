---
layout: post
author: danny Kim
title: "linux에서 svnserve를 서비스로 구동시 권한오류문제"
category: "linux"
tags:  linux svnserve svn chcon service centos
---
centos7 에서 svnserve를 사용하는데
cmd 에서 실행하는 서버는 정상적으로 외부에서 접근이 가능한 상태였다.

서비스에서 svnserve 를 구동시키기 위해서 환경설정을 진행하고 `systemctl start svnserve.service` 명령을 이용해서 구동을 시켰는데....

권한문제로 거절되는 현상이 계속 되었다.

chown 과 chmod 드으로 권한을 체크해보았지만 문제가 없어서 구글링해보니

`SELinux` 라는 보안이 막고 있었다.

selinux의 상태는 `sestatus`를 통해서 알 수 있다.

방법을 찾아보니 `chcon`이라는 처음보는 명령어로 설정을 해주면 되는데

해당 파일에 대한 권한은 `ls -Z` 를 통해서 확인가능하다.

svn에 대한 권한은 결국

```
chcon -R -t svnserve_content_t /home/svn/svn_repos
```
를 통해서 설정가능하다.

chcon으로 확인해보면 default 어쩌고 였던 권한이 svnserve_content_t 로 변경되었다.

이제 다시 서비스를 재시작하니 모든 것이 정상적으로 동작하였다.