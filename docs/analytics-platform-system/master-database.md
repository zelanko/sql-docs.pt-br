---
title: Banco de dados mestre
description: Saiba mais sobre o banco de dados mestre em paralelo data warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafef8a5b702b6df4475d34e9395bb12bc9461fb
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400982"
---
# <a name="master-database---parallel-data-warehouse"></a>Banco de dados mestre-data warehouse paralelos
O banco de dados mestre do SQL Server PDW armazena informações de logon no nível do dispositivo e o catálogo de banco de dados. É um banco de dados mestre SQL Server que reside no nó de controle. Assim, ele fornece uma funcionalidade semelhante à SQL Server PDW como o mestre fornece a SQL Server.  
  
Para obter mais informações sobre bancos de dados do sistema, consulte [bancos de dados do sistema](system-databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
A lista a seguir descreve as operações que você não pode executar no banco de dados do SQL Server PDW mestre.  
  
Você *não pode:*  
  
-   Execute um backup diferencial do mestre.  
  
-   Crie objetos de usuário no mestre.  
  
-   Alterar o agrupamento do mestre.  
  
-   Altere o proprietário do mestre.  
  
-   Remover ou renomear mestre.  
  
-   Modificar permissões para mestre.  
  
-   Execute **DBCC SHRINKLOG**.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarefa|Descrição|  
|--------|---------------|  
|Crie um backup completo do mestre.|Exemplo:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />Para obter mais informações, consulte [backup Database](../t-sql/statements/backup-database-parallel-data-warehouse.md).|  
|Restaurar o banco de dados mestre|Para restaurar o banco de dados mestre, use a página [restaurar o banco de dados mestre](restore-the-master-database.md) na ferramenta de Configuration Manager.|  
|Exibir informações do catálogo de banco de dados.|`SELECT * FROM master.sys.databases;`|  
|Exibir informações de logon e permissão de todo o sistema.|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
