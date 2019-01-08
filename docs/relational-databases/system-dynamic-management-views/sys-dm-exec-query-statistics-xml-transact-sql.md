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
manager: craigg
ms.openlocfilehash: 99e51be32264dd90b126860b33abe35c7a27781a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819098"
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
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|Mapa de hash do texto SQL da solicitação. Anulável.|
|plan_handle|**varbinary(64)**|Mapa de hash do plano de consulta. Anulável.|
|query_plan|**xml**|Showplan XML estatísticas parcial. Anulável.|

## <a name="remarks"></a>Comentários
Essa função do sistema está disponível começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. Consulte o artigo [3190871](https://support.microsoft.com/en-us/help/3190871)

Essa função do sistema funciona em ambos **standard** e **leve** infraestrutura de criação de perfil de estatísticas de execução de consulta.  
  
**Padrão** infraestrutura de criação de perfil de estatísticas podem ser habilitadas usando:
  -  [SET STATISTICS XML EM](../../t-sql/statements/set-statistics-xml-transact-sql.md)
  -  [SET STATISTICS PROFILE EM](../../t-sql/statements/set-statistics-profile-transact-sql.md)
  -  o `query_post_execution_showplan` evento estendido.  
  
**Lightweight** infraestrutura de criação de perfil de estatísticas estão disponível em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e pode ser habilitado:
  -  Globalmente usando o rastreamento de sinalizador 7412.
  -  Usando o [ *query_thread_profile* ](https://support.microsoft.com/kb/3170113) evento estendido.
  
> [!NOTE]
> Uma vez habilitado pelo sinalizador de rastreamento 7412, criação de perfil leve será habilitada para qualquer consumidor das estatísticas de execução de consulta infraestrutura em vez de padrão de criação de perfil, como o DMV de criação de perfil [DM exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md).
> No entanto, a criação de perfil padrão ainda é usada para SET STATISTICS XML *incluir plano real* ação no [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], e `query_post_execution_showplan` xEvent.

> [!IMPORTANT]
> Em TPC-C, como testes de carga de trabalho, permitindo que a infraestrutura de criação de perfil de estatísticas leve adiciona uma sobrecarga de 1,5 a 2 por cento. Por outro lado, a infraestrutura de criação de perfil de padrão de estatísticas pode adicionar até 90% de sobrecarga para o mesmo cenário de carga de trabalho.

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

