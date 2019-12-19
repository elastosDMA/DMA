# Profile API

## **介绍**

Profile是一个开放式的数据结构，包含了通用用户肖像的profile，以及和特定场景及业务相关的extended profile。在用户授权的情况下，相关的应用可以通过使用用户的profile去实现商业行为和收益，而授权的个人也因为提供了profile可以得到自己应该分享到的收益。在应用层面，用户的认证及诚信机制亦可以基于Profile来实现。

## **目录**

- [设置did信息](#1-设置did信息)
- [根据key获取指定txid的did信息](#3-根据key获取指定txid的did信息)
- [删除指定key的信息](#4-删除指定key的信息)
- [修改指定key的信息](#5-修改指定key的信息)
- [根据did获取多个key信息](#7-根据did获取多个key信息)
- [根据did获取所有信息](#8-根据did获取所有信息)
- [根据did获取所有可用信息](#9-根据did获取所有可用信息)
- [根据did获取所有已删除Key](#10-根据did获取所有已删除Key)
- [根据did获取指定key信息](#11-根据did获取指定key信息)


##  **API**


###   1. 设置did信息

-   方法名 ：`setDIDInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| didPrivateKey | String  | did拥有者私钥|
| payPrivateKey | String  | 上链费用支付者私钥私钥|
| map | Map  | 信息(以key-value形式存储)|



-   返回值类型：`ReturnMsgEntity`


-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|


-   示例代码

```
  @Test
    public void test() {
        String didPrivateKey = "4B1AA0C6F0BF55BDF3DB22122215FBAE5743B0D5BB199AF951AF6306E812704E";
        String payPrivateKey = "4B1AA0C6F0BF55BDF3DB22122215FBAE5743B0D5BB199AF951AF6306E812704E";
        Map<String, String> map = new HashMap<>();
        map.put("test_key1", "test_value");
        passportService.setAgentInfo(didPrivateKey, payPrivateKey, map);
    }
```




###   3. 根据key获取指定txid的did信息

-   方法名 ：`getAgentInfoByTxid()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| txid | String  | 交易txid|
| key | String  | 信息key|


-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
	@Test
    public void getAgentInfoByTxid() {
        String txid = "02475a4f159dde180fb4c24c3e05d396bfb9e153f076c039d23a45bc69174646";
        String key = "test";
        ReturnMsgEntity returnMsgEntity = profileService.getAgentInfoByTxid(txid, key);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }

```



###   4. 删除指定key的信息

-   方法名 ：`deleteAgentInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| didPrivateKey | String  | did拥有者私钥|
| key | String  | 信息key|


-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
  @Test
    public void deleteAgentInfo() {
        String key = "test";
        String didPrivateKey="4B1AA0C6F0BF55BDF3DB22122215FBAE5743B0D5BB199AF951AF6306E812704E";
        ReturnMsgEntity returnMsgEntity = profileService.deleteAgentInfo(didPrivateKey, key);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```


###   5. 修改指定key的信息

-   方法名 ：`updateAgentInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| didPrivateKey | String  | did拥有者私钥|
| key | String  | 信息key|
| propertie | String  | 修改内容|

-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
	@Test
    public void updateAgentInfo() {
        String key = "test";
        String propertie="test_value";
        String didPrivateKey="4B1AA0C6F0BF55BDF3DB22122215FBAE5743B0D5BB199AF951AF6306E812704E";
        ReturnMsgEntity returnMsgEntity = profileService.updateAgentInfo(didPrivateKey, key,propertie);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```





###   7. 根据did获取多个key信息

-   方法名 ：`getDIDInfoByKeys()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| did | String  | txid|
| propertyKey | Collection<String>   | 可变长 key|


-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
    @Test
    public void getDIDInfoByKeys() {
        String did = "io3KrMrJczRyDNRyLhK7ejpdzgQq6rTN2H";
        Collection<String> collection=new ArrayList<>();
        collection.add("test_key1");
        collection.add("test_key2");
        ReturnMsgEntity returnMsgEntity = profileService.getDIDInfoByKeys(did,collection);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```

###   8. 根据did获取所有信息

-   方法名 ：`getAllAgentInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| did | String  | txid|



-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
    @Test
    public void getAllAgentInfo() {
        String did = "io3KrMrJczRyDNRyLhK7ejpdzgQq6rTN2H";
        ReturnMsgEntity returnMsgEntity = profileService.getAllAgentInfo(did);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```


###   9. 根据did获取所有可用信息

-   方法名 ：`getNormalAgentInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| did | String  | txid|



-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
    @Test
    public void getNormalAgentInfo() {
        String did = "io3KrMrJczRyDNRyLhK7ejpdzgQq6rTN2H";
        ReturnMsgEntity returnMsgEntity = profileService.getNormalAgentInfo(did);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }

```


###   10. 根据did获取所有已删除Key

-   方法名 ：`getDeprecatedAgentInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| did | String  | txid|



-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
    @Test
    public void getDeprecatedAgentInfo() {
        String did = "io3KrMrJczRyDNRyLhK7ejpdzgQq6rTN2H";
        ReturnMsgEntity returnMsgEntity = profileService.getDeprecatedAgentInfo(did);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```



###   11. 根据did获取指定key信息

-   方法名 ：`getAgentInfoByKey()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| did | String  | txid|
| key | String  | 信息key|


-   返回值类型：`ReturnMsgEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| status | Long  | 状态码(200 成功；404 错误)|
| result | String  | 返回内容|



-   示例代码

```
    @Test
    public void getAgentInfoByKey() {
        String did = "io3KrMrJczRyDNRyLhK7ejpdzgQq6rTN2H";
        String key="test";
        ReturnMsgEntity returnMsgEntity = profileService.getAgentInfoByKey(did,key);
        System.out.println(JSONObject.toJSONString(returnMsgEntity));
    }
```


