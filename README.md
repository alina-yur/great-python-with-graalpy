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
