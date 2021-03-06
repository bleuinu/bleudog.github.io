---
title: git commit 서명하기
date: 2022-04-05 22:20:15
tags: [git, gpg]
categories: [Git]
lang: ko
---

## Signing commits
GPG key를 사용하여 커밋에 서명하는 것이 가능하다 -- 오래된 커밋에 서명하는 방법은 [여기](https://medium.com/@midotype/signing-previous-commits-787a077bdb62).

![Signed commits](/images/posts/05042022-sign-commit-1.png)

우선 사용 할 GPG key ID를 정해야한다. `gpg --list-secret-keys --keyid-format=long` 명령어를 사용하여 등록되어 있는 GPG key들을 확인 할 수 있다.

```sh
$ gpg --list-secret-keys --keyid-format=long

------------------------------------
sec   4096R/SAMPLE4371567BD2 2016-03-10 [expires: 2023-04-05]
uid                          Mido Eu <mido.eu@proton.me> 
ssb   4096R/42B317FD4BA89E7A 2016-03-10 [expires: 2023-04-05]
------------------------------------
```

여기는 하나의 GPG key만이 존재하기 때문에 해당 키를 사용한다. 
4번째 줄의 `SAMPLE4371567BD2`가 GPG key ID이므로 이 값을 복사한다.

해당 key로 커밋을 한다는 것을 git에 알려주어야 한다.

```sh
# 개별 git 리포지토리
$ git config user.signingkey SAMPLE4371567BD2

# 모든 git 리포지토리
$ git config --global user.signingkey SAMPLE4371567BD2
```

하나의 리포지토리에만 적용하고 싶은 경우는 2번째 줄의 명령어를, 모든 리포지토리에 적용하고 싶다면 `--global` 사용한 4번째 줄의 명령어를 사용한다.

그리고 커밋을 할때 `-S` 플래그를 사용해주면 된다.

```sh
$ git commit -S
```

매번 `-S` 플래그를 같이 쓰는게 귀찮다면 `commit.gpgsign`값을 `true`로 설정해두면 된다.

```sh
## 개별 git 리포지토리
git config commit.gpgsign true

## 모든 git 리포지토리
git config --global commit.gpgsign true
```

또는 `.gitconfig`에 alias를 설정해서 사용해도 된다.

## .gitconfig

내가 쓰는 git 명령어 alias.

<script src="https://gist.github.com/midotype/7d09f53e421a1fc04987363110c522cf.js"></script>