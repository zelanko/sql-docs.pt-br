---
title: "Fazer logon em uma instância do SQL Server (prompt de comando) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: "26"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 00b2a66c23d60597c3a2c4c0f66a660788b3c0af
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Fazer logon em uma instância do SQL Server (prompt de comando)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como testar a conectividade com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; use o utilitário **SQLCMD**.  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>Para fazer logon em a instância padrão do SQL Server  
  
1.  De um prompt de comando, insira o comando a seguir para se conectar usando a Autenticação do Windows:  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>Para fazer logon em uma instância nomeada do SQL Server  
  
1.  De um prompt de comando, insira o comando a seguir para se conectar usando a Autenticação do Windows:  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Utilitário osql](../../tools/osql-utility.md)  
  
  
