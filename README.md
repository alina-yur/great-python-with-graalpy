# Great Python with GraalPy

GraalPy brings **modern Python 3.11** to the JVM. It can run Python code with GraalVM JIT, works well with Java (and other Graal languages), and can be just as easily embedded in GraalVM Native Image. You can run it on any JVM of your choice, such as GraalVM, Oracle JDK, OpenJDK, but you will get the best performance on GraalVM.

### What makes GraalPy great
- **Embeddability.** Use the Polyglot API to call Python from Java, easily embeddable and manageable via Maven or Gradle.  
- **Compatibility.** Most pure-Python packages just work, and many data/ML packages, such as `openai`, `pydantic`, `matplotlib`, and `huggingface`, are also supported. 
- **Runtime choice.**  
  - **JVM mode:** easy Java interop + higher peak performance.  
  - **Native mode:** smaller standalone binaries, faster startup.  
- **Your favourite tooling** GraalPy works with Maven/Gradle plugins, pyenv, virtualenvs, and popular IDEs, such as as IntelliJ IDEA, PyCharm, and VS Code, including debugging and profiling.

### What you can do with it
- Embed Python into a Java application.
- Call Java types from Python programs (and interop with other Graal languages).
- Build native executables that bundle your Python code and all dependencies.



## How to embed Python in Java

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

### Embedding context options

**CheckHashPycsMode**  
Controls how `.pyc` files are validated.  
`default` = follow the hash-based flag in the file, `always` = re-hash source every time, `never` = trust the existing hash. Useful if you care about reproducible builds or performance.

**CompressionModulesBackend**  
Lets you pick whether `zlib`, `bz2`, and `lzma` use the Java backend or native backend. Has to match across all contexts in the same engine.

**DontWriteBytecodeFlag**  
Same as Python `-B`. Disables writing `.pyc` files. Handy for read-only filesystems or when you don’t want GraalPy touching the source tree.

**IgnoreEnvironmentFlag**  
Same as Python `-E`. Ignores all `PYTHON*` env vars. Good for sandboxing and avoiding “works on my machine” issues.

**IsolateFlag**  
Same as Python `-I`. Prevents adding the current working directory to `sys.path`. Makes the context fully isolated from the host machine.

**PyCachePrefix**  
Redirects `.pyc` output to a separate directory instead of writing into `__pycache__` next to source files. Useful for container builds or when source trees must stay clean.

**PythonOptimizeFlag**  
Same as `-O`. Strips `assert` and `__debug__` blocks. Slight performance gain, but removes debug checks.

**StandardStreamEncoding**  
Force a specific encoding for stdin/stdout/stderr (like setting `PYTHONIOENCODING`). Useful if you're embedding Python in a non-UTF-8 environment.

**WarnExperimentalFeatures**  
Logs warnings when you're using experimental GraalPy features. Good for debugging or when you're preparing code for production.



## Installing GraalPy for running Python applications

To install GraalPy for executing Python applications, run the following:

```shell
pyenv install graalpy-25.0.0
pyenv shell graalpy-25.0.0 # sets GraalPy 25.0.0 for your current shell
```

## Intalling packages with GraalPy

The best way to work with Python packages is via **virtual environments (venvs)**. Venvs are isolated persistent Python workspaces, that can be created per project. They keep dependencies separate so each project can use its own package versions without conflicts. 

Typical venv workflow is the following:

- create a venv
- activate it
- install necessary packages
- deactivate (closes the venv)

To install packages within a venv, just use GraalPy's `pip`. For example:

```shell
pip install pygal
```
In some cases, GraalPy's `pip` might choose package versions other than the latest for better compatibility.



