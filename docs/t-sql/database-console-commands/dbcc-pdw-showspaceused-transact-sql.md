---
title: DBCC PDW_SHOWSPACEUSED (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: f8c5d7ac822546d8334f1a174684f35733d9571b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68116490"
---
# <a name="dbcc-pdw_showspaceused-transact-sql"></a>DBCC PDW_SHOWSPACEUSED (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o número de linhas, o espaço em disco reservado e o espaço em disco usado para uma tabela específica ou para todas as tabelas em um banco de dados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
-- Show the space used for all user tables and system tables in the current database  
DBCC PDW_SHOWSPACEUSED  
[;]  
  
-- Show the space used for a table  
DBCC PDW_SHOWSPACEUSED ( " [ database_name . [ schema_name ] . ] | [ schema_name .] table_name  " )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 O nome de uma, duas ou três partes da tabela a ser exibido. Para nomes de tabela de duas partes, o nome precisa ser colocado entre aspas duplas (""). O uso de aspas para um nome de tabela de uma única parte é opcional. Quando nenhum nome de tabela for especificado, as informações serão exibidas para o banco de dados atual.  
  
## <a name="permissions"></a>Permissões  
Requer a permissão VIEW SERVER STAT.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Este é o conjunto de resultados de todas as tabelas.
  
|Coluna|Tipo de Dados|DESCRIÇÃO|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|Espaço total usado para o banco de dados, em KB.|  
|data_space|BIGINT|Espaço usado para dados, em KB.|  
|index_space|BIGINT|Espaço usado para índices, em KB.|  
|unused_space|BIGINT|O espaço que faz parte do espaço reservado e não é usado, em KB.|  
|pdw_node_id|INT|O nó de computação que está sendo usado para os dados.|  
  
Este é o conjunto de resultados de uma tabela.
  
|Coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|------------|---------------|-----------------|-----------|  
|rows|BIGINT|Número de linhas.||  
|reserved_space|BIGINT|Espaço reservado total para o objeto, em KB.||  
|data_space|BIGINT|Espaço usado para os dados, em KB.||  
|index_space|BIGINT|Espaço usado para índices, em KB.||  
|unused_space|BIGINT|O espaço que faz parte do espaço reservado e não é usado, em KB.||  
|pdw_node_id|INT|O nó de computação que é usado para relatar o uso do espaço.||  
|distribution_id|INT|A distribuição que é usada para relatar o uso do espaço.|O valor é -1 para tabelas replicadas.|  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showspaceused-basic-syntax"></a>a. Sintaxe básica do DBCC PDW_SHOWSPACEUSED  
Os exemplos a seguir mostram várias maneiras de exibir o número de linhas, o espaço em disco reservado e o espaço em disco usado pela tabela FactInternetSales no banco de dados [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012.dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "AdventureWorksPDW2012..FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( "dbo.FactInternetSales" );  
DBCC PDW_SHOWSPACEUSED ( FactInternetSales );  
```  
  
### <a name="b-show-the-disk-space-used-by-all-tables-in-the-current-database"></a>B. Mostrar o espaço em disco usado por todas as tabelas no banco de dados atual  
 O exemplo a seguir mostra o espaço em disco reservado e usado por todas as tabelas de usuário e tabelas do sistema no banco de dados [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```sql
-- Uses AdventureWorks  
  
DBCC PDW_SHOWSPACEUSED;  
```  
 ## <a name="see-also"></a>Confira também
[DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)

  
