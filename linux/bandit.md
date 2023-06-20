# Intro
### 준비 사항
1. Linux (ex: Kali Linux)
2. Linux Basic

### Rule
1. bandit 시스템에 접속: ssh
2. bandit0 -> bandit1 -> .... 비밀번호 찾아 다음 단계로 이동

### ssh 접속 방법
```
ssh [계정]@[시스템주소(도메인)] -p [포트번호]
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
# Problem
## level 0
```shell
ssh bandit0@bandit.labs.overthewire.org -p 2220
```
## level 0 -> level 1
```shell
cat readme
```
## level 1 -> level 2
```shell
cat ./-
```
## level 2 -> level 3
```shell
cat spaces\ in\ this\ filename
```
## level 3 -> level 4
```shell
cd inhere
ls -a
cat .hidden
```
## level 4 -> level 5
```shell
cd inhere
ls
file ./-file00
file ./-file01
file ./-file02
file ./-file03
file ./-file04
file ./-file05
file ./-file06
file ./-file07
cat ./-file07
```
