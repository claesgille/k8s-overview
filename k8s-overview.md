---
marp: true
title: Kubernetes
theme: gaia
author: Claes Gille
header: ![w:200px](images/kubernetes-horizontal-color.png)
footer: Claes Gille
---

<style>
img[alt~="center"] {
  display: block;
  margin: 0 auto;
}
div.twocols {
  margin-top: 35px;
  column-count: 2;
}
div.twocols p:first-child,
div.twocols h1:first-child,
div.twocols h2:first-child,
div.twocols ul:first-child,
div.twocols ul li:first-child,
div.twocols ul li p:first-child {
  margin-top: 0 !important;
}
div.twocols p.break {
  break-before: column;
  margin-top: 0;
}
</style>

![w:1000px center](images/kubernetes-horizontal-color.png)

<div align="center">

Kort presentation av kubernetes

</div>



---

# Vad är kubernetes?

* Orkestrering av containers i ett kluster
* En komplett driftmiljö
* Open source, stort ekosystem
* Linux native
* Skapades av Google (project Borg)
* Namnet Kubernetes förkortas ofta till k8s

---

# Var finns k8s?

Tillgängligt hos de flesta molntjänstleverantörer och on premise

* Google cloud services GKE
* Azure AKS
* Amazon EKS
* Open Shift (On premise)
* Kan köras på riktig plåt eller VM

---

# Köra k8s lokalt för utveckling

* Docker desktop har inbyggd k8s (https://www.docker.com/products/docker-desktop)
* Minikube (https://minikube.sigs.k8s.io/)
* Kind (https://kind.sigs.k8s.io/)
* Kan installeras lokalt på Linux (krångligt)

----
<div align="center">

# Delar i ett k8s kluster

</divs>

![w:800px center](images/clusters.png)

---

# Namespace

![w:800px center](images/img-for-ns.png)

---

# Konfigurering av k8s objekt

* Konfigureras med yaml-filer som beskriver desired state
* Det finns ett yaml format för varje typ av objekt i k8s
* kubectl används för att skicka yaml filer till klustret
* kubectl kan också användas för att hämta konfigurationer från klustret

Exempel hur man applicerar en yaml-fil på sitt kluster:

```
kubectl apply -f ./some-config.yaml
```

---

# Kubernetes objekt

* Applikations definitioner: Deployment, StatefulSet, Job, CronJob
* Applikations instanser: Pod
* Nätverks access till applikation: Service, Ingress
* Konfiguration av applikationer: ConfigMap, Secret
* Lagring: StorageClass, PersistentVolume, PersistentVolumeClaim  

---

# Pod

* Applikationsinstans
* Är en instans av en Deployment eller StatefulSet
* Konfigurera sällan direkt, skapas internt ifrån ett annat objekt

---

# Deployment - stateless apps

<div class="twocols">

* Används för att definiera stateless applikationer
* Beskriver hur poddar skall konfigureras och startas
* labels: används för att referera till deployment
* replicas: anger hur många poddar som skall startas


<p class="break"></p>

<span style="font-size:68%">

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/name: load-balancer-example
  name: hello-world
spec:
  replicas: 5
  selector:
    matchLabels:
      app.kubernetes.io/name: load-balancer-example
  template:
    metadata:
      labels:
        app.kubernetes.io/name: load-balancer-example
    spec:
      containers:
      - image: gcr.io/google-samples/node-hello:1.0
        name: hello-world
        ports:
        - containerPort: 8080
```
</span>

---

# Service

---

# PerstentVolume & PerstistentVolumeClaim

* Storage class (typ av persistent lagring)

---

# StatefulSet - stateful apps

---

#  ConfigMap

---

# Secret

