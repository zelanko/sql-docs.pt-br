---
title: Verificar o status de mensagens de email enviadas com o Database Mail | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- e-mail [SQL Server], status information
- mail [SQL Server], status information
- Database Mail [SQL Server], message status
- status information [Database Mail]
ms.assetid: eb290f24-b52f-46bc-84eb-595afee6a5f3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73d0cf3a374a7f3dda7797238d2c1702360aa955
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62872320"
---
# <a name="check-the-status-of-e-mail-messages-sent-with-database-mail"></a>Verificar o status de mensagens de email enviadas por Database Mail
  Este tópico descreve como verificar o status da mensagem de email enviada usando o Database no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] com [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  
  
-   **Para exibir o status do email enviado usando Database Mail, usando:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 O Database Mail mantém cópias das mensagens de email enviadas, que podem ser visualizadas nas exibições **sysmail_allitems**, **sysmail_sentitems**, **sysmail_unsentitems**e **sysmail_faileditems** do banco de dados **msdb** . O programa externo do Database Mail registra a atividade e exibe o log por meio do Log de Eventos de Aplicativos do Windows e da exibição **sysmail_event_log** do banco de dados **msdb** . Para verificar o status de uma mensagem de email, execute uma consulta para essa exibição. São quatro os status possíveis das mensagens de email: **sent**(enviada), **unsent**(não enviada), **retrying**(tentando novamente) e **failed**(falhou).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir o status do email enviado usando Database Mail**  
  
> [!NOTE]  
>  Para obter um exemplo desse procedimento, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
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
 [Registro em log e auditoria do Database Mail](database-mail-log-and-audits.md)  
  
  
