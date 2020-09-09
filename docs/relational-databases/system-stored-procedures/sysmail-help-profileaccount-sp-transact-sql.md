---
description: sysmail_help_profileaccount_sp (Transact-SQL)
title: sysmail_help_profileaccount_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profileaccount_sp_TSQL
- sysmail_help_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profileaccount_sp
ms.assetid: 3ea68271-0a6b-4d77-991c-4757f48f747a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6894b44d7a09fa8f49ffa1d76a8613f930db7d18
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541039"
---
# <a name="sysmail_help_profileaccount_sp-transact-sql"></a>sysmail_help_profileaccount_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lista as contas associadas a um ou mais perfis do Database Mail.  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_profileaccount_sp  
   {   [ @profile_id = ] profile_id   
      | [ @profile_name = ] 'profile_name' }  
   [ , {   [ @account_id = ] account_id  
         | [ @account_name = ] 'account_name' } ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` É a ID do perfil a ser listada. *profile_id* é **int**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @profile_name = ] 'profile_name'` É o nome do perfil do perfil a ser listado. *profile_name* é **sysname**, com um padrão de NULL. O *profile_id* ou *profile_name* deve ser especificado.  
  
`[ @account_id = ] account_id` É a ID da conta a ser listada. *account_id* é **int**, com um padrão de NULL. Quando *account_id* e *account_name* são nulos, o lista todas as contas no perfil.  
  
`[ @account_name = ] 'account_name'` É o nome da conta a ser listada. *account_name* é **sysname**, com um padrão de NULL. Quando *account_id* e *account_name* são nulos, o lista todas as contas no perfil.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados com as seguintes colunas.  
  
| Nome da coluna | Tipo de dados | Descrição |
| ----------- | --------- | ----------- |
|**profile_id**|**int**|O ID do perfil.|  
|**profile_name**|**sysname**|O nome do perfil.|  
|**account_id**|**int**|A ID da conta.|  
|**account_name**|**sysname**|O nome da conta.|  
|**sequence_number**|**int**|O número de sequência da conta dentro do perfil.|  
  
## <a name="remarks"></a>Comentários  
 Quando nenhum *profile_id* ou *profile_name* é especificado, esse procedimento armazenado retorna informações para cada perfil na instância.  
  
 O procedimento armazenado **sysmail_help_profileaccount_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Listando as contas de um perfil específico por nome**  
  
 O exemplo a seguir mostra a lista de informações do perfil `AdventureWorks Administrator`, especificando o nome do perfil.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
   @profile_name = 'AdventureWorks Administrator';  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **B. Listando as contas de um perfil específico por ID de perfil**  
  
 O exemplo a seguir mostra a lista de informações do perfil `AdventureWorks Administrator`, especificando o ID do perfil.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp  
    @profile_id = 131 ;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
```  
  
 **C. Listando as contas de todos os perfis**  
  
 O exemplo a seguir mostra a lista de contas de todos os perfis na instância.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profileaccount_sp;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
profile_id  profile_name                 account_id  account_name         sequence_number  
----------- ---------------------------- ----------- -------------------- ---------------  
131         AdventureWorks Administrator 197         Admin-MainServer     1  
131         AdventureWorks Administrator 198         Admin-BackupServer   2  
106         AdventureWorks Operator      210         Operator-MainServer  1  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
