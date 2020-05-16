
# C++

## gSOAP
[The gSOAP Toolkit for SOAP and REST Web Services and XML-Based Applications](https://www.cs.fsu.edu/~engelen/soap.html)

## Apache Axis
[Apache Axis2/C](http://axis.apache.org/axis2/c/core/)

## [KD-SOAP](https://www.kdab.com/development-resources/qt-tools/kd-soap/)
Qt客户端

# JS

## jQuery.soap()

[jQuery.soap](https://github.com/doedje/jquery.soap)

```js
$.soap({
	url: 'http://my.server.com/soapservices/',
	method: 'helloWorld',

	data: {
		name: 'Remy Blom',
		msg: 'Hi!'
	}
}).done(function(data, textStatus, jqXHR) {
	// do stuff on success here...
}).fail(function(jqXHR, textStatus, errorThrown) {
	// do stuff on error here...
})
```


## Node.js Soap server and client

[soap server and client](https://github.com/vpulim/node-soap)

```js
//client
  var soap = require('soap');
  var url = 'http://example.com/wsdl?wsdl';
  var args = {name: 'value'};
  soap.createClientAsync(url).then((client) => {
    return client.MyFunctionAsync(args);
  }).then((result) => {
    console.log(result);
  });
```

### server

```js
var xml = require('fs').readFileSync('myservice.wsdl', 'utf8');

soap.listen(server, {
    // Server options.
    path: '/wsdl',
    services: myService,
    xml: xml,

    // WSDL options.
    attributesKey: 'theAttrs',
    valueKey: 'theVal',
    xmlKey: 'theXml'
});
```