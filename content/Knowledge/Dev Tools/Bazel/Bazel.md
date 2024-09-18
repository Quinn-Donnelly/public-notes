---
tags:
  - devtool
---
# Summary
At built tool with support to orchestrate hermetic monorepos

# Versioning the tool
[Bazelisk](https://github.com/bazelbuild/bazelisk) used for managing and auto detecting bazel version

# Golang auto migration
[Gazelle](https://github.com/bazelbuild/bazel-gazelle) can be used to auto generate the BUILD files for Bazel for [Golang] projects
*Note you will need to specify the prefix so that it knows what is project local - see screenshot below*
![[Pasted image 20240104221819.png]]
Command to have Gazelle update the dependencies from go.mod 
![[Pasted image 20240104222025.png]]
