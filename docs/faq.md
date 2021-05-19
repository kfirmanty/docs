# Frequently Asked Questions

We're putting together answers to all your burning questions.

Check back in very soon, or ask us directly through our [support channels](support.md).

### Some of my runnables have problem resolving hostnames of other runnables
If some of the runnables crash with errors like `Error connecting to Redis on templates-stack-redis-redis:6379 (SocketError)` and you are using `alpine` based image then you have probably encountered a bug with `alpine` hostname resolving.

How to verify it:
```clojure
monk shell problematic-runnable-name
ping templates-stack-redis-redis
```

If the ping works correctly then it might be problem with your service. If on the other hand the host is not reachable when pinging it might be problem related to some `alpine` versions. It can be mitigated by adding `.monk` at the end of the host. For example `templates-stack-redis-redis.monk`. After that you can verify that host is working by loading template again and updating your runnable. In `monk` templates the `.monk` suffix can be added using `arrowscript`:

```clojure
<- get-hostname("stack/redis", "redis") ".monk" concat
```
