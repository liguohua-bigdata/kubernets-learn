http://www.dockerinfo.net/1132.html
https://segmentfault.com/a/1190000007990723
http://www.cnblogs.com/ericnie/p/6965091.html
http://blog.csdn.net/u013812710/article/details/52801656

1.默认后端
生成一个默认的后端，如果遇到解析不到的URL就转发到默认后端页面
default-backend.yaml 


kubectl delete -f  default-backend.yaml 
kubectl create -f  default-backend.yaml 

kubectl get pod --namespace=kube-system
kubectl get rc --namespace=kube-system

2.部署Ingress Controller
nginx-ingress-controller.yaml


kubectl delete -f  nginx-ingress-controller.yaml
kubectl create -f  nginx-ingress-controller.yaml

kubectl get pod --namespace=kube-system
kubectl get rc --namespace=kube-system



3.配置ingress
nginx-ingress-controller.yaml


host指虚拟出来的域名，具体地址(我理解应该是Ingress-controller那台Pod所在的主机的地址)应该加入/etc/hosts中,这样所有去helloworld.eric的请求都会发到nginx
path:/console匹配后面的应用路径
servicePort主要是定义服务的时候的端口，不是NodePort.
path:/ 匹配后面dashboard应用的路径,以前通过访问master节点8080/ui进入dashboard的，但dashboard其实是部署在minion节点中，实际是通过某个路由语句转发过去而已，dashboard真实路径如下:


