---
title: "Understanding Kubernetes Services: Deploying a Django Todo Web App Step-by-Step"
datePublished: Wed Sep 13 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clmjfq28t000i0amr94gcdvut
slug: understanding-kubernetes-services-deploying-a-django-todo-web-app-step-by-step
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1694711722981/78da9534-07e6-4c41-b33e-535102e2b7b8.png
tags: django, kubernetes, devops, 90daysofdevops, day34

---

---

# 📍Introduction

Welcome to my Kubernetes blog series, where I share my Kubernetes learnings and try to deep dive into topics. In this blog, we will explore the K8s service in detail and understand the difference between them by doing a hands-on project of deploying a Django Todo Web Application. Let's get started!🚀

---

# 📍Types of Services:

There are 4 types of services:

1. **ClusterIP**
    
2. **NodePort**
    
3. **LoadBalancer**
    
4. **ExternalName**
    

We will be seeing about the first 3 services with a hands-on project.

## ✔Cluster IP

The default type of service is ClusterIP so there is no need to mention the type while defining this service type. ClusterIP service provides a service proxy using the Cluster IP address to access the application at the service port. This solves the issue of directly accessing the pod IP address which is dynamically allocated causing it to change when the pod is crashed. It provides access to the application inside the cluster therefore, you can access it only when you are logged in to your K8s Cluster.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694611684450/8262e97b-ef1f-4ef5-ab3c-4ec0d3f06000.png align="center")

If you are using **Minikube** you can log into the cluster using the `minikube ssh` command. If you are using **Kubeadm** there is no need for login. It is mainly used for intra-cluster communication between pods or services. **Examples**: Database services, and microservices communication.

ClusterIP service provides the following functionalities:

* Service Discovery
    
* Load Balancing
    

## ✔NodePort

The NodePort service is mainly used to access our application outside the K8s cluster i.e. without logging into the cluster. When we define a `NodePort` service exposes a port `nodePort` that we had defined in its manifest files on all the nodes, where we can access the application using the **Node IP**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694611691316/6338bd88-8ddc-44c3-aec1-a1b8388ed0d8.png align="center")

The `nodePort` defined in its Manifest file ranges between **30000-32767**. It can be used by the organization. It is useful for development and testing or when you need external access to services in a non-production environment. **Examples**: Web applications, and APIs for testing.

NodePort service provides the following functionalities:

* Service Discovery
    
* Load Balancing
    
* Exposing to the organization.
    

## ✔LoadBalancer

We were accessing the application within the cluster or the organization using the above 2 services. To access the application outside the system by an external user who can use a Public IP we use the **LoadBalancer** service. There are some other methods to make the application running inside a cluster externally accessible. This service can only be used when you are running the Kubernetes cluster on any Cloud Service Provider Platform like **AWS**, **Azure**, **Google Cloud**, **etc**.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694702653223/f877efd3-301c-47d2-a272-4c140a0aa5ae.png align="center")

Kubernetes does not provide a load balancing component, LoadBalancer service helps us to use a Load balancing component of the Cloud Service. This component allows the external traffic coming from the **User** via the **Public/External IP** to access the application from the browser.

LoadBalancer service provides the following functionalities:

* Service Discovery
    
* Load Balancing
    
* Exposing to the outside world
    

For the **ExternalName** service, you can visit the **official Kubernetes documentation** on services: [K8s Services](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer)

Now let's do a hands-on project and understand the above services in practice.🚀

---

# 📍Django Todo Web Application

