---
title: Banco de dados mestre - Parallel Data Warehouse | Microsoft Docs
description: Saiba mais sobre o banco de dados mestre no Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: bf07b9c27e08a49cb0866b177a0ec37fed4528a0
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="master-database---parallel-data-warehouse"></a>Banco de dados mestre - Parallel Data Warehouse
O banco de dados mestre do SQL Server PDW armazena informações de logon de nível de dispositivo e o catálogo de banco de dados. É um SQL Server banco de dados mestre que reside no nó de controle. Como tal, ele oferece funcionalidade semelhante para o SQL Server PDW como mestre fornece para o SQL Server.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
A lista a seguir descreve as operações que você não pode executar o banco de dados mestre do SQL Server PDW.  
  
Você *não pode:*  
  
-   Execute um backup diferencial do mestre.  
  
-   Crie objetos de usuário no mestre.  
  
-   Altere o agrupamento de mestre.  
  
-   Altere o proprietário do mestre.  
  
-   Remover ou renomear mestre.  
  
-   Modificar permissões para mestre.  
  
-   Executar **SHRINKLOG DBCC**.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Tarefa|Description|  
|--------|---------------|  
|Crie um backup completo do mestre.|Exemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obter mais informações, consulte [banco de dados de BACKUP](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restaurar o banco de dados mestre|Para restaurar o banco de dados mestre, use o [restaurar o banco de dados mestre](restore-the-master-database.md) página ferramenta do Configuration Manager.|  
|Exibir informações de catálogo de banco de dados.|`SELECT * FROM master.sys.databases;`|  
|Exibir informações de logon e a permissão de todo o sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
