---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 06091ffc26ea036a4a0bd7e30196545bcaca60d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936941"
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna o plano de execução para solicitações em andamento de consulta. Use essa DMV para recuperar o showplan XML estatísticas transitórias. 

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argumentos 
*session_id*  
 A id de sessão está executando o lote a ser pesquisado. *session_id* está **smallint**. *session_id* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou procedimento armazenado que a consulta faz parte. Anulável.|
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote que está sendo executado. Anulável.|
|query_plan|**xml**|Contém a representação de plano de execução do plano de execução de consulta que é especificado com o tempo de execução *plan_handle* que contém estatísticas parciais. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário. Anulável.|

## <a name="remarks"></a>Comentários
Essa função do sistema está disponível começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. Consulte o artigo [3190871](https://support.microsoft.com/en-us/help/3190871)

Essa função do sistema funciona em ambos **standard** e **leve** infraestrutura de criação de perfil de estatísticas de execução de consulta. Para obter mais informações, confira [Infraestrutura de Criação de Perfil de Consulta](../../relational-databases/performance/query-profiling-infrastructure.md).  

Sob as seguintes condições, nenhuma saída Showplan é retornada na **query_plan** coluna da tabela retornada para **DM exec_query_statistics_xml**:  
  
-   Se o plano de consulta que corresponde à especificada *session_id* não está em execução, o **query_plan** coluna da tabela retornada é nula. Por exemplo, essa condição pode ocorrer se houver um atraso entre quando o identificador de plano foi capturado e quando ele foi usado com **DM exec_query_statistics_xml**.  
    
Devido a uma limitação no número de níveis aninhados permitida na **xml** tipo de dados **DM exec_query_statistics_xml** não pode retornar planos de consulta que atendem ou excedem 128 níveis de elementos aninhados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condição evitava que o plano de consulta retornasse e gerasse um erro 6335. Na [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versões posteriores, o **query_plan** coluna retorna NULL.   

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. Observando as estatísticas de plano e execução de consulta ao vivo para um lote em execução  
 A exemplo a seguir consulta **. DM exec_requests** para localizar a consulta interessante e copiar seu `session_id` da saída.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Em seguida, para obter as estatísticas de plano e execução de consultas dinâmicas, use copiado `session_id` com a função do sistema **DM exec_query_statistics_xml**.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 Ou combinados para todas as solicitações em execução.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Consulte também
  [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Banco de dados relacionados a exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

