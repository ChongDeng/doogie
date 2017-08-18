
# Doogie

A power browser

## Building

### Windows Prerequisites

Before running the build script on Windows, you must have the prerequisites:

* Latest Qt (5.x) installed w/ `qmake.exe` on the `PATH`
* Latest CMake installed w/ `cmake.exe` on the `PATH`
* Latest Python (2.x) installed w/ `python.exe` on the `PATH`
* Latest Go installed w/ `go.exe` on the `PATH`
* [MSVC 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools) installed w/ the following
  executed to put 64-bit VC compiler on the `PATH`:
  `"C:\Program Files (x86)\Microsoft Visual Studio 14.0\VC\vcvarsall.bat" amd64`
* Latest [Windows 64-bit standard dist of CEF](http://opensource.spotify.com/cefbuilds/index.html#windows64_builds)
  extracted w/ `CEF_DIR` environment variable set to the base CEF extracted dir
* This repo cloned w/ the shell at the `src` folder

### Linux Prerequisites

(NOTE: Linux support is not yet complete)

Before running the build script on Windows, you must have the prerequisites:

* Latest Qt (5.x) installed w/ `qmake` on the `PATH`
* Latest CMake installed w/ `cmake` on the `PATH`
* Latest Python (2.x) installed w/ `python` on the `PATH`
* Latest Go installed w/ `go` on the `PATH`
* Latest GCC installed w/ `gcc` and `g++` on the `PATH`
* Latest Make installed w/ `make` on the `PATH`
* Latest [Linux 64-bit standard dist of CEF](http://opensource.spotify.com/cefbuilds/index.html#linux64_builds)
  extracted w/ `CEF_DIR` environment variable set to the base CEF extracted dir
* Latest GTK 2.x installed and on the library path
* This repo cloned w/ the shell at the `src` folder

### MacOS Prerequisites

(TODO)

### Running Build

The application uses the CEF C++ wrapper, which can be built via:

    go run build.go build-cef

Now the application can easily be run via:

    go run build.go run

That will run the `debug` version. For the `release` version, run:

    go run build.go run release

Internally, that just builds and runs the exe. To just build, call `build` instead. To package a deployment artifact
from a previously run build, `package` is used. For example, to package a `release` deployment artifact from a
previously run `release` build, run:

    go run build.go package release

Once complete, the package(s) will in `release/package` (e.g. doogie.zip in Windows)

### Testing

There are two types of tests, unit and integration tests at `tests/unit` and `tests/integration` respectively.

#### Integration Tests

The integration tests are not yet integrated in `build.go`. The tests are written in node.js. Make sure you have the
latest LTS release of node installed and navigate to `src/tests/integration`. To setup the test infrastructure, run:

    npm install

To run the tests, make sure a debug instance of Doogie is running then run

    npm test

#### Unit Tests

Assuming CEF is built (see the first "Running Build" step), unit tests can be run with:

    go run build.go unit-test

Like the `run` command, the `unit-test` command can be given a `release` target, otherwise it defaults to `debug`.

### Development

To do a lint check of the code, have the
[Chromium depot_tools](https://chromium.googlesource.com/chromium/tools/depot_tools.git) cloned somewhere and set the
`DEPOT_TOOLS_DIR` env var to the dir. Then run:

    go run build.go lint
