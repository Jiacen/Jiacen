---
title: TIPS4TIA
date: 2019-04-03 11:26:09
tags: [Siemens, TIA PORTAL]
---
*All the screenshots based on TIA PORTAL STEP7 PRO Version V15 Upd3 and S7-1500 V2.X*
***
### 1. Group editor on Task Bar
before 
![](/images/TIPS4TIA_01.png)   
after
![](/images/TIPS4TIA_02.png)  
***
### 2. Specify a central storage location for user-defined documents, then press <Shift+F1> to open user help
![](/images/TIPS4TIA_03.png)  
***
### 3. Reinitialization or Synchronization all the tags in DB
![](/images/TIPS4TIA_04.png)  
***
### 4. How to specify the block parameters displayed or hidden?
![](/images/TIPS4TIA_05.png)
***
### 5. Set "Retain" attribute for newly created tags of iDB w/o optimized access 
![](/images/TIPS4TIA_06.png)
***
### 6. How to measure the totally cycle time of OB?
With the "RT_INFO" instruction, via the "MODE" parameter you define which runtime you want to read out, then at the "INFO" parameter you generate statistics on the runtime of specific OB.  
- MODE:= 1 (runtime of a specific OB)  
- MODE:= 2 (maximum runtime of a specific OB)  
- MODE:= 3 (minimum runtime of a specific OB)  
- MODE:= 25 (current / last cycle time or duration of the last cycle)  

*more information can be check out from id: 87668055*
***
### 7. Arrays with variable length via formal parameter Array [*]
![](/images/TIPS4TIA_07.png)
***
### 8. How to unlocked and configure the alarm text of "Program_alarms"?
![](/images/TIPS4TIA_08.png)
![](/images/TIPS4TIA_09.png)
***
### 9. Declares all internal parameters (included step & transition) of a GRAPH block as retentive parameters
![](/images/TIPS4TIA_10.png)
***
### 10. How to reduce or complete the parameters of call template in SCL?
![](/images/TIPS4TIA_11.png)