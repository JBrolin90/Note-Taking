---
Note-Type: Permanent
tags:
  - Permanent
Date: "2026-01-26"
---
[[SQL-Server]]

Install
```bash
sudo apt install freetds-dev freetds-bin tdsodbc unixodbc unixodbc-dev
```
If not using odbc, there is no need to install tdsodbc unixodbc unixodbc-dev

I cloned from git.
Need to install autoconf, automake and libtool
sudo apt install autoconf automake libtool gperf

Then
cd ~/your_project

git clone https://github.com/FreeTDS/freetds.git

cd freetds

./autogen.sh # if needed (generates configure script)

./configure --prefix=$PWD/../freetds-local --enable-static

make

make install