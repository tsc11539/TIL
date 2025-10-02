# [URL Shortener](https://blog.algomaster.io/p/design-a-url-shortener)
A URL shortener is a Service that takes a long URL and retuens a shorter, unique alias that redirects to the original URL. 
## Database Design
### SQL vs NoSQL
To choose the right database for our needs, let's consider some factors that can affect our choice:
* We need to store billions of records.
* Most database operations are simple key-value lookups.
* Read queries are much higher than write queries.
* We don't need joins between tables.
* Database needs to be highly scalable and available.

## URL Generator Service
Here are some things to think about when picking an algorithm to shorten the URL:
* URL Length: Shorter is generally better, but it limits the number of possible distinct URLs you can generate.
* Scalability: The algorithm should work well even with billions of URLs.
* Collision Handling: The algorithm should be able to handle duplicate url generations.
### Approach 1: Hashing and Encoding
Use a hash function, such as **MD5** and **SHA-256** to generate a fixed-length hash of the original URL.

#### Why hash?
* Uniformity: URLs can be very long and unenevly distributed (some very similar, some widely different). A hash function (MD5, SHA-256, etc.) converts them into a fixed-length string and spreadis them in a huge space to decrease collision chance.
* Privacy: Hashing hides the actual structure/content of the original URL.

#### Why encode after hashing?
* It gives shorter, denser, more URL-friendly characters with the same entropy.
* Base62 = Base64 - ('+' and '\\')
    * Encoding turns bunary data into a shorter alphanumeric string using `[A-Z, a-z, 0-9]`
    * It is URL-safe and compact, which means for the same entropy, a Base62 string is about 1/3 shorter than hex.
        * Example:
            * 48 bits of entropy
                * Hex = 12 chars
                * Base62 = ~8 chars
#### It has some issues
* It can generate the same shortened url for the i