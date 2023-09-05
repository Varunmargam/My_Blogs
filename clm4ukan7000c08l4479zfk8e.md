---
title: "K8's Assignment Deploying Flask-Microservices and Reddit Clone Application"
datePublished: Sun Sep 03 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clm4ukan7000c08l4479zfk8e
slug: k8s-assignment-deploying-flask-microservices-and-reddit-clone-application
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1693829709485/7e1ff9e7-26a5-4fc7-bf20-ee496b12c1d7.png
tags: kubernetes, reddit, flask-cje4g3tgk00wdm0wtaepqxd29, devops-journey, 90daysofdevops

---

---

# 📍Task 1:

**1\. Deployment of a Microservices Application on K8s**

\- Do Mongo Db Deployment

\- Do Flask App Deployment

\- Connect both using Service Discovery

# 📍Flask-microservice app

`Step 1`: Installing minikube on AWS EC2 instance visit this GitHub URL for the guide:

[https://github.com/LondheShubham153/kubestarter/blob/main/minikube\_installation.md](https://github.com/LondheShubham153/kubestarter/blob/main/minikube_installation.md)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813537312/2b86291a-5206-425b-8faf-4708a0420846.png align="center")

`Step 2`: Create a `projects` directory inside the `home` directory:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813846751/c12288e9-b7df-427e-9ab3-8ea634bb255d.png align="center")

`Step 3`: Clone this GitHub repository: [https://github.com/Varunmargam/microservices-k8s](https://github.com/Varunmargam/microservices-k8s)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813950816/5f14db90-acf5-4adf-9d3f-916ff0782e5d.png align="center")

Inside the `project` folder:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693813982032/6c715926-c8ab-4cc1-9200-3f8dcd92fec9.png align="center")

`Step 4`: Change the directory to `k8s` inside the `microservices-k8s` folder:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693814116388/7556814d-2010-4b5a-ae04-e46966039138.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693814122694/e9d98d50-450a-4378-917d-8bac4393c3d6.png align="center")

**It contains the following 6 files:**

**Deployment Manifest file for the backend**: `taskmaster.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: taskmaster
  namespace: flask
  labels:
    app: taskmaster
spec:
  replicas: 1
  selector:
    matchLabels:
      app: taskmaster
  template:
    metadata:
      namespace: flask
      labels:
        app: taskmaster
    spec:
      containers:
        - name: taskmaster
          image: trainwithshubham/taskmaster-python:latest
          ports:
            - containerPort: 5000
          imagePullPolicy: Always
```

**Service Manifest file for the backend**: `taskmaster-svc.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: taskmaster-svc
  namespace: flask
spec:
  selector:
    app: taskmaster
  ports:
    - port: 80
      targetPort: 5000
      nodePort: 30007
  type: NodePort
```

**MongoDB Database Deployment Manifest file**: `mongo.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mongo
  namespace: flask
  labels:
      app: mongo
spec:
  selector:
    matchLabels:
      app: mongo
  template:
    metadata:
      namespace: flask
      labels:
        app: mongo
    spec:
      containers:
        - name: mongo
          image: mongo
          ports:
            - containerPort: 27017
          volumeMounts:
            - name: storage
              mountPath: /data/db
      volumes:
        - name: storage
          persistentVolumeClaim:
            claimName: mongo-pvc
```

**MongoDB Database Service Manifest file**: `mongo-svc.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  namespace: flask
  labels:
    app: mongo
  name: mongo
spec:
  ports:
    - port: 27017
      targetPort: 27017
  selector:
    app: mongo
```

**MongoDB Database PersistentVolume Manifest file**: `mongo-pv.yml`

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mongo-pv
  namespace: flask
spec:
  capacity:
    storage: 256Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /tmp/db
```

**MongoDB Database PersistentVolumeClaim Manifest file**: `mongo-pvc.yml`

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mongo-pvc
  namespace: flask
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 256Mi
```

`Step 5`: Create a namespace named `flask` :

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693814748915/c226a3c2-3591-4777-ac76-26760dbab2bf.png align="center")

`Step 6`: Executing the `kubectl apply` commands in this order following the best practice:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693814879432/0a4ba755-6513-480c-92cb-7540f4beb2b5.png align="center")

