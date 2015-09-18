

# Decompiler #

If you would like to display the source code (and not the bytecode) of a method or a class, you can call the _source_ method of the corresponding object.

```
In [1]: a, d, dx = AnalyzeAPK("./apks/malwares/DroidDream/Magic Hypnotic Spiral.apk", decompiler="dad")

In [2]: d.CLASS_Lcom_android_root_adbRoot.METHOD_crypt.source()
```

```
In [1]: a, d, dx = AnalyzeAPK("./apks/malwares/DroidDream/Magic Hypnotic Spiral.apk", decompiler="ded")

In [2]: d.CLASS_Lcom_android_root_adbRoot.METHOD_crypt.source()
```

```
In [1]: a, d, dx = AnalyzeAPK("./apks/malwares/DroidDream/Magic Hypnotic Spiral.apk", decompiler="dex2jad")

In [2]: d.CLASS_Lcom_android_root_adbRoot.METHOD_crypt.source()
```


If you would like to change configuration paths, it's possible direcly by modifing the hashtable in the _androconf_ module:
```
In [2]: androconf.CONF
Out[2]: 
{'BIN_DED': 'ded.sh',
 'BIN_DEX2JAR': 'dex2jar.sh',
 'BIN_JAD': 'jad',
 'PATH_DED': './decompiler/ded/',
 'PATH_DEX2JAR': './decompiler/dex2jar/',
 'PATH_JAD': './decompiler/jad/'}
```

## DAD (DAD is A Decompiler) ##

DAD is the default decompiler (python) of Androguard (include in the project), so you have nothing to do for the installation, and DAD is very fast due to the fact that it is a native decompiler, and the decompilation is done on the fly for each class/method.

## DED ##

In order to have the support of [DED](http://siis.cse.psu.edu/ded/) directly in androguard, you must following this [installation](http://siis.cse.psu.edu/ded/installation.html).

By default, the path of ded is in the androguard directory:
  * decompiler/ded/

where you have the following files (if you follow ded installation):
```
desnos@destiny:~/androguard/decompiler$ ls ded/
android-libs  ded-0.7.1  ded-launcher-0.7.1  ded.sh  jasminclasses-2.4.0.jar  LICENCE  output  README  soot
```

## dex2jar + jad -> (dex2jad) ##

It's also possible to use [code.google.com/p/dex2jar dex2jar] (dex to class) and [jad](http://www.varaneckas.com/jad) (class to java) to decompile methods.

By default, the paths of dex2jar and jad is in the androguard directory:
  * decompiler/dex2jar
  * decompiler/jad

where you have the following files:

```
desnos@destiny:~/androguard/decompiler$ ls dex2jar/
com  dex2jar.bat  dex2jar-dump.bat  dex2jar-dump.sh  dex2jar.sh  jackpal  lib  LICENSE.txt  NOTICE.txt  setclasspath.bat  toto.apk  toto_dex2jar.jar
desnos@destiny:~/androguard/decompiler$ ls jad/
jad
```