---
title: "Fazer logon em uma instância do SQL Server (prompt de comando) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f5899510b24205d4ebc82dc5779505c522b340d6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Fazer logon em uma instância do SQL Server (prompt de comando)
  Este tópico descreve como testar a conectividade com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; use o utilitário **sqlcmd** .  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Utilitário osql](../../tools/osql-utility.md)  
  
  
