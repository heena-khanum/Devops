Setting up a gradle project, understanding build scripts(groovy and Kotlin DSL), Dependency
management and Task Automation.
(Note: better to use java 17 version)
Update java:
sudo apt update
sudo apt install openjdk-17-jdk
java --version
(Note: Once gradle installation done, go with below steps)
Create a New Gradle Project:
Run the following command to generate a new Gradle project:
gradle init
You will be prompted to select a project type:
• Application: For Java/Kotlin projects that create executables.
• Library: For reusable Java/Kotlin libraries.
• Basic: A simple Gradle setup without predefined conventions.
Example selection:
• Select "application" for a Java project.
• Choose "Java" as the language.
• Pick a build script DSL: either Groovy (default) or Kotlin.
• Set the package name (optional).
Alternatively, create a simple Java application project directly:
gradle init --type java-application
code:
build.gradle ->
plugins {
 id 'java'
 id 'application'
}
group = 'com.example'
version = '1.0.0'
java {
 sourceCompatibility = JavaVersion.VERSION_17
 targetCompatibility = JavaVersion.VERSION_17
}
application {
 mainClass = 'com.example.Main'
}
repositories {
 mavenCentral()
}
dependencies {
 // Use latest stable JUnit for testing
 testImplementation 'org.junit.jupiter:junit-jupiter:5.9.2'
 // Example dependency: Gson for JSON parsing
 implementation 'com.google.code.gson:gson:2.10'
}
tasks.withType(JavaCompile).configureEach {
 options.encoding = 'UTF-8'
}
test {
 useJUnitPlatform()
}

gradle init
gradle build
or
gradle clean build
gradle dependencies
If Main.java doesnot exist, create it as below
mkdir -p src/main/java/com/example
vi src/main/java/com/example/Main.java
code:
package com.example;
public class Main {
 public static void main(String[] args) {
 System.out.println("Hello, Gradle!");
 }
}
save and exit then run the project(gradle run)
gradle run

Theory

Task Automation in Gradle:
Gradle tasks automate processes like compilation, testing, packaging, and deployment. You can use
built-in tasks or create custom tasks to streamline your workflow.
1. Running Built-in Tasks
Gradle provides many predefined tasks. Some common ones are:
Command Description
gradle tasks Lists available tasks.
gradle build Compiles, tests, and packages the project.
gradle clean Deletes the build/ directory.
gradle test Runs unit tests.
gradle run Runs the application (if using application plugin).
gradle dependencies Lists all dependencies.
2. Creating Custom Tasks
You can define custom tasks in build.gradle:
a) Simple Task
tasks.register('hello') {
 doLast {
 println 'Hello, Gradle!'
 }
}
Run it with:
gradle hello
b) Task with Multiple Actions
tasks.register('greet') {
 doFirst {
 println 'Starting the task...'
 }
 doLast {
 println 'Hello, World!'
 }
}
 doFirst runs before the main action.
 doLast runs after the main action.
