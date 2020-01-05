[toc]

## 一、产品简介

###  1、 产品概述

DMA开放平台基于亦来云基础服务支持，将支付，智能合约，数据存储，数据营销通过接口的形式开放给第三方合作伙伴，帮助第三方合作伙伴快速创建具有区块链特性的应用。

###  2、 产品优势

 通过接入DMA平台，开发人员无需详细了解区块链的工作原理，就能基于亦来云主链、DID侧链、ETH侧链开发去中心化应用。
 
###  3、 功能特性
 通用型移动APP钱包，现支持ELA 主链钱包、DID侧链钱包、ETH侧链钱包
  
 去中心化存储
    
 合约模板丰富，包含ERC20合约模板、ERC721合约模板，ERC721模板中有 收费类模板，质押类模板、N元购模板、票券销售类模板等
    
###  4、 应用场景
 
#### 4.1 区块链钱包

拥有一个区块链数字货币钱包，便象征着迈进区块链领域的大门。区块链去中心化特点可省去第三方中介环节，实现点对点的对接，在大大降低成本的同时，快速完成交易支付。

Elastos DMA 提供完善的Wallet（钱包）API服务。是对Wallet模块的封装，包含以太坊钱包功能封装、亦来云钱包封装。包含各类钱包创建，导出，查询余额，转账交易等。

#### 4.2 发布纪念币

使用ERC721合约发布的资产具有不可置换性，你可以赋予每个token独一无二的属性，开发者们可以开发一个纪念币相关的dApp。将值得纪念事情记录下来，发布你的专属纪念币。

####  4.3 票务应用

ElastosDMA团队自主开发了ElastosDMA平台上的第一家去中心化电子商务体验商店——uptick。是一个由可信商家参与的，为设计师提供分账的，去中心化的电子商务dAPP，并将售卖商品的范围限定在精致的、有版权设计的一手文创类产品。

####  4.4 收费类活动应用

收费类活动主要用于小型活动，活动类型为收费类活动，交易过程中用户支付的报名费用暂时存在托管合约作为质押，当会议举行时，现场经过举办方验票之后，费用才能进入举办方账户。

####  4.5 质押类活动应用

质押活动，用户支付的费用暂时存在托管合约，当用户验票之后，用户报名活动的费用会退还到用户钱包，如果用户在活动结束前一直没有验票，此部分的报名费通过合约设置可归举办方所有或守约人均分。

###  5、基础术语



名词 | 说明
---|---
智能合约	Smart Contract|	一种旨在以信息化方式传播、验证或执行合同的计算机协议。一个智能合约是一套以数字形式定义的承诺（promises），包括合约参与方可以在上面执行这些承诺的协议。智能合约允许在没有第三方的情况下进行可信交易，这些交易可追踪且不可逆转。
私钥	Private key	|私钥是一组64位的16进制字符，通过私钥我们能够访问一个账户。用户需要保存好自己的私钥。
GasLimit|	该交易的执行时使用gas的上限
GasPrice|	交易发送者愿意支付的gas费用的价格。一个单位的gas表示了执行一个基本指令，例如一个计算步骤。
地址	address	|钱包账户地址
助记词	Mnemonic |	助记词由12-24个单词组成，助记词可以生成私钥。一个助记词可以生成无穷个私钥，可以理解成助记词是个树的根，这个根上可以长很多分支，每个叶子是一个私钥，Cobo钱包不同币种用的是不同的分支。这也是为何一个助记词可以管理HD账户下所有的钱包地址。
随机数	nonce|	用于维护以太坊交易的随机数
交易	Transaction |	区块链上的一个事务请求，用来承载具体业务操作数据的结构。区块链上所有针对世界状态的变化操作均是基于交易来完成的。
交易哈希	Transaction hash|	交易上链成功后，产生的唯一哈希值。
交易回执	Transaction receipt|	是交易的执行结果。区块链是异步的系统，交易执行后需要共识，与传统架构不同，不能直接返回交易执行是否成功，因此需在回执中查看最终交易结果。
节点信息	Node information|	区块链节点的相关信息。一个区块链一般由多节点组成。
区块	Block|	区块链上存储打包交易数据以及交易执行结果数据的一种组织形式。区块彼此之间通过前向的应用彼此链接形成区块链。 每个区块记录着上一个区块的哈希值、本区块中的交易集合、本区块的哈希等基础数据。
区块高度	Block height|	区块高度，简称块高，用来识别区块在区块链中的位置，并据此找到和这个区块相关的所有基础属性和交易记录。
区块链技术	Blockchain|	也被称之为分布式账本技术，是一种去中心化的分布式数据库技术，其特点是去中心化、公开透明、不可篡改、可信任。区块链的每笔数据，都会广播全网的区块链节点，每个节点都有全量的、一致的数据。
去中心化应用	Decentralized applications（DApp）|	与传统中心化应用的主要区别是，DApp 通过客户端直接连接区块链节点，通过智能合约计算和访问数据，没有中心化的后端服务。
燃料	Gas|	智能合约在虚拟机中执行计算和存储的消耗度量，通过燃料可防止一些恶意攻击和计算、存储的浪费。


