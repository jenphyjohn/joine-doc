# 项目简介

# Joine-稻田企业级快速开发框架 {docsify-ignore}
<p>
  <img src="https://img.shields.io/badge/Spring%20Boot-2.1.5-brightgreen.svg">
  <img src="https://img.shields.io/badge/Apache%20Shiro-1.4.0-blue.svg">
  <img src="https://img.shields.io/badge/template-Thymeleaf-green.svg">
  <img src="https://img.shields.io/badge/ORM-MyBatis-blueviolet.svg">
</p>

### 功能
- 后台管理：用户管理、角色管理、菜单管理、部门管理、岗位管理等
- 参数配置：数据字典、系统参数
- 日志监控：定时任务、操作日志、登录日志、在线用户、数据监控、服务器监控
- 开发工具：表单构建、代码生成、Swagger文档
- 前端工程：JWT Token登录、Restful接口
- 其他功能：国际化资源、多Module支持等

### 模块
```
joine
├── joine-admin -- 后台管理系统工程
├── joine-restapi -- 前端接口工程
├── joine-common -- 系统公共模块 包含各种基类以及工具
├── joine-framework -- 后台系统核心模块 包含各种配置及核心组件
├── joine-system -- 系统基础领域模块 存放系统数据的 domain|mapper|service
├── joine-business -- 业务领域模块 存放需开发的业务数据的 domain|mapper|service
├── joine-quartz -- 定时任务模块
└── joine-generator -- 代码生成模块
```
