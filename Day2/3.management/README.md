# MySQL Deployment in Kubernetes

## **1. Creating Namespaces (Projects)**
To separate different environments, create the following namespaces:

```sh
oc create namespace dev
oc create namespace test
oc create namespace prod
```

## **2. Deploying MySQL using Kustomize**
Kustomize allows for flexible deployments across different environments. Deploy MySQL for `dev`, `test`, and `prod` using:

```sh
cd openshift-adv/Day2/3.Management/kustomize
oc apply -k overlays/dev
oc apply -k overlays/test
oc apply -k overlays/prod
```

This applies the respective configurations for each namespace.

## **3. Testing Database Connection Between Namespaces**
To verify MySQL connectivity between environments:

### **3.1 Open a Shell in the MySQL Pod (dev Namespace)**
```sh
oc exec -it mysql-0 -n dev -- sh
```

### **3.2 Get the IP Address of a MySQL Pod in `prod`**
```sh
oc get pods -n prod -o wide
```
Find the `IP` of the target MySQL pod from the output.

### **3.3 Connect to MySQL in `prod` from `dev`**
```sh
mysql -h <POD-IP> -P 3306 -u root -p
```

🔹 **Password:** `password`

### **3.4 Verify MySQL Connection Status**
Once connected, check the database status using:
```sh
\s
```
This command provides details about the MySQL server, including uptime, connections, and threads.


This ensures a structured deployment and enables easy management across different environments. 

---
**Copyright (c) 2025 by Alexander Kolin. All rights reserved.**