Verifying the mongo deployment and the service created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693814797081/7f14bba6-6fca-4746-8ace-578d8d9ed0f3.png align="center")

`Step 7`: Executing inside the mongo pod to see if we can access it:

```bash
kubectl exec -it <pod_name> -n <namespace> -- bash
# If successfully entered the pod then to login to the mongo database do
mongosh
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693827731932/19ba6dcd-3e7e-4362-b59e-6058d5c84208.png align="center")

Type `exit` to exit from the Mongo database.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693828060701/278fdfe9-2625-4522-b7e3-a4c1c4644dfc.png align="center")

`Step 8`: Applying the backend deployment file and verifying it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693815031459/e8613625-0536-4329-8b75-8c52b51c57db.png align="center")

Applying the backend service deployment file and verifying it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693815042245/b8e96040-d5cd-4517-b0c0-35a653c62756.png align="center")

`Step 8`: Verify both pods are running:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693815124984/27296c66-b3eb-4dfc-94e8-cf63ebf4d46b.png align="center")

`Step 9`: Testing the application on the minikube ip:

```bash
# command to access the service ip:
minikube service taskmaster-svc -n flask --url

# test the application on minikube:
curl -L http://minikube_ip:30007 
# the link that we got from the fiest command
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693815482494/c4f91100-759f-4e98-bc68-6e562690c98d.png align="center")

You can see our application is running!

To list the tasks:

```bash
curl -L http://minikube_ip:30007/tasks
curl -L http://minikube_ip:30007/task
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693828177142/aba6cebb-a8ee-4ca5-81ae-660c8bad5ff5.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693828223450/8c4498b1-4cc0-4061-a738-56901d1820cb.png align="center")

`Step 10`: To run the application in our browser we have to expose the deployment and the app service:

```bash
# command to expose deployment
kubectl expose deployment taskmaster -n flask --type=NodePort
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693815845101/27323a90-6f5c-4036-be19-981f894389be.png align="center")

Exposing the service:

```bash
kubectl port-forward svc/taskmaster-svc -n flask 30007:80 --address 0.0.0.0
```

Before that, we have to expose the `port 30007` in the security group of our instance running the minikube.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693816036539/8f52bc40-ddf8-46df-8ebb-7ebf02b8a70d.png align="center")

Now execute the above command:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693816072563/bfee672e-d331-46b4-b607-046f98bc46f8.png align="center")

Now go to your browser and type the link ec2\_ip:30007:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693816142733/1a81b4a7-e150-4157-b40a-ef96f385da1a.png align="center")

I tried to add some data using the command:

```bash
curl -d '{"task":"completed the assignment"}' -H "Content-Type: application/json" -X POST http://ec2_ip:30007/task
```

**ISSUE: But, suddenly the connection was refused and the connection in my browser was also refused don't know why? I would appreciate it if you could give some possible solutions or reasons in the comments.**

---

# 📍Task 2:

**2\. Deployment of a Reddit-Clone Application**

\- Do Deployment of the Reddit Clone app

\- Write an ingress controller for the same to give a custom route

# 📍**Deployment of a Reddit-Clone Application using Ingress**

`Step 1`: Install minikube on AWS EC2 instance.

