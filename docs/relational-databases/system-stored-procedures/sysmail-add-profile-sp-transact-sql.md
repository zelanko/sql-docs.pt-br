---
title: sysmail_add_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-non-specified
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
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6295b1f239f136c43e00e047186ce408ab9a4a93
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@profile_name** = ] **'***profile_name***'**  
 O nome para o novo perfil. *profile_name* é **sysname**, sem padrão.  
  
 [ **@description** =] **'***descrição***'**  
 A descrição opcional para o novo perfil. *Descrição* é **nvarchar (256)**, sem padrão.  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 Retorna a ID para o novo perfil. *new_profile_id* é **int**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Um perfil Database Mail contém qualquer número de contas do Database Mail. Os procedimentos armazenados do Database Mail podem se referir a um perfil por meio do nome do perfil ou da identificação do perfil gerada por este procedimento. Para obter mais informações sobre como adicionar uma conta a um perfil, consulte [sysmail_add_profileaccount_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md).  
  
 O nome do perfil e a descrição podem ser alterados com o procedimento armazenado **sysmail_update_profile_sp**, enquanto a id do perfil permanece constante durante a vida útil do perfil.  
  
 O nome de perfil deve ser exclusivo para o Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], caso contrário o procedimento armazenado retornará um erro.  
  
 O procedimento armazenado **sysmail_add_profile_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Criando um novo perfil**  
  
 O exemplo a seguir cria um novo perfil do Database Mail chamado `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B. Criando um novo perfil, salvando a identificação do perfil em uma variável**  
  
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
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
