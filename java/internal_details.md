# How java file get executed?

To compile: javac Simple.java
To execute: java Simple

- At compile time, the Java file is compiled by Java Compiler (It does not interact with OS) and converts the Java code into bytecode. A .class file is created in our case Simple.class and passed for runtime execution. The

- At runtime, the class file id loaded by ClassLoader: It is the subsystem of JVM that is used to load class files. then it is sent to bytecode verifier. Bytecode Verifier: Checks the code fragments for illegal code that can violate access rights to objects. Then it is passed to Interpreter which read bytecode stream then execute the instructions.

- static is a keyword. If we declare any method as static, it is known as the static method. The core advantage of the static method is that there is no need to create an object to invoke the static method. The main() method is executed by the JVM, so it doesn't require creating an object to invoke the main() method. So, it saves memory.

## JVM(Java Virtual Machine)

JVM (Java Virtual Machine) is an abstract machine.
It is called a virtual machine because it doesn't physically exist.
It is a specification that provides a runtime environment in which Java bytecode can be executed.
It can also run those programs which are written in other languages and compiled to Java bytecode.

JVMs are available for many hardware and software platforms. JVM, JRE, and JDK are platform dependent because the configuration of each OS is different from each other. However, Java is platform independent. There are three notions of the JVM: specification, implementation, and instance.

The JVM performs the following main tasks:

Loads code
Verifies code
Executes code

## JRE(Java Runtime Environment)

- It is also written as Java RTE. The Java Runtime Environment is a set of software tools and libraries which are used for developing Java applications. It is used to provide the runtime environment.
- It is the implementation of JVM.
- It physically exists.
- It contains a set of libraries + other files that JVM uses at runtime.
  <https://static.javatpoint.com/images/jre2.png>

- The implementation of JVM is also actively released by other companies besides Sun Micro Systems.

## JDK(Java Development Kit)

- The Java Development Kit (JDK) is a software development environment which is used to develop Java applications and applets. It physically exists. It contains JRE + development tools.
  <https://static.javatpoint.com/images/jdk2.png>

JDK is an implementation of any one of the below given Java Platforms released by Oracle Corporation:

- Standard Edition Java Platform
- Enterprise Edition Java Platform
- Micro Edition Java Platform

- The JDK contains a private Java Virtual Machine (JVM) and a few other resources such as an interpreter/loader (java), a compiler (javac), an archiver (jar), a documentation generator (Javadoc), etc. to complete the development of a Java Application.
