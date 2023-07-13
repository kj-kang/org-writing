---
title: Window 에서 암호 없이 Git 인증을 위한 ssh-agent 설정하기
description: 윈도우
author: Kukjin Kang
date: 2023-07-12
tags: ['windows', 'ssh']
options: toc:nil
---

SSH-Agent와 OpenSSH는 GitHub, GitLab등과 같은 원격 Git 저장소 인증에 사용하는
도구이다. SSH 키를 등록하면, 매번 암호를 입력하지 않고도 쉽게 인증할 수 있으며,
Push, Pull 등을 수행할 때마다 암호를 입력해야 하는 번거로움을 없앤다.


# Window에서 SSH-Agent 서비스를 실행하기

관리자 권한의 PowerShell 창을 실행합니다. 다음 명령을 실행하여 SSH-Agent
서비스를 설치하고, 컴퓨터에 로그인 할 때 자동으로 시작하도록 구성한다.

```sh
$ Get-Service ssh-agent | Set-Service -StartupType Automatic -PassThru | Start-Service
```


# SSH KEY 쌍을 생성하기

Bash 또는 PowerShell과 같은 명령 도구를 사용하여, 다음과 같은 명령을
실행한다. 이번 예시에서는 ED25519 키를 생성하지만, RSA와 같은 다른 키를 생성할
수도 있다.

```sh
$ ssh-keygen -t ed25519 -C 'your_email@example.com'
```

생성하는 키의 위치는 기본적으로 로컬 사용자의 SSH 저장소 (~/.ssh)를
사용한다. 필요한 경우 다른 위치나 파일명을 변경할 수 있다.

암호를 추가 하거나 비워 둘 수 있다.


# ssh-agent에 ssh 키 추가하기

```sh
$ ssh-add ~/.ssh/id_ede5519_git_demo
```

...


# ssh-agent를 사용하도록 Git 구성하기

```sh
$ git config --global core.sshCommand C:/Windows/System32/OpenSSH/ssh.exe
```