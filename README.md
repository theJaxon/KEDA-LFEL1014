# KEDA-LFEL1014
Scaling Cloud Native Applications with KEDA (LFEL1014)

### What is KEDA
- KEDA is short for Kubernetes Event-Driven Autoscaling
- It's a bridge between Kubernetes and event sources
- Empowers developers to scale their apps in response to workload changes due to some `events` (ex: change in message queue, incoming HTTP requests)

---

### Autoscaling
- The capability of the system to adjust its resources (computing, storage, network bandwidth) based on the current load 
- In Kubernetes we can as en example adjust number of running pod instances based on resource usage

#### HPA in Kubernetes
- A controller that automatically scales the workload to match the demand
- Horizontal scaling means deploying more pods as a result of increased load
- HPA controller adjusts number of pods based on some observed metrics (ex: avg CPU utilization, avg Memory utilization)

