# Sending Kafka data to IBM Event Streams using ACE

This demo helps you learn how to connect App Connect Enterprise to IBM Event Streams. Apache Kafka is an open source project that provides a messaging service capability, based upon a distributed commit log. It lets you publish and subscribe data to streams of data records (messages). 



For this we will be using eventStream service available in IBM Cloud : https://cloud.ibm.com/catalog/services/event-streams

## Requirement

- Create IBM EventStream service in IBM Cloud : https://cloud.ibm.com/catalog/services/event-streams
- Install App Connect Toolkit : https://developer.ibm.com/integration/docs/app-connect-enterprise/get-started/

## Test Flow in App Connect Toolkit

- Import the provided project interchange file into your ACE Toolkit’s workspace [here](resources/PI_EventStreams.zip). You will find an application called EventStreams which contains a message flow named EventStreamsFlow. 

![Flow](images/flow.png)

- The purpose of this flow is to receive a simple JSON message over HTTP, which contains the name of a Kafka topic and some payload data. The KafkaProducer message flow node sends the payload to the provided topic. Look at the KafkaProducer node’s properties. 

- You will need to change the Bootstrap servers property to refer to your IBM Event Streams system and the Topic name on the message flow node. 

![Flow](images/kafkaproperties.jpg)


>  Retrieve Bootstrap server endpoint in service credential of your Event Stream service instance
  https://cloud.ibm.com/docs/EventStreams?topic=EventStreams-connecting


- For secure connection with EvenStream, open the file server.conf.yaml of you test ACE Server in your favoured text editor. Locate the ResourceManagers … JVM section, and uncomment the truststore properties and assign the following values (Replace with your values):

```
ResourceManagers:
  JVM:
    truststoreType: 'JKS'
    truststoreFile: 'C:\data\truststore\trustStore.jks'
    truststorePass: 'MyServer::truststorePass'
```

The JKS certificate file which is placed into the ACE trust store, is used by ACE to verify the certificate which is presented by IBM Event Streams during the handshake when an SSL connection is made. The file trustStore.jks is a copy of the server-side public certificate which you can download from IBM Event Streams. When you download the jks file, by default it is protected by a simple password which is the value password but you will want to change this, or export the certificate and import it into your own trust store using a tool such as keytool.

## Deploy Bar file in IBN App Connect on IBM Cloud

- Create IBM App Connect service in IBM Cloud : https://cloud.ibm.com/catalog/services/app-connect

> Note: You can use Lite Plan

- You will also need an API key which can be generated from the IBM Cloud Private user interface that comes with IBM Event Streams. 

Retrieve apikey value from service credential of the IBM Event Stream service.



We will provide these passwords to the ACE infrastructure in the commands which follow:

`mqsisetdbparms -w C:\Users\FredericDutheil\workspace\ace\sandbox\TEST_SERVER -n MyServer::truststorePass -u thiscanbeanyvalue -p xxxxx`

`mqsisetdbparms -w C:\Users\FredericDutheil\workspace\ace\sandbox\TEST_SERVER -n kafka::KAFKA -u token -p "hmHbWpFWewExxxxxxxxxxxxxxx"`




# Resources

https://developer.ibm.com/integration/blog/2018/10/01/connecting-app-connect-enterprise-and-ibm-integration-bus-to-ibm-event-streams/