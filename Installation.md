Androguard is a collection of tools that run on Linux, Windows, MacOSX.





# Getting Androguard #

There are three ways to get Androguard working:

  1. Default solution: use the mercurial version

```
hg clone https://androguard.googlecode.com/hg/ androguard 
```

> 2. Use AndroGuard from a pre-installed Virtual Machine. Download [ARE](https://redmine.honeynet.org/projects/are/wiki), then don't forget to update AndroGuard to get the latest functionalities:

```
hg pull && hg update
```

> 3. Use pre-built executables (Windows only). Get the [Microsoft Visual C++ 2008 Redistributable Package](http://www.microsoft.com/en-us/download/details.aspx?id=29), and download pre-built executables: currently, only [androsim.exe](http://code.google.com/p/androguard/downloads/detail?name=androsim.exe&can=2&q=) is pre-built.

# Building from source code (default install) #

## Requirements ##

Mandatory:
  * [>= python 2.6](http://www.python.org). Note that if you wish to use andromercury, python >= 2.7 is required.

Only with default python installation, you can disassemble/decompile Android Application (APK/DEX/ODEX), but if you need more features (images, interactive shell, similarities, elf analysis), you must install the next modules:

Optional:
  * [python-dev](http://www.python.org)
  * [ipython](http://ipython.scipy.org) >= 0.12 is required by **androlyze.py**.
  * [pygments](http://pygments.org/) is required by **androlyze.py**, to have colors with decompilation
  * [pydot](http://code.google.com/p/pydot) for **androdd.py**
  * [python-ptrace](https://bitbucket.org/haypo/python-ptrace/wiki/Home) for **androdump.py**
  * [chilkat](http://www.chilkatsoft.com/): used to unzip the APK application for python2.6, otherwise the zip python module is used (module apk.py). Also used to retrieve the APK's certificate.
  * [magic](https://github.com/ahupp/python-magic) is used in method get\_files\_types in APK module to found files types (module apk.py)
  * [pyfuzzy](http://pyfuzzy.sourceforge.net/) is used to calculate risk indicator (module **androrisk.py**)
  * [mercury](http://labs.mwrinfosecurity.com/tools/2012/03/16/mercury/downloads/) is required by **andromercury.py**
  * the elsim subdirectory, used by **androcsign.py, androsign.py, androdiff.py, androsim.py and andromercury.py**, also require:
    * [sparsehash](http://code.google.com/p/google-sparsehash/)
    * [muparser](http://muparser.sourceforge.net/)
    * [snappy](http://code.google.com/p/snappy/)
    * [bzip2](http://bzip.org/)
    * [zlib](http://zlib.net/)
  * [psyco](http://psyco.sourceforge.net/) is used to accelerate androguard, but it's not mandatory to install it.


/ To check: requirement of numpy, scipy,   [smiasm](http://code.google.com/p/smiasm/), [xz](http://tukaani.org/xz/) /

## Building AndroGuard ##

For now, androsim.py + androdiff.py + androsign.py + androcsign.py are available for linux 32/64 bits and MacOSX with **native libraries**. Thus, if you would like to use them, you need to compile librairies.

To compile the elsim directory (and thus Androguard), you might have to patch the formula and libelsign Makefiles:

  * in elsim/elsign/formula/Makefile: add the appropriate include directory where to find muParser.h. For example:
```
CFLAGS += -I/usr/include/muParser
```
  * in elsim/elsign/libelsign/Makefile, add the appropriate include directory for muParser.h and python. Example:
```
CFLAGS += -I/usr/include/muParser -I/usr/include/python2.6
```

Once those Makefiles are patched, compile from the root directory of AndroGuard:
```
$ make
```

## Guided install on Ubuntu/Debian ##

To build AndroGuard on a Ubuntu or Debian host, follow these instructions.

Install development packages on your host:
```
$ sudo apt-get install mercurial python python-setuptools g++
```

Download Androguard's sources:
```
$ hg clone https://androguard.googlecode.com/hg/ androguard 
```

Install requirements:
```
$ sudo apt-get install python-dev python-bzutils libbz2-dev libmuparser-dev libsparsehash-dev python-ptrace python-pygments python-pydot graphviz liblzma-dev libsnappy-dev
```

Some requirements should be installed from sources or as python packages (i.e the current Ubuntu/Debian package does not exist or is insufficient).

chilkat: download the latest Chilkat for Python, then install or, more simply, unpack in androguard's dir.


iPython:
```
$ sudo easy_install ipython
```

pyFuzzy: get the latest and install from sources. For example,
```
$ wget http://sourceforge.net/projects/pyfuzzy/files/latest/download?source=files
$ tar xvfz pyfuzzy-0.1.0.tar.gz
$ cd pyfuzzy-0.1.0
$ sudo python setup.py install
```

python-magic: the default package, released with some systems, won't work in all cases. If you get magic errors at using Androlyze, get the latest python-magic sources, and install.
```
$ git clone git://github.com/ahupp/python-magic.git
$ cd python-magic
$ sudo python setup.py install 
```


mercury: install mercury in a different directory and link that directory to a directory inside androguard:
```
$ mkdir mercury
$ wget http://labs.mwrinfosecurity.com/assets/254/mercury-v1.0.zip
$ unzip mercury-v1.0.zip
$ cd <ANDROGUARDDIR>
$ ln -s <PATH>/mercury ./mercury
```


Finally, build Androguard as [explained here](http://code.google.com/p/androguard/wiki/Installation#Building)


## Run AndroGuard ##

After the installation of requirements, you can direcly run the tools in the main directory of AndroGuard.

```
$ ls
androapkinfo.py  androgexf.py     androsim.py     dad        mercury     tools
androaxml.py     androguard       androxgmml.py   demos      README.txt
androcsign.py    androlyze.py     apkviewer.py    elsim      setup.py
androdd.py       andromercury.py  CHANGELOG       examples   signatures
androdiff.py     androrisk.py     COPYING         externals  specs
androdump.py     androsign.py     COPYING.LESSER  Makefile   tests
```

Examples :
```
$ ./demos/dalvikvm_format_1.py
$ ./androlyze.py -i ~/Téléchargements/com.rovio.angrybirdsseasons-1.apk -m . -p
```

There are a few demos in the **demos** directory, and all tests are in **tests** directory.