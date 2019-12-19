# Ticket API

## **介绍**

Ticket 模块覆盖了通用的票务领域，目前可实现收费类型、免费类型、质押类型的票务资产的发行、售卖、转移、验票等。整个交易过程没有平台、三方的参与，使用智能合约完成去中心化的可信交易。我们站在通用票务领域的角度，设计了符合票务标准的数据结构，同时也为用户提供自定义属性设置的接口，方便应用扩展。


## **目录**
- [common](#1common)
    - [资产合约](#11资产合约)
        - [转移门票](#111转移门票)
        - [销毁门票](#112销毁门票)
        - [签到](#113签到)
        - [设置门票是否可转移](#114设置门票是否可转移)
        - [获取发行量](#115获取发行量)
    - [托管合约](#12托管合约)
        - [创建托管合约](#121创建托管合约)
        - [创建订单](#122创建订单)
        - [获取所有订单记录](#123获取所有订单记录)
        - [获取订单详情](#124获取订单详情)
- [票务](#2票务) 
    - [资产合约](#21资产合约)
        - [创建门票合约](#211创建门票合约)
        - [生成门票](#212生成门票)
        - [获取票务合约信息](#213获取票务合约信息)
        - [获取票务信息](#214获取票务信息)
        - [获取用户地址下拥有的门票合约](#215查询用户地址下拥有的门票合约)
        - [查询用户地址下拥有的门票](#216查询用户地址下拥有的门票)
    - [托管合约](#22托管合约)
        - [上架](#221上架)
        - [下架](#222下架)
        - [我上架的合约信息](#223我上架的合约信息)
        - [我上架的](#224我上架的)
        - [我未上架的](#225我未上架的)
- [活动](#3活动) 
    - [资产合约](#31资产合约)
        - [创建门票合约](#31资产合约)
        - [生成门票](#312生成门票)
        - [获取票务合约信息](#313获取票务合约信息)
        - [获取票务信息](#314获取票务信息)
        - [查询用户地址下拥有的门票合约](#315查询用户地址下拥有的门票合约)
        - [查询用户地址下拥有的门票](#316查询用户地址下拥有的门票)
    - [托管合约](#32托管合约) 
        - [收费合约](#321收费合约)
            - [上架](#3211上架)
            - [下架](#3212下架)
            - [结束活动](#3213结束活动)
            - [我上架的合约信息](#3214我上架的合约信息)
            - [我上架的](#3215我上架的)
            - [我未上架的](#3216我未上架的)
        - [质押合约](#322质押合约)
            - [上架](#3221上架)
            - [下架](#3222下架)
            - [结束活动](#3223结束活动)
            - [退还押金](#3224退还押金)
            - [签到](#3225签到)
            - [我上架的合约信息](#3226我上架的合约信息)
            - [我上架的](#3227我上架的)
            - [我未上架的](#3228我未上架的)

##  **API**

### 1.common
#### 1.1资产合约

##### 1.1.1.转移门票
-   方法名 ：`transfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| from | String  | from|
| to | String  |  to |
| tokenIds | List  |  tokenIds |
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |


##### 1.1.2.销毁门票
-   方法名 ：`burn()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| tokenId | number  |   |
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |

##### 1.1.3.签到
-   方法名 ：`verify()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenId | number  | tokenId |
| owner | String  | 资产拥有者 |

##### 1.1.4.设置门票是否可转移

-   方法名 ：`setCanTransfer()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| tokenId | number  |   |
| transferable | bool  | 是否可转移  |
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |

##### 1.1.5.获取发行量
-   方法名 ：`getTotalSupply()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|

####1.2.托管合约
##### 1.2.1.创建托管合约
-   方法名 ：`createContract()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |


##### 1.2.2.创建订单
-   方法名 ：`placeOrder()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenIds|List|  |
| sumPrice|decimal| 支付金额 |
| owner| String| 拥有者 |


##### 1.2.3.获取所有订单记录
-   方法名 ：`getOrders()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustContractAddress | String  | 托管合约地址|
| dmaNodeUrl | String  | dma 节点地址 |
| from | String  | from|
| to | String  |  to |

##### 1.2.4.获取订单详情
-   方法名 ：`getOrderInfoByHash()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | txId|
| dmaNodeUrl | String  | dma 节点地址 |





### 2.票务

#### 2.1.资产合约
##### 2.1.1.创建门票合约
-   方法名 ：`createContract()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| tokenMap | Map<BigInteger, TicketTokenInfo>  | token的信息|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |


##### 2.1.2.生成门票
-   方法名 ：`createAsset()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| tokenMap | Map<BigInteger, TicketTokenInfo>  | token的信息|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |



##### 2.1.3.获取票务合约信息
-   方法名 ：`getContractInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|




##### 2.1.4.获取票务信息
-   方法名 ：`getAssetInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| tokenId | number  |   |



##### 2.1.5.查询用户地址下拥有的门票合约
-   方法名 ：`getContracts()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 用户地址|
| dmaNodeUrl | String  | dma 节点地址 |


##### 2.1.6.查询用户地址下拥有的门票
-   方法名 ：`getAssets()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner | String  | 用户地址|
| dmaNodeUrl | String  | dma 节点地址 |


#### 2.2.托管合约

##### 2.2.1.上架
-   方法名 ：`onShelves()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
|map|Map<tokenId,price>|  |
|owner| String| 拥有者 |



##### 2.2.2.下架
-   方法名 ：`offShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenIds|List|  |
| owner| String| 拥有者 |



##### 2.2.3.我上架的合约信息
-   方法名 ：`getOnShelveContracts()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管地址|


##### 2.2.4.我上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |


##### 2.2.5.我未上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |



### 3.活动
#### 3.1.资产合约
##### 3.1.1.创建门票合约
-   方法名 ：`createContract()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| ActivityContractInfo | ActivityContractInfo  | token的信息|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |

```
    private String dmaTag = "DMA_Activity";//固定字段，标识DMA票务类型。
    private String dmaExtenfTag;//扩展标签，使用者自定义
    private Long startTime; //开始时间
    private Long endTime;//结束时间
    private String title;//活动主题，使用者自定义
    private String describe;//活动描述，使用者自定义
    private String imgUrl;//活动封面图片，使用者自定义
    private String location;//主办地理位置，使用者自定义
    private String type;//类型，使用者自定义
    private String json;//扩展json，使用者自定义

```

##### 3.1.2.生成门票
-   方法名 ：`createAsset()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| tokenMap | Map<BigInteger, ActivityTokenInfo>  | token的信息|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |

```
    //ActivityTokenInfo
    private String contractAddress;
    private Boolean canTransfer;
    private String owner;
    private Long startTime; //开始时间
    private Long endTime;//结束时间
    private String ticketTag;//活动标签
    private String ticketType;//活动类型
    private Double price;//活动定价
    private String json;//扩展json

```





##### 3.1.3.获取票务合约信息
-   方法名 ：`getContractInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|




##### 3.1.4.获取票务信息
-   方法名 ：`getAssetInfo()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| tokenId | number  |   |



##### 3.1.5.查询用户地址下拥有的门票合约
-   方法名 ：`getContracts()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| owner | String  | 用户地址|
| dmaNodeUrl | String  | dma 节点地址 |


##### 3.1.6.查询用户地址下拥有的门票
-   方法名 ：`getAssets()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner | String  | 用户地址|
| dmaNodeUrl | String  | dma 节点地址 |



#### 3.2.托管合约

##### 3.2.1.收费合约


###### 3.2.1.1.上架
-   方法名 ：`onShelves()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
|map|Map<tokenId,price>|  |
|owner| String| 拥有者 |
|endTime| number| 活动结束时间(unixtime) |



###### 3.2.1.2.下架
-   方法名 ：`offShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenIds|List|  |
| owner| String| 拥有者 |

###### 3.2.1.3.结束活动
-   方法名 ：`endActivity()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |


###### 3.2.1.4.我上架的合约信息
-   方法名 ：`getOnShelveContracts()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管地址|



###### 3.2.1.5.我上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |


###### 3.2.1.6.我未上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |





##### 3.2.2.质押合约


###### 3.2.2.1.上架
-   方法名 ：`onShelves()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
|map|Map<tokenId,price>|  |
|owner| String| 拥有者 |
|endTime| number| 活动结束时间(unixtime) |



###### 3.2.2.2.下架
-   方法名 ：`offShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenIds|List|  |
| owner| String| 拥有者 |

###### 3.2.2.3.结束活动
-   方法名 ：`endActivity()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |


###### 3.2.2.4.退还押金
-   方法名 ：`refund()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenId | number  | tokenId |


###### 3.2.2.5.签到
-   方法名 ：`verify()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| privateKey | String  | 私钥|
| gasPrice | String  | gasPrice |
| gasLimit | String  | gasLimit |
| tokenId | number  | tokenId |
| owner | String  | 资产拥有者 |

###### 3.2.2.6.我上架的合约信息
-   方法名 ：`getOnShelveContracts()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管地址|



###### 3.2.2.7.我上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| trustAddress | String  | 托管合约地址|
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |


###### 3.2.2.8.我未上架的
-   方法名 ：`getOnShelves()`


-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| contractAddress | String  | 合约地址|
| owner| String| 拥有者 |
| dmaNodeUrl | String  | dma 节点地址 |