`Step 2`: Inside the `projects` directory clone using the `git clone <HTTP_URL>` command this GitHub repository: [https://github.com/Varunmargam/reddit-clone-k8s-ingress](https://github.com/Varunmargam/reddit-clone-k8s-ingress)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693819880160/13918d71-9cc3-4594-9110-1bcf2110981a.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693819988613/4fe35b0f-356a-49ca-8013-3011dad8430d.png align="center")

**It contains 3 manifest files**:

**Deployment manifest file for the Reddit app**: `deployment.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: reddit-clone-deployment
  namespace: reddit
  labels:
    app: reddit-clone
spec:
  replicas: 2
  selector:
    matchLabels:
      app: reddit-clone
  template:
    metadata:
      namespace: reddit
      labels:
        app: reddit-clone
    spec:
      containers:
      - name: reddit-clone
        image: rohanrustagi18/redditclone
        ports:
        - containerPort: 3000
```

**Service Manifest file**: `service.yml`

```yaml
apiVersion: v1
# Indicates this as a service
kind: Service
metadata:
  # Service name
  name: reddit-clone-service
  namespace: reddit
spec:
  selector:
    # Selector for Pods
    app: reddit-clone
  ports:
    # Port Map
  - port: 3000
    targetPort: 3000
    protocol: TCP
  type: LoadBalancer
```

**Ingress Manifest file**: `ingress.yml`

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-reddit-app
  namespace: reddit
spec:
  rules:
  - host: "domain.com"
    http:
      paths:
      - pathType: Prefix
        path: "/test"
        backend:
          service:
            name: reddit-clone-service
            port:
              number: 3000
  - host: "*.domain.com"
    http:
      paths:
      - pathType: Prefix
        path: "/test"
        backend:
          service:
            name: reddit-clone-service
            port:
              number: 3000
```

`Step 3`: Create a namespace named `reddit`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820326940/2a8f6d18-a86c-40fb-a063-18adf6adca11.png align="center")

`Step 4`: Apply the deployment file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820429470/995b5842-c241-4edf-af61-68dd8979af36.png align="center")

Verifying the pods are running:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820478287/57deec3a-5cd1-4800-a6b1-b8b4e360cda7.png align="center")

`Step 5`: Apply the service file and verify it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820530937/6ada21ad-cb2f-4033-b0fa-65b402520e1d.png align="center")

`Step 6`: Apply the ingress file and verify it:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820576818/6edf8da8-23f1-4ee9-b614-9c7e4e55e494.png align="center")

`Step 7`: Exposing the deployment:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820615088/0043bf1f-7f76-4206-9ad4-fcf5c6f9f0ae.png align="center")

`Step 8`: Exposing the service:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820676872/de1eb6e1-e07f-4c42-a076-266e64c36c51.png align="center")

`Step 9`: Go to the security group of your instance and add the `port 3000`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820739805/c5861ec7-0a07-4c69-a93b-9e5787776655.png align="center")

`Step 10`: Go to your browser and access the application at `ec2_ip:3000`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693820860352/3e1fcccb-a1fe-4c44-a822-19a8f24f57b5.png align="center")

---

# 📍Basic Flask-QA Application

The previous 2 assignments had the deployment and the service file inside the GitHub repository. Therefore, I thought of writing a deployment and the service file and tried to deploy a basic **Question and Answer Flask application** that I got from **ChatGPT**.

`Step 1`: Inside the projects directory make a directory named `flask-qa`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693821752473/2507b19a-5e80-4099-80ab-e1c917151066.png align="center")

`Step 2`: Go inside the `flask-qa` directory and create a Python file `app.py`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693821864023/f7242407-7dbf-46f2-8a29-26c546a34f5b.png align="center")

`Step 3`: Copy the below Python code inside this file, then save and quit the Vim editor:

**Application code**:

```python
from flask import Flask, render_template, request, redirect, url_for

app = Flask(__name__)

# Mock data for questions and answers
questions = [
    {"id": 1, "title": "What is your favorite programming language?", "answers": []},
    {"id": 2, "title": "How do you deploy a Flask app?", "answers": []},
]

@app.route("/")
def index():
    return render_template("index.html", questions=questions)

@app.route("/ask", methods=["GET", "POST"])
def ask():
    if request.method == "POST":
        title = request.form["title"]
        new_question = {"id": len(questions) + 1, "title": title, "answers": []}
        questions.append(new_question)
        return redirect(url_for("index"))
    return render_template("ask.html")

@app.route("/question/<int:question_id>", methods=["GET", "POST"])
def question(question_id):
    question = next((q for q in questions if q["id"] == question_id), None)
    if not question:
        return redirect(url_for("index"))

    if request.method == "POST":
        answer_text = request.form["answer"]
        question["answers"].append(answer_text)
    return render_template("question.html", question=question)

if __name__ == "__main__":
    app.run(debug=True)
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693821951625/74549c61-7fb3-4f35-a67a-f268b76d51a6.png align="center")

`Step 4`: Create a requirements.txt file open it in the Vim editor and copy the below content inside the file.

