---
description: sys.database_service_objectives (Banco de Dados SQL do Azure)
title: sys.database_service_objectives
titleSuffix: Azure SQL Database
ms.date: 03/21/2018
ms.service: sql-database
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.topic: conceptual
keywords:
- pool elástico
- pool elástico, gerenciamento
f1_keywords:
- DATABASE_SERVICE_OBJECTIVES_TSQL
ms.assetid: cecd8c31-06c0-4aa7-85d3-ac590e6874fa
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ffaa2eb4d9016436813ac57bdfb47031eadb1e97
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551451"
---
# <a name="sysdatabase_service_objectives-azure-sql-database"></a>sys.database_service_objectives (Banco de Dados SQL do Azure)
[!INCLUDE [asdb-asdbmi-asa](../../includes/applies-to-version/asdb-asdbmi-asa.md)]

Retorna a edição (camada de serviço), o objetivo de serviço (tipo de preço) e o nome do pool elástico, se houver, para um banco de dados SQL do Azure ou um SQL Data Warehouse do Azure. Se estiver conectado ao banco de dados mestre em um servidor do Banco de Dados SQL do Azure, retornará informações sobre todos os bancos de dados. Para o SQL Data Warehouse do Azure, você deve estar conectado ao banco de dados mestre.  
  
  
 Para obter informações sobre preços, consulte [Opções e desempenho do banco de dados SQL: preços do banco de dados SQL](https://azure.microsoft.com/pricing/details/sql-database/) e [preços de SQL data warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).  
  
 Para alterar as configurações de serviço, consulte [ALTER DATABASE (banco de dados SQL do Azure)](../../t-sql/statements/alter-database-azure-sql-database.md) e [alter database (Azure SQL data warehouse)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest).  
  
 A exibição sys. database_service_objectives contém as colunas a seguir.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|INT|A ID do banco de dados, exclusiva dentro de uma instância do servidor de banco de dados SQL do Azure. É possível associá [-lo com sys. databases &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).|  
|edition|sysname|A camada de serviço para o banco de dados ou data warehouse: **Basic**, **Standard**, **Premium** ou **data warehouse**.|  
|service_objective|sysname|O tipo de preço do banco de dados. Se o banco de dados estiver em um pool elástico, retornará **ElasticPool**.<br /><br /> Na camada **básica** , retorna **Basic**.<br /><br /> O **banco de dados individual em uma camada de serviço Standard** retorna um dos seguintes: S0, S1, S2, S3, S4, S6, S7, S9 ou S12.<br /><br /> **Um banco de dados individual em uma camada Premium** retorna do seguinte: P1, P2, P4, P6, P11 ou P15.<br /><br /> **SQL data warehouse** retorna DW100 por meio de DW30000c.<br /><br /> Para obter detalhes, consulte bancos de dados [individuais](/azure/sql-database/sql-database-dtu-resource-limits-single-databases/), [pools elásticos](/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools/)e [data warehouses](/azure/sql-data-warehouse/what-is-a-data-warehouse-unit-dwu-cdwu/)|  
|elastic_pool_name|sysname|O nome do [pool elástico](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/) ao qual o banco de dados pertence. Retornará **NULL** se o banco de dados for um banco de dados individual ou um data warehouse.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **dbManager** no banco de dados mestre.  No nível do banco de dados, o usuário deve ser o criador ou proprietário.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo pode ser executado no banco de dados mestre ou em bancos de dados de usuário do banco de dados SQL do Azure. A consulta retorna o nome, o serviço e as informações do nível de desempenho dos bancos de dados.  
  
```sql  
SELECT  d.name,   
     slo.*    
FROM sys.databases d   
JOIN sys.database_service_objectives slo    
ON d.database_id = slo.database_id;  
  
```  
  
  
