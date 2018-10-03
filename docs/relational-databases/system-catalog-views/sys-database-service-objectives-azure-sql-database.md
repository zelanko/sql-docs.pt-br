---
title: database_service_objectives (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/30/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
keywords:
- pool Elástico
- pool Elástico, gerenciamento
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: a8b37ada1fa7c6024a5454ed907b886e513c151c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769304"
---
# <a name="sysdatabaseserviceobjectives-azure-sql-database"></a>database_service_objectives (banco de dados SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Retorna a edição (camada de serviço), o objetivo de serviço (tipo de preço) e o nome do pool Elástico, se houver, para um banco de dados SQL do Azure ou um Azure SQL Data Warehouse. Se conectado ao banco de dados mestre em um servidor de banco de dados SQL, retorna informações sobre todos os bancos de dados. SQL Data Warehouse do Azure, você deve estar conectado ao banco de dados mestre.  
  
  
 Para obter informações sobre preços, consulte [opções de banco de dados SQL e desempenho: preços de banco de dados SQL](https://azure.microsoft.com/pricing/details/sql-database/) e [preços do SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para alterar as configurações de serviço, consulte [ALTER DATABASE (banco de dados SQL)](../../t-sql/statements/alter-database-azure-sql-database.md) e [ALTER DATABASE (SQL Data Warehouse do Azure)](../../t-sql/statements/alter-database-azure-sql-data-warehouse.md).  
  
 O modo de exibição database_service_objectives contém as colunas a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|database_id|INT|A ID do banco de dados, exclusivo em uma instância do servidor de banco de dados SQL. Permite junções com [sys. Databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edição|sysname|A camada de serviço para o banco de dados ou data warehouse: **básicas**, **padrão**, **Premium** ou **Data Warehouse**.|  
|service_objective|sysname|O tipo de preço do banco de dados. Se o banco de dados está em um pool Elástico, retornará **ElasticPool**.<br /><br /> Sobre o **básica** tier, retorna **básica**.<br /><br /> **Banco de dados individual em uma camada de serviço standard** retorna um dos seguintes: S0, S1, S2, S3, S4, S6, S7, S9 ou S12.<br /><br /> **Banco de dados individual em uma camada premium** retorna o seguinte: P1, P2, P4, P6, P11 ou P15.<br /><br /> **SQL Data Warehouse** retorna DW100 por meio de DW10000c.|  
|elastic_pool_name|sysname|O nome da [pool Elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) que o banco de dados pertence. Retorna **nulo** se o banco de dados é um banco de dados ou um warehoue de dados.|  
  
## <a name="permissions"></a>Permissões  
 Requer **dbManager** permissão no banco de dados mestre.  No nível do banco de dados, o usuário deve ser o criador ou proprietário.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo pode ser executado no banco de dados mestre ou em bancos de dados do usuário. A consulta retorna o nome, serviço e informações sobre níveis de desempenho dos bancos de dados.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
