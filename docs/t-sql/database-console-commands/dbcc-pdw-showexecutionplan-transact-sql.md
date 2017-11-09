---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: 
ms.reviewer: 
ms.service: sql-data-warehouse
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
caps.latest.revision: 12
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 461ee87f41692172b31125e36553c0eab0b09772
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] plano de execução de uma consulta em execução em um determinado [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] nó ou controle de computação. Use isto para solucionar problemas de desempenho de consulta, enquanto as consultas são executadas em nós de computação e nó de controle.
  
Depois que os problemas de desempenho de consulta são entendidos para SMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consultas em execução em nós de computação, há várias maneiras para melhorar o desempenho. Possíveis maneiras de melhorar o desempenho de consulta em nós de computação incluem a criação de estatísticas de várias colunas, criar índices não clusterizados ou usando as dicas de consulta.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "ícone de link do tópico") [convenções de sintaxe do Transact-SQL &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
Sintaxe do SQL Server:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Sintaxe do Azure Parallel Data Warehouse:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *distribution_id*  
 Identificador de distribuição que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. Usada ao direcionar [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificador para o nó que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. Usada ao direcionar um dispositivo.  
  
 *SPID*  
 Identificador para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sessão que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL em [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Requer a permissão de servidor de modo de exibição de estado no dispositivo.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Exemplos:[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. Sintaxe básica de DBCC PDW_SHOWEXECUTIONPLAN  
 Quando executado em um [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] da instância, modifique a consulta acima para também selecionar a distribution_id.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Isso retornará o spid para executar cada ativamente a distribuição. Se você estivesse curioso sobre qual distribuição 1 estava em execução na sessão 375, você executaria o seguinte comando.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. Sintaxe básica de DBCC PDW_SHOWEXECUTIONPLAN  
 A consulta que está em execução muito longa é um DMS executando consulta de operação do plano ou uma operação de plano de consulta SQL.  
  
Se a consulta estiver executando uma operação DMS do plano de consulta, você pode usar a consulta a seguir para recuperar uma lista de IDs de nó e IDs de sessão para as etapas que não estão completas.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
Com base nos resultados da consulta anterior, use o sql_spid e pdw_node_id como parâmetros para DBCC PDW_SHOWEXEUCTIONPLAN. Por exemplo, o comando a seguir mostra o plano de execução para pdw_node_id 201001 e sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Consulte também
[DBCC PDW_SHOWPARTITIONSTATS &#40; Transact-SQL &#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40; Transact-SQL &#41;](dbcc-pdw-showspaceused-transact-sql.md)

