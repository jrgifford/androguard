

# Visualization #


## ASCII ##

The first mode to visualize methods is ascii.

### default ###

You can use directly the method show with a method object :

```
for method in a.get_methods() :
  method.show()
```


![http://androguard.googlecode.com/files/visu1.png](http://androguard.googlecode.com/files/visu1.png)

### pretty ###

But it's more interesting to display the CFG of the method by using the pretty show method.

The first display draw automatically edges between nodes :

```
import dvm
import analysis

d = DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )
d.set_vmanalysis( x )

for method in a.get_methods() :
   method.pretty_show()
```

![http://androguard.googlecode.com/files/visu2.png](http://androguard.googlecode.com/files/visu2.png)

With big methods, this display is not very useful, this is why you can choose a more classical view (IDA view) by using the set\_pretty\_show method (with the value 1) :

```
import dvm
import analysis
import bytecode

d = dvm.DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )
d.set_vmanalysis( x )

bytecode.set_pretty_show( 1 )

for method in a.get_methods() :
   method.pretty_show()
```


![http://androguard.googlecode.com/files/visu3.png](http://androguard.googlecode.com/files/visu3.png)

Or without color :
```
import dvm
import analysis
import bytecode

d = dvm.DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )
d.set_vmanalysis( x )


bytecode.set_pretty_show( 2 )

for method in a.get_methods() :
   method.pretty_show()
```

![http://androguard.googlecode.com/files/visu5.png](http://androguard.googlecode.com/files/visu5.png)


## DOT ##

Every method can be translated in DOT format with pydot :

```
import dvm
import analysis
import bytecode

d = dvm.DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )

# m will be an EncodedMethod
m = d.get_method_descriptor("Lorg/t0t0/androguard/TC/TCMod1;", "T1", "()V")


# get the analysis method and transform it in dot
buff_dot = bytecode.method2dot(x.get_method( m ))

print buff_dot
```

When you have obtained the dot format, with pydot you can display it in differents graphics formats ('canon', 'cmap', 'cmapx', 'cmapx\_np', 'dia', 'dot', 'fig', 'gd', 'gd2', 'gif', 'hpgl', 'imap', 'imap\_np', 'ismap', 'jpe', 'jpeg', 'jpg', 'mif', 'mp', 'pcl', 'pdf', 'pic', 'plain', 'plain-ext', 'png', 'ps', 'ps2', 'svg', 'svgz', 'vml', 'vmlz', 'vrml', 'vtx', 'wbmp', 'xdot', 'xlib').

To do that you must used the method2format function :

```
import dvm
import analysis
import bytecode

d = dvm.DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )

# m will be an EncodedMethod
m = d.get_method_descriptor("Lorg/t0t0/androguard/TC/TCMod1;", "T1", "()V")


# get the analysis method and transform it in dot
buff_dot = bytecode.method2dot(x.get_method( m ))

method2format( "toto.jpg", "jpg", raw=buff_dot )

# or without the dot buffer because method2format can call it directly
# method2format( "toto.jpg", "jpg", x.get_method( m ) )
```



### PNG ###

```
import dvm
import analysis
import bytecode

d = dvm.DalvikVMFormat( open("test.dex").read() )
x = analysis.VMAnalysis( d )

# m will be an EncodedMethod
m = d.get_method_descriptor("Lorg/t0t0/androguard/TC/TCMod1;", "T1", "()V")

# get the analysis method and transform it in png
bytecode.method2png("visu4.png", x.get_method( m ))
```

![http://androguard.googlecode.com/files/visu4.png](http://androguard.googlecode.com/files/visu4.png)

## Gephi ##

[Gephi](http://www.gephi.org) is an awesome tool for graph visualisation. We support the methods calls graph of an Android application by creating a [GEXF](http://www.gexf.net) format in order to open it with gephi.

In this format, you will have information about each node (in our case a node is a method), with a specific color if necessary (more quick to research something) :
  * type of the method (activity, service, receiver) (string)
  * class name (string)
  * method name (string)
  * descriptor (string)
  * permissions (how many permissions are used in a method) (integer)
  * permissions level (normal, signature, dangerous ...) (string)
  * android api entropy (float)
  * java api entropy (float)
  * dynamic code (it's indicate that this method created a DexClassLoader object, so this method tries probably to load dynamic dex code) (boolean)

Moreover, we add specific node (colorized) to an existing node if necessary :
  * an activity/service/receiver node (green, cyan, purple)
  * a risk (internet, privacy, phone, sms, money) node from blue color to red color
  * a dynamic code node (black)

It's very easy to create a gexf file (see [Usage](http://code.google.com/p/androguard/wiki/Usage?ts=1337957819&updated=Usage#Androgexf)).

```
desnos@destiny:~/androguard$ ./androgexf.py -i YOURAPP.apk -o YOURAPP.gexf
```

smshider malware :
![http://androguard.googlecode.com/files/smshider-gexf.png](http://androguard.googlecode.com/files/smshider-gexf.png)
![http://androguard.googlecode.com/files/smshider-gexf-2.png](http://androguard.googlecode.com/files/smshider-gexf-2.png)

droiddream malware :
![http://androguard.googlecode.com/files/droiddream-gexf.png](http://androguard.googlecode.com/files/droiddream-gexf.png)

anserverbot malware :
![http://androguard.googlecode.com/files/anserverbot-gexf.png](http://androguard.googlecode.com/files/anserverbot-gexf.png)

You can also watch this movie : http://androguard.googlecode.com/files/androguard-gexf.avi
http://www.youtube.com/watch?v=nbVfi5ejlWw


## XGMML ##