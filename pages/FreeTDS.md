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

`make install` copies the compiled binaries, libraries, and headers from the build directory to the installation directory specified by `--prefix`.

**What it does:**

- Copies compiled libraries (`.so`, `.a` files) to `prefix/lib/`
- Copies header files (`.h`) to `prefix/include/`
- Copies executables/tools to `prefix/bin/`
- Copies documentation to `prefix/share/`
- Sets proper permissions

**In your case with `--prefix=$PWD/../freetds-local`:**
```
freetds-local/
├── bin/          # FreeTDS utilities (tsql, etc.)
├── include/      # Headers you need for compiling
├── lib/          # Libraries you need for linking
└── share/        # Documentation, man pages
```

For loading library at runtime
```make
FREETDS_DIR = ./freetds-local
CXXFLAGS = -g -Wall -I$(FREETDS_DIR)/include `pkg-config --cflags gtkmm-4.0`
CXXLIBS = -L$(FREETDS_DIR)/lib -lsybdb -Wl,-rpath,$(FREETDS_DIR)/lib `pkg-config --libs gtkmm-4.0`
```

For static linking.
```make
CXXLIBS = $(FREETDS_DIR)/lib/libsybdb.a `pkg-config --libs gtkmm-4.0`
```