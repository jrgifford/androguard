

# USAGE #

## Androaxml ##

[BlogPost1](http://androguard.blogspot.com/2011/03/androids-binary-xml.html)

You can used it to transform Android's binary XML (eg: AndroidManifest.xml) into classic xml (human readable ;)).

```
$ ./androaxml.py -h
Usage: androaxml.py [options]

Options:
-h, --help            show this help message and exit
-i INPUT, --input=INPUT
                      filename input (APK or android's binary xml)
-o OUTPUT, --output=OUTPUT
                      filename output of the xml
-v, --version         version of the API

$ ./androaxml.py -i yourfile.apk -o output.xml
$ ./androaxml.py -i AndroidManifest.xml -o output.xml
```

## Androapkinfo ##

This tool displays information on a given APK:
  * permissions
  * services
  * activities
  * receivers
  * usage of native code
  * usage of native code

```
axelle$ ./androapkinfo.py -i qicsomos.apk
FILES: 
	META-INF/MANIFEST.MF 	META-INF/MANIFEST.MF -7eb55c04
	res/layout/main.xml 	res/layout/main.xml 54a83b5b
	AndroidManifest.xml 	AndroidManifest.xml 2eef2f86
	res/drawable-mdpi/ic_launcher.png 	res/drawable-mdpi/ic_launcher.png -22437ab
	res/drawable-hdpi/ic_launcher.png 	res/drawable-hdpi/ic_launcher.png -4e108fda
	META-INF/PLATFORM.RSA 	META-INF/PLATFORM.RSA 5c8d71d3
	META-INF/PLATFORM.SF 	META-INF/PLATFORM.SF 5b48f7ec
	resources.arsc 	resources.arsc -55923b8c
	classes.dex 	classes.dex -bafd464
	res/drawable-ldpi/ic_launcher.png 	res/drawable-ldpi/ic_launcher.png -6272d259
PERMISSIONS: 
	android.permission.SEND_SMS ['dangerous', 'send SMS messages', 'Allows application to send SMS messages. Malicious applications may cost you money by sending messages without your confirmation.']
	android.permission.READ_LOGS ['dangerous', 'read sensitive log data', "Allows an application to read from the system's various log files. This allows it to discover general information about what you are doing with the phone, potentially including personal or private information."]
MAIN ACTIVITY:  org.projectvoodoo.simplecarrieriqdetector.Main
ACTIVITIES:  ['org.projectvoodoo.simplecarrieriqdetector.Main']
SERVICES:  []
RECEIVERS:  []
PROVIDERS:  []
Native code: False
Dynamic code: False
Reflection code: False
```

## Androcsign ##

This tool helps you to create your own signatures in order to add them in the database. In fact, it's more easy after an analysis to isolate which parts are the more interesting to add in the database in order to detect the malware (and variants). So, the idea is to describe your signature of a malware in a json format file to add this signature to the database.

```
desnos@destiny:~/androguard$ ./androcsign.py -h
Usage: androcsign.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use this filename
  -r REMOVE, --remove=REMOVE
                        remote the signature
  -o OUTPUT, --output=OUTPUT
                        output database
  -l LIST, --list=LIST  list signatures in database
  -c CHECK, --check=CHECK
                        check signatures in database
  -v, --version         version of the API
```

The input file is a classical json format :

```
[ { "SAMPLE" : "apks/malwares/DroidDream/Magic Hypnotic Spiral.apk" }, { "BASE" : "AndroidOS", "NAME" : "DroidDream", "SIGNATURE" : [ { "TYPE" : "METHSIM", "CN" : "Lcom/android/root/Setting;", "MN" : "postUrl", "D" : "(Ljava/lang/String; Landroid/content/Context;)V" } ], "BF" : "0" } ]
```

where SAMPLE is the file where signatures will be extracted. NAME is the name of your signature. And SIGNATURE is a list of dictionnary which describes all sub-signatures.

A sub-signature can be a :

METHSIM : CN is the classname, NM is the method name, and D is the descriptor
CLASSSIM : CN is the classname
So a sub-signature can be apply on a specific method or directly on an entire class.

BF is the boolean formula of the whole signature, so it's possible to mix different sub-signatures.

When the sub-signature is added to the database, the engine will keep only interesting information :

entropies of general signature, android packages, java packages, binary raw, and exceptions. These entropies are using to clustering sub-signatures and compare items : it is these values that which will be used to apply clustering,
value of the general signature : it is this value that which will be used to apply similarity distance on each required cluster.
In the previous output, we isolated one method (postUrl) in an application (droiddream malware) to create a new signature. Androcsign will extract useful information of this application to add the signature in the database :

```
desnos@destiny:~/androguard$ ./androcsign.py -i signatures/droiddream.sign -o signatures/dbandroguard
[{u'DroidDream': [[[0, 'QltTUDBQMVNTUDJQMlAwRjBQMVAxU1AxRjBQMVAxUDFQMVAxUDJQMFAxUDFQMVAxU1AxUDFQMFAxXUJbUDFJUDFdQltQMVAxUDBQMVAwUDFQMV1CW1AxSVAxXUJbUDFQMUlTXUJbU1Axe0xhbmRyb2lkL2NvbnRlbnQvQ29udGV4dDtnZXRTaGFyZWRQcmVmZXJlbmNlcyhMamF2YS9sYW5nL1N0cmluZzsgSSlMYW5kcm9pZC9jb250ZW50L1NoYXJlZFByZWZlcmVuY2VzO31QMXtMYW5kcm9pZC9jb250ZW50L1NoYXJlZFByZWZlcmVuY2VzO2VkaXQoKUxhbmRyb2lkL2NvbnRlbnQvU2hhcmVkUHJlZmVyZW5jZXMkRWRpdG9yO31TUDF7TGFuZHJvaWQvY29udGVudC9TaGFyZWRQcmVmZXJlbmNlcyRFZGl0b3I7cHV0SW50KExqYXZhL2xhbmcvU3RyaW5nOyBJKUxhbmRyb2lkL2NvbnRlbnQvU2hhcmVkUHJlZmVyZW5jZXMkRWRpdG9yO31QMXtMYW5kcm9pZC9jb250ZW50L1NoYXJlZFByZWZlcmVuY2VzJEVkaXRvcjtjb21taXQoKVp9XUJbUl1CW1AxUDFHXUJbUDFHXQ==', 4.7122836112976074, 4.4915299415588379, 4.9674844741821289, 4.9468302726745605, 0.0]], u'a']}]
```

## Androdd ##

This tool is used to output graphs for each method of each class of an Android package.

```
$ ./androdd.py --help
Usage: androdd.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use this filename
  -o OUTPUT, --output=OUTPUT
                        base directory to output all files
  -d, --dot             write the method in dot format
  -f FORMAT, --format=FORMAT
                        write the method in specific format (png, ...)
  -v, --version         version of the API
```

  * input: an Android APK or classes.dex
  * output directory is mandatory, or the tool does not output anything.
  * output formats: PNG, JPG.
  * if you wish both DOT and PNG output for ex, mix options -d and -f PNG



## Androdiff ##

The tool is used to compare/display the differences between two apps.
The documentation is available [here](http://code.google.com/p/elsim/wiki/Similarity#Androdiff)


## Androdump ##

[BlogPost1](http://androguard.blogspot.fr/2010/11/androdump-dump-your-jvm.html)

You can used it to dump a linux process in order to get the original class files.

```
$ ./androdump.py -h
Usage: androdump.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        pid
  -v, --version         version of the API


```

```
pouik@camelot:~/androguard$ ps aux |grep java
pouik 21008 0.1 0.5 673840 10688 pts/5 Sl+ 10:28 0:02 java Test2
pouik 21548 0.0 0.0 3060 812 pts/2 S+ 11:00 0:00 grep java
pouik@camelot:~/androguard$ ./androdump.py -i 21008
HEADER 0x6f990000-0x6fee0000 (rw-p)
Test2 ()V
Test2 get_x ()I
Test2 main ([Ljava/lang/String;)V
Test2bis ()V
Test2bis get_T ()Ljava/lang/String;
```

## Androgexf ##

This tool outputs graphs using the GEXF format.

```
desnos@destiny:~/androguard$ ./androgexf.py -h
Usage: androgexf.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        filename input (dex, apk)
  -o OUTPUT, --output=OUTPUT
                        filename output of the xgmml
```

For instance,

```
desnos@destiny:~/androguard$ ./androgexf.py -i YOURAPP.apk -o YOURAPP.gexf
```

The output graph can be viewed using an external tool, named [Gephi](http://www.gephi.org/). For real examples of visualization of Android malware, please see [this page](http://code.google.com/p/androguard/wiki/Visualization#Gephi).

## Androlyze ##

Androlyze is a tool to analyze Android applications.
The most common features are available via command line, the others via a Python interactive shell:
```
Usage: androlyze.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use this filename
  -d, --display         display the file in human readable format
  -m METHOD, --method=METHOD
                        display method(s) respect with a regexp
  -f FIELD, --field=FIELD
                        display field(s) respect with a regexp
  -s, --shell           open a shell to interact more easily with objects
  -v, --version         version of the API
  -p, --pretty          pretty print !
  -t TYPE_PRETTY, --type_pretty=TYPE_PRETTY
                        set the type of pretty print (0, 1) !
  -x, --xpermissions    show paths of permissions
```

Using androlyze via the interactive shell opens up to tons of other features. Basically, all functions of the code are available that way:

```

./androlyze.py -s
Welcome to Androlyze ALPHA 0-update1
>>> j = JVMFormat( open("./VM.class").read() )
>>> j.show()

# Get specific methods
>>> x = j.get_method("<init>")[0]
>>> x.show()

# Change name
>>> x.set_name("toto")

# Save it
>>> fd = open("VM2.class", "w")
>>> fd.write(j.save())
>>> fd.close()

```

## Andromercury ##

This tool links with the [Mercury](http://labs.mwrinfosecurity.com/tools/2012/03/16/mercury/) framework

See [blog post](http://androguard.blogspot.fr/2012/03/androguard-mercury.html)

```
$ ./andromercury.py -h
Usage: andromercury.py [options]

Options:
  -h, --help            show this help message and exit
  -l LIST, --list=LIST  list all packages
  -i INPUT, --input=INPUT
                        get specific packages (a filter)
  -r REMOTEHOST, --remotehost=REMOTEHOST
                        specify ip of emulator/device
  -p PORT, --port=PORT  specify the port
  -o OUTPUT, --output=OUTPUT
                        output directory to write packages
  -b DATABASE, --database=DATABASE
                        database : use this database
  -c CONFIG, --config=CONFIG
                        use this configuration
  -v, --verbose         display debug information
```

## Androrisk ##

```
 ./androrisk.py -h
Usage: androrisk.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use these filenames
  -a, --analysis        perform analysis to calculate the risk
  -m, --method          perform analysis of each method
  -d DIRECTORY, --directory=DIRECTORY
                        directory : use this directory
  -v, --version         version of the API
```



## Androsign ##

Checks whether a given sample is listed in the database or not.

```
$ ./androsign.py -h
Usage: androsign.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use this filename
  -d DIRECTORY, --directory=DIRECTORY
                        directory : use this directory
  -b DATABASE, --database=DATABASE
                        database : use this database
  -c CONFIG, --config=CONFIG
                        use this configuration
  -v, --verbose         display debug information

```

For example, see [http://code.google.com/p/androguard/wiki/AndroidMalwareAnalysis](AndroidMalwareAnalysis.md):

```
$ ./androsign.py -d apks/malwares/foncy/ -b signatures/dbandroguard -c signatures/dbconfig
98a402d885cdb941dca8b45a4bbcbbe7f44ba62910d519bc1c2161dba117ebd2 : ----> Foncy
81dd17ea168cf884bfb5aebb7cd2241a5624d1ae14444594bf7677e1080339f9 : ----> Foncy
d9ef940236f285548a60be0d575d7bba4587bdfc3f6c56f38b5da601686344a9 : ----> Foncy
SuiConFo 1.26.apk : ----> None
127sc.apk : ----> None
```

## Androsim ##

The tool is used to get the similarities between two apps.
The documentation is available [here](http://code.google.com/p/elsim/wiki/Similarity#Androsim)

```
axelle@caiman:~/softs/androguard$ ./androsim.py -h
Usage: androsim.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        file : use these filenames
  -t THRESHOLD, --threshold=THRESHOLD
                        define the threshold
  -c COMPRESSOR, --compressor=COMPRESSOR
                        define the compressor
  -d, --display         display all information about methods
  -n, --new             don't calculate the similarity score with new methods
  -e EXCLUDE, --exclude=EXCLUDE
                        exclude specific class name (python regexp)
  -s SIZE, --size=SIZE  exclude specific method below the specific size
  -x, --xstrings        display similarities of strings
  -v, --version         version of the API
  -l LIBRARY, --library=LIBRARY
                        use python library (python) or specify the path of the
shared library)
```

## Androxgmml ##

[BlogPost1](http://androguard.blogspot.com/2011/02/android-apps-visualization.html)

You can used it to transform an apk/jar/class/dex files format into an xgmml graph which represent the control flow graph or the functions call.

```
$ ./androxgmml.py -h
Usage: androxgmml.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        filename input
  -o OUTPUT, --output=OUTPUT
                        filename output of the xgmml
  -f, --functions       include function calls
  -e, --externals       include extern function calls
  -v, --version         version of the API
```

```
./androxgmml.py -i myapp.jar -o output.xgmml
./androxgmml.py -i myapp.apk -o output.xgmml
./androxgmml.py -i myclass.class -o output.xgmml
./androxgmml.py -i mydex.dex -o output.xgmml

# with functions call :
./androxgmml.py -i myapp.jar -f -o output.xgmml

# with external function calls
./androxgmml.py -i myapp.jar -e -o output.xgmml

# with both
./androxgmml.py -i myapp.jar -e -f -o output.xgmml


```

## Apkviewer ##

```
 ./apkviewer.py -h
Usage: apkviewer.py [options]

Options:
  -h, --help            show this help message and exit
  -i INPUT, --input=INPUT
                        filename input (dex, apk)
  -o OUTPUT, --output=OUTPUT
                        directory output
```