
# 响应式编程

## 缘起

严重的缺陷：Java 线程的实现被操作系统认定为系统进程，这使得线程的切换等价于操作系统的上下文切换，这个代价非常高。

响应式编程的好处就是执行的代码和执行的线程是分开的。因此在操作系统的层面上，上下文切换的代价比较低

## 现存问题

在与传统的企业应用集成的过程中，也出现了很多新的问题，像安全认证、事务还有链路追踪等仍然附加在当前线程里面。当你开始执行响应式编程的程序时，这种机制也无法奏效，所以需要找到一个更好的解决办法。

# libs


## [Reactor Netty](https://github.com/reactor/reactor-netty)

```java
HttpServer.create()   // Prepares an HTTP server ready for configuration
          .port(0)    // Configures the port number as zero, this will let the system pick up
                      // an ephemeral port when binding the server
          .route(routes ->
                      // The server will respond only on POST requests
                      // where the path starts with /test and then there is path parameter
                  routes.post("/test/{param}", (request, response) ->
                          response.sendString(request.receive()
                                                     .asString()
                                                     .map(s -> s + ' ' + request.param("param") + '!')
                                                     .log("http-server"))))
          .bindNow(); // Starts the server in a blocking fashion, and waits for it to finish its initialization
```

```java
HttpClient.create()             // Prepares an HTTP client ready for configuration
          .port(server.port())  // Obtains the server's port and provides it as a port to which this
                                // client should connect
          .post()               // Specifies that POST method will be used
          .uri("/test/World")   // Specifies the path
          .send(ByteBufFlux.fromString(Flux.just("Hello")))  // Sends the request body
          .responseContent()    // Receives the response body
          .aggregate()
          .asString()
          .log("http-client")
          .block();
```

## introduction
[Spring 5与Spring cloud的响应式编程之旅](https://www.jdon.com/49561)