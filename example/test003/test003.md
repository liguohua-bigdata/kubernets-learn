
参考

0.进入配置文件目录
cd /cloudstar/k8stest/test003
1.创建服务
    kubectl create -s bigdata03:8080 -f test003.yml
2.查看服务
    kubectl get pods 
    kubectl get rc
    kubectl get services
3.测试发布的nginx服务
    http://10.100.134.3:30009
    http://10.100.134.4:30009
    http://10.100.134.5:30009
4.删除服务
    kubectl delete -s bigdata03:8080  -f test003.yml
 
 
 
 
 
