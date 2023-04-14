# MyChanggou
参考网课的SpringBoot项目，实现商城后端部分功能。

关键技术包括：
1. 项目搭建基于**SpringCloud**微服务架构，数据库、中间件均以docker方式部署在linux服务器。
2. 注册中心微服务中使用eureka作服务注册中心。
3. 在商品微服务中基于**通用mapper**实现商品信息的CURD操作，数据存储在**mysql**数据库。其中，活动图片的存储使用了**二级缓存——redis+nginx本地缓存**。
3. 在文件存储微服务中使用**FastDFS**对图片信息存储并提供直链访问。
4. 网关微服务中，借助**SpringGateway**组件实现跨域访问、路由和**负载均衡**、请求过滤和**限流**、**JWT鉴权**功能。其中，负载均衡功能配合redis实现。
5. 搜索微服务中，为商品创建索引实体类，使用**elasticsearch**作为搜索引擎。
6. 数据同步微服务中，使用**cannal**监听mysql中同步信息字段的改变，通过**rabbitmq**实现消息的传递与接收，实现数据同步。
- 活动图片的更新涉及到redis缓存的同步，nginx接收同步请求，借由**openRestry**处理后调用**lua脚本**，保证redis更新操作的原子性。
- 商品上架状态的更新涉及到索引的同步，通过elasticsearch模板方法实现删除索引、导入索引功能。

文档整理：https://i2igfgkrnh.feishu.cn/docx/TD0odPKMEoyttIxemAccgnZqnIf
