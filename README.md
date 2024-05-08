# KEDA-LFEL1014
Scaling Cloud Native Applications with KEDA (LFEL1014)

### What is KEDA
- KEDA is short for Kubernetes Event-Driven Autoscaling
- It's a bridge between Kubernetes and event sources
- Empowers developers to scale their apps in response to workload changes due to some `events` (ex: change in message queue, incoming HTTP requests)
- It supports a wide range of **event sources** (ex: Azure Queues, RabbitMQ, Kafka )

---

### Autoscaling
- The capability of the system to adjust its resources (computing, storage, network bandwidth) based on the current load 
- In Kubernetes we can as en example adjust number of running pod instances based on resource usage

#### HPA in Kubernetes
- A controller that automatically scales the workload to match the demand
- Horizontal scaling means deploying more pods as a result of increased load
- HPA controller adjusts number of pods based on some observed metrics (ex: avg CPU utilization, avg Memory utilization)

#### KEDA Vs HPA
|                 |                                         KEDA                                        |                                       HPA                                       |
|:---------------:|:-----------------------------------------------------------------------------------:|:-------------------------------------------------------------------------------:|
| Scaling Trigger |   * Event driven <br> * Allows scaling based on custom metrics or external events   |         - Metric driven <br> - Scales based on CPU or Memory utilization        |
|   Versatility   |                        Supports broad range of event sources                        |                   Scales based on metrics associated with pods                  |
|    Use Cases    | Applications with variable workloads triggered by events (ex: message queue depths) | Applications with predictable scaling needs based on standard resource metrics. |

---

### How KEDA Works
1. **Agent**: `keda-operator` responsible for scaling
2. **Metrics**: KEDA exposes metrics (stream lag, message queue length) to HPA enabling it to scale the deployments, the container `keda-operator-metrics-apiserver` is responsible for metrics serving
3. **Admission Webhook**: KEDA can be used in conjunction with admission controller to automatically detect resource configuration changes, It also preserves a scale target from being scaled by multiple ScaledObjects.

#### ScaledObject
- Defines how a scale target (ex: deployment, custom resources, jobs or STS) must be scaled
- A scaler detects if a deployment should be activated or deactivated (ex: Google Cloud Platform Storage, memory, Redis, PostgreSQL)

#### KEDA CRDs
1. scaledobjects.keda.sh 
2. scaledjobs.keda.sh
3. triggerauthentications.keda.sh: used to secure communication between KEDA and external event sources (Ensuring only authenticated sources can trigger autoscaling)
4. clustertriggerauthentications.keda.sh