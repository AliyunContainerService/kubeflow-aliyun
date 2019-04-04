1. 在阿里云容器服务创建Kubernetes集群, 可以参考 [文档](https://github.com/AliyunContainerService/ai-starter/blob/master/docs/setup/CREATE_CLUSTER.md)

2. 下载源代码

```
git clone https://github.com/aliyunContainerService/kubeflow-aliyun
```

3. 

```
kustomize build overlays/ack-auto-clouddisk > /tmp/ack-auto-clouddisk.yaml
```

3. 首先利用

查看所在的Kubernetes集群节点所在的地域和可用区,并且根据其所在节点替换可用区，假设您的集群所在可用区为`cn-hangzhou-g`,可以执行下列命令

```
sed -i.bak 's/regionid: cn-beijing/regionid: cn-hangzhou/g' \
    /tmp/ack-auto-clouddisk.yaml

sed -i.bak 's/zoneid: cn-beijing-e/zoneid: cn-hangzhou-g/g' \
    /tmp/ack-auto-clouddisk.yaml
```
> 建议您检查一下/tmp/ack-auto-clouddisk.yaml修改是否已经设置

4. 将容器镜像地址由`gcr.io`替换为`registry.aliyuncs.com`

```
sed -i.bak 's/gcr.io/registry.aliyuncs.com/g' \
    /tmp/ack-auto-clouddisk.yaml
```

> 建议您检查一下/tmp/ack-auto-clouddisk.yaml修改是否已经设置

5. 调整使用磁盘空间大小, 比如需要调整磁盘空间为200G

```
sed -i.bak 's/storage: 100Gi/storage: 200Gi/g' \
    /tmp/ack-auto-clouddisk.yaml
```


### Q&A

1.