# Stream Processing Fraud Detection with Kafka and Flink

## Lab 1 - Introduction

In this lab exercise, you will implement a data processing infrastructure that is able to detect money laundering. 

In the context of money laundering, we want to detect amounts larger than $10,000 transferred between two accounts, even if that amount is split into many small batches. (See also US and EU legislation and regulations on this topic for more information.)

The architecture mostly follows the [SMACK stack architecture](https://mesosphere.com/blog/smack-stack-new-lamp-stack/):

- Events: Events are generated by a small [GOLANG generator](https://github.com/dcos/demos/blob/master/flink/1.11/generator/generator.go). The events are in the form 'Sunday, 23-Jul-17 01:06:47 UTC;66;26;7810', where the first field '23-Jul-17 01:06:47 UTC' represents the (increasing) timestamp of transactions; the second field '66' represent the sender account; the third field the receiver account; and the fourth field represent the dollar amount transferred during that transaction.
- Ingestion: The generated events are being ingested and buffered by a Kafka queue with the default topic 'transactions'. Being a Microservice we will deploy the data-generator on kubernetes.
- Stream Processing: As we require fast response times, we use Apache Flink as a Stream processor running the FinancialTransactionJob.
- Storage: Here we diverge a bit from the typical SMACK stack setup and don't write the results into a Datastore such as Apache Cassandra. Instead we write the results again into a Kafka Stream (default: 'fraud'). Note, that Kafka also offers data persistence for all unprocessed events.
Actor: In order to view the results we use again a small Golang viewer which simply reads and displays the results from the output Kafka stream. Being a Microservice we will deploy the viewer on kubernetes.


![](https://github.com/dcos/demos/blob/master/flink-k8s/1.11/img/kafka-flink-arch.png)

[Next Lab >>](https://github.com/gregpalmr/dcos-workshop-2019-03-19/blob/master/labs/2%20-%20Data-Services-labs/Lab_02_Install_Kafka_and_Flink.md)
