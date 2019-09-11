# 银通券权益平台API接口调用说明v1.5

---

### 一、接口数据规范

#### 1、所有接口通讯使用数据编码为UTF-8。
#### 2、接口参数名称及地址均使用小写字母。
#### 3、服务端接口返回数据格式为json。
#### 4、接口申请访问时需要提供数据校验信息。本文档中数据校验时加密秘钥变量名为signkey。
#### 5、在做API接入前请先通过商务将要接入API的服务器IP设置到白名单中，同时获取接口通讯校验用的加密秘钥。

#### 测试baseUrl：http://www.maoxiaojie.club:2347

### 二、接口说明

#### 1、获取图形验证码，用于登录接口
- **请求接口**
> [/api/client/getImgCode](#)

示例：
```js
    <img src="http://www.maoxiaojie.club:2347/api/client/getImgCode" alt="">    
```

#### 2、卡密登录
- **请求接口**
> [/api/client/login](#)
- **请求方式**
> **GET/POST**

- **请求参数**
>

| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cardNo | String | 是 | 1001110002345| 卡号 |
| pwd | String | 是 | 23456| 密码 |
| code | String | 是 | 1234| 图形验证码 |
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
>
```js
{
	"status": "success",  //成功状态
	"code": 10000,       //响应状态码 10000为成功 其他为失败
	"msg": "成功",        // 响应描述
	"time": 1567482261,   // 时间戳 可忽略
	"data": {
		"isSelected": true  //true已选择权益  false 未选择权益
	},
	"bcxgame_id": "8e1f803f785bd741270c3eee"  //忽略
}
```
#### 3、查询卡密对应的权益
- **请求接口**
> [/test/client/getAllProfitByCardNo](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cardNo | String | 是 | 1001110002345| 卡号 |
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1567482279,
	"data": {
		"code": 3,                   // 可选择的权益数量
		"profitList": [{
			"profitId": 25,                              //权益ID
			"profitName": "【测试】猫眼电影优惠券",        //权益名称
			"profitType": 0,                             //0：卷码 1：外链
			"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190725160424277678.jpg",  //权益icon图标
			"profitPrice": 5,            //权益单价
			"profitCount": 20,           //权益数量
			"profitStock": 17,            //权益库存
			"endTimeStr": "2019-09-19",   //过期日期
			"packageId": 15               //套餐标识
		}, {
			"profitId": 24,
			"profitName": "【测试】美团点评优惠券",
			"profitType": 1,
			"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190725160309279102.jpg",
			"profitPrice": 5,
			"profitCount": 1000,
			"profitStock": 1000,
			"endTimeStr": "2019-09-30",
			"packageId": 15
		}, {
			"profitId": 27,
			"profitName": "【测试】权益添加字数限制",
			"profitType": 0,
			"profitIcon": null,
			"profitPrice": 40,
			"profitCount": 0,
			"profitStock": 0,
			"endTimeStr": "2020-07-26",
			"packageId": 15
		}]
	},
	"bcxgame_id": "8e1f803f785bd741270c3eee"
}
```

#### 4、查询已选择的权益
- **请求接口**
> [/api/client/getSelectedProfit](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cardNo | String | 是 | 1001110002345| 卡号 |
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1567482279,
	"data": [{
			"profitId": 25,                              //权益ID
			"profitName": "【测试】猫眼电影优惠券",        //权益名称
			"profitType": 0,                             //0：卷码 1：外链
			"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190725160424277678.jpg",  //权益icon图标
			"profitPrice": 5,            //权益单价
			"profitCount": 20,           //权益数量
			"profitStock": 17,            //权益库存
			"endTimeStr": "2019-09-19",   //过期日期
			"packageId": 15               //套餐标识
		}, {
			"profitId": 24,
			"profitName": "【测试】美团点评优惠券",
			"profitType": 1,
			"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190725160309279102.jpg",
			"profitPrice": 5,
			"profitCount": 1000,
			"profitStock": 1000,
			"endTimeStr": "2019-09-30",
			"packageId": 15
		}, {
			"profitId": 27,
			"profitName": "【测试】权益添加字数限制",
			"profitType": 0,
			"profitIcon": null,
			"profitPrice": 40,
			"profitCount": 0,
			"profitStock": 0,
			"endTimeStr": "2020-07-26",
			"packageId": 15
		}],
	"bcxgame_id": "8e1f803f785bd741270c3eee"
}
```

#### 5、提交选择卡密对应的权益
- **请求接口**
> [/api/client/selectProfit](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cardNo | String | 是 | 1001110002345| 卡号 |
| ids | String | 是 | 25,26,27| 多个权益ID（用户逗号隔开） |
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1567482279,
	"data": null,
	"bcxgame_id": "8e1f803f785bd741270c3eee"
}
```


#### 6、查询权益详情
- **请求接口**
> [/api/client/getProfitDetail](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| profitId | Integer | 是 | 1 | 权益ID |
| packageId | Integer | 是 | 1| 套餐标识 |
| cpno | String | 是 | 1001 | 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1567487634,
	"data": {
		"profitId": 25,                               //权益ID
		"profitName": "【测试】猫眼电影优惠券",          //权益名称
		"profitType": 0,                               //0：卷码 1：外链
		"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190725160424277678.jpg",   //权益icon图标
		"profitPrice": 5,                 //权益单价
		"profitCount": 20,                //权益数量
		"profitStock": 17,                //权益库存
		"profitDetail": "<p>【使用方式】<\/p><p>1、点击猫眼APP在“我的”页面中选择钱包；<\/p><p>2、进入“我的”界面后选择“优惠券”；<\/p><p>3、进入后输入短信中收到的券码，点击“添加”，就会出现购买的相对应的券码信息；<\/p><p>4、用户在选好影片、座位等环节后进入到支付界面在“活动与优惠券”中查看通兑券信息后，点击确认支付。<\/p><p><img src=\"http:\/\/47.105.34.241:9999\/upload\/20190725160342770192.jpg\" _src=\"http:\/\/47.105.34.241:9999\/upload\/20190725160342770192.jpg\"\/><\/p>",       //权益明细
		"profitBanner": "http:\/\/47.105.34.241:9999\/upload\/20190725160424909494.jpg",  //权益banner图片
		"exchangeUrl": "",               // 权益兑换地址
		"endTimeStr": "2019-09-19"      //过期日期
	},
	"bcxgame_id": "8e1f803f785bd741270c3eee"
}
```

#### 7、提交选择卡密对应的权益
- **请求接口**
> [/api/client/takeProfit](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cardNo | String | 是 | 1001110002345| 卡号 |
| profitId | String | 是 | 27| 权益ID |
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1567487809,
	"data": [{
		"orderId": 28,                   // 订单ID
		"orderNo": "20190829192345-28",   //订单号
		"cardId": 1589,                   //卡密ID
		"profitId": 25,                  // 权益ID
		"profitCodeId": 23605,            //权益卷码ID
		"profitName": "【测试】猫眼电影优惠券",  //权益名称
		"code": "1291894794719",   // 权益卷码
		"endtime": 1571846400,      // 过期时间
		"status": 0,                // 0，已发放
		"createTime": "2019-08-29 19:23:45"   //创建日期
	}],
	"bcxgame_id": "8e1f803f785bd741270c3eee"
}
```


#### 8、根据客户编号获取账户余额
- **请求接口**
> [/api/server/queryAccountBalance](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data": {
		"balance": 9662.5 // 余额
	},
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```


#### 8、根据客户编号获取账户余额
- **请求接口**
> [/api/server/queryAccountBalance](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data": {
		"balance": 9662.5 // 余额
	},
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```


#### 9、查询客户附属套餐可买卡密限额
- **请求接口**
> [/api/server/queryPackageQuota](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| pgno | int | 是 | 1| 套餐标识 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data": {
		"paname": "腾讯视频vip" // 套餐名称
		"price":200, // 套餐单价
		"quota":20  // 可买限额
	},
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```

#### 10、套餐单张卡密即时创建及提取接口
- **请求接口**
> [/api/server/createSingleCard](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| pgno | int | 是 | 1| 套餐标识 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data": {
		"pgname": "腾讯视频 vip",  //套餐名称
        "price": 200,   // 套餐单价
        "marketPrice": 200,  // 套餐市场价
        "cardno": "1001110002345", // 卡密
        "pass": "23456"  // 密码
	},
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```


#### 11、查询套餐对应的权益列表接口
- **请求接口**
> [/api/server/queryProfitsListInPackages](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| packageid | int | 是 | 1| 套餐标识 |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data":[{
		"id": 43,   // 权益标识
		"profitName": "今今乐道读书会月卡",   // 权益名称
		"profitType": 0,     // 权益类型 0：卷码  1：链接
		"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190728153216817661.jpg",   // icon 
		"profitPrice": 30,   // 权益单价
		"profitCount": 998,   // 权益总数
		"profitStock": 971,   // 权益库存
		"profitDetail": "<p style=\"text-align: center;\"><span style=\"white-space: nowrap;font-family:微软雅黑, Microsoft YaHei;font-size:24px\">【今今乐道读书会月卡使用方法】&nbsp;&nbsp;<\/span><\/p><p>1、在各大应用商店搜索今今乐道，下载安装今今乐道APP，在APP内完成兑换。<\/p><p>2、兑换路径：打开今今乐道APP——登陆——右下方“我的”页面——兑换码选项，输入兑换码即可。<\/p><p>3、兑换后直接生效，千本企业内训经典书籍免费听；<\/p><p>4、同一用户仅限兑换一次；30天到期后，免费听书权限自动失效。<\/p><p>5、总部客服：&nbsp; &nbsp; &nbsp;<\/p><p>联系人：乐道小妹<\/p><p>联系电话：010-53577662- 转999<\/p><p>邮箱：sa@dggroup.cn<\/p><p><img src=\"http:\/\/47.105.34.241:9999\/upload\/20190728153131404499.jpg\" _src=\"http:\/\/47.105.34.241:9999\/upload\/20190728153131404499.jpg\"\/><\/p>",     // 权益详情
		"endTime": 1648742399,     // 过期时间
		"profitBanner": "http:\/\/47.105.34.241:9999\/upload\/20190728153216955337.jpg",  // banner图
		"profitService": null,   // service图
		"exchangeUrl": "",   // 兑换跳转页面
		"status": 1,
		"gcount": null,
		"createTime": "2019-07-28",
		"endTimeStr": "2022-03-31"
	}],
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```


#### 12、查询权益详情接口
- **请求接口**
> [/api/server/queryProfitsDetail](#)

- **请求方式**
> **GET/POST**


- **请求参数**

>
| 名称 | 类型 | 是否必须 | 示例值 | 描述 |
| -------- | --------| ------ | ------ | ------|
| cpno | String | 是 | 1001| 客户编号 |
| profitid | int | 是 | 23| 权益标识(对应查询套餐对应的
权益列表接口里面的权益标识) |
| applytime | String | 是 | 20190420202111| 申请时间。Yyyymmddhhiiss，以北京时间为基准正负 5 分钟为有效数据。 |
| sign | String | 是 | ********| 数据校验串。创建规则：MD5(signkey+applytime+MD5(cpno+signkey)) |

- **返回结果**
```js
{
	"status": "success",
	"code": 10000,
	"msg": "成功",
	"time": 1568166738,
	"data": {
		"id": 43,   // 权益标识
		"profitName": "今今乐道读书会月卡",   // 权益名称
		"profitType": 0,     // 权益类型 0：卷码  1：链接
		"profitIcon": "http:\/\/47.105.34.241:9999\/upload\/20190728153216817661.jpg",   // icon 
		"profitPrice": 30,   // 权益单价
		"profitCount": 998,   // 权益总数
		"profitStock": 971,   // 权益库存
		"profitDetail": "<p style=\"text-align: center;\"><span style=\"white-space: nowrap;font-family:微软雅黑, Microsoft YaHei;font-size:24px\">【今今乐道读书会月卡使用方法】&nbsp;&nbsp;<\/span><\/p><p>1、在各大应用商店搜索今今乐道，下载安装今今乐道APP，在APP内完成兑换。<\/p><p>2、兑换路径：打开今今乐道APP——登陆——右下方“我的”页面——兑换码选项，输入兑换码即可。<\/p><p>3、兑换后直接生效，千本企业内训经典书籍免费听；<\/p><p>4、同一用户仅限兑换一次；30天到期后，免费听书权限自动失效。<\/p><p>5、总部客服：&nbsp; &nbsp; &nbsp;<\/p><p>联系人：乐道小妹<\/p><p>联系电话：010-53577662- 转999<\/p><p>邮箱：sa@dggroup.cn<\/p><p><img src=\"http:\/\/47.105.34.241:9999\/upload\/20190728153131404499.jpg\" _src=\"http:\/\/47.105.34.241:9999\/upload\/20190728153131404499.jpg\"\/><\/p>",     // 权益详情
		"endTime": 1648742399,     // 过期时间
		"profitBanner": "http:\/\/47.105.34.241:9999\/upload\/20190728153216955337.jpg",  // banner图
		"profitService": null,   // service图
		"exchangeUrl": "",   // 兑换跳转页面
		"status": 1,
		"gcount": null,
		"createTime": "2019-07-28",
		"endTimeStr": "2022-03-31"
	},
	"bcxgame_id": "9d83bcd4145ed74163893ecf"
}
```