# Assignment 1 — Java Setup: Concepts Cheat Sheet

This README covers the "Learn first" section. The tasks themselves you do by hand.

---

## 1. JDK vs JRE vs JVM

```
JDK  (Java Development Kit)   = JRE + developer tools (javac, jar, jshell, javadoc...)
 └─ JRE (Java Runtime Env.)   = JVM + standard class libraries (java.lang, java.util...)
     └─ JVM (Java Virtual Machine) = the engine that runs bytecode
```

- **JVM**: Executes compiled `.class` files (bytecode). It's platform-specific (a Windows JVM, a Linux JVM), which is why the same bytecode runs anywhere ("write once, run anywhere").
- **JRE**: What you need to *run* Java programs. Since Java 11 it's no longer shipped separately by most vendors.
- **JDK**: What you need to *write and build* Java. It includes `javac` (compiler: `.java` → `.class`) and `java` (launcher that starts the JVM).

Flow: `Main.java` --`javac`--> `Main.class` (bytecode) --`java`--> JVM executes it.

Also know: **LTS** releases (8, 11, 17, 21, 25) get long-term support. This course uses **JDK 21**. Distributions (Temurin/Adoptium, Oracle, Microsoft, Corretto) are builds of the same OpenJDK source.

`JAVA_HOME` is an environment variable pointing at the JDK folder; Maven and IDEs use it to find Java.

---

## 2. Maven

Maven is a **build and dependency management tool**. You describe your project in `pom.xml` and Maven handles compiling, testing, packaging, and downloading libraries.

### Standard layout (convention over configuration)

```
my-project/
├── pom.xml                  <- project definition
└── src/
    ├── main/
    │   ├── java/            <- production code (com/example/Main.java)
    │   └── resources/       <- config files, etc.
    └── test/
        ├── java/            <- test code
        └── resources/
```
Build output goes to `target/`.

### pom.xml (Project Object Model)

Key parts:
- **Coordinates**: `groupId` (your org/namespace, e.g. `com.yourname`), `artifactId` (project name), `version` (e.g. `1.0-SNAPSHOT`). Together they uniquely identify the artifact.
- **`<properties>`**: e.g. the Java version (`maven.compiler.release` = 21).
- **`<dependencies>`**: libraries to download from Maven Central.
- **`<build><plugins>`**: extra build behaviour (e.g. making a runnable jar).

### Lifecycle commands

| Command | What it does |
|---|---|
| `mvn compile` | Compiles `src/main/java` into `target/classes` |
| `mvn test` | Compiles and runs tests in `src/test/java` |
| `mvn package` | Compile + test + bundle into a `.jar` in `target/` |
| `mvn clean` | Deletes `target/` |
| `mvn install` | Package + copy jar to your local `~/.m2` repository |

Phases are cumulative: `package` runs `compile` and `test` first.

Dependencies are cached in `~/.m2/repository` (on Windows: `C:\Users\<you>\.m2`).

---

## 3. Git basics

Git tracks versions of your files. Three areas: **working directory** → (`add`) → **staging area** → (`commit`) → **local repository** → (`push`) → **remote** (GitHub).

| Command | Purpose |
|---|---|
| `git init` | Turn the current folder into a repo |
| `git status` | See what changed / is staged |
| `git add <file>` / `git add .` | Stage changes |
| `git commit -m "message"` | Save a snapshot of staged changes |
| `git remote add origin <url>` | Link your local repo to a GitHub repo |
| `git push -u origin main` | Upload commits (`-u` sets the default upstream) |
| `git log --oneline` | View history |

Tips:
- Commit small and often, with meaningful messages.
- Add a `.gitignore` so you don't commit `target/`, `.idea/`, etc.
- One-time config: `git config --global user.name "..."` and `git config --global user.email "..."`.

---

# Tasks — Step-by-step (you do these)

## Current machine status (checked)

| Tool | Status |
|---|---|
| JDK | **17.0.15 (Temurin)** installed — but the assignment needs **21** |
| Maven | **Not installed** (`mvn` not recognized) |
| Git | 2.49.0 installed |
| `JAVA_HOME` | Not set |

## Task 1 — Install and verify

1. **Install JDK 21** (Temurin): download the Windows x64 `.msi` from https://adoptium.net and run it. In the installer, enable **"Set JAVA_HOME variable"** and **"Add to PATH"**. It can coexist with your JDK 17.
2. **Install Maven**: download the binary zip from https://maven.apache.org/download.cgi, extract to e.g. `C:\tools\apache-maven-3.9.x`. Then add `C:\tools\apache-maven-3.9.x\bin` to your PATH (Start → "Edit the system environment variables" → Environment Variables → Path → New). Alternative: `winget install Apache.Maven`.
3. **IDE**: install IntelliJ IDEA Community or VS Code + "Extension Pack for Java".
4. **Git**: already installed.
5. **Open a NEW terminal** (PATH changes only apply to new windows) and run:
   ```
   java -version
   mvn -v
   git --version
   ```
   `java -version` must say 21. If it still says 17, move the JDK 21 `bin` folder above JDK 17 in PATH. `mvn -v` also prints which Java it uses; check it shows 21 (if not, check `JAVA_HOME`).
6. **Evidence**: screenshot those three outputs.

## Task 2 — First Maven project

1. Generate a project:
   ```
   mvn archetype:generate -DgroupId=com.yourname -DartifactId=hello-maven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   (Or create the folders and `pom.xml` by hand — good for learning the layout.)
2. In `pom.xml`, set the Java version:
   ```xml
   <properties>
     <maven.compiler.release>21</maven.compiler.release>
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   ```
3. Make sure `src/main/java/com/yourname/Main.java` exists (rename the generated `App` if needed) and prints a message:
   ```java
   package com.yourname;

   public class Main {
       public static void main(String[] args) {
           System.out.println("Hello, Maven!");
       }
   }
   ```
4. Build: `cd hello-maven` then `mvn package`. Look for `BUILD SUCCESS`.
5. Run it:
   ```
   java -cp target/classes com.yourname.Main
   ```
   (Running the jar with `java -jar` needs a `Main-Class` manifest entry via `maven-jar-plugin` — a nice stretch goal.)
6. **Evidence**: screenshot `BUILD SUCCESS` and the program output.

## Git (also part of Day 1 goals)

1. `cd hello-maven`, `git init`
2. Create `.gitignore` containing `target/`
3. `git add .` then `git commit -m "Initial Maven project"`
4. Create an empty repo on GitHub, then `git remote add origin <url>`, `git branch -M main`, `git push -u origin main`

## Common problems

- **`mvn` not recognized**: PATH not updated or terminal not restarted.
- **"No compiler is provided" / wrong Java version**: `JAVA_HOME` points to a JRE or JDK 17; set it to the JDK 21 folder.
- **"release version 21 not supported"**: Maven is running on Java 17; fix `JAVA_HOME`.
