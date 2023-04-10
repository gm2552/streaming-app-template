# Streaming App Template

## Description

The Streaming App Template is an application accelerator for quickly generating a starter application that implements aspects of streaming application
using Spring Cloud Streams concepts.  The created application can take on one of more the following traits of a streaming pattern:

- Source: Source application that generates new events
- Processor: Processing applications that perform business logic on events from the sources and sends them onto a sink
- Sink: Sink application that persists of performs some type of final operation of processed events.

The generated application contains source code and configuration needed for each trait as well as an default event model object.

## Usage

The application accelerator generates a starter project based on selected configuration options.  These options include:

* **Name:**  The name of the workload/project that will be created.  The spring.application.name will also reflect this option.
* **Maven Group Name:** The maven group name used for a build application.
* **Service Root Package Name:**  The base Java package name used for the application.
* **Application Main Class Name:**  The name of class that will be used as the SpringBoot main class.
* **Model Class Name:**  The name of class that will be used for the model object that implements the event passed between services.
* **Event Source:** If this option is checked, the application will contain boilerplate code and configuration to generate events using a default `PollingBean`
* **Event Processor:** If this option is checked, the application will contain boilerplate code and configuration to process an event using a `Function`.
* **Event Sink:** If this option is checked, the application will contain boilerplate code and configuration to store or perform final processing using a `Consumer`.
* **Event Source Channel:** If the application is an event source or processor, this is the name of the messaging channel for the source event object. 
* **Event Source Channel Group:** If the application is an event processor, this is the name of the messaging group for the source event object. 
* **Event Result Channel:** If the application is an event processor or sink, this is the name of the messaging channel for the processing result object. 
* **Event Result Channel Group:** If the application is an event sink, this is the name of the messaging group for the processing result object. 
* **Message Broker Name:** The name of the message broker that will be used for service binding.  This is generally the name of a `ResourceClaim` or `ClassClaim`. 
* **Source Image Repository:** When TAP IDE support is checked, this is the source image repository name populated into the Tiltfile. Exmaple format <registryServerName>/<repositoryName>

## Project Layout

The generated application will have the following layout; function classes will be generated based on selected applications traits:

```
pom.xml
 + - src/main/java
     + - resources
         | application.yaml
     + - <package root>
         | - <MainApplciationClass>.java  
         + - functions
             | - <Model>Process.java
             | - <Model>Source.java
             | - <Model>Sink.java
             + - model
                 | <EventModelClass>.java
```

## Application Function

By default, the source application generates a new event using a `PollableBean` method that simply return a new instance of the event model class (by default, a new event is
generated every second).  The processor simply logs out message that the event was received and returns the event unmodified.  Lastly, the sink outputs that the 
processor result was received.