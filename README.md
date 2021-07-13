Developing Reactive Streams with Quarkus and Red Hat OpenShift Streams for Apache Kafka
========================

This project illustrates how you can interact with Red Hat OpenShift Streams for Apache Kafka using Quarkus Reactive application.

## Creating a new Kafka instance on Red Hat OpenShift Streams

Go to [cloud.redhat.com](cloud.redhat.com^) and log in with your Red Hat account. Create a new Kafka instance in *Application Services* menu then create a topic as well as service account. See more details about [Getting started with Red Hat OpenShift Streams for Apache Kafka](https://developers.redhat.com/articles/2021/07/07/getting-started-red-hat-openshift-streams-apache-kafka^).

## Update configurations

Replace the following configurations in `application.properties` with your service account and connection information of the Red Hat OpenShift Streams for Apache Kafka:

* KAFKA_BOOTSTRAP_SERVERS
* CLIENT_ID
* CLIENT_SECRET

## Start the application

The application can be started using: 

```bash
mvn quarkus:dev
```

_NOTE_: Quarkus Dev Services starts a Kafka broker for you automatically. 

Then, open your browser to `http://localhost:8080/prices.html`, and you should see a fluctuating price.

## Anatomy

In addition to the `prices.html` page, the application is composed by 3 components:

* `PriceGenerator` - a bean generating random price. They are sent to a Kafka topic
* `PriceConverter` - on the consuming side, the `PriceConverter` receives the Kafka message and convert the price.
The result is sent to an in-memory stream of data
* `PriceResource`  - the `PriceResource` retrieves the in-memory stream of data in which the converted prices are sent and send these prices to the browser using Server-Sent Events.

The interaction with Kafka is managed by MicroProfile Reactive Messaging.
The configuration is located in the application configuration.

## Running in native

You can compile the application into a native binary using:

`mvn clean install -Pnative`

Then run with:

`./target/kafka-quickstart-1.0.0-SNAPSHOT-runner` 

## Watch the demo

[![Developing Reactive Streams with Quarkus and Red Hat OpenShift Streams for Apache Kafka](images/thumbnail.png)](https://youtu.be/WDPx7abR328^)

