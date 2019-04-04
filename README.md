# 在阿里云容器服务上部署Kubeflow服务

Kubeflow致力于利用Kubernetes将机器学习（ML）工作流程的部署变得简单，便携和可扩展。其目标是将机器学习的最佳开源系统部署到各种基础架构中。 可以在运行Kubernetes的任何地方运行Kubeflow。该项目一直在不断的演进和丰富之中，特别是最近加入pipelines和TFX的能力，进一步将Google内部的最佳实践推广到整个社区。

但是Kubeflow的部署对于使用者来说是巨大的挑战，针对这个问题，阿里云容器服务提供了Kubeflow核心组件的运行方案，帮助您在阿里云上玩转Kubeflow。

## 前提条件

- 您需要安装[kustomize](https://github.com/kubernetes-sigs/kustomize.git)

在Linux和Mac OS环境，可以执行

```
opsys=linux  # or darwin, or windows
curl -s https://api.github.com/repos/kubernetes-sigs/kustomize/releases/latest |\
  grep browser_download |\
  grep $opsys |\
  cut -d '"' -f 4 |\
  xargs curl -O -L
mv kustomize_*_${opsys}_amd64 /usr/bin/kustomize
chmod u+x /usr/bin/kustomize
```

在Windows环境，可以下载[kustomize_2.0.3_windows_amd64.exe](https://github.com/kubernetes-sigs/kustomize/releases/download/v2.0.3/kustomize_2.0.3_windows_amd64.exe)

## 服务部署

### Kubeflow Pipelines Service

Pipelines是Kubeflow社区在2019年带给社区的最大惊喜。和普通的Kubeflow基础服务不同，Kubeflow Pipelines需要依赖于mysql和minio这些有状态服务，也就需要考虑如何持久化和备份数据。对此阿里云容器服务会提供一系列方案，您可以实际情况进行选择：

- [自动创建SSD云盘，部署pipelines](overlays/ack-auto-clouddisk)
- [手动创建SSD云盘，部署pipelines](overlays/ack-auto-clouddisk)
- 利用RDS和OSS，部署pipelines(TODO)
- 欢迎Hack