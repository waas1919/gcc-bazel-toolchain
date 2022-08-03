# gcc-bazel-toolchain

This repo contains the gcc toolchain for Bazel builds for C++.

To use it you should have a Bazel repository with a .bazelrc file with:

```
# Use our custom-configured c++ toolchain.
build:gcc_config --crosstool_top=@gcc-bazel-toolchain//:gcc_suite

# Use --cpu as a differentiator.
build:gcc_config --cpu=k8

# Use the default Bazel C++ toolchain to build the tools used during the build.
build:gcc_config --host_crosstool_top=@bazel_tools//tools/cpp:toolchain
```

And a WORKSPACE file with:

```
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

git_repository(
    name = "gcc-bazel-toolchain",
    remote = "git@github.com:waas1919/gcc-bazel-toolchain.git",
    commit = "18e79f2c6d19004c8c289173441faab3c555c46a", 
    shallow_since = "1659532746 +0100"
)
```

See my rules_cpp repository on how to use it from a BUILD file.
