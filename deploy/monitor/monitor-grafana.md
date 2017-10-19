http://blog.csdn.net/syshzbtt/article/details/71574204
1.下载
    wget https://s3-us-west-2.amazonaws.com/grafana-releases/release/grafana-4.2.0-1.x86_64.rpm
2.安装
    yum localinstall -y grafana-4.2.0-1.x86_64.rpm
3.将grafana加入开机启动
    systemctl daemon-reload 
    systemctl enable grafana-server.service 
4.启动grafana-server
    systemctl start grafana-server.service //将服务开启
