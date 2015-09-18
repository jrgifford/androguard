


# APK #

## APK( filename, raw=False, mode="r") ##
@param raw : specify (boolean) if the filename is a path or raw data


## get\_dex() ##
Return the raw data of the classes dex file (this is a string)
Example:
```
In [13]: dex = a.get_dex()

In [14]: dex
Out[14]: 'dex\n035\x00Q)\xd1\xe8\xf5r\x95\xc0g\x11\x9a\xcf\xc7 A\x07\x05\'\xfe\xd5\t\xb20\xd6\xf85\x00\x00p\x00\x00\x00xV4\x12\x00\x00\x00\x00\x00\x00\x00\x00d5\x00\x00\xf6\x00\x00\x00p\x00\x00\x00N
...
```

## get\_files() ##
Return the files inside the APK
Example:
```
In [11]: a.get_files()
Out[11]: 
['res/drawable/ic_launcher.png',
 'res/layout/main.xml',
 'AndroidManifest.xml',
 'resources.arsc',
 'classes.dex',
 'META-INF/MANIFEST.MF',
 'META-INF/CERT.SF',
 'META-INF/CERT.RSA']
```

## get\_permissions() ##
```
In [19]: a.get_permissions()
Out[19]: 
['android.permission.RECEIVE_BOOT_COMPLETED',
 'android.permission.INTERNET',
 'android.permission.READ_PHONE_STATE',
 'android.permission.WRITE_EXTERNAL_STORAGE',
 'android.permission.ACCESS_NETWORK_STATE',
 'android.permission.SEND_SMS',
 'android.permission.RECEIVE_SMS']
```

## is\_valid\_APK() ##
Return true if the APK is valid, false otherwise


# DalvikVMFormat #

This class can parse a classes.dex file of an Android application (APK).

## DalvikVMFormat(buffer, decompiler=None) ##
buffer is a string which represents the classes.dex file (raw buffer)
decompiler object can be associated to display the java source code

# TaintedVariable #

## show\_paths(self) ##

# VMAnalysis #

This class analyses a class file or a dex file

## VMAnalysis(vm) ##

@param vm : a virtual machine object

# Static #

## AnalyzeAPK(filename, raw=False, decompiler=None) ##

Analyze an android application and setup all stuff for a more quickly analysis !

@param filename : the filename of the android application or a buffer which represents the application
@param raw : True is you would like to use a buffer
@param decompiler : ded, dex2jad, dad
@rtype : return the APK, DalvikVMFormat, and VMAnalysis objects

## ExportVMToPython(vm) ##

Export classes/methods/fields' names in the python namespace
@param vm : a VM object (e.g DalvikVMFormat, JVMFormat)