## 数据库设计
根据业务需求，进行新的数据库表及字段设计，运行新脚本并保存脚本到doc文件夹下，以便后续维护，业务表前缀默认使用biz_，否则需改变[代码生成配置](#代码生成配置)

## 代码生成配置
修改``joine-generator``工程下``resources/generator.yml``代码生成的相关配置  
```yaml
# 代码生成
gen:
  # 作者
  author: JenphyJohn
  # 默认生成包路径 business 也可配置成其他的模块名称 如 system monitor tool
  packageName: com.sunfield.joine.business
  # 自动去除表前缀，默认是true
  autoRemovePre: true
  # 表前缀(类名不会包含表前缀)
  tablePrefix: biz_
```

## 使用代码生成
1. 启动``joine-admin``工程并登陆系统用户
2. 进入``系统工具-代码生成``页面，生成业务表的代码
3. 将生成的zip包解压缩，并拷贝各文件到相应目录，代码对应模块：  

内容 | 模块
-|-
main/java/com/sunfield/joine/business/service | joine-business
main/java/com/sunfield/joine/business/mapper | joine-business
main/java/com/sunfield/joine/business/domain | joine-business
main/resources/mapper/business | joine-business
main/java/com/sunfield/joine/business/controller/* | joine-admin
main/resources/templates/business | joine-admin

4. 执行生成菜单SQL脚本（只选择需要配置的菜单，也可手动配置）

## 阶段开发
1. 根据业务设计RESTful风格的API接口，并使用swagger展示文档
2. 根据后台管理的要求，进行后台功能的定制开发