# Service Mesh
The way to manage traffic inside the kubernetes cluster. The services in a fast pace microservice type environment where many applications are talking to each other, the requirements for the proxy( connection flows) for each application becomes to huge to manually manage. 
Instead of injecting logic on each service or having many services for an application is cumbersome. Therefore a service mesh is an infrastructure that handles the data plane for all the services and controls the flow of traffic in a cluster. With  a service mesh the logic for traffic flow 
can be a stand alone application without introducing the network logic in the application design. Istio is a open source service mesh popular in the company standard. 

## Istio
## Installation 
The installation of istio control plane is done at the `istio-system` namespace. The process for installation can be followed at https://github.com/anityam/istio . The installation will install the control plane at `istio-system`.

## Component
Istiod --> This is the main component of the control plane. The custom resources that istio uses like `virtualhost` are converted to envoy configs by istiod

## Traffic Entry point
The traffic in the istio cluster moves inside the cluster through the **INGRESS** resource.
### Concept
Istiod is the controller for the Ingress resource. It looks at the configs and configures the envoy based proxy. This can have a corresponding nodePort or external cloud based loadbalancer that exposes the traffic 

#### Envoy Proxy


## Concept
Istio keeps a database of it's managed service and service endpoints in a registry called service registry. The envoy proxy uses this service registry to route the traffic. Istio has a mechanism of service discovery (Pilot) or [ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/) configuration can be added to add the service to the service Registry.
Envoy proxy distributes traffic based on least load model. If there are more than two loadbalancer or host receiving the traffic than envoy routes the traffic to the host that is handling the least amount of traffic
Outside of the routes istio can also split traffic across instances 

## Apis
1. Virtual Service
2. Destination Rule
3. Service Entry
4. Gateways
5. Sidecars

### Ingress Gateway
The entry point to the cluster. This is deployed in the `istio-system` namespace. This uses an Envoy proxy for the traffic coming from outside the cluster which is usually a loadbalancer(for external cloud based deployment) or a nodeport. We can use `istioctl` to inspect all the traffic flows that are being listed in the ingress gateway envoy filter. The process running inside the ingressgateway is the 
```bash
k exec -n istio-system deploy/istio-ingressgateway -- ps  
    PID TTY          TIME CMD
      1 ?        00:00:04 pilot-agent
     20 ?        00:00:21 envoy
     39 ?        00:00:00 ps
```
The `pilot-agent` bootstraps the envoy filter and creates the rules which can be view by
```bash
istioctl -n istio-system proxy-config route deploy/istio-ingressgateway
NAME     VHOST NAME     DOMAINS     MATCH                  VIRTUAL SERVICE
         backend        *           /stats/prometheus*     
         backend        *           /healthz/ready*        
```

The next chapter is to open up the traffic flow inside the cluster

### Gateway
Gateway are how traffic comes to the cluster and then it can be routed to a virtual service. The gateway opens up a specific port on the ingress-gateway for incoming traffic. once a gateway is deploy 
```bash
k get gateway
NAME                AGE
coolstore-gateway   63s
```

Now when we look at the envoy proxy-config we will see the port being opened 
```bash
istioctl -n istio-system proxy-config route deploy/istio-ingressgateway
NAME          VHOST NAME         DOMAINS     MATCH                  VIRTUAL SERVICE
http.8080     blackhole:8080     *           /*                     404
              backend            *           /stats/prometheus*     
              backend            *           /healthz/ready* 
```
**blackhole** is due to the absence of any routing to the upstream cluster. Therefore all the traffic is now passed to a blackhole of 404 so when you hit the endpoint `http://127.0.0.1:3000/` (port 3000 is due to the nodePort setup of istio-ingressgateway) we will see a 404


### Virtual Service
This routes the traffic from to specific services at the backend. It can be used to define routes to various real services based on the rules.In the VirtualService we will define the routes specified for the upstream traffic. Once the virtual service defines the traffic we can see the traffic routes in the proxy

```bash
istioctl -n istio-system proxy-config route deploy/istio-ingressgateway
NAME          VHOST NAME                       DOMAINS                     MATCH                  VIRTUAL SERVICE
http.8080     webapp.istioinaction.io:8080     webapp.istioinaction.io     /*                     webapp-vs-from-gw.istioinaction
              backend                          *                           /stats/prometheus*     
              backend                          *                           /healthz/ready* 
```
With the route set now the webpage can be viewed at `http://webapp.istioinaction.io:3000/` (here the http://weapp.istioinaction.io is pointing to 127.0.0.1 at `/etc/hosts`). 
### Destination Rule 
This handles traffic to the specific destination. This is behind the virtual service once the traffic is directed to specific host then the destination service can apply the rules to the traffic


### Service Entry
This is usually used to define a traffic leaving a cluster where a specific call in the cluster can be routed to an entry point pointing to the external cluster.

### sidecars
To define a special rules for the sidecars used by the istio







## Document
https://istio.io/latest/docs/concepts/traffic-management/ --> Traffic management read
https://banzaicloud.com/blog/backyards-ingress/  ---> Ingress Istio
https://istio.io/latest/docs/concepts/traffic-management/#virtual-services --> Virtual Service