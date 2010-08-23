
# Connect JSON-RPC

The _jsonrpc_ middleware provides JSON-RPC 2.0 support. Below is an example exposing the _add_ and _sub_ methods:

	  var math = {
	      add: function(a, b, fn){
	          fn(null, a + b);
	      },
	      sub: function(a, b, fn){
	          fn(null, a - b);
	      }
	  };
    
	  var date = {
	      time: function(fn){
	          fn(null, new Date().toUTCString());
	      }
	  };
    
	  connect.createServer(
	      require('connect-jsonrpc')(math, date)
	  );
    
When you wish to pass an exception simply invoke `fn(err)`, or pass the error code `fn(jsonrpc.INVALID_PARAMS)`. Otherwise `fn(null, result)` will respond with the given results.

## Example Requests

Regular params:

    $ curl -H "Content-Type: application/json" -d '{ "jsonrpc": "2.0", "method": "add", "params": [1,2], "id":2 }' http://localhost:3000

Named params:

    $ curl -H "Content-Type: application/json" -d '{ "jsonrpc": "2.0", "method": "add", "params": { "b": 1, "a": 2 }, "id":2 }' http://localhost:3000

## License 

(The MIT License)

Copyright (c) 2010 Sencha Inc.

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.