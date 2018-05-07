---
title: sp_notify_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_notify_operator_TSQL
- sp_notify_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_notify_operator
ms.assetid: c440f5c9-9884-4196-b07c-55d87afb17c3
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07c05c67f0b4e199ad096d8f2a5f12951e46178
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spnotifyoperator-transact-sql"></a>sp_notify_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Envia uma mensagem de email a um operador usando o Database Mail.  
  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@profile_name=** ] **'***profilename***'**  
 O nome do perfil do Database Mail a ser usado para enviar a mensagem. *ProfileName* é **nvarchar (128)**. Se *profilename* não for especificado, o perfil de email de banco de dados padrão será usado.  
  
 [ **@id=** ] *id*  
 O identificador do operador para envio da mensagem. *ID* é **int**, com um padrão NULL. Um dos *id* ou *nome* deve ser especificado.  
  
 [ **@name=** ] **'***name***'**  
 O nome do operador para o qual enviar a mensagem. *nome* é **nvarchar (128)**, com um padrão NULL. Um dos *id* ou *nome* deve ser especificado.  
  
> **Observação:** um endereço de email deve ser definido para o operador antes de poder receber mensagens.  
  
 [  **@subject=** ] **'***assunto***'**  
 O assunto da mensagem de email. *entidade* é **nvarchar (256)** sem nenhum padrão.  
  
 [  **@body=** ] **'***mensagem***'**  
 O corpo da mensagem de email. *mensagem* é **nvarchar (max)** sem nenhum padrão.  
  
 [ **@file_attachments=** ] **'***attachment***'**  
 O nome de um arquivo a ser anexado à mensagem de email. *anexo* é **nvarchar (512)**, sem padrão.  
  
 [ **@mail_database=** ] **'***mail_host_database***'**  
 Especifica o nome do banco de dados host de email. *mail_host_database* é **nvarchar (128)**. Se nenhum *mail_host_database* for especificado, o **msdb** banco de dados é usado por padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Envia a mensagem especificada ao endereço de email do operador especificado. Se o operador não tiver nenhum endereço de email configurado, retornará um erro.  
  
 O Database Mail e um banco de dados host de email devem ser configurados para que uma notificação possa ser enviada a um operador.  
  
## <a name="permissions"></a>Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem executar este procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Para obter detalhes sobre as permissões dessas funções, consulte [Funções de banco de dados fixas do SQL Server Agent](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)  
  
  
