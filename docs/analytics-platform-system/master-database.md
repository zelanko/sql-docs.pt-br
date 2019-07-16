---
title: Banco de dados mestre - Parallel Data Warehouse | Microsoft Docs
description: Saiba mais sobre o banco de dados mestre no Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 9f37c7a85baea3b41f6016a57e4f57579b427719
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960659"
---
# <a name="master-database---parallel-data-warehouse"></a>Banco de dados mestre - Parallel Data Warehouse
O banco de dados mestre do SQL Server PDW armazena informações de logon de nível de dispositivo e o catálogo de banco de dados. É um SQL Server banco de dados mestre que reside no nó de controle. Como tal, ele fornece funcionalidade semelhante para o SQL Server PDW como mestre fornece ao SQL Server.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
A lista a seguir descreve as operações que você não pode executar no banco de dados mestre do SQL Server PDW.  
  
Você *não é possível:*  
  
-   Execute um backup diferencial do mestre.  
  
-   Crie objetos de usuário no mestre.  
  
-   Altere o agrupamento de mestre.  
  
-   Altere o proprietário do mestre.  
  
-   Descarte ou renomeie o mestre.  
  
-   Modificar permissões para o mestre.  
  
-   Execute **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Crie um backup completo do mestre.|Exemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obter mais informações, consulte [banco de dados de BACKUP](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restaurar o banco de dados mestre|Para restaurar o banco de dados mestre, use o [restaurar o banco de dados mestre](restore-the-master-database.md) página na ferramenta do Configuration Manager.|  
|Exibir informações de catálogo do banco de dados.|`SELECT * FROM master.sys.databases;`|  
|Exibir informações de logon e a permissão de todo o sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
