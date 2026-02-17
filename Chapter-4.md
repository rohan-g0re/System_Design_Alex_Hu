# Step 1: Ask Questions

The first question is, "How is preventing a resource starvation a benefit of having an API rate limiter? Because we are not really preventing resource starvation. We are preventing resource exhaustion." That's the first question.

Question number two. We spoke about server-side API rate limiter, but what is and how do we implement a client-side rate limiter? 

Question number three. What do you mean by throttle and throttling? Is it a positive or negative thing? Because here the question that the candidate asks is, "Does the rate limiter throttle API requests based on IPA, user ID, or other properties?" --> Also, what does it really mean about it should be flexible to support different sets of throttle rules? Also, what are throttle rules?

Question number four. What are the differences between having rate limiter as a separate service or it implemented in application code? What are the fundamental differences that both of these will cause? Isn't implying or implementing in application code easier so that the distributed environment basically directly has that feature inherently?

This is question number five. Based on all the conversation, how did we reach the consensus that we have to accurately limit excessive requests? And how did we know that we are asking for low latency? Tell me that. Or is it supposed to be understood directly? Also, how did we know that we are supposed to use digital memory?

Question number 6. Explain to me everything about these terms: SSL termination, authentication, IP, white listing, servicing static content, etc. Because the sentence we have over here is, "API gateway is fully managed service that supports rate limiting, SSL termination, authentication, IP white listing, servicing static content, etc."

Question number seven: We said that we need to inform the users who are throttled. Why was this question asked? What part does its answer play in the actual system design?



### Token bucket algorithm

Question number 8: I don't really understand what the refill has to do with all the rate limiting part, but now when I see the example, are the refill tokens just a counter that gets decremented in a given time and are reset after a given time interval? For example, just tell me if I'm correct that if the bucket quantities for and the refill rate is 4 per minute, it basically is saying that each request will require one token to be fulfilled, and when it fulfils a request, will decrement the number of tokens that is a token got utilized which also means that we can only do four requests in a minute. Am I doing right?

Question number 9. They're saying that we can have multiple buckets, but they're saying the different buckets are for different API endpoints, which makes sense because not all the endpoints will have the same number of incoming requests and the overall capacity for every endpoint will be different. But tell me, is there really a need or also tell me if it is actually possible that we would need multiple buckets for a single API endpoint? I think that if we have two buckets with whatever 10 tokens per second of the rate, it basically means that we have one bucket with 20 tokens per second. So I don't really think that there is a difference of having multiple buckets or different types of buckets for a single API endpoint. Am I right?


Question number 10: I still don't understand what is the meaning of this? What is this process? Just tell me what is this process so that I can understand what is throttling a request based on IP address. Tell me that so that I can understand why are we requiring a bucket for it. --> context sentence: "• If we need to throttle requests based on IP addresses, each IP address requires a bucket."


Question number 11. Can we have a hierarchy of buckets? As you can see over here, we have a global bucket of 10,000 requests. But again, we have different types of requests for different API points, so can we have a second level of requests? First, as we first request goes to the 10,000 level bucket (which is basically the level one bucket). Then, if that is approved, it goes to the second layer where we are actually doing a call (which might be making a POST) and it goes to that specific bucket. Is it possible? --> Sentence context from book: "• If the system allows a maximum of 10,000 requests per second, it makes sense to have a
global bucket shared by all requests."

IS THIS RIGHT: Bucket capacity determines bust size and data capacity determines sustained throughput? explain

### Leaking bucket algorithm

Give me a simple C++ code that tells me how the leaky bucket algorithm works.



### System Design

1. What is an edge server, and how is it different from a simple server? How does edge server reduce latency? Where are edge servers located or typically located or placed?
2. For distributed systems, they have suggested that we use an eventual consistency model. What is it and are there any popular examples? How does it really work? Just give me an overview of the working.
3. 