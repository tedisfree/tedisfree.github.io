---
title: "Git Submodule 관련 커맨드"
date: 2021-08-12 19:10:28 -0400
categories: git
---

# Submodule 생성

서브모듈을 사용하고자 하는 프로젝트에서 아래와 같은 커맨드를 통해 서브모듈을 추가한다.

```git
git submodule add https://ted.com/subproject
```

# Submodule Clone

서브 모듈이 포함된 프로젝트를 clone하면, 서브모듈은 비어 있는 것을 볼 수 있다.
아래와 같은 커맨드를 통해 서브모듈을 초기화하고 clone하자.

```git
git submodule init
git submodule update
```

더 편한 방법은 프로젝트 clone 시, `--recurse-submodules` 옵션을 추가하는 방법이 있다.
```git
git clone --recurse-submodules https://ted.com/project
```


