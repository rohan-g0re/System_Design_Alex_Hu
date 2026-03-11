
- What is the difference between real-time and soft real-time systems?

- Candidate: What are the supported devices? --> Interviewer: iOS devices, android devices, and laptop/desktop. Why are we asking this question? How is it going to change anything because we already have asked for the different types of notifications, then how is this device going to help us? 

- Explain what is APNS. Is it like a microservice or a service natively available on Apple devices?

- Based on the architecture, can you tell me that we are designing a notification system as a part of an application or basically an intermediary middleware application which can be used by all the other applications, something similar to a rate limiter where it is not tied to a given application? That's what I think it is, because over here I've serviced one to n, which I termed to be a microservice, a cron job, or a distributed system that triggers notification sending events. I think it can also be interpreted as different applications all together, maybe something like a banking application along with a mobile game. Anything can be part of service, but the notification in between should work the same, am I right?

- Performance bottleneck: Processing and sending notifications can be resource intensive. For example, constructing HTML pages and waiting for responses from third party services could take time. --> Why do we need to construct HTML pages? What does it have to do with a notification system?



- BOOK Excerpt --> Will recipients receive a notification exactly once? The short answer is no. Although notification is delivered exactly once most of the time, the distributed nature could result in duplicate notifications. To reduce the duplication occurrence, we introduce a dedupe mechanism and handle each failure case carefully. Here is a simple dedupe logic: When a notification event first arrives, we check if it is seen before by checking the event ID. If it is seen before, it is discarded. --> Question: over here, it is said that when the notification event first arrives, what I am referring to when we say "arrives" is when it arrives at the iOS PN or the workers or the APNs or at the client side. When do we check the event ID? That's the question.




## Functional Requirements
- should support: IOS and Android push notifications, SMS messages and emails
- Notifications are sent by applications, which are referred to as services, and there can be a number of services.


## Non-Functional Requirements
- soft real time system
- Reliability: Notifications can usually be delayed or re-ordered, but never lost.
- Scalable: PER DAY STATS --> 10 million mobile push notifications, 1 million SMS messages, and 5 million emails



## High Level Design to get a Buy In

### 1. Different types of notifications:

- ios 
    - sends requests to APNs(Apple Push Notification Service)
    - Data Format:
        - DEvice Token
        - JSON Payload 

- APNS: This is a remote service provided by Apple to propagate push notifications to iOS devices.




android 

- 