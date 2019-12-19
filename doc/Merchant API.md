# Merchant API

## **介绍**

Merchant API是对Merchant模块进行的功能封装。提供一些通用的模板，供开发者使用。目前有以下三种模板：
##### **普通销售模板：**  销售者创建资产，然后将资产授权给托管合约，进行上架销售。消费者通过托管合约购买资产。托管合约完成销售者资产与消费者资金进行交换的过程。解决双方信任问题。
##### **收费活动模板：** 活动发起者创建一次活动，发行一定数量的活动门票。然后将门票授权给托管合约进行上架出售。活动参与在通过托管合约购买活动门票，参与者付出的资金由托管合约进行保管。当活动结束后，活动发起者才能获得活动门票的资金。
##### **质押活动模板：** 活动发起者创建一次活动，发行一定数量的活动门票。然后将门票授权给托管合约进行上架出售。活动参与在通过托管合约购买活动门票，参与者付出的资金由托管合约进行保管。活动开始前活动发起者校验到场者的门票id，并返回其支付的押金。未到场者押金在活动结束后转移到活动发起者地址。

使用Merchant API快速进行开发，请阅读以下文档

##  **Build**

```
//公用参数
String node = "http://47.105.149.174:8545";//节点地址
BigInteger gasPrice = BigInteger.valueOf(1000000000);
BigInteger gasLimit = BigInteger.valueOf(8000000);

//普通销售模板
MerchantService ethMerchantService = new MerchantServiceImpl("DMA_TESTNET",nodeurl);

//收费活动模板
ChargeActivityServiceImpl chargeActivityService = new ChargeActivityServiceImpl("DMA_TESTNET", nodeurl);

//质押活动模板
PledgeActivityService pledgeActivityService = new PledgeActivityServiceImpl("DMA_TESTNET",nodeurl);


```


