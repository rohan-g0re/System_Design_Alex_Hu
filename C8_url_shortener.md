## Questions

- how does base62 encoding reallly work - Didn't quite understand it.

- Difference between Redis and Memcache

- What is indexing really, and how does indexing help in faster queries? Is the index stored in memory? Also, what is the difference between indexing and sharding?

- What is read-through when referred to cache?

- In one of the articles, the author said that instead of Redis, we can also use CDN and cache it over there. But weren't CDNs only able to store static data like static frontend files? How can we store this, which is basically a map, right? A map of long URL and short URL. How can we store this on CDN? What does CDN really support?

- It also said about keeping a counter, and as our write services will be distributed, we need a global counter now so that all the write services are in sync with what the current count is. For that, the article said that the global counter can be in Redis HashTable. I thought we can just have data over there and not really programmatic, but then they also said that Redis has a function called INCR (all caps) which helps in incrementing. What really does Redis give us? What all does it provide us?

## Functional and Non-Functional Requirements

1. (f1) URL shortening: Given a long URL, return a much shorter URL.
2. (f2) URL redirecting: Given a short URL, redirect to the original long URL.
3. (f3) High availability, scalability, and fault tolerance considerations.
4. (f4) shortened URLs cannot be updated or deleted.

## High Level Design

- **301 Redirect:** Indicates that the requested URL has been **permanently** moved to a new location (the long URL). --> Browsers cache the redirect, so future requests **go directly to the long URL without contacting the URL shortening service**.
    - Advantages:
        - Reduces load on the tinyurl service.
        - Maintains SEO quality by avoiding redirects.
######

- **302 Redirect:** Indicates a **temporary** move to the long URL. --> Browsers do not cache the redirect, so **every request for the short URL is sent to the URL shortening service first**.
  - Advantages:
    - Useful if we want analytics of click rate and source of click.
    - Can be used when the original URL may change again in the future.