---
layout: post
title:  "Introduction to Actors (Akka)"
date:   2017-05-23 23:37:44
categories: scala
---

### Creating Actors
1. **Extending Actor Class** 

    Actor classes are implemented by extending the Actor class and implementing the `receive` method.
    The receive method should define a series of case statements (which has the type `PartialFunction[Any,
    Unit]`) that defines which messages your Actor can handle, using standard Scala pattern matching.

    Example
    ```
    class MyActor extends Actor {
        val log = Logging(context.system, this)
            def receive = {
                case "test" => log.info("received test")
                case _ => log.info("received unknown message")
        }
    }
    ```

2. **Creating Actors with default constructor**
    ```
        val system = ActorSystem("MySystem")
        val myActor = system.actorOf(Props[MyActor], name = "myactor")
    ```
    The call to actorOf returns an instance of ActorRef. This is a handle to the Actor instance which you can
    use to interact with the Actor.

    It is also possible to create actors from other actors with the actor context.
    
    ```
        class FirstActor extends Actor {
        val myActor = context.actorOf(Props[MyActor], name = "myactor")
    ```
    The name parameter is optional, but you should preferably name your actors, since that is used in log messages
    and for identifying actors

3. **Creating Actors with non-default constructor** 
    
    If your Actor has a constructor that takes parameters then you can’t create it using `actorOf(Props[TYPE])`
    ```
        val myActor = system.actorOf(Props(new MyActor("...")), name = "myactor")
    ```
4. **Using Props**

    Props is a configuration class to specify options for the creation of actors

    ```
        import akka.actor.Props
        val props1 = Props()
        val props2 = Props[MyActor]
        val props3 = Props(new MyActor)
        val props4 = Props(
        creator = { () ) new MyActor },
        dispatcher = "my-dispatcher")
        val props5 = props1.withCreator(new MyActor)
        val props6 = props5.withDispatcher("my-dispatcher")
    ```

    ```
        val myActor = system.actorOf(Props[MyActor].withDispatcher("my-dispatcher"), name = "myactor2")
    ```
### Actor API
The Actor trait defines only one abstract method, the above mentioned receive, which implements the behavior
of the actor. If the current actor behavior does not match a received message, unhandled is called, which by default publishes
an akka.actor.UnhandledMessage(message, sender, recipient) on the actor system’s event stream. In addition

- `self` reference to the ActorRef of the actor
- `sender` reference sender Actor of the last received message, typically used as described in Reply to messages
- `supervisorStrategy` user overridable definition the strategy to use for supervising child actors
- `context` exposes contextual information for the actor and the current message.

### Identifying Actors

Each actor has a unique logical path, which is obtained
by following the chain of actors from child to parent until reaching the root of the actor system

Example
```
    context.actorFor("/user/serviceA/aggregator") // will look up this absolute path
    context.actorFor("../joe") // will look up sibling beneath same supervisor
```

Remote actor addresses may also be looked up, if remoting is enabled.

```
    context.actorFor("akka://app@otherhost:1234/user/serviceB")
```

### Send messages
- `!` means “fire-and-forget”, e.g. send a message asynchronously and return immediately. Also known as tell.
- `?` sends a message asynchronously and returns a Future representing a possible reply. Also known as ask.

### Reply to messages
If you want to have a handle for replying to a message, you can use sender.

```
    case request => val result = process(request)
                    sender ! result
```