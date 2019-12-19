
# Node SDK API


## **介绍**

Node SDK 调用节点服务，节点服务对节点上721资产定义的事件进行分析处理，为去中心化数据收集提供依据

##  **目录**

- [根据拥有者地址查询我创建的合约](#根据拥有者地址查询我创建的合约)
- [根据合约地址查询所有资产](#根据合约地址查询所有资产)
- [我的【我获得的资产】](#我的【我获得的资产】)
- [我转卖的【正在出售的】](#我转卖的【正在出售的】)
- [获取已上架的资产](#获取已上架的资产)
- [获取未上架的资产](#获取未上架的资产)
- [订单列表](#订单列表)
- [根据交易hash获取订单明细](#根据交易hash获取订单明细)
- [当前合约下的交易记录](#当前合约下的交易记录)



----------

##  **API**

### 根据拥有者地址查询我创建的合约


-   方法名 ：`contracts()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|


-   返回值类型：`List`

-   返回说明：


-   示例代码

```
    /**
     * 【我】创建的所有合约
     */
    @Test
    public void contracts() {
        JsonResult<List<Contract>> contracts = nodeService.contracts("0xd07de12d15e686c013666fb9c47f23c5997faa21");
        print(contracts);

        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //		"id": "9ac13cf75d2746cb862419c74cca3487",
        //		"type": null,
        //		"symbol": "一样",
        //		"name": "测试六",
        //		"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //		"to": null,
        //		"status": "0x1",
        //		"blockNumber": 1767776,
        //		"blockHash": "0x52fc0a515d66de9c65a0c4abd66d16c16c1daf03d26ff53db4f520bb0e2ec646",
        //		"createTime": 1571308805,
        //		"transactionHash": "0x9cbcf3c8b62a18d165b2227232ecc1bc57a260eb0c713a2f675fb3fe6d1730ae",
        //		"value": null,
        //		"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //		"address": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //		"metadata": "{\"normalDepositRefundRate\":\"\",\"images\":\"\",\"name\":\"测试六\",\"timeInfoModel\":{\"tokenPrice\":\"1\",\"name\":\"测试六\",\"startTime\":\"1570982400000\",\"endTime\":\"1571068800000\"},\"templateId\":\"25\",\"endTime\":\"1571068800000\",\"startSellTime\":\"1570982400000\",\"startTime\":\"1570982400000\",\"canReissue\":false,\"abnormalDepositRefundRate\":\"\",\"regType\":\"0\",\"symbol\":\"一样\",\"endSellTime\":\"1571068800000\",\"transferLimit\":\"1\",\"unlockCountdown\":\"1800\",\"assetTransferLimit\":\"3\",\"groupBuyLimit\":\"1\",\"timeInfoList\":\"[{\\\"endTime\\\":\\\"1571068800000\\\",\\\"name\\\":\\\"测试六\\\",\\\"startTime\\\":\\\"1570982400000\\\",\\\"tokenPrice\\\":\\\"1\\\"}]\",\"parInfoModel\":{\"name\":\"测试六\",\"supplyLimit\":\"35\",\"marketPrice\":\"1\",\"maxPrice\":\"1\",\"deleted\":\"false\",\"minPrice\":\"1\",\"price\":\"1\"},\"owner\":\"0xd07de12d15e686c013666fb9c47f23c5997faa21\",\"did\":\"ibEbUzsANbvZv2rhMvDq7K39d1JAAwZiQS\",\"positionId\":\"1002\",\"canBurn\":true,\"location\":\"日本 嘤嘤嘤\",\"imgUrl\":\"QmWr8EdCcbLSgVrysFbFZXVHqGU64iv72ek2sBbyNeKKLb\",\"parInfoList\":\"[{\\\"deleted\\\":false,\\\"marketPrice\\\":\\\"1\\\",\\\"maxPrice\\\":\\\"1\\\",\\\"minPrice\\\":\\\"1\\\",\\\"name\\\":\\\"测试六\\\",\\\"price\\\":\\\"1\\\",\\\"supplyLimit\\\":\\\"35\\\"}]\",\"deleted\":false,\"description\":\"\",\"quantity\":\"5\",\"buyLimit\":\"1\"}",
        //		"supplyLimit": 35,
        //		"transferCount": 2
        //	}],
        //	"map": {}
        //}
    }
```

### 根据合约地址查询所有资产


-   方法名 ：`assets()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void assets() {
        JsonResult<List<Asset>> assets = nodeService.assets(null, null, null);
        print(assets);

        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //		"assetLevel": 1,
        //		"blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //		"blockNumber": 1786736,
        //		"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //		"createTime": 1571309005,
        //		"id": "db16182b0d6e4713a61792aae8da300d",
        //		"metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //		"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //		"price": 1,
        //		"saleStatus": 1,
        //		"status": "0x1",
        //		"tokenId": "1571279480",
        //		"transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //		"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //	}]
        //}
    }
```

### 我的【我获得的资产】

-   方法名 ：`my()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void testMy() {
        JsonResult<List<MyAsset>> my = nodeService.my("0xd07de12d15e686c013666fb9c47f23c5997faa21", null, null);
        print(my);

        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //		"id": "9ac13cf75d2746cb862419c74cca3487",
        //		"type": null,
        //		"symbol": "一样",
        //		"name": "测试六",
        //		"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //		"to": null,
        //		"status": "0x1",
        //		"blockNumber": 1767776,
        //		"blockHash": "0x52fc0a515d66de9c65a0c4abd66d16c16c1daf03d26ff53db4f520bb0e2ec646",
        //		"createTime": 1571308805,
        //		"transactionHash": "0x9cbcf3c8b62a18d165b2227232ecc1bc57a260eb0c713a2f675fb3fe6d1730ae",
        //		"value": null,
        //		"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //		"address": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //		"metadata": "{\"normalDepositRefundRate\":\"\",\"images\":\"\",\"name\":\"测试六\",\"timeInfoModel\":{\"tokenPrice\":\"1\",\"name\":\"测试六\",\"startTime\":\"1570982400000\",\"endTime\":\"1571068800000\"},\"templateId\":\"25\",\"endTime\":\"1571068800000\",\"startSellTime\":\"1570982400000\",\"startTime\":\"1570982400000\",\"canReissue\":false,\"abnormalDepositRefundRate\":\"\",\"regType\":\"0\",\"symbol\":\"一样\",\"endSellTime\":\"1571068800000\",\"transferLimit\":\"1\",\"unlockCountdown\":\"1800\",\"assetTransferLimit\":\"3\",\"groupBuyLimit\":\"1\",\"timeInfoList\":\"[{\\\"endTime\\\":\\\"1571068800000\\\",\\\"name\\\":\\\"测试六\\\",\\\"startTime\\\":\\\"1570982400000\\\",\\\"tokenPrice\\\":\\\"1\\\"}]\",\"parInfoModel\":{\"name\":\"测试六\",\"supplyLimit\":\"35\",\"marketPrice\":\"1\",\"maxPrice\":\"1\",\"deleted\":\"false\",\"minPrice\":\"1\",\"price\":\"1\"},\"owner\":\"0xd07de12d15e686c013666fb9c47f23c5997faa21\",\"did\":\"ibEbUzsANbvZv2rhMvDq7K39d1JAAwZiQS\",\"positionId\":\"1002\",\"canBurn\":true,\"location\":\"日本 嘤嘤嘤\",\"imgUrl\":\"QmWr8EdCcbLSgVrysFbFZXVHqGU64iv72ek2sBbyNeKKLb\",\"parInfoList\":\"[{\\\"deleted\\\":false,\\\"marketPrice\\\":\\\"1\\\",\\\"maxPrice\\\":\\\"1\\\",\\\"minPrice\\\":\\\"1\\\",\\\"name\\\":\\\"测试六\\\",\\\"price\\\":\\\"1\\\",\\\"supplyLimit\\\":\\\"35\\\"}]\",\"deleted\":false,\"description\":\"\",\"quantity\":\"5\",\"buyLimit\":\"1\"}",
        //		"supplyLimit": 35,
        //		"transferCount": 2,
        //		"assetList": [{
        //			"id": "79251d90edcb416ca2531f75c09c8009",
        //			"tokenId": "100000000000000022",
        //			"assetLevel": 2,
        //			"price": 1,
        //			"metaData": "{\"name\":\"测试六\",\"tokenPrice\":\"1\",\"startTime\":\"1570982400000\",\"endTime\":\"1571068800000\"}",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 0,
        //			"contractAddress": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //			"status": "0x1",
        //			"blockNumber": 1767777,
        //			"blockHash": "0x694ca62d2ba607e65a471db7bbd796e3e4655f01dec0d887828661fd97b4d595",
        //			"createTime": 1571308807,
        //			"transactionHash": "0x8ef7e940ccecde94bbc3032c993bac3540fc6e6558dd7e1e8298c0a1dddc43ba",
        //			"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //			"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //		}]
        //	}],
        //	"map": {}
        //}
    }

```




### 我转卖的【正在出售的】



-   方法名 ：`myReselling()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void myReselling() {
        JsonResult<List<MyAsset>> listJsonResult = nodeService.myReselling("0xd07de12d15e686c013666fb9c47f23c5997faa21", null, null);
        print(listJsonResult);

        //{
        //  "code": 0,
        //  "success": true,
        //  "msg": "操作成功",
        //  "data": [
        //    {
        //      "id": "70d3826fe71e4bfa93dc68457c555c70",
        //      "type": null,
        //      "symbol": "ii",
        //      "name": "测试八",
        //      "from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //      "to": null,
        //      "status": "0x1",
        //      "blockNumber": 1774997,
        //      "blockHash": "0x0a8a02f868cf5cf5f9cbfb2f443be052660aa19f2debc20dd6ca480743fa2a87",
        //      "createTime": 1571308883,
        //      "transactionHash": "0x88ffe7c28ddf0e8c6bfc8b6aaf213e875a4058c12415f13f2bcd90437c0dbc3c",
        //      "value": null,
        //      "owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //      "address": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //      "metadata": "{\"regType\":\"0\",\"canBurn\":true,\"abnormalDepositRefundRate\":\"\",\"location\":\"日本 iii\",\"timeInfoModel\":{\"endTime\":\"1571155200000\",\"name\":\"测试八\",\"tokenPrice\":\"2\",\"startTime\":\"1571068800000\"},\"groupBuyLimit\":\"1\",\"startTime\":\"1571068800000\",\"owner\":\"0x5e09d572e2d47cb804b55e27b18846ab4d3f8429\",\"startSellTime\":\"1571068800000\",\"parInfoModel\":{\"minPrice\":\"2\",\"supplyLimit\":\"20\",\"price\":\"2\",\"name\":\"测试八\",\"marketPrice\":\"2\",\"deleted\":\"false\",\"maxPrice\":\"2\"},\"unlockCountdown\":\"1800\",\"timeInfoList\":\"[{\\\"endTime\\\":\\\"1571155200000\\\",\\\"name\\\":\\\"测试八\\\",\\\"startTime\\\":\\\"1571068800000\\\",\\\"tokenPrice\\\":\\\"2\\\"}]\",\"did\":\"imdSkYGQqnGGXF6PXFT3f6JCnahZrXTqY2\",\"images\":\"QmbKFFKM66WMgBhL3e812muqrjG2GjSW7cxS3PxgJnABCL\",\"description\":\"<pre><div style='padding:30px;max-width:100%;'><img  class='product-img' src='http:\\/\\/47.105.136.158:8080\\/ipfs\\/QmbKFFKM66WMgBhL3e812muqrjG2GjSW7cxS3PxgJnABCL'\\/><br\\/><br\\/><\\/div><br\\/><br\\/><br\\/>哦哦哦<\\/pre>\",\"deleted\":false,\"buyLimit\":\"1\",\"name\":\"测试八\",\"endSellTime\":\"1571155200000\",\"quantity\":\"5\",\"symbol\":\"ii\",\"normalDepositRefundRate\":\"\",\"positionId\":\"1002\",\"endTime\":\"1571155200000\",\"templateId\":\"25\",\"canReissue\":false,\"assetTransferLimit\":\"3\",\"parInfoList\":\"[{\\\"deleted\\\":false,\\\"marketPrice\\\":\\\"2\\\",\\\"maxPrice\\\":\\\"2\\\",\\\"minPrice\\\":\\\"2\\\",\\\"name\\\":\\\"测试八\\\",\\\"price\\\":\\\"2\\\",\\\"supplyLimit\\\":\\\"20\\\"}]\",\"transferLimit\":\"1\",\"imgUrl\":\"Qmci9MyiBLQKT7k3dN4Mm2sYyc5XJQA7nrA5ZUuqNdX2nh\"}",
        //      "supplyLimit": 18,
        //      "transferCount": 2,
        //      "assetList": [
        //        {
        //          "id": "f64bf263073f4d6291818d22c8306d82",
        //          "tokenId": "100000000000000006",
        //          "assetLevel": 2,
        //          "price": 4,
        //          "metaData": "{\"endTime\":\"1571155200000\",\"startTime\":\"1571068800000\",\"name\":\"测试八\",\"tokenPrice\":\"2\"}",
        //          "canTrans": null,
        //          "canBurn": null,
        //          "saleStatus": 1,
        //          "contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //          "status": "0x1",
        //          "blockNumber": 1775000,
        //          "blockHash": "0xdb21790a7fafccb431c027c393af52307311113f5038aafdc3e541dc3fbd3c52",
        //          "createTime": 1571308884,
        //          "transactionHash": "0x57daeaa9194182e5d65e173f75ff021d986a8ec05ba69d1bfaafce757abdd2b3",
        //          "owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //          "trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //        }
        //      ]
        //    },
        //    {
        //      "id": "3c13a826b2f2416398bc7675349ad974",
        //      "type": null,
        //      "symbol": "听音乐",
        //      "name": "哦哦哦哦",
        //      "from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //      "to": null,
        //      "status": "0x1",
        //      "blockNumber": 1786735,
        //      "blockHash": "0x66185ea82e1ce9c2a79e49f9837721062c77636c4ffbf2dbd9dbcad2e9f273e0",
        //      "createTime": 1571309003,
        //      "transactionHash": "0x899319289f56210d30631362076c37dee3d3b469f1ec6b925f94d8c98903e529",
        //      "value": null,
        //      "owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //      "address": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //      "metadata": "QmbNNVKn4jiVyMhksF8fFPJQwJCwnA5JYYkhjygUL1iwP9",
        //      "supplyLimit": 24,
        //      "transferCount": 3,
        //      "assetList": [
        //        {
        //          "id": "ec55a45ef01747fd8edd22d77de95277",
        //          "tokenId": "1571279499",
        //          "assetLevel": 2,
        //          "price": 2,
        //          "metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //          "canTrans": null,
        //          "canBurn": null,
        //          "saleStatus": 1,
        //          "contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //          "status": "0x1",
        //          "blockNumber": 1786736,
        //          "blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //          "createTime": 1571309004,
        //          "transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //          "owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //          "trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //        }
        //      ]
        //    }
        //  ],
        //  "map": {}
        //}
    }
```

### 获取已上架的资产

-   方法名 ：`onSale()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|
| level | String  | 1:一手，2：二手|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void testOnSales() {
        JsonResult<List<Asset>> listJsonResult = nodeService.onSale(null, null, null, null);
        print(listJsonResult);
        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //			"id": "c004ec89639f454eb521b9bb5176749a",
        //			"tokenId": "1571279497",
        //			"assetLevel": 1,
        //			"price": 1,
        //			"metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 1,
        //			"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //			"status": "0x1",
        //			"blockNumber": 1786736,
        //			"blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //			"createTime": 1571309004,
        //			"transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //		},
        //		{
        //			"id": "ad6f3124308a4f2297d4e097207fdcb7",
        //			"tokenId": "1571279498",
        //			"assetLevel": 1,
        //			"price": 1,
        //			"metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 1,
        //			"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //			"status": "0x1",
        //			"blockNumber": 1786736,
        //			"blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //			"createTime": 1571309004,
        //			"transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //		},
        //		{
        //			"id": "891ded2011d6469aa2f88227123e882b",
        //			"tokenId": "1571279491",
        //			"assetLevel": 1,
        //			"price": 1,
        //			"metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 1,
        //			"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //			"status": "0x1",
        //			"blockNumber": 1786736,
        //			"blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //			"createTime": 1571309004,
        //			"transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //		}
        //	],
        //	"map": {}
        //}
    }
```
### 获取未上架的资产

-   方法名 ：`offSale()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 拥有者地址|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|
| level | String  | 1:一手，2：二手|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void testOffSales() {
        JsonResult<List<Asset>> listJsonResult = nodeService.offSale(null, null, null);
        print(listJsonResult);
        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //			"id": "6d0b850754834f6db6296c6c9aafeff7",
        //			"tokenId": "100000000000000011",
        //			"assetLevel": 2,
        //			"price": 1,
        //			"metaData": "{\"startTime\":\"1571068800000\",\"name\":\"测试七\",\"tokenPrice\":\"1\",\"endTime\":\"1571155200000\"}",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 0,
        //			"contractAddress": "0x607478e2720997554e6ef8ff04ecc13289815f3f",
        //			"status": "0x1",
        //			"blockNumber": 1774563,
        //			"blockHash": "0xc63bafa26ada9290c9b1194ee1191146797f58631b3d499f477cdf62b7abf1e7",
        //			"createTime": 1571308876,
        //			"transactionHash": "0x34ce72f87feb3035b907eb25c1c6a2a06760c5750c91ba37b61a931379914ff2",
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //		},
        //		{
        //			"id": "de4ebb621a374e009051829371bec8a5",
        //			"tokenId": "100000000000000018",
        //			"assetLevel": 2,
        //			"price": 2,
        //			"metaData": "{\"endTime\":\"1571155200000\",\"startTime\":\"1571068800000\",\"name\":\"测试八\",\"tokenPrice\":\"2\"}",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 0,
        //			"contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //			"status": "0x1",
        //			"blockNumber": 1775000,
        //			"blockHash": "0xdb21790a7fafccb431c027c393af52307311113f5038aafdc3e541dc3fbd3c52",
        //			"createTime": 1571308884,
        //			"transactionHash": "0x57daeaa9194182e5d65e173f75ff021d986a8ec05ba69d1bfaafce757abdd2b3",
        //			"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //			"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //		},
        //		{
        //			"id": "960927bda64f4ff3ae75ead26ff6880a",
        //			"tokenId": "1571279485",
        //			"assetLevel": 2,
        //			"price": 1,
        //			"metaData": "QmTFbujcvnAYasjFUJjGCK7Eg5j8r4vAYLZgH4cJPEcCvu",
        //			"canTrans": null,
        //			"canBurn": null,
        //			"saleStatus": 0,
        //			"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //			"status": "0x1",
        //			"blockNumber": 1786736,
        //			"blockHash": "0xbe7e9dee1ee4846d9b9a8fdd51f42ce0485ee91ab244768046846a23719088f7",
        //			"createTime": 1571309004,
        //			"transactionHash": "0x41d88f58cd707000878469931482ac4a57aea0c0466a8e5629536354e185aba3",
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //		}
        //	],
        //	"map": {}
        //}
    }
```
### 订单列表

-   方法名 ：`orders()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| from | String  | from|
| to | String  | to|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|

-   返回值类型：`List`


-   示例代码

```
    @Test
    public void testOrders() {
        JsonResult<List<Order>> orders = nodeService.orders(null,null, "0x2009ee0b90749a9b76f8ee23323069dbb0658b79", "");
        print(orders);
        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //		"id": "cef9f1ba517843b9a7c4d822ef13a271",
        //		"quantity": 1,
        //		"contractAddress": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //		"status": "0x1",
        //		"blockNumber": 1767811,
        //		"blockHash": "0x07b1b1c88bb38ce210b452d188f283605aa3ec44fee89d9d61d8b74cc990505c",
        //		"createTime": 1571308808,
        //		"transactionHash": "0x30c2bd2ef6e8d90a985f49763e7518dc92d7d1a53f94d6d9d1fd1507870cf72b",
        //		"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //		"to": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //		"level": 1,
        //		"name": "测试六",
        //		"orderStatus": 21,
        //		"orderPrice": 1,
        //		"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5",
        //		"orderItems": [{
        //			"id": "3ab683f731aa44e782441cc1f66b640c",
        //			"quantity": 1,
        //			"tokenId": "100000000000000022",
        //			"contractAddress": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //			"status": "0x1",
        //			"blockNumber": 1767811,
        //			"blockHash": "0x07b1b1c88bb38ce210b452d188f283605aa3ec44fee89d9d61d8b74cc990505c",
        //			"createTime": 1571308808,
        //			"transactionHash": "0x30c2bd2ef6e8d90a985f49763e7518dc92d7d1a53f94d6d9d1fd1507870cf72b",
        //			"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //			"to": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"level": 1,
        //			"name": "测试六",
        //			"orderPrice": 1,
        //			"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //		}]
        //	}],
        //	"map": {}
        //}
    }
```
### 根据交易hash获取订单明细

-   方法名 ：`orderItems()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| transactionHash | String  | 交易hash|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void testOrderItems() {
        JsonResult<List<OrderItem>> listJsonResult = nodeService.orderItems("0x30c2bd2ef6e8d90a985f49763e7518dc92d7d1a53f94d6d9d1fd1507870cf72b");
        print(listJsonResult);
        //{
        //  "code": 0,
        //  "success": true,
        //  "msg": "操作成功",
        //  "data": [
        //    {
        //      "id": "3ab683f731aa44e782441cc1f66b640c",
        //      "quantity": 1,
        //      "tokenId": "100000000000000022",
        //      "contractAddress": "0x2009ee0b90749a9b76f8ee23323069dbb0658b79",
        //      "status": "0x1",
        //      "blockNumber": 1767811,
        //      "blockHash": "0x07b1b1c88bb38ce210b452d188f283605aa3ec44fee89d9d61d8b74cc990505c",
        //      "createTime": 1571308808,
        //      "transactionHash": "0x30c2bd2ef6e8d90a985f49763e7518dc92d7d1a53f94d6d9d1fd1507870cf72b",
        //      "from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //      "to": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //      "level": 1,
        //      "name": "测试六",
        //      "orderPrice": 1,
        //      "trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //    }
        //  ],
        //  "map": {}
        //}

    }
```
### 当前合约下的交易记录


-   方法名 ：`contractOrders()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| from | String  | from|
| to | String  | to|
| contractAddress | String  | 合约地址|
| trustAddress | String  | 托管地址|


-   返回值类型：`List`


-   示例代码

```
    @Test
    public void contractOrders() {
        JsonResult<List<ContractOrders>> listJsonResult = nodeService.contractOrders(null, null, null, null);
        print(listJsonResult);

        //{
        //	"code": 0,
        //	"success": true,
        //	"msg": "操作成功",
        //	"data": [{
        //			"id": "70d3826fe71e4bfa93dc68457c555c70",
        //			"type": null,
        //			"symbol": "ii",
        //			"name": "测试八",
        //			"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"to": null,
        //			"status": "0x1",
        //			"blockNumber": 1774997,
        //			"blockHash": "0x0a8a02f868cf5cf5f9cbfb2f443be052660aa19f2debc20dd6ca480743fa2a87",
        //			"createTime": 1571308883,
        //			"transactionHash": "0x88ffe7c28ddf0e8c6bfc8b6aaf213e875a4058c12415f13f2bcd90437c0dbc3c",
        //			"value": null,
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"address": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //			"metadata": "{\"regType\":\"0\",\"canBurn\":true,\"abnormalDepositRefundRate\":\"\",\"location\":\"日本 iii\",\"timeInfoModel\":{\"endTime\":\"1571155200000\",\"name\":\"测试八\",\"tokenPrice\":\"2\",\"startTime\":\"1571068800000\"},\"groupBuyLimit\":\"1\",\"startTime\":\"1571068800000\",\"owner\":\"0x5e09d572e2d47cb804b55e27b18846ab4d3f8429\",\"startSellTime\":\"1571068800000\",\"parInfoModel\":{\"minPrice\":\"2\",\"supplyLimit\":\"20\",\"price\":\"2\",\"name\":\"测试八\",\"marketPrice\":\"2\",\"deleted\":\"false\",\"maxPrice\":\"2\"},\"unlockCountdown\":\"1800\",\"timeInfoList\":\"[{\\\"endTime\\\":\\\"1571155200000\\\",\\\"name\\\":\\\"测试八\\\",\\\"startTime\\\":\\\"1571068800000\\\",\\\"tokenPrice\\\":\\\"2\\\"}]\",\"did\":\"imdSkYGQqnGGXF6PXFT3f6JCnahZrXTqY2\",\"images\":\"QmbKFFKM66WMgBhL3e812muqrjG2GjSW7cxS3PxgJnABCL\",\"description\":\"<pre><div style='padding:30px;max-width:100%;'><img  class='product-img' src='http:\\/\\/47.105.136.158:8080\\/ipfs\\/QmbKFFKM66WMgBhL3e812muqrjG2GjSW7cxS3PxgJnABCL'\\/><br\\/><br\\/><\\/div><br\\/><br\\/><br\\/>哦哦哦<\\/pre>\",\"deleted\":false,\"buyLimit\":\"1\",\"name\":\"测试八\",\"endSellTime\":\"1571155200000\",\"quantity\":\"5\",\"symbol\":\"ii\",\"normalDepositRefundRate\":\"\",\"positionId\":\"1002\",\"endTime\":\"1571155200000\",\"templateId\":\"25\",\"canReissue\":false,\"assetTransferLimit\":\"3\",\"parInfoList\":\"[{\\\"deleted\\\":false,\\\"marketPrice\\\":\\\"2\\\",\\\"maxPrice\\\":\\\"2\\\",\\\"minPrice\\\":\\\"2\\\",\\\"name\\\":\\\"测试八\\\",\\\"price\\\":\\\"2\\\",\\\"supplyLimit\\\":\\\"20\\\"}]\",\"transferLimit\":\"1\",\"imgUrl\":\"Qmci9MyiBLQKT7k3dN4Mm2sYyc5XJQA7nrA5ZUuqNdX2nh\"}",
        //			"supplyLimit": 18,
        //			"transferCount": 2,
        //			"orders": [{
        //					"id": "f2a2e8c17021451d86e3459d662c9a98",
        //					"quantity": 1,
        //					"contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //					"status": "0x1",
        //					"blockNumber": 1775109,
        //					"blockHash": "0x196804febcbbdbfbb361d7d2016fd48741a5fcd7a8cada581891cb6df3aa95ab",
        //					"createTime": 1571308886,
        //					"transactionHash": "0x73112a60bdb0eebe1e38bfaee5a908fa3cb1bdd9242f1bf917b08355f4f3b997",
        //					"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //					"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //					"level": 1,
        //					"name": "测试八",
        //					"orderStatus": 21,
        //					"orderPrice": 2,
        //					"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5",
        //					"orderItems": [{
        //						"id": "cc82a6f045ed46308243d89d6d3faaa6",
        //						"quantity": 1,
        //						"tokenId": "100000000000000006",
        //						"contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //						"status": "0x1",
        //						"blockNumber": 1775109,
        //						"blockHash": "0x196804febcbbdbfbb361d7d2016fd48741a5fcd7a8cada581891cb6df3aa95ab",
        //						"createTime": 1571308886,
        //						"transactionHash": "0x73112a60bdb0eebe1e38bfaee5a908fa3cb1bdd9242f1bf917b08355f4f3b997",
        //						"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //						"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //						"level": 1,
        //						"name": "测试八",
        //						"orderPrice": 2,
        //						"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //					}]
        //				},
        //				{
        //					"id": "ea1a525fc5694b4a95bd62d9e726e09d",
        //					"quantity": 1,
        //					"contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //					"status": "0x1",
        //					"blockNumber": 1775416,
        //					"blockHash": "0x22fa03d319bd16714c30b69baa82ad948c27c5697f287380eefe0b672a78cdac",
        //					"createTime": 1571308889,
        //					"transactionHash": "0x6a445c36c9d9fd042ae9d9dd81d45949953a609d5551ef7962d625f3d69b1fa6",
        //					"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //					"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //					"level": 1,
        //					"name": "测试八",
        //					"orderStatus": 21,
        //					"orderPrice": 2,
        //					"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5",
        //					"orderItems": [{
        //						"id": "34ef34fb1cb2404cb7fa724f749d731b",
        //						"quantity": 1,
        //						"tokenId": "100000000000000018",
        //						"contractAddress": "0x23a2f4ba13ecfdeb127c2459489b667e369fae5f",
        //						"status": "0x1",
        //						"blockNumber": 1775416,
        //						"blockHash": "0x22fa03d319bd16714c30b69baa82ad948c27c5697f287380eefe0b672a78cdac",
        //						"createTime": 1571308889,
        //						"transactionHash": "0x6a445c36c9d9fd042ae9d9dd81d45949953a609d5551ef7962d625f3d69b1fa6",
        //						"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //						"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //						"level": 1,
        //						"name": "测试八",
        //						"orderPrice": 2,
        //						"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //					}]
        //				}
        //			]
        //		},
        //		{
        //			"id": "3c13a826b2f2416398bc7675349ad974",
        //			"type": null,
        //			"symbol": "听音乐",
        //			"name": "哦哦哦哦",
        //			"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"to": null,
        //			"status": "0x1",
        //			"blockNumber": 1786735,
        //			"blockHash": "0x66185ea82e1ce9c2a79e49f9837721062c77636c4ffbf2dbd9dbcad2e9f273e0",
        //			"createTime": 1571309003,
        //			"transactionHash": "0x899319289f56210d30631362076c37dee3d3b469f1ec6b925f94d8c98903e529",
        //			"value": null,
        //			"owner": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //			"address": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //			"metadata": "QmbNNVKn4jiVyMhksF8fFPJQwJCwnA5JYYkhjygUL1iwP9",
        //			"supplyLimit": 24,
        //			"transferCount": 3,
        //			"orders": [{
        //					"id": "6b0c787f7bfc42fab53d1167962a94dd",
        //					"quantity": 1,
        //					"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //					"status": "0x1",
        //					"blockNumber": 1788415,
        //					"blockHash": "0x833e3b8ade96cc61e33f5c50d6bb4543c9481b2e58ab938a1e2f102c5927e516",
        //					"createTime": 1571309021,
        //					"transactionHash": "0x2113b1338efc47a6c7f18c83b6fdb1d7f7709efac68d6762feccd6092f447ab3",
        //					"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //					"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //					"level": 1,
        //					"name": "哦哦哦哦",
        //					"orderStatus": 21,
        //					"orderPrice": 1,
        //					"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69",
        //					"orderItems": [{
        //						"id": "7afd0e2e93d549da9d2ac406095eefb1",
        //						"quantity": 1,
        //						"tokenId": "1571279499",
        //						"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //						"status": "0x1",
        //						"blockNumber": 1788415,
        //						"blockHash": "0x833e3b8ade96cc61e33f5c50d6bb4543c9481b2e58ab938a1e2f102c5927e516",
        //						"createTime": 1571309021,
        //						"transactionHash": "0x2113b1338efc47a6c7f18c83b6fdb1d7f7709efac68d6762feccd6092f447ab3",
        //						"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //						"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //						"level": 1,
        //						"name": "哦哦哦哦",
        //						"orderPrice": 1,
        //						"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //					}]
        //				},
        //				{
        //					"id": "48a39d33e89c4f86885715e3c827df81",
        //					"quantity": 1,
        //					"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //					"status": "0x1",
        //					"blockNumber": 1788816,
        //					"blockHash": "0x7718fa3e780e313f7a1e34ea34c99bb46fb3f64fd2f53d5fc8b0f2a2dcfe1601",
        //					"createTime": 1571309025,
        //					"transactionHash": "0xa413cb8e6db96a558d64ceb118ad4f8fa47137f8ec785eb2964529178e7b1e20",
        //					"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //					"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //					"level": 1,
        //					"name": "哦哦哦哦",
        //					"orderStatus": 21,
        //					"orderPrice": 1,
        //					"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69",
        //					"orderItems": [{
        //						"id": "a4f36e2d842f427ba18b2b002caa15ea",
        //						"quantity": 1,
        //						"tokenId": "1571279485",
        //						"contractAddress": "0xc0312155e88a99aebe6a8b0698734052cfa5ed41",
        //						"status": "0x1",
        //						"blockNumber": 1788816,
        //						"blockHash": "0x7718fa3e780e313f7a1e34ea34c99bb46fb3f64fd2f53d5fc8b0f2a2dcfe1601",
        //						"createTime": 1571309025,
        //						"transactionHash": "0xa413cb8e6db96a558d64ceb118ad4f8fa47137f8ec785eb2964529178e7b1e20",
        //						"from": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //						"to": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //						"level": 1,
        //						"name": "哦哦哦哦",
        //						"orderPrice": 1,
        //						"trustAddress": "0x65ce882698521e714fd683da4bee4175fbe7de69"
        //					}]
        //				}
        //			]
        //		},
        //		{
        //			"id": "58fe74cf7d44491db2a82e1fa5ac9c0e",
        //			"type": null,
        //			"symbol": "你好",
        //			"name": "测试七",
        //			"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //			"to": null,
        //			"status": "0x1",
        //			"blockNumber": 1774562,
        //			"blockHash": "0x475901795577542d5d5e0cc4f667b07040dd1587e2a2ce297bb0f88c62c5841a",
        //			"createTime": 1571308875,
        //			"transactionHash": "0x343e9b01f0e3f5d0c47f3581431808c02a742d1b44d8c5c400502c82cc78ce12",
        //			"value": null,
        //			"owner": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //			"address": "0x607478e2720997554e6ef8ff04ecc13289815f3f",
        //			"metadata": "{\"quantity\":\"5\",\"endTime\":\"1571155200000\",\"symbol\":\"你好\",\"endSellTime\":\"1571155200000\",\"buyLimit\":\"1\",\"startTime\":\"1571068800000\",\"unlockCountdown\":\"1800\",\"parInfoModel\":{\"supplyLimit\":\"48\",\"deleted\":\"false\",\"name\":\"测试七\",\"marketPrice\":\"1\",\"price\":\"1\",\"minPrice\":\"1\",\"maxPrice\":\"1\"},\"location\":\"日本 雨\",\"normalDepositRefundRate\":\"\",\"startSellTime\":\"1571068800000\",\"canBurn\":true,\"imgUrl\":\"QmSsf4eLE1knNUtK2eMBrjBpqTVAFBaMZAhHCvhKCYcPbJ\",\"timeInfoList\":\"[{\\\"endTime\\\":\\\"1571155200000\\\",\\\"name\\\":\\\"测试七\\\",\\\"startTime\\\":\\\"1571068800000\\\",\\\"tokenPrice\\\":\\\"1\\\"}]\",\"abnormalDepositRefundRate\":\"\",\"groupBuyLimit\":\"1\",\"deleted\":false,\"regType\":\"0\",\"timeInfoModel\":{\"endTime\":\"1571155200000\",\"tokenPrice\":\"1\",\"startTime\":\"1571068800000\",\"name\":\"测试七\"},\"parInfoList\":\"[{\\\"deleted\\\":false,\\\"marketPrice\\\":\\\"1\\\",\\\"maxPrice\\\":\\\"1\\\",\\\"minPrice\\\":\\\"1\\\",\\\"name\\\":\\\"测试七\\\",\\\"price\\\":\\\"1\\\",\\\"supplyLimit\\\":\\\"48\\\"}]\",\"images\":\"\",\"owner\":\"0xd07de12d15e686c013666fb9c47f23c5997faa21\",\"canReissue\":false,\"templateId\":\"25\",\"description\":\"嘿嘿\",\"assetTransferLimit\":\"3\",\"positionId\":\"1002\",\"did\":\"ibEbUzsANbvZv2rhMvDq7K39d1JAAwZiQS\",\"name\":\"测试七\",\"transferLimit\":\"1\"}",
        //			"supplyLimit": 47,
        //			"transferCount": 1,
        //			"orders": [{
        //				"id": "aaa6e7ba4ed742da8506c2f19aa66d88",
        //				"quantity": 1,
        //				"contractAddress": "0x607478e2720997554e6ef8ff04ecc13289815f3f",
        //				"status": "0x1",
        //				"blockNumber": 1774649,
        //				"blockHash": "0xe37434b94b6e05c7220319f85b921c4f07decbd972ff1ecde1f31e9fa431fc9a",
        //				"createTime": 1571308879,
        //				"transactionHash": "0xcbe4148c66ae70aea2c1afdd63bac2b3e27005ba9023426974a5b2639c4052f1",
        //				"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //				"to": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //				"level": 1,
        //				"name": "测试七",
        //				"orderStatus": 21,
        //				"orderPrice": 1,
        //				"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5",
        //				"orderItems": [{
        //					"id": "3c12b71194c4415eb1c3832ec06b3924",
        //					"quantity": 1,
        //					"tokenId": "100000000000000011",
        //					"contractAddress": "0x607478e2720997554e6ef8ff04ecc13289815f3f",
        //					"status": "0x1",
        //					"blockNumber": 1774649,
        //					"blockHash": "0xe37434b94b6e05c7220319f85b921c4f07decbd972ff1ecde1f31e9fa431fc9a",
        //					"createTime": 1571308879,
        //					"transactionHash": "0xcbe4148c66ae70aea2c1afdd63bac2b3e27005ba9023426974a5b2639c4052f1",
        //					"from": "0xd07de12d15e686c013666fb9c47f23c5997faa21",
        //					"to": "0x5e09d572e2d47cb804b55e27b18846ab4d3f8429",
        //					"level": 1,
        //					"name": "测试七",
        //					"orderPrice": 1,
        //					"trustAddress": "0xddb8f0d0f69faf4a46d08eeae773e69ad860aaa5"
        //				}]
        //			}]
        //		}
        //	],
        //	"map": {}
        //}
    }
```