## 二、发布说明

2018.12.31 DMA 测试版

2019.6.30 DMA1.0 稳定版 
更新了钱包SDK，Carrier离线消息

2019.10.30 DMA1.1 去中心化版
将DMA的BASE、Service 根据功能模块进行拆分成
 dma-assetManagement
 dma-config
 dma-merchant
 dma-message
 dma-passport
 dma-node-sdk
 dma-payment
 dma-storage
 dma-ticket
 dma-utility
 dma-wallet
更新了智能合约，在销售合约中增加授权、转移等事件
增加DMA Node服务，对合约执行过程中的数据进行整理，为应用提供服务


## 三、用户指南

###  1、JAVA SDK 开发指南

 ####   1.1 SDK说明
 
 平台JAVA SDK 是通过服务（Service）的形式对外提供功能，具体包括资产管理服务（AssetManagement ）个人数据服务（Passport）存储服务（Storage）钱包服务（ Wallet）商户服务 （ Merchant），消息服务（ Message），工具类（ Utility） 。

#####   运行环境说明

-   JDK 8 及以上版本在终端运行 java -version 查看当前 Java 版本。
-   Maven 3.5.4 及以上版本在终端运行 mvn -v 查看当前 Maven 版本。




 #### 1.2 快速开始
 
 
 
步骤一：在Maven文件中引入SDK包

-   根据需要安装下载的 jar 包到本地仓库。
-   从命令终端进入到下载的文件根目录，执行以下命令：

```
//安装 SDK 到本地仓库
mvn install:install-file -Dfile=dma-assetManagement-1.1.0.jar -DgroupId=org.elastos -DartifactId=dma-assetManagement -Dversion=1.1.0 -Dpackaging=jar

mvn install:install-file -Dfile=dma-wallet-1.1.0.jar -DgroupId=org.elastos -DartifactId=dma-wallet -Dversion=1.1.0 -Dpackaging=jar

mvn install:install-file -Dfile=dma-utility-1.1.0.jar -DgroupId=org.elastos -DartifactId=dma-utility -Dversion=1.1.0 -Dpackaging=jar

```

步骤二：使用 Intellij IDEA 创建一个基于 Maven 构建的空项目（Demo）。

步骤三：导入依赖

```

<repositories>
        <repository>
            <id>jitpack.io</id>
            <url>https://jitpack.io</url>
        </repository>
    </repositories>

    <dependencies>

        <dependency>
            <groupId>org.elastos</groupId>
            <artifactId>dma-base</artifactId>
            <version>1.1.0</version>
        </dependency>
        <dependency>
            <groupId>org.elastos</groupId>
            <artifactId>dma-service</artifactId>
            <version>1.1.0</version>
        </dependency>

        <dependency>
            <groupId>org.elastos</groupId>
            <artifactId>dma-utility</artifactId>
            <version>1.1.0</version>
        </dependency>

        <dependency>
            <groupId>com.github.ipfs</groupId>
            <artifactId>java-ipfs-api</artifactId>
            <version>v1.2.2</version>
        </dependency>
        <dependency>
            <groupId>org.elastos</groupId>
            <artifactId>wallet.lib</artifactId>
            <version>0.0.9</version>
        </dependency>
    </dependencies>



```
 
 
 

