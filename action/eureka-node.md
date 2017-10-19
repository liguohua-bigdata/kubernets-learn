一、微服务方面的准备
1.微服务读取env并
eureka:
  client:
    serviceUrl:
      defaultZone: http://${EUREKA_SERVER_HOST:localhost}:${EUREKA_SERVER_PORT:8761}/eureka/
2.配置 preferIpAddress: true
eureka:
  instance:
    preferIpAddress: true
    
二、Kubernetes方面的的准备  
1.将eureka部署到指定节点
      nodeSelector:
        kubernetes.io/hostname: bigdata03
        
2.将eureka端口映射出来
    apiVersion: v1
    kind: Service
    metadata:
      name: eureka-service
      labels:
        app: eureka-service
    spec:
      type: NodePort
      ports:
        # the port that this service should serve on
      - port: 8761
        nodePort: 8761

3.其他服务并更新ENV
        env:
          - name: EUREKA_SERVER_HOST_01
            value: "10.100.134.3"
5.重新上传k8s部署文件，并启动全部微服务
            