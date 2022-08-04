This is a Helm chart to provision a CFK Clusterlink CRD.

# Prerequisites

1. At least one CFK cluster.
2. The target cluster which needs to be linked.


# How to run

1. Clone this repository.
2. Install the Helm chart. Here's an example command.

```bash
$ helm install clusterlink-tls ./clusterlink --values <your-values-file>.yaml -n <target-namespace>
```

# Configuration values

The chart takes in all the values under the official version of [CFK ClusterLink CRD](https://docs.confluent.io/operator/current/co-api.html#tag/ClusterLink). **NOTE** that there is no schema validation done from the chart's end for the spec.

Here's an example `values.yaml` file.

```yaml
spec:
  destinationKafkaCluster:
    kafkaRestClassRef:
      name: krc-example
  sourceKafkaCluster:
    bootstrapEndpoint: example.com:9092
    clusterID: test_kafka_cluster_id
  consumerGroupFilters:
    - name: filter-example
      patternType: LITERAL
      filterType: INCLUDE
  aclFilters:
      - resourceFilter:
          resourceType: topic
          name: coffee
          patternType: prefixed
        accessFilter:
          principal: User:Bob
          host: example .com
          operation: read
          permissionType: allow
  configs:
    connections.max.idle.ms: "620000"
```

# Version

This setup was tested with `7.2.0`, which was the latest version at the time of writing this chart.