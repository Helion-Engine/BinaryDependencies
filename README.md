# Helion GLFW and OpenAL-Soft
This repository contains submodules for [OpenAL-Soft](https://github.com/kcat/openal-soft) and [GLFW](https://github.com/glfw/glfw), and some simple "glue" to build Nuget packages from them in a standard GitHub pipeline.  It is not really intended to be built on an individual developer workstation.

Please look at the workflows in `./github/workflows` to see what flags we are passing to CMAKE when we build these projects.  Note that we are performing a trivial modification to the Linux build of GLFW that adds a function that is really part of its _Windows_ ABI.  This is to work around a limitation in how OpenTK is written, which would otherwise prevent us from using it in a Native AOT build.

To update a dependency:
1.  Clone this repository including submodules (`git clone --recurse-submodules`)
2.  Navigate to the submodule directory you are interested in
3.  Use a `git checkout <hash>` command to check out a new version (please only use tagged versions for official releases of these projects!)
4.  Edit the dummy .csproj file in the `/csharp` subdirectory, changing the PackageVersion to match the new version
5.  Push your changes
6.  Manually trigger the workflow for the affected subproject(s).  If the workflow completes successfully, the artifacts produced should include a ZIP file that contains a Nuget package.