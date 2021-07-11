https://abp.io/

### Infrastructure

1. Domain Driven Design
2. Muti-Tenancy 租赁 integrate 整合
3. Built-in bunding & minification
4. authorization
5. cross cutting concerns
6. virtual file system
7. Theming
8. http apis & dynamic proxies
9. bootstrap tag helper & dynamic forms

DDD分层
表示层: 为用户提供接口，使用应用层实现与用户交互。
应用层: 表示层与领域层的中介，编排业务对象执行特定的应用程序任务，使用应用程序逻辑实现用例。
领域层: 包含业务对象以及业务规则，是应用程序的核心。
基础设施层: 提供通用的技术功能，支持更高的层，主要使用第三方类库

审计(Audit)
审计是用于追踪数据变化的过程。平时开发中，你一定经常见到类似创建时间、创建人、修改时间、修改人等属性，这些属性就是用于数据审计。ABP框架提供了一些接口和基类来标准化这些属性，并自动设置它们的值；并且ABP提供了一个可扩展的审计日志系统，自动化的根据约定记录审计日志，并提供配置来控制审计日志的级别。ABP中审计相关基类/接口有：IAuditedObject、AuditedEntity、AuditedAggregateRoot等等。