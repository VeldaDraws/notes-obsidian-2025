### IaC (Infrastructure as Code)
### CDN (Content Distribution Network)
- Serves cached content that is nearby.
- Distributes cached copy at Edge Locations.
- Edge Locations aren't just not read-only, you can write to them.
- TTL (Time-to-Live) defines how long until the cache expires.
- When you invalidate your cache, you are forcing it to immediately expire.
- Refreshing the cache costs money because of transfer costs to update Edge Locations.
- Origin is the address of where the original copies of your files reside.
- Distribution defines a collection 