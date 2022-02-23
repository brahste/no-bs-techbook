# Using GDB

To debug a C/C++ application using GDB the executable has to be compiled with the `-g` flag.

Start the debugger
```bash
$ gdb main
```
Use the `-q` option to supress GDB's intro text

Set breakpoints with `b`. For, example
```bash
(gdb) b 19
```
will set a breakpoint at line 43 of the source file.

Start the program in the debugger
```bash
(gdb) run
```
Command line arguments can be provided as normal after the `run` command.

At breakpoints you can step into a function with `step` or `s`
```bash
(gdb) s
```
Alternatively you can step over a function with `next` or `n`
```bash
(gdb) n
```

You can help determine where you are in a program's execution with the `backtrace` or `bt` command
```bash
(gdb) bt
```

You can view the values in a program with the `print` or `p` command
```bash

```


