---
title: "Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usu&#225;rio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UDTs [SQL Server], XML"
  - "tipos definidos pelo usuário [SQL Server], XML"
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Suporte a FOR XML para os UDTs (tipos de dados definidos pelo usu&#225;rio)
  FOR XML não oferece suporte a UDTs (tipos de dados definidos pelo usuário) do CLR (Common Language Runtime).  
  
 Para usar FOR XML com tipos definidos pelo usuário do CLR, verifique se o tipo de dados tem uma serialização XML e usa uma conversão explícita para XML na cláusula select de FOR XML.  
  
## Consulte também  
 [Suporte a FOR XML para vários tipos de dados SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  