## **目录**
- [1. 普通销售模板](#1-普通销售模板)
    - [创建合约](#1-1-创建合约)
    - [资产上架](#1-3-资产上架)
    - [资产下架](#1-4-资产下架)
    - [创建订单](#1-5-创建订单)
    - [查询指定tokenid上架信息](#1-6-查询指定tokenid上架信息)
- [2. 收费活动模板](#2-收费活动模板)
    - [创建合约](#2-1-创建合约)
    - [资产上架](#2-3-资产上架)
    - [资产下架](#2-4-资产下架)
    - [创建订单](#2-5-创建订单)
    - [查询指定tokenid上架信息](#2-6-查询指定tokenid上架信息)
    - [结束活动](#2-7-结束活动)
    - [获取活动结束时间](#2-8-获取活动结束时间) 
- [3. 质押活动模板](#3-质押活动模板)
    - [创建合约](#3-1-创建合约)
    - [资产上架](#3-3-资产上架)
    - [资产下架](#3-4-资产下架)
    - [创建订单](#3-5-创建订单)
    - [查询指定tokenid上架信息](#3-6-查询指定tokenid上架信息)
    - [结束活动](#3-7-结束活动)
    - [获取活动结束时间](#3-8-获取活动结束时间) 
    - [验证签到后退还押金](#3-9-验证签到后退还押金)
    - [发起方主动退款](#3-10-发起方主动退款) 
       
      



----------




##  **API**

### 1. 普通销售模板

#### 1. 1 创建合约

-   方法名 ：` deploy() `

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 用户私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|


-   返回值类型：`JsonResult`

-   返回说明：

```
    /*
    {
	"code": 0,
	"data": "0xac047d394e92061ba0c3ceeab7e658264ea13d98",
	"map": {},
	"msg": "操作成功",
	"success": true
}
    */
```

-   示例代码

```
    @Test
    public void deploy() throws Exception {
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String name = "Test merchant";
        String symbol = "TM";
        String _metadata = "TestData";
        JsonResult<DeployResult> jsonResult = merchantService.deploy(privateKey, gasPrice, gasLimit);
        System.out.println(JSON.toJSONString(jsonResult));
    }
```



#### 1. 3 资产上架

-   方法名 ：` onSales()`

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String   | 托管合约地址|
| assetAddress | String  | 资产合约地址|
| privateKey |  String  |私钥|
| map |  Map  | [{1000000001: 1.0 }] |
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| owner |  String   | 资产拥有者|


-   返回值类型：`JsonResult`

-   返回说明：

```
/*{
	"code": 0,
	"data": {
		"saveApprove": ["0x799f75c8997471725c00d9c5a976745c33c9cdfb2b142b058944035483f4e012"],
		"approve": ["0xd8a33f82422243277b162a5444a565440c652dea9f624ba58ea3506596a74eae"]
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}*/
```

-   示例代码

```
      @Test
    public void onSales() throws Exception {

        List<Long> longs = Arrays.asList(8672524357L,5584566998L,9767553216L,9913677584L,6355617671L);

        String assetAddress = "0xbc1Bea10F80f4EA26d9344F0e7c588502539Ea2A";
        String trustAddress = "0xac047d394e92061ba0c3ceeab7e658264ea13d98";
        Map<BigInteger, BigDecimal> list = new HashMap<>();

        for (Long aLong : longs) {
            list.put(BigInteger.valueOf(aLong ) , BigDecimal.ONE) ;
        }
        String owner = credentials.getAddress();
        JsonResult<Map<String, List<String>>> map = merchantService.onSales(trustAddress ,assetAddress, privateKey, gasPrice, gasLimit, list, owner);
        System.out.println(JSON.toJSONString(map));
    }
```



#### 1. 4 资产下架

-   方法名 ：` offSales（）`

-    参数说明:


| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:|
| trustAddress | String   | 托管合约地址|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| tokenids | List   | 资产id|

-   返回值类型：` JsonResult`

-   返回说明：

```
    /*{
	"code": 0,
	"data": ["0x1c93d141447c7f1c2a356e31251ca3616c3131185a01a4437ddecd2291d19bcc"],
	"map": {},
	"msg": "操作成功",
	"success": true
}*/
```


#### 1. 5 创建订单

-   方法名 ：` createOrder()`

>   方法说明：
>   创建订单操作先执行代币合约的 `approve()`授权操作，再执行平台托管合约的`transfer()`交易操作

-   参数说明

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String   | 平台托管合约地址|
| tokenIdList |  List  |资产id数组|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| sumPrice | String   | 总金额|
| owner |  String   | 资产拥有者|

-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
	"code": 0,
	"data": "0xf049cbe05dd14361bc7b2c01d79be0eb97530e6c249c43f6db7e352c7f61ba15",
	"map": {},
	"msg": "操作成功",
	"success": true
}*/
```
-   示例代码

```
     @Test
    public void createOrder() throws Exception {
        String assetAddress = "0xbc1Bea10F80f4EA26d9344F0e7c588502539Ea2A";
        String trustAddress = "0xac047d394e92061ba0c3ceeab7e658264ea13d98";
        List<Long> longs = Arrays.asList(8672524357L,5584566998L,9767553216L,9913677584L,6355617671L);
        BigDecimal sumPrice =BigDecimal.valueOf(longs.size());

        List<BigInteger> tokenIds   = new ArrayList<>( );
        for (Long aLong : longs) {
            tokenIds.add(BigInteger.valueOf(aLong ) ) ;
        }

        JsonResult<String> map = merchantService.createOrder(trustAddress, assetAddress, privateKeyB, gasPrice, gasLimit, tokenIds, sumPrice, credentials.getAddress());

        System.out.println(JSON.toJSONString(map));
    }

```


#### 1. 6 查询指定tokenid上架信息

-   方法名 ：`getApproveInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| tokenId | String |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
{
	"code": 0,
	"data": {
		"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
		"tokenid": 8672524357,
		"value": "1"
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}
```

-   示例代码

```
    @Test public  void getApproveInfo(){
        String assetAddress = "0xbc1Bea10F80f4EA26d9344F0e7c588502539Ea2A";
        String trustAddress = "0xac047d394e92061ba0c3ceeab7e658264ea13d98";
        JsonResult<PlatFormApproveInfo> approveInfo = merchantService.getApproveInfo(trustAddress, assetAddress, BigInteger.valueOf(8672524357L));
        System.out.println("approveInfo = " + approveInfo);
    }
```



### 2. 收费活动模板

####    2. 1 创建合约

-   方法名 ：` deploy() `

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 用户私钥|
| name |  String  |合约名称|
| symbol | String  |合约简称|
| metaData | String  |描述信息|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| endTime | long   | 活动结束时间戳|
endTime
-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
	"code": "0",
    "data": {
        "trustAddress": "0x919f05c5845e67edd5f7f627f9340c61405d1c39",//平台托管合约地址
        "assetAddress": "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca"//资产合约地址
    },
    "map": {},
    "msg": "操作成功",
    "success": true
}*/
```

-   示例代码

```
    @Test
    public void deploy() throws Exception {
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String name = "Test merchant";
        String symbol = "TM";
        String _metadata = "TestData";
        long endTime = 1564140675;
        JsonResult<DeployResult> jsonResult = chargeActivityService.deploy(privateKey, gasPrice, gasLimit, name, symbol, _metadata);
        System.out.println(JSON.toJSONString(jsonResult));
    }
```



####  2. 2 发布资产

-   方法名 ：` mint() `

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| assetAddress | String  | 资产合约地址|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| to | String   | 资产拥有者|
| metaData | String   | 自定义信息|
| tokenIdList |  List   | 资产Id数组|
| canTrans | Boolean   | 是否可转移|
| canBurn | Boolean   | 是否可销毁|


-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
        "code": "0",
        "data": "0xe4843ccebe183be09e5d306f77eecea42ac2e1e443782cfde952b9a56a5596e7",
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```
-   示例代码

```
    @Test
    public void mint() throws Exception {
        String assetAddress = "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca";
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String to = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        String _metadata = "TestData";
        List<BigInteger> list=new ArrayList<>();
        list.add(BigInteger.valueOf(210001));
        list.add(BigInteger.valueOf(210002));
        list.add(BigInteger.valueOf(210003));
        list.add(BigInteger.valueOf(210004));
        JsonResult<String> map = chargeActivityService.mint(assetAddress,privateKey, gasPrice, gasLimit, to, _metadata,list,true,true);
        System.out.println(JSON.toJSONString(map));

    }
```


#### 2. 3 资产上架

-   方法名 ：` onSales()`

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| assetAddress | String  | 资产合约地址|
| trustAddress | String   | 托管合约地址|
| tokenIdList |  List  |资产id数组|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| price | BigDecimal   | 上架单价|
| owner |  String   | 资产拥有者|


-   返回值类型：`JsonResult`

-   返回说明：

```
/*{
        "code": "0",
        "data": {
            "approveTxId": "0x3964e6f84eda2abe381aa7f9dcf357cf91346ab639b5e78e7e6d4762300edb4e",//资产合约授权返回hash
            "saveApproveTxId": "0x1dd86d2a15bf5d3c8a9fbf33c2a2b0dd571397e74f112a6736307c20a5b86358"//平台托管合约上架返回hash
        },
        "map": {},
        "msg": "操作成功",
            "success": true
    }*/
```

-   示例代码

```
    @Test
    public void onSales() throws Exception {
        String assetAddress = "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca";
        String trustAddress = "0x919f05c5845e67edd5f7f627f9340c61405d1c39";
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String owner = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        List<BigInteger> list=new ArrayList<>();
        list.add(BigInteger.valueOf(390001));
        list.add(BigInteger.valueOf(390002));
        list.add(BigInteger.valueOf(390003));
        list.add(BigInteger.valueOf(390004));
        JsonResult<OnSaleResult> map = chargeActivityService.onSales( assetAddress,  trustAddress,  privateKey,  gasPrice,  gasLimit,  list, new BigDecimal("10"),  owner);
       System.out.println(JSON.toJSONString(map));
    }
```



#### 2. 4 资产下架

-   方法名 ：` offSales（）`

-    参数说明:


| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:|
| trustAddress | String   | 托管合约地址|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| tokenids | List   | 资产id|

-   返回值类型：` JsonResult`

-   返回说明：

```
    /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```


#### 2. 5 创建订单

-   方法名 ：` createOrder()`

>   方法说明：
>   创建订单操作先执行代币合约的 `approve()`授权操作，再执行平台托管合约的`transfer()`交易操作

-   参数说明

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String   | 平台托管合约地址|
| tokenIdList |  List  |资产id数组|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| sumPrice | String   | 总金额|
| owner |  String   | 资产拥有者|

-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
        "code": "0",
        "data": {
        "transferTxId": "0xd1dcd4fc74d8980fde8073fc939ee4bcafd584a0987e5bdaac2917c008a4b7cb",//平台托管合约交易返回hash
        "approveTxId": "0xf69606bc7c25ee450777a7d7836141ed5f8ef4bf1fb30456cf45724b9f60e6f1"//代币授权返回hash
        },
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```
-   示例代码

```
    @Test
    public void createOrder() throws Exception {
        String trustAddress = "0x919f05c5845e67edd5f7f627f9340c61405d1c39";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
        String owner = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        List<BigInteger> list = new ArrayList<>();
        list.add(BigInteger.valueOf(2001));
        list.add(BigInteger.valueOf(2002));
        list.add(BigInteger.valueOf(2003));
        list.add(BigInteger.valueOf(2004));
        String sumPrice = "40";
        JsonResult<Map<String, String>> map = chargeActivityService.createOrder(trustAddress, privateKey, gasPrice, gasLimit, list, sumPrice, owner);
        System.out.println(JSON.toJSONString(map));
    }

```


#### 2. 6 查询指定tokenid上架信息

-   方法名 ：`getApproveInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| tokenId | String |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
{
	"code": "0",
	"data": {
		"owner": "0x591f62ef4b811dc400473cabe0d6641f59186089",
		"tokenid": 450002,
		"value": "1"
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}
```

-   示例代码

```
    @Test
    public void getApproveInfo() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        BigInteger tokenid = BigInteger.valueOf(450002);
        JsonResult<PlatFormApproveInfo> platFormApproveInfo = chargeActivityService.getApproveInfo(trustAddress, tokenid);
        System.out.println(JSON.toJSONString(platFormApproveInfo));
    }
```

#### 2. 7 结束活动

-   方法名 ：`endActivity()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| privateKey | String |私钥|
| gasPrice | BigInteger |tokenId|
| gasLimit | BigInteger |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
 /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```

-   示例代码

```
    @Test
    public void endActivity() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
        JsonResult<String> platFormApproveInfo = chargeActivityService.endActivity(trustAddress, privateKey,gasPrice,gasLimit);
       
    }
```

#### 2. 8 获取活动结束时间

-   方法名 ：`getEndTime()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|



-   返回值类型：`JsonResult`

-   返回说明：

```
{
	"code": "0",
	"data": { 1564140675
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}
```

-   示例代码

```
    @Test
    public void getEndTime() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        BigInteger tokenid = BigInteger.valueOf(450002);
        JsonResult<Long> json = chargeActivityService.getEndTime(trustAddress, tokenid);
    }
```


### 3. 质押活动模板

####    3. 1 创建合约

-   方法名 ：` deploy() `

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 用户私钥|
| name |  String  |合约名称|
| symbol | String  |合约简称|
| metaData | String  |描述信息|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|


-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
	"code": "0",
    "data": {
        "trustAddress": "0x919f05c5845e67edd5f7f627f9340c61405d1c39",//平台托管合约地址
        "assetAddress": "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca"//资产合约地址
    },
    "map": {},
    "msg": "操作成功",
    "success": true
}*/
```

-   示例代码

```
    @Test
    public void deploy() throws Exception {
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String name = "Test merchant";
        String symbol = "TM";
        String _metadata = "TestData";
        JsonResult<DeployResult> jsonResult = pledgeActivityService.deploy(privateKey, gasPrice, gasLimit, name, symbol, _metadata);
        System.out.println(JSON.toJSONString(jsonResult));
    }
```



####  3. 2 发布资产

-   方法名 ：` mint() `

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| assetAddress | String  | 资产合约地址|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| to | String   | 资产拥有者|
| metaData | String   | 自定义信息|
| tokenIdList |  List   | 资产Id数组|
| canTrans | Boolean   | 是否可转移|
| canBurn | Boolean   | 是否可销毁|


-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
        "code": "0",
        "data": "0xe4843ccebe183be09e5d306f77eecea42ac2e1e443782cfde952b9a56a5596e7",
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```
-   示例代码

```
    @Test
    public void mint() throws Exception {
        String assetAddress = "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca";
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String to = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        String _metadata = "TestData";
        List<BigInteger> list=new ArrayList<>();
        list.add(BigInteger.valueOf(210001));
        list.add(BigInteger.valueOf(210002));
        list.add(BigInteger.valueOf(210003));
        list.add(BigInteger.valueOf(210004));
        JsonResult<String> map = pledgeActivityService.mint(assetAddress,privateKey, gasPrice, gasLimit, to, _metadata,list,true,true);
        System.out.println(JSON.toJSONString(map));

    }
```


#### 3. 3 资产上架

-   方法名 ：` onSales()`

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| assetAddress | String  | 资产合约地址|
| trustAddress | String   | 托管合约地址|
| tokenIdList |  List  |资产id数组|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| price | BigDecimal   | 上架单价|
| owner |  String   | 资产拥有者|


-   返回值类型：`JsonResult`

-   返回说明：

```
/*{
        "code": "0",
        "data": {
            "approveTxId": "0x3964e6f84eda2abe381aa7f9dcf357cf91346ab639b5e78e7e6d4762300edb4e",//资产合约授权返回hash
            "saveApproveTxId": "0x1dd86d2a15bf5d3c8a9fbf33c2a2b0dd571397e74f112a6736307c20a5b86358"//平台托管合约上架返回hash
        },
        "map": {},
        "msg": "操作成功",
            "success": true
    }*/
```

-   示例代码

```
    @Test
    public void onSales() throws Exception {
        String assetAddress = "0x41c73a10c9bf866e413d93a2d8ebf2a2a9d533ca";
        String trustAddress = "0x919f05c5845e67edd5f7f627f9340c61405d1c39";
        String privateKey = "afac4908cd6230baa24ef265e5609e9d0908989582779355b307f86a1e6db64d";
        String owner = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        List<BigInteger> list=new ArrayList<>();
        list.add(BigInteger.valueOf(390001));
        list.add(BigInteger.valueOf(390002));
        list.add(BigInteger.valueOf(390003));
        list.add(BigInteger.valueOf(390004));
        JsonResult<OnSaleResult> map = pledgeActivityService.onSales( assetAddress,  trustAddress,  privateKey,  gasPrice,  gasLimit,  list, new BigDecimal("10"),  owner);
       System.out.println(JSON.toJSONString(map));
    }
```



#### 3. 4 资产下架

-   方法名 ：` offSales（）`

-    参数说明:


| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:|
| trustAddress | String   | 托管合约地址|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| tokenids | List   | 资产id|

-   返回值类型：` JsonResult`

-   返回说明：

```
    /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```


#### 3. 5 创建订单

-   方法名 ：` createOrder()`

>   方法说明：
>   创建订单操作先执行代币合约的 `approve()`授权操作，再执行平台托管合约的`transfer()`交易操作

-   参数说明

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String   | 平台托管合约地址|
| tokenIdList |  List  |资产id数组|
| privateKey |  String  |私钥|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|
| sumPrice | String   | 总金额|
| owner |  String   | 资产拥有者|

-   返回值类型：`JsonResult`

-   返回说明：

```
    /*{
        "code": "0",
        "data": {
        "transferTxId": "0xd1dcd4fc74d8980fde8073fc939ee4bcafd584a0987e5bdaac2917c008a4b7cb",//平台托管合约交易返回hash
        "approveTxId": "0xf69606bc7c25ee450777a7d7836141ed5f8ef4bf1fb30456cf45724b9f60e6f1"//代币授权返回hash
        },
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```
-   示例代码

```
    @Test
    public void createOrder() throws Exception {
        String trustAddress = "0x919f05c5845e67edd5f7f627f9340c61405d1c39";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
        String owner = "0xB6901ccE4e9643e73B5E43948CAf888E8BDF9453";
        List<BigInteger> list = new ArrayList<>();
        list.add(BigInteger.valueOf(2001));
        list.add(BigInteger.valueOf(2002));
        list.add(BigInteger.valueOf(2003));
        list.add(BigInteger.valueOf(2004));
        String sumPrice = "40";
        JsonResult<Map<String, String>> map = pledgeActivityService.createOrder(trustAddress, privateKey, gasPrice, gasLimit, list, sumPrice, owner);
        System.out.println(JSON.toJSONString(map));
    }

```


#### 3. 6 查询指定tokenid上架信息

-   方法名 ：`getApproveInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| tokenId | String |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
{
	"code": "0",
	"data": {
		"owner": "0x591f62ef4b811dc400473cabe0d6641f59186089",
		"tokenid": 450002,
		"value": "1"
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}
```

-   示例代码

```
    @Test
    public void getApproveInfo() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        BigInteger tokenid = BigInteger.valueOf(450002);
        JsonResult<PlatFormApproveInfo> json = pledgeActivityService.getApproveInfo(trustAddress, tokenid);
        
    }
```

#### 3. 7 结束活动

-   方法名 ：`endActivity()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| privateKey | String |私钥|
| gasPrice | BigInteger |tokenId|
| gasLimit | BigInteger |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
 /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```

-   示例代码

```
    @Test
    public void endActivity() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
        JsonResult<String> json = pledgeActivityService.endActivity(trustAddress, privateKey,gasPrice,gasLimit);
       
    }
```

#### 3. 8 获取活动结束时间

-   方法名 ：`getEndTime()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|



-   返回值类型：`JsonResult`

-   返回说明：

```
{
	"code": "0",
	"data": { 1564140675
	},
	"map": {},
	"msg": "操作成功",
	"success": true
}
```

-   示例代码

```
    @Test
    public void getEndTime() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        BigInteger tokenid = BigInteger.valueOf(450002);
        JsonResult<Long> json = pledgeActivityService.getEndTime(trustAddress, tokenid);
    }
```


#### 3. 9 验证签到后退还押金

-   方法名 ：`verify()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| privateKey | String |私钥|
| gasPrice | BigInteger |tokenId|
| gasLimit | BigInteger |tokenId|
| tokenId | BigInteger |待验证tokenId|
| owner | String |待验证拥有者地址|

-   返回值类型：`JsonResult`

-   返回说明：

```
 /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```

-   示例代码

```
    @Test
    public void verify() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
       BigInteger tokenid = BigInteger.valueOf(450002);
       String owner="0x0b23eff3a9d8f02829d3b0714cf2e00f5fae2b47";
        JsonResult<String> json = pledgeActivityService.endActivity(trustAddress, privateKey,gasPrice,gasLimit,tokenid,owner);
       
    }
```

#### 3. 10 发起方主动退款

-   方法名 ：`refund()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 交易托管合约地址|
| privateKey | String |私钥|
| gasPrice | BigInteger |tokenId|
| gasLimit | BigInteger |tokenId|
| tokenId | BigInteger |tokenId|


-   返回值类型：`JsonResult`

-   返回说明：

```
 /* {
        "code": "0",
        "data": "0x4d645a3465be5bb54d1ff2aaabbcf49040e715eb8988e434f75e01bc31fed8ea",//hash
        "map": {},
        "msg": "操作成功",
        "success": true
    }*/
```

-   示例代码

```
    @Test
    public void refund() throws Exception {
        String trustAddress = "0x6bc5d6249344b3372f6a18d0285c94f677f2afaa";
        String privateKey = "b6c77d007c04e1b2f1bf8e2f8eab8c012f5a4044ca09f02980ae79b148c921e0";
       BigInteger tokenid = BigInteger.valueOf(450002);
       String owner="0x0b23eff3a9d8f02829d3b0714cf2e00f5fae2b47";
        JsonResult<String> json = pledgeActivityService.refund(trustAddress, privateKey,gasPrice,gasLimit,tokenid);
       
    }
```
