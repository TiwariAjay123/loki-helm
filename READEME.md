This Helm Chart deploys Grafana Loki on Kubernetes.

This Helm chart deploys Loki to run Loki in microservice mode within a Kubernetes cluster. The microservices deployment mode runs components of Loki as distinct processes.

The default Helm chart deploys the following components:

Compactor component (1 replica): Compacts and processes stored data.
Distributor component (3 replicas, maxUnavailable: 2): Distributes incoming requests. Up to 2 replicas can be unavailable during updates.
IndexGateway component (2 replicas, maxUnavailable: 1): Handles indexing. Up to 1 replica can be unavailable during updates.
Ingester component (3 replicas): Handles ingestion of data.
Querier component (3 replicas, maxUnavailable: 2): Processes queries. Up to 2 replicas can be unavailable during updates.
QueryFrontend component (2 replicas, maxUnavailable: 1): Manages frontend queries. Up to 1 replica can be unavailable during updates.
QueryScheduler component (2 replicas): Schedules queries.

Prerequisites
Helm 3 or above. See Installing Helm.
A running Kubernetes cluster (must have at least 3 nodes).

Step #1
helm repo add grafana https://grafana.github.io/helm-charts

Step #2 
helm repo update

Step #3 (If namespace doesnt exist)
kubectl create namespace loki-helm

Step#4 To install:
helm install --values values.yaml loki grafana/loki

OR  

To upgrade:

helm upgrade --values values.yaml loki grafana/loki

Step#5 : Verify that Loki is running:
kubectl get pods -n loki

EXPECTED OUTPUT

  loki-canary-8thrx                      1/1     Running   0          167m
  loki-canary-h965l                      1/1     Running   0          167m
  loki-canary-th8kb                      1/1     Running   0          167m
  loki-chunks-cache-0                    2/2     Running   0          167m
  loki-compactor-0                       1/1     Running   0          167m
  loki-compactor-1                       1/1     Running   0          167m
  loki-distributor-7c9bb8f4dd-bcwc5      1/1     Running   0          167m
  loki-distributor-7c9bb8f4dd-jh9h8      1/1     Running   0          167m
  loki-distributor-7c9bb8f4dd-np5dw      1/1     Running   0          167m
  loki-gateway-77bc447887-qgc56          1/1     Running   0          167m
  loki-index-gateway-0                   1/1     Running   0          167m
  loki-index-gateway-1                   1/1     Running   0          166m
  loki-ingester-zone-a-0                 1/1     Running   0          167m
  loki-ingester-zone-b-0                 1/1     Running   0          167m
  loki-ingester-zone-c-0                 1/1     Running   0          167m
  loki-minio-0                           1/1     Running   0          167m
  loki-querier-bb8695c6d-bv9x2           1/1     Running   0          167m
  loki-querier-bb8695c6d-bz2rw           1/1     Running   0          167m
  loki-querier-bb8695c6d-z9qf8           1/1     Running   0          167m
  loki-query-frontend-6659566b49-528j5   1/1     Running   0          167m
  loki-query-frontend-6659566b49-84jtx   1/1     Running   0          167m
  loki-query-frontend-6659566b49-9wfr7   1/1     Running   0          167m
  loki-query-scheduler-f6dc4b949-fknfk   1/1     Running   0          167m
  loki-query-scheduler-f6dc4b949-h4nwh   1/1     Running   0          167m
  loki-query-scheduler-f6dc4b949-scfwp   1/1     Running   0          167m
  loki-results-cache-0                   2/2     Running   0          167m