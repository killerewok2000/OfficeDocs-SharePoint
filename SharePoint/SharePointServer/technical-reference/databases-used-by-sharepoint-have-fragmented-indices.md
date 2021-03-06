---
title: "Databases used by SharePoint have fragmented indices (SharePoint Server)"
ms.author: stevhord
author: bentoncity
manager: pamgreen
ms.date: 8/31/2017
ms.audience: ITPro
ms.topic: troubleshooting
ms.prod: sharepoint-server-itpro
localization_priority: Normal
ms.collection:
- IT_Sharepoint_Server
- IT_Sharepoint_Server_Top
ms.assetid: 043481c0-f467-44ed-9772-d822eb314a81
description: "Summary: Learn how to resolve the SharePoint Health Analyzer ruleDatabases used by SharePoint have fragmented indicesfor SharePoint Server 2016 and SharePoint 2013."
---

# Databases used by SharePoint have fragmented indices (SharePoint Server)

 **Summary:** Learn how to resolve the SharePoint Health Analyzer rule "Databases used by SharePoint have fragmented indices" for SharePoint Server 2016 and SharePoint 2013. 
  
 **Rule Name:** Databases used by SharePoint have fragmented indices. 
  
 **Summary:** SharePoint Server uses SQL Server to store most of the content for the Web site and configuration settings. One or more of the databases used by SharePoint Server have fragmented indexes. A fragmented index can cause a degrade in performance. 
  
 **Cause:** Database indexes can fragment over time as a result of insert and update operations performed by SharePoint Server. We recommend that you periodically delete and rebuild these indexes to improve system performance. 
  
 **Resolution: Reorganize and rebuild indexes**
  
1. To correct index fragmentation, you can reorganize an index or rebuild an index. For more information, see [Reorganize and Rebuild Indexes](http://go.microsoft.com/fwlink/?LinkID=780583&amp;clcid=0x409).
    

