# Cogvio Checkstyle Config

[![Maven Central](https://img.shields.io/maven-central/v/com.cogvio/checkstyle-config.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.cogvio%22%20checkstyle-config)

[Checkstyle](http://checkstyle.sourceforge.net/) plugin configuration shared among Cogvio projects.

## Usage

setup the plugin in the `<build><plugins>` section

```
<plugin>
 <artifactId>maven-checkstyle-plugin</artifactId>
 <version>${maven-checkstyle-plugin.version}</version>
 <dependencies>
   <dependency>
     <groupId>com.cogvio</groupId>
     <artifactId>checkstyle-config</artifactId>
     <version>${cogvio-checkstyle.version}</version>
   </dependency>
   <dependency>
     <groupId>com.puppycrawl.tools</groupId>
     <artifactId>checkstyle</artifactId>
     <version>${checkstyle.version}</version>
   </dependency>
 </dependencies>
 <configuration>
   <configLocation>cogvio_checkstyle.xml</configLocation>
   <encoding>UTF-8</encoding>
   <consoleOutput>true</consoleOutput>
   <failOnViolation>true</failOnViolation>
   <violationSeverity>warning</violationSeverity>
   <includeTestSourceDirectory>true</includeTestSourceDirectory>
 </configuration>
 <executions>
   <execution>
     <id>validate</id>
     <phase>validate</phase>
     <goals>
       <goal>check</goal>
     </goals>
   </execution>
 </executions>
</plugin>
```

### Suppressions

Optionally, you can create a `checkstyle_suppressions.xml` file in your classpath and it should get picked up automatically

```xml
<?xml version="1.0"?>
<!DOCTYPE suppressions PUBLIC
    "-//Puppy Crawl//DTD Suppressions 1.1//EN"
    "http://www.puppycrawl.com/dtds/suppressions_1_1.dtd">
<suppressions>
    <suppress files=".*[\\/]src[\\/]test[\\/]java[\\/].*" id="VisibilityModifierCode"/>
    <suppress files=".*[\\/]src[\\/]test[\\/]java[\\/].*" id="MagicNumberCode"/>
</suppressions>
```

or you can specify the location using `<suppressionsLocation>` in above configuration.
