http://www.cnblogs.com/zhenyuyaodidiao/p/6654481.html

挂载磁盘
    echo "/data/disk001 10.100.134.0/24(rw,sync,all_squash)" >> /etc/exports
    exportfs -rv
    mkdir -p /data/disk001
    chown nfsnobody.nfsnobody /data/disk001
    mkdir -p /cloudstar/data/disk001
    mount -t nfs 10.100.134.3:/data/disk001 /cloudstar/data/disk001
    
创建pv
    *[](yml/nfs-pv1.yaml)
    *[](yml/nfs-pv2.yaml)
    
    kubectl create -f nfs-pv1.yaml 
    kubectl create -f nfs-pv2.yaml 
    
创建PetSet
    创建PetSet的时候需要先创建一个“headless”的Service，即service显示的将ClusterIP设置
    为none。而用户可以通过直接访问PetSet中的Pod的IP（通过Pod的HostName解析得到），来访问
    后端的服务的。 
     
    kubectl create -f test-petset.yaml     