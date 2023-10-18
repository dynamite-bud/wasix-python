The is a build of CPython for WASIX

This is done using a github mirror repo here: https://github.com/wasix-org/cpython/tree/wasix-compatibility

Build command, to be adapted, was:

```shell
RANLIB=llvm-ranlib-15 AR=llvm-ar-15 NM=llvm-nm-15 CC="clang-15 --target=wasm32-wasi --sysroot=/home/seb/wasix-libc/sysroot32" CXX="clang-15 --target=wasm32-wasi --sysroot=/home/seb/wasix-libc/sysroot32" CFLAGS="-I/home/seb/wasix-libs/include -I/home/seb/wasix-libs/include/ncurses -I/home/seb/git/sqlite/build/ -I/home/seb/git/liblzma/src/liblzma/api -I/home/seb/git/openssl/include -I/home/seb/git/zlib -matomics -mbulk-memory -mmutable-globals -pthread -mthread-model posix -ftls-model=local-exec -fno-trapping-math -DOPENSSL_THREADS -O2 -g -flto" LIBS="-L/home/seb/wasix-libs/lib -L/home/seb/git/sqlite/build/.libs -L/home/seb/git/liblzma/src/liblzma/.libs/ -L/home/seb/git/openssl/ -L/home/seb/git/zlib -Wl,--shared-memory -Wl,--max-memory=4294967296 -Wl,--import-memory -Wl,--export-dynamic -Wl,--export=__heap_base -Wl,--export=__stack_pointer -Wl,--export=__data_end -Wl,--export=__wasm_init_tls -Wl,--export=__wasm_signal -Wl,--export=__tls_size -Wl,--export=__tls_align -Wl,--export=__tls_base -lwasi-emulated-mman -O2 -flto -g" ../configure --disable-shared --host=wasm32-unknown-wasix --target=wasm32-unknown-wasix --prefix=/cpython --program-suffix=".wasm" --disable-test-modules --build=x86_64-linux-gnu --with-build-python=$(pwd)/../build64/python ax_cv_c_float_words_bigendian=no ac_cv_file__dev_ptmx=no ac_cv_file__dev_ptc=no --with-readline --with-pkg-config=no --with-openssl=/home/seb/git/openssl --enable-wasm-pthreads --enable-ipv6
```

Using pre-built openssl, lzma, libz and sqlite3. Also using latest `wasix-libc` build


Once built, this gives the following enabled modules:

```
The following modules are *disabled* in configure script:
_testbuffer           _testcapi             _testclinic
_testimportmultiple   _testinternalcapi     _testmultiphase
_xxtestfuzz           xxsubtype

The necessary bits to build these optional modules were not found:
_bz2                  _ctypes               _curses_panel
_uuid                 xxlimited             xxlimited_35
To find the necessary bits, look in configure.ac and config.log.

Checked 110 modules (79 built-in, 0 shared, 17 n/a on wasix-wasm32, 8 disabled, 6 missing, 0 failed on import)
```


History log
===========

* Build 09

- Updated sources to 3.12.0 release

* Build 08

- Stripped wasm binary for a 20MB of space saved

* Build 07

- Fixed issues with subprocess not launching

* Build 06

-  Fixed some issue with sqlite

* Build 05

- Updated build, linked with latest wasix-libc

* Build 04

- Added in more modules
- Using a new wasix-libc

* Build 03

- Fixed issues with httpd.server

* Build 02

- repackage to change version number

* Build 01

- New wasix build, fixing asyncio assues

