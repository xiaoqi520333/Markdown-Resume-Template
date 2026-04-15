<center>
 
# 杨腾云

</center>

## 个人信息

* 性 别：男&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&ensp;年 龄：21
* 手 机：19071947879 &emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&ensp;&ensp;邮 箱：15185717938@163.com
* 专 业：计算机科学与技术 &emsp;&emsp;&emsp;&emsp;&emsp;岗 位：后端开发（实习中，可实习六个月）
* 学 历：本科

### 教育经历
**中南民族大学**　`2023-09 ~ 2027-07`  
计算机科学与技术 · 本科  
主修课程：计算机组成原理、数据结构、操作系统、软件工程、离散数学、设计模式
### 实习经历

**华信咨询设计研究院有限公司 — 全栈开发实习生**　`2025-07 ~ 2025-10`

* 负责粮仓 / 库区 / 粮情等业务模块接口与数据侧开发与迭代，参与前后端联调及上线验证，保障需求按期发布。
* 基于 MyBatis 拦截器实现敏感字段透明加解密，降低明文暴露风险，满足政务侧数据安全与合规要求。
* 使用 EasyExcel 对万级粮情与仓储报表做分批导入导出，控制内存占用，避免大批量导出 OOM。
* 结合慢 SQL 做索引与 SQL 优化，为列表与统计类查询补充组合索引，列表接口响应由约 1500ms 降至约 600ms（约 60%），改善高峰期查询体验。
## 专业技能

* **Java 与 Web 后端：** 熟悉 Java 与 Spring Boot 3、MyBatis / MyBatis-Plus；熟悉 Spring Cloud Alibaba 微服务开发与联调（Nacos、Dubbo 等）。
* **网关：** 使用 Higress 完成 API 网关接入与路由等配置（与微服务及环境联调）。
* **数据与性能：** 熟悉 MySQL 表结构与索引设计、慢 SQL 与 EXPLAIN 分析；有列表、统计类查询与索引优化及政务类项目数据侧实践经验。
* **缓存与中间件：** 熟悉 Redis、Caffeine + Redis 多级缓存；掌握 Redisson 分布式限流；熟悉 RabbitMQ 的异步解耦与削峰；了解 Kafka；
* **RPC 与网络：** 熟悉 Netty（NIO、Pipeline、编解码）；熟悉 Zookeeper / Curator 服务注册发现、子节点监听与客户端本地缓存更新。
* **搜索：** 熟悉 Elasticsearch 全文检索及与 MySQL 在不同查询场景下的选型与配合。
* **AI 工程化：** 熟悉 LangChain4j、RAG、Agent 编排与工具调用；具备 Reactor + SSE 流式响应、Prompt 护栏与限流、缓存等线上成本控制经验。

## 项目经历

### 1. 开源 — AI Agent 驱动的 Web 应用生成平台 — 核心开发 — `2025-08 ~ 2026-03`

* **具体功能：** 流式对话、Agent 执行编排、RAG、工具调用、会话与记忆、分布式限流与成本控制。
* **技术栈：** LangChain4j、Spring Cloud Alibaba、Dubbo、Nacos、Reactor + SSE。
* **技术难点与效果：**
  * 实现 Reactor + SSE 流式对话链路，首 Token 响应约 1.6s，较非流式完整等待（75s+）降低 98%。
  * 设计 Agent 执行编排（Plan/Execute/Retry/Replan），将执行轨迹回写记忆与 RAG 知识库，增强多轮任务连续性与失败恢复能力。
  * 基于 LangChain4j 实现结构化路由与输入护栏，完成 Prompt 注入拦截、工具幻觉兜底与基础输出校验。
  * 通过 Redisson + AOP 落地分布式令牌桶限流，基于 Redis 共享令牌桶实现多实例全局限速，防止突发流量下 AI API 成本失控。
  * Redis 缓存近期会话，读取耗时较 MySQL 全量查询降低 64%（28ms vs 79ms）；异步线程池将 MySQL/向量库写入从主链路剥离，总耗时降低 68%（6368ms → 2008ms）。
