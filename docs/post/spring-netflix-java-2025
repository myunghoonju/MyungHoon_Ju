#### Spring framework 7.x & boot 4: November 2025
```text
Related with java
    6.x 
    - jdk 17+
    - jakarta EE 9 / 10
    - custom nullability declarations
    - virtual threads on jdk 21(LTS)*
    
    7.x 
    - jdk 17+
    - jakarta EE 11
    - JSpecify nullability
    - virtual threads on jdk 25(LTS)*
    
    * virtual thread
    in jdk 21
    revised in jdk 24 
    recommend to use jdk 25 from jdk 17, if major spring upgrade needed
    
```

```text
Third-party integration
    - netty 4.2
    - jackson 3.0
    - junit 6.0
```

```text
JSpecify
    - type-use annotations
    - @NullMarked packages with @Nullable parameters / fields / etc.
```

#### Netflix java in 2025
```text
where
  streaming, studio app
  HTTP, 
  graphQL, 
  DGS
  grpc(within internal java services)
how
  version 8 to 17
    all springboot
    for a new GC use 21, 23
    G1 -> 20% less cpu usage for doing GC
    23 uses ZGC(generational is good)
  virtual threads jdk 23
    - no specific logic needed?(parallel, completableFuture etc..,)
    - make it default
    - rx is complicated(e.g., webClient)
    - but thread pinning problem -> fixed in jdk 24
  springboot
    sec
    service mesh
    observability(micrometer)
    remote dynamic configuration
  deployment
    not using native images
    exploded jar with embedded tomcat
    leyden, aot
    no way of going back to webflx
  gradle transform(migration tool)
  DGS
    fully integrated with spring for graphQL
  IPC mechanism
    graphGL - flexible schema, think data
    gRPC - server to server calls, think method
    REST - nope
```
#### Where is the Java language going?
```text
  java is going more expressive path
  records & sealed classes
   - records: syntax related, emphasizing the statement
   - sealed classes(discriminated unions) are sometimes called sum types, coz the values of a sealed class is the sum (union) of their permitted subtypes.
      e.g., a shape is a circle or a rectangle
   - algebraic data types(ADTs) is powerful tool for data description
```
