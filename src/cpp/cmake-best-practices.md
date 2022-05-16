# CMake Best Practices
## Best Practices
In the top level *CMakeLists.txt*, it is a good practice to use `include(...)` statements. These statements directly embed the included file in the location where the `include` statement is made, allowing for better modularity and readability of the *CMakeLists.txt* file. For clarity, a *cmake* folder is typically used to house important included CMake files. Important files that should be included are
- *cmake/Testing.cmake* - Has build directives for the testing library.
- *cmake/CodeCoverage.cmake* - Has build directives for making code coverage reports during testing (often included in *Testing.cmake*).
- *cmake/Cpack.cmake* - Has build directives for packing the library into a DEB archive.


## Cheatsheet
### Using Command Line Arguments in CMakeLists.txt

When compiling the `Makefile` using `cmake ..`, pass arguments prepended with `-D<argument>`. These arguments can then be accessed in `CMakeLists.txt` using `${<argument>}`.

For example, if your `CMakeLists.txt` contains the following code.
```cmake
message("CUSTOM_VARIABLE=${CUSTOM_VARIABLE}")
if( CUSTOM_VARIABLE ) 
    message("CUSTOM_VARIABLE evaluated to True")
endif()
```

Then at the command line use
```
$ cmake .. -DCUSTOM_VARIABLE=True
CUSTOM_VARIABLE evaluates to True
-- Configuring done
-- Generating done
-- Build files have been written to: <build_path>
```

---

## Misc Commands

@ONLY restricts variable replacement to references of the form @VAR@. This is useful for configuring scripts that use ${VAR} syntax

**configure_file**: Copy a file to another location and modify it's contents.
- This can be done with a *config.h.in* files, for example, to auto populate a configuration header given project name, version, etc in the *CMakeLists.txt*.

**install**: Defines the installation rules for a project


