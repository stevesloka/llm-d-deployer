# Setup for Intel Gaudi on Kubernetes

## Init

### Helm

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

## Depedencies

```bash
kubectl create namespace habana-ai-operator
kubectl label namespace habana-ai-operator pod-security.kubernetes.io/enforce=privileged --overwrite
kubectl label namespace habana-ai-operator pod-security.kubernetes.io/audit=privileged --overwrite
kubectl label namespace habana-ai-operator pod-security.kubernetes.io/warn=privileged --overwrite

helm repo add gaudi-helm https://vault.habana.ai/artifactory/api/helm/gaudi-helm
helm repo update
helm install habana-ai-operator gaudi-helm/habana-ai-operator --version 1.21.1-16 -n habana-ai-operator

kubectl create -f https://vault.habana.ai/artifactory/docker-k8s-device-plugin/habana-k8s-device-plugin.yaml
```

// ref: https://docs.habana.ai/en/latest/Installation_Guide/Additional_Installation/Kubernetes_Installation/Kubernetes_Operator.html#intel-gaudi-operator-for-kubernetes
