---
title: sys.database_service_objectives (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 08/30/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "Pool Elástico"
- "pool Elástico, gerenciamento"
f1_keywords: DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
caps.latest.revision: "16"
author: CarlRabeler
ms.author: carlrab
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 72cc970e8e6b37988399707b5cef77cbda3afd36
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>sys.database_service_objectives (banco de dados do SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Retorna a edição (camada de serviço), o objetivo de serviço (preço) e o nome do pool Elástico, se houver, para um banco de dados do SQL Azure ou um Azure SQL Data Warehouse. Se conectado ao banco de dados mestre em um servidor de banco de dados SQL, retorna informações sobre todos os bancos de dados. Para o Azure SQL Data Warehouse, você deve estar conectado ao banco de dados mestre.  
  
  
 Para obter informações sobre preços, consulte [desempenho e opções de banco de dados SQL: preços de banco de dados do SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/) e [preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para alterar as configurações de serviço, consulte [ALTER DATABASE (banco de dados do SQL Azure)](../../t-sql/statements/alter-database-azure-sql-database.md) e [ALTER DATABASE (Azure SQL Data Warehouse)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
  
 A exibição sys.database_service_objectives contém as seguintes colunas.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|INT|A ID do banco de dados, exclusivo em uma instância do servidor de banco de dados SQL. Junções com [sys. Databases &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edição|sysname|A camada de serviço para o banco de dados ou de data warehouse: **básica**, **padrão**, **Premium** ou **Data Warehouse**.|  
|service_objective|sysname|A camada de preços do banco de dados. Retorna se o banco de dados em um pool Elástico, **ElasticPool**.<br /><br /> Sobre o **básica** camada, retorna **básica**.<br /><br /> **Banco de dados único em uma camada de serviço padrão** retorna um dos seguintes: S0, S1, S2 ou S3.<br /><br /> **Banco de dados único em uma camada premium** retorna o seguinte: P1, P2, P4, P6/P3 ou P11.<br /><br /> **SQL Data Warehouse** retorna DW100 por meio de DW2000.|  
|elastic_pool_name|sysname|O nome do [pool Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) que o banco de dados pertence. Retorna **nulo** se o banco de dados é um banco de dados ou um warehoue de dados.|  
  
## <a name="permissions"></a>Permissões  
 Requer **dbManager** no banco de dados mestre.  No nível do banco de dados, o usuário deve ser o criador ou o proprietário.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo pode ser executado no banco de dados mestre ou em bancos de dados do usuário. A consulta retorna o nome, serviço e informações sobre níveis de desempenho dos bancos de dados.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
