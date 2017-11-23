---
title: sys.dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords: sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
caps.latest.revision: "6"
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 051b93348547603d2e68a007ede531bfa73a6d58
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecquerystatisticsxml-transact-sql"></a>sys.dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Retorna o plano de execução para solicitações em andamento de consulta. Use essa DMV para recuperar o showplan XML estatísticas transitório. 

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argumentos 
*session_id*  
 A id de sessão está executando o lote a ser pesquisado. *session_id* é **smallint**. *session_id* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabela retornada
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|Mapa de hash do texto SQL da solicitação. Anulável.|
|plan_handle|**varbinary(64)**|Mapa de hash do plano de consulta. Anulável.|
|query_plan|**xml**|Showplan XML estatísticas parcial. Anulável.|

## <a name="remarks"></a>Comentários
Essa função de sistema está disponível desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1.

Essa função do sistema funciona em ambos **padrão** e **leve** infraestrutura de criação de perfil de estatísticas de execução de consulta.  
  
**Padrão** estatísticas de infraestrutura de criação de perfil podem ser habilitadas usando:
  -  [SET STATISTICS XML EM](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [DEFINIR O PERFIL DE ESTATÍSTICAS EM](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  o `query_post_execution_showplan` eventos estendidos.  
  
**Lightweight** estatísticas de infraestrutura de criação de perfil estão disponível em [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e pode ser habilitado:
  -  Globalmente usando rastreamento sinalizador 7412.
  -  Usando o [ *query_thread_profile* ](http://support.microsoft.com/kb/3170113) eventos estendidos.
  
> [!NOTE]
> Uma vez habilitada, o sinalizador de rastreamento 7412, criação de perfil leve será habilitada para qualquer consumidor das estatísticas de execução de consulta perfis de infraestrutura, em vez de padrão de criação de perfil, como o DMV [sys.DM exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).
> No entanto, a criação de perfil padrão ainda é usada para SET STATISTICS XML, *incluir plano real* ação [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], e `query_post_execution_showplan` xEvent.

> [!IMPORTANT]
> TPC-C como testes de carga de trabalho, permitindo que a infraestrutura de criação de perfil de estatísticas leve adiciona uma sobrecarga de 1,5 a 2 por cento. Por outro lado, a infraestrutura de criação de perfil de padrão de estatísticas pode adicionar até 90% de sobrecarga para o mesmo cenário de carga de trabalho.

## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE` no servidor.  

## <a name="examples"></a>Exemplos  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>A. Procurando nas estatísticas de plano e execução de consulta ao vivo de um lote em execução  
 A exemplo a seguir consulta **exec_requests** para localizar a consulta interessante e copiar seu `session_id` da saída.  
  
```t-sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Em seguida, para obter as estatísticas de plano e execução de consulta em tempo real, use copiado `session_id` com a função de sistema **sys.dm_exec_query_statistics_xml**.  
  
```t-sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 Ou combinado de todas as solicitações em execução.  
  
```t-sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Consulte também
  [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao &#40; do banco de dados Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

