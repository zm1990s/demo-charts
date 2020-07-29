# 支持多云环境部署的 demo app

允许用户选择当前的应用应该部署在哪个云，根据不同云使用不同的 image 地址、configmap、service、PVC等 来创建应用。



# 配置调研表模板

| 项目                                            | AKS                              | CCE                              | ACE               | 对应Charts表单设计                                          |
| ----------------------------------------------- | -------------------------------- | -------------------------------- | ----------------- | ----------------------------------------------------------- |
| 容器镜像仓库                                    | harbor-aks.xx.com                | harbor-cce.xx.com                | harbor-ace.xx.com | 自动根据选择的云使用不同镜像仓库，表单不暴露                |
| Pod数量                                         | 2                                | 3                                | 不在此云部署      | 在表单中暴露，并指定默认值                                  |
| 应用配置configmap                               | 使用cm-aks.yaml                  | 使用cm-cce.yaml                  | 不在此云部署      | 自动根据选择的云使用不同镜像仓库，表单不暴露                |
| PVC/PV                                          | 使用已有的，名称为xxx            | 使用已有的，名称为xxx            | 不在此云部署      | 不进行配置，只调用已有的                                    |
| Service                                         | 使用已有的，名称为yyy            | 使用已有的，名称为yyy            | 不在此云部署      | 不进行配置，只调用已有的                                    |
| 亲和/反亲和                                     | 不设置                           | 设置反亲和                       | 不在此云部署      | 自动根据选择的云使用确定是否设置亲和/反亲和策略，表单不暴露 |
| 环境变量                                        | App_1_ip=192.168.2.5             | App_1_ip=10.12.2.5               | 不在此云部署      | 自动根据选择的云使用不同镜像仓库，表单不暴露                |
| 资源限制  Limit/request  (此选项和硬件性能相关) | Request: 1200m CPU，200mi 内存。 | Request: 1000m CPU，200mi 内存。 | 不在此云部署      | 自动根据选择的云使用不同镜像仓库，表单不暴露                |
