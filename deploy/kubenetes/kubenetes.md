一、部署文档
http://www.cnblogs.com/zhenyuyaodidiao/p/6500897.html


主要的集群为何命令
systemctl  stop kube-apiserver kube-controller-manager kube-scheduler kubelet kube-proxy

systemctl enable kube-apiserver.service
systemctl start kube-apiserver.service
systemctl enable kube-controller-manager.service
systemctl start kube-controller-manager.service
systemctl enable kube-scheduler.service
systemctl start kube-scheduler.service



systemctl enable kubelet.service
systemctl start kubelet.service
systemctl enable kube-proxy.service
systemctl start kube-proxy.service





重启flannel
systemctl stop flanneld.service 
systemctl start flanneld.service 

重启master
systemctl restart kube-apiserver.service
systemctl restart kube-controller-manager.service
systemctl restart kube-scheduler.service
重启slave
systemctl restart  kubelet.service
systemctl restart  kube-proxy.service
查看节点信息
kubectl -s http://bigdata03:8080 get node

停止集群
systemctl stop kube-apiserver.service kube-scheduler.service kube-controller-manager.service
systemctl stop  kubelet.service kube-proxy.service


