Java 11 enhancements and features:
--
### Some of the developer visible features: 

Elaborated Informations [Click Here](https://gunnarmorling.github.io/jdk-api-diff/jdk10-jdk11-api-diff.html)

JDK11 has witnessed many new feature compared to the earlier versions of the JDK certainly at the JVM level
 .
 
 There is one small change to the language syntax, a fair number of new APIs, and the ability to run single-file applications without the need to use the compiler. Also, the removal of the java.se.ee aggregator module is now visible, which may impact migrating an existing application to JDK 11.
 
 - JEP (JDK enhancement Proposal) 323 : 
 
 _Avoiding usage of explicit type and introducing "var" ._
 
 ````
list.stream()

    .map((var s) -> s.toLowerCase())

    .collect(Collectors.toList());
````
 Of course as a Java developer we can argue that there is no point in declaring the variable type (in this case) and can 
 extend the lambda usage as follows:
  ````
list.stream()

     .map(s -> s.toLowerCase())

     .collect(Collectors.toList());
````

But what if we have to add annotation before the variable (we have to Explicitly give variable name) to avoid that var makes things more smooth.

````
list.stream()

      .map((@Notnull var s) -> s.toLowerCase())

      .collect(Collectors.toList());
````

  

- JEP 330: Launch Single-File Source-Code Programs:

In earlier versions of the JDKs the java source file must be first compiled javac then execute it using java "classpath" "soucefile.java" "Parameter".
But in JDK 11 this is done by one single command (compile + execute) :

Earlier:

````
javac -classpath /home/foo/java Hello.java

java -classpath /home/foo/java Hello Bonjour
````

JDK11 :

 ````
java -classpath /home/foo/java Hello.java Bonjour
````

- JEP 321: HTTP Client (Standard) :

One of the amazing feature about JDK 11 is that we can have standard HTTP protocols which can be imported using the new package 
called **java.net.http.** The main types defined are:
  
  - HttpClient 
  - HttpRequest
  - HttpResponse
  - WebSocket
  
  The API can be used synchronously or asynchronously. The asynchronous mode makes use of CompletableFutures and CompletionStages.
  
  