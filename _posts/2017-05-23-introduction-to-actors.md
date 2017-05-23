---
layout: post
title:  "Introduction to Actors (Akka)"
date:   2017-05-21 23:37:44
categories: scala
---

### Actors
Actors are objects which encapsulate state and behavior, 
they communicate exclusively by exchanging messages which are placed into the recipient’s mailbox.
One actor, which is to oversee a certain function in the program might want to split up its task into smaller, 
more manageable pieces. For this purpose it starts child actors which it supervises.
The only prerequisite is to know that each actor has exactly one supervisor,
which is the actor that created it.
  
An actor is a container for State, Behavior, a Mailbox, Children and a Supervisor Strategy. All of this is encapsulated
behind an Actor Reference.

### Actor Reference
Actors are represented to the outside using actor references.

### State
Actor objects will typically contain some variables which reflect possible states the actor may be in.
This data is what make an actor valuable, and it must be protected from corruption by other actors.

Because the internal state is vital to an actor’s operations, having inconsistent state is fatal. Thus, when the actor
fails and is restarted by its supervisor, the state will be created from scratch, like upon first creating the actor. 
This is to enable the ability of self-healing of the system.

### Behavior
Behavior means a function which defines the actions to be taken in reaction to the 
message at that point in time, say forward a request if the client is authorized, deny it otherwise.

### Mailbox
The piece which connects sender and receiver is the actor’s mailbox. Each actor
has exactly one mailbox to which all senders enqueue their messages. Enqueuing happens in the time-order of
send operations, which means that messages sent from different actors may not have a defined order at runtime
due to the apparent randomness of distributing actors across threads.

There are different mailbox implementations to choose from, the default being a FIFO

Failure to handle a message will typically be treated as a failure, unless this behavior is overridden.

### Children
Each actor is potentially a supervisor: if it creates children for delegating sub-tasks, it will automatically supervise
them. The list of children is maintained within the actor’s context and the actor has access to it.


### Few important guidelines
- Do not pass mutable objects between actors.
- Do not send behavior within messages (which may be tempting using Scala closures).
- Manager knows which kind of failures are expected and how to handle them.
- If one actor depends on another actor for carrying out its duty, it should watch that other actor’s liveness and act upon receiving a termination notice.

