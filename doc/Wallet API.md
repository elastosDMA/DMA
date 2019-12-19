# Wallet API


## **介绍**


Wallet API是对Wallet模块的封装，包含以太坊钱包功能封装、亦来云主链钱包封装、亦来云侧链（DID、ETH）钱包封装。使用Wallet API进行钱包开发，请阅读以下文档。


##  **Build**

```
//eth wallet

    private String nodeurl = "http://127.0.0.1:8545";//以太坊节点地址
    private EthWalletService ethWalletService = new EthWalletService(nodeurl);


    
//ela main wallet

    private String nodeurl = "http://54.64.220.165:21334";//亦来云主链测试节点地址
    private ElaWalletService elaWalletService = new ElaWalletService(nodeurl);
    
    
//ela did wallet

    private String nodeurl = "http://54.64.220.165:21604";//亦来云did侧链测试节点地址
    private ElaDIDSideWalletService elaDIDSideWalletService = new ElaDIDSideWalletService(nodeurl);
    
    
//ela eth wallet

    private String nodeurl = "http://52.205.30.16:8545";//亦来云eth侧链测试节点地址
    private ElaETHSideWalletService elaETHSideWalletService = new ElaETHSideWalletService(nodeurl);

```

##  **目录**


- [1.ETH Wallet (以太坊钱包)](#1-eth-wallet)
    - [1.1 创建钱包](#1-1-创建钱包)
    - [1.2 根据私钥导出钱包](#1-2-根据私钥导出钱包)
    - [1.3 根据助记词导出钱包](#1-3-根据助记词导出钱包)
    - [1.4 根据地址获取余额](#1-4-根据地址获取余额)
    - [1.5 转账](#1-5-转账)
    - [1.6 根据hash查询交易详情](#1-6-根据hash查询交易详情)
    - [1.7 地址校验](#1-7-地址校验)
    - [1.8 根据地址获取代币余额](#1-8-根据地址获取代币余额)
    - [1.9 erc20代币转账](#1-9-erc20代币转账)
    - [1.10 根据hash查询交易状态](#1-10-根据hash查询交易状态)
- [2.ELA Wallet (亦来云钱包)](#2-ela-wallet)
    - [2.1 创建钱包](#2-1-创建钱包)
    - [2.2 根据私钥导出钱包](#2-2-根据私钥导出钱包)
    - [2.3 根据助记词导出钱包](#2-3-根据助记词导出钱包)
    - [2.4 根据地址获取余额](#2-4-根据地址获取余额)
    - [2.5 转账](#2-5-转账)
    - [2.6 查询交易详情](#2-6-查询交易详情)
    - [2.7 地址校验](#2-7-地址校验)
    - [2.8 据txid查询交易状态](#2-8-根据txid查询交易状态)
    - [2.9 本地交易签名](#2-9-本地交易签名)
    - [2.10 解析交易签名](#2-10-解析交易签名)
    - [2.11 发送交易签名上链](#2-11-发送交易签名上链)
    - [2.12 主链向DID侧链充值](#2-12-主链向did侧链充值)
    - [2.13 主链向ETH侧链充值](#2-13-主链向eth侧链充值链)
- [3.DID Side Wallet (亦来云did侧链钱包)](#3-did-side-wallet)
    - [3.1 创建钱包](#3-1-创建钱包)
    - [3.2 根据私钥导出钱包](#3-2-根据私钥导出钱包)
    - [3.3 根据助记词导出钱包](#3-3-根据助记词导出钱包)
    - [3.4 根据地址获取余额](#3-4-根据地址获取余额)
    - [3.5 转账](#3-5-转账)
    - [3.6 查询交易详情](#3-6-查询交易详情)
    - [3.7 地址校验](#3-7-地址校验)
    - [3.8 据txid查询交易状态](#3-8-根据txid查询交易状态)
    - [3.9 DID侧链向主链提现](#3-9-did侧链向主链提现)
- [4.ETH Side Wallet (亦来云ETH侧链钱包)](#4-eth-side-wallet)
    - [4.1 创建钱包](#4-1-创建钱包)
    - [4.2 根据私钥导出钱包](#4-2-根据私钥导出钱包)
    - [4.3 根据助记词导出钱包](#4-3-根据助记词导出钱包)
    - [4.4 根据地址获取余额](#4-4-根据地址获取余额)
    - [4.5 转账](#4-5-转账)
    - [4.6 根据hash查询交易详情](#4-6-根据hash查询交易详情)
    - [4.7 地址校验](#4-7-地址校验)
    - [4.8 根据hash查询交易状态](#4-8-根据hash查询交易状态)
    - [4.9 ETH侧链向主链提现](#4-9-eth侧链向主链提现)    


----------




##  **API**

### 1. eth wallet

####   1. 1 创建钱包

-   方法名 ：`create()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| mnemonicType | MnemonicType  |助记词类型（目前支持中文、英文）|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|
| mnemonic | String  |助记词|

-   示例代码

```
    /*
    * 创建钱包
    * */
    @Test
    public void createTest() {
        EthAccount ethAccount =ethWalletService.create(HdSupport.MnemonicType.ENGLISH);
        String address = ethAccount.getAddress();//地址
        String mnemonic = ethAccount.getMnemonic();//助记词
        String privateKey = ethAccount.getPrivateKey();//私钥
        String publicKey = ethAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


####    1. 2 根据私钥导出钱包

-   方法名 ：`exportByPrivateKey()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| privateKey | String  | 私钥|


-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----: | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|

-   示例代码

```
    /*
     * 根据私钥导出钱包
     *
     */
    @Test
    public void exportByPrivateKey() throws ApiException {
        String privateKey = "d6ed30f07efa7ccd641186e752f827f9f4901c797d3b614e9f6aee56a031147f";
        EthAccount elaAccount = ethWalletService.exportByPrivateKey(privateKey);
        String address = elaAccount.getAddress();//地址
        String publicKey = elaAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####    1. 3 根据助记词导出钱包

-   方法名 ：`exportByMnemonic()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| mnemonic | String  | 助记词|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|


-   示例代码

```
   /**
     * 根据 助记词导出钱包
     */
    @Test
    public void exportByMnemonic() {
        String mnemonic = "hospital educate still slam december hidden video what member next raise junior";
        EthAccount ethAccount = ethWalletService.exportByMnemonic(mnemonic);
        String address = ethAccount.getAddress();//地址
        String privateKey = ethAccount.getPrivateKey();//私钥
        String publicKey = ethAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }

```


####    1. 4 根据地址获取余额

-   方法名 ：`balance()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`String`

-   返回说明：

>   余额

-   示例代码

```
    /**
     * 获取余额
     */
    @Test
    public void balance() throws IOException {
        String address = "0x6e55aaebaefe953931fcfc251079b874484e69ed";
        BigDecimal balance = ethWalletService.balance(address);
        System.out.println(balance);
    }

```


####    1. 5 转账

-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | String  | 转出金额|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|


-   返回值类型：`String`

-   返回说明：交易hash

-   示例代码

```
     /**
     * eth转账
     */
    @Test
    public void transfer() throws Exception {
        String privateKey = "8194cfe0650f004785b176f83a88af84ed73087a72609174605ef87054272811";
        String _to = "0x6e55aaebaefe953931fcfc251079b874484e69ed";
        BigInteger gasPrice = BigInteger.valueOf(10000000000L);
        BigInteger gasLimit = BigInteger.valueOf(60000);
        String hash = ethWalletService.transfer(privateKey, _to, BigDecimal.valueOf(1), gasPrice, gasLimit);
        System.out.println(hash);

    }
```



####    1. 6 根据hash查询交易详情

-   方法名 ：`getTransaction()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | 交易hash|


-   返回值类型：`TransactionInfo`

-   返回说明：

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| transactionHash | String  | 交易hash|
| transactionIndex | String  | 在一个区块中交易序号|
| blockHash | String  | 区块hash|
| blockNumber | String   | 区块好|
| status | String   | 交易状态(1 交易成功；0 交易失败；空(null) 等待打包确认)|
| from | String   | 发送方地址|
| to | String   | 接收方地址|
| value | String   | 交易金额(eth)|
| timestamp | BigInteger   | 交易时间戳|
| nonce | BigInteger   | 交易随机数|
| gasPrice | String   | gas价格|
| gasLimit | BigInteger   | gas限制|
| gasUsed | String   | 实际使用gas限制|
| logs | List<Log>   | 交易日志|


-   示例代码

```
/**
     * 获取交易信息
     */
    @Test
    public void transactionInfo() throws IOException {
        String hash = "0x548fc720a4c12a22ce55b434ae44d18a685a0d8381dcafd72b95291d87026b9a";
        TransactionInfo transactionInfo = ethWalletService.getTransaction(hash);
        System.out.println(JSON.toJSONString(transactionInfo));
        
        //{
        //	"blockHash": "0xd889806afb3ef11b633cd9e43e441063d771a4fe39bff71e63a43fa4f4dcfa29",
        //	"blockNumber": "59",
        //	"from": "0x872c74d84c3a6df6814409219ad68f155df01706",
        //	"gasLimit": 60000,
        //	"gasPrice": "1E-8",
        //	"gasUsed": "21000",
        //	"logs": [],
        //	"nonce": 4,
        //	"status": "1",
        //	"timestamp": 1571305073,
        //	"to": "0x6e55aaebaefe953931fcfc251079b874484e69ed",
        //	"transactionHash": "0x548fc720a4c12a22ce55b434ae44d18a685a0d8381dcafd72b95291d87026b9a",
        //	"transactionIndex": "0",
        //	"value": "1"
        //}
    }
```



####    1. 7 地址校验

-   方法名 ：`checkAddr()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`Boolean`

-   返回说明：

| 参数类型 | 参数说明|
| :----:  | :----:  |
| Boolean  | true 有效地址；false 无效地址|


-   示例代码

```
    /**
     * 检查地址是否正确
     */
    @Test
    public void checkAddr() {
        String address = "0x6e55aaebaefe953931fcfc251079b874484e69ed";
        boolean checkAddr = ethWalletService.checkAddr(address);
        System.out.println(checkAddr);
    }
```

####    1. 8 根据地址获取代币余额

-   方法名 ：`tokenBalance()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| address | String  | 地址|


-   返回值类型：`String`

-   返回说明：

>   余额

-   示例代码

```
    /**
     * 获取代币余额
     */
    @Test
    public void tokenBalance() throws Exception {
        String owner = "0xA258f950203b46A4036CE4c71BC64CE1d010EaaC";//地址
        String contractAddress = "0xd08f65e3895750201c620b1951079e4ee12a251a";//代币地址
        String tokenBalance = ethWalletService.tokenBalance(owner, contractAddress);
        System.out.println(tokenBalance);
    }
```



####    1. 9 erc20代币转账

-   方法名 ：`tokenTransfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | String  | 转出金额|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|


-   返回值类型：`String`

-   返回说明：

>   交易hash

-   示例代码

```
    /**
     * eth转账
     */
    @Test
    public void tokenTransfer() throws Exception {
        String contractAddress = "0xd08f65e3895750201c620b1951079e4ee12a251a";//代币地址
        String privateKey="f4b7957d7f11b014a77ad80e5d03d1c732f51c08ec7925c3d6175e19d099d832";
        String _to="0x21f017BA0937426e8d68417b59658e2DC74c8936";
        String _value="10";
        BigInteger gasPrice=BigInteger.valueOf(1000000000);
        BigInteger gasLimit=BigInteger.valueOf(60000);
        String hash = ethWalletService.tokenTransfer(contractAddress,privateKey, _to,_value,gasPrice,gasLimit);
        System.out.println(hash);

    }
```


####  1. 10 根据hash查询交易状态

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
    public void getTransferStatus() throws IOException {
        String txid = "0xb4628a779ce00cb5dd0b321325554802f701600516fed8c292511c831151f06a";
        Boolean transferStatus = ethWalletService.getTransferStatus(txid);
        System.out.println(transferStatus);
    }
```


### 2. ela wallet


####   2. 1 创建钱包

-   方法名 ：`create()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| mnemonicType | MnemonicType  |助记词类型（目前支持中文、英文）|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`ElaAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|
| mnemonic | String  |助记词|

-   示例代码

```
    /*
    * 创建钱包
    * */
    @Test
    public void create() {
        ElaAccount elaAccount = elaWalletService.create();
        String address = elaAccount.getAddress();//地址
        String mnemonic = elaAccount.getMnemonic();//助记词
        String privateKey = elaAccount.getPrivateKey();//私钥
        String publicKey = elaAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####   2. 2 根据私钥导出钱包

-   方法名 ：`exportByPrivateKey()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|


-   返回值类型：`ElaAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|

-   示例代码

```
    /*
    * 根据私钥导出钱包
    * */
    @Test
    public void exportByPrivateKey() {
        String privateKey = "4CDA5C9D041CD0281E5724A106B84977071A454FD56EA1294985DE76210073EA";
        ElaAccount elaAccount = elaWalletService.exportByPrivateKey(privateKey);
        String address = elaAccount.getAddress();//地址
        String publicKey = elaAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####    2. 3 根据助记词导出钱包

-   方法名 ：`exportByMnemonic()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| mnemonic | String  | 助记词|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`ElaAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |亦来云钱包地址|

-   示例代码

```
    /*
    * 根据 助记词导出钱包
    * */
    @Test
    public void exportByMnemonic() {
        String mnemonic = "satoshi patient awake crush great behave glide melody neither can version bargain";
        ElaAccount elaAccount = elaWalletService.exportByMnemonic(mnemonic);
        String address = elaAccount.getAddress();//地址
        String privateKey = elaAccount.getPrivateKey();//私钥
        String publicKey = elaAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


####    2. 4 根据地址获取余额

-   方法名 ：`balance()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`String`

-   返回说明：余额

-   示例代码

```
    /*
     * 获取余额
    * */
    @Test
    public void balance() {
        String address = "EaYijL4HLkqMHbUNQCbArgmZjsNNPMAaXk";
        String balance = elaWalletService.balance(address);
        System.out.println(balance);
    }

```


####    2. 5 转账

-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | String  | 转出金额|
| memo | String  | 备注|


-   返回值类型：`String`

-   返回说明： 交易txid



-   示例代码

```
    /**
     * 转账
     */
    @Test
    public void transfer() throws Exception {
        String privateKey = "4CDA5C9D041CD0281E5724A106B84977071A454FD56EA1294985DE76210073EA";
        String to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        String value = "0.1";
        String txid = elaWalletService.transfer(privateKey, to, value);
        System.out.println(txid);
    }
```


####    2. 6 查询交易详情

-   方法名 ：`transactionInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| txid | String  | 交易txid|


-   返回值类型：`Map`

-   返回说明:交易信息


-   示例代码

```
     /*
    * 获取交易信息
    * */
    @Test
    public void transactionInfo() {
   
        Map<String, Object> map = elaWalletService.transactionInfo("b10fe88db3f23565efc93fa7a6549d1a5618855caecee549715fadab087c99b3");
       
    }
```


####    2. 7 地址校验

-   方法名 ：`checkAddr()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`Boolean`

-   返回说明：

| 参数类型 | 参数说明|
| :----:| :----:  |
| Boolean  | true 有效地址；false 无效地址|
 
 
 -   示例代码
 
```
    /*
    * 检查地址是否正确
    * */
    @Test
    public void checkAddr() {
        String address = "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC";
        boolean checkAddr = elaWalletService.checkAddr(address);
        System.out.println(checkAddr);
    }
```


####   2. 8 根据txid查询交易状态

-   方法名 ：`getTransferStatus()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| txid | String  | txid|


-   返回值类型：`Boolean`

-   返回说明：

>   true 交易成功；false 交易失败；空（null） 交易打包中

 -   示例代码

```
    /*
    * 获取交易状态
    * */
    @Test
    public void getTransferStatus() {
        String txid = "493cca9ff816afec74d9ab7e119c013f2536b6fa0ca63d5b47a914583ca3b860";
        Boolean transferStatus = elaWalletService.getTransferStatus(txid);
        System.out.println(transferStatus);
    }
```


####    2. 9 本地交易签名

-   方法名 ：`getRawTx()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | Double  | 转出金额|
| memo | String  | 备注|


-   返回值类型：`String`

-   返回说明：

>   交易签名code

-   示例代码

```
 /**
     * 签名交易
     */
    @Test
    public void getRawTx() throws Exception {
        String privateKey = "4CDA5C9D041CD0281E5724A106B84977071A454FD56EA1294985DE76210073EA";
        String to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        String value = "0.1";
        String txCode = elaWalletService.getRawTx(privateKey, to, new BigDecimal(value));
        System.out.println(txCode);
    }
```


####    2. 10 解析交易签名

-   方法名 ：`decodeRawTx()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| rawTransaction | String  | 交易签名|


-   返回值类型：`Map`



-   示例代码

```
 /**
     * 解析交易签名
     */
    @Test
    public void decodeRawTx() throws Exception {
      String txCode="020001001337303131303438383338323035323538353537012F08CBCC8616F251F04621A481F24DC5287EEFA1A916A2E8FDEC5365B132A84201000000000002B037DB964A231458D2D6FFD5EA18944C4F90E63D547C5D3B9874DF66A4EAD0A380969800000000000000000021383C336427B1FA251CC48B5A9C1069226E44B3DDB037DB964A231458D2D6FFD5EA18944C4F90E63D547C5D3B9874DF66A4EAD0A3602DC304000000000000000021829A879DD9936EAF5A892514F9279AD0DB3F98B3000000000141402A351EE9120B2D3BFEEF2F1B1AA0F53D75F5D8041BFAA3FC5309461561C0180BA8AD2942AC4AC5517CD93E5CABD95AA2A1D029CEA688168EA9CBA514C8F3419C2321038BA51F7221E0660CE83EBDCC6A9BC1581C36B895F367DB34AB66CBE56DC6D61BAC";
        Map result = elaWalletService.decodeRawTx(txCode);
        System.out.println(result);
    }
```


####    2. 11 发送交易签名上链

-   方法名 ：`sendTx()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| txCode | String  | 交易签名|


-   返回值类型：`String`

-   返回说明：交易txid



-   示例代码

```
    /**
     * 发送交易签名上链
     */
    @Test
    public void sendTx() throws Exception {
        String txCode="020001001337303131303438383338323035323538353537012F08CBCC8616F251F04621A481F24DC5287EEFA1A916A2E8FDEC5365B132A84201000000000002B037DB964A231458D2D6FFD5EA18944C4F90E63D547C5D3B9874DF66A4EAD0A380969800000000000000000021383C336427B1FA251CC48B5A9C1069226E44B3DDB037DB964A231458D2D6FFD5EA18944C4F90E63D547C5D3B9874DF66A4EAD0A3602DC304000000000000000021829A879DD9936EAF5A892514F9279AD0DB3F98B3000000000141402A351EE9120B2D3BFEEF2F1B1AA0F53D75F5D8041BFAA3FC5309461561C0180BA8AD2942AC4AC5517CD93E5CABD95AA2A1D029CEA688168EA9CBA514C8F3419C2321038BA51F7221E0660CE83EBDCC6A9BC1581C36B895F367DB34AB66CBE56DC6D61BAC";
        String result = elaWalletService.sendTx(txCode);
        System.out.println(result);
    }
```


####    2. 12 主链向did侧链充值

-   方法名 ：`crossTransferToDID()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 主链私钥|
| _to | String  | did侧链钱包地址|
| _value | Double  | 充值金额|

-   返回值类型：`String`

-   返回说明：交易txid



-   示例代码

```
    //主链向did侧链转账
    @Test
    public void crossTransferToDID() throws Exception {
        String privateKey = "b14f0ad5a014ee82080ed9234ee6cae3440ae4fe93903dcd836b53d71d82ab4e";
        String _to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        Double _value = 4.0;
        String str = elaWalletService.crossTransferToDID(privateKey, _to, _value);
        System.out.println(str);
    }

```


####    2. 13 主链向eth侧链充值

-   方法名 ：`crossTransferToETH()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 主链私钥|
| _to | String  | eth侧链钱包地址|
| _value | Double  | 充值金额|

-   返回值类型：`String`

-   返回说明：交易txid



-   示例代码

```
    //主链向eth侧链转账
    @Test
    public void crossTransferToETH() throws Exception {
        String privateKey = "b14f0ad5a014ee82080ed9234ee6cae3440ae4fe93903dcd836b53d71d82ab4e";
        String _to = "0x0b23eff3a9d8f02829d3b0714cf2e00f5fae2b47";
        Double _value = 4.0;
        String str = elaWalletService.crossTransferToETH(privateKey, _to, _value);
        System.out.println(str);
    }

```


### 3. did side wallet


####   3. 1 创建钱包

-   方法名 ：`create()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| mnemonicType | MnemonicType  |助记词类型（目前支持中文、英文）|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`DIDAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|
| mnemonic | String  |助记词|

-   示例代码

```
    /*
    * 创建钱包
    * */
    @Test
    public void create() {
        DIDAccount didAccount = elaDIDSideWalletService.create();
        String address = didAccount.getAddress();//地址
        String mnemonic = didAccount.getMnemonic();//助记词
        String privateKey = didAccount.getPrivateKey();//私钥
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####   3. 2 根据私钥导出钱包

-   方法名 ：`exportByPrivateKey()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|


-   返回值类型：`DIDAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|

-   示例代码

```
    /*
    * 根据私钥导出钱包
    * */
    @Test
    public void exportByPrivateKey() {
        String privateKey = "4CDA5C9D041CD0281E5724A106B84977071A454FD56EA1294985DE76210073EA";
        DIDAccount didAccount = elaDIDSideWalletService.exportByPrivateKey(privateKey);
        String address = didAccount.getAddress();//地址
        String privateKey = didAccount.getPrivateKey();//私钥
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####    3. 3 根据助记词导出钱包

-   方法名 ：`exportByMnemonic()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| mnemonic | String  | 助记词|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`DIDAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |亦来云钱包地址|

-   示例代码

```
    /*
    * 根据 助记词导出钱包
    * */
    @Test
    public void exportByMnemonic() {
        String mnemonic = "satoshi patient awake crush great behave glide melody neither can version bargain";
        DIDAccount didAccount = elaDIDSideWalletService.exportByMnemonic(mnemonic);
        String address = didAccount.getAddress();//地址
        String privateKey = didAccount.getPrivateKey();//私钥
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


####    3. 4 根据地址获取余额

-   方法名 ：`balance()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`String`

-   返回说明：余额

-   示例代码

```
    /*
     * 获取余额
    * */
    @Test
    public void balance() {
        String address = "EaYijL4HLkqMHbUNQCbArgmZjsNNPMAaXk";
        String balance = elaDIDSideWalletService.balance(address);
        System.out.println(balance);
    }

```


####    3. 5 转账

-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | String  | 转出金额|
| memo | String  | 备注|


-   返回值类型：`String`

-   返回说明： 交易txid



-   示例代码

```
    /**
     * 转账
     */
    @Test
    public void transfer() throws Exception {
        String privateKey = "4CDA5C9D041CD0281E5724A106B84977071A454FD56EA1294985DE76210073EA";
        String to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        String value = "0.1";
        String txid = elaDIDSideWalletService.transfer(privateKey, to, value);
        System.out.println(txid);
    }
```


####    3. 6 查询交易详情

-   方法名 ：`transactionInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| txid | String  | 交易txid|


-   返回值类型：`Map`

-   返回说明:交易信息


-   示例代码

```
     /*
    * 获取交易信息
    * */
    @Test
    public void transactionInfo() {
   
        Map<String, Object> map = elaDIDSideWalletService.transactionInfo("b10fe88db3f23565efc93fa7a6549d1a5618855caecee549715fadab087c99b3");
       
    }
```


####    3. 7 地址校验

-   方法名 ：`checkAddr()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`Boolean`

-   返回说明：

| 参数类型 | 参数说明|
| :----:| :----:  |
| Boolean  | true 有效地址；false 无效地址|
 
 
 -   示例代码
 
```
    /*
    * 检查地址是否正确
    * */
    @Test
    public void checkAddr() {
        String address = "EV4UTSLGpFMM8Y5jjZp4TLVc9QaNFHGosC";
        boolean checkAddr = elaDIDSideWalletService.checkAddr(address);
        System.out.println(checkAddr);
    }
```


####   3. 8 根据txid查询交易状态

-   方法名 ：`getTransferStatus()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| txid | String  | txid|


-   返回值类型：`Boolean`

-   返回说明：

>   true 交易成功；false 交易失败；空（null） 交易打包中

 -   示例代码

```
    /*
    * 获取交易状态
    * */
    @Test
    public void getTransferStatus() {
        String txid = "493cca9ff816afec74d9ab7e119c013f2536b6fa0ca63d5b47a914583ca3b860";
        Boolean transferStatus = elaDIDSideWalletService.getTransferStatus(txid);
        System.out.println(transferStatus);
    }
```


####    3. 9 did侧链向主链提现

-   方法名 ：`crossTransfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | did侧链私钥|
| _to | String  | 主链钱包地址|
| _value | Double  | 提现金额|

-   返回值类型：`String`

-   返回说明：交易txid



-   示例代码

```
    //did侧链向主链提现
    @Test
    public void crossTransfer() throws Exception {
        String privateKey = "b14f0ad5a014ee82080ed9234ee6cae3440ae4fe93903dcd836b53d71d82ab4e";
        String _to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        Double _value = 4.0;
        String str = elaDIDSideWalletService.crossTransfer(privateKey, _to, _value);
        System.out.println(str);
    }

```

### 4. eth side wallet

####   4. 1 创建钱包

-   方法名 ：`create()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| mnemonicType | MnemonicType  |助记词类型（目前支持中文、英文）|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|
| mnemonic | String  |助记词|

-   示例代码

```
    /*
    * 创建钱包
    * */
    @Test
    public void createTest() {
        EthAccount ethAccount =elaETHSideWalletService.create(HdSupport.MnemonicType.ENGLISH);
        String address = ethAccount.getAddress();//地址
        String mnemonic = ethAccount.getMnemonic();//助记词
        String privateKey = ethAccount.getPrivateKey();//私钥
        String publicKey = ethAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


####    4. 2 根据私钥导出钱包

-   方法名 ：`exportByPrivateKey()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:| :----:|
| privateKey | String  | 私钥|


-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----: | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|

-   示例代码

```
    /*
    * 根据私钥导出钱包
    * */
    @Test
    public void exportByPrivateKey() {
        String privateKey = "d6ed30f07efa7ccd641186e752f827f9f4901c797d3b614e9f6aee56a031147f";
        EthAccount elaAccount = elaETHSideWalletService.exportByPrivateKey(privateKey);
        String address = elaAccount.getAddress();//地址
        String publicKey = elaAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```



####    4. 3 根据助记词导出钱包

-   方法名 ：`exportByMnemonic()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| mnemonic | String  | 助记词|
| pwd | String  | 助记词密码（选填）|

-   返回值类型：`EthAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |钱包地址|


-   示例代码

```
    /*
    * 根据 助记词导出钱包
    * */
    @Test
    public void exportByMnemonic() {
        String mnemonic = "hospital educate still slam december hidden video what member next raise junior";
        EthAccount ethAccount = elaETHSideWalletService.exportByMnemonic(mnemonic);
        String address = ethAccount.getAddress();//地址
        String privateKey = ethAccount.getPrivateKey();//私钥
        String publicKey = ethAccount.getPublicKey();//公钥
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


####    4. 4 根据地址获取余额

-   方法名 ：`balance()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`String`

-   返回说明：

>   余额

-   示例代码

```
    /*
    * 获取余额
    * */
    @Test
    public void balance() throws IOException {
        String address = "0x6e55aaebaefe953931fcfc251079b874484e69ed";
        String balance = elaETHSideWalletService.balance(address);
        System.out.println(balance);
    }

```


####    4. 5 转账

-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privatekey | String  | 私钥|
| to | String  | 接收者地址|
| value | String  | 转出金额|
| gasPrice | BigInteger   | gas价格|
| gasLimit | BigInteger   | gas限制|


-   返回值类型：`String`

-   返回说明：交易hash

-   示例代码

```
    /**
     * eth转账
     */
    @Test
    public void transfer() throws Exception {
        String privateKey="8194cfe0650f004785b176f83a88af84ed73087a72609174605ef87054272811";
        String _to="0x6e55aaebaefe953931fcfc251079b874484e69ed";
        String _value="100";

        String hash = elaETHSideWalletService.transfer(privateKey, _to,_value,gasPrice,gasLimit);
        System.out.println(hash);

    }
```



####    4. 6 根据hash查询交易详情

-   方法名 ：`transactionInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | 交易hash|


-   返回值类型：`TransactionInfo`

-   返回说明：

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| transactionHash | String  | 交易hash|
| transactionIndex | String  | 在一个区块中交易序号|
| blockHash | String  | 区块hash|
| blockNumber | String   | 区块好|
| status | String   | 交易状态(1 交易成功；0 交易失败；空(null) 等待打包确认)|
| from | String   | 发送方地址|
| to | String   | 接收方地址|
| value | String   | 交易金额(eth)|
| timestamp | BigInteger   | 交易时间戳|
| nonce | BigInteger   | 交易随机数|
| gasPrice | String   | gas价格|
| gasLimit | BigInteger   | gas限制|
| gasUsed | String   | 实际使用gas限制|
| logs | List<Log>   | 交易日志|


-   示例代码

```
    /*
    * 获取交易信息
    * */
    @Test
    public void transactionInfo() throws IOException {
        String hash = "0xb4628a779ce00cb5dd0b321325554802f701600516fed8c292511c831151f06a";
        TransactionInfo transactionInfo = elaETHSideWalletService.transactionInfo(hash);
        System.out.println(JSON.toJSONString(transactionInfo));
    }
```



####    4. 7 地址校验

-   方法名 ：`checkAddr()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| address | String  | 地址|


-   返回值类型：`Boolean`

-   返回说明：

| 参数类型 | 参数说明|
| :----:  | :----:  |
| Boolean  | true 有效地址；false 无效地址|


-   示例代码

```
    /*
   * 检查地址是否正确
   * */
    @Test
    public void checkAddr() {
        String address = "0x6e55aaebaefe953931fcfc251079b874484e69ed";
        boolean checkAddr = elaETHSideWalletService.checkAddr(address);
        System.out.println(checkAddr);
    }
```



####  4. 8 根据hash查询交易状态

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
    public void getTransferStatus() throws IOException {
        String txid = "0xb4628a779ce00cb5dd0b321325554802f701600516fed8c292511c831151f06a";
        Boolean transferStatus = elaETHSideWalletService.getTransferStatus(txid);
        System.out.println(transferStatus);
    }
```

####    4. 9 eth侧链向主链提现

-   方法名 ：`crossTransfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | eth侧链私钥|
| _to | String  | 主链钱包地址|
| _value | BigDecimal  | 提现金额|
| gasPrice | BigInteger  | 提现金额|
| gasLimit | BigInteger  | 提现金额|

-   返回值类型：`String`

-   返回说明：交易hash



-   示例代码

```
    //did侧链向主链提现
    @Test
    public void crossTransfer() {
      
        String privateKey = "b14f0ad5a014ee82080ed9234ee6cae3440ae4fe93903dcd836b53d71d82ab4e";
        String _to = "ENHFT9Xuo3Z1bJn5d2pLfpndwVez7sVG5H";
        BigDecimal _value = BigDecimal.valueOf(10);
        String hash = elaETHSideWalletService.crossTransfer(privateKey, _to, _value, gasPrice, gasLimit);
        System.out.println(hash);
    }
```
