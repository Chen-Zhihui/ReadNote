# 服务器发送事件

The EventSource interface is web content's interface to server-sent events. An EventSource instance opens a persistent connection to an HTTP server, which sends events in text/event-stream format. The connection remains open until closed by calling EventSource.close().

[IE 支持](https://github.com/EventSource/eventsource)
[结合Webflux](https://www.ibm.com/developerworks/cn/java/spring5-webflux-reactive/index.html)


与WebSocket相比，只是在协议上较为简单，从开发库的成熟度上看，该技术并无优势