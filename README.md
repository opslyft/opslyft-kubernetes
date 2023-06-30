# Opslyft Kubernetes Deployment

Follow the steps below to install OpenCost

## Step 1: Prometheus

Opencost relies on metrics scraped by Prometheus. For express installation of Prometheus use the following command:

```
helm install opskube-prometheus --repo https://prometheus-community.github.io/helm-charts prometheus \
  --namespace prometheus --create-namespace \
  --set pushgateway.enabled=false \
  --set alertmanager.enabled=false \
  -f https://raw.githubusercontent.com/opencost/opencost/develop/kubernetes/prometheus/extraScrapeConfigs.yaml
```
This Prometheus installation is based on Prom community helm chart, and by default your Prometheus might scrape unnecessary metrics.

## Step 2: Installing OpenCost

To install OpenCost on your cluster, you need to replace <your-cluster-name> with your actual Kubernetes cluster name in the command below before running it:

```
curl -s https://raw.githubusercontent.com/opslyft/opslyft-kubernetes/main/opencost.yaml | sed 's/cluster-one/<your-cluster-name>/g' | kubectl apply --namespace opencost -f -
```

## Testing

```
kubectl get svc -n opencost
```
Copy the ```EXTERNAL-IP``` from the response of above command and hit ```http://EXTERNAL-IP:9003/allocation/compute?window=60m```
