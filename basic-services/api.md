# 用户注册
### 简要描述

 * 用户注册接口
 
 ### 请求URL：
 
 `http://xx.com/api/user/register`

### 请求方式：

* POST

### 参数：

| 参数名  | 必选 | 类型 | 说明|
|--|:--:|--|--|
| username | 是  | string |  用户名
| password | 是  | string |  密码
| name | 是  | string |  昵称

 ### 返回示例

```json
{  
  "error_code": 0,  
  "data": {  
  "uid": "1",  
  "username": "12154545",  
  "name": "吴系挂",  
  "groupid": 2 ,  
  "reg_time": "1436864169",  
  "last_login_time": "0",  
 }
```
**返回参数说明**

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzQ0MzcwMDU4LC0yMzUwMzM4NzhdfQ==
-->