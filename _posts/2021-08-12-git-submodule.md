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

# Submodule에 Push

메인 프로젝트에서 서브모듈의 내용을 수정한 경우, 이를 서브모듈 repository에 push하고 싶을 때는 다음과 같이 진행하면 된다.
서브모듈은 메인 프로젝트와 별개로 독립된 repository로 처리되므로, 서브모듈이 있는 위치에서 일반적인 push 작업을 진행하면 된다.

```git
cd submodule
git add . 
git commit -m "submodule changes"
git push 
```

이제 메인 repository에도 submodule의 변경 사항을 커밋해 줘야한다.

```git
cd main_proj_git_root
git add submodule
git commit -m "updated some..."
git push
```