`Step 1`: Set Up a Minikube or a Kubeadm cluster on your AWS EC2 instance. I will be executing this project on Minikube. You can refer to this guide: [https://github.com/LondheShubham153/kubestarter](https://github.com/LondheShubham153/kubestarter)

`Step 2`: Clone the project using the `git clone <HTTP_URL>` from this GitHub repository: [https://github.com/LondheShubham153/django-todo-cicd](https://github.com/LondheShubham153/django-todo-cicd)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707046241/1bb15dec-fb91-465e-85fb-5c4997412fde.png align="center")

`Step 3`: Go to the `k8s` directory inside the project:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707131323/10ac9d38-07a5-4c1c-9fc7-75802fc76f96.png align="center")

`Step 4`: Modify the `deployment.yml` file by adding a `django` namespace. Copy the below manifest file inside the `deployment.yml` file using the Vim editor.

```yaml
apiVersion: apps/v1

kind: Deployment

metadata:

  name: todo-deployment

  namespace: django

  labels:

    app: todo-app

spec:

  replicas: 3

  selector:

    matchLabels:

      app: todo-app

  template:

    metadata:

      namespace: django

      labels:

        app: todo-app

    spec:

      containers:

      - name: todo-app

        image: trainwithshubham/django-todo:latest

        ports:

        - containerPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707382137/17cd7e0a-9667-4c27-8c82-194c95fee736.png align="center")

`Step 5`: Similarly modify the `service.yml` file by adding the `django` namespace with the following content.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: todo-service
  namespace: django
spec:
  type: NodePort
  selector:
    app: todo-app
  ports:
      # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
    - port: 80
      targetPort: 8000
      # Optional field
      # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
      nodePort: 30007
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707444517/7258a410-7bdd-4495-9474-e0c691dc273b.png align="center")

`Step 6`: Create the `django` namespace using the command `kubectl create namespace django` and verifying the namespace using the `kubectl get namespace` command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707579545/4570aa87-fb58-459d-a4c4-8543ab3ebe72.png align="center")

`Step 7`: Apply the deployment manifest using the `kubectl apply -f <fileame>` command and verify the applied deployment using `kubectl get deployment -n django`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707706543/40268d54-2483-4356-b7ea-fe12f2df6901.png align="center")

Wait for the pods to be running keep verifying using the above command till you see the deployment and pods in the running state:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707802194/1727bcda-7d83-40b9-9977-2b0f2e035b3b.png align="center")

Once the pods are running we can access the application running on any of the pods using the pod IP.

`Step 8`: Use the `kubectl get pods -n django -o wide` command to get the pod IP:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694707971822/3e3a7022-6199-4025-96ce-dec0ff4fcd31.png align="center")

`Step 9`: Open a separate terminal of the same instance where Minikube is running, log in to the cluster using `minikube ssh` command and access the application using the command `curl -L <PodIP>:<containerport>`:

`curl -L <podIP>:8000`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694708194474/4551c587-3709-4ee8-ae25-26b86ea2909d.png align="center")

You can try to access the application outside the cluster you cannot:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694708310986/5d991281-aef2-4790-a8aa-944aa7a92d15.png align="center")

Let's see in practice how the pod IP is changed when a new pod is created once we delete a pod:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694708501830/49b646e7-7a62-42f7-8bf2-b455e0e8bfbf.png align="center")

And if you try to access the pod with the **IP** `10.244.0.5` you cannot since that pod is deleted.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694708940112/354437fe-97e6-4e1c-9433-41d67a1e47f4.png align="center")

Accessing the application with the newly created Pod IP:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709093295/b0a07054-00a0-4ce5-a070-45622ed478c4.png align="center")

Here, we have deleted the pod manually but in production, there will be many scenarios where a pod gets crashed and if the user tries to access the pod using the Pod IP it will not be able to. Therefore, let's create a Service and apply it.

We will be creating a ClusterIP service i.e. the default service:

`Step 10`: Create a `svc.yml` file and copy the below Service Manifest file and apply it:

( Try to write the service file on your own, to learn how to write a manifest file you can refer to my blog: [Kubernetes Fundamentals: Understanding Pods, Deployments, Services, and Manifests](https://varunmargam.hashnode.dev/kubernetes-fundamentals-understanding-pods-deployments-services-and-manifests) )

```yaml
apiVersion: v1
kind: Service
metadata:
  name: todo-service
  namespace: django
spec:
  selector:
    app: todo-app
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8000
  type: ClusterIP
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709054434/0edde12b-9b7f-404d-9e86-6326e97be0c5.png align="center")

Verify the service using the command `kubectl get svc -n django`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709174772/2203749d-c91d-4463-8d69-5b53a323d4e4.png align="center")

