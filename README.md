# TIL
Sharing my daily TILs

## 2025/10/01
### [URL Shortener](https://blog.algomaster.io/p/design-a-url-shortener)
A URL shortener is a Service that takes a long URL and retuens a shorter, unique alias that redirects to the original URL. 
* Base62 = Base64 - ('+' and '\\')
    * Encoding turns bunary data into a shorter alphanumeric string using `[A-Z, a-z, 0-9]`
    * It is URL-safe and compact, which means for the same entropy as 