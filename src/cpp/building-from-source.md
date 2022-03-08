# Building from Source

If you're using a `cmake` project then you can build the project from source starting with the `CMakeLists.txt`. First, create you target build folder

```
mkdir build
cd build
```

Once in the `build` folder, compile the `Makefile` from the top-level `CMakeLists.txt`. This should be one level up from your current build folder.

```
cmake ..
```

This will create a `Makefile` that can be used to actually compile the program.

```
make
```

Now the program executable will be available, likely in the `build` folder, or in a seperate folder sometimes labelled `bin` (it depends on the way the `CMakeLists` is set up).

Finally you can create a DEB package using the `cpack` command

```
cpack
```

Finally, you can install the DEB package into your root file system with `dpkg`

```
sudo dpkg -i <name-of-your-deb-package>.deb
```
