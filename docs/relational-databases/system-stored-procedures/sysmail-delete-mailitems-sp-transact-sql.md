---
title: sysmail_delete_mailitems_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_mailitems_sp_TSQL
- sysmail_delete_mailitems_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_mailitems_sp
ms.assetid: f87c9f4a-bda1-4bce-84b2-a055a3229ecd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c1e161a678b6834123aabf1eb5126445927a7fe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650765"
---
# <a name="sysmaildeletemailitemssp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui permanentemente mensagens de email das tabelas internas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@sent_before=** ] **'***sent_before***'**  
 Exclui emails até a data e hora fornecido como o *sent_before* argumento. *sent_before* está **datetime** com NULL como padrão. NULL indica todas as datas.  
  
 [ **@sent_status=** ] **'***sent_status***'**  
 Exclui emails do tipo especificado pelo *sent_status*. *sent_status* está **varchar(8)** sem nenhum padrão. As entradas válidas são **enviado**, **unsent**, **repetindo**, e **falha**. NULL indica todos os status.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Mensagens do Database Mail e seus anexos são armazenados na **msdb** banco de dados. As mensagens devem ser excluídas periodicamente para evitar **msdb** fique maior do que o esperado e para estar em conformidade com seu programa de retenção de documentos de organizações. Use o **sysmail_delete_mailitems_sp** procedimento armazenado para excluir permanentemente as mensagens de email das tabelas do Database Mail. Um argumento opcional permite excluir somente os emails mais antigos fornecendo uma data e hora. Os emails mais antigos que o argumento serão excluídos. Outro argumento opcional permite excluir somente os emails de um determinado tipo, especificado como o **sent_status** argumento. Você deve fornecer um argumento para **@sent_before** ou **@sent_status**. Para excluir todas as mensagens, use  **@sent_before = getDate ()**.  
  
 A exclusão de email também exclui anexos relacionados a essas mensagens. A exclusão de email não exclui as entradas correspondentes no **sysmail_event_log**. Use [sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) para excluir itens do log.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, esse procedimento armazenado é concedido para execução por membros desativar o **sysadmin** função de servidor fixa e **DatabaseMailUserRole**. Os membros de **sysadmin** função fixa de servidor pode executar este procedimento para excluir emails enviados por todos os usuários. Os membros **DatabaseMailUserRole** só pode excluir emails enviados por esse usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-all-e-mails"></a>A. Excluindo todos os emails  
 O exemplo a seguir exclui todos os emails do sistema do Database Mail.  
  
```  
DECLARE @GETDATE datetime  
SET @GETDATE = GETDATE();  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @GETDATE;  
GO  
```  
  
### <a name="b-deleting-the-oldest-e-mails"></a>B. Excluindo os emails mais antigos  
 O exemplo a seguir exclui os emails do Database Mail anteriores a `October 9, 2005`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_before = 'October 9, 2005' ;  
GO  
```  
  
### <a name="c-deleting-all-e-mails-of-a-certain-type"></a>C. Excluindo todos os emails de um determinado tipo  
 O exemplo a seguir exclui todos os emails que falharam do log do Database Mail.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_mailitems_sp   
    @sent_status = 'failed' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sysmail_allitems &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [sysmail_mailattachments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [Criar um trabalho do SQL Server Agent para arquivar mensagens e logs de eventos do Database Mail](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
