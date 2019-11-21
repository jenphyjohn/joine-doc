## 增加新的配置文件  
需求场景：针对于一些配置项越来越多的项目，对于大部分配置是在所有环境（dev，test，pro）下相同的，这个时候开发人员如果维护三套配置文件会很麻烦  
解决方案：可以在对应工程的resources文件夹下增加一个新的配置文件，命名规则是``application-{name}.yml``，例如：``application-common.yml``，并在三个环境下的``spring.profiles.active``后面加上新配置文件名的后缀``{name}``，例如：
```yaml
# Spring配置
spring:
  profiles: 
    active: druid, common
```
之后就可以愉快的使用了😺