# Public-comment
这是一个基于Spring Boot开发的后端点评系统项目

## 项目架构概览

### 1. 技术栈
- **框架**: Spring Boot 2.3.12
- **数据库**: MySQL 5.1.47
- **缓存**: Redis + Lettuce连接池
- **ORM**: MyBatis-Plus 3.4.3
- **工具**: Lombok、Hutool、Redisson

### 2. 分层结构
```
├── controller  # 控制层，处理HTTP请求
├── service     # 服务层，实现业务逻辑
├── mapper      # 数据访问层
├── entity      # 实体类
├── dto         # 数据传输对象
├── config      # 配置类
└── utils       # 工具类
```

## 核心功能模块

### 1. 用户模块 (User)
- **功能**:
  - 手机号验证码登录
  - 用户签到
  - 用户信息管理
- **关键类**:
  - `UserController`: 用户接口
  - `UserServiceImpl`: 用户服务实现
  - `LoginInterceptor`: 登录拦截器

### 2. 商户模块 (Shop)
- **功能**:
  - 商户信息查询
  - 商户类型管理
  - 地理位置查询
- **关键类**:
  - `ShopController`: 商户接口
  - `ShopServiceImpl`: 商户服务实现
  - `ShopTypeController`: 商户类型接口

### 3. 博客模块 (Blog)
- **功能**:
  - 博客发布
  - 点赞功能
  - 评论管理
  - 关注推送
- **关键类**:
  - `BlogController`: 博客接口
  - `BlogServiceImpl`: 博客服务实现
  - `BlogCommentsController`: 评论接口

### 4. 优惠券模块 (Voucher)
- **功能**:
  - 优惠券管理
  - 秒杀功能
  - 订单处理
- **关键类**:
  - `VoucherController`: 优惠券接口
  - `VoucherOrderServiceImpl`: 秒杀服务实现
  - `SeckillVoucher`: 秒杀优惠券实体

## 技术亮点

### 1. 缓存策略
- 使用Redis作为缓存
- 实现了多级缓存方案
- 包含缓存穿透、击穿、雪崩的解决方案

### 2. 分布式锁
- 使用Redisson实现分布式锁
- 自定义Redis锁实现
- 支持锁续期

### 3. 性能优化
- 分页查询优化
- 异步处理
- 连接池配置

### 4. 安全性
- 登录拦截器
- Token刷新机制
- 参数校验

## 配置要点

### 1. 数据库配置
```yaml
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://{mysqlurl}
    username: {yourName}
    password: {password}
```

### 2. Redis配置
```yaml
spring:
  redis:
    host: {redisurl}
    port: 6379
    lettuce:
      pool:
        max-active: 10
        max-idle: 10
```

### 3. MyBatis-Plus配置
- 分页插件配置
- 类型别名包扫描
- SQL打印配置

## 特色功能

1. **秒杀系统**
   - Lua脚本保证原子性
   - 异步下单
   - 库存预扣减

2. **签到系统**
   - Bitmap实现
   - 连续签到统计
   - 奖励机制

3. **关注推送**
   - Feed流实现
   - 滚动分页
   - 实时更新

4. **地理位置服务**
   - GEO数据结构
   - 附近商户查询
   - 距离计算

这个项目是一个功能完整的点评系统，包含了用户管理、商户管理、博客系统、优惠券秒杀等核心功能，并且在性能优化、并发处理、缓存策略等方面都有很好的实践。