* **仓库地址：** [https://gitee.com/xiaoqiwangzhe/aicodeCloud](https://gitee.com/xiaoqiwangzhe/aicodeCloud)

### 2. 开源 — YunPictureHub | 智能云图库平台 — 核心开发 — `2025-01 ~ 2026-03`

* **具体功能：** 面向个人与团队的云端图片管理平台，支持多来源上传、AI 自动分类打标、全文检索与社交互动，集成 QwenAI 扩图能力。
* **技术栈：** MySQL、Redis、Caffeine、Elasticsearch、RabbitMQ、Kafka、腾讯云 COS/数据万象、Sa-Token、多模态大模型 API（DashScope / 智谱 GLM）。
* **技术难点与效果：**
  * 采用模板方法模式固定 COS 上传与清理主流程，文件上传与 URL 上传的差异逻辑由子类实现。
  * 用 COS + 数据万象生成压缩缩略图与元信息，智谱 AI 提取分类标签，线程池异步降库；接口响应从 4360ms 降至 677ms（降低 80%），吞吐从 5.9 升至 37.5 QPS（提升约 6 倍）。
  * 浏览、点赞、评论等操作接入 RabbitMQ 异步解耦，P95 响应从 9494ms 降至 371ms（提升约 25 倍），吞吐从 16 升至 601 QPS。
  * 首页热点分页由 MySQL 改为 Caffeine + Redis 二级缓存，同场景 OPS 从 30 提升至 390（提升约 13 倍）。
  * 基于 Elasticsearch 实现名称、分类、标签全文检索，倒排索引支撑百万级数据 P95 延迟 1850ms，较 MySQL LIKE 全表扫描（9739ms）提升约 5 倍，吞吐从 4.8 升至 20.4 QPS。
  * 基于 Sa-Token 实现登录与团队权限，按请求 spaceId 动态解析空间角色；私人空间用户层级 + 编程式事务保证一人一空间。
  * 自定义操作日志注解，AOP 异步写入 Kafka，与业务解耦，支持审计与消费分析。
* **仓库地址：** [https://gitee.com/xiaoqiwangzhe/AIYunPictureHub](https://gitee.com/xiaoqiwangzhe/AIYunPictureHub)

### 3. 个人项目 — DoubleRpc — 独立开发 — `2026-03 ~ 至今`

* **具体功能：** 基于 Java，从零实现分布式场景下的服务注册发现与远程调用；在 Netty 自定义通信协议、Zookeeper 注册中心、客户端本地缓存与监听等基础上，完成多策略负载均衡与调用可靠性（超时重试 + 白名单）等能力。
* **技术：** Netty，Zookeeper/Curator，Fastjson，Java 原生序列化，一致性哈希。
* **技术难点与效果：**
  * 设计并实现自定义 RPC 报文：定长/类型头 + 自定义 Encoder/Decoder，解决 TCP 粘包/半包下的按帧解析与分发。
  * 基于 Netty 实现 NIO 通信：客户端/服务端 Pipeline 编排，支撑长连接上的请求/响应。
  * 使用 Zookeeper + Curator 做注册与发现：提供者注册临时节点；消费侧服务发现 + 地址解析；Watcher 监听子节点变更。
  * 客户端本地缓存：减少对频繁 ZK 读；与监听联动增量更新本地提供者列表。
  * 客户端多策略负载均衡：实现轮询、随机、一致性哈希（含虚拟节点）等，在发现结果上路由到具体实例。
  * 调用可靠性：基于 Guava Retry 等对白名单内幂等接口做超时重试。


## 个人账号

* **Gitee：** [https://gitee.com/xiaoqiwangzhe](https://gitee.com/xiaoqiwangzhe)
