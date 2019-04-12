# API说明

## 访问方式

提供一个以Http协议访问的URL，如：

> http://localhost/api.jsp

数据以Post方式发送，内容包括以下部分：

* type : 发送的是哪种数据(company|pay)
* data : 数据的json字符串，具体Json中为Key和Value组成的键值对
* order_id : 字符串，业务流水号
* sign : 用于进行安全验证的签名，**这个版本先不实现**

## 数据格式

当前共有两种数据格式，用不同的type区分：

* company : 公司数据，在公司注册的时候调用
* pay : 交易数据，在公司向个人支付时调用

不同类型数据中，data包含的数据格式如下：

### company

* id : 字符串，公司的唯一标示，一般为税号
* name : 字符串，公司的名称
* address : 字符串，公司地址
* phone : 字符串，公司电话
* linkman : 字符串，公司联系人
* mail : 字符串，公司邮件
* time : 数字，时间戳，精确到秒

### pay

数据最外层是一个数组（只有一项也要放在数组中），其中每一项包括：

* company_id : 字符串，公司代码
* company_name : 字符串，公司名称
* user_name : 字符串，个人用户名称
* user_id_card : 字符串，个人用户的身份证号
* user_mobile : 字符串，个人用户的手机号
* user_bank_name : 字符串，个人用户的开户行
* user_bank_card : 字符串，个人用户的银行卡号
* money1 : 数字，金额，所有用于显示的费用都这个
* money2 : 数字，税费
* money3 : 数字，业务费用
* time : 数字，时间戳，精确到秒

## 异常处理

### Url访问失败

如果因为网络等原因，造成API访问失败，可以不断重试到成功为止。相同order_id的请求，只会被处理一次。
