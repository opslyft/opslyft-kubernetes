# Opslyft Kubernetes Deployment

Follow the steps below to install OpenCost

## Step 1: Prometheus

Opencost relies on metrics scraped by Prometheus. For express installation of Prometheus use the following command:

```
helm install my-prometheus --repo https://prometheus-community.github.io/helm-charts prometheus \
  --namespace prometheus --create-namespace \
  --set pushgateway.enabled=false \
  --set alertmanager.enabled=false \
  -f https://raw.githubusercontent.com/opencost/opencost/develop/kubernetes/prometheus/extraScrapeConfigs.yaml
```
This Prometheus installation is based on Prom community helm chart, and by default your Prometheus might scrape unnecessary metrics.

## Step 2: Installing OpenCost

This command will install OpenCost on your cluster.

```
kubectl apply --namespace opencost -f https://raw.githubusercontent.com/opslyft/opslyft-kubernetes/main/opencost.yaml
```

## Testing

```
kubectl get svc -n opencost
```
Copy the ```EXTERNAL-IP``` from the response of above command and hit ```http://EXTERNAL-IP:9003/allocation/compute?window=60m```
