# wso2esb-rabbitmq-message-store
## WSO2 ESB Message Store and Message Processor implementation for RabbitMQ

This Message Store and Message Processor (MS&MP) implements the way how to WSO2 ESB and RabbitMQ (or any Message Broker) should work.
With this MS&MP we can implement different EIP related to messaging such as:

- Dead Letter Queue
- Wire Tap
- Retry Queue
- Throttling

For further information about EIP, I recommend the next pages:  
* <a target="_new" href="https://docs.wso2.com/display/IntegrationPatterns/Enterprise+Integration+Patterns+with+WSO2+ESB">https://docs.wso2.com/display/IntegrationPatterns/Enterprise+Integration+Patterns+with+WSO2+ESB</a>
* <a href="https://holisticsecurity.wordpress.com/2014/12/03/wso2-message-broker-vs-apache-qpid-messaging-eip/" target="_new">https://holisticsecurity.wordpress.com/2014/12/03/wso2-message-broker-vs-apache-qpid-messaging-eip/</a>

This is valid for:

- WSO2 ESB 4.8.1
- RabbitMQ 3.4.4
- Apache Qpid client 0.30

<h3>How to check the sourcecode and configuration</h3>

Follow the next commands:

```bash
$ mkdir wso2esb-rabbitmq-message-store
$ cd wso2esb-rabbitmq-message-store
$ git pull https://github.com/Chilcano/wso2esb-rabbitmq-message-store.git
$ mvn clean install
$ mvn exec:java -Dexec.mainClass="com.chakray.chilcano.wso2.rabbitmq.sample.HelloRabbitMQ"
```

The <code>com.chakray.chilcano.wso2.rabbitmq.sample.HelloRabbitMQ</code> is a simple JMS client that publish and consume a message to/from RabbitMQ. This sample uses Apache Qpid client library, does not use RabbitMQ client libraries. To execute properly you should update the <code>hello_rabbitmq_jndi.properties</code> with your values.

### How to deploy on WSO2 ESB

Deploy the libraries:

1. Copy `hello_rabbitmq_jndi.properties, qpid-client-0.30.jar, qpid-common-0.30.jar, wso2esb-rabbitmq-msmp-0.1.jar` to <code>%WSO2ESB_HOME%/repository/components/lib/</code> folder.
2. Restart WSO2 ESB

Deploy the Synapse files for the Message Store and API samples:

1. In RabbitMQ side you need to create a queue and 2 routing keys. I recommend you use the <code>hello_rabbitmq_config_broker.json</code> and import it from the RabbitMQ web admin console.
2. Copy <code>HelloRabbitMQMsgStore1.xml</code> into <code>%WSO2ESB_HOME%/repository/deployment/server/synapse-configs/default/message-stores/</code>
3. Copy <code>HelloRabbitMQRest1.xml</code> into <code>%WSO2ESB_HOME%/repository/deployment/server/synapse-configs/default/api/</code>

WSO2 ESB automatically will deploy these 2 synapse files and after that you are ready to send a message to WSO2 ESB and store this message in RabbitMQ side.


-end-


