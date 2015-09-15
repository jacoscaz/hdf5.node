---
layout: page
title: "Install & Setup"
category: doc
date: 2015-05-02 12:02:34
---

## Status

Currently testing with node v0.12.x and V8 3.28.73.  Prebuilt native modules for Ubuntu 14_04, Windows VS2013 and MacOSX 10.7.
Resources leaks are being found when the h5 file is closed.  When found they are being eliminated.  Error handling component is being investigated; how to best leverage V8 and node from the native side.

```
npm install --fallback-to-build
```

## Dependencies

+ [HDF5 C Library](http://www.hdfgroup.org/downloads/index.html) v5-1.8.14
        (Prior v5-1.8.x's untested yet should work)


## Compiling [if need be]

The code requires a gcc compiler supporting C++11 for linux. MacOSX & Windows build target has been added.  The binding.gyp defines the cflags with -std=c++11.
The `binding.gyp` expects the HDF5_HOME environment variable set to your install.


### In a working copy of git

```bash
export HDF5_HOME=/home/user/NodeProjects/hdf5
export NODE_PATH=/home/user/NodeProjects/hdf5.node/build/Release:$NODE_PATH
npm install  --build-from-source

```

NODE_PATH is still used for the mocha tests.

### Including as a node module

The HDF5_HOME needs to be set. NODE_PATH should not. Then an 'npm install hdf5 --fallback-to-build' will try to locate a prebuilt version or fall back to building the source
in node_modules/hdf5. There is no need for the node-gyp step.


## Environment Variables

The path to the HDF5 shared objects must be added to the runtime library search path. 

for linux

```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:./hdf5.node/../hdf5/lib
```

for Mac OSX

```bash
export DYLD_LIBRARY_PATH=$DYLD_LIBRARY_PATH:./hdf5.node/../hdf5/lib
```

for Windows

```bash
set PATH=$PATH;./hdf5.node/../hdf5/bin
```

If you want one of the third party filters available put its install path on HDF5_PLUGIN_PATH

```bash
export HDF5_PLUGIN_PATH=/home/user/NodeProjects/HDF5Plugin
```

## Running Test

The tests are based on co-mocha

```bash
mocha --require should  --require co-mocha
```

