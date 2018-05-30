# IMBench: Intermittent Benchmark Suite

IMBench is a a set of applications for intermittently-powered devices.

Some applications are end-to-end applicatios typical of embedded domain with
sensing, computation, and communication workload. Some applications are
computational kernels.

This repo contains only references to per-application repos; this repo does not
own any code, neither for applications nor for dependencies.  This repo does
offer an association between each app and a set of dependencies, which is an
alternative association besides the association provided by each app repo.
Despite being part of this suite, each application repo is sulf-sufficient, the
app repo refers to all dependencies of the app as submodules, and the app can
be built when its repo is cloned individually, outside of this suite.
Dependencies include both libraries and systems for intermittent computing.

Applications are built using [Maker](https://github.com/CMUAbstract/maker).

Dependencies of all applications are shared across applications in this repo,
are included as submodules in `ext/`, and are built automatically by Maker.

Applications are buildable with different systems for intermittent computing.
The systems are also included as submodules, in `tools/`. Build artifacts for
each system (aka. toolchain) are created in `<app>/bld/<system>/`. For system
that require the app code to differ significantly, an app may have different
branches. In this case, each app variant (i.e. branch) is added as a separate
submodule for convenience (to avoid having to switch branches).

## Build and run

List of applications, and list of shared dependencies and the configuration
variables for dependencies are all defined in top-level [Makefile](Makefile).
The list of source files for each applications, list of dependencies for a
each application is defined in its own Makefile, which is the same makefile
that is used for the standalone build of the application.

For parallel build, either pass `-j4` to each make command define this variable
for the lifetime of the shell:

    export MAKEFLAGS="-j4"

### Tools/toolchains

Some toolchains (the particular subset referred to as "tools" in Maker
terminology) that are used to build the apps must themselves be built
first. This includes systems for intermittent computing with compiler passes.
This does not include third-party toolchains like GCC and Clang (see [Maker
documentation](https://github.com/CMUAbstract/maker) for details).

To clean and build all toolchains listed in top-level Makefile:

    make tools/all/clean
    make tools/all/all

To build a subset of tools, set the `TOOLS` variable:

    make TOOLS="mementos dino" tools/all/all

To build a particular toolchain pass its name instead of `all` :

    make tools/mementos/all

### Dependencies

To clean and build shared dependencies with all toolchains listed in top-level
Makefile:

    make bld/all/depclean
    make bld/all/dep

To build with subset of toolchains, set `TOOLCHAINS` variable:

    make TOOLCHAINS="gcc clang" bld/all/dep

To build with a specific toolchain, pass its name instead of `all`:
    make bld/gcc/dep

### Applications

To clean build all applications in the suite with all toolchains:

    make apps/all/bld/all/clean
    make apps/all/bld/all/all

To clean and build a specific application with a specific toolchain, e.g. GCC:

    make apps/app-blinker/bld/gcc/clean
    make apps/app-blinker/bld/gcc/all

The symmetric targets for building a specific app with all toolchains, and
vice-a-versa are also available.
