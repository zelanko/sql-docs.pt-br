---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9d1a4659deeab00589a09e66d885d7f7005f7a43
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o tamanho e o número de linhas para cada partição de uma tabela em uma [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*  
 A uma, duas ou três partes de nome da tabela a ser exibida.  Para duas ou nomes de tabela de três partes, o nome devem ser colocados entre aspas duplas (""). O uso de aspas ao redor de um nome de parte de uma tabela é opcional.  
  
## <a name="permissions"></a>Permissões
Requer **VIEW SERVER STATE** permissão.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Isso é que os resultados do comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|partition_number|int|Número da partição.|  
|used_page_count|bigint|Número de páginas usadas para os dados.|  
|reserved_page_count|bigint|Número de páginas alocadas para a partição.|  
|row_count|bigint|Número de linhas na partição.|  
|pdw_node_id|int|Compute o nó para os dados.|  
|distribution_id|int|Id de distribuição para os dados.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowpartitionstats-basic-syntax-examples"></a>A. Exemplos de sintaxe básica de DBCC PDW_SHOWPARTITIONSTATS  
Os exemplos a seguir exibem o espaço usado e o número de linhas por partição da tabela FactInternetSales o [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] banco de dados.
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  
## <a name="see-also"></a>Consulte também
[DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)  
  

