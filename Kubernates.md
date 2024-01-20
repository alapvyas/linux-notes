## Kubernates useful commands

```kubectl get nodes```

This is to get the number of nodes in the cluster

```kubectl get pod```

This is to get the pods in the cluster

```kubectl get service```

This is to get services in the cluster. 

```kubectl create deployment``` | ```kubectl get deployment```

In Kubernates, you don't (You can though!) create pods as pods are the smallest units of a Kubernates cluster.
You would instead create a deployment. 

```kubectl get replicaset```

It gets the replicasets created by the deployment. 

```kubectl create deployment nginx-depl --image=nginx```

Example of how to create a deployment

```kubectl edit deployment nginx-depl```

To edit the deployment. 

```kubectl logs <pod name>```

To check logs of the applications in the pod

```kubectl describe pod <pod name>```

To get a proper description of the pod. 

```kubectl exec -it <pod name> -- /bin/bash```

To exec into a pod. 

```kubectl delete deployments <name of deployment>```

To delete a deployment

```kubectl apply -f <nameofthefile.yaml>```

Instead of passing all arguments in a single command, its easier to configure deployments in a file in yaml and
then run the file instead. If any changes are required, you can always edit the file and run it again. Basically,
you can create and update deployments with this. 

```kubectl create namespace <name>``` | ```kubectl get namespace```
To create and get namespaces. 

``` kubectl api-resources -namespace=true``` | ``` kubectl api-resources -namespace=fales```

To check the resources in namespaces. 

```kubectl apply -f <filename> --namespace=<nameofnamespace>```

To create a component in a namespace. (Not recommended though. Better practice to define it in the configuration file instead.)

```kubectl get svc```

To get services 


## Kubernetes Configuration Files: An Overview

Kubernetes configuration files are used to create, modify, and manage Kubernetes objects like pods, services, and deployments. These files are typically written in YAML, which is a human-readable data serialization standard.

### Key Characteristics

1. **YAML Format**: YAML is preferred due to its readability and support for complex data structures.
2. **Declarative Syntax**: Kubernetes configurations are declarative, meaning you describe the desired state rather than the steps to achieve it.
3. **Resource Definitions**: Each file typically defines a single Kubernetes resource (like a pod or service).

## Important Components

### Metadata
- **`apiVersion`**: Specifies the Kubernetes API version (e.g., `v1`, `apps/v1`).
- **`kind`**: The type of resource (e.g., Pod, Service, Deployment).
- **`metadata`**: Includes names, namespaces, labels, and annotations.

### Spec and Status
- **`spec`**: Describes the desired state of the resource.
- **`status`**: Reflects the current state of the resource (usually set by Kubernetes and read-only).

### Pod Configuration
- **Containers**: Define the containers that run in the pod.
- **Volumes**: Specify the storage volumes attached to the pod.

### Service Configuration
- **Type**: Determines how the service is exposed (ClusterIP, NodePort, LoadBalancer).
- **Selector**: Maps the service to specific pods.

### Deployment Configuration
- **Replicas**: Number of pod instances.
- **Selector**: Defines how to identify pods to manage.
- **Template**: The template for creating new pods.

## Kubernetes Namespaces

### Overview
Kubernetes namespaces provide a mechanism for isolating groups of resources within a single cluster. They are useful in scenarios where multiple teams or projects share a Kubernetes cluster and need a way to divide cluster resources. Using multiple namespaces allows you to split complex systems with numerous components into smaller distinct groups. They can also be used for separating resources
in a multi-tenant environment, splitting up resources into production, development,
and QA environments, or in any other way you may need. Resource names only need
to be unique within a namespace. Two different namespaces can contain resources of
the same name. But, while most types of resources are namespaced, a few aren’t. One
of them is the Node resource, which is global and not tied to a single namespace.

### Characteristics of Kubernetes Namespaces

1. **Isolation**: Namespaces provide a logical separation between different teams, projects, or stages of deployment. For example, you could have separate namespaces for development, testing, and production environments.

2. **Resource Management**: They allow for more granular control over resources. Resource quotas can be set on a per-namespace basis, ensuring that one namespace doesn’t consume more than its fair share of cluster resources.

