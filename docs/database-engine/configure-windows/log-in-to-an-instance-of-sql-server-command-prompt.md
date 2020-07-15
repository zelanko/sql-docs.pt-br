---
title: Fazer logon em uma instância do SQL Server (prompt de comando) | Microsoft Docs
description: Saiba mais sobre o utilitário "sqlcmd". Veja como usá-lo em um prompt de comando para testar a conectividade com uma instância do SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0723a5d463757eca93dd7bacb1fc2b8fe232cdd8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772408"
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>Fazer logon em uma instância do SQL Server (prompt de comando)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [Utilitário osql](../../tools/osql-utility.md)  
  
  
