# CountR Api Documentation
## Introduction / Quick Start

This is a proposal for the simplest use of a FaceRecognition system.


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

<a><image src="https://github.com/dariuszlee/dariuszlee.github.io/blob/master/DataFlow2.png?raw=true" alt="SessionDiagram" style="width:100%"/>
</a>
<!-- <a href="./DataFlow2.png"><image src="./DataFlow2.png" alt="SessionDiagram" style="width:100%"/> -->
<!-- </a> -->

Here is the above image in Java-like pseudo-code.

```java
Integer timeout = 1000
FaceRecognitionSession session = FaceRecognition.createSession(6000);
while(true){
    GetFaceStatus faceStatus = session.GetFace(timeout)
    if(faceStatus.IsFound()){
        FaceRecognitionStatus recognizedStatus = session.Recognize(faceStatus, timeout)
        if(recognizedStatus.IsRecognized()){
            break
        }
    }
    else{
        // Do something else
    }
}
ArrayList<FaceRecognitionInfo> sessionResults = session.GetResults()
session.close()
```

FaceRecognitionInfo would look something like this.

```java
class FaceRecognitionInfo {
    int faceId;
    float confidenceInterval;
}
```

## Delivery

Client and server can be delivered as a JAR through maven or a private repository.

## Conclusion

This paper requires a decision if this implementation would be acceptable for CountR's current system.
