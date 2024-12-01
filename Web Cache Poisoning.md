## **Detecting Cached Responses**

To confirm caching behavior, inspect response headers and time differences:

- **`X-Cache: hit`** – Response served from the cache.  
- **`X-Cache: miss`** – Response fetched from the origin server and potentially cached.  
- **`X-Cache: refresh`** – Cache was outdated and revalidated.

Additionally, check `Cache-Control` headers for caching directives like `public` with a non-zero `max-age`.

---

### Web cache poisoning with an unkeyed header

Some websites use unkeyed headers to dynamically generate URLs for importing resources, such as externally hosted JavaScript files. In this case, if an attacker changes the value of the appropriate header to a domain that they control, they could potentially manipulate the URL to point to their own malicious JavaScript file instead. We can use ```X-Forwarded-For:``` header for this.

**Step**
```
  1. Add X-forwarded-For header in request.
  2. Add a arbitrary domain (example.com) and send the request.
  3. If the example.com reflected in response page, we can now place our malicious link in it.
```
The malicius link contain with js file will trigger on all users browser if the site is vulnerable to the Web Cache Poisoning.
     
---
