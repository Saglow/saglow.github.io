---
title: java-agent
description: java代理
date: 2023-1-8
tags:	[实习项目]
toc: true
finished: true
comments: true
---


### A Simple Example
Profiler tools often report about different parameters of the Java objects at runtime by extracting information from the JVM. These parameters include information about the memory usage of an object, and the like, by using the instrumentation framework.

* Here we create an agent class with the premain method.
* The Instrumentation instance passed to the premain method will give the information about the object size.
* Package the agent class in a JAR file along with the MANIFEST.MF file.
* Pass the agent to the JVM using command line arguments.
* This is a sample class that we will use in our example. There’s nothing special about it.

```java
package com.mano.examples;
public class Main {
   public static void greet(String msg){
      System.out.println(msg);
   }
   public static void main(String[] args){
      greet("Hello Agents");
   }
}
```

### Agent Class
The instrumentation agent class with the premain method is used to retrieve the information we need. The implementation of the Instrumentation interface is passed to the premain method. We use the getObjectSize method defined by the instrumentation interface to get memory usage of the Main object at runtime.

```java
package com.mano.examples;
import java.lang.instrument.Instrumentation;
public class MyAgentClass {
   public static void premain(String agentArgs,
      Instrumentation inst) {
      System.out.println(inst.getObjectSize
         (new Main()))
   }
}
```

After that, we must create a MANIFEST.MF file. This is nothing but a text file where we put information related to the agent class. JVM will use it to load the agent. The file is typically stored in the META-INF directory. The content required for our example is pretty basic:

Manifest-Version: 1.0
Premain-Class: com.mano.examples.MyAgentClass
Now, compile all the Java files to create the class file. And finally, create the JAR files as follows:

jar -cmf META-INF/MANIFEST.MF myagent.jar com/mano/examples/
   MyAgentClass.class
Deploying Java Agents
Once an agent is created, it is deployed as a JAR file. The attribute in the manifest file specifies the agent class which will be loaded to start the agent. Note that there are many ways to start an agent: using the command-line, at runtime, or as JAR executables. We’ll use command-line here.

### Running the Agent Using the Command-line
The command-line is:
```
java -javaagent:myagent.jar -cp . com.mano.examples.Main
```

This indicates that the premain method will run prior to application execution and the size of the instance of Main is created.

### Conclusion
The power provided by the instrumentation API is open to numerous innovations. AOP is a simple example. Although Java agents and Java Instrumentation APIs are not be very frequently used in application development, the idea of what it is all about can clarify many other aspects of Java. The code example given here is rudimentary, just to give an idea how agents are created. The Java API Documentation elaborates on many aspects with greater detail; refer to it for more information.