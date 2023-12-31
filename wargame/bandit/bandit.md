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

## level 15 -> level 16
```shell
openssl s_client -connect localhost:30001
[password] (enter)
```
## level 16 -> level 17
```shell
nc -nv -w 1 -z 127.0.0.1 31000-32000 # refused된 port도 출력
nc -nv -w 1 -z 127.0.0.1 31000-32000 2>&1 | grep succeeded
openssl s_client -connect localhost:3xxxx
"
"
[password] (enter)
# copy output
mkdir /tmp/hacksin
cd /tmp/hacksin
vi sshkey # paste output
chmod 600 sshkey
ssh -i sshkey bandit17@localhost
ls /etc/bandit_pass
cat /etc/bandit_pass/bandit17
```
## level 17 -> level 18
```shell
ls -a
diff passwords.new passwords.old
```
## level 18 -> level 19
```shell
ssh -h
ssh bandit18@bandit.labs.overthewire.org -p 2220 /bin/sh
pwd
ls -a
cat readme
```

## level 19 -> level 20
```shell
ls -a
./bandit20-do id
./bandit20-do cat /etc/bandit_pass/bandit20
```

## level 20 -> level 21
```shell
# shell 1
nc -lnvp 7777
[bandit20 password] (enter)
# shell 2
./suconnect 7777
(print bandit21 password)
```

## level 21 -> level 22
```shell
cd /etc/cron.d
ls
cat cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
cat /tmp/xxxxxxxxxxxxxxxxxxxxxx
```

## level 22 -> level 23
```shell
ls
cat cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
# new shell script
# myname = 'bandit23'
# mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
# echo $mytarget
```
```shell
ls
cat cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```

## level 23 -> level 24
```shell
cd /etc/cron.d
ls
cat cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh

echo "cat /etc/bandit_pass/bandit24 > /tmp/normal_test" > normal.sh
cat normal.sh
chmod 777 normal.sh
# ...wait
cat /tmp/normal_test
```

## level 24 -> level 25
```shell
nc localhost 30002
[password] [xxxx] (enter)
exit
cd /tmp
mkdir hacksin
cd hacksin
vi test.sh
# #!/bin/bash
# 
# for i in {0000..9999}
# do
#   echo "goiergiowrhr02ur034ur $i"
# done

./test.sh | nc localhost 30002 | grep -v "Wrong"
```

## level 25 -> level 26
```shell
ls -l
ssh -i bandit26.sshkey bandit26@localhost (-p 2220)
cat /etc/passwd | grep bandit26
cat /usr/bin/showtext
# more이 실행중인 상태에서 vi를 실행시킬 수 있다. vi에서 명령어를 실행할 수 있다.
# 화면을 줄어 more를 실행 -> vi 실행 -> 명령어 사용
# more -> v -> :set shell=/bin/bash -> :sh
# Login!!
# bandit26으로 들어갈 때 위의 방식으로 들어가야 함
```

## level 26 -> level 27
```shell
ls -al
./bandit27-do
./bandit27-do /bin/sh
cat /etc/bandit_pass/bandit27
```
```shell
./bandit27-do cat /etc/bandit_pass/bandit27
```

## level 27 -> level 28
```shell
cd /tmp
mkdir hacksin
cd hacksin
git clone ssh://bandit27....
ls
cd repo
cat README
```

## level 28 -> level 29
```shell
mkdir /tmp/hacksin
cd /tmp/hacksin
git clone ssh://bandit28....
cd repo
cat README.md
git log
git checkout fi02jg3.... # 이전 커밋으로 돌아감
cat README.md
```

## level 29 -> level 30
```shell
mkdir /tmp/hacksin
cd /tmp/hacksin
git clone ssh://bandit29....
ls
cd repo
cat README.md
git branch -a
git checkout remote/origin/dev
ls
cat README.md
```

## level 30 -> level 31
```shell
mkdir /tmp/hacksin
cd /tmp/hacksin
git clone ssh://bandit29....
ls
cd repo
cat README.md
# git log, git branch 모두 확인, but nothing...
git tag
git show secret
```

## level 31 -> level 32
```shell
mkdir /tmp/hacksin
cd /tmp/hacksin
git clone ssh://bandit29....
ls
cd repo
cat README.md
vi .gitignore
# remove *.txt
vi key.txt
# May I come in?
git add .
git commit -m "commit"
git push origin master
```

## level 32 -> level 33
```shell
$0
cat /etc/bandit_pass/bandit33
```