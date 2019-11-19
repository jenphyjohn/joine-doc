## 接口统一返回体  
模块：``joine-common``  
类：``com.sunfield.joine.common.core.domain.ResponseResult``  
描述：开发接口需使用规定的统一返回体进行封装，对于业务的返回码定义，需使用[统一枚举类](#统一枚举类)结合[国际化资源文件](#国际化资源文件)进行设置

## 统一枚举类
模块：``joine-common``  
类：``com.sunfield.joine.common.constant.ResponseEnum``  
描述：特定业务场景下的返回码在这里定义，例如：
```java
/**
  * 用户昵称已存在
  */
USER_NAME_EXISTS(10007, "user.name.exists"),
```

## 国际化资源文件
模块：``joine-common``  
位置：``resources/i18n/messages.properties``  
描述：[统一枚举类](#统一枚举类)中定义的返回码对应的描述信息在这里配置，默认只包含中文，如需国际化，扩展即可
注意：开发工具默认字符集请使用UTF-8以便显示中文  
```properties
# 10007
user.name.exists=用户昵称已存在
```

## 断言工具类
模块：``joine-common``  
位置：``com.sunfield.joine.common.utils.Assert``  
描述：对参数等进行校验时，可以使用断言工具类简化代码，断言工具类中可按需增加断言  
断言示例：
```java
    /**
     * 校验手机号1开头11位
     *
     * @param mobile
     * @param responseEnum
     */
    public static void isNotMobile(String mobile, ResponseEnum responseEnum) {
        String pattern = "^1\\d{10}$";
        Pattern regexp = Pattern.compile(pattern);
        if (StringUtils.isBlank(mobile) || !regexp.matcher(mobile).matches()) {
            throw new CustomizeException(responseEnum);
        }
    }
```
使用示例：
```java
    /**
     * 发送手机验证码
     *
     * @param mobile 手机号
     * @return ResponseResult
     */
    @ApiOperation(value = "发送手机验证码")
    @GetMapping("/verifyCode/{mobile}")
    @PassAuth
    public ResponseResult createCode(@ApiParam(name = "mobile", value = "手机号", required = true) @PathVariable String mobile) {
        Assert.isNotMobile(mobile, ResponseEnum.MOBILE_FORMAT_INCORRECT);
        // TODO发送短信验证码
        return ResponseResult.successResponse();
    }
```
解释：校验接口传入的手机号，如果格式不正确，则会抛出自定义异常，响应``ResponseEnum.MOBILE_FORMAT_INCORRECT``定义的返回码：
```json
{
  "code": 10006,
  "msg": "手机号格式不正确",
  "data": null
}
```

## facade层
模块：``joine-admin``、``joine-restapi``  
位置：``com.sunfield.joine.web.facade``、``com.sunfield.joine.restapi.facade``  
描述：在``service``和``controller``层中间增加了facade层，用于编写业务代码，被controller直接调用  
示例：
```java
/**
 * 登录业务层
 * <p>
 * Description:
 * </p>
 *
 * @author JenphyJohn
 * @date 2019/11/15 2:08 PM
 */
@Service
public class LoginFacade {

    @Autowired
    private ISysUserService userService;

    public ResponseResult login(ParamLoginDTO loginBean) {
        String loginName = loginBean.getLoginName();
        SysUser user = userService.selectUserByLoginName(loginName);
        if (user == null) {
            // 未注册
            ResultLoginDTO loginResult = new ResultLoginDTO().setRegFlag(BusinessConstants.COMMON_FALSE);
            return ResponseResult.success(loginResult);
        }
        if (BusinessConstants.COMMON_TRUE.equals(user.getStatus())) {
            return ResponseResult.response(ResponseEnum.USER_ACCOUNT_LOCKED);
        }
        ResultLoginDTO loginResult = new ResultLoginDTO()
                .setRegFlag(BusinessConstants.COMMON_TRUE)
                .setToken(loginJWT(user));
        return ResponseResult.success(loginResult);
    }
}
```

## 数据传输对象（DTO）
模块：``joine-restapi``  
位置：``com.sunfield.joine.restapi.dto``  
描述：请求Body参数命名为``ParamXXXDTO``，响应Body参数命名为``ResultXXXDTO``，尽量按照规则命名

## 第三方支持
模块：``joine-common``  
位置：``com.sunfield.joine.common.support``  
描述：默认集成了七牛云存储、阿里云OSS、华为云OBS（前端）、阿里短信、阿里支付、Spring邮件等（陆续完善中）