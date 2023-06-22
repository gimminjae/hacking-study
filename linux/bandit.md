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
other way
```shell
cd inhere
ls
file * or file ./*
cat ./-file07
```

## level 5 -> level 6
```shell
cd inhere
ls
find * -type f -size 1033c
cat maybehere07/.file2
```
other way
```shell
find ./ -type f -size 1033c ! -executable
```

## level 6 -> level 7
```shell
ls -a
cd /
find * -user bandit7 -group bandit6 -size -34c 2>/dev/null
cat var/lib/dpkg/info/bandit7.password
```
other way
```shell
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
## level 7 -> level 8
```shell
ls
cat data.txt | grep millionth
```
other way
```shell
ls
vi data.txt
    [esc]
    /millionth
```
```shell
grep millionth ./data.txt
```
## level 8 -> level 9
```shell
ls
cat data.txt
sort data.txt | uniq -c # 정렬 후 중복횟수 세기
```
other way
```shell
sort data.txt | uniq -u # 중복되는 요소를 없앰
```

## level 9 -> level 10
```shell
ls
file data.txt
cat data.txt | grep -a "======="
# grep은 binary 파일을 읽을 수 x
# -a 옵션을 붙이면 binary 파일을 txt 파일처럼 처리할 수 있다.
```
other way
```shell
strings data.txt | grep ====
# strings {file} 파일에서 문자열만 추출한다.
```
## level 10 -> level 11
```shell
ls -a
base64 --decode data.txt
```
## level 11 -> level 12
```shell
cat data.txt | tr '[a-z]' '[n-za-m]' | tr '[A-Z]' '[N-ZA-M]'
```
other way
```shell
# ROT13 알고리즘 사용
```
```shell
cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
```
## level 12 -> level 13
```shell
mkdir /tmp/hacksin
cp data.txt /tmp/hacksin/data.txt
cd /tmp/hacksin
xxd -r data.txt > data2
file data2
mv data2 data2.gz
gunzip data2.gz
file data2
mv data2 data2.bz2
bzip2 -d data2.bz2
file data2
mv data2 data2.gz
gunzip data2.gz
file data2
mv data2 data2.tar
tar -xf data2.tar
file data5.bin
mv data5.bin data5.tar
tar -xf data5.tar
file data6.bin
mv data6.bin data6.bz2
bzip2 -d data6.bz2
file data6
mv data6 data6.tar
tar -xf data6.tar
file data8.bin
mv data8.bin data7.gz
gunzip data8.gz
file data8
cat data8
```
## level 13 -> level 14
```shell
ls -a
cat sshkey.private
ssh -i sshkey.private bandit14@localhost -p 2220
cat /etc/bandit_pass/bandit14
```
## level 14 -> level 15
```shell
nc localhost 30000
[password] (enter)
```