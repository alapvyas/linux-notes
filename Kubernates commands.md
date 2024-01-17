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

