---
layout: post
author: danny Kim
title: "VFS: Unable to mount root fs on unknown-block (0,0)"
category: "system"
tags: virtualbox system tools disk error centos7 centos
---

**ISSUE**
virtualbox 디스크 용량 올린 후 centos 에서 구동 문제 발생
```
VFS: Unable to mount root fs on unknown-block (0,0)
```

**Solution**

```
VBoxManage clonehd <infilename or UUID> <outfilename> --format VDI --variant Standard
```
