---
tags:
  - golang
  - std
---
[Original Discussion Thread](https://github.com/golang/go/discussions/54763)
[Proposal Issue](https://github.com/golang/go/issues/56345)
	[Talk on Slog from the author of the RFC](https://opensourcelive.withgoogle.com/events/go-day-2022/watch?talk=talk2)
[Approved Proposal](https://github.com/golang/proposal/blob/master/design/56345-structured-logging.md)

Checking out the `slog` package for structured logging in golang new to v1.21
[slog](https://pkg.go.dev/log/slog)

In the example in the documentation they pass `os.Stderr` to the `Handler` as the writer. Wondering how this will effect command line apps which need to typically write to stdout but then write errors to stderr

Built in handlers for text and json

`Logger.With` will allow for centrally managing fields which should be on all logs avoiding the need to repeat it all over the log statements
```go
logger2 := logger.With("url", r.URL)
```

Can use group to organize / avoid duplicate keys in large systems
```go
slog.Group("request",
    "method", r.Method,
    "url", r.URL)
```

Can help with packages that have logging with duplicates you can send a logger that will nest all under a key
```go
logger := slog.Default().With("id", systemID)
parserLogger := logger.WithGroup("parser")
parseInput(input, parserLogger)
```

The top level `Info` and other convenience methods do not allow context to be passed to them. However, there are corresponding function calls that will accept `context.Context` 
```go
slog.InfoContext(ctx, "message")
```


This is a more efficient way to log out the attributes since it doesn't support the other syntax where key and value are interleaved. Doing this allows the implementation to avoid allocations.


>[!Note]
> This will likely be another common interface to implement on foreign types to control the logging of feilds you want.
>
If a type implements the [LogValuer](https://pkg.go.dev/log/slog#LogValuer) interface, the [Value](https://pkg.go.dev/log/slog#Value) returned from its LogValue method is used for logging.

## Performance
If many log lines have a common attribute, use [Logger.With](https://pkg.go.dev/log/slog#Logger.With) to create a Logger with that attribute. The built-in handlers will format that attribute only once, at the call to [Logger.With](https://pkg.go.dev/log/slog#Logger.With). The [Handler](https://pkg.go.dev/log/slog#Handler) interface is designed to allow that optimization, and a well-written Handler should take advantage of it.

> [!Note]
> #### func (*Logger) [LogAttrs](https://cs.opensource.google/go/go/+/go1.21.6:src/log/slog/logger.go;l=162) [¶](https://pkg.go.dev/log/slog#Logger.LogAttrs)
> 
> func (l *[Logger](https://pkg.go.dev/log/slog#Logger)) LogAttrs(ctx [context](https://pkg.go.dev/context).[Context](https://pkg.go.dev/context#Context), level [Level](https://pkg.go.dev/log/slog#Level), msg [string](https://pkg.go.dev/builtin#string), attrs ...[Attr](https://pkg.go.dev/log/slog#Attr))
> 
> LogAttrs is a more efficient version of [Logger.Log](https://pkg.go.dev/log/slog#Logger.Log) that accepts only Attrs.

The arguments to a log call are always evaluated, even if the log event is discarded. If possible, defer computation so that it happens only if the value is actually logged. For example, consider the call
```go
slog.Info("starting request", "url", r.URL.String())  // may compute String unnecessarily
```

The URL.String method will be called even if the logger discards Info-level events. Instead, pass the URL directly:
```go
slog.Info("starting request", "url", &r.URL) // calls URL.String only if needed
```

You can also use the [LogValuer](https://pkg.go.dev/log/slog#LogValuer) interface to avoid unnecessary work in disabled log calls. Say you need to log some expensive value:
```go
slog.Debug("frobbing", "value", computeExpensiveValue(arg))
```
Even if this line is disabled, computeExpensiveValue will be called. To avoid that, define a type implementing LogValuer:
```go
type expensive struct { arg int }

func (e expensive) LogValue() slog.Value {
    return slog.AnyValue(computeExpensiveValue(e.arg))
}
```
