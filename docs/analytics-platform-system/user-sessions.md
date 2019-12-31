---
title: Sessões de usuário
description: Sessões de usuário na data warehouse paralela do sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74399404"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sessões de usuário no Analytics Platform System
Um logon com as permissões apropriadas pode gerenciar as sessões de todos os logons em um dispositivo SQL Server PDW, incluindo a execução dessas ações:  
  
-   Exiba as sessões atuais no dispositivo, incluindo sessões ativas e ociosas.  
  
-   Exibir as consultas ativas e recentes para uma sessão.  
  
-   Encerrar sessões ativas.  
  
Essas ações podem ser executadas usando o [Monitor do dispositivo usando o console de administração do](monitor-the-appliance-by-using-the-admin-console.md) ou [exibições do sistema](tsql-system-views.md) por meio de comandos SQL, conforme mostrado abaixo.  
  
As permissões necessárias para gerenciar sessões usando um dos métodos são as mesmas e são descritas em [conceder permissões para gerenciar logons, usuários e funções de banco de dados](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Gerenciar sessões usando o console de administração  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para exibir as sessões atuais usando o console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  A lista resultante exibe todas as sessões recentes. Para exibir somente sessões ' ativas ' ou ' ociosas ', clique no cabeçalho da coluna **status** para classificar os resultados por status.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para exibir consultas ativas e recentes para uma sessão usando o console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Na lista de resultados, clique na ID de sessão da sessão desejada.  
  
3.  A lista consultas resultantes mostra as consultas recentes para a sessão. Para obter informações sobre como exibir detalhes da consulta, consulte [monitorando consultas ativas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para encerrar sessões usando o console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Localize a ID de sessão da sessão a ser cancelada.  
  
3.  Clique no **X** vermelho à esquerda da ID da sessão para encerrar a sessão. Somente as sessões com status ' ativo ' ou ' ocioso ' terão um **X**vermelho; somente essas sessões podem ser encerradas.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Gerenciar sessões usando exibições do sistema e comandos SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para exibir sessões atuais usando exibições do sistema  
Use [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para gerar uma lista de sessões atuais.  
  
Este exemplo retorna o session_id, o login_name e o status de todas as sessões com o status ' ativo ' ou ' ocioso '.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Para exibir consultas ativas e recentes para uma sessão usando exibições do sistema  
Para ver as consultas ativas e recentemente concluídas associadas a uma sessão, use as exibições [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) e [Sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) . Essa consulta retorna uma lista de todas as sessões ativas ou ociosas, além de quaisquer consultas ativas ou recentes associadas a cada ID de sessão.  
  
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
Use o comando [Kill](../t-sql/language-elements/kill-transact-sql.md) para encerrar uma sessão atual. Você precisará da ID da sessão para que o processo seja encerrado, o que pode ser obtido usando a exibição [Sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) .  
  
Neste exemplo, selecione os valores de login_name, session_id e status para localizar uma sessão com base no nome de logon.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
As sessões com status ' ativo ' ou ' ocioso ' podem ser encerradas usando o comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
