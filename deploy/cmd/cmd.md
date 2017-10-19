

常用kubectl命令
查看节点情况（other）    
    kubectl -s http://bigdata03:8080 get node
    kubectl -s http://bigdata03:8080 get nodes
查看节点情况（master）
    kubectl get nodes
查看集群信息
    kubectl cluster-info 
查看版本信息
    kubectl version
查看组件监控情况
    kubectl get componentstatus 
查看deployment-namespace情况   
    kubectl get deployment --all-namespaces
查看service-namespace情况      
    kubectl get svc  --all-namespaces
查看pod-namespace情况     
    kubectl get pod  -o wide  --all-namespaces

查看rc
    kubectl get rc
查看pod
    kubectl get pod
查看namespace
    kubectl get namespace