#### 1.3 接口调用说明

#####  AssetManagement模块

`AssetManagement`模块基于ETH侧链，资产分为ERC20类型资产和ERC721类型资产

-   ERC20资产管理类构建

```
    @Test
    public void ERC20Test() {
        String nodeUrl = "http://127.0.0.1:8545";//节点地址
        Token20 token20 = new Token20Service(nodeUrl);
    }


```

-   ERC721资产管理类构建

```
    @Test
    public void ERC721Test() {
        String nodeUrl = "http://127.0.0.1:8545";//节点地址
        Token721 token721 = new Token721Service(nodeUrl);
    }

```

#####   Merchant模块

`Merchant`模块中有三种不同类型的实现。`MerchantService`接口实现ERC721资产以售卖形式进行资产的流通；`ChargeActivityService`接口以收费活动形式进行资产的流通;`PledgeActivityService`接口以质押活动形式进行资产的流通。

-   MerchantService


```

    @Test
    public void merchant() throws TokenException, RpcException {
        String nodeUrl = "http://127.0.0.1:8545";//ETH链节点地址
        String chainType = "";//链类型（自定义）
        //创建MerchantService
        MerchantService merchantService = new MerchantServiceImpl(chainType, nodeUrl);

        String privateKey = "";//用户私钥
        BigInteger gasPrice = BigInteger.valueOf(1000000000);//gas费用
        BigInteger gasLimit = BigInteger.valueOf(7000000);//gas限制
        String name = ""; //ERC721资产名称
        String symbol = ""; //ERC721资产标识
        String metadata = "";//ERC721资产信息（自定义）
        //创建合约
        JsonResult<DeployResult> jsonResult = merchantService.deploy(privateKey, gasPrice, gasLimit, name, symbol, metadata);

        System.out.println(jsonResult.getData().getAssetAddress());//资产合约地址
        System.out.println(jsonResult.getData().getTrustAddress());//资产托管合约地址
        
    }

```

-   ChargeActivityService

```
    @Test
    public void chargeActivityService() throws TokenException, RpcException {
        String nodeUrl = "http://127.0.0.1:8545";//ETH链节点地址
        String chainType = "";//链类型（自定义）
        //ChargeActivityService
        ChargeActivityService chargeActivityService = new ChargeActivityServiceImpl(chainType, nodeUrl);

        String privateKey = "";//用户私钥
        BigInteger gasPrice = BigInteger.valueOf(1000000000);//gas费用
        BigInteger gasLimit = BigInteger.valueOf(7000000);//gas限制
        String name = ""; //ERC721资产名称
        String symbol = ""; //ERC721资产标识
        String metadata = "";//ERC721资产信息（自定义）
        Long endTime = 1568876617L;//活动结束时间
        //创建合约
        JsonResult<DeployResult> jsonResult = chargeActivityService.deploy(privateKey, gasPrice, gasLimit, name, symbol, metadata, endTime);

        System.out.println(jsonResult.getData().getAssetAddress());//资产合约地址
        System.out.println(jsonResult.getData().getTrustAddress());//资产托管合约地址

    }

```

-   PledgeActivityService

```
    @Test
    public void pledgeActivityService() throws TokenException, RpcException {
        String nodeUrl = "http://127.0.0.1:8545";//ETH链节点地址
        String chainType = "";//链类型（自定义）
        //PledgeActivityService
        PledgeActivityService pledgeActivityService = new PledgeActivityServiceImpl(chainType, nodeUrl);

        String privateKey = "";//用户私钥
        BigInteger gasPrice = BigInteger.valueOf(1000000000);//gas费用
        BigInteger gasLimit = BigInteger.valueOf(7000000);//gas限制
        String name = ""; //ERC721资产名称
        String symbol = ""; //ERC721资产标识
        String metadata = "";//ERC721资产信息（自定义）
        Long endTime = 1568876617L;//活动结束时间
        //创建合约
        JsonResult<DeployResult> jsonResult = pledgeActivityService.deploy(privateKey, gasPrice, gasLimit, name, symbol, metadata, endTime);

        System.out.println(jsonResult.getData().getAssetAddress());//资产合约地址
        System.out.println(jsonResult.getData().getTrustAddress());//资产托管合约地址

    }

```

