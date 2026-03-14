Question: What is relaying? Because here it is said that the chat service, after receiving the message, you will find the right recipients for each message and relay the message. Is it basically sending?

Question: why are we using a key-value store for storing the chat history? Can you give me an example, because I can't imagine why we would do that?

Question: What does this mean? --> "The read to write ratio is about 1:1 for 1 on 1 chat apps."

Question: even though we have chosen a local sequence number generator for every channel, still how is it implemented? Is it implemented using auto-increment logic? Now again, I know it is not an inherent feature, but we can implement that logic in a message ID generator, or are we still using the 64-bit sequence number generator, but not for a global but a local scope?

Now, here you are seeing that we have in the present server. Every queue is called, let's say, Channel AB. We will be dealing with data packets, or whatever, basically messages, when user A changes its status, like online status. If it is changed, it will go into the Channel AB, and we will pull it as it is subscribed to the present server of Channel AB. I wanted to ask: there can be multiple users who are connected to user B. Let's say we have a user X and a user Y who is also connected to B. Will they use a different queue for B, such as Channel XB and YB, whatever it was, or is this present server channel common for user B? For example, if there is a signal, if there is a state change in user X, Y, and A, then all of these will fall into the same queue for B. This is my question. In short, I want to ask that, as for chat, we had a single queue for all the messages such that user B can get a message from user A, X, and Y, and all of them were falling into the same queue. Similarly, do we have the similar setup for a present server where all of the status signal changes from A, X, and Y will fall into the same queue, or are there different queues?

---------------

## Functional Requirements
- mobile app and web app
- 1 to 1 chat && group chat
- max group chat people = 100
- "online?" indicator
- only text messages
- encryption if possible 
- Multiple device support. The same account can be logged in to multiple accounts at the
same time.
- Push notifications

## Non-Functional Requirements
- 50 Million DAU
- max limit of message = 100,000
- **storing chat history FOREVER**


## High-level design and getting a buy-in

### Protocols:

#### 1. Time-tested HTTP protocol

#### 2. Polling

#### 3. Long Polling

#### 4. Websockets
- WebSocket connection is initiated by the client.
- It is bi-directional and persistent.
- **It starts its life as an HTTP connection and could be upgraded via some well-defined handshake to a WebSocket connection.**
- WebSocket connections generally work even if a firewall is in place.
- This is because they use port 80 or 443, which are also used by HTTP/HTTPS connections.
- Use WebSocket on the sender as well as the receiver side because it is bi-directional and does not have the limitation that HTTP had.



