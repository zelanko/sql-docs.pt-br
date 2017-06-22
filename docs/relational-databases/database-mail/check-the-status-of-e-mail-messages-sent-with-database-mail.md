---
title: Verificar o status de mensagens de email enviadas com o Database Mail | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- e-mail [SQL Server], status information
- mail [SQL Server], status information
- Database Mail [SQL Server], message status
- status information [Database Mail]
ms.assetid: eb290f24-b52f-46bc-84eb-595afee6a5f3
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 691f6b69f1921d6710eba29d85b9120f39a686c4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="check-the-status-of-e-mail-messages-sent-with-database-mail"></a>Verificar o status de mensagens de email enviadas por Database Mail
  Este tópico descreve como verificar o status da mensagem de email enviada usando o Database no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  
  
-   **Para exibir o status do email enviado usando o Database Mail, com:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 O Database Mail mantém cópias das mensagens de email enviadas, que podem ser visualizadas nas exibições **sysmail_allitems**, **sysmail_sentitems**, **sysmail_unsentitems**e **sysmail_faileditems** do banco de dados **msdb** . O programa externo do Database Mail registra a atividade e exibe o log por meio do Log de Eventos de Aplicativos do Windows e da exibição **sysmail_event_log** do banco de dados **msdb** . Para verificar o status de uma mensagem de email, execute uma consulta para essa exibição. São quatro os status possíveis das mensagens de email: **sent**(enviada), **unsent**(não enviada), **retrying**(tentando novamente) e **failed**(falhou).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 **Para exibir o status do email enviado usando Database Mail**  
  
1.  Selecione na tabela **sysmail_allitems** as mensagens de interesse, especificando-as por **mailitem_id** ou **sent_status**.  
  
2.  Para verificar o status retornado pelo programa externo para as mensagens de email, una a exibição **sysmail_allitems** à exibição **sysmail_event_log** na coluna **mailitem_id** , como mostra a seção a seguir.  
  
     Por padrão, o programa externo não registra informações sobre mensagens enviadas com êxito. Para registrar todas as mensagens, defina o nível de log como detalhado na página **Configurar Parâmetros do Sistema** do **Assistente para Configuração do Database Mail**.  
  
###  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 O exemplo a seguir lista informações sobre todas as mensagens de email enviadas a `danw` que o programa externo não conseguiu enviar com êxito. A instrução lista o assunto, a data e a hora que o programa externo falhou em enviar a mensagem, além da mensagem de erro do log do Database Mail.  
  
```  
USE msdb ;  
GO  
  
-- Show the subject, the time that the mail item row was last  
-- modified, and the log information.  
-- Join sysmail_faileditems to sysmail_event_log   
-- on the mailitem_id column.  
-- In the WHERE clause list items where danw was in the recipients,  
-- copy_recipients, or blind_copy_recipients.  
-- These are the items that would have been sent  
-- to danw.  
  
SELECT items.subject,  
    items.last_mod_date  
    ,l.description FROM dbo.sysmail_faileditems as items  
INNER JOIN dbo.sysmail_event_log AS l  
    ON items.mailitem_id = l.mailitem_id  
WHERE items.recipients LIKE '%danw%'    
    OR items.copy_recipients LIKE '%danw%'   
    OR items.blind_copy_recipients LIKE '%danw%'  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Registro em log e auditoria do Database Mail](../../relational-databases/database-mail/database-mail-log-and-audits.md)  
  
  
