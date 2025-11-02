---
layout: post
title: 'Making Connections'
date:   2025-10-16 19:13:23 -0400
categories: programming
---

'What is a TCP Connection?' This seemingly simple question led to a lot of digging and a lot of learning. I've danced around networking for a long time. Like many (most?) software developers, networking is sometimes a twist, often a struggle, and never the point. 

## Mystery
I don't inherently dislike networking. It's actually sort of fascinating and beautiful. But it's also mysterious. Counterintuitive. Hidden. Daunting. I received a rushed intro on TCP and other networking concepts early in my journey. TCP got brief attention - enough to grasp the basic idea - and little more. I saw a diagram that looked like this:
![tcp-diagram](tcp-diagram.jpg "tcp-diagram")
(Credit: AI Slop. Check out that spelling...!)

Since then, I have had many scenarios where this understanding wasn't enough. Troubleshooting mostly. I ran into this yet again the other day. Applications weren't talking to each other. They were on machines that were practically touching, yet might as well have been light years apart. There is a stark aloneness when you can't get machines or processes to talk. It's like a relationship that has broken down, or an argument that has finally gone too far. My frustration trumped my anxiety and I started searching for answers.

## So really, what is it?
So what *is* a TCP connection? I know how they're setup. I know why they are used. I (roughly) know what they can do when packets are dropped. But what is it? On re-researching this, I felt validated at the fact that nearly every search result is about how TCP connections are *created.* A worthy topic, but not the only one that matters. It's as if someone from another planet asked what a car is, and the answer is a deep dive on assembly lines and principles of manufacturing.

So before It's important to thoroughly understand the *thing* itself first before jumping into other questions. What is it? What is it made of? How is it represented? What does it look like? Why does it exist? I didn't have solid answers to these questions, other than a high-level explanation that is usually offered for the 'why.'

A TCP connection isn't much of a *thing* at all. It's a data structure generated independently by the server and the client based on shared information. It's the remaining artifact of the TCP handshake process, and updated independently on both sides of the transaction as new information comes in. The closest thing to a *thing* is the TCP control block (TCB) - a small piece of information stored in the kernel of the client and server that keeps a record of this. It keeps a record of connection status, sequence numbers, addresses/ports, timers, and other information related to the communication.

So it's a data structure. Stored in memory. That's not weird. Half of what we do is dealing with imaginary (or at least volatile *things*.) But for one, the TCP connection is share data that is never shared between client and server - just imputed through a shared process. That seems unusual. Especially when the thing being managed is literally a communication channel. (On further reflection - is this bad? Data redundancy is generally bad. Do the server and client ever get out of sync? Probably. Has anyone ever explored shared client-server state for connections, or other networking processes? Maybe?)

Next, I asked how I can actually look at the connections on my machine. The answer? `netstat` This was surprising. I've used this command many times. It never occurred to me that I was looking at a list of TCP connections on my machine. Wait, hang on. Are these connections or sockets? What is a socket? We jumped from connection to socket...

## Socket to me
Ok, a socket appears to be a generic *interface* for communication between two processes. Sockets are associated with a protocol+address+port - just like a connection. So a socket is conceptually at the same level as a connection. It bridges data from applications/processes to network communications and vice-versa. A connection is information stored on the kernel about communication with a remote host. A socket is a local file descriptor that points at that connection

## Show me
Ok. So then *netstat* is showing me the connections currently stored on my machine:

```
❯ netstat
Active Internet connections
Proto Recv-Q Send-Q  Local Address          Foreign Address        (state)
tcp4       0      0  10.226.245.157.60596   20.189.173.17.https    ESTABLISHED
tcp4       0      0  10.226.245.157.60520   ec2-54-189-176-1.https ESTABLISHED
tcp4       0      0  10.226.245.157.60357   ec2-44-240-41-36.https ESTABLISHED
tcp4       0      0  10.226.245.157.60282   ord38s33-in-f10..https ESTABLISHED
```


I see a column for the protocol. Clear enough. What are columns two and three? Recv-Q and Send-Q are apparently buffers, showing data that has been received or is about to be sent but hasn't made it all the way. So under normal operation these will generally be empty. Makes sense. Local address and foreign address and clear enough. State seems to make sense, intuitively, though I don't know what ESTABLISHED really means. Ok, that appears to mean that a connection is fully established between two hosts, and is ready for data transmission in either direction.

Ok, so that's all pretty clear. And not that hard. Sometimes I get to the end of these dives and I think "What was my question?" It can be hard to remember what it's like to not understand this stuff. Either way, now it's more clear. Or less unclear. I'm sure this will be helpful at some point...

