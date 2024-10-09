# MapStruct - Java bean mappings, the easy way!

[![Latest Stable Version](https://img.shields.io/badge/Latest%20Stable%20Version-1.6.2-blue.svg)](https://central.sonatype.com/search?q=g:org.mapstruct%20v:1.6.2)
[![Latest Version](https://img.shields.io/maven-central/v/org.mapstruct/mapstruct-processor.svg?maxAge=3600&label=Latest%20Release)](https://central.sonatype.com/search?q=g:org.mapstruct)
[![License](https://img.shields.io/badge/License-Apache%202.0-yellowgreen.svg)](https://github.com/mapstruct/mapstruct/blob/main/LICENSE.txt)

[![Build Status](https://github.com/mapstruct/mapstruct/workflows/CI/badge.svg?branch=main)](https://github.com/mapstruct/mapstruct/actions?query=branch%3Amain+workflow%3ACI)
[![Coverage Status](https://img.shields.io/codecov/c/github/mapstruct/mapstruct.svg)](https://codecov.io/gh/mapstruct/mapstruct/tree/main)

* [What is MapStruct?](#what-is-mapstruct)
* [Requirements](#requirements)
* [Using MapStruct](#using-mapstruct)
 * [Maven](#maven)
 * [Gradle](#gradle)
* [Documentation and getting help](#documentation-and-getting-help)
* [Building from Source](#building-from-source)
* [Links](#links)
* [Licensing](#licensing)

## What is MapStruct?

* == Java [annotation processor](https://docs.oracle.com/javase/6/docs/technotes/guides/apt/index.html) 
  * goal
    * generation of mappers -- for -- Java bean classes 
      * type-safe
      * performant
  * allows
    * alternative to write mapping code by hand / can be
      * tedious
      * error-prone
  * features
    * type conversions
      * sensible defaults
      * many
  * vs mapping frameworks | runtime
    * **Fast execution**
      * Reason: 🧠use plain method invocations -- instead of -- reflection 🧠
    * **Compile-time type safety**
      * ONLY objects and attributes / mapping to each other -- can be -- mapped
    * **Self-contained code**
      * == NO runtime dependencies
    * **Clear error reports** | build time, if
      * mappings are incomplete 
        * == NOT ALL target properties -- are -- mapped
      * mappings are incorrect 
        * == can NOT find a proper mapping method or type conversion
    * **Easily debuggable mapping code**

* how does it work?
  * declare a mapper interface / will map between 2 types

    ```java
    @Mapper
    public interface CarMapper {
    
        CarMapper INSTANCE = Mappers.getMapper( CarMapper.class );
    
        @Mapping(target = "seatCount", source = "numberOfSeats")
        CarDto carToCarDto(Car car);
    }
    ```

  * once you compile it -> MapStruct -- will generate an -- implementation of this interface /
    * for mapping between source and target objects -- uses -- plain Java method invocations (NO reflection)
    * properties are mapped
      * by default, if source's property name == target's property name
      * & customized -- via -- annotations (_Example:_ `@Mapping`) 

## Requirements

* Java v1.8+

## Using MapStruct

* works -- via --
  * CL builds (plain javac, via Maven, Gradle, Ant, etc.)
    * if you do NOT use a dependency management tool -> you can obtain a [distribution bundle from | Releases](https://github.com/mapstruct/mapstruct/releases)
  * IDEs
    * Eclipse, a [dedicated plug-in is in development](https://github.com/mapstruct/mapstruct-eclipse) / provides content assist for
      * annotation attributes
      * quick fixes
    * IntelliJ, a [dedicated plug-in](https://plugins.jetbrains.com/plugin/10036-mapstruct-support)

### Maven

* add | your "pom.xml" 
  * ALL dependencies are available | Maven Central

```xml
...
<properties>
    <org.mapstruct.version>1.6.2</org.mapstruct.version>
</properties>
...
<dependencies>
    <dependency>
        <groupId>org.mapstruct</groupId>
        <artifactId>mapstruct</artifactId>
        <version>${org.mapstruct.version}</version>
    </dependency>
</dependencies>
...
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <version>3.13.0</version>
            <configuration>
                <source>17</source>
                <target>17</target>
                <annotationProcessorPaths>
                    <path>
                        <groupId>org.mapstruct</groupId>
                        <artifactId>mapstruct-processor</artifactId>
                        <version>${org.mapstruct.version}</version>
                    </path>
                </annotationProcessorPaths>
            </configuration>
        </plugin>
    </plugins>
</build>
...
```

### Gradle

* add | "build.gradle"

```groovy
plugins {
    ...
    id "com.diffplug.eclipse.apt" version "3.26.0" // Only for Eclipse
}

dependencies {
    ...
    implementation 'org.mapstruct:mapstruct:1.6.2'

    annotationProcessor 'org.mapstruct:mapstruct-processor:1.6.2'
    testAnnotationProcessor 'org.mapstruct:mapstruct-processor:1.6.2' // if you are using mapstruct in test code
}
...
```

## Documentation and getting help

* [reference documentation](https://mapstruct.org/documentation/reference-guide/)
* [Discussions](https://github.com/mapstruct/mapstruct/discussions)

## Building Mapstruct from Source

* requirements
  * Java v11+
  * Maven
* ways
  * `./mvnw clean install`
  * `./mvnw clean install -DskipDistribution=true`
    * if you want to skip the distribution module

    
## Importing into IDE

* requirements
  * enable annotation processing | IDE
    * Reason: 🧠MapStruct, to generate mapping gems for its own annotations -- uses the -- gem annotation processor 🧠

### IntelliJ 

* requirements
  * IntelliJ v2018.2.x+
    * Reason: 🧠needed support for `maven-compiler-plugin` 's `annotationProcessors` 🧠
* Enable annotation processing in IntelliJ (Build, Execution, Deployment -> Compiler -> Annotation Processors)

### Eclipse

* install [m2e_apt](https://marketplace.eclipse.org/content/m2e-apt) 

## Links

* [Homepage](https://mapstruct.org)
* [Source code](https://github.com/mapstruct/mapstruct/)
* [Downloads](https://github.com/mapstruct/mapstruct/releases)
* [Issue tracker](https://github.com/mapstruct/mapstruct/issues)
* [User group](https://groups.google.com/forum/?hl=en#!forum/mapstruct-users)
* [CI build](https://github.com/mapstruct/mapstruct/actions/)

## Licensing

MapStruct is licensed under the Apache License, Version 2.0 (the "License"); you may not use this project except in compliance with the License. You may obtain a copy of the License at https://www.apache.org/licenses/LICENSE-2.0.
