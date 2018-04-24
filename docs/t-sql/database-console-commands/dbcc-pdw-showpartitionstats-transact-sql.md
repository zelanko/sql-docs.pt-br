---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: t-sql|database-console-commands
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: b332ea733016fbbe1f6343cf024c3c5ef22088cc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o tamanho e o número de linhas de cada partição de uma tabela em um banco de dados do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *database_name* . [ *schema_name* ]. | *schema_name*. ] *table_name*  
 O nome de uma, duas ou três partes da tabela a ser exibido.  Para nomes de tabela de duas partes, o nome precisa ser colocado entre aspas duplas (""). O uso de aspas para um nome de tabela de uma única parte é opcional.  
  
## <a name="permissions"></a>Permissões
Requer a permissão **VIEW SERVER STATE**.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Estes são os resultados do comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|partition_number|INT|Número da partição.|  
|used_page_count|BIGINT|Número de páginas usadas para os dados.|  
|reserved_page_count|BIGINT|Número de páginas alocadas para a partição.|  
|row_count|BIGINT|Número de linhas na partição.|  
|pdw_node_id|INT|Nó de computação dos dados.|  
|distribution_id|INT|Id de distribuição dos dados.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. Exemplos de sintaxe básica do DBCC PDW_SHOWPARTITIONSTATS  
Os exemplos a seguir exibem o espaço usado e o número de linhas por partição da tabela FactInternetSales no banco de dados do [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>Confira também
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  
