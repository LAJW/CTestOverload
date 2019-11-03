# Visual Studio 2019 CMake add_test timeout demo

## Steps to reproduce

In Visual Studio:
File -> Open -> CMake -> CMakeLists.txt

CMake cache generation (through Visual Studio) times out on i7 8750 HQ.
It doesn't time out (and is pretty fast) when running:

```
cmake "-H" -Bbuild
```

If you have a faster processor, try increasing the number of generated tests
in CMakeLists.txt
