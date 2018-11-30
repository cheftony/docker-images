# Benchmarking ElasticSearch deployments

## Simple

1. Update `rally.ini` to use in-memory store for simple tests

1. Build esrally container

At the root of this repository:
```
docker build -t cheftony/esrally:1.0.2 .
docker push cheftony/esrally:1.0.2
```

1. Run esrally container in kubernetes:

```
kubectl run -it --generator "run-pod/v1" esrally --image cheftony/esrally:1.0.2 -- /bin/sh
```

TLS Support
```
--client-options="use_ssl:true,verify_certs:true,ca_certs:'/path/to/cacert.pem',client_cert:'/path/to/client_cert.pem',client_key='/path/to/client_key.pem'"
```

1. start benchmark agains es-cluster (from the attached terminal)

```
esrally list tracks
esrally --pipeline=benchmark-only --target-hosts=es-elasticsearch:9200
```

NOTE: Read warnings about why you shouldn't run esrally against your production escluster.
(It may delete all indices... you have been warned)

1. Copy benchmark results from pod to local machine locally:

```
kubectl exec -i esrally -- tar cz '/root/.rally/benchmarks/races/' | tar xz --strip-components 3
```

Decompress all log files:
```
for f in races/*/local/logs-*; do unzip $f -d ${f:0:26}; done
```

Print rally report
```
sed -n '/Lap/,/Sweeping/p' races/*/logs/rally_out.log
```

## Tournaments

1. Install Kibana and ES cluster to store race results

```
helm install kibana-es -f=benchstore-values.yaml -n benchstore .
```

1. Update `rally.ini` to use the external es cluster

```
esrally configure --advanced-config
```

1. Run multiple races

```
esrally --pipeline=benchmark-only --target-hosts=benchtest-elasticsearch:9200 --track=tiny --user-tag=race1
```

1. List races and compare

```
esrally list races
esrally compare --baseline=<race1> --contencer=<race2>
```

You should do comparison between the metrics recorded...
