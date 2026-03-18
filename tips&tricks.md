# Back of the hand estimations

1. AWS t3 medium can support 1,000 qps.
2. Seconds in a day ≈ 10^5.




# Status Codes
**200** OK: fetched link metadata  
**201** Created: created a new short link  
**301** Moved Permanently: cache-friendly redirect  
**302** Found: redirect but keep coming back (good for analytics control)  
**400** Bad Request: invalid URL, missing fields  
**401** Unauthorized / **403** Forbidden: auth issues  
**404** Not Found: code doesn’t exist  
**409** Conflict: custom alias already taken  
**429** Too Many Requests: rate-limited  
**500**/**503**: server issues


# Random Facts

1. Whenever we require an alphanumeric string, remember that we can use base 62 encoding, which allows characters from 0-9, A-Z, and a-z. This, in total, makes 62 characters. Therefore if we have a string of 7 characters we can have **62^7 = 3.5 trillion unique combinations**.

2. NoSQL databases do not provide an auto increment feature for keys.