http://blog.csdn.net/wenwst/article/details/54015693


挂载磁盘
    echo "/data/jenkins 10.100.134.0/24(rw,sync,all_squash)" >> /etc/exports
    exportfs -rv
    mkdir -p /data/jenkins
    chown nfsnobody.nfsnobody /data/jenkins
    mkdir -p /cloudstar/data/jenkins
    mount -t nfs 10.100.134.3:/data/jenkins /cloudstar/data/jenkins
    
下载镜像
    docker pull  index.tenxcloud.com/loulan/docker-jenkins:latest
创建服务
    cd /cloudstar/k8stest/jenkins
    kubectl delete -f .
    kubectl create -f .
查看服务    
    kubectl get ing 
    kubectl get svc
    kubectl get pod
    
    
     kubectl logs jenkins-1225187225-wmnp5
     
     
     kubectl exec busybox -c busybox -- nslookup jenkins.kube-system
     kubectl get ing 