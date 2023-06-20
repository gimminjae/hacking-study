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
