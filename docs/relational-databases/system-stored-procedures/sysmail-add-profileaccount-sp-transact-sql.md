---
title: sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8bbb10c196f00beb542ff917ed6e2df6bbbf9746
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysmailaddprofileaccountsp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma conta do Database Mail a um perfil do Database Mail. Executar **sysmail_add_profileaccount_sp** depois que uma conta de banco de dados é criada com [sysmail_add_account_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md), e um perfil de banco de dados é criado com [sysmail_add_profile_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@profile_id** =] *profile_id*  
 A ID do perfil no qual adicionar a conta. *profile_id* é **int**, com um padrão NULL. Ambos os *profile_id* ou o *profile_name* deve ser especificado.  
  
 [ **@profile_name** =] **'***profile_name***'**  
 O nome do perfil no qual adicionar a conta. *profile_name* é **sysname**, com um padrão NULL. Ambos os *profile_id* ou o *profile_name* deve ser especificado.  
  
 [ **@account_id** = ] *account_id*  
 A ID da conta a ser adicionada ao perfil. *account_id* é **int**, com um padrão NULL. Ambos o *account_id* ou *account_name* deve ser especificado.  
  
 [ **@account_name** = ] **'***account_name***'**  
 O nome da conta a ser adicionada ao perfil. *account_name* é **sysname**, com um padrão NULL. Ambos o *account_id* ou *account_name* deve ser especificado.  
  
 [ **@sequence_number** =] *sequence_number*  
 O número de sequência da conta dentro do perfil. *sequence_number* é **int**, sem padrão. O número de sequência determina a ordem na qual as contas são usadas no perfil.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 O perfil e a conta já devem existir. Caso contrário, o procedimento armazenado retornará um erro.  
  
 Observe que este procedimento armazenado não altera o número de sequência de uma conta já associada ao perfil especificado. Para obter mais informações sobre como atualizar o número de sequência de uma conta, consulte [sysmail_update_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md).  
  
 O número de sequência determina a ordem na qual o Database Mail usa as contas no perfil. Para uma nova mensagem de email, o Database Mail inicia com a conta que tem o número de sequência mais baixo. Se essa conta falhar, o Database Mail usará a conta com o próximo número de sequência mais alto, e assim por diante, até que o Database Mail envie a mensagem com êxito ou a conta com o número de sequência mais alto falhe. Se a conta com o número de sequência mais alto falhar, o Database Mail pausará as tentativas de enviar o email pelo período de tempo configurado no parâmetro *AccountRetryDelay* de **sysmail_configure_sp**e, em seguida, iniciará o processo de tentar enviar o email novamente, começando pelo número de sequência mais baixo. Use o parâmetro *AccountRetryAttempts* de **sysmail_configure_sp**para configurar o número de vezes que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado.  
  
 Se houver mais de uma conta com o mesmo número de sequência, o Database Mail só usará uma dessas contas para uma mensagem de email fornecido. Nesse caso, o Database Mail não pode garantir qual das contas será usada para o número de sequência em questão nem que a mesma conta seja usada em todas as mensagens.  
  
 O procedimento armazenado **sysmail_add_profileaccount_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir associa o perfil `AdventureWorks Administrator` à conta `Audit Account`. A conta de auditoria tem um número de sequência igual a 1.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