**Requirements file**:

```plaintext
Flask==2.1.0
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822060346/bca2804a-f42e-4ed3-93a1-33c70e5df554.png align="center")

`Step 5`: Create a `Dockerfile` and copy the below content in it.

**Dockerfile**:

```dockerfile
FROM python:3.8-slim-buster

WORKDIR /app

COPY . /app

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["python", "app.py"]
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822143005/ecaaa64d-b906-4a5c-b6dd-b6b693c8f7c1.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822181242/57cc5961-70ca-4fab-bd66-769a7e192da1.png align="center")

`Step 6`: Build a Docker image from the Dockerfile with the tag `<dockerhub_username>/flask-qa:latest`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822294450/4f68aaf7-7029-4b1d-9f0b-080f2aa6c047.png align="center")

The below output image shows that the build has been successful:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822376079/80047a2b-374b-47a5-b7e6-19b6664596ae.png align="center")

The docker image has been created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822579157/5db69fd3-b4ca-4f5e-8434-d0fcf935f9c2.png align="center")

Now, we will upload this docker image to our DockerHub account.

`Step 7`: Log in to your DockerHub account:

```bash
docker login -u <dockerhub_username>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822482370/cf44b26c-66b0-4a60-8804-37dfb17ee719.png align="center")

`Step 8`: Push this docker image to our DockerHub Account:

```bash
docker push <image_name>
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822658643/2b7f5635-50c6-4b90-9ea0-926a1dcff798.png align="center")

`Step 9`: Go to your DockerHub account and see if the image has been uploaded:

The `flask-qa` image has been uploaded:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822758484/016e6fbc-40f7-4599-908c-7bac2f475e1c.png align="center")

Now, let's start creating the Deployment and Service manifest file.

`Step 10`: Create a namespace `flask-qa`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693822877766/aecc53c4-e6e9-4a90-8fcb-d8644c126bf6.png align="center")

`Step 11`: Create a file named **deployment.yml** and write the deployment manifest file.

**(📝Note**: Try to write the manifest files on your own and then compare them with the below deployment file)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823241326/f24dc0bf-ccd3-40ea-952f-bec9d8c82a25.png align="center")

**Deployment Manifest file**: `deployment.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: qa-deployment
  namespace: flask-qa
  labels:
    app: qa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: qa
  template:
    metadata:
      namespace: flask-qa
      labels:
        app: qa
    spec:
      containers:
      - name: qa-app
        image: varunmargam/flask-qa:latest
        ports:
        - containerPort: 5000
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823250735/04b9862a-06e6-4c5b-a2d5-4a9e61003b3e.png align="center")

`Step 12`: Apply the created `deployment.yml` file by `kubectl apply`:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823339719/aaa4dfcf-c075-4629-a774-84b70bb2d6ef.png align="center")

Verifying the pods are running:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823396758/33c876fd-9489-47e5-b062-7b1646232dde.png align="center")

`Step 13`: Create a service.yml file and write the Service Manifest file:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823616136/3aa0e133-5fc7-4ebc-8e4a-4f323f031b89.png align="center")

**Service Manifest file**: `service.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: qa-svc
  namespace: flask-qa
spec:
  selector:
    app: qa
  type: NodePort
  ports:
  - protocol: TCP
    port: 5000
    targetPort: 5000
    nodePort: 30001
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823681871/5cc301d7-4468-43c0-b96d-9cc8a5666b19.png align="center")

`Step 14`: Apply `service.yml` file and verify if the service has been created:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823786310/378c8e70-ef9c-4dc0-b174-f5aa49ebc668.png align="center")

`Step 15`: Exposing the deployment and service:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693823937400/a0ad228e-c493-49ae-823a-fa68796c33fe.png align="center")

Added the `port 30001` in the Ec2 Instance security groups inbound rules:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1693824054741/af14ae31-34e7-46b3-8e1b-228aeddf28d3.png align="center")

However I was unable to access the application on my browser at port 30001, I would appreciate it if anyone could share what can be the issue with this in the comments.

@[Shubham Londhe](@TrainWithShubham) I kindly request your advice on the issues I am facing in the k8s-microservice app and the above flask-qa app.

---