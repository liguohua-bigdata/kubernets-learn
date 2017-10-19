
二、集成dashboard，需要设置hosts
vim /etc/hosts，添加如下内容
61.91.161.217 google.com
61.91.161.217 gcr.io      #在国内，你可能需要指定gcr.io的host，如不指定你需要手动下载google-containers. 如何下载其他文档说的方法挺多

创建
kubectl create -f dashboard.yaml
kubectl create -f dashboardsvc.yaml
销毁
kubectl delete deployment kubernetes-dashboard-latest --namespace=kube-system
kubectl delete svc  kubernetes-dashboard --namespace=kube-system


查看信息
kubectl describe svc kubernetes-dashboard --namespace=kube-system



kubectl delete deployment kubernetes-dashboard-latest --namespace=kube-system
kubectl delete svc  kubernetes-dashboard --namespace=kube-system

kubectl create -f dashboard.yaml
kubectl create -f dashboardsvc.yaml

kubectl get pod


kubectl get nodes
kubectl get pod
kubectl get service


