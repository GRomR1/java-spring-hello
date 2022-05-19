# java-spring-hello
An example of Java project with Spring Boot. Included:
- [actuator module](https://docs.spring.io/spring-boot/docs/2.5.0/reference/htmlsingle/#actuator)

# Requirements
- java 18 and later
- maven 3.8 and later

# Run & Test

To run the application, run the following command in a terminal:
```
$ mvn spring-boot:run
```

The output is similar to the following sample output:
```
...
[INFO] --- spring-boot-maven-plugin:2.6.7:run (default-cli) @ world ---
[INFO] Attaching agents: []

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::                (v2.6.7)
...
2022-05-18 19:59:52.378  INFO 97671 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2022-05-18 19:59:52.386  INFO 97671 --- [           main] hello.world.HelloWorldApplication        : Started HelloWorldApplication in 0.95 seconds (JVM running for 1.153)
```

Now run the service with curl, by running the following command (shown with its output):
```
$ curl localhost:8080
Hello world!%
```

Show metrics in Prometheus format:
```
$ curl localhost:8080/actuator/prometheus
# HELP jvm_memory_used_bytes The amount of used memory
# TYPE jvm_memory_used_bytes gauge
jvm_memory_used_bytes{application="java-spring-hello",area="nonheap",id="Metaspace",} 3.9847672E7
jvm_memory_used_bytes{application="java-spring-hello",area="nonheap",id="CodeCache",} 7019776.0
jvm_memory_used_bytes{application="java-spring-hello",area="heap",id="G1 Old Gen",} 1.1802624E7
jvm_memory_used_bytes{application="java-spring-hello",area="heap",id="G1 Survivor Space",} 3673368.0
jvm_memory_used_bytes{application="java-spring-hello",area="nonheap",id="Compressed Class Space",} 5112272.0
jvm_memory_used_bytes{application="java-spring-hello",area="heap",id="G1 Eden Space",} 1.048576E7
...
```

## Docker

### Build
Build container from [Dockerfile](Dockerfile) and set the tag `java-spring-hello`.
```
docker build -t java-spring-hello .
```

### Run
Use `java-spring-hello` image to start a container named java-spring-hello and map `8080` port inside the container to the `8080` port on my host machine.
```
docker run -p 8080:8080 --rm --name=java-spring-hello java-spring-hello
```

Test in an other terminal window
```
$ curl localhost:8080
Hello world!%
```