# Decentralised Social

You are tasked to build a decentralized Twitter, BE, FE, entire stack. And you are alone, and within 4 weeks.

- Can you clearly describe the design and the whole process. Feel free to include mockup, diagrams, cryptography design and anything else that explain your ideas clearly.
- With the above process, do you think it can be done within 4 weeks? What are the tradeoffs that are made because of time factor.

# Table of Contents

1. Brief overview - List out some personal thoughts regarding the topic of decentralised social networks
2. Design process
3. Tradeoffs and Final Thoughts

# Brief Overview

### Introduction

Before embarking on the task to build a decentralised twitter/social network, I would like to first examine the case for building a decentralised social network, and understand what are some features that would make a decentralised twitter superior to that of its web2 counterpart.

By first acknowledging its strengths and weaknesses, we can subsequently strive to amplify its benefits and work around its shortcomings in order to build an end product that would entice existing users to migrate over.

Being aware of the inherent differences between the decentralised and web2 products would also allow us to take the best parts of the current implementation, while avoiding the situation where we re-invent the wheel.

### The case for decentralised social networks

I have identified 3 main benefits of social networks:

1. Owning your audience and content
   - your audience will follow you across different applications
   - Users can monetize their own contents
2. Prevents social discourse from being controlled by a small group of people - related to algorithm
3. ZK proves - ability to say and prove something anonymously

### Assumptions surrounding the task

# Design Process

## A) Functional Requirements

Identity

- Cross-platform identity
- Claiming a unique username

Tweets

- Ability to create tweets
- Ability to own your tweets
- Ability to view tweets from a certain user
- Ability to interact with tweets

Follow

- Ability to follow/subscribers to another user
- Ability to own your subsribers

Feed

- View feed according to a customised algorithm

## B) Non-functional Requirements

Behaviour of users

- In a social network, some people might end up having more followers than others. There are users who are more popular, where everybody wants to read their posts. In general, users are reading more posts than they a producing. This hints at a read-heavy system.

Availability

- Although people use social network applications for entertainment, it is still considered an essential service and should have high availability guarantees and a high level of uptime. This is achieved through replication and redundancy of data storage.

Partition Tolerance

- The system has to be able to continue processing requests even if there are network errors between subsystem, which is another guarantee given the communication over TCP.

Eventual Consistency

- Based on the CAP theorem and the above 2 requirements, we cannot guarantee a high level of consistency. However, this is not an issue because due to the nature of the home page feed feature, we do not have to show the most recent tweets as long as there is a high degree of availability. However, the system will strive to achieve eventual consistency, where users will be able to accurately query all the posts made by another user.

Data load and storage

-

## C) System Design

Application servers

- Application servers will be hosted by traditional web2 hosting solutions. These servers will be responsible for directly serving request from users and their clients.

Load balancer

- Because clients will directly communicate to these application servers in order to

Transaction relayers

- Gasless transactions - higher conversion rate, easier user onboarding
- Ensure reliability of actions
- Batch transactions for lower gas

Ethereum Name Service

- With regards to handling user identity, we can make use of a the ENS registry to resolve a human-readable address to their corresponding ethereum accounts.

Profile Storage

- Profile information including a user's followers and their corresponding profile information will be stored in an ERC-721 token. Considering the nature of the frequent writes to the blockchain due to adding or removing followers, this smart contract should be deployed to the Polygon network with its dramatically lower gas fees than Ethereum.
- Storing of a user's social graph information on the ERC-721 token allows users to own their audience, allowing their following to be client-agnostic.
- There would be a reference between the token to the Domain Name Regs

Tweet Storage

- To ensure that posts/tweets are immutable and not hosted on a centralised server, we can make pin posts onto IPFS.

Video Storage

- On the other hand, storage of more complex multimedia object can be done on storj.

Redis Caching

- Some tweets from popular individuals might be accessed often, so we should cache them in a distributed cache like redis.

CDN

- Meanwhile, geographically distributed CDNs can ensure the timely delivery of multimedia assets, as well as serve static data such as client HTML pages

## D) Front End

To be honest, I am not really a UI/UX person, but I would say that for a start, the current twitter user experience is the quintessential way that short tweets can be consumed en masse. However, a way that our decentralized Twitter can stand out from the competition would be to include notifications and on-chain activities of other users that we follow. This would give users a more hollistic view of what is going on in their blockchain networks and physical networks literally.

## E) Smart contract

# Tradeoffs and Final Thoughts

Being honest again, I don't think that I alone can complete this task in 4 weeks. However, what I can guarantee is that I can produce a working minimum viable product that actually connects and interacts with said blockchains, together with a web-frontend that allows users to view and interact with tweets. Scaleability would also not be an issue, as the focus would be on a working prototype is created.

Additionally, in order to ensure that we get the system up and running in the shortest amount of time, a trade-off is that instead of building all the components ourselves, we can leverage on existing protocols that have already created primitives to solve certain problems in the realm of decentralised social networks. An example would be lens protocol or the farcaster network, where many projects are currently building upon. Leveraging on these existing decentralised social network protocols allow us to provide more feature-rich interactions by building upon these primitives, that are tried and tested.

I am not sure how much of the decentralised twitter is required to be built in-house, but if we could leverage on these protocols, more time and effort can be placed on refining the user experience and user interface to produce the best browsing experience in the industry. Successful social networks are usually built around a new communication paradigm, like tinder's swipe to match or tiktok's scrolling agorithm. Offering a product experience that doesn’t yet exist is far more compelling than a clone of an existing network.
