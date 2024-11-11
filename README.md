# jmspoc

This creates an incmoing API endpoint with three resources, each posts a message to a corresponding message queue:

* /pay posts to -> OrderPaymentMQ
* /fail posts to ->  OrderPaymentErrorMQ
* /retry posts to -> OrderPaymentRetryMQ

A message from the OrderPaymentErrorMQ to either of the other message queues in ActiveMQ should be processed.
This proof-of-concept that an error queue (with no message processor) can act as a triage queue.

There are there environment variables:

| Variable Name | Example |
| --- | --- |
| `jmsurl` | `failover(activeMQ uri, activeMQ failover uri)` |
| `jmsuser` | `activeMQ user` |

Following secrets should be configured when deploying this component in Choreo.

| Secret Name | Hint|
| --- |--- |
| `jmspass` | `Active MQ password` |