#####   Passport模块

Passport模块基于亦来云DID侧链

```
    @Test
    public void passportService() {
        String didNodeUrl = "http://127.0.0.1:20336";//did侧链节点地址
        PassportService passportService = new PassportServiceImpl(didNodeUrl, "");
        DIDAccount didAccount = passportService.create(HdSupport.MnemonicType.ENGLISH);
        System.out.println(didAccount.getPrivateKey());//私钥
        System.out.println(didAccount.getMnemonic());//助记词
        System.out.println(didAccount.getAddress());//did钱包地址
        System.out.println(didAccount.getDid());//did
    }


```


#####   Storage模块

Storage模块基于ipfs实现

```
    @Test
    public void IpfsService(){
        String multiaddr = "/ip4/127.0.0.1/tcp/5001";
        IpfsService ipfsService= IpfsService.getInstance(multiaddr);
    }

```

#####   Wallet模块

`Wallet`模块是对用户钱包的管理，针对不同的链，有不同的实现。目前主要有基于ETH链的`EthWalletService`;基于ELA链的`ElaWalletService`;基于ETH侧链的`ElaETHSideWalletService`;基于DID侧链的`ElaDIDSideWalletService`。用户根据自己的需要，选择不同的实现类。




####  1.4 API说明

 -  1.1.[ AssetManagement（资产管理）][1]
 -  1.2.[ Merchant（商家）][2]
 -  1.3.[ Passport（身份认证）][3]
 -  1.4.[ Storage（存储）][4]
 -  1.5.[ Utility（工具）][5]
 -  1.6.[ Wallet（钱包）][6]
 <!---  1.7.[ Payment（支付）] [7]-->
 <!---  1.8. [Message（消息）] [8]-->
 
[1]: http://www.elastosdma.org/apidoc/AssetManagement%20API.html
[2]: http://www.elastosdma.org/apidoc/Merchant%20API.html

[3]: http://www.elastosdma.org/apidoc/Passport%20API.html
[4]: http://www.elastosdma.org/apidoc/Storage%20API.html
[5]: http://www.elastosdma.org/apidoc/Utility%20API.html
[6]: http://www.elastosdma.org/apidoc/Wallet%20API.html
[7]: http://www.elastosdma.org/apidoc/Payment%20API.html
[8]: http://www.elastosdma.org/apidoc/Message%20API.html

### 2、Android SDK 开发指南

#### 2.1 SDK说明

平台Android SDK 是通过服务（Service）的形式对外提供功能，具体包括资产管理服务（AssetManagement ）个人数据服务（Passport）存储服务（Storage）钱包服务（ Wallet）商户服务 （ Merchant），消息服务（ Message），支付服务（Payment）工具类（ Utility） 。SDK 提供以同步或异步方式发送交易、查询交易等的接口。无论以同步或异步的方式发送交易，SDK 封装了发送交易后查询收据的逻辑，以便您查看交易的执行结果。

####  2.2 快速开始

集成和开发，本项目SDK使用AAR的打包方式

步骤1：下载DMA客户端SDK

包含DMA_BASE、DMA_SERVICE、DMA_MESSAGE、DMA_utility

 步骤2：导入SDK


步骤3：在主项目的 build.gradle 中，添加下面的内容，将 libs 目录作为依赖仓库：


    allprojects {
    
        repositories {
        // 添加下面的内容
        flatDir {
            dirs 'libs'
        }

        // ... jcenter() 等其他仓库
    }
    }

步骤4：在您 App Module 的 build.gradle 中，添加下面的内容，将DMA SDK 作为项目依赖：

    dependencies {
    
    // 添加下面的内容
    api 'org.elastos:carrier:5.4.0'
    implementation 'org.elastos:ElastosSdkWallet:v0.1.20@aar'
    api 'org.web3j:core:3.3.1-android'
	api(name: 'dma_assetmanagement_common1.0', ext: 'aar')
    api(name: 'dma_config_sf1.0', ext: 'aar')
    api(name: 'dma_merchant_sf1.0', ext: 'aar')
    api(name: 'dma_passport_common1.0', ext: 'aar')
    api(name: 'dma_payment_sf1.0', ext: 'aar')
    api(name: 'dma_storage_sf1.0', ext: 'aar')
    api(name: 'dma_wallet_common1.0', ext: 'aar')
    api(name: 'dma_node_sf1.0', ext: 'aar')
    api(name: 'dma_utility_common1.0', ext: 'aar')
    api(name: 'dma_message_common1.0', ext: 'aar')
    api(name: 'dma_ticket_sf1.0', ext: 'aar')
        // ... 其他依赖项
    }
