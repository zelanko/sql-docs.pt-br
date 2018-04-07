---
title: Sessões de usuário (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0425cef2-de4d-4f42-91c5-cb1cd4bb1265
caps.latest.revision: 15
ms.openlocfilehash: 4ed0fab1fae1fe2d1a5a3ebb961d6c4d4747764f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="user-sessions"></a>Sessões de usuário
Um logon com as permissões adequadas pode gerenciar as sessões de todos os logons em um dispositivo de PDW do SQL Server, incluindo executar estas ações:  
  
-   Exibir as sessões atuais no dispositivo, incluindo sessões ativas e ociosas.  
  
-   Exiba as consultas ativas e recentes de uma sessão.  
  
-   Termine as sessões ativas.  
  
Essas ações podem ser executadas usando o [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md) ou [exibições do sistema](tsql-system-views.md) por meio de comandos SQL, conforme mostrado abaixo.  
  
As permissões necessárias para gerenciar sessões usando qualquer um dos métodos são os mesmos e são descritas na [conceder permissões para gerenciar logons, usuários e funções de banco de dados](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Gerenciar sessões usando o Console de administração  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para exibir as sessões atuais usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  A lista resultante exibe todas as sessões recentes. Para exibir apenas as sessões 'Active' ou 'Ocioso', clique o **Status** cabeçalho de coluna para classificar os resultados por status.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para exibir consultas ativas e recentes de uma sessão usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Na lista de resultados, clique a ID de sessão da sessão desejada.  
  
3.  A lista de consultas resultante mostra as consultas recentes para a sessão. Para obter informações sobre como exibir detalhes da consulta, consulte [monitoramento consultas ativas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para encerrar sessões usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Localize a ID de sessão para a sessão para cancelar.  
  
3.  Clique no vermelho **X** à esquerda da ID de sessão para encerrar a sessão. Somente as sessões com um status de 'Active' ou 'Ocioso' terá um vermelho **X**; somente essas sessões podem ser encerradas.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Gerenciar sessões usando comandos SQL e exibições do sistema  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para exibir as sessões atuais usando exibições do sistema  
Use [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para gerar uma lista de sessões atuais.  
  
Este exemplo retorna o status, login_name e a session_id para todas as sessões com um status de 'Active' ou 'Ocioso'.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Para exibir consultas ativas e recentes de uma sessão usando exibições do sistema  
Para ver as consultas de ativas e concluídas recentemente associadas a uma sessão, você deve usar o [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) e [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) modos de exibição. Esta consulta retorna uma lista de todas as sessões ativas ou ociosas, além de todas as consultas ativas ou recentes associadas a cada ID de sessão.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Para encerrar sessões usando comandos SQL  
Use o [KILL](../t-sql/language-elements/kill-transact-sql.md) comando para terminar uma sessão atual. Será necessário a ID de sessão para o processo seja finalizado, o que pode ser obtido usando o [sys.dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) exibição.  
  
Neste exemplo, selecione o login_name, session_id e valores de status para localizar uma sessão com base no nome de logon.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Sessões com um status 'Active' ou 'Ocioso' podem ser encerradas, usando o comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
