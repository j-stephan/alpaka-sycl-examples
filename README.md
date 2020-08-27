# Prerequisites

1. A working SYCL environment. This minimal example was tested with ComputeCpp
   1.2.0 as well as the Intel SYCL compiler. Both were used with the Intel
   Graphics Compute Runtime for OpenCL.
2. Alpaka with the experimental SYCL backend. Fetch it here:
   https://github.com/j-stephan/alpaka and switch to the `sycl` branch.
3. Codeplay's ComputeCpp SDK. Fetch it here:
   https://github.com/codeplaysoftware/computecpp-sdk

# Compilation

Currently there is no support in Alpaka's CMake build system for SYCL.
Compilation with ComputeCpp:

```
compute++ -std=c++17 -O3 \
    -sycl-driver -sycl-target spirv64 \
    -I/path/to/alpaka/include \
    -I/path/to/computecpp/include \
    -I/path/to/computecpp-sdk/include \
    -DALPAKA_ACC_SYCL_ENABLED \
    -DALPAKA_ACC_CPU_B_SEQ_T_SEQ_ENABLED \
    -DBOOST_LANG_SYCL=1 main.cpp \
    -no-serial-memop \
    -o vectorAdd 
    -L/path/to/computecpp/lib \
    -lComputeCpp \
    -lOpenCL
```

Compilation with Intel:

```
clang++ -std=c++17 -O3 \
    -fsycl \
    -I/path/to/alpaka/include \
    -I/path/to/computecpp-sdk/include \
    -DALPAKA_ACC_SYCL_ENABLED \
    -DALPAKA_ACC_CPU_B_SEQ_T_SEQ_ENABLED \
    -DBOOST_LANG_SYCL=1 \
    main.cpp \
    -o vectorAdd -lOpenCL
```

# Execution

```
./vectorAdd
```

This should produce the following output:

```
Execution results correct!
```
