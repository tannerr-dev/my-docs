# Service Worker Cache Issue

## The Problem

CSS changes weren't appearing after refresh. It seemed to require 2+ refreshes to see updates.

## Root Cause

The original fetch handler in `sw.js` had a bug:

```js
return cachedResponse || fetchPromise;
```

**Issue**: JavaScript's short-circuit evaluation. When `cachedResponse` exists:
1. Returns cached (stale) response immediately
2. `fetchPromise` runs in background and updates cache for the **next** request
3. User sees old content until they refresh again

This is why 2 refreshes were needed.

## The Fix

Implemented **stale-while-revalidate** strategy:

1. **Serve stale immediately** - return cached response to user right away
2. **Revalidate in background** - fetch fresh version from network
3. **Update cache** - store new version for next request
4. **Notify client** - postMessage to tell frontend when resources update

```js
// Serve stale immediately
return cachedResponse;

// Meanwhile, fetch fresh in background
fetch(event.request)
  .then((networkResponse) => {
    cache.put(event.request, networkResponse.clone());
    
    // Notify all clients
    self.clients.matchAll().then((clients) => {
      clients.forEach((client) => {
        client.postMessage({
          type: "CACHE_UPDATED",
          url: event.request.url,
        });
      });
    });
  });
```

## Files Changed

- `public/sw.js` - fetch handler rewritten with stale-while-revalidate
- `public/app.js` - added message listener for cache update notifications

## Client-Side Handling

Currently logs when cache updates. To show a reload banner:

```js
navigator.serviceWorker.addEventListener("message", (event) => {
  if (event.data && event.data.type === "CACHE_UPDATED") {
    // Show reload banner
  }
});
```

## Alternative Quick Fixes

During development:
- Hard refresh (Cmd+Shift+R) bypasses service worker
- Disable service worker in DevTools → Application → Service Workers
- Bump cache version number in sw.js (triggers new install/activate cycle)