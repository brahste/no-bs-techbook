# Making `deb` packages

links: 
- https://www.internalpointers.com/post/build-binary-deb-package-practical-guide

Tips:
- The **control file** is the most important file in a `deb` package; it stores the information about the package and the program it installs.

- A `deb` package has a directory structure that shadows the file system.
- When the package is installed, a file in a directory will be copied to the same location on the host computer (eg. `/usr/bin` `/opt`)


Commands:

`cpack`: creates a deb file ?given the contents of the CMake?

`dpkg-deb -c <name_of_deb_file>.deb`: This will show the structure contained within the *deb* package


The below code is one way to create a deb file from within CMake
```
include(InstallRequiredSystemLibraries)
set(CPACK_GENERATOR "DEB")
set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Description")
set(CPACK_PACKAGE_VENDOR "Your Vendor Name")
set(CPACK_PACKAGE_HOMEPAGE_URL "Homepage URL")
set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Your Name")
set(CPACK_PACKAGE_CONTACT "your@email.com")
set(CPACK_RESOURCE_FILE_LICENSE "${CMAKE_CURRENT_SOURCE_DIR}/LICENSE")
set(CPACK_PACKAGE_INSTALL_DIRECTORY "CMake ${CMake_VERSION_MAJOR}.${CMake_VERSION_MINOR}")
if( DEVELOP )
  set(CPACK_PACKAGE_NAME ${CMAKE_PROJECT_NAME}-dev)
else()
  set(CPACK_PACKAGE_NAME ${CMAKE_PROJECT_NAME})
endif()
set(CPACK_PACKAGE_VERSION_MAJOR ${PROJECT_VERSION_MAJOR})
set(CPACK_PACKAGE_VERSION_MINOR ${PROJECT_VERSION_MINOR})
set(CPACK_PACKAGE_VERSION_PATCH ${PROJECT_VERSION_PATCH})
if( DEVELOP )
  set(CPACK_DEBIAN_PACKAGE_DEPENDS "libtest-dev, libattempt-dev")
else()
  set(CPACK_DEBIAN_PACKAGE_DEPENDS "libtest, libattempt")
endif()

execute_process(
  COMMAND dpkg --print-architecture
  RESULT_VARIABLE RESULT_VAR
  OUTPUT_VARIABLE SYS_ARCH
  OUTPUT_STRIP_TRAILING_WHITESPACE
)
set(CPACK_PACKAGE_FILE_NAME ${CPACK_PACKAGE_NAME}-${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_      VERSION_PATCH}-${SYS_ARCH})
include(CPack)

set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES ENABLE_EXPORTS 1)
```
