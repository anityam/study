# Envoy

Envoy is the backbone of the Istio service mesh. It is an open source project that lives in https://envoyproxy.io .

It is a transparent proxy. The main concept of which was established to create a transparent network proxy which is easy to debug. A proxy is a middleman that sits between the client and the server and through which the traffic flows for the communication between server and client.
 Client ---> Proxy ---> Server
 Technically a proxy can stand between the client and server and simplify the setting. The communication logic can be placed in the proxy without the server and client having to delete with the communication logic and able to focus on their specific client or server based logics.

## Concept
 Envoy is designed as an application level proxy and can understand the layer 7 protocols. It can be extended to understand other level proxies. Lot of more telemetries come out of box due to Envoy understanding application level protocols


## Feature
Listeners --> ports where downstream(something sending information from to the server or to the )
Routes --> The route setup for the downstream routes to be moved to the upstream clusters
Clusters --> the server portion or the 

### Service Discovery
It uses service discovery api to look for the service. 

### Load Balancing
It uses local-aware load balancing. Can be configured to use other routing strategies.

### Traffic and Request Routing
Sophisticated routing rules since it can understand L7 protocols like HTTP/1 or HTTp/2

### Traffic Shifting and Shadowing
Envoy can split traffic based on weight and also move copy of traffic to certain version( only a copy of the traffic the real flow still can use the other version)

### Network Resilience
Retries, timeouts, Health checks can be configured in Envoy.

### Metrics
It can generate a lot of metrics

### Tracing
It will generate x-request-id header to trace traffic.

### Tls and Mutul Tls, Tls termination 

### Rate limiting


## Documents 

https://envoyproxy.io ---> the main place for envoy
https://www.envoyproxy.io/docs/envoy/v1.27.0/intro/arch_overview/intro/terminology --> docs