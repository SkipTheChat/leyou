## 1.leyou-manage-web

后台管理页面，负责商品和品牌的上架下架修改搜索等等。

主要对应leyou（后端代码）中的leyou-item，leyou-upload模块

#### 1.1需要环境

vue

1.2启动命令

```
npm start
```



## 2.leyou-portal

前台用户搜索购买界面。

主要对应leyou（后端代码）中的leyou-search，leyou-goods，leyou-sms，leyou-user，leyou-auth，leyou-cart，leyou-order模块

#### 1.1启动命令

```
live-server --port=9002
```



## 3.leyou

#### 1.1模块介绍

leyou-registry：eruka配置中心

leyou-gateway：网关

leyou-item：后台商品页面

leyou-upload：图片上传模块

leyou-search：elasticseatch搜索功能

leyou-goods：商品详情

leyou-sms：短信验证工具模块，使用了rabbitMQ接收消息

leyou-user：用户登录注册校验身份模块，使用了rabbitMQ发送消息给leyou-sms

leyou-auth：授权中心（生成与解析token）

leyou-cart：购物车模块

leyou-order：订单模块



#### 1.2模块开启顺序

与1.1介绍一致，开启顺序不一致可能导致错误



#### 1.3开启项目前准备

##### 1.3.1开启elasticsearch

在leyou-search模块用到了。如果不使用leyou-search的功能，不开也行

我这里是虚拟机开的，在leyou用户下，去虚拟机配置一下elasticsearch并开启就行了。

```
su - leyou
cd elasticsearch/bin/
./elasticsearch
```



##### 1.3.2启动redis

我是虚拟机开机自启的。



##### 1.3.3生成公钥和私钥

找到leyou-auth/leyou-auth-common/src/test/com/leyou/auth/test/JwtTest.java

pubKeyPath和priKeyPath为你想要生成的密钥的路径，你可以放在想要的位置

改好了路径注释掉以下代码

```
@Before
public void testGetRsa() throws Exception {
    this.publicKey = RsaUtils.getPublicKey(pubKeyPath);
    this.privateKey = RsaUtils.getPrivateKey(priKeyPath);
}
```

**运行testRsa方法生成密码**



testGenerateToken和testParseToken分别了生成和解析token的测试，你可以把上面注释的代码还原后进行测试是否成功。



##### 1.3.4修改公钥和私钥为你自己设置的位置

leyou-gateway，leyou-auth-service,leyou-cart,leyou-order这四个模块的application.yml文件中

除了leyou-auth-service配置了公私钥（授权中心），其他都是配置的公钥



#### 1.4注意事项

##### 1.4.1阿里云短信

在leyou-ssm模块application.yml中配置了阿里云短信，这里改成你自己的账号。具体申请方式自发百度。

```
#自己去阿里云短信申请账号填一下这里就行了
  sms:
    accessKeyId:  # 你自己的accessKeyId
    accessKeySecret:  # 你自己的AccessKeySecret
    signName:  # 签名名称
    verifyCodeTemplate:  # 模板名称
```



##### 1.4.2虚拟机地址

所有application.yml中的虚拟机地址请都改成自己的。



1.4.2微信支付

在leyou-order模块的微信支付配置（application.yml）需要自己去申请。

我没申请到所以用的是别人的。

申请方式自行百度。



## 4.leyou.sql

sql文件

注意：只能MySQL5.6环境，其他的不行哦。



## 5.nginx.conf

nginx的配置文件参考。

