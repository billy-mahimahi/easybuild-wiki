This short guide will explain how to install the environment modules software package without root permissions, together with Tcl on which it depends.

### Tcl

1. Go to [[http://www.tcl.tk]] and download the latest Tcl sources. 
At the time of writing, the latest available Tcl version was 8.5.13, which can be downloaded [[here|http://prdownloads.sourceforge.net/tcl/tcl8.5.13-src.tar.gz]]. The remainder of these commands will assume Tcl v8.5.13 is being installed, you may need to adjust them accordingly.
2. Unpack the Tcl source tarball:
```bash
tar xfvz tcl8.5.13-src.tar.gz
```
3. Pick a location where you will install Tcl. It should be a directory you have write permissions on.
My suggestion would be to use something like `$HOME/.local/Tcl`.
4. Go to the `unix` subdirectory of the unpacked Tcl directory, and run the `configure` script using the `--prefix` option:
```bash
cd tcl8.5.13/unix
./configure --prefix=$HOME/.local/Tcl
```
If you're building Tcl and environment modules on Mac, you should run `configure` in the `tcl8.5.13/macosx` directory instead.
5. Next, build Tcl using the `make` command. If the system you are building on has multiple cores, running make in parallel will speed up the build. Just use the `-j` option, and pass it a degree of parallelism (just use the number of cores your system has available), e.g.:
```
make -j 4
```
6. If you want to make sure the build is correct, you can run the test suite that comes with Tcl, using:
```bash
make test
```
It's probably OK to skip this step if you're in a hurry.
7. The final step consists of installing Tcl to the directory specified in step 4. To do this, simply run:
```bash
make install
```
**All done!** Now you are ready to build the environment modules package, which requires Tcl.

### environment modules

1. Download the latest source tarball for the environment modules tools from [[http://modules.sourceforge.net/]].

At the time of writing, the latest available version is 3.2.9c which can be downloaded [[here|http://prdownloads.sourceforge.net/modules/modules-3.2.9c.tar.gz]].