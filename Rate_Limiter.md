# Rate Limiter  
*Http Error Code : 429*  
### User Case  
- D-Dos Attack Protection  
- Bot or user or system misbehaviour {looping} protection  
- User usage tier limiter  
- Limit Api operation {for paid api }  
- Limit Resource heavy operation {Heavy DB joins}  
## Methods  
### Client Side  
#### Explanation  
-  Track request count of client side and pause request if exceed threshold.
#### Pros  
-  Faster (No Api Call)
-  Cheaper (No Api costing or server costing)
#### Cons  
-  Unreliable and Easy to bypass
-  Harder to sync if customer have multiple instance

### Server Side (Api gateway)  
#### Explanation  
-  This happens before the request even touches your application code. It usually lives in your Reverse Proxy (Nginx) or API Gateway (Kong, AWS API Gateway).
-  The web server tracks IP addresses {or any other details present in request} in its own memory zone and drops "429 Too Many Requests" immediately.
#### Pros  
-  Don't impact or use application resources
#### Cons  
-  Can't Limit based on User tier
-  Request count can be only based on request

### Server Side (Middleware)  
#### Explanation  
-  It sits between the incoming request and your route handler.
-  Usually uses cache like redis
#### Pros  
-  Finner Business logic for rate limiter
#### Cons  
- Consume Application resource (So massive D-Dos attack still works) 

## Algorithms
