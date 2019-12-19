# Passport API


##  **介绍**

Passport API是对Passport模块进行的功能，Passport模块可完成对用户身份信息的管理。快速开发请阅读以下文档


## **Build**

```
 private String nodeurl = "http://54.64.220.165:21604";//亦来云测试节点地址
 private PassportServiceImpl passportService = new PassportServiceImpl(nodeurl);

```

##  **目录**


- [1. 创建did](#1-创建did)
- [2. 根据私钥导出did](#2-根据私钥导出did)
- [3. 根据助记词导出did](#3-根据助记词导出did)
- [4. 使用私钥签名信息](#4-使用私钥签名信息)
- [5. 验证签名](#5-验证签名)


----------



## **API**

### 1. 创建did

-   方法名 ：`create()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| mnemonicType | MnemonicType  | 助记词类型（目前支持中文、英文）|

-   返回值类型：`DIDAccount`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |侧链地址|
| did | String  |did地址|
| mnemonic | String  |助记词|


-   示例代码

```
    /*
    * 创建did
    * */
    @Test
    public void createDid() {
        DIDAccount didAccount = passportService.create(HdSupport.MnemonicType.ENGLISH);
        String didAddress = didAccount.getDid();//did地址
        String address = didAccount.getAddress();//侧链地址
        String mnemonic = didAccount.getMnemonic();//助记词
        String privateKey = didAccount.getPrivateKey();//私钥
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(didAddress);
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }

        /*    
        iUa4HdUPsXqexgKXzpDomJRdW831BDQ7RL
        ELw7jSZ5Mvriw65h3x9G5oezwzzMkanwUm
        deny correct hello ride junior raise clever phrase aspect inflict stone enter
        B6873904CB64F13395F37D238F7F6580308F30C9E9ECB7EB98454A565A573B44
        02E9B224CC68DFB7980B32755DA87140C6B9315D8D6C706A698D49CA6E7A5ABC40

        */
```


###   2. 根据私钥导出did

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
| address | String  |侧链地址|
| did | String  |did地址|

-   示例代码

```
    /*
    * 根据私钥导出钱包
    * */
    @Test
    public void exportByPrivateKey() {
        String privateKey = "B6873904CB64F13395F37D238F7F6580308F30C9E9ECB7EB98454A565A573B44";
        DIDAccount didAccount = passportService.exportByPrivateKey(privateKey);
        String did = didAccount.getDid();//did
        String address = didAccount.getAddress();//侧链地址
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(did);
        System.out.println(address);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


###   3. 根据助记词导出did

-   方法名 ：`exportByMnemonic()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----| :----  | :----  |
| mnemonic | String  | 助记词|


-   返回值类型：`DIDAccount`

-  返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----| :----  | :----  |
| privateKey | String  | 私钥|
| publicKey | String  |公钥|
| address | String  |侧链地址|
| did | String  |did地址|
| mnemonic | String  |助记词|

-   示例代码

```
    /*
    * 根据 助记词导出钱包
    * */
    @Test
    public void exportByMnemonic() {
        String mnemonic = "deny correct hello ride junior raise clever phrase aspect inflict stone enter";
        DIDAccount didAccount = passportService.exportByMnemonic(mnemonic);
        String did = didAccount.getDid();//did
        String address = didAccount.getAddress();//侧链地址
        String privateKey = didAccount.getPrivateKey();//私钥
        String publicKey = didAccount.getPublicKey();//公钥
        System.out.println(did);
        System.out.println(address);
        System.out.println(mnemonic);
        System.out.println(privateKey);
        System.out.println(publicKey);
    }
```


###   4. 使用私钥签名信息

-   方法名 ：`sign()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| msg | String  | 签名信息|


-   返回值类型：`SignDataEntity`

-   返回说明：

| 返回值 | 参数类型 | 返回值说明|
| :----:| :----:  | :----:  |
| msg | String  | 信息|
| pub | String  | 公钥|
| sig | String  | 已签名信息|

-   示例代码

```
    @Test
    public void sign() throws Exception {
        String privateKey = "4B1AA0C6F0BF55BDF3DB22122215FBAE5743B0D5BB199AF951AF6306E812704E";
        String msg="test msg";
        SignDataEntity signDataEntity = passportService.sign(msg,privateKey);
        System.out.println(JSON.toJSONString(signDataEntity));
       // {"msg":"74657374206D7367",
        // "pub":"026E57442BEC014401C0484CD844A05785083656B51A393DC7C1F1BA9269203278",
        // "sig":"86A0C2F4CCDA3BC753F15592FF50335CD2BDB72777F0A062433CBB7045C30920EE9DF2E2169832C14E310FF45E3D02CCC3E5E8F7D870F82FD750DC1ECFD35A60"}

    }
```



###   5. 验证签名

-   方法名 ：`verify()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| msg | String  | 验证信息|
| sig | String  | 签名信息|
| pub | String  | 公钥|


-   返回值类型：`Boolean`

-   返回说明： 

>   true 验证通过；false 验证不通过

-   示例代码

```
    @Test
    public void verify() throws Exception {
        String msg = "test msg";
        String sig = "86A0C2F4CCDA3BC753F15592FF50335CD2BDB72777F0A062433CBB7045C30920EE9DF2E2169832C14E310FF45E3D02CCC3E5E8F7D870F82FD750DC1ECFD35A60";
        String pub = "026E57442BEC014401C0484CD844A05785083656B51A393DC7C1F1BA9269203278";
        Boolean aBoolean = passportService.verify(msg, sig, pub);
        System.out.println(aBoolean);
    }
```









