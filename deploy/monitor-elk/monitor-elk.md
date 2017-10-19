https://github.com/opsnull/follow-me-install-kubernetes-cluster/blob/master/11-%E9%83%A8%E7%BD%B2EFK%E6%8F%92%E4%BB%B6.md

cd /cloudstar/k8stest/monitor-elk




kubectl get nodes
kubectl label nodes bigdata04 beta.kubernetes.io/fluentd-ds-ready=true




kubectl delete -f .
kubectl create -f . --validate=false

