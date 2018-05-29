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
The systems are also included as submodules. Build artifacts for each system
(aka. toolchain) are created in `<app>/bld/<system>/`. For system that require
the app code to differ significantly, an app may have different branches. In
this case, each app variant (i.e. branch) is added as a separate submodule for
convenience (to avoid having to switch branches).
