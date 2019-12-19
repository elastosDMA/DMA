[toc]

# AssetManagement API

## **介绍**

AssetManagement API是对AssetManagement模块的封装。使用AssetManagement API可完成对资产的管理、确权。快速开发请阅读以下文档。

## **API**

##  **目录**

- [创建合约](#-创建合约)
- [创建资产](#-创建资产)
- [批量创建资产](#-批量创建资产)
- [查询拥有资产数量](#-查询拥有资产数量)
- [查询资产的拥有者地址](#-查询资产的拥有者地址)
- [安全转移资产](#-安全转移资产)
- [转移资产](#-转移资产)
- [资产授权](#-资产授权)
- [资产批量授权](#-资产批量授权)
- [合约名字](#-合约名字)
- [合约拥有者](#-合约拥有者)
- [合约简称](#-合约简称)
- [查询tokenId的data信息](#-查询tokenId的data信息)
- [查询总发行token数量](#-查询总发行token数量)
- [根据下标查询tokenId](#-根据下标查询tokenId)
- [根据资产id获取授权地址](#-根据资产id获取授权地址)
- [获取资产合约拥有者地址](#-获取资产合约拥有者地址)
- [根据地址查询所拥有资产id](#-根据地址查询所拥有资产id)
- [根据资产id查询资产拥有者](#-根据资产id查询资产拥有者)
- [根据资产id查询资产信息](#-根据资产id查询资产信息)
- [获取合约信息](#-获取合约信息)
- [销毁资产](#-销毁资产)
- [根据地址查询资产数量](#-根据地址查询资产数量)
- [根据hash查询交易状态](#-根据hash查询交易状态)




----------

###  创建合约

-   方法名 ：`deploy()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| gasPrice | String  | gas|
| gasLimit | String  | gas限制|
| name | String  | 资产名称|
| symbol | String  | 资产标识符|
| metadata | String  | 单元数据|
| destroyed | String  | 是否可销毁|


-   返回值类型：`String`

-   返回说明： 资产合约地址

-   示例代码

```

    /**
     * 创建资产合约
     */
    @Test
    public void deploy() throws Exception {
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        String name = "Test Asset";//资产名称
        String symbol = "TA";//
        String _metadata = "TestData";
        String assetAddress = assetManagementService.deploy(privateKey, gasPrice, gasLimit, name, symbol, _metadata);
        System.out.println(assetAddress);//资产合约地址
        //0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce
    }

```

###    创建资产

-   方法名 ：`mint()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 资产归属者地址|
| _info | String  | 资产信息|
| tokenid | BigInteger  | 资产id|
| _isTransfer | Boolean  | 资产是否可转移|
| _isBurn | Boolean  | 资产是否可销毁|


-   返回值类型：`String`

-   返回说明： 

>   交易hash

-   示例代码

```
    /**
     * 创建资产
     */
    @Test
    public void mint() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        BigInteger tokenid = BigInteger.valueOf(1001);
        String to = "0xA258f950203b46A4036CE4c71BC64CE1d010EaaC";//资产拥有者
        String info = "testInfo";//资产信息
        String hash = assetManagementService.mint(assetAddress, privateKey, gasPrice, gasLimit, to, info, tokenid, true, true);
        System.out.println(hash);
    }
```

###    批量创建资产

-   方法名 ：`mintWithArray()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 资产归属者地址|
| _info | String  | 资产信息|
| tokenid | List  | 资产id|
| _isTransfer | Boolean  | 资产是否可转移|
| _isBurn | Boolean  | 资产是否可销毁|


-   返回值类型：`String`

-   返回说明：

>   交易hash

-   示例代码

```
    /**
     * 批量创建资产
     */
    @Test
    public void mintWithArray() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        List<BigInteger> list = new ArrayList<>();//资产id数组
        list.add(BigInteger.valueOf(1001));
        list.add(BigInteger.valueOf(1002));
        list.add(BigInteger.valueOf(1003));
        String to = "0xA258f950203b46A4036CE4c71BC64CE1d010EaaC";//资产拥有者
        String info = "testInfo";//资产信息
        String hash = assetManagementService.mintWithArray(assetAddress, privateKey, gasPrice, gasLimit, to, info, list, true, true);
        System.out.println(hash);
    }

```



### 查询拥有资产数量


-   方法名 ：`balanceOf()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner | String  | 拥有者地址|


-   返回值类型：`BigInteger`

-   返回说明： 数量

### 查询资产的拥有者地址
-   方法名 ：`getTokenOwner()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| tokenId | number  | tokenId|


-   返回值类型：`String`

-   返回说明： 拥有者地址

### 安全转移资产

-   方法名 ：`safeTransferFrom()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥 |
| from | String  | 发起方地址|
| to | String  | 接收地址|
| data | String  | 若指定表示只能转移给指定合约|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |

-   返回值类型：`String`

-   返回说明： hash

### 转移资产

-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 资产归属者地址|
| tokenid | BigInteger  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   交易hash

-   示例代码

```
    /*
   * 转移资产
   *
   * */
    @Test
    public void transfer() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "9fab7194e57f483c9bf27a8583c0abf4488a64529a12e8bfec4b76efbe66732a";//私钥
        BigInteger tokenid=BigInteger.valueOf(1001);//资产id
        String from = "0xA258f950203b46A4036CE4c71BC64CE1d010EaaC";//资产拥有者
        String to = "0x21f017BA0937426e8d68417b59658e2DC74c8936";//资产接收者
        String hash = assetManagementService.transfer(assetAddress, privateKey, gasPrice, gasLimit, from, to, tokenid);
        System.out.println(hash);//资产合约地址
    }
```

### 批量转移资产

-   方法名 ：`transferWithAarry()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 资产归属者地址|
| tokenids | List  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   交易hash

-   示例代码

```
    /*
    * 批量转移资产
    *
    * */
    @Test
    public void transferWithAarry() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "9fab7194e57f483c9bf27a8583c0abf4488a64529a12e8bfec4b76efbe66732a";//私钥
        List<BigInteger> list = new ArrayList<>();//资产id数组
        list.add(BigInteger.valueOf(1002));
        String from = "0xA258f950203b46A4036CE4c71BC64CE1d010EaaC";//资产拥有者
        String to = "0x21f017BA0937426e8d68417b59658e2DC74c8936";//资产接收者
        String hash = assetManagementService.transferWithAarry(assetAddress, privateKey, gasPrice, gasLimit, from, to, list);
        System.out.println(hash);
    }
```



### 资产授权


-   方法名 ：`approve()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 授权地址|
| tokenid | BigInteger  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   交易hash

-   示例代码

```
    /**
     * 资产授权
     */
    @Test
    public void approve() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        BigInteger tokenid=BigInteger.valueOf(1003);//资产id
        String to = "0x21f017BA0937426e8d68417b59658e2DC74c8936";//授权地址者
        String hash = assetManagementService.approve(assetAddress, privateKey, gasPrice, gasLimit, to, tokenid);
        System.out.println(hash);
    }
```

###    资产批量授权

-   方法名 ：`approveWithAarry()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| privateKey | String  | 私钥|
| gasPrice | BigInteger  | gas|
| gasLimit | BigInteger  | gas限制|
| _to | String  | 授权地址|
| tokenids | List  | 资产id|


-   返回值类型：`String`

-   返回说明： 

>   交易hash


-   示例代码

```
    /**
     * 批量资产授权
     */
    @Test
    public void approveWithAarry() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        List<BigInteger> list = new ArrayList<>();//资产id数组
        list.add(BigInteger.valueOf(1002));
        String to = "0x21f017BA0937426e8d68417b59658e2DC74c8936";//授权地址者
        String hash = assetManagementService.approveWithAarry(assetAddress, privateKey, gasPrice, gasLimit, to, list);
        System.out.println(hash);
    }
```






### 合约名字
-   方法名 ：`getContractName()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|

-   返回值类型：`String`

-   返回说明： 

>   合约名称

### 合约拥有者
-   方法名 ：`getContractOwner()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|

-   返回值类型：`String`

-   返回说明： 

>   合约拥有者

### 合约简称
-   方法名 ：`getContractSymbol()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|

-   返回值类型：`String`

-   返回说明： 

>   合约简称（符号）

### 查询tokenId的data信息
-   方法名 ：`getTokenURI()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| tokenId | String  | tokenId|

-   返回值类型：`String`

-   返回说明： 

>   uri


### 查询总发行token数量
-   方法名 ：`totalSupply()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|

-   返回值类型：`number`

-   返回说明： 

>   总发行量

### 根据下标查询tokenId

-   方法名 ：`tokenByIndex()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| index | number  | index|

-   返回值类型：`number`

-   返回说明： 

>   tokenId




###    根据资产id获取授权地址

方法名 ：`getApproved()`

参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| tokenids | List  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   授权地址

-   示例代码

```
    /*
    * 获取授权地址
    * */
    @Test
    public void getApproved() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        BigInteger tokenid = BigInteger.valueOf(1002);
        String approvedAddress = assetManagementService.getApproved(assetAddress, tokenid);
        System.out.println(approvedAddress);
    }
```


###    获取资产合约拥有者地址

-   方法名 ：`owner()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|


-   返回值类型：`String`

-   返回说明： 

>   资产合约拥有者地址

-   示例代码

```
    /*
    * 资产合约拥有者
    * */
    @Test
    public void owner() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String owner = assetManagementService.owner(assetAddress);
        System.out.println(owner);
    }
```



###    根据地址查询所拥有资产id

-   方法名 ：`tokenIds()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| owner | String  | 拥有者地址|


-   返回值类型：`List<BigInteger>`

-   返回说明： 

>   资产id数组

-   示例代码

```
     /*
    * 拥有的资产id
    *
    * */
    @Test
    public void tokenIds() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String owner = "0x21f017BA0937426e8d68417b59658e2DC74c8936";
        List<BigInteger> tokenIds = assetManagementService.tokenIds(assetAddress, owner);
        System.out.println(JSON.toJSONString(tokenIds));
    }
```

###    根据资产id查询资产拥有者

-   方法名 ：`getTokenOwner()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| tokenId | BigInteger  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   资产拥有者

-   示例代码

```
     /*
    * 资产拥有者
    * */
    @Test
    public void ownerOf() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        BigInteger tokenid = BigInteger.valueOf(1002);
        String ownerOf = assetManagementService.getTokenOwner(assetAddress, tokenid);
        System.out.println(ownerOf);
    }
```



###    根据资产id查询资产信息

-   方法名 ：`getAssetInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| tokenId | BigInteger  | 资产id|


-   返回值类型：`AssetInfoDto`

-   返回说明： 

| 返回值 | 返回值类型 | 返回值说明|
| :----:| :----:  | :----:  |
| owner | String  | 资产拥有者地址|
| isTransfer | BigInteger  | 是否可转移|
| isBurn | BigInteger  | 是否可销毁|
| data | BigInteger  | 资产信息|

-   示例代码

```
    /*
    * 资产信息
    * */
    @Test
    public void assetInfo() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        BigInteger tokenid = BigInteger.valueOf(1002);
        AssetInfoDto assetInfoDto = assetManagementService.assetInfo(assetAddress, tokenid);
        System.out.println(JSON.toJSONString(assetInfoDto));
    }
```


###    获取合约信息

-   方法名 ：`getContractMetadata()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|


-   返回值类型：`ContractInfoDto`

-   返回说明： 

| 返回值 | 返回值类型 | 返回值说明|
| :----:| :----:  | :----:  |
| name | String  | 合约名称|
| symbol | BigInteger  | 合约标识符|
| metadata | BigInteger  | 合约单元数据|
| owner | BigInteger  | 合约拥有者|

-   示例代码

```
    /*
    * 资产合约信息
    * */
    @Test
    public void getContractMetadata() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        ContractInfoDto contractInfoDto = assetManagementService.getContractMetadata(assetAddress);
        System.out.println(JSON.toJSONString(contractInfoDto));
    }
```


###    销毁资产

-   方法名 ：`burn()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| tokenId | BigInteger  | 资产id|


-   返回值类型：`String`

-   返回说明：

>   hash值

-   示例代码

```
    /**
     * 资产授权
     */
    @Test
    public void burn() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String privateKey = "f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";//私钥
        BigInteger tokenid=BigInteger.valueOf(1003);//资产id
        String owner = "0x21f017BA0937426e8d68417b59658e2DC74c8936";//资产拥有者地址
        String hash = assetManagementService.burn(assetAddress, privateKey, gasPrice, gasLimit, owner, tokenid);
        System.out.println(hash);
    }
```


###    根据地址查询资产数量

-   方法名 ：`balanceOf()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 资产合约地址|
| owner | String  | 拥有者地址|


-   返回值类型：`BigInteger`

-   返回说明： 

>   资产数量

-   示例代码

```
    /*
    * 拥有资产数量
    *
    * */
    @Test
    public void balanceOf() throws Exception {
        String assetAddress = "0xe8699073280c2f8bf6a47a2dd3c2ba4dcabd22ce";//资产合约地址
        String owner = "0x21f017BA0937426e8d68417b59658e2DC74c8936";
        BigInteger balanceOf = assetManagementService.balanceOf(assetAddress, owner);
        System.out.println(balanceOf);
    }
```



###    根据hash查询交易状态

-   方法名 ：`getTransferStatus()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | hash|

-   返回值类型：`Boolean`

-   返回说明：

>   true 交易成功；false 交易失败；空（null） 交易打包中

-   示例代码

```
    /*
   * 获取交易状态
   * */
    @Test
    public void getTransferStatus() throws Exception {
        String hash = "0x7cc931ff895229f902061d2aafcefbeea4fa1e6ba69c834ecd8006069375f8f7";//资产合约地址
        boolean falg = assetManagementService.getTransferStatus(hash);
        System.out.println(falg);
    }
```






