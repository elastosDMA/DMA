# Payment API

## **介绍**
我们payment模块主要是想完成法币到币的通道，将来大家也可以使用法币直接购买电子票，商家也可能实现数字货币到法币的提现。目前payment模块主要实现了文档中提到的功能，然而DMA的SDK并不具备开账号等运营的责任，交易过程中需要借助币币交易的第三方平台，我们预留下了接口，将来可随时对接Elastos认可的币币交易第三方支付。

我们接通了币昇交易所。但目前SDK还是处于调试阶段，使用测试环境


## **目录**

- [1. 法币充值ELA](#1-法币充值)
- [2. 法币充值DMA](#2-法币充值)
- [3. ELA兑换DMA](#3-币币兑换)
- [4. DMA兑换ELA](#4-币币兑换)
- [5. 充值订单详情](#5-充值订单详情)
- [6. 充值订单列表](#6-充值订单列表)
- [7. 币币兑换订单详情](#7-币币兑换订单详情)
- [8. 币币兑换订单列表](#8-币币兑换订单列表)


##  **API**

###  1. 法币充值

-   说明 法币充值ELA

-   方法名 ：` rechargeELA() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| merchantId | String  | 商户id|
| secret |  String  |商户私钥|
| amount | String  |充值数量|
| userId | String  |商户内部用户id|
| address | String   | 充值地址|
| orderNo | String   | 商户内部订单号|
| notifyUrl | String   | 通知回调地址|
| callbackUrl | String   | 跳转地址|


-   返回值类型：`JsonResult`

-   返回说明：

```
   {
	"code": "0",
	"success": true,
	"msg": "操作成功",
	"data": "http://pay164.yibeix.com/?Timestamp=1556601305&appId=z6txymewn&bizOrderId=c703425fff3c4a21a968f20055bd032a&callbackURL=http://127.0.0.1:9997//&currencyName=CNY&merchantId=583&notifyURL=http://www.starrymedia.com&prdName=USDT&price=6.29&qty=0.0026504987&side=buy&userId=402823816a5d399d016a5d3c3c440000&Signature=ii9hj0SYu3sniJtnLNRw0t1ipehOynhfFAWpKO6qaqs%3D",//支付页面
	"map": {}
}
```



###  2. 法币充值

-   说明：法币充值DMA

-   方法名 ：` rechargeDMA() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| merchantId | String  | 商户id|
| secret |  String  |商户私钥|
| amount | String  |充值数量|
| userId | String  |商户内部用户id|
| address | String   | 充值地址|
| orderNo | String   | 商户内部订单号|
| notifyUrl | String   | 通知回调地址|
| callbackUrl | String   | 跳转地址|


-   返回值类型：`JsonResult`

-   返回说明：

```
   {
	"code": "0",
	"success": true,
	"msg": "操作成功",
	"data": "http://pay164.yibeix.com/?Timestamp=1556601305&appId=z6txymewn&bizOrderId=c703425fff3c4a21a968f20055bd032a&callbackURL=http://127.0.0.1:9997//&currencyName=CNY&merchantId=583&notifyURL=http://www.starrymedia.com&prdName=USDT&price=6.29&qty=0.0026504987&side=buy&userId=402823816a5d399d016a5d3c3c440000&Signature=ii9hj0SYu3sniJtnLNRw0t1ipehOynhfFAWpKO6qaqs%3D",//支付页面
	"map": {}
}
```


###  3. 币币兑换

-   说明：ELA兑换DMA

-   方法名 ：` elaToDma() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| merchantId | String  | 商户id|
| secret |  String  |商户私钥|
| privateKey | String  |ELA私钥|
| value | String  |ELA数量|
| address | String   | DMA地址|
| orderNo | String   | 商户内部订单号|
| userId | String   | 商户内部用户id|
| notifyUrl | String   | 通知回调地址|


-   返回值类型：`JsonResult`

-   返回说明：

```
   {
	"code": "0",
	"success": true,
	"msg": "操作成功",
	"map": {}
}
```



###  4. 币币兑换

-   说明：DMA兑换ELA

-   方法名 ：` dmaToEla() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| merchantId | String  | 商户id|
| secret |  String  |商户私钥|
| privateKey | String  |DMA私钥|
| value | String  |DMA数量|
| address | String   | ELA地址|
| orderNo | String   | 商户内部订单号|
| userId | String   | 商户内部用户id|
| notifyUrl | String   | 通知回调地址|


-   返回值类型：`JsonResult`

-   返回说明：

```
   {
	"code": "0",
	"success": true,
	"msg": "操作成功",
	"map": {}
}
```





###  5. 充值订单详情

-   方法名 ：` orderInfo() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| serialNo | String  | 服务订单号|


-   返回值类型：`JsonResult`

-   返回说明：

```
  {
  "code": "0",
  "success": true,
  "msg": "操作成功",
  "data": {
    "orderNo": "12345678",
    "serialNo": "8cc7c933ea8a402798f73be50575983a",
    "userId": "23456",
    "remark": null,
    "side": "FAIT_TO_ELA",
    "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
    "notifyUrl": "http://www.starrymedia.com",
    "callbackUrl": "http://www.starrymedia.com",
    "merchantId": null,
    "rechargeType": [
      {
        "createTime": 1556543382,
        "status": 6,
        "okTime": null,
        "type": "FAIT_TO_USDT",
        "amount": 3,
        "arrivalAmount": 1.04
      },
      {
        "createTime": 1556543382,
        "status": 9,
        "okTime": null,
        "type": "USDT_TO_ELA",
        "amount": 3,
        "arrivalAmount": 1.04
      },
      {
        "createTime": 1556543382,
        "status": 12,
        "okTime": 1556543405,
        "type": "ELA_WITHDRAW",
        "amount": 3,
        "arrivalAmount": 1.04
      }
    ]
  },
  "map": {}
}
}
```




###  6. 充值订单列表

-   方法名 ：` orderList() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| pageNumber | String  | 页码|
| pageSize | String  | 每页条数|
| userId | String  | 商户内部用户id（选填）|
| merchantId | String  | 商户号|


-   返回值类型：`JsonResult`

-   返回说明：

```
{
  "code": "0",
  "success": true,
  "msg": "操作成功",
  "data": {
    "list": [
      {
        "orderNo": "12345678",
        "serialNo": "8cc7c933ea8a402798f73be50575983a",
        "userId": "23456",
        "remark": null,
        "side": "FAIT_TO_ELA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "callbackUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "rechargeType": null
      },
      {
        "orderNo": "12345678",
        "serialNo": "d90e052a024045e397a51e3c2251a1f1",
        "userId": "23456",
        "remark": null,
        "side": "FAIT_TO_DMA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "callbackUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "rechargeType": null
      },
      {
        "orderNo": "12345678",
        "serialNo": "59b7edf3fc64493a90bec8fb24976f00",
        "userId": "23456",
        "remark": null,
        "side": "FAIT_TO_DMA",
        "address": "0x8791a194e061848385cd50dc93a606331dae8581",
        "notifyUrl": "http://www.starrymedia.com",
        "callbackUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "rechargeType": null
      }
    ],
    "pageNumber": 0,
    "pageSize": 3,
    "totalPage": 1,
    "totalRow": 3
  },
  "map": {}
}

```

###  7. 币币兑换订单详情

-   方法名 ：` exchangeInfo() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| serialNo | String  | 服务内部订单号|



-   返回值类型：`JsonResult`

-   返回说明：


```
{
  "code": "0",
  "success": true,
  "msg": "操作成功",
  "data": {
    "orderNo": "12345678",
    "serialNo": "d90e052a024045e397a51e3c2251a1f1",
    "userId": "23456",
    "remark": null,
    "side": "FAIT_TO_DMA",
    "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
    "notifyUrl": "http://www.starrymedia.com",
    "merchantId": "583",
    "amount": 1.04,
    "arrivalAmount": 1040,
    "txid": "f5a942d91869a48c7653bb0a4dbfaaef3f90e6cdc2a0f96b6891c6fd434e1c30",
    "hash": "0xb014aaa96462f9a89cf44fb3c583f6e693a07252b9d128637c67fa471732dd64",
    "createTime": 1556543455,
    "status": 16
  },
  "map": {}
}


```


###  8. 币币兑换订单列表

-   方法名 ：` exchangeList() `

参数说明:

| 参数名 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| pageNumber | String  | 页码|
| pageSize | String  | 每页条数|
| userId | String  | 商户内部用户id（选填）|
| merchantId | String  | 商户号|
-   返回值类型：`JsonResult`

-   返回说明：


```
{
  "code": "0",
  "success": true,
  "msg": "操作成功",
  "data": {
    "list": [
      {
        "orderNo": "12345678",
        "serialNo": "226098bb8c9344b1866cda75cc9ce314",
        "userId": "23456",
        "remark": null,
        "side": "DMA_TO_ELA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "amount": 3,
        "arrivalAmount": 0.003,
        "txid": "f5a942d91869a48c7653bb0a4dbfaaef3f90e6cdc2a0f96b6891c6fd434e1c30",
        "hash": "0xb014aaa96462f9a89cf44fb3c583f6e693a07252b9d128637c67fa471732dd64",
        "createTime": 1556543976,
        "status": 20
      },
      {
        "orderNo": "12345678",
        "serialNo": "3034a8d89fa84c19b92b274e358944d7",
        "userId": "23456",
        "remark": null,
        "side": "DMA_TO_ELA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "amount": 3,
        "arrivalAmount": 0,
        "txid": "f5a942d91869a48c7653bb0a4dbfaaef3f90e6cdc2a0f96b6891c6fd434e1c30",
        "hash": "0xb014aaa96462f9a89cf44fb3c583f6e693a07252b9d128637c67fa471732dd64",
        "createTime": 1556543873,
        "status": 20
      },
      {
        "orderNo": "12345678",
        "serialNo": "435fcac7c0a74606b45452f35e3147a6",
        "userId": "23456",
        "remark": null,
        "side": "DMA_TO_ELA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "amount": 3,
        "arrivalAmount": 0,
        "txid": "f5a942d91869a48c7653bb0a4dbfaaef3f90e6cdc2a0f96b6891c6fd434e1c30",
        "hash": "0xb014aaa96462f9a89cf44fb3c583f6e693a07252b9d128637c67fa471732dd64",
        "createTime": 1556543719,
        "status": 20
      },
      {
        "orderNo": "12345678",
        "serialNo": "175b17a957204df9b34414de7f4269c9",
        "userId": "23456",
        "remark": null,
        "side": "ELA_TO_DMA",
        "address": "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC",
        "notifyUrl": "http://www.starrymedia.com",
        "merchantId": "583",
        "amount": 3,
        "arrivalAmount": 3000,
        "txid": "f5a942d91869a48c7653bb0a4dbfaaef3f90e6cdc2a0f96b6891c6fd434e1c30",
        "hash": "0xb014aaa96462f9a89cf44fb3c583f6e693a07252b9d128637c67fa471732dd64",
        "createTime": 1556543610,
        "status": 16
      }
    ],
    "pageNumber": 1,
    "pageSize": 20,
    "totalPage": 0,
    "totalRow": -1
  },
  "map": {}
}


```
