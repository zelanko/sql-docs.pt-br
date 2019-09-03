---
title: sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: stevestein
ms.author: sstein
ms.openlocfilehash: a4bd7f90688d61f9ecee487d553393e38bed82e3
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211274"
---
# <a name="sysmail_add_profile_sp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Cria um novo perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_name = ] 'profile\_name'`O nome do novo perfil. o profile_name é **sysname**, sem padrão.  
 
   > [!NOTE]
   > O nome do perfil que usa o Azure SQL Instância Gerenciada SQL Agent deve ser chamado **AzureManagedInstance_dbmail_profile**
  
`[ @description = ] 'description'`A descrição opcional para o novo perfil. a *Descrição* é **nvarchar (256)** , sem padrão.  
  
`[ @profile_id = ] _new\_profile\_id OUTPUT`Retorna a ID do novo perfil. *new_profile_id* é **int**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Um perfil Database Mail contém qualquer número de contas do Database Mail. Os procedimentos armazenados do Database Mail podem se referir a um perfil por meio do nome do perfil ou da identificação do perfil gerada por este procedimento. Para obter mais informações sobre como adicionar uma conta a um perfil, consulte [Transact &#40;-&#41;SQL sysmail_add_profileaccount_sp](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 O nome do perfil e a descrição podem ser alterados com o procedimento armazenado **sysmail_update_profile_sp**, enquanto a ID do perfil permanece constante durante a vida útil do perfil.  
  
 O nome de perfil deve ser exclusivo para o Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], caso contrário o procedimento armazenado retornará um erro.  
  
 O procedimento armazenado **sysmail_add_profile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Criando um novo perfil**  
  
 O exemplo a seguir cria um novo perfil do Database Mail chamado `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. Criando um novo perfil, salvando a ID do perfil em uma variável**  
  
 O exemplo a seguir cria um novo perfil do Database Mail chamado `AdventureWorks Administrator`. O exemplo armazena o número da identificação do perfil na variável `@profileId` e retorna um conjunto de resultados contendo o número de identificação do perfil para o novo perfil.  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Database Mail procedimentos &#40;armazenados TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
