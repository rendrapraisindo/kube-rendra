# Introduction
Berisi file yaml untuk [Kubernetes Dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). 
File yaml ini berasal dari https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml

File ini diedit supaya menggunakan [NodePort](https://kubernetes.io/docs/concepts/services-networking/service/#nodeport) 30099.

# Getting Started
Apply dengan perintah dibawah ini
````
kubectl apply -f kube-dashboard-nodeport-30099.yaml
````
Setelah itu buat token dengan mengikuti tutorial di https://www.replex.io/blog/how-to-install-access-and-add-heapster-metrics-to-the-kubernetes-dashboard

Setelah itu anda dapat login dengan menggunakan browser melalui https ke cluster anda pada port 30099. Contoh
````
https://192.168.26.152:30099/
````
