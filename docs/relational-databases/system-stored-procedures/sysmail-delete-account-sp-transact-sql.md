---
title: sysmail_delete_account_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_account_sp
- sysmail_delete_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_account_sp
ms.assetid: 2adcac78-4a4a-407e-9666-1d9c43c73cc2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4b6adc5f6c02eae49a5f5e2598c6b02e5b00534e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70211267"
---
# <a name="sysmail_delete_account_sp-transact-sql"></a>sysmail_delete_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Exclui uma conta SMTP do Database Mail. Você também pode usar o Assistente para Configuração do Database Mail a fim de excluir uma conta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_delete_account_sp { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @account_id = ] account_id`O número de ID da conta a ser excluída. *account_id* é **int**, sem padrão. O *account_id* ou *account_name* deve ser especificado.  
  
`[ @account_name = ] 'account_name'`O nome da conta a ser excluída. *account_name* é **sysname**, sem padrão. O *account_id* ou *account_name* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Este procedimento exclui a conta especificada, independentemente de a conta estar em uso por um perfil. Um perfil que não contém nenhuma conta não pode enviar email com êxito.  
  
 O procedimento armazenado **sysmail_delete_account_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a exclusão da conta do Database Mail denominada `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_delete_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [&#41;&#40;Transact-SQL de sysmail_add_account_sp](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_delete_profile_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profile-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_delete_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-delete-profileaccount-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_help_account_sp](../../relational-databases/system-stored-procedures/sysmail-help-account-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_help_profile_sp](../../relational-databases/system-stored-procedures/sysmail-help-profile-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_help_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-help-profileaccount-sp-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sysmail_update_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md)  
  
  
