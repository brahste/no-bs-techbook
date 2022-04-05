# CMake Cheatsheet

## Using Command Line Arguments in CMakeLists.txt

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

**configure_file**: Copy a file to another location and modify it's contents

**install**: Defines the installation rules for a project