至此，DMA SDK 开发资源导入完成。

步骤5：添加运行权限

为正常完成良好的体验，DMA SDK 需要使用下面这些权限：

    android.permission.INTERNET
    android.permission.ACCESS_NETWORK_STATE
    android.permission.ACCESS_WIFI_STATE

您需要在 AndroidManifest 里配置以上 3 个权限，DMA SDK 在运行时需要进行网络连接，并在必要的时候判断网络连接的状态（4G/Wi-Fi）等来进行应用体验的优化。

#### 2.3 接口调用说明

    初始化节点信息
      public static String didip = "http://54.64.220.165:21604";//测试DID 
    public static String elaip = "http://54.64.220.165:21334";//测试ELA
    public static String ip = "http://47.105.136.158:8545";//DMAtestlink
    public static String ipfsIP="http://47.105.136.158:8080";//ipfs生产
    private volatile static EthWalletService ethWalletService;
    	/**
    	*初始化钱包服务
    	**/
        public static EthWalletService getClient() {
        if (ethWalletService == null) {
            ethWalletService = new EthWalletService(ip);
        }
        return ethWalletService;
    }
  需要在新线程中调用接口（可参考 demo 实现）

    示例代码：
    private void verifyWallet(String pwd){
    new AsyncTask<Void, Void,  Passport >(){
    @Override
    protected  Passport doInBackground(Void... params) {
       Passport passport= passportService.create(HdSupport.MnemonicType.ENGLISH,"");
        return passport;
    }
    protected void onPostExecute( Passport  passport) {
             System.out.println(passport.getMnemonic());
       System.out.println(passport.getId
    ());
    //根据DID产生的助记词，导出ETH钱包
    EthAccount ethAccount=NodeClient.getClient().exportByMnemonic(passport.getMnemonic());
    //根据DID产生的助记词，导出ELA钱包
    ElaWallet elaWallet= NodeClient.getHdWallet(TestActivity.this,words);

    };
    }.executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR);
    }
#### 2.4   接口测试
  
  首先根据选择测试的链，调用对应的创建钱包账户接口，创建无需准备对应的货币
  
  ELA主链 转账交易transfer()测试需要ELA主链币
  
  DID链，写入数据passport.setInfo() 需要准备DID侧链币，可通过主链充值的方式，也可以通过其他钱包转账的方式
  
  ETH侧链，转账交易transfer()，合约发布deploy()，发布资产mint() 资产上架onSales() 资产下架 offSales() 创建订单createOrder() 等链上交易接口需要准备测试币
  
  
#### 2.5 API详细说明

 - 1.1. [AssetManagement（资产管理）][1]
 - 1.2.[ Merchant（商家）][2]
 -  1.3. [Message（消息）][3]
 -  1.4.[ Passport（身份认证）][4]
 -  1.5.[ Payment（支付）][5]
 -  1.6. [Storage（存储）][6]
 -  1.7.[ Utility（工具）][7]
 -  1.8.[ Wallet（钱包）][8]
 -  1.9 [环境配置 ][9]
    
[1]: http://www.elastosdma.org/apidoc/AssetManagement%20API.html
[2]: http://www.elastosdma.org/apidoc/Merchant%20API.html
[3]: http://www.elastosdma.org/apidoc/Message%20API.html
[4]: http://www.elastosdma.org/apidoc/Passport%20API.html
[5]: http://www.elastosdma.org/apidoc/Payment%20API.html
[6]: http://www.elastosdma.org/apidoc/Storage%20API.html
[7]: http://www.elastosdma.org/apidoc/Utility%20API.html
[8]: http://www.elastosdma.org/apidoc/Wallet%20API.html
[9]: http://www.elastosdma.org/apidoc/index.html

