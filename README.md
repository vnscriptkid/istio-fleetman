# Istio learning

## concepts
- data plane: proxies
- control plane: pods run inside istio-system ns like istiod,...
- proxy (sidecar, envoy)
- kiali
    - how services are connected
    - how traffic goes between services
- prometheus
    - scrape metrics
- grafana
- telemetry
- traffic management
    - virtualservices: custom routing configurations (on proxies)
    - destinationrules: which pod goes in which subset
- trace
    - span
    - propagate headers
    - x-request-id
- canaries
    - approach 1 (purely k8s):
        - 1 service has multiple service pods
        - separate: 2 pods using stable build, 1 pod using risky build (all share the same label)
        - diff depl name
    - approach 2 (istio)
- session affinity
    - consistent hashing
    - doesn't work with weighted routing
- gateways:
    - ingress gateway (k8s)
    - istio gateway: custom routing rules for edge service in the cluster (to which clients hit directly)

## what
- tool that's deployed along with k8s
- features:
    - visibility on how reqs flow in cluster
    - error tracing
    - circuit breaker
    - timeout
    - ...

## notes

## setups
- `kubectl apply -f ./_course_files/1\ Telemetry/1-istio-init.yaml`
- `kubectl apply -f ./_course_files/1\ Telemetry/2-istio-minikube.yaml`
- `kubectl apply -f ./_course_files/1\ Telemetry/3-kiali-secret.yaml`
- `kubectl apply -f ./_course_files/1\ Telemetry/4-label-default-namespace.yaml` -> inject proxy to all pods inside ns
    - `kubectl describe ns default`
- `kubectl apply -f ./_course_files/1\ Telemetry/5-application-no-istio.yaml`
- `kubectl get pods -n istio-system`

## webapp
- `kubectl describe service fleetman-webapp`
- http://localhost:30080

## kiali
- `kubectl describe service kiali -n istio-system`
- http://localhost:31000

## Jaeger
- http://localhost:31001/jaeger/search

## grafana
- http://localhost:31002/?orgId=1

## Batch reqs using Bash
- `while true; do curl http://localhost:30080/api/vehicles/driver/London%20Riverside; echo; sleep 0.5; done;`

## TODO
- https://blog.risingstack.com/distributed-tracing-opentracing-node-js/
