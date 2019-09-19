# Istio in 5 minutes

Got 5 minutes and a cluster? That's all you need to learn Istio.

## Basics

### Download Istio 
```
curl -L https://git.io/getLatestIstio | ISTIO_VERSION=1.3.0 sh - && cd istio-1.3.0
```

### Install Demo profile
```
for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
kubectl apply -f install/kubernetes/istio-demo.yaml
```

### Create a new namespace and enable automatic sidecar injector for it
```
kubectl create namespace demo
kubectl label namespace demo istio-injection=enabled
```

### Install BookInfo sample
```
kubectl apply -f ./samples/bookinfo/platform/kube/bookinfo.yaml -n demo
```

## Routing
Your BookInfo application has a `productpage` service which is the main 
