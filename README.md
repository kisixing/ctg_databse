<h1 align="center">CTG Database</h1>



## 1.CTG数据查看

### web访问地址

```bash
地址： http://cqmu.lian-med.com/ctg/  
账号/密码：admin admin
```
<p align="center">
<img width="780px" height="450px" src="https://obcdn.oss-cn-shenzhen.aliyuncs.com/static/web_ctgdatabase.png" />
</p>
    
### 功能说明
>档案查询、CTG曲线查看、经典分析评分、数据标记等功能
    
    备注：基于用户隐私，系统没有直接展示孕产妇相关信息（接口包含）
    

## 2.数据接口访问

### 根据档案号获取CTG数据
<p align="center">
<img width="780px" height="450px" src="https://obcdn.oss-cn-shenzhen.aliyuncs.com/static/interface1.png" />
</p>

### 分页获取档案列表（包含用户信息）
<p align="center">
<img width="780px" height="450px" src="https://obcdn.oss-cn-shenzhen.aliyuncs.com/static/interface2.png" />
</p>
> 根据条件查询总条数
> 分页查询记录 

    详见文档末yapi接口文档
    yapi账号/密码 doctor@qq.com  lian-med 
### 接口授权
>认证

    系统默认采用JWT的认证机制。JSON Web Token (JWT) authentication is a stateless security mechanism, so it’s a good option if you want to scale your application on several different servers.
    客户端通过对应的接口向服务器请求JWT，将其存储在Cookie或localStorage中。此后客户端将在与服务器交互中都会带JWT，一般是将它放入HTTP请求的Header Authorization字段中：Authorization: Bearer+token
    JWT本身包含认证信息，因此一旦信息泄露，任何人都可以获得令牌的所有权限。为了减少盗用，JWT的有效期不宜设置太长。对于某些重要操作，用户在使用时应该每次都进行进行身份验证。
    账号密码登录
    支持传入remember字段，系统默认jwt有效期1天，选择记住jwt有效期1个月
    手机号+验证码登录
    因为验证码的方式相对比较安全，默认有效期为1个月。该方式的权限为系统默认授权。
    微信oauth2.0
    支持微信code换取openid并绑定用户信息
    APP跳转登录
    通过url加密串+发送token方式传递认证
>角色与权限

    系统使用基于角色的权限管理（RBAC）框架作为基础，也针对业务特点进行了部分扩展。RBAC，的对应关系如下，用户：用户组（角色）= 1：多， 用户组：权限 = 1：多。
    接口默认支持对应资源名称的权限，前端需要对菜单、路由进行相关的权限绑定。
    相关接口资源为user、group、authority。为配合前端的路由和菜单的授权，后端应加对应menu、router资源接口。
### 接口风格
>criteria查询

    查询条件风格采用JPA Criteria风格，即用get请求字符串实现查询条件的拼接，根据资源的字段类型和业务需求灵活组织
    例如：查询孕妇号为1的用户的产程图记录
    api/prenatal-visits?gynecologicalExamId.specified=true&pregnancyId.equals=1
    gynecologicalExamId 为管理的产程图的记录id， specified 意思是不为空 equals 相当于 =
    其他的关键字如下
    For each xyz field （所有字段都可以用的）
    xyz.equals=someValue 【 equal 即 = 】
    To list all the entities, where xyz equals to ‘someValue’
    xyz.in=someValue,otherValue 【in 即 包含】
    To list all the entities, where xyz equals to ‘someValue’ or ‘otherValue’
    xyz.specified=true【specified=true 即 不为空】
    To list all the entities, where xyz is not null, specified.
    xyz.specified=false【specified=false 即 为空】
    To list all the entities, where xyz is null, unspecified.

    If xyz’s type is string: （对于字符串字段还支持）
    xyz.contains=something 【contains 即 包含 】
    To list all the entities, where xyz contains ‘something’.

    If xyz’s is either any of the number types, or the date types.（对于数字类型字段还支持）
    xyz.greaterThan=someValue 【大于】
    To list all the entities, where xyz is greater than ‘someValue’.
    xyz.lessThan=someValue【小于】
    To list all the entities, where xyz is less than ‘someValue’.
    xyz.greaterOrEqualThan=someValue 【大于等于】
    To list all the entities, where xyz is greater than or equal to ‘someValue’.
    xyz.lessOrEqualThan=someValue 【小于等于】
    To list all the entities, where xyz is less than or equal to ‘someValue’.

>动态查询资源列表
  
     pregnancy
     prenantal-visit
## 3.其他接口功能
### 围产保健接口
>支持孕妇常规产检信息、高危信息、分娩信息、新生儿等信息增删查改接口
### 临床事件
>支持事件记录接口
### 其他接口
>ESB与第三方信息系统对接

### 链接
1.[CTG-cqmu](http://cqmu.lian-med.com/ctg)<br />
2.[CTG其他数据库](http://transfer.lian-med.com/lm)<br />
3.[YAPI接口文档](http://yapi.lian-med.com:8080/project/40/interface/api)<br />
