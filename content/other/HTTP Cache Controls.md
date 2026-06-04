## Cache Controls:
max-age
no-store
no-cache
must-revalidate
public, private
immutable
stale-while-revalidate
stale-if-error

### Other
pragma - old tech
expires - old tech
vary - for cdns, for language cdns

## Heuristic caching
If-Modified-Since
ETag/If-None-Match
Cache busting


https://www.youtube.com/watch?v=Cy2ZJOBgk84&t=314s


caddyfile syntax
```
header {
        Cache-Control no-cache, no-store, must-revalidate
        Pragma no-cache
        Expires 0
}
```
