---
title: sp_notify_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
author: stevestein
ms.author: sstein
ms.openlocfilehash: 74558320df59414a756e1655bb073e9bf0d7d73c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68107986"
---
# <a name="sp_notify_operator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envia uma mensagem de email a um operador usando o Database Mail.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_notify_operator  
    [ @profile_name = ] 'profilename' ,  
    [ @id = ] id ,  
    [ @name = ] 'name' ,  
    [ @subject = ] 'subject' ,  
    [ @body = ] 'message' ,  
    [ @file_attachments = ] 'attachment'  
    [ @mail_database = ] 'mail_host_database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profilename'`O nome do perfil de Database Mail a ser usado para enviar a mensagem. *ProfileName* é **nvarchar (128)**. Se *ProfileName* não for especificado, o perfil de Database Mail padrão será usado.  
  
`[ @id = ] id`O identificador para o operador para o qual enviar a mensagem. a *ID* é **int**, com um padrão de NULL. Um de *ID* ou *nome* deve ser especificado.  
  
`[ @name = ] 'name'`O nome do operador para o qual enviar a mensagem. o *nome* é **nvarchar (128)**, com um padrão de NULL. Um de *ID* ou *nome* deve ser especificado.  
  
> **Observação:** Um endereço de email deve ser definido para o operador antes que ele possa receber mensagens.  
  
`[ @subject = ] 'subject'`O assunto da mensagem de email. *Subject* é **nvarchar (256)** sem padrão.  
  
`[ @body = ] 'message'`O corpo da mensagem de email. a *mensagem* é **nvarchar (max)** sem padrão.  
  
`[ @file_attachments = ] 'attachment'`O nome de um arquivo a ser anexado à mensagem de email. o *anexo* é **nvarchar (512)**, sem padrão.  
  
`[ @mail_database = ] 'mail_host_database'`Especifica o nome do banco de dados do host de email. *mail_host_database* é **nvarchar (128)**. Se nenhum *mail_host_database* for especificado, o banco de dados **msdb** será usado por padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Envia a mensagem especificada ao endereço de email do operador especificado. Se o operador não tiver nenhum endereço de email configurado, retornará um erro.  
  
 O Database Mail e um banco de dados host de email devem ser configurados para que uma notificação possa ser enviada a um operador.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir envia um email de notificação ao operador `François Ajenstat` que usa o perfil do Database Mail `AdventureWorks Administrator` . O assunto do email é `Test Notification`. A mensagem de email contém a oração: "Este é um email de teste enviado pelo Database Mail".  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_notify_operator  
   @profile_name = N'AdventureWorks Administrator',  
   @name = N'François Ajenstat',  
   @subject = N'Test Notification',  
   @body = N'This is a test of notification via e-mail.' ;  
GO  
```  
  
## <a name="see-also"></a>Confira também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_add_operator](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_operator](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_delete_operator](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
