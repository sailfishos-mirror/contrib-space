# INSTRUCTIONS

**This is the old SWI-Prolog space package as a core package.  New users
should use the add-on from https://github.com/JanWielemaker/space.  This
version will be dropped in the near future.**

Make sure you have at least SWI-Prolog 5.7.13. This is necessary for
non-deterministic C++ predicates.

Install spatialindex. (Use spatialindex release >= 1.3.3 or the current
source in the Trac repository at
http://trac.gispython.org/spatialindex.) Install GEOS. The space package
has been tested with version 3.1.1.

An outline of the installation procedure (please let me know where it
fails with your setup) is listed below:

## Install GEOS

Debian/Ubuntu systems can install the package libgeos++-dev using

  ```
  $ sudo apt-get install libgeos++-dev
  ```

The fragment below describes installation from source.

  ```
  $ svn checkout http://svn.osgeo.org/geos/trunk geos-svn
  $ cd geos-svn/trunk
  $ ./autogen.sh
  $ ./configure --prefix=[...]
  $ make
  $ sudo make install
  ```

## Install spatialindex

  ```
  $ git clone http://github.com/libspatialindex/libspatialindex
  $ cd libspatialindex
  $ ./autogen.sh
  $ ./configure --prefix=[...]
  $ make
  $ sudo make install
  ```

## Download the development version of SWI-Prolog

  ```
  $ git clone git://www.swi-prolog.org/home/pl/git/pl-devel.git
  ```

## Install SWI-Prolog and the space package

  ```
  $ cp build.templ build
  [add space to variable EXTRA_PKGS]
  $ ./prepare
  $ ./build
  ```

## run the tests and the demo

  ```
  $ cd packages/space
  $ pl -s demo_space.pl
  ```

## Mac OS X

On Mac OS X you might have to help ./configure a bit by telling it how
to call the preprocessor. This should work:

  ```
  CXXCPP="g++ -E" ./configure
  ```

Also, since 'pl' is a reserved command, Prolog should be called with
'swipl'.

If the compilation finished without errors the demo script will prompt
you with instructions.

If it does not work, please contact me.

Willem Robert van Hage <W.R.van.Hage@vu.nl>

## Ubuntu/Debian

This explains getting the prerequisites on Ubuntu/Debian. Tested on
Ubuntu Jaunty (9.04, 64-bits). Install the following packages (in
addition to what you need to build SWI-Prolog in the first place):

  ```
  $ sudo apt-get install libtool subversion libgeos++-dev
  ```

Fetch and install spatialindex using the instructions above.

## Windows

To compile the space package as part of SWI-Prolog by running "/pl-devel/src/make.cmd" you need to put "space" in the list of packages in the PKGS variable in "/pl-devel/src/rules.mk".

## Problems with local installations of GEOS and spatialindex

If you install spatialindex or geos in a local directory, for example
your home directory, using a prefix (with ./configure --prefix=$PREFIX),
make sure that the directory where the spatialindex
library or geos library was installed, e.g. /usr/local/lib, is in the
environment variables LD_LIBRARY_PATH and LIBRARY_PATH. Make sure that
the directory where the spatialindex header files were installed, e.g.
/usr/local/include, is in the environment variable CPLUS_INCLUDE_PATH.
Usually, this will work correctly automatically.

On unixlike systems using bash, for example, you could add this to your
.bashrc or .bash_profile before running ./configure --prefix=$PREFIX:

  ```
  export PREFIX=/home/yourself
  export CPLUS_INCLUDE_PATH=$PREFIX/include
  export LIBRARY_PATH=$PREFIX/lib
  export LD_LIBRARY_PATH=$PREFIX/lib
  ```


