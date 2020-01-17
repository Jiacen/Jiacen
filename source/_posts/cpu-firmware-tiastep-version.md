---
title: S7-1500 CPU 固件版本和 TIA STEP 7 版本你应该知道的事情
date: 2020-01-17 12:24:22
tags: [Siemens, TIA PORTAL, S7-1500, firmware] 
---
### 1. CPU的固件版本真正决定了所有的软件、硬件的新功能

| 新固件发布时的highlight功能    | S7-1500 CPU 的固件版本  | 
| :-------- | --------:|
| Modify tags via Display or Web Server	     | FW V1.8 及以上     | 
| Array [*]	     | FW V2.0 及以上     | 
| Interface X2 support PROFINET RT(Controller or iDevice)| FW V 2.0 及以上|
|Server of the OPC UA data access	| FW V 2.0 及以上|
|Consistent upload of fail-safe projects	|FW V 2.1 及以上|
|Break point for SCL & STL programming language|	FW V 2.5 及以上|
|References |	FW V 2.5 及以上|
|Structure of the Software units	|FW V 2.6 及以上|
|OPC UA Client integrated	|FW V 2.6 及以上|
|PROFINET IRT DX	|FW V 2.8 及以上|

***

### 2. 固件版本的组态与TIA STEP7的版本密切相关
| S7-1500 CPU 的固件版本    | STEP 7 Professional 的版本(或者更高版本) | 
| :-------- | --------:|
| FW V 2.8	     | V 16     | 
| FW V 2.6     | V 15.1     | 
| FW V 2.5| V 15|
|FW V 2.1	| V 14 SP1|
|FW V 2.0	|V 14|
|FW V 1.5/1.6/1.7/1.8	|	V 13/V 13 SP1|
|FW V 1.0/1.1 |	V 12|

***

### 3. 只有通过TIA STEP7组态了CPU的新功能版本后，该软件功能才能真正实现

***

### 4. 旧版TIA STEP7（<V 16）组态旧版 CPU 固件版本兼容新硬件

![](/images/cpufirmware.JPG)

***

### 5. CPU 的固件版本可自行升级

但只能在相同订货号的前提下进行（在相同订货号下可以从V x-->V y)；  
一旦新固件版本对应的 CPU 订货号与旧有硬件不同，无法进行升级操作。  
固件版本的下载与升级方式，详见在线支持ID: 109478459。
