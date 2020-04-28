---
title: sysmail_add_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profileaccount_sp
- sysmail_add_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profileaccount_sp
ms.assetid: 7cbf430f-1997-45ea-9707-0086184de744
author: stevestein
ms.author: sstein
ms.openlocfilehash: 11ada827add27ae2186fdcc565b3dd2f99f76452
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68017758"
---
# <a name="sysmail_add_profileaccount_sp-transact-sql"></a>sysmail_add_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma conta do Database Mail a um perfil do Database Mail. Execute **sysmail_add_profileaccount_sp** depois que uma conta de banco de dados for criada com [sysmail_add_account_sp &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sysmail-add-account-sp-transact-sql.md)e um perfil de banco de dados for criado com SYSMAIL_ADD_PROFILE_SP &#40;[Transact-SQL ](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)&#41;.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_profileaccount_sp { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
    [ , [ @sequence_number = ] sequence_number ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`A ID do perfil para adicionar a conta. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'`O nome do perfil ao qual adicionar a conta. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @account_id = ] account_id`A ID da conta a ser adicionada ao perfil. *account_id* é **int**, com um padrão de NULL. O *account_id* ou o *account_name* deve ser especificado.  
  
`[ @account_name = ] 'account_name'`O nome da conta a ser adicionada ao perfil. *account_name* é **sysname**, com um padrão de NULL. O *account_id* ou o *account_name* deve ser especificado.  
  
`[ @sequence_number = ] sequence_number`O número de sequência da conta no perfil. *sequence_number* é **int**, sem padrão. O número de sequência determina a ordem na qual as contas são usadas no perfil.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 O perfil e a conta já devem existir. Caso contrário, o procedimento armazenado retornará um erro.  
  
 Observe que este procedimento armazenado não altera o número de sequência de uma conta já associada ao perfil especificado. Para obter mais informações sobre como atualizar o número de sequência de uma conta, consulte [sysmail_update_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-update-profileaccount-sp-transact-sql.md).  
  
 O número de sequência determina a ordem na qual o Database Mail usa as contas no perfil. Para uma nova mensagem de email, o Database Mail inicia com a conta que tem o número de sequência mais baixo. Se essa conta falhar, o Database Mail usará a conta com o próximo número de sequência mais alto, e assim por diante, até que o Database Mail envie a mensagem com êxito ou a conta com o número de sequência mais alto falhe. Se a conta com o número de sequência mais alto falhar, o Database Mail pausará as tentativas de enviar o email pelo período de tempo configurado no parâmetro *AccountRetryDelay* de **sysmail_configure_sp**e, em seguida, iniciará o processo de tentar enviar o email novamente, começando pelo número de sequência mais baixo. Use o parâmetro *AccountRetryAttempts* de **sysmail_configure_sp**para configurar o número de vezes que o processo de email externo tenta enviar a mensagem de email usando cada conta no perfil especificado.  
  
 Se houver mais de uma conta com o mesmo número de sequência, Database Mail usará apenas uma dessas contas para uma determinada mensagem de email. Nesse caso, o Database Mail não pode garantir qual das contas será usada para o número de sequência em questão nem que a mesma conta seja usada em todas as mensagens.  
  
 O procedimento armazenado **sysmail_add_profileaccount_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir associa o perfil `AdventureWorks Administrator` à conta `Audit Account`. A conta de auditoria tem um número de sequência igual a 1.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account',  
    @sequence_number = 1 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
