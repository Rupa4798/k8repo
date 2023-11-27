# Kubernetes
## Official References
  - [Kubernetes Reference](https://kubernetes.io/docs/concepts/)
## Introduction to Kubernetes
  
### 1.0 What is Container?
- A container is a **lightweight, standalone, and executable software package** that contains everything needed to run a piece of software, including the **code, runtime, system tools, libraries, and settings.**
-  Containers are a form of virtualization that packages an application.
-  Its dependencies in an isolated environment, ensuring consistency and reproducibility across different computing environments.

#### How Docker and Kubernetes are related:
* Docker is an open-source platform used to handle software development.
* Its main benefit is that it packages the settings and dependencies that the software/application needs to run into a container, which allows for portability and several other advantages.
* Kubernetes allows for the manual linking and orchestration of several containers, running on multiple hosts that have been created using Docker. 

  #### Key characteristics of containers include:

**Isolation**:
-  Containers run in isolated environments, known as **container runtimes** (e.g., Docker, containerd), which share the same kernel as the host operating system but have separate user spaces.
-  This isolation ensures that one container's operations do not interfere with others.

**Portability**: 
- Containers are highly portable.
- They can run on any system that supports the container runtime, whether it's a developer's laptop, a data center server, or a cloud instance.
- This portability is enabled by packaging all dependencies within the container image.

**Consistency**: 
- Containers ensure consistent runtime environments across different stages of the software development lifecycle, from development and testing to production.
-  This consistency reduces "it works on my machine" issues.

**Efficiency**: Containers are lightweight and have low overhead because they share the host operating system's kernel. This makes them efficient in terms of resource usage, which allows running more containers on a single host.

**Scalability**: 
- Containers can be easily **scaled up** or **down to meet application demand**.
- Container orchestration platforms like Kubernetes manage the deployment, scaling, and management of containers.

**Versioning**:
- Container images are versioned, making it easy to roll back to a specific version of an application if issues arise.

**Security**: 
- Containers offer a level of security through isolation, but it's essential to follow best practices to ensure that containerized applications are properly secured.
- Tools like Docker Security Scanning and container security policies help enhance security.

Popular containerization technologies and tools include Docker, containerd, and Podman. Docker, in particular, played a significant role in popularizing containers and simplifying their use.

Containers have become a fundamental building block of modern software development and deployment. They facilitate DevOps practices, microservices architecture, and cloud-native application development by providing a consistent and efficient way to package and deploy applications, regardless of the underlying infrastructure.
  
### 1.1. What is Kubernetes?
- Kubernetes (often abbreviated as K8s) is an open-source container orchestration platform for **automating the deployment, scaling, management, and orchestration of containerized applications.** 
- Developed by Google and later donated to the Cloud Native Computing Foundation (CNCF), Kubernetes has become the industry standard for managing containerized workloads in both on-premises and cloud environments.
 #### Key features and concepts of Kubernetes include:

**Container Orchestration**: 
- Kubernetes manages the **deployment, scaling, and operation of containers.**
- It automates tasks like **container placement, scaling pods (groups of containers), and rolling updates.**

**Master-Worker Architecture**:
- Kubernetes operates on a **master-node architecture.**
- The master node **controls the cluster and makes decisions** about the desired state, while worker nodes (also called minions) execute those instructions.

**Container Abstraction**: 
- Kubernetes abstracts containers, allowing you to **deploy and manage applications without needing to worry about the underlying infrastructure**, which could be on-premises or in the cloud.

**Desired State Management**: 
- You define the desired state of your application, including the number of replicas, resource requirements, and other parameters, in declarative configuration files (YAML).
- Kubernetes continuously works to ensure that the actual state matches the desired state.

**Scalability**: Kubernetes can automatically scale applications based on CPU or memory usage, ensuring optimal resource allocation. It can also scale pods horizontally by adding or removing instances as needed.

**Service Discovery and Load Balancing**:
- Kubernetes provides **built-in service discovery** and **load balancing for pods.**
- This simplifies communication between components of an application.

**Self-Healing**:
- Kubernetes **monitors the health of containers **and restarts them if they fail.
-  It can also **perform rolling updates ** without downtime.

**Storage Orchestration**: 
- Kubernetes can manage storage volumes, allowing applications to request the storage they need.
- It supports various **storage providers**, including cloud and on-premises solutions.

**Networking**: 
- Kubernetes manages networking to ensure that pods can communicate with each other within the cluster.
-  It supports various **network models**, including overlay networks.

**Security**: 
- Kubernetes provides security features like role-based access control (RBAC), network policies, and the ability to run containers with different levels of privilege.

**Extensibility**: 
- Kubernetes is highly extensible.
- You can add functionality to your cluster through custom resources and operators, or you can use a wide range of plugins and extensions.

**Ecosystem**: 
- Kubernetes has a vibrant ecosystem with a variety of tools, libraries, and services that enhance its capabilities, such as Helm for package management and Prometheus for monitoring.


### 1.2. Why Use Kubernetes?
- Kubernetes is used by organizations of all sizes to manage containerized applications, and it is a critical component in the world of cloud-native and microservices-based application development.
- Kubernetes abstracts the complexities of managing containers at scale and helps ensure applications are highly available, reliable, and easily scalable.
  <img><img width="753" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/78a49d4d-9341-429a-a968-254b1d3ee8ab">
### What node in Kubernetes?
 * Node is the smallest fundamental unit of computing hardware.
 *  It represents a single machine in a cluster, which could be a physical machine in a data center or a virtual machine from a cloud 
  provider.
 *  Each machine can substitute any other machine in a Kubernetes cluster. The master in Kubernetes controls the nodes that have containers
### 1.3. Kubernetes Architecture

1. Control Plane
    -    The control plane is responsible for **container orchestration** and maintaining the **desired state of the cluster.**
3. Worker Node
    - The Worker nodes are responsible for **running containerized applications.**
 <img> <img width="1107" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/38bb8137-ab7a-4950-92b4-fd0ad6d04571">
 
1. kube-apiserver
   Kubernetes api-server is responsible for the following

    **API management**: Exposes the cluster API endpoint and handles all API requests.
    **Authentication** (Using client certificates, bearer tokens, and HTTP Basic Authentication) and Authorization (ABAC and RBAC evaluation)
    **Processing API** requests and validating data for the API objects like pods, services, etc. (Validation and Mutation Admission controllers)
    **It is the only component that communicates with etcd**
    **api-server** coordinates all the processes between the control plane and worker node components.
    **api-server** has a built-in bastion apiserver proxy. It is part of the API server process.
      It is primarily used to enable access to ClusterIP services from outside the cluster,     even though these services are typically only reachable within the cluster itself.
   
3. etcd
  -  distributed key-value store
  -  etcd **stores all configurations, states, and metadata of Kubernetes objects** (pods, secrets, daemonsets, deployments, configmaps, statefulsets, etc).
  -  etcd allows a client to **subscribe to events using Watch() API .**
  -  Kubernetes api-server uses the etcd’s watch functionality to **track the change in the state of an object.**
  - etcd exposes key-value API using gRPC. Also, the gRPC gateway is a RESTful proxy that translates all the HTTP API calls into gRPC messages.
  -  It makes it an ideal **database for Kubernetes.**
     etcd stores all objects under the /registry directory key in key-value format. For example, information on a pod named Nginx in the default namespace can be found under       
    /registry/pods/default/nginx
  NOTE: etcd it is the **only Statefulset component in the control plane.**
 4. kube-scheduler
  - It is responsible for scheduling Kubernetes pods on worker nodes.
  - When you deploy a pod, you specify the pod requirements such as CPU, memory, affinity, taints or tolerations, priority, persistent volumes (PV),  etc.
  - The scheduler’s primary task 
   is to identify the create request and choose the best node for a pod that satisfies the requirements.
<img> <img width="743" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/2e29b518-9f44-4e05-987b-c5b9bd6313a9">


5. Kube Controller Manager
   - The controller manager is a daemon that is used for embedding core control loops, garbage collection, and Namespace creation. It enables the running of multiple processes on the master node even though they are compiled to run as a single process.
   - Controllers are control loops that watch the state of your cluster, then make or request changes where needed.
   - Each controller tries to move the current cluster state closer to the   desired state.
   - [Let’s say you want to create a deployment, you specify the desired state in the manifest YAML file (declarative approach). For example, 2 replicas, one volume mount, configmap, etc. The in-built deployment controller ensures that the deployment is in the desired state all the time. If a user updates the deployment with 5 replicas, the deployment controller recognizes it and ensures the desired state is 5 replicas.]
     <img> <img width="415" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/85281396-d0ce-44b9-9a51-a8ddff7fe5b5">
Following is the list of important built-in Kubernetes controllers.
- Deployment controller
- Replicaset controller
- DaemonSet controller 
- Job Controller (Kubernetes Jobs)
- CronJob Controller
- endpoints controller
- namespace controller
- service accounts controller.
- Node controller
  It manages all the controllers and the controllers try to keep the cluster in the desired state. <br>
  
  ** Namespace ** <br>
  * Namespaces are used for dividing cluster resources between multiple users.
  * They are meant for environments where there are many users 
 spread across projects or teams and provide a scope of resources.
 Initial Namespace are:
    - Default
    - Kube – system
    - Kube – public
  
7. Cloud Controller Manager (CCM)
  -  You must have heard about Public, Private and hybrid clouds.
  -  With the help of cloud infrastructure technologies, you can run Kubernetes on them.
  -  In the context of Cloud Controller Manager, it is the control panel component that embeds the cloud-specific control logic.
  -   This process lets you link the cluster into the cloud provider's API and separates the elements that interact with the cloud 
 platform from components that only interact with your cluster. 

This also enables the cloud providers to release the features at a different pace compared to the main Kubernetes project. It is structured using a plugin mechanism and allows various cloud providers to integrate their platforms with Kubernetes.
   - When kubernetes is deployed in cloud environments, the cloud controller manager acts as a **bridge between Cloud Platform APIs and the Kubernetes cluster.**
   - This way the core kubernetes core components can work independently and allow the cloud providers to integrate with kubernetes using plugins. (For example, an interface between kubernetes cluster and AWS cloud API)
   - Cloud controller integration allows Kubernetes cluster to provision cloud resources like instances (for nodes), Load Balancers (for services), and Storage Volumes (for persistent volumes).


   
  #### Kubernetes Worker Node Components
  The Worker nodes are responsible for running containerized applications.
1. Kubelet
   - Kubelet is an **agent component that runs on every node in the cluster.** It does not run as a container instead runs as a daemon, managed by systemd.
   - It is responsible for registering worker nodes with the API server and working with the podSpec (Pod specification – YAML or JSON) primarily from the API server.
     kubelet is responsible for the following.
      a. Creating, modifying, and deleting containers for the pod.
      b. Responsible for handling liveliness, readiness, and startup probes.
      c. Responsible for Mounting volumes by reading pod configuration and creating respective directories on the host for the volume mount.
      d. Collecting and reporting Node and pod status via calls to the API server.
     <img> <img width="448" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/721880d2-f6cf-46f4-8f6f-9f0833f10673">

3. Kube proxy
   kube-proxy is a **network proxy component** that runs on each worker node within the cluster.
   - Its primary function is **to maintain network rules on the host and enable network communication to and from individual pods.**
   
   - Kube-proxy is a daemon that runs on every node as a daemonset. It is a proxy component that implements the Kubernetes Services concept for pods. (single DNS for a set of pods 
  with load balancing). It primarily proxies UDP, TCP, and SCTP and does not understand HTTP.

 - When you expose pods using a Service (ClusterIP), Kube-proxy creates network rules to send traffic to the backend pods (endpoints) grouped under the Service object. Meaning, all 
  the load balancing, and service discovery are handled by the Kube proxy.

The key functions of kube-proxy in Kubernetes are as follows:

**Service Load Balancing**: One of the primary roles of kube-proxy is to implement service load balancing. When you create a Kubernetes Service object, it is associated with a set of pods. The kube-proxy ensures that incoming network traffic to a service is properly load-balanced across the pods in the service. It sets up rules in the host's network stack to forward traffic to the correct pod, distributing traffic evenly to achieve service redundancy and high availability.

**Pod-to-Pod Communication**: kube-proxy helps enable communication between pods in different nodes. It sets up rules to perform source network address translation (SNAT) or destination network address translation (DNAT) to make sure that pods can reach each other across different nodes while keeping their IP addresses consistent.

**Service Discovery**: When a pod wants to communicate with a service, it can do so using the service's DNS name. kube-proxy ensures that DNS requests for services are resolved to the appropriate IP addresses of the pods that make up the service.

**Node Port Services**: For services of type "NodePort," kube-proxy is responsible for configuring a port on the host machine, which can be used to access services from outside the cluster. It forwards traffic from the node's IP and port to the appropriate service, thus exposing the service to external clients.

**Session Affinity**: kube-proxy supports session affinity (also known as client IP affinity) for services. This means that it can be configured to route requests from a particular source IP to the same pod in order to maintain state or session consistency.

**Health Checks**: kube-proxy continuously monitors the health of pods associated with a service. If a pod becomes unhealthy, it adjusts the network rules to stop directing traffic to the failing pod, ensuring that traffic is only sent to healthy pods.

**Rule Management**: kube-proxy dynamically manages and updates the rules in the host's network stack to reflect the changing state of the cluster. It observes the Kubernetes API server for changes in service and endpoint configurations and reacts accordingly to ensure the network traffic is routed correctly.

5. Container Runtime
As Java Runtime (JRE). It is the software required to run Java programs on a host.
In the same way, container runtime is a software component that is required to run containers.
- Container runtime runs on all the nodes in the Kubernetes cluster. It is responsible for pulling images from container registries, running containers, allocating and isolating resources for containers, and managing the entire lifecycle of a container on a host.
**how does Kubernetes make use of the container runtime?**
  The kubelet agent is responsible for interacting with the container runtime using CRI APIs to manage the lifecycle of a container. It also gets all the container information from the container runtime and provides it to the control plane.
<img> <img width="585" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/b191c46c-a0ce-4b19-a760-478e1f77d1b5">

Let’s take an example of CRI-O container runtime interface. Here is a high-level overview of how container runtime works with kubernetes.
1. When there is a new request for a pod from the API server, the kubelet talks to CRI-O daemon to launch the required containers via Kubernetes Container Runtime Interface.
2. CRI-O checks and pulls the required container image from the configured container registry using containers/image library.
3. CRI-O then generates OCI runtime specification (JSON) for a container.
4. CRI-O then launches an OCI-compatible runtime (runc) to start the container process as per the runtime specification.

### Heapster in Kubernetes
* A Heapster is a performance monitoring and metrics collection system for data collected by the Kublet.
* This aggregator is natively supported and runs like any other pod within a Kubernetes cluster, which allows it to discover and query usage data from all nodes within the cluster.
* 
### Summary:

<img> <img width="1356" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/243e93cf-eecd-49f6-936e-469defebda5d">


<img> <img width="1368" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/8e8ee960-6648-4507-86dc-c05976ae0904">


<img> <img width="1360" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/1f2fcbe7-0207-46c1-8ac5-23307419b76c">


<img> <img width="1402" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/9d7ecc7d-d794-4482-be7c-745fc670d0d3">

### Master and Worker together
<img> <img width="880" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/63e39ce3-0443-4888-8675-de0471fd0d99">

 
### 1.4. Kubernetes Features and Benefits
 Advanages Summary
  - <img> <img width="377" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/005cedbe-c288-44e8-9673-8d3fe6c1c3e7">

### 1.5 The Declarative Model and Desired State
In the context of Kubernetes, the declarative model and desired state are fundamental concepts that underpin how the platform manages containerized applications and infrastructure. These concepts are essential for understanding how Kubernetes ensures that your application remains in a desired state, regardless of external factors or failures. Let's explore these concepts in more detail:

#### Declarative Model:
- In Kubernetes, you describe the desired state of your application and infrastructure in a declarative manner. This means you specify what you want the system to look like, rather than providing a sequence of steps to achieve that state.
- You define the desired state using YAML or JSON files, which include information about the containerized applications, pods, services, deployments, and other resources.
  
This declarative approach is opposed to an imperative model, where you specify a series of actions to reach a desired state. Kubernetes abstracts away the underlying infrastructure and focuses on what should be achieved, not how to achieve it.
Desired State:

<img width="744" alt="image" src="https://github.com/Ashujauhari/Kubernetes2023/assets/27730844/e60abd6c-4805-4894-8b58-16f327dcf117">

#### Desired State
  - The desired state in Kubernetes refers to the state that you have declared in your YAML or JSON resource manifests.
  - It defines how your application should run and what resources it should use.

* Kubernetes continuously works to reconcile the current state of the system with the desired state. If there are any deviations, Kubernetes takes actions to correct them.
* Kubernetes controllers, which are control loops responsible for managing resources like Pods, ReplicationControllers, Deployments, and StatefulSets, play a crucial role in maintaining the desired state.

#### How the Declarative Model and Desired State Work Together:

**Resource Declaration**: You create resource manifests (e.g., Pod, Deployment, Service) that describe the desired state of your application and infrastructure. You specify the number of replicas, resource requirements, container images, and more in these manifests.

**Kubernetes Control Loop**: Kubernetes has control loops for each resource type. These control loops continuously compare the current state of the cluster to the desired state defined in the resource manifests.

**Reconciliation**: If there are discrepancies between the current state and the desired state, the control loop takes corrective actions to bring the system in line with the declared state. For example, if a Pod crashes, a Deployment controller ensures that a new Pod is created to replace it.

**Idempotent Operations**: Kubernetes performs operations in an idempotent manner. This means that even if the system is repeatedly reconciled, it should eventually reach the same desired state without unintended side effects.
