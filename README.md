# codenarc-error

## Current analysis
I've built with Java11 , Java 13, and Java 17 with the same results, so it is
either something specific I am doing, or a specific rule that I am attempting
to utilize.  I thought I had it working for groovy 3.0.9 code, but I seem to
be able to produce the same error regardless whenever I use certain
annotations.

I've also tried Gradle 6.9.2 up to 7.4.1 with the same results.

I now think it's how I'm building up the compilationClasspath or it's
specific to some ruleset that I've enabled.  I've included the CodeNarcRules.groovy
file that I'm using.

### Steps to reproduce original error
```shell
gradlew clean check
```

```
java.lang.ClassCastException: class groovy.transform.AnnotationCollectorMode cannot be cast to class groovy.transform.AnnotationCollectorMode (groovy.transform.AnnotationCollectorMode is in unnamed module of loader java.net.URLClassLoader @77b5d35c; groovy.transform.AnnotationCollectorMode is in unnamed module of loader org.gradle.internal.classloader.VisitableURLClassLoader @2def9ecd)
```

Without setting the compilationClasspath at all, just about everything triggers
an unable to resolve class error.

### Shows that explicitly setting something for the compilationClasspath is necessary
```shell
gradlew clean check -PdisableCompilationClasspath
```

```
None: 1: unable to resolve class groovy.transform.Immutable
 @ line 1, column 1.
   import groovy.transform.Immutable
   ^

None: 3: unable to resolve class groovy.transform.Immutable for annotation
 @ line 3, column 1.
   @Immutable
```