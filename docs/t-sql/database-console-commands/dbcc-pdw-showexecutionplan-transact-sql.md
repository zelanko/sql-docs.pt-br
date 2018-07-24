---
title: DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.suite: sql
ms.component: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: uc-msft
ms.author: umajay
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 83826259d76cbe27cad4451baed07221e6afed2c
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38052922"
---
# <a name="dbcc-pdwshowexecutionplan-transact-sql"></a>DBCC PDW_SHOWEXECUTIONPLAN (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

Exibe o plano de execução do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma consulta em execução em um nó de computação ou em um nó de controle específico do [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ou do [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Use isso para solucionar problemas de desempenho de consulta enquanto as consultas estiverem sendo executadas em nós de computação e no nó de controle.
  
Depois que forem esclarecidos os problemas de desempenho das consultas de SMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução nos nós de computação, haverá várias maneiras de melhorar o desempenho. Algumas possíveis maneiras de melhorar o desempenho da consulta nos nós de computação incluem a criação de estatísticas de várias colunas, a criação de índices não clusterizados ou o uso de dicas de consulta.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
Sintaxe do SQL Server:

```sql
DBCC PDW_SHOWEXECUTIONPLAN ( distribution_id, spid )  
[;]  
```  
Sintaxe do Parallel Data Warehouse do Azure:
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( pdw_node_id, spid )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *distribution_id*  
 Identificador da distribuição que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. Usado ao direcionar ao [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 *pdw_node_id*  
 Identificador do nó que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL. Usado ao direcionar a um dispositivo.  
  
 *spid*  
 Identificador da sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está executando o plano de consulta. Este é um número inteiro e não pode ser NULL.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
Requer a permissão VIEW-SERVER-STATE no dispositivo.
  
## <a name="examples-includesssdwincludessssdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
  
### <a name="a-dbcc-pdwshowexecutionplan-basic-syntax"></a>A. Sintaxe básica do DBCC PDW_SHOWEXECUTIONPLAN  
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

## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="b-dbcc-pdwshowexecutionplan-basic-syntax"></a>B. Sintaxe básica do DBCC PDW_SHOWEXECUTIONPLAN  
 A consulta que está em uma execução muito longa está executando uma operação de plano de consulta do DMS ou uma operação de plano de consulta do SQL.  
  
Se a consulta estiver executando uma operação de plano de consulta do DMS, use a consulta a seguir para recuperar uma lista de IDs de nó e de IDs de sessão para as etapas que não estão completas.
  
```sql
SELECT [sql_spid], [pdw_node_id], [request_id], [dms_step_index], [type], [start_time], [end_time], [status]   
FROM sys.dm_pdw_dms_workers   
WHERE [status] <> 'StepComplete' and [status] <> 'StepError'  
AND pdw_node_id = 201001   
order by request_id, [dms_step_index], [distribution_id];  
```  
  
Com base nos resultados da consulta anterior, use sql_spid e pdw_node_id como parâmetros para DBCC PDW_SHOWEXEUCTIONPLAN. Por exemplo, o comando a seguir mostra o plano de execução para pdw_node_id 201001 e sql_spid 375.
  
```sql
DBCC PDW_SHOWEXECUTIONPLAN ( 201001, 375 );  
```  

## <a name="see-also"></a>Confira também
[DBCC PDW_SHOWPARTITIONSTATS &#40;Transact-SQL&#41;](dbcc-pdw-showpartitionstats-transact-sql.md)  
[DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)
