## 环境要求
- JDK 1.8 + (推荐1.8)
- Mysql 5.6 + (推荐5.7)
- Maven 3.0 +

## 下载项目
1. 前往[项目页面](<http://gogs.join-e.tech:10080/Sunfield/joine>)克隆/下载解压到工作目录
2. 使用IDEA打开工程
3. 创建数据库并导入doc文件夹下的数据库脚本（*注：数据库字符集使用utf8mb4）

## 修改后台工程配置
修改``joine-admin``后台工程下必要配置
  1. 数据库连接``resources/profiles/dev/application-druid.yml``
  2. 文件上传路径（不使用云存储）``resources/profiles/dev/application.yml``
  3. 日志存放路径``resources/profiles/dev/logback.xml``

## 启动后台管理工程
1. 运行springboot启动类``com.sunfield.joine.JoineAdminApplication``
2. 打开浏览器，输入：``http://localhost:8080/mana``展示登录页面
3. 登录系统用户``admin/123456``，若成功登录，菜单及页面展示正常，则后台环境搭建成功

## 修改接口工程配置（提供接口给客户端使用）
修改``joine-restapi``接口工程下必要配置
  1. 数据库连接``resources/profiles/dev/application-druid.yml``
  2. 日志存放路径``resources/profiles/dev/logback.xml``

## 启动接口工程（提供接口给客户端使用）
1. 运行springboot启动类``com.sunfield.joine.JoineRestApplication``
2. 打开浏览器，输入：``http://localhost:8081/api/swagger-ui.html``展示swagger页面正常，则接口工程环境搭建成功