http://www.cnblogs.com/zhenyuyaodidiao/p/6501434.html


创建redis主节点
kubectl create -f redis-master-controller.yaml
kubectl create -f redis-master-service.yaml

创建Redis从节点
kubectl create -f redis-slave-controller.yaml
kubectl create -f redis-slave-service.yaml

创建前端
kubectl create -f frontend-controller.yaml 
kubectl create -f frontend-service.yaml

查看运行情况
kubectl get rc
kubectl get pod
kubectl get service


访问地址
http://bigdata03:30001/