### 3、IOS SDK 开发指南

#### 3.1 SDK说明
平台Android SDK 是通过服务（Service）的形式对外提供功能，具体包括资产管理服务（AssetManagement ）个人数据服务（Passport）存储服务（Storage）钱包服务（ Wallet）商户服务 （ Merchant），消息服务（ Message），支付服务（Payment）工具类（ Utility） 。SDK 提供以同步或异步方式发送交易、查询交易等的接口。无论以同步或异步的方式发送交易，SDK 封装了发送交易后查询收据的逻辑，以便您查看交易的执行结果。
#### 3.2 快速开始
#Swift: 5.0 以上

1 -- 先使用Carthage

在文件中添加如下


```
github "tang3680564/DMASDK" "master"
```


执行命令


```
Carthage update --platform ios
```


2 -- 再使用 pod

在文件中添加如下


```
pod 'ElastosCarrierSDK', '~> 5.3.2'
```


执行命令


```
pod install
```


最后将 carthage 的 build 里面的 framework 和 lib目录中的ElastosSdkWallet.framework ,ElastosSdkKeypair.framework添加到项目当中

builsetting: bitcode -> false

在使用的地方使用

import DMASDKV1
#### 3.3 接口调用说明
#### 1.钱包相关:现在支持 eth,ela,did三个钱包


###### 生成eth钱包:

```

///创建 eth 钱包服务

let ethService : EthService = EthService();

///生成(助记词,私钥,地址,)

let result = ethService.create()

///助记词

let mnemonic = result.0

///私钥

let privateKey = result.1

///地址

let address = result.2
```

###### 查询余额


```
///节点地址

let url = ""

///创建 eth 钱包服务

let ethService : EthService = EthService(url : url);

///查询地址

let address = ""

///查询余额

let balance = ethService.balances(address:address)
```

#### 2存储相关

##### 1.上传


```
///ipfs节点地址,例如:"47.105.136.158"

let url = ""

///上传节点端口,例如:8080

let serverPost = ""

///创建 ipfs 服务

let ipfs = IpfsService(URL : url,serverPost : serverPost)

///上传,data 数据

let data = Data()

///上传返回凭证

let hash = ipfs.add(fileData : data)
```

##### 2.下载

```
///ipfs节点地址,例如:"47.105.136.158"

let url = ""

///下载节点端口,例如:5001

let serverPost = ""

///创建 ipfs 服务

let ipfs = IpfsService(URL : url,serverPost : serverPost)


///上传返回的凭证

let hash = ""

///下载

let arrary = ipfs.getBytes(hash:hash)

```

#### 3.资产相关

##### 1.ChargeActivityService(收费活动模板)

###### 发布合约


```
///eth的节点地址

let url = ""

///创建服务

let chargeActivityService = ChargeActivityService(url : url)
let privateKey = ""
let gasPrice = defaultGasPrice
let gasLimit = defaultGasLimit
let name = ""
let symbol = ""
let metadata = ""
let endtime = "\(Int(Date().timeIntervalSince1970) + 3600 * 24)"
/// - Parameters:
    ///   - privateKey: 私钥
    ///   - gasPrice: gasPrice description
    ///   - gasLimit: gasLimit description
    ///   - name: 合约名称
    ///   - symbol: 合约简介
    ///   - metadata: 合约描述
    ///   - endtime: 活动结束时间
    /// - Returns: assetAddress : 资产合约地址,platformAddress : 托管合约地址
    let result = chargeActivityService.deploy(privateKey:privateKey,gasPrice:gasPrice,gasLimit:gasLimit,name:name,symbol:symbol,metadata:metadata,endtime : endtime)
```

###### 初始化资产


```
///eth的节点地址

let url = ""

///创建服务

let chargeActivityService = ChargeActivityService(url : url)

let privateKey = ""
let contractAddress = ""
let toAddress = ""
let tokenArr : NSMutableArray = [1000]

 /// 批量创建资产
    ///
    /// - Parameters:
    ///   - privateKey: 私钥
    ///   - assetAddress: 资产合约地址
    ///   - to: 资产归属地址
    ///   - array: 资产 id 数组
    ///   - metaData: 资产描述
    ///   - isTransfer: 是否可以转送
    ///   - isBurn: 是否可以销毁
    ///   - gasLimit: gasLimit description
    ///   - gasPrice: gasPrice description
    /// - Returns: return value description
    
let reult = charge.mintWithArrayGas(privateKey : privateKey,assetAddress : contractAddress,to: toAddress, array: tokenArr as! Array<Any>, metaData: "", isTransfer: true, isBurn: true)
```



