# API Description #

It depends if you are using the high API with Androguard classes which manage automatically class/dex files, or directly the **VM classes.**

**Check online documentation of the API** : http://doc.androguard.re/
(TO DO: update)


## Example ##

Example :
```
import androguard

_a = androguard.AndroguardS( './examples/java/Hello.class' )

# Use Androguard API to access to objects
for i in _a.gets("constant_pool") :
   i.show()

for method in _a.gets("methods") :
   method.show()

for method in _a.get("method", "test") :
   method.show()

# Or directly with the object which manage the jvm/dex format
j = _a.get_vm()

for i in j.get_methods() :
   i.show()

for i in j.get_method("test") :
   i.show()
```

It's better to use the interactive mode with Androlyze with the option "-s".



### HOW TO ###

#### open a dex/class file ? ####

By using Androguard, if you would like to open one file or a list of files :

```
_a = androguard.AndroguardS( './examples/java/Hello.class' )

# OR

a = androguard.Androguard(['./examples/java/Hello.class', './examples/java/Hello2.class', './examples/dalvik/Hello.dex'])

_a = a.get("file", './examples/java/Hello.class')
```

Or directly the low level API :

```
import jvm

TEST = "./examples/java/test/orig/Test1.class"
j = jvm.JVMFormat( open(TEST).read() )
```


```
import dvm

TEST = "./examples/dalvik/test/bin/classes.dex"
d = dvm.DalvikVMFormat( open(TEST).read() )
```

#### open an apk/jar file ? ####

You can used directly Androguard or AndroguardS, the format will be recognize automatically. But you can also used the low level API :

```
import jvm

x = jvm.JAR( "myfile.jar" )
bc = x.get_classes()
vms = []

for j in bc :
 vms.append( jvm.JVMFormat(j[1]) )

```


```
import dvm

x = dvm.APK( "myfile.apk" )
d = dvm.DalvikVMFormat( x.get_dex() )

```

#### open an axml file ? ####

```
a = AXMLPrinter( open("myfile.xml", "r").read() )
```


#### access to the constant pool table ####

With the JVMFormat, you can access directly to the constant pool table which is a simple list. All elements in the list are objects.

```
# supposed vm is a JVMFormat 
for i in vm.constant_pool :
   print i

```

#### access to methods/fields ? ####

With the JVMFormat or DalvikVMFormat, the access is easy, with get\_method(s) or get\_field(s) methods.

```
# supposed vm is a JVMFormat or DalvikVMFormat

lx = vm.get_method("test")
for x in lx : 
  print x.format
  print x.get_access(), x.get_name(), x.get_descriptor()

```

But you can also access to a specific method or field :
```
# supposed vm is a JVMFormat or DalvikVMFormat

x = vm.get_method_descriptor("Hello", "test", "([B)[B")
x.show()
```

#### modify a method/field ? ####

You can directly play with the format to modify the method, or by using high level functions if you don't know what to do exactly.

```
# Change the access flags
x.format.set_value( { "access_flags" : 2 } 

```

#### patch bytecodes of a method ? ####

You can remove, remplace, insert at a specific index (which is the position of the instruction into the list of instructions) :

```
# supposed vm is a JVMFormat or DalvikVMFormat
x = vm.get_method_descriptor("Hello", "test", "([B)[B")

code = x.get_code()

code.remove_at( 19 ) 
code.insert_at( 19, [ "sipush", 254 ] )
```

#### insert new methods into a class file ? ####

You can insert a craft method, by giving the name of the method, the descriptor (return type + parameters) and the instructions :

```
# supposed vm is a JVMFormat or DalvikVMFormat

vm.insert_craft_method( "toto", [ "ACC_PUBLIC", "[B", "[B" ], [ [ "aconst_null" ], [ "areturn" ] ] )
```

But it's better to use the insertion of method from another format because it's more powerfull. You must give a new name of the method if you would like and the Method object :

```
# supposed vm and vm2 are a JVMFormat or DalvikVMFormat

vm.insert_direct_method( "toto2", vm2.get_method("test3")[0] )


```

#### embedded Dalvik and Java virtual machines modules in your software ? ####

The first step is to get the source code :
```
pouik@camelot:~/$ hg clone https://androguard.googlecode.com/hg/ androguard
```

Now you must create your software directory, and copy all needed files :
```
pouik@camelot:~/$ mkdir myapp
pouik@camelot:~/myapp$ cp ../androguard/core/bytecode.py ./
pouik@camelot:~/myapp$ cp ../androguard/core/misc.py ./
pouik@camelot:~/myapp$ cp ../androguard/core/bytecodes/*.py ./
```

And you can create a file myapp.py and used the dvm or jvm modules :
```
#!/usr/bin/env python

import dvm

TEST = "../androguard/examples/dalvik/test/bin/classes.dex"

j = dvm.DalvikVMFormat( open(TEST).read() )
j.show()
```

After, you can used the API to do what you would like !