# Istio in 5 minutes

Got 5 minutes and a cluster? That's all you need to learn Istio.

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

### Routing

The BookInfo application has a front-end.`productpage` service. We need to create 
 - Istio `Gateway` resource to configure the Ingress Gateway operating at the edge of the mesh receiving incoming connections
 - Istio `Virtual Service` to route from the Gateway to the `productpage` service
 
 ```
 kubectl apply -f ./samples/bookinfo/networking/bookinfo-gateway.yaml -n demo
 ```
 
 ### Visit your application
 
Get the EXTERNAL-IP address of your `istio-ingressgateway`.
 ```
kubectl get svc -n istio-system
```

Visit `http://<EXTERNAL-IP>/productpage` in your browser
 
 ### Dashboards
 
 Launch the various Istio dashboards
 ```
 ./bin/istioctl x dashboard kiali
 ./bin/istioctl x dashboard grafana
 ./bin/istioctl x dashboard jaeger
 ```
