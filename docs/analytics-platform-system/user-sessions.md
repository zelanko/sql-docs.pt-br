---
title: Sessões de usuário no Analytics Platform System | Microsoft Docs"
description: Sessões de usuário no Analytics Platform System Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 33bf052e27640ee08784927351579378bffbec2b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63316355"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sessões de usuário no Analytics Platform System
Um logon com as permissões apropriadas pode gerenciar as sessões de todos os logons em um dispositivo de PDW do SQL Server, incluindo executar estas ações:  
  
-   Exibir as sessões atuais no dispositivo, incluindo sessões ativas e ociosas.  
  
-   Exiba as consultas recentes e Active Directory para uma sessão.  
  
-   Encerrar sessões do Active Directory.  
  
Essas ações podem ser executadas usando o [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md) ou [exibições do sistema](tsql-system-views.md) por meio de comandos SQL, conforme mostrado abaixo.  
  
As permissões necessárias para gerenciar sessões, usando qualquer um dos métodos são os mesmos e são descritas em [conceder permissões para gerenciar logons, usuários e funções de banco de dados](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Gerenciar sessões usando o Console de administração  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Para exibir as sessões atuais, usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  A lista resultante exibe todas as sessões mais recentes. Para exibir apenas as sessões 'Active' ou 'Ociosa', clique o **Status** cabeçalho de coluna para classificar os resultados por status.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Para exibir consultas recentes e Active Directory para uma sessão usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Na lista de resultados, clique a ID de sessão da sessão desejada.  
  
3.  A lista de consultas resultante mostra as consultas recentes para a sessão. Para obter informações sobre como exibir detalhes da consulta, consulte [monitorando consultas ativas](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Para encerrar sessões usando o Console de administração  
  
1.  No menu superior, clique em **sessões**.  
  
2.  Encontre a ID de sessão para a sessão para cancelar.  
  
3.  Clique em vermelha **X** à esquerda da ID da sessão para encerrar a sessão. Apenas sessões com um status de 'Active' ou 'Ociosa' terá um vermelho **X**; somente essas sessões podem ser encerradas.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Gerenciar sessões usando exibições do sistema e comandos SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Para exibir as sessões atuais usando exibições do sistema  
Use [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) para gerar uma lista de sessões atuais.  
  
Este exemplo retorna a session_id login_name e o status de todas as sessões com um status de 'Active' ou 'Ociosa'.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Exibir consultas recentes e Active Directory para uma sessão por meio de exibições do sistema  
Para ver as consultas ativas e concluídas recentemente associadas a uma sessão, você deve usar o [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) e [DM pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) modos de exibição. Essa consulta retorna uma lista de todas as sessões ativas ou ociosas, além de todas as consultas ativas ou recentes associadas com cada ID de sessão.  
  
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
Use o [KILL](../t-sql/language-elements/kill-transact-sql.md) comando para encerrar uma sessão atual. Será necessário a ID de sessão para o processo seja finalizado, o que pode ser obtido usando o [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) modo de exibição.  
  
Neste exemplo, selecione o login_name, session_id e valores de status para encontrar uma sessão com base no nome do logon.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
Sessões com um status 'Active' ou 'Ociosa' podem ser encerradas usando o comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
