https://blog.csdn.net/zjcjava/article/details/71606144


 每个业务服务采用独立的MYSQL数据库，初期考虑用到如下组件：

服务注册、发现: eureka
配置管理:spring config , spring security
集群容错: hystrix（待实现）
API网关: zuul（待实现）
服务负载:feign+ribbon
api文档输出:swagger2
代码简化:lombok
消息队列:rabbitmq
分布式锁: redis （待实现）
链路跟踪:spring cloud sletuh ->zipkin
安全认证:oauth2/JWT(待实现)
服务监控:spring-boot-admin



各模块介绍

模块名称	端口	简介
admin-server	9002	服务监控中心，监控所有服务模块
conf-server	9004	分布式配置中心，结合spring-security/rabbitmq同时使用
eureka-server	9003	服务注册中心，提供服务注册、发现功能
sleuth-server	9001	SpringCloud实现的一种分布式追踪解决方案，兼容Zipkin
zuul-server	9005	API网关模块
account-service	8080	用户服务，提供注册、登录、地址等服务
product-service	8081	商品服务，提供商品列表、详情、库存更新等服务
payment-service	8082	支付服务，支付记录
order-service	8083	订单服务，提供订单创建、详情、状态变更
msg-service	8084	消息处理服务
front-app	8088	前端服务，结合swagger2提供API管理








快速上手

1、先启动admin-server,eureka-server,conf-server三个基础服务
2、再依次启动payment/order/product/account基础业务服务
3、最后启动front-app服务，打开浏览器，输入http://localhost:8088/swagger-ui.html ，根据流程API依次可使用功能
4、后续有时间再提供页面，基于VUE2+BOOTSTRAP，将流程串起来
Release Version

v2.1

Release Date : 2017-08-29
1、引入swagger2，完成API接口文档管理完成整体业务数据流程流转

2、通过API接口完成整体业务数据

3、基于Spring-cloud-config引入配置中心，结合security加强安全配置，同时引入bus-amqp(rabbitmq)高效更新配置内容[配置中心数据结合sc-cloud-repo工程使用]

4、引入feign，满足客户端调用服务端的服务

5、引入ribbon，可以满足客户端的负载均衡调用后端服务

v1.0

Release Date : 2017-08-17
1、完成基本服务及业务子模块服务的搭建 ，业务子模块可正常运行

2、完成SpringBootAdmin业务模块的运行监控，及Eureka服务运行，满足各业务基础服务的注册、发现功能

3、可通过Front-app端，借助Feign组件发起login/signup等功能的 简单测试运行。

下一版本，将基于此版本之上，继续完善完整的购物实现，包括简单的页面、api管理/调用等等。
