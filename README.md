# 乐优商城 - 微服务架构 [![issues](https://img.shields.io/bitbucket/issues-raw/2227324689/ToBeBetter.svg?style=flat-square)](#)  [![author](https://img.shields.io/badge/author-Charlotte-blue.svg?style=flat-square)](#) 

高仿项目。非原创。



# 1.项目用到的技术



项目采用前后端分离开发，前端代码已给，为leyou-manage-web和leyou-portal。

核心的技术栈用的是SpringBoot+SpringCloud。



### 1.1 前端使用的技术

- vue

  

### 1.2 后端使用的技术

- SpringBoot
- SpringCloud
- SpringJPA
- Mybatis
- Elasticsearch
- RabbitMQ
- Thymeleaf
- MySQL
- Redis
- FastDFS



# 2.项目模块说明

| 作用                                                        | 模块名          | 端口     |
| :---------------------------------------------------------- | :-------------- | :------- |
| Springcloud的eruka注册中心，注册了所有的模块业务            | leyou-registry  | 10086    |
| 网关                                                        | leyou-gateway   | 10010    |
| 商家后台的管理商品页面                                      | leyou-item      | 9081     |
| 专门的图片上传模块                                          | leyou-upload    | 9082     |
| 搜索功能(elasticsearch)                                     | leyou-search    | 9083     |
| 点击商品打开后的商品详情页面模块                            | leyou-goods-web | 9084     |
| 短信验证工具模块，并使用了rabbitMQ接收消息                  | leyou-sms       | 9086     |
| 用户登录注册校验身份模块，使用了rabbitMQ发送消息给leyou-sms | leyou-user      | 9085     |
| 授权中心（生成与解析token）                                 | leyou-auth      | 9087     |
| 购物车模块                                                  | leyou-cart      | 9088     |
| 订单模块                                                    | leyou-order     | 9089     |
| 公共模块，存放工具类等。（无需启动）                        | leyou-common    | 无需启动 |



# 3.项目开发进度



### 3.1 前台用户界面

- 首页渲染、根据关键词搜索、根据分类过滤搜索、点击商品进入详情页
- 注册、登录、点击商品属性加入购物车
- 购物车、下单、支付

 ![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/1.jpg)

 



![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/2.jpg)

 





![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/3.jpg)









![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/4.png)









![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/5.png)







### 3.2 后台商家管理界面

- 首页渲染
- 商品管理的分类管理、品牌管理、商品列表、规格参数四个模块的增删改查



![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/TIM截图20191209214657.png)







![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/TIM截图20191209214804.png)









![image](https://raw.githubusercontent.com/cristinejssssss/leyou/master/assets/TIM截图20191209214851.png)





# 4.项目部署

>部署前请先看注意事项修改相关配置





### 4.1 开启商家管理界面

cmd进入leyou-manage-web项目路径，启动命令：

```
npm start
```



>[访问网址：manage.leyou.com](manage.leyou.com)





### 4.2 开启用户搜索界面

cmd进入leyou-portal项目路径，启动命令：

```
live-server --port=9002
```



> [访问网址：www.leyou.com](www.leyou.com)



### 4.3 开启后端项目

用编译器打开项目，分别用tomcat启动各个模块。

**模块启动顺序与项目模块说明的顺序一致**。若不一致，可能导致启动报错。





# 5.注意事项



### 5.1依赖

项目启动之前需启动**elasticsearch，redis以及nginx**，相关虚拟机地址在各yml文件中修改。



### 5.2公钥私钥生成

 验证用户登录需要使用公私钥，自动生成的代码在leyou项目目录下：

	leyou-auth/leyou-auth-common/src/test/com/leyou/auth/test/JwtTest.java



使用方法：

- 先注释下面代码块代码
- 然后运行testRsa方法生成密钥

```
@Before
public void testGetRsa() throws Exception {
    this.publicKey = RsaUtils.getPublicKey(pubKeyPath);
    this.privateKey = RsaUtils.getPrivateKey(priKeyPath);
}
```

- 生好了记得修改leyou-gateway，leyou-auth-service,leyou-cart,leyou-order这四个模块的application.yml文件公私钥地址为你自己的公私钥生成地址





### 5.3 阿里云验证码短信

在leyou-ssm模块application.yml中配置了阿里云短信，这里改成你自己的账号。具体申请方式自发百度。

```
#自己去阿里云短信申请账号填一下这里就行了
  sms:
    accessKeyId:  # 你自己的accessKeyId
    accessKeySecret:  # 你自己的AccessKeySecret
    signName:  # 签名名称
    verifyCodeTemplate:  # 模板名称
```





### 5.4 微信支付

在leyou-order模块的微信支付配置（application.yml）需要自己去申请。

我没申请到所以用的是别人的。

申请方式自行百度。





### 5.5 sql文件

> 注意：只能MySQL5.6环境引入sql文件，其他的不行哦。





### 5.6 nginx地址&host地址配置参考

- nginx配置参考当前目录下nginx.conf

- host配置如下

  ```
  # SwitchHosts!
  
  # My hosts
  
  # leyou
  127.0.0.1 manage.leyou.com
  127.0.0.1 api.leyou.com
  192.168.153.129 image.leyou.com
  127.0.0.1 www.leyou.com
  ```

  



