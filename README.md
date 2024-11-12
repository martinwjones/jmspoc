# jmspoc

An WSO2 Micro Integrator project written in Apache synsapse code.
This creates an incoming API endpoint with three resources, each posts a message to a corresponding message queue:

* /pay posts to -> OrderPaymentMQ -> is processed and the payload printed out. It then gets sent to the OrderPaymentErrorMQ
* /fail posts to ->  OrderPaymentErrorMQ -> has NO processor. Messages should be manually copied to the OrderPaymentRetryMQ
* /retry posts to -> OrderPaymentRetryMQ -> is processed and the payload printed out - END.

This proof-of-concept that an error queue (with no message processor) can act as a triage queue.

There are three environment variables:

| Variable Name | Example |
| --- | --- |
| `jmsurl` | `failover(activeMQ uri, activeMQ failover uri)` |
| `jmsuser` | `activeMQ user` |

Following secrets should be configured when deploying this component in Choreo.

| Secret Name | Hint|
| --- |--- |
| `jmspass` | `Active MQ password` |

## libs folder

The following jar files are required to work with ActiveMQ 5.17.6
These can be downloaded from ActiveMQ's website <https://activemq.apache.org/components/classic/download/>:

* activeio-core-3.1.4.jar
* activemq-broker-5.17.6.jar
* activemq-client-5.17.6.jar
* activemq-kahadb-store-5.17.6.jar
* geronimo-j2ee-management_1.1_spec-1.0.1.jar
* geronimo-jms_1.1_spec-1.1.1.jar
* geronimo-jta_1.1_spec-1.1.1.jar
* hawtbuf-1.11.jar
* slf4j-api-1.7.36.jar

## deployment.toml

The following should be added to your deployment.toml file so local://services/Proxy urls are allowed

```bash
    [transport.local.sender.nonblocking]
    enable = true
```
