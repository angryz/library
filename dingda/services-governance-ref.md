# 服务治理框架说明

## 为何需要

* 在我们的分布式服务架构中，前期追求速度和简单，没有使用服务治理框架
* 随着服务的增加，用户量订单量的上升，对弹性伸缩和扩展性有了更高要求
* 人工对不同服务器上的多个服务进行伸缩管理越来越麻烦，耗费时间且容易出错
* 依赖负载均衡的伸缩机制需要管理大量域名

## 提供能力

![main](services-governance-main.png)

1. 服务启动时，自动向注册中心(zookeeper)进行注册，同一个服务可注册多个实例
2. 服务的消费者消费服务时，向注册中心获取一个服务实例的接口地址
3. 消费者使用获取到的服务实例地址直接进行服务消费

## 框架模型

![model](services-governance-model.png)

### Consumer Side

#### ServiceDiscovery

* 访问注册中心，发现需要消费的服务实例
* 将消费者也注册到注册中心，便于监控管理
* 订阅服务实例节点变化，以便服务实例离线时及时更换调用的实例
* 如果调用服务实例发生异常，向注册中心报告（投票）

#### ServiceProxy

* 远程服务的本地代理，本地消费服务时直接调用该代理
* 内部封装了对远程服务调用的序列/反序列化和通信实现

### Provider Side

#### ServiceRegistration

#### ServiceExporter

#### ServiceImplement

#### @RpcService

### Monitor
