# Using PkgConfig with CMake

> Links:
> 
> - https://stackoverflow.com/questions/29191855/what-is-the-proper-way-to-use-pkg-config-from-cmake (see item 2, accepted answer)
> - https://people.freedesktop.org/~dbn/pkg-config-guide.html

One of the difficulties with using C/C++ is related to the integration of various libraries and dependencies needed for an application. *pkg-config* is a metadata system that helps ease this process by providing information about how to integrate libraries into an program. While there are a number of ways to use *pkg-config* and *cmake* here I outline a few specific methods that have worked well for me in the past.

## Creating a Library that has PkgConfig

Say your project is called *foo*, such that your top-level *CMakeLists.txt* contains the block

```cmake
project(foo
    VERSION 0.1.6
    DESCRIPTION "Foo C++ library"
)
```

In your project, create a *pc.in* file with the following contents.

```
prefix=@CMAKE_INSTALL_PREFIX@
exec_prefix="${prefix}"
libdir="${prefix}"/lib
includedir="${prefix}"/include

Name: libfoo
Version: @CMAKE_PROJECT_VERSION@
Description: @CMAKE_PROJECT_DESCRIPTION@
Libs: -L${libdir} -lfoo
Libs.private: -ldep1 -ldep2
Cflags: -I${includedir}/libfoo
```

The variables nested between `@` symbols will be replaced once the project is built. The `Libs.private` field should be used to identify any dependencies of the library itself.

Next, in the top-level *CMakeLists.txt* file add the lines

```cmake
configure_file(pc.in lib${CMAKE_PROJECT_NAME}.pc @ONLY)
install(
    FILES ${PROJECT_BINARY_DIR}/lib${CMAKE_PROJECT_NAME}.pc
    DESTINATION "local/lib/pkgconfig"
)
```

When the project is built this will create a file called *libfoo.pc*. If you use *cpack* to package your program into a *deb*, upon install this will place the file at */usr/local/lib/pkgconfig/libfoo.pc*.

## Using a Library in a Program

Say you're writing a program that uses [ZeroMQ](https://zeromq.org/). Depending on your system, the ZeroMQ *pkg-config* file may be located at */usr/lib/x86_64-linux-gnu/pkgconfig/libzmq.pc*.

This file contains the following information.

```
prefix=/usr
exec_prefix=${prefix}
libdir=${prefix}/lib/x86_64-linux-gnu
includedir=${prefix}/include

Name: libzmq
Description: 0MQ c++ library
Version: 4.3.2
Libs: -L${libdir} -lzmq
Libs.private: -lstdc++  -lpthread -lrt
Requires.private:  krb5-gssapi libsodium openpgm-5.2 >= 5.2 norm
Cflags: -I${includedir}
```

To use ZeroMQ with *pkg-config, in your top-level *CMakeLists.txt* add the following block.

```cmake
find_package(PkgConfig REQUIRED)

pkg_search_module(LIBZMQ REQUIRED IMPORTED_TARGET libzmq)
```

Then, add the include directory and link library to your executable target. 

```cmake
target_include_directories(${CMAKE_PROJECT_NAME} 
  PRIVATE 
    ${LIBZMQ_INCLUDE_DIRS}
)

target_link_libraries(${CMAKE_PROJECT_NAME} 
  PUBLIC 
    PkgConfig::LIBZMQ
)
```
