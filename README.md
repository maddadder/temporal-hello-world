# Hello World

This is the default project that is scaffolded out when you run `npx @temporalio/create@latest ./myfolder`.

The [Hello World Tutorial](https://docs.temporal.io/docs/typescript/hello-world/) walks through the code in this sample.

### Running this sample

1. Make sure Temporal Server is running locally (see the [quick install guide](https://docs.temporal.io/docs/server/quick-install/)).
```
kubectl port-forward services/temporaltest-frontend-headless 7233:7233
kubectl port-forward services/temporaltest-web 8088:8088
```
2. `npm install` to install dependencies.
3. `npm run start.watch` to start the Worker.
4. In another shell, `npm run workflow` to run the Workflow Client.

The Workflow should return:

```bash
Hello, Temporal!
```

### Initial setup
```
git clone https://github.com/temporalio/helm-charts
# cd into that folder
helm dependencies update
helm install \
    --set server.replicaCount=1 \
    --set cassandra.config.cluster_size=1 \
    --set prometheus.enabled=false \
    --set grafana.enabled=false \
    --set elasticsearch.enabled=false \
    temporaltest . --timeout 15m
kubectl port-forward services/temporaltest-frontend-headless 7233:7233
#open new console
kubectl port-forward services/temporaltest-web 8088:8088
#open new console
docker run --rm -it --entrypoint /bin/bash --network host --env TEMPORAL_CLI_ADDRESS=localhost:7233 temporalio/admin-tools:1.14.0
tctl --namespace default namespace register
```