3. **Access Control**: Namespaces can be used to scope access control permissions. Roles and RoleBindings in Kubernetes can be namespace-specific, allowing for fine-grained control over who can access what resources.

4. **Simplified Resource Naming**: Within a namespace, resources only need to have unique names within that namespace, not across the entire cluster. This simplifies resource naming conventions.

5. **Network Policies**: Namespaces enable you to implement network policies that control the communication between pods across different namespaces.


## Default Namespaces
Kubernetes comes with a few default namespaces that are used for different purposes. Understanding these namespaces is important for effectively managing and organizing resources within a Kubernetes cluster.


### 1. `default`

- **Purpose**: This is the default namespace for objects with no other namespace.
- **Usage**: Any resource created without a specified namespace is automatically placed into the `default` namespace. It's commonly used for general-purpose or development workloads.
- **Consideration**: Since it’s the default catch-all namespace, it can become cluttered if not managed properly.

### 2. `kube-system`

- **Purpose**: The `kube-system` namespace contains objects created by the Kubernetes system, typically system-level resources.
- **Usage**: This includes resources like the DNS server, metrics server, and various controllers. These are essential for the functioning of the Kubernetes cluster.
- **Consideration**: Users should be cautious about modifying resources in this namespace as it can affect the cluster's stability and functioning.

### 3. `kube-public`

- **Purpose**: This namespace is automatically created and is readable by all users (including those not authenticated).
- **Usage**: It's mostly used for public resources, like the cluster's public ConfigMap.
- **Consideration**: Since it's public, sensitive data should not be stored in this namespace.

### 4. `kube-node-lease`

- **Purpose**: Used for node heartbeats. Each node in the cluster has an associated Lease object in this namespace.
- **Usage**: It helps the Kubernetes scheduler in determining node availability and managing node lifecycles more efficiently.
- **Consideration**: This namespace is specifically for system use and typically doesn't require user intervention.

## Kubernetes Ingress Explained  

### Overview
- **Purpose**: Kubernetes Ingress is used to manage external access to the services in a Kubernetes cluster.
- **Functionality**: It primarily handles HTTP and HTTPS traffic routing to different services based on the incoming URL.

### Key Components
1. **Ingress Resources**: Define rules for traffic routing.
2. **Ingress Controller**: A pod that implements the rules set in the Ingress, typically using a load balancer or a reverse proxy.
3. **Annotations**: Used to customize behavior of Ingress, depending on the Ingress controller.

### How It Works
- **Routing Traffic**: Routes external requests to the appropriate services based on the defined rules.
- **Load Balancing**: Can provide load balancing, SSL termination, and name-based virtual hosting.

## Advantages
- **Centralized Management**: Offers a single resource to manage access to multiple services.
- **Scalability**: Facilitates scaling of web applications.
- **Security**: Can be configured to give services externally-reachable URLs, load balance traffic, terminate SSL, and offer name-based virtual hosting.

### Use Cases
- **Single Service Access**: Expose a single service for a web application.
- **Path-Based Routing**: Route traffic to different services based on the URL path.
- **Name-Based Virtual Hosting**: Host multiple domains using a single IP address.

### Implementation
- **Define Ingress Resource**: Create a YAML file to define the Ingress resource with the desired rules.
- **Deploy Ingress Controller**: Choose and deploy an Ingress controller like NGINX or Traefik.
- **Apply Ingress Resource**: Apply the Ingress resource to your Kubernetes cluster using `kubectl apply`.

### Limitations
- **Dependency on Ingress Controller**: Requires a specific Ingress controller to be deployed in the cluster.
- **Complex Configurations**: Complex routing logic might require additional configurations or custom annotations.

## Deploying resources through Helm

Helm is a package manager for Kubernetes (similar to OS package managers like yum or apt in Linux or homebrew in MacOS).

Helm is comprised of two things:

    A helm CLI tool (the client).
    Tiller, a server component running as a Pod inside the Kubernetes cluster.

Those two components are used to deploy and manage application packages in a Kubernetes cluster. Helm application packages are called Charts. They’re combined with a Config, which contains configuration information and is merged into a Chart to create a Release, which is a running instance of an application (a combined Chart and Config). You deploy and manage Releases using the helm CLI tool, which talks to the Tiller server, which is the component that creates all the necessary Kubernetes resources defined in the Chart, 

