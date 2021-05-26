# kPow Helm // Kubernetes

This repository contains Helm configuration to install an instance of kPow for Apache Kafka in a Kubernetes cluster. 

This Helm chart uses the latest [operatr/kpow](https://hub.docker.com/r/operatr/kpow) container.

You will need to supply some configuration specific to your environment and license in [operatr-io/operatr-io-config.yaml](operatr-io/templates/operatr-io-config.yaml).

Once deployed, access the kPow UI on port 3000 with kubectl port-forwarding or change the service/type in [operatr-io/values.yaml](operatr-io/values.yaml).

## Instructions

* Check out this repository
* CD into this directory
* Confirm Kubernetes availability

```bash
$ kubectl get svc

NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   12.345.6.7   <none>        443/TCP   28h
```
* Update [operatr-io/templates/operatr-io-config.yaml](operatr-io/templates/operatr-io-config.yaml) with your configuration (see: [kPow Documentation](https://docs.kpow.io))
* Install kPow with Helm
```bash
$ helm install operatr-io operatr-io/

NAME: operatr-io
LAST DEPLOYED: Tue Jul 28 22:35:30 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=operatr-io,app.kubernetes.io/instance=operatr-io" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:3000 to use your application"
  kubectl --namespace default port-forward $POD_NAME 3000:3000
  ```
* Once deployed, follow the instructions in the notes (above) to access the kPow UI.
* Checking the pod deployment:
```bash
$ kubectl describe pods

Name:           operatr-io-688bbc74-lrm6x
Namespace:      default
Priority:       0
Node:           <none>
Labels:         app.kubernetes.io/instance=operatr-io
                app.kubernetes.io/name=operatr-io
                pod-template-hash=688bbc74
Annotations:    kubernetes.io/psp: eks.privileged
Status:         Pending
...
```
* Viewing the pod logs:
```bash
kubectl logs operatr-io-688bbc74-lrm6x

11:36:49.111 INFO  [main] operatr.system ? start OPERATR
...
...
```
* If you have any issues or errors, please contact support@operatr.io