---
title: sysmail_update_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: af6578c98acfdd9fe5dea664ecea4cf21aa74f85
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890804"
---
# <a name="sysmail_update_profileaccount_sp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Atualiza o número de sequência de uma conta dentro de um perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id`A ID de perfil do perfil a ser atualizado. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'`O nome do perfil do perfil a ser atualizado. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou o *profile_name* deve ser especificado.  
  
`[ @account_id = ] account_id`A ID da conta a ser atualizada. *account_id* é **int**, com um padrão de NULL. O *account_id* ou o *account_name* deve ser especificado.  
  
`[ @account_name = ] 'account_name'`O nome da conta a ser atualizada. *account_name* é **sysname**, com um padrão de NULL. O *account_id* ou o *account_name* deve ser especificado.  
  
`[ @sequence_number = ] sequence_number`O novo número de sequência para a conta. *sequence_number* é **int**, sem padrão. O número de sequência determina a ordem na qual as contas são usadas no perfil.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Retorna um erro se a conta especificada não estiver associada ao perfil especificado.  
  
 O número de sequência determina a ordem na qual o Database Mail usa as contas no perfil. Para uma nova mensagem de email, o Database Mail inicia com a conta que tem o número de sequência mais baixo. Se essa conta falhar, o Database Mail usará a conta com o próximo número de sequência mais alto, e assim por diante, até que o Database Mail envie a mensagem com êxito ou a conta com o número de sequência mais alto falhe. Se houver falha na conta com o número de sequência mais alto, a mensagem de email falhará.  
  
 Se existir mais de uma conta com o mesmo número de sequência, o Database Mail utilizará apenas uma delas para uma dada mensagem de email. Nesse caso, o Database Mail não pode garantir qual das contas será usada para o número de sequência em questão nem que a mesma conta seja usada em todas as mensagens.  
  
 O procedimento armazenado **sysmail_update_profileaccount_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o número de sequência da conta `Admin-BackupServer` dentro do perfil `AdventureWorks Administrator` no banco de dados **msdb** . Depois de executar este código, o número de sequência da conta será `3`, indicando que ela será tentada no caso das duas primeiras contas falharem.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
