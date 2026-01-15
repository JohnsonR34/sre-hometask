Tried deploying the file, and faced this error:
Command used: kubectl -f create nginx.yaml 
error: error parsing nginx.yaml: error converting YAML to JSON: yaml: line 25: did not find expected key
---

Opened the file using VS code and noticed the  indentation error and incorrect spelling. 
1. requiredDuringSchedulingIgnoreDuringExecution - Missing "d" in "Ignored".
Fix: changed it to requiredDuringSchedulingIgnoredDuringExecution

2. containers -  extra space, did not align with "spec", 
Fix: removed one space

3. targetport - "p" in targetport should be capital.
Fix: changed it to targetPort

---
Again, tried deploying and faced this error:

A) Warning: resource deployments/sretest is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
deployment.apps/sretest configured

B) Warning: resource services/sretest-service is missing the kubectl.kubernetes.io/last-applied-configuration annotation which is required by kubectl apply. kubectl apply should only be used on resources created declaratively by either kubectl create --save-config or kubectl apply. The missing annotation will be patched automatically.
service/sretest-service configured

Reason for the error: 
A) The minikube did not contain this label "node-role.kubernetes.io/application", which is a required label, mentioned under "affinity"

B) The minikube had only two cpus, but the requirement was 3cpus. 

Fix: 
A) Added the label "node-role.kubernetes.io/application", using this command: 
kubectl label nodes minikube node-role.kubernetes.io/application="sretest"

B) Created a new minikube and assigned 3 cpus. 
minikube start --driver=virtualbox --cpus=3

--driver=virtualbox - to use Virtualbox to run minikube

---
Deployment was a success, but there is another issue. There was no connection between the service and the deployment. The configuration of the service, does not select the deployment and it caused issues while accessing the service. 

Error: ❌  Exiting due to SVC_UNREACHABLE: service not available: no running pod for service sretest-service found
This error displayed when trying to connect the service from minikube. 
Command used: minikube service sretest-service

Fix: Updated the selector to "sretest", instead of  "sretest-service", applied the changes. 
Command to apply changes:  kubectl apply -f nginx.yaml 
During this time, I rearranged the position of Service and Deployment. 

The Nginx is accessible on the web browser. 






