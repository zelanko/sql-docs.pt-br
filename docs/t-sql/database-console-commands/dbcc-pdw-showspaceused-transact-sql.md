---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
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
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
caps.latest.revision: 10
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4a16d4a7a10eb4f36d0ead2a19f8e37d251e417f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o número de linhas, espaço em disco reservado e espaço em disco usado para uma tabela específica ou para todas as tabelas em um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ *database_name* . [ *schema_name* ]. | *schema_name* . ] *table_name*  
 A uma, duas ou três partes de nome da tabela a ser exibida. Para duas ou nomes de tabela de três partes, o nome devem ser colocados entre aspas duplas (""). O uso de aspas ao redor de um nome de parte de uma tabela é opcional. Quando nenhum nome de tabela for especificado, as informações são exibidas para o banco de dados atual.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão VIEW SERVER STAT.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Este é o conjunto de resultados de todas as tabelas.
  
|Coluna|Tipo de Dados|Description|  
|------------|---------------|-----------------|  
|reserved_space|bigint|Espaço total usado para o banco de dados, em KB.|  
|data_space|bigint|Espaço usado para dados, em KB.|  
|index_space|bigint|Espaço usado para índices, em KB.|  
|unused_space|bigint|Espaço que faz parte do espaço reservado e não usado, em KB.|  
|pdw_node_id|int|Nó de computação que está sendo usado para os dados.|  
  
Este é o conjunto de resultados de uma tabela.
  
|Coluna|Tipo de Dados|Description|Intervalo|  
|------------|---------------|-----------------|-----------|  
|rows|bigint|Número de linhas.||  
|reserved_space|bigint|Total do espaço reservado para o objeto, em KB.||  
|data_space|bigint|Espaço usado para os dados, em KB.||  
|index_space|bigint|Espaço usado para índices, em KB.||  
|unused_space|bigint|Espaço que faz parte do espaço reservado e não usado, em KB.||  
|pdw_node_id|int|Nó de computação que é usado para relatar o uso do espaço.||  
|distribution_id|int|Distribuição que é usada para relatar o uso do espaço.|Valor é -1 para tabelas replicadas.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdwshowspaceused-basic-syntax"></a>A. Sintaxe básica de DBCC PDW_SHOWSPACEUSED  
Os exemplos a seguir mostram várias maneiras de exibir o número de linhas, o espaço reservado do disco e espaço em disco usado pela tabela FactInternetSales no [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] banco de dados.
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Mostrar o espaço em disco usado por todas as tabelas no banco de dados atual  
 O exemplo a seguir mostra o espaço em disco reservado e usado por todas as tabelas de usuário e tabelas do sistema no [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)] banco de dados.  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Consulte também
[DBCC PDW_SHOWEXECUTIONPLAN &#40; Transact-SQL &#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  

