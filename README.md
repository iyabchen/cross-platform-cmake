A very simple example to show how to use cmake to build libraries on Windows. The same code base should also apply on Linux.

## Prerequisite

Windows - a compiler(eg. msvc), cmake
Linux - a compiler(eg. gcc), make/ninja, cmake

## Code structure

The idea is `sum` is a library for summing two numbers together, `addten` uses sum library to add 10 to a number, and `main` invokes `addten` library.

The total number of the programs are less than 20 lines.

## How to run

First, build the libraries under `app` folder.

```
$ mkdir build
$ cd build
$ cmake ..
...
$ cmake --build .
Microsoft (R) Build Engine version 16.2.37902+b5aaefc9f for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

  Building Custom Rule D:/cross-platform-cmake/app/CMakeLists.txt
  sum.cpp
  Auto build dll exports
     Creating library D:/cross-platform-cmake/app/build/Debug/sum.lib and object D:/cross-platform-cmake/app/build/Debug/sum.exp
  sum.vcxproj -> D:\cross-platform-cmake\app\build\Debug\sum.dll
  Building Custom Rule D:/cross-platform-cmake/app/CMakeLists.txt
  addten.cpp
  Auto build dll exports
     Creating library D:/cross-platform-cmake/app/build/Debug/addten.lib and object D:/cross-platform-cmake/app/build/Debug/addten.exp
  addten.vcxproj -> D:\cross-platform-cmake\app\build\Debug\addten.dll

```

We can see lib and dll files are built under `app/build/Debug`.

Second, build the main program. Do the similar under `main` folder.

```
$ mkdir build
$ cd build
$ cmake ..
...
$ cmake --build .
Microsoft (R) Build Engine version 16.2.37902+b5aaefc9f for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

  Checking Build System
  Building Custom Rule D:/cross-platform-cmake/main/CMakeLists.txt
  main.cpp
  main.vcxproj -> D:\cross-platform-cmake\main\build\Debug\main.exe
  Building Custom Rule D:/cross-platform-cmake/main/CMakeLists.txt
```

Copy `sum.dll` and `addten.dll` over to `main/build/Debug`. Then run `main.exe` should work.

```
$ ls
addten.dll*  main.exe*  main.ilk  main.pdb  sum.dll*
$ ./main.exe
20
```

To build static library, simply change `SHARED` to `STATIC` in the cmake file. Then only `.lib` files are generated. At `main` build, both libraries are still required to be linked, but no files need to be copied over to run `main.exe`.

There is no way to specify both `SHARED` and `STATIC` together on the same statement, so they have to be specified as libraries with different names.