#### 3.4 API详细说明

 -  1.1.[ AssetManagement（资产管理）][1]
 -  1.2.[ Merchant（商家）][2]
 -  1.3.[ Passport（身份认证）][3]
 -  1.4.[ Storage（存储）][4]
 -  1.5.[ Utility（工具）][5]
 -  1.6.[ Wallet（钱包）][6]
 -  1.7.[ Payment（支付）][7]
 -  1.8.[Message（消息）][8]
 
[1]: http://www.elastosdma.org/apidoc/AssetManagement%20API.html
[2]: http://www.elastosdma.org/apidoc/Merchant%20API.html

[3]: http://www.elastosdma.org/apidoc/Passport%20API.html
[4]: http://www.elastosdma.org/apidoc/Storage%20API.html
[5]: http://www.elastosdma.org/apidoc/Utility%20API.html
[6]: http://www.elastosdma.org/apidoc/Wallet%20API.html
[7]: http://www.elastosdma.org/apidoc/Payment%20API.html
[8]: http://www.elastosdma.org/apidoc/Message%20API.html

## 四、常见问题

## 五、错误码


    SUCCESS | 0 | 操作成功
    ERROR | -1 | 请求失败
    PARAMS_ERROR | 2 | 参数错误
    SYSTEM_ERROR | 4 | 系统异常

    IO_ERROR | 29 | 远程调用失败
    REVOKE_ERROR | 72 | 下架失败
    ON_SALE_ERROR | 73 | 上架失败
    CONFIRM_ORDER_ERROR | 92 | 下单失败

    CREATE_ORDER_ERROR | 96 | 创建订单失败
    PAYMENT_MERCHANT_REGISTERED | 116 | 已注册
    WALLET_ADDRESS_EMPTY | 117 | 钱包地址不能为空
    PAYMENT_MERCHANT_ID_EMPTY | 118 | 支付商户号不能为空
    PAYMENT_MERCHANT_ID_NOT_EXISTS | 119 | 支付商户号不存在
    PAYMENT_SIGN_EMPTY | 120 | 验签字段不能为空
    PAYMENT_SIGN_INVALID | 121 | 验签不通过
    ORDER_EXISTS | 124 | 订单号已存在
    SIDE_ERROR | 127 | 交易类型错误

    CONTRACT_ADDRESS_NOT_EXISTS | 8 | 合约不存在
    ORDER_NO_EMPTY | 19 | 订单号不能为空
    TOKEN_ADDRESS_ERROR | 10001 | token地址不存在或错误
    TOKEN_BALANCE_UNDERFINANCED | 10002 | token余额不足
    GASLIMINT_SHORT | 10003 | gasLimit缺少
    BALANCE_UNDERFINANCED | 10004 | 余额不足
    APPROVE_TOKEN_BALANCE_UNDERFINANCED | 10005 | 授权token余额不足
    CONTRACT_DEPLOY_ERROR | 10006 | 合约创建失败
    PRIVATEKEY_ERROR | 10007 | 私钥错误
    ADDRESS_ERROR | 10008 | 地址错误
    RPC_REQUEST_FAILED | 20001 | rpc请求失败
    RPC_ERROR | 30001 | 远程调用失败
    NOT_ENOUGH_TRANSACTION_PARAMETER | 40001 | 参数不足
    NOT_VALID_DATA_TO_RAW_TX | 40002 | 交易数据无效
    NOT_VALID_TYPE_TO_TRANSFER | 40003 | 交易类型无效
    PARAMETER_INVALID | 40004 | 参数无效
    SIGN_DID_INFO_INVALID | 40005 | did信息签名错误
    TRANSFER_FAILED | 40006 | 交易失败
    NO_INFO | 40007 | 未查询到信息
