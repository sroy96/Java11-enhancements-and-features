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
  
  
  - NEW APIs:

Lot of new API are added in JDK11 including HTTP client module which is now a part of the standard , as well as inclusion of the Flight recorder,
What I list here are all the new methods other than those in the java.net.http and jdk.jfr modules. I’ve also not listed the new methods and classes in the java.security modules, which are pretty specific to the changes of JEP 324 and JEP 329.

Let's start with one of the most talked and discussed enhancement JDK 11 has provided i.e in java.lang.String package :
 - java.lang.String :
 ````
1. boolean isBlank(): Returns true if the string is empty or contains only white space codepoints, otherwise false.

2. Stream lines(): Returns a stream of lines extracted from this string, separated by line terminators.

 3. String repeat(int): Returns a string whose value is the concatenation of this string repeated count times.

 4. String strip(): Returns a string whose value is this string, with all leading and trailing whitespace removed.

5.  String stripLeading(): Returns a string whose value is this string, with all leading whitespace removed.

 6. String stripTrainling(): Returns a string whose value is this string, with all trailing whitespace removed.
````
- java.lang.StringBuffer
- java.lang.StringBuilder
````

Both these classes have a new compareTo() method that takes a  StringBuffer/StringBuilder and returns an int. The lexographical comparison method is the same as the new compareTo() method of the CharSequence.
````


- java.lang.Thread :
````
No additional methods but the destroy() and stop(Throwable) methods have been removed. The stop()method that takes no arguments is still present. This might present a compatibility issue.
````
- java.io.ByteArrayOutputStream :
````
     void writeBytes(byte[]): Write all the bytes of the parameter to the output stream.
````
- java.io.FileReader:
````
Four new constructors that allow a Charset to be specified.
````
- java.io.InputStream:
````
     io.InputStream nullInputStream(): Returns an InputStream that reads no bytes. When you first look at this method (and the ones in OutputStream, Reader, and Writer), you wonder what use they are. You can think of them like /dev/null for throwing away an output you don’t need or providing an input that always returns zero bytes.
````
- java.io.OutputStream:
````
     io.OutputStream nullOutputStream() 
````
- java.io.Reader:
````
     io.Reader nullReader() 
````
- java.io.Writer:
````
     io.Writer nullWriter() 
````
- java.lang.Character :
````
     String toString(int): This is an overloaded form of the existing method but takes an int instead of a char. The int is a Unicode code point.
````
- java.lang.CharSequence :
````
    int compare( CharSequence , CharSequence): Compares two CharSequence instances lexicographically. Returns a negative value, zero, or a positive value if the first sequence is lexicographically less than, equal to, or greater than the second, respectively.
````

- java.nio.ByteBuffer
-  java.nio.CharBuffer
- java.nio.DoubleBuffer
- java.nio.FloatBuffer
- java.nio.LongBuffer
- java.nio.ShortBuffer

All these classes now have a mismatch() method that finds and returns the relative index of the first mismatch between this buffer and a given buffer.

- java.nio.channels.SelectionKey

````
int interestOpsAnd(int): Atomically sets this key’s interest set to the bitwise intersection (“and”) of the existing interest set and the given value.
 
int interestOpsOr(int): Atomically sets this key’s interest set to the bitwise union (“or”) of the existing interest set and the given value.
````

- java.nio.channels.Selector :

````
int select(java.util.function.Consumer, long): Selects and performs an action on the keys whose corresponding channels are ready for I/O operations. The long parameter is a timeout.

int select(java.util.function.Consumer): As above, except without the timeout.

int selectNow(java.util.function.Consumer): As above, except it is non-blocking.
````

java.nio.file.Files :

````
1. String readString(Path): Reads all content from a file into a string, decoding from bytes to characters using the UTF-8 charset.
 
2. String readString(Path, Charset): As above, except decoding from bytes to characters using the specified Charset.

3. Path writeString(Path, CharSequence, java.nio.file. OpenOption[]:Write a CharSequence to a file. Characters are encoded into bytes using the UTF-8 charset.

4. PathwriteString(Path, CharSequence, java.nio.file. Charset, OpenOption[]: As above, except Characters are encoded into bytes using the specified Charset.
````

- java.util.concurrent.PriorityBlockingQueue


- java.util.PriorityQueue
````
    1. void forEach(java.util.function.Consumer): Performs the given action for each element of the Iterable until all elements have been processed or the action throws an exception.
    
    2. boolean removeAll(java.util.Collection): Removes all of this collection’s elements that are also contained in the specified collection (optional operation).
    
    3. boolean removeIf(java.util.function.Predicate): Removes all of the elements of this collection that satisfy the given predicate.
    
    4. boolean retainAll(java.util.Collection): Retains only the elements in this collection that are contained in the specified collection (optional operation).
````
java.util.concurrent.TimeUnit

````
     long convert(java.time.Duration): Converts the given time duration to this unit.
````
java.util.function.Predicate
````
     Predicate not(Predicate). Returns a predicate that is the negation of the supplied predicate.
````
Using this you can convert this code: 

````
lines.stream()          

         .filter(str -> !str.isBlank());
````

To more simpler form :

````
lines.stream()

     .filter(Predicate.not(String::isBlank))
````

And moreover if we use static then becomes:

````
lines.stream()

          .filter(not(String::isBlank))
````

- java.util.Optional
- java.util.OptionalInt
- java.util.OptionalDouble
- java.util.OptionalLong
````
     boolean isEmpty():If a value is not present, it returns true, otherwise it is false.
````

- java.util.regex.Pattern
````
     Predicate asMatchPredicate(): I think this could be a hidden gem in the new JDK 11 APIs. It creates a predicate that tests if this pattern matches a given input string.
````

- java.util.zip.Deflater
````
    1. int deflate(ByteBuffer): Compresses the input data and fills the specified buffer with compressed data.
    
    2. int deflate(ByteBuffer, int): Compresses the input data and fills the specified buffer with compressed data. Returns the actual number of bytes of data compressed.

    3.  void setDictionary(ByteBuffer): Sets the preset dictionary for compression to the bytes in the given buffer. This is an overloaded form of an existing method that can now accept a ByteBuffer, rather than a byte array.

    4.  void setInput(ByteBuffer): Sets input data for compression. Also an overloaded form of an existing method.
````
- java.util.zip.Inflater
````
    1. int inflate(ByteBuffer): Uncompresses bytes into the specified buffer. Returns the actual number of bytes uncompressed.
    
    2. void setDictionary(ByteBuffer): Sets the preset dictionary to the bytes in the given buffer. An overloaded form of an existing method.

    3. void setInput(ByteBuffer): Sets input data for decompression. An overloaded form of an existing method.
````
- javax.print.attribute.standard.DialogOwner
````
    This is a new class in JDK 11 and is an attribute class used to support requesting a print or page setup dialog be kept displayed on top of all windows or some specific window.
````
-javax.swing.DefaultComboBoxModel

- javax.swing.DefaultListModel
````
    1. void addAll(Collection): Adds all of the elements present in the collection.
    
    2.  void addAll(int, Collection): Adds all of the elements present in the collection, starting from the specified index.
````
- javax.swing.ListSelectionModel
````
     int[] getSelectedIndices(): Returns an array of all of the selected indices in the selection model in increasing order.
    
     int getSelectedItemsCount(): Returns the number of selected items.
````


- jdk.jshell.EvalException
````
     jshell.JShellException getCause(): Returns the wrapped cause of the throwable in the executing client represented by this EvalException or null if the cause is non-existent or unknown.
````