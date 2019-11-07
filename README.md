# CountR Api Documentation

## Introduction / Quick Start

This is a proposal for the simplest use of a FaceRecognition system.

<image src="https://github.com/dariuszlee/dariuszlee.github.io/blob/master/countr_session_diagram.png?raw=true" alt="SessionDiagram" style="width:600px"/>
[Better quality image](https://github.com/dariuszlee/dariuszlee.github.io/blob/master/countr_session_diagram.png?raw=true)

### Server
Simply start the server.
```bash
java -jar server.jar -port 6000
```

#### Scaling the server

If we are finding that we need to more server compute power (ie. server response time is too slow), we can configure another server on another port.

```bash
java -jar server.jar -port 6000
java -jar server.jar -port 6001
...
```

Clients would simply need to connect to a different port. 

The limit for number of servers is likely the size of GPU memory.

### Client
The code itself can be delivered as a Jar dependency, through Maven, for example.

#### Proposal 1
From application code, we can start a session and query a session.
```java
FaceRecognitionSession session = FaceRecognition.createSession(6000);
session.identify();
while(true){
    // Do some work that takes time
    FaceRecognitionInfo info = session.GetSessionInfo();
    if(info.confidenceInterval > threshold)
        break;
}
session.close()
```

FaceRecognitionInfo would look something like this.

```java
class FaceRecognitionInfo {
    int faceId;
    float confidenceInterval;
}
```

## Conclusion

This paper requires a decision if this implementation would be acceptable for CountR's current system.