## Volumes: 

Kubernetes volumes are a component of a pod and are thus defined in the pod’s specification—much like containers. They aren’t a standalone Kubernetes object and cannot be created or deleted on their own. A volume is available to all containers in the pod, but it must be mounted in each container that needs to access it. In each container, you can mount the volume in any location of its filesystem.

**emptyDir**—A simple empty directory used for storing transient data.

**hostPath**—Used for mounting directories from the worker node’s filesystem into the pod.

**gitRepo**—A volume initialized by checking out the contents of a Git repository.

**nfs**—An NFS share mounted into the pod.

**gcePersistentDisk (Google Compute Engine Persistent Disk), awsElasticBlockStore (Amazon Web Services Elastic Block Store Volume), azureDisk (Microsoft Azure Disk Volume)**—Used for mounting cloud provider-specific storage.

**cinder, cephfs, iscsi, flocker, glusterfs, quobyte, rbd, flexVolume, vsphere**-Volume, photonPersistentDisk, scaleIO—Used for mounting other types of network storage.

**configMap, secret, downwardAPI**—Special types of volumes used to expose certain Kubernetes resources and cluster information to the pod.

**persistentVolumeClaim**—A way to use a pre- or dynamically provisioned persistent storage. 

Using PersistentVolumes and PersistentVolumeClaims makes it easy to obtain persistent storage without the user having to deal with the actual storage technology used underneath. But this still requires a cluster administrator to provision the actual storage up front. Kubernetes can also perform this job automatically through dynamic provisioning of PersistentVolumes. You can deploy a PersistentVolume provisioner and define one or more StorageClass objects to let users choose what type of PersistentVolume they want. The users can refer to the StorageClass in their PersistentVolumeClaims and the provisioner will take that into account when provisioning the persistent storage.

## StatefulSet in Kubernetes

StatefulSet is a Kubernetes workload API object used to manage stateful applications. Unlike Deployment and ReplicaSet, which are intended for stateless applications, StatefulSet is ideal for applications that require a stable, unique network identifier, persistent storage, and orderly, graceful deployment and scaling.

  -**Stable, Unique Network Identifiers**: Each pod in a StatefulSet derives its hostname from the name of the StatefulSet and the ordinal of the pod. The pattern for the constructed hostname is $(statefulset name)-$(ordinal). This ensures that each pod in a StatefulSet has a unique and predictable name, which is crucial for stateful applications like databases that rely on stable identifiers.

   - **Stable, Persistent Storage**: StatefulSet allows you to assign PersistentVolumes to each pod via PersistentVolumeClaims. When a pod is (re)scheduled onto a node, its volume mount will have the same data as before, which is essential for stateful services that need to maintain their state across restarts.

   - **Ordered, Graceful Deployment and Scaling**: Pods in a StatefulSet are created, scaled, and deleted in a predictable order. When scaling down, the pods are terminated in reverse ordinal order. This orderly execution is critical for stateful apps that require careful handling of startup and shutdown sequences.

   - **Ordered, Automated Rolling Updates**: When the StatefulSet’s pod template is updated, each pod is updated in reverse ordinal order, with the next pod updated only after the current pod is running and ready.
	
## Kubernetes Services

Kubernetes Services are an abstract way to expose an application running on a set of Pods as a network service. With Kubernetes, you don't need to modify your application to use an unfamiliar service discovery mechanism. Kubernetes provides Pods with their own IP addresses and a single DNS name for a set of Pods and can load-balance across them.

- **Service Discovery and Load Balancing:** Kubernetes gives Pods their own IP addresses and a single DNS name for a set of Pods and can load-balance across them.

- **Stable Network Interface:** Services provide a stable IP address and port combination which remains consistent even as the pods they represent are updated or replaced.

### Different Service Types:
	
- **ClusterIP:** Exposes the Service on a cluster-internal IP. This type makes the Service only reachable from within the cluster.
- **NodePort:** Exposes the Service on each Node's IP at a static port. A ClusterIP Service is created automatically, and the NodePort Service will route to it.
- **LoadBalancer:** Exposes the Service externally using a cloud provider's load balancer. NodePort and ClusterIP Services are created automatically.-
