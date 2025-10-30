# Great Python with GraalPy

GraalPy brings **modern Python 3.11** to the JVM. It can run Python code with GraalVM JIT, works well with Java (and other Graal languages), and can be just as easily embedded in GraalVM Native Image.

### What makes it great
- **Embeddability.** Use the Polyglot API to call Python from Java, easily embeddable and manageable via Maven or Gradle.  
- **Compatibility.** Most pure-Python packages “just work,” and many data/ML stacks are in scope.  
- **Runtime choice.**  
  - **JVM mode:** deep Java interop + higher peak performance.  
  - **Native mode:** smaller standalone binaries, faster startup.  
- **Tooling you already know.** Works with Maven/Gradle plugins, pyenv, virtualenvs, and common IDEs. Debugging and profiling included.

### What you can do with it
- Embed Python into a Java application.
- Call Java types from Python scripts (and interop with other Graal languages).
- Build native executables that bundle your Python code and all dependencies.

# Embedding languages in Java

The GraalVM Polyglot API lets you embed and run guest languages (like JavaScript, Python, Ruby, or R) inside Java applications.

Let's see how you can set up dependencies, compile and run a polyglot app, and exchange values between Java and guest languages.

You can get everything from Maven Central.

Add the following to your pom.xml:

```xml
<dependency>
	<groupId>org.graalvm.polyglot</groupId>
	<!-- Select a language: js, ruby, python, java, llvm, wasm, languages-->
	<artifactId>python</artifactId>
	<version>25.0.0</version>
	<type>pom</type>
</dependency>
```
Note tha language and tool dependencies have to be of a type `pom`. All our language artifacts are open-source licensed.
