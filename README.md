FLANN - Fast Library for Approximate Nearest Neighbors
======================================================

FLANN is a library for performing fast approximate nearest neighbor searches in high dimensional spaces. It contains a collection of algorithms we found to work best for nearest neighbor search and a system for automatically choosing the best algorithm and optimum parameters depending on the dataset.
FLANN is written in C++ and contains bindings for the following languages: C, MATLAB, Python, and Ruby.


Documentation
-------------

Check FLANN web page [here](http://www.cs.ubc.ca/research/flann).

Documentation on how to use the library can be found in the doc/manual.pdf file included in the release archives.

More information and experimental results can be found in the following paper:

  * Marius Muja and David G. Lowe, "Fast Approximate Nearest Neighbors with Automatic Algorithm Configuration", in International Conference on Computer Vision Theory and Applications (VISAPP'09), 2009 [(PDF)](https://www.cs.ubc.ca/research/flann/uploads/FLANN/flann_visapp09.pdf) [(BibTex)](http://people.cs.ubc.ca/~mariusm/index.php/FLANN/BibTex)


Getting FLANN
-------------

If you want to try out the latest changes or contribute to FLANN, then it's recommended that you checkout the git source repository: `git clone git://github.com/mariusmuja/flann.git`

If you just want to browse the repository, you can do so by going [here](https://github.com/mariusmuja/flann).

Building FLANN
--------------
## Windows
Following assumes Win11 x64 and MSVC as development environment.

FLANN Depends on `pkg-config`, which is in instance a part of [`GTK` distribution](https://www.gtk.org/). Thus you will need to build GTK in order to be able to go on with building FLANN on Windows.

### MATLAB
>as for now you will not able to build .mex64 files to use flann with matlab. Help needed. 

If you are going to build the matlab mex files, then be sure to have configured a mex compiler in matlab first. You can issue following in terminal:
```
  matlab -nodesktop -r "mex -setup; mex -setup C++; quit"
```

### Building `GTK`
In case if you don't have `MSYS2` installed in your sytem you should install it first by issuing:
```sh
  mkdir -F build/downloads && cd build
  curl -o downloads/msys2-x86_64-latest.sfx.exe https://repo.msys2.org/distrib/msys2-x86_64-latest.sfx.exe
  .\downloads\msys2-x86_64-latest.sfx.exe -y
  .\msys64\usr\bin\bash -lc ' '
```
restart the terminal after msys2 was called for the first time
```
  .\msys64\usr\bin\bash -lc 'pacman --noconfirm -Syuu'
  .\msys64\usr\bin\bash -lc 'pacman --noconfirm -Su'
  .\msys64\usr\bin\bash -lc 'pacman --noconfirm -S patch make diffutils bison flex'
```
Then you can go ahead with building `GTK`:
```sh
  ##FIXME: remove when merged git clone https://github.com/wingtk/gvsbuild && cd ./gvsbuild
  git clone https://github.com/iAnyKey/gvsbuild -b fix_vs2022build_lz4 && cd ./gvsbuild
  python ./build.py build --build-dir=$pwd\\..\\gtk -p=x64 --vs-ver=17 --msys-dir="$pwd\\..\\msys64" pkg-config lz4 && cd ..
```
Then you can proceed building `FLANN`

### Building `FLANN`
In case if you have built `GTK` to have `pkg-config` in your system, it may be necessary to specify `PKG_CONFIG_ROOT` and `PKG_CONFIG_EXECUTABLE`, which point to the package.

Out of the `build` directory issue
```
   cmake .. -DPKG_CONFIG_ROOT="$pwd/gtk/gtk/x64/release/bin" -DPKG_CONFIG_EXECUTABLE="$pwd/gtk/gtk/x64/release/bin/pkg-config.exe"
   cmake --build .
```

Installing FLANN
----------------
In Order to install FLANN to its default folder (e.g. `C:/Program Files (x86)/flann/` on Windows) you will need to run following command from `./build` folder with elevated command prompt:
```
  cmake --install .
```

Conditions of use
-----------------

FLANN is distributed under the terms of the [BSD License](https://github.com/mariusmuja/flann/blob/master/COPYING).

Bug reporting
-------------

Please report bugs or feature requests using [github's issue tracker](http://github.com/mariusmuja/flann/issues).
