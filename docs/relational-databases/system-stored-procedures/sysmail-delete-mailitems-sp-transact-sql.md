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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9619ee410e0df014961e9f46a7e536508e0616c1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85639491"
---
# <a name="sysmail_delete_mailitems_sp-transact-sql"></a>sysmail_delete_mailitems_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Exclui permanentemente mensagens de email das tabelas internas do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_mailitems_sp  [ [ @sent_before = ] 'sent_before' ]  
    [ , [ @sent_status = ] 'sent_status' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ \@sent_before = ] 'sent_before'`Exclui emails até a data e a hora fornecidas como o argumento de *sent_before* . *sent_before* é **DateTime** com NULL como padrão. NULL indica todas as datas.  
  
`[ \@sent_status = ] 'sent_status'`Exclui emails do tipo especificado por *sent_status*. *sent_status* é **varchar (8)** sem padrão. As entradas válidas são **enviadas**, não **enviadas**, **repetidas**e **com falha**. NULL indica todos os status.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Database Mail mensagens e seus anexos são armazenados no banco de dados **msdb** . As mensagens devem ser excluídas periodicamente para evitar que o **msdb** cresça mais do que o esperado e para estar em conformidade com o programa de retenção de documentos de suas organizações. Use o procedimento armazenado **sysmail_delete_mailitems_sp** para excluir permanentemente mensagens de email das tabelas Database Mail. Um argumento opcional permite excluir somente os emails mais antigos fornecendo uma data e hora. Os emails mais antigos que o argumento serão excluídos. Outro argumento opcional permite excluir somente emails de um determinado tipo, especificado como o argumento de **sent_status** . Você deve fornecer um argumento para ** \@ sent_before** ou ** \@ sent_status**. Para excluir todas as mensagens, use ** \@ sent_before = GETDATE ()**.  
  
 A exclusão de email também exclui anexos relacionados a essas mensagens. Excluir emails não exclui as entradas correspondentes no **sysmail_event_log**. Use [sysmail_delete_log_sp](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md) para excluir itens do log.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, esse procedimento armazenado é concedido para execução de membros da função de servidor fixa **sysadmin** e **DatabaseMailUserRole**. Os membros da função de servidor fixa **sysadmin** podem executar este procedimento para excluir emails enviados por todos os usuários. Os membros de **DatabaseMailUserRole** só podem excluir emails enviados por esse usuário.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-deleting-all-e-mails"></a>a. Excluindo todos os emails  
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
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sysmail_allitems](../../relational-databases/system-catalog-views/sysmail-allitems-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_event_log](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_mailattachments](../../relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql.md)   
 [Criar um trabalho do SQL Server Agent para arquivar mensagens do Database Mail e logs de eventos](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)  
  
  
