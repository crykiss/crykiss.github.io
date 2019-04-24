---
layout: post
author: danny Kim
title: "vim에서 YouCompleteMe가 동작하지 않을때"
category: "linux"
tags: go vim vi python3 python plugin
---

vim에서 개발환경을 만들기 위해서
여러 플러그인 설치를 진행하였다.

모두 정상적으로 동작하였는데

유독 YouCompleteMe는 설치가 끝났음에도 동작을 하지 않아서
설치를 몇번이다 다시 했는지 모른다.

결국 `vim --version` 으로 확인 시 python3 가 - 표시가 되어 지원을 하지 않기 때문이었다.

MacOS 였기 때문에 homebrew 로 vim 을 다시 설치해주려고 했는데
우선 uninstall 과정에서부터 오류가 발생했다.

이유는 brew 로 vim을 설치 한 적이 없기 때문이다.

요즘에는 brew로 vim을 설치하면 python3 가 기본으로 적용
단순히 설치를 진행했다.

`brew install vim`

문제는 그 후에도 `vim --version` 에서 python3 가 - 표기가 된다는 점이었다.

원인은 단순한 문제였다.

/usr/local/bin 아래 기존의 vim 자리 잡고 있기 때문에
새로 설치한 vim이 실행되지 않기 때문이었다.

결국 .zshrc (사용하는 초기화 스크립트) 에 path 환경을 변경하고 나서
YouCompleteMe 재설치 과정을 거치니

*정상적으로 자동완성이 동작하였다.*

```
export PATH=/usr/local/Cellar/vim/8.1.1200/bin:$PATH
```