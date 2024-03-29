# Stream Processing Fraud Detection with Kafka and Flink

## Lab 2 - Install Kafka and Flink

### Step 1 - Install Kafka
To begin, install the Kafka framework on DC/OS using the following command:

```bash
dcos package install kafka --yes
```

Next, figure out where the broker is:

```bash
dcos kafka endpoints broker
{
  "address": [
    "10.0.2.64:1025",
    "10.0.2.83:1025",
    "10.0.0.161:1025"
  ],
  "dns": [
    "kafka-0-broker.kafka.autoip.dcos.thisdcos.directory:1025",
    "kafka-1-broker.kafka.autoip.dcos.thisdcos.directory:1025",
    "kafka-2-broker.kafka.autoip.dcos.thisdcos.directory:1025"
  ],
  "vip": "broker.kafka.l4lb.thisdcos.directory:9092"
}
```

Note the FQDN for the vip: In our case `broker.kafka.l4lb.thisdcos.directory:9092`, which is independent of the actual broker locations.

It is possible to use the FQDN of any of the brokers, but using the VIP FQDN will give us load balancing.

### Step 2 - Create Kafka topics

DC/OS makes managing Kafka topics incredibly easy using the Kafka CLI.

Run the following 2 commands:

```
dcos kafka topic create transactions
dcos kafka topic create fraud
```

### Step 3 - Install Flink

Next, we need to install Flink.

```bash
dcos package install --yes flink
```

The Services tab in your DC/OS UI should show the full suite of services you have successfully deployed.

[Next Lab >>](https://github.com/gregpalmr/dcos-workshop-2019-03-19/blob/master/labs/2%20-%20Data-Services-labs/Lab_03_Install_Microservices.md)
