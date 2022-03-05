# Making `deb` packages

links: 
- https://www.internalpointers.com/post/build-binary-deb-package-practical-guide

Tips:
- The **control file** is the most important file in a `deb` package; it stores the information about the package and the program it installs.

- A `deb` package has a directory structure that shadows the file system.
- When the package is installed, a file in a directory will be copied to the same location on the host computer (eg. `/usr/bin` `/opt`)


