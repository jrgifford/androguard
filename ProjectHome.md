<font color='red'>
<h1>Project is now on <a href='https://github.com/androguard/androguard'>GitHub</a></h1>
</font>

<h2>The following documentation is deprecated</h2>



# Description #

Androguard is mainly a tool written in python to play with :
  * Dex/Odex ([Dalvik](https://sites.google.com/site/io/dalvik-vm-internals) virtual machine) (.dex) (disassemble, decompilation),
  * APK (Android [application](https://play.google.com/)) (.apk),
  * Android's binary xml (.xml),
  * Android Resources (.arsc).

Androguard is available for Linux/OSX/Windows (python powered).

**If you have decided to make a donation for the Androguard project in order to help the developers, click the donate button below for Paypal:**

[![](https://www.paypal.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=anthony%2edesnos%40gmail%2ecom&lc=FR&item_name=Androguard&currency_code=EUR&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHosted)

# Features #

**Androguard has the following features** :
  * Map and manipulate DEX/ODEX/APK/AXML/ARSC format into full Python objects,
  * Diassemble/Decompilation/Modification of DEX/ODEX/APK format,
  * Decompilation with the first native (directly from dalvik bytecodes to java source codes) dalvik decompiler (DAD),
  * Access to the static [analysis](http://code.google.com/p/androguard/wiki/Analysis) of the code (basic blocks, instructions, permissions (with database from http://www.android-permissions.org/) ...) and create your own static analysis tool,
  * Analysis a bunch of android apps,
  * Analysis with ipython/Sublime Text Editor,
  * [Diffing](http://code.google.com/p/elsim/wiki/Similarity#Diffing_of_applications) of android applications,
  * [Measure](http://code.google.com/p/elsim/wiki/Similarity#Similarity_of_applications_(aka_rip-off_indicator)) the efficiency of obfuscators (proguard, ...),
  * [Determine](http://code.google.com/p/elsim/wiki/Similarity#Similarity_of_applications_(aka_rip-off_indicator)) if your application has been pirated (plagiarism/similarities/rip-off indicator),
  * Check if an android application is [present](http://code.google.com/p/androguard/wiki/DetectingApplications) in a database (malwares, goodwares ?),
  * Open source [database](http://code.google.com/p/androguard/wiki/DatabaseAndroidMalwares) of android malware (this opensource database is done on my free time, of course my free time is limited, so if you want to help, you are welcome !),
  * Detection of ad/open source librairies (WIP),
  * Risk indicator of malicious application,
  * [Reverse](http://code.google.com/p/androguard/wiki/RE) engineering of applications (goodwares, malwares),
  * [Transform](http://code.google.com/p/androguard/wiki/Usage#Androaxml) Android's binary xml (like `AndroidManifest.xml`) into classic xml,
  * [Visualize](http://code.google.com/p/androguard/wiki/Visualization) your application with [gephi](http://www.gephi.org) (gexf format), or with [cytoscape](http://www.cytoscape.org) (xgmml format), or PNG/DOT output,
  * Integration with external decompilers (JAD+dex2jar/DED/fernflower/jd-gui...)
  * ....

# **Downloads** #

Our new repository is hosted on [github](https://github.com/androguard/androguard/)

# Sublime Text 2 Plugin #

Please read the [documentation](http://code.google.com/p/androguard/wiki/RE).

<a href='http://www.youtube.com/watch?feature=player_embedded&v=q4D9-1XJpsk' target='_blank'><img src='http://img.youtube.com/vi/q4D9-1XJpsk/0.jpg' width='425' height=344 /></a>

# Documentation #

To install androguard, please follow this [link](http://code.google.com/p/androguard/wiki/Installation) in order to respect the **requirements**.

**You can play directly with Androguard by using [Santoku](https://santoku-linux.com/) Distribution**

Please, follow the reverse engineering [tutorial](http://code.google.com/p/androguard/wiki/RE). Moreover, the [roadmap and features](http://code.google.com/p/androguard/wiki/RoadMap) are now available.

So, you can analyze, display, modify and save your apps easily and statically by creating your own software (by using the API), or by using the tool (androlyze) in command line. This tool is useful when you would like to do reverse engineering on a specific application (e.g : malware).

The second part of the tool is to do new tools to get differences between two android/java applications, or to find similarities in different applications (e.g : to check if a part or entire application has been stolen).

And for now, you can check if an android application is present in a database (like a malware).

**Check online documentation of the API** : http://doc.androguard.re/

# Screenshots #

![http://androguard.googlecode.com/files/1.3-10.png](http://androguard.googlecode.com/files/1.3-10.png)
![http://androguard.googlecode.com/files/dad.png](http://androguard.googlecode.com/files/dad.png)
![![](http://androguard.googlecode.com/files/func1mini.png)](http://androguard.googlecode.com/files/func1.png)
![![](http://androguard.googlecode.com/files/func2mini.png)](http://androguard.googlecode.com/files/func2.png)


More [screenshots ?](http://code.google.com/p/androguard/wiki/Screenshots).

# Release #

**Release Schedule:**
  * Version [1.9](http://code.google.com/p/androguard/downloads/detail?name=androguard-1.9.tar.gz)
  * Version [1.6](http://code.google.com/p/androguard/downloads/detail?name=androguard-1.6.tar.gz)
  * Version [1.5.1](http://code.google.com/p/androguard/downloads/detail?name=androguard-1.5.1.tar.gz)
  * Version [1.5](http://code.google.com/p/androguard/downloads/detail?name=androguard-1.5.tar.gz)
  * Version [1.1](http://androguard.googlecode.com/files/androguard-1.1.tar.gz)
  * Version [1.0](http://androguard.googlecode.com/files/androguard-1.0-phrack.tar.gz) of Phrack

**Win32 binaries**
  * **Androsim** [1.2](http://code.google.com/p/androguard/downloads/detail?name=androsim-1.2.exe&can=2)

**Get the latest development source code:**
https://github.com/androguard/androguard/

# Sponsors #

**Selected in the first round of the Magnificent 7 project !**

[![](http://androguard.googlecode.com/files/powered-by-rapid7.png)](http://www.rapid7.com/news-events/press-releases/2012/2012-magnificent7-program.jsp)

**Powered by:**

[![](https://www.virustotal.com/static/img/logo-small.png)](https://www.virustotal.com)

[![](https://www.python.org/static/img/python-logo.png)](http://python.org/)

**Who's using Androguard ?** (Do you use Androguard ? Contact us to have a link !)

  * Virustotal http://www.virustotal.com/
  * APKInspector http://code.google.com/p/apkinspector/
  * Marvinsafe http://www.marvinsafe.com/
  * Anubis (Andrubis) http://blog.iseclab.org/2012/06/04/andrubis-a-tool-for-analyzing-unknown-android-applications-2/ http://anubis.iseclab.org/
  * Androwarn https://github.com/maaaaz/androwarn
  * googleplay-api http://www.segmentationfault.fr/publications/reversing-google-play-and-micro-protobuf-applications/
  * MalloDroid http://www2.dcsec.uni-hannover.de/files/android/p50-fahl.pdf

# Authors #

The original authors (created on our free time) are:
  * Anthony Desnos [@adesnos](https://twitter.com/adesnos) <dev (at) androguard.re>: main author + hunter of evil angry birds
  * Zost: DAD is A Decompiler !


# Contributors #
  * Axelle Apvrille [@cryptax](https://twitter.com/cryptax)
  * Yanick Fratantonio <yanick (at) cs.ucsb.edu> http://www.cs.ucsb.edu/~yanick/
  * Craig Smith <agent (dot) craig (at) gmail.com>: 64 bits patch + magic tricks
  * Users who reported issues ([@timstrazz](https://twitter.com/timstrazz), [@thuxnder](https://twitter.com/thuxnder), ...) !

# Papers #

  * Pacsec Conference 2012: [New "open source" step in Android Application Analysis](http://code.google.com/p/androguard/downloads/detail?name=pacsec2012.pdf)
  * Phrack 68 : [Similarities for Fun & Profit](http://www.phrack.org/issues.html?issue=68&id=15#article)
  * Blackhat Abu Dhabi 2011 : [Android: from reversing to decompilation](http://code.google.com/p/androguard/downloads/detail?name=bh2011.pdf)

# Contacts #

**New features ? go to the [issues](http://code.google.com/p/androguard/issues/list)**

**Training ? Are you interesting by a training about reverse engineering on android apps ?** contact us !

**If you are interesting to be a developer and to work on this new project (check the [roadmap](http://code.google.com/p/androguard/wiki/RoadMap)), you can contact me at:**

_contact_: **dev (at) androguard.re**

_irc_: irc.freenode.net #androguard

_google\_groups_: http://groups.google.com/group/androguard

# Donation #
  * [Antiy Labs](http://www.antiy.net/)

# Friends tools #

  * [smali/baksmali](http://code.google.com/p/smali/): awesome !
  * [dex2jar](http://code.google.com/p/dex2jar/): if you wish the java bytecodes !
  * [sublimetext](http://www.sublimetext.com/): awesome editor !