一、微服务方面的准备
1.各个服务更新其bootstrap.yml，将其defaultZone改为集群
eureka:
  instance:
    preferIpAddress: true
    instance-id: ${spring.cloud.client.ipAddress}:${server.port}
  client:
    serviceUrl:
      defaultZone: http://${EUREKA_SERVER_HOST_01:localhost}:${EUREKA_SERVER_PORT:8761}/eureka/,http://${EUREKA_SERVER_HOST_02:localhost}:${EUREKA_SERVER_PORT:8761}/eureka/,http://${EUREKA_SERVER_HOST_03:localhost}:${EUREKA_SERVER_PORT:8761}/eureka/

2.重新build镜像，并上传至docker仓库中

二、Kubernetes方面的的准备
1.机器打标签
	kubectl label node bigdata03  serviceGroup=eureka
	kubectl label node bigdata04  serviceGroup=eureka
	kubectl label node bigdata05  serviceGroup=eureka

2.查看情况
	kubectl get nodes --show-labels

3.eureka服务配置亲和性并更新ENV
apiVersion: v1
kind: Service
metadata:
  name: eureka-service
  labels:
    app: eureka-service
spec:
  # if your cluster supports it, uncomment the following to automatically create
  # an external load-balanced IP for the frontend service.
  type: NodePort
  ports:
    # the port that this service should serve on
  - port: 8761
    nodePort: 8761
  selector:
    app: eureka-service
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: eureka-service
  # these labels can be applied automatically
  # from the labels in the pod template if not set
  labels:
    app: eureka-service
spec:
  # this replicas value is default
  # modify it according to your case
  replicas: 3
  # selector can be applied automatically
  # from the labels in the pod template if not set
  # selector:
  #   matchLabels:
  #     app: guestbook
  #     tier: frontend
  template:
    metadata:
      labels:
        app: eureka-service
      annotations:
              scheduler.alpha.kubernetes.io/affinity: >
                {
                  "nodeAffinity": {
                    "requiredDuringSchedulingIgnoredDuringExecution": {
                      "nodeSelectorTerms": [
                        {
                          "matchExpressions": [
                            {
                              "key": "serviceGroup",
                              "operator": "In",
                              "values": ["eureka"]
                            }
                          ]
                        }
                      ]
                    }
                  }
                }
    spec:
      containers:
      - name: eureka-service
        imagePullPolicy: Always
        image: 10.100.134.2:5000/telecomapistore-backend-services/eureka-service
        resources:
          requests:
            cpu: 100m
            memory: 100Mi
        ports:
        - containerPort: 8761
        env:
          - name: EUREKA_SERVER_HOST_01
            value: "10.100.134.3"
          - name: EUREKA_SERVER_HOST_02
            value: "10.100.134.4"
          - name: EUREKA_SERVER_HOST_03
            value: "10.100.134.5"
          - name: ZIPKIN_SERVER_HOST
            value: "10.100.134.4"
          - name: MONITOR_SERVER_HOST
            value: "10.100.134.5"

4.其他服务并更新ENV
        env:
          - name: EUREKA_SERVER_HOST_01
            value: "10.100.134.3"
          - name: EUREKA_SERVER_HOST_02
            value: "10.100.134.4"
          - name: EUREKA_SERVER_HOST_03
            value: "10.100.134.5"
          - name: ZIPKIN_SERVER_HOST
            value: "10.100.134.4"
          - name: MONITOR_SERVER_HOST
            value: "10.100.134.5"
5.重新上传k8s部署文件，并重新启动全部微服务