`Step 11`: Access the application using the `ClusterIP` at the port defined in the service manifest file, where the service is listening at `port 80` i.e. the default HTTP port, therefore, you can even directly access only using the ClusterIP (Login to your Minikube cluster ):

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709399702/6921afc2-6c8a-4958-84e5-2ec4b829b158.png align="center")

If you are using **Kubeadm** then no need to log in to the cluster.

Now that our service has been defined we can access the application regardless of the Pod IP changes since the service uses service discovery i.e. labels as a selector to apply the service.

Let's try and apply a Service of type **NodePort** and access the application outside the cluster without logging into it:

`Step 12`: Delete the **ClusterIP** service using `kubectl delete svc <service_name> -n <namespace>`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709703793/480705ab-3c6c-4e3c-93e8-8c7e38c5c988.png align="center")

`Step 13`: Apply the `service.yaml` file i.e. NodePort service present in the `k8s` directory

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709805641/c2ebfe8b-161d-4252-bb83-c368c83ba572.png align="center")

`Step 14`: Now, access the application using the `NodeIP` at the `nodePort`. Getting the NodeIP:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694709917265/043bfd2a-8f24-4229-801b-c28d6d209d39.png align="center")

`Step 15`: Access the application using `curl -L <NodeIP>:<nodePort>`. In our case the nodePort is `30007` defined in the service file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710049792/8724f27c-ed8e-4c1d-ba5a-734bdc953f81.png align="center")

You can also try to access it on the browser using the same IP, make sure you allow the inbound traffic at `port 30007` ( `https://<NodeIP>:<nodePort>` on the browser )

Now, let's try to access the application using a public IP with LoadBalancer service making it accessible for external users.

`Step 16`: Delete the **NodePort** service using `kubectl delete svc <service_name> -n <namespace>`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710155066/86dbea51-cb70-4c11-8b10-17b33f755896.png align="center")

`Step 17`: Create a `service2.yml` file and copy the below LoadBalancer Manifest file into it:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: todo-service
  namespace: django
spec:
  selector:
    app: todo-app
  type: LoadBalancer
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710290352/3ca57ce3-22df-48ae-8dc1-ad82e97555b8.png align="center")

`Step 18`: Apply this `service2.yml` manifest file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710350368/742f96b7-0dcf-42b0-ab8a-ffa32ee8e971.png align="center")

`Step 19`: Go to your second terminal and execute the `minikube tunnel` command. Make sure that you have allowed incoming traffic to `port 80` at the inbound rules in the security group of your EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710515802/0a0bf008-a16d-4db1-afac-c7f1317e7454.png align="center")

`Step 20`: After this, you will see the External IP:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710551799/962c11f5-6386-464e-9211-4c2299a35a5b.png align="center")

Now, you can access the application using this `External IP` at the `port 80` or at `31748`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710684575/edcc5abd-4ffd-4a32-8645-8f1ecb9516e6.png align="center")

---

# 📍Facing an issue

I am unable to access the application using the external IP from the above Load Balancer service from my browser:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710798570/fca4d090-8c5c-4ece-9055-bac98685bca6.png align="center")

I am unable to ping from my local machine to the External IP even after adding ICMP rule to the security group of my instance (One of the solutions I got from the ChatGPT)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1694710970959/428651cd-0e75-4a61-936e-2672eb84fb8d.png align="center")

I am unable to troubleshoot this issue, I would highly appreciate your advice or suggestions regarding how to troubleshoot this issue in the comments section.

---

# 📍Conclusion

Thank you for reading this blog! 📖 Hope you have gained some value. If you want to practice Kubernetes make sure you do it on Minikube or at [killercoda.com](https://killercoda.com/) where you get K8s playground for free.

If you enjoyed this blog and found it helpful, please give it a like 👍, share it with your friends, share your thoughts, and give me some valuable feedback.😇 Don't forget to follow me for more such blogs! 🌟

---

# 📍Reference

* [ChatGPT](https://openai.com/chatgpt)
    
* [Kubernetes Documentation](https://kubernetes.io/docs/home/)
    
* [https://www.youtube.com/watch?v=OJths\_RojFA&feature=youtu.be](https://www.youtube.com/watch?v=OJths_RojFA&feature=youtu.be)
    

---