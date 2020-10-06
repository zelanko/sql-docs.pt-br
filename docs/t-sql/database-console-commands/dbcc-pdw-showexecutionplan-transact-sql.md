---
description: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.technology: data-warehouse
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 67eea4a666519ec5a9dd1dce7e1e33e3c8da4831
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91722351"
---
# <a name="dbcc-pdw_showexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Exibe o plano de execução do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma consulta em execução em um nó de computação ou em um nó de controle específico do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use isso para solucionar problemas de desempenho de consulta enquanto as consultas estiverem sendo executadas em nós de computação e no nó de controle.
  
Depois que forem esclarecidos os problemas de desempenho das consultas de SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução nos nós de computação, haverá várias maneiras de melhorar o desempenho. Algumas possíveis maneiras de melhorar o desempenho da consulta nos nós de computação incluem a criação de estatísticas de várias colunas, a criação de índices não clusterizados ou o uso de dicas de consulta.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
Sintaxe para [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]:

```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[ ; ]  
```  

Sintaxe para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:
  
```syntaxsql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[ ; ]  
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>Argumentos  
 *distribution_id*  
 Identificador da distribuição que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. O valor deve estar entre 1 e 60. Usado ao direcionar ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificador do nó que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. Usado ao direcionar a um dispositivo.  
  
 *spid*  
 Identificador da sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Requer a permissão VIEW-SERVER-STATE no dispositivo.
  
## <a name="examples-sssdw"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdw_showexecutionplan-basic-syntax"></a>a. Sintaxe básica do DBCC PDW_SHOWEXECUTIONPLAN  
 Quando estiver executando em uma instância do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], modifique a consulta acima para também selecionar a distribution_id.  
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status], [distribution_id]  
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
order by request_id, [dms_step_index];  
```  
  
Isso retornará o spid de cada distribuição em execução ativa. Se você ficou curioso para saber o que a distribuição 1 estava executando na sessão 375, execute o seguinte comando.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 1, 375 );  
```  

## <a name="examples-sspdw"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdw_showexecutionplan-basic-syntax"></a>B. Sintaxe básica do DBCC PDW_SHOWEXECUTIONPLAN  
 A consulta que está em uma execução muito longa está executando uma operação de plano de consulta do DMS ou uma operação de plano de consulta do SQL.  
  
Se a consulta estiver executando uma operação de plano de consulta do DMS, use a consulta a seguir para recuperar uma lista de IDs de nó e de IDs de sessão para as etapas que não estão completas.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
ORDER BY request_id, [dms_step_index], [distribution_id];  
```  
  
Com base nos resultados da consulta anterior, use sql_spid e pdw_node_id como parâmetros para DBCC PDW_SHOWEXECUTIONPLAN. Por exemplo, o comando a seguir mostra o plano de execução para pdw_node_id 201001 e sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Confira também

- [DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
- [DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
