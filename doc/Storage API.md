# Storage API


## **介绍**

Storage API提供存储相关功能，目前对ipfs进行封装，使用请阅读以下文档


## **Build**

```
private String httpUrl = "http://47.105.136.158:8080" ;
private String multiaddr = "/ip4/47.105.136.158/tcp/5001";
IpfsService ipfsService=IpfsService.getInstance();
```


## **目录**


- [1. 存储字节流](#1-存储字节流)
- [2. 存储文件](#2-存储文件)
- [3. 存储json](#3-存储json)
- [4. 根据hash值获取json](#4-根据hash值获取json)
- [5. 根据hash值获取字节流](#5-根据hash值获取字节流)


----------



## **API**

###   1. 存储字节流

-   方法名 ：`add()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| data | byte[]  | 字节流|


-   返回值类型：`String`

-   返回说明：

>   存储hash

###   2. 存储文件

-   方法名 ：`add()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| file | File  | 文件|


-   返回值类型：`String`

-   返回说明：

>   存储hash

###   3. 存储json

-   方法名 ：`add()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| json | String  | json|


-   返回值类型：`String`

-   返回说明：

>   存储hash

###   4. 根据hash值获取json

-   方法名 ：`getJson()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | hash|


-   返回值类型：`String`

-   返回说明：

>   json串


###   5. 根据hash值获取字节流

-   方法名 ：`getBytes()`

-   参数说明:

| 参数名 | 参数类型 | 参数说明|
| :----:| :----:  | :----:  |
| hash | String  | hash|


-   返回值类型：`byte[]`

-   返回说明：

>   字节流


