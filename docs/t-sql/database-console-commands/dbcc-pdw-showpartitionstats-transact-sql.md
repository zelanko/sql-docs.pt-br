---
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 8d53158198b2df5ae5aaa0fbc3b176bdcd544367
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/09/2019
ms.locfileid: "57684907"
---
# <a name="dbcc-pdwshowpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o tamanho e o número de linhas de cada partição de uma tabela em um banco de dados do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
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
Este conjunto é composto pelos resultados do comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|partition_number|INT|Número da partição.|  
|used_page_count|BIGINT|Número de páginas usadas para os dados.|  
|reserved_page_count|BIGINT|Número de páginas reservadas para a partição.|  
|row_count|BIGINT|Número de linhas na partição.|  
|pdw_node_id|INT|Nó de computação dos dados.|  
|distribution_id|INT|Identificador de distribuição para os dados.|  
  
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
 