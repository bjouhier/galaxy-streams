The `galaxy-streams` module provides a simple API to work with node.js streams. It contains wrappers for all the main streams of the node API, as well as generic `ReadableStream` and `WritableStream` wrappers.

## Readable Streams

Once you have wrapped a _readable_ stream, you can read from it with:

```
var data = yield stream.read(size);
```

The `size` parameter is optional. If you pass it and if the stream does not end prematurely, the `read` call returns a `string`/`Buffer` of exactly `size` characters / bytes. If the stream ends before `size` characters / bytes, the remaining data is returned. If you try to read past the end of the stream, `null` is returned.

Without `size` argument, `read` returns the next chunk of data available from the stream, as a `string` or `Buffer` depending on encoding. It returns `null` at the end of the stream.

Readable streams also support a synchronous `unread(data)` method, which is handy for parsers.

## Writable Streams

Writable streams are similar. Once you have wrapped a _writable_ stream, you can write to it with:

```
yield stream.write(data, encoding);
```

Encoding is optional. For a binary stream, you do not pass any `encoding` and `data` is a `Buffer`. For a character stream, you must pass an `encoding` and `data` is a `string`. 

To end a stream, just write `null` or `undefined`. For example: `yield stream.write();`. You can also end it with a synchronous `stream.end()` call.

