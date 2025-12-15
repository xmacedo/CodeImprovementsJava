# Annotations 

## The Baseline: Understanding What Was Slow

```shell
spring.main.log-startup-info=true
```


## Change 3: Trimming Auto-Configuration (Saved 240ms)

- To find what to exclude, we ran:


```shell
java -jar app.jar --debug
```

Look for <b>“positive matches”</b> and <b>“negative matches”</b> in the output. Everything in negative matches is wasted work.


## Change 4: AOT Compilation with GraalVM (Saved 280ms)
This is where things got interesting.

Spring Boot 3 introduced Ahead-of-Time compilation. Instead of doing reflection at startup, the framework generates optimized code at build time.

```xml
<plugin>
    <groupId>org.graalvm.buildtools</groupId>
    <artifactId>native-maven-plugin</artifactId>
</plugin>
```

Build command:
```shell
mvn -Pnative native:compile
```

The build takes 4 minutes instead of 30 seconds. But startup? 200ms.