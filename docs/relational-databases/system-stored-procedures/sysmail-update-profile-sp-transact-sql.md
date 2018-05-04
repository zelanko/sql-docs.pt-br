---
title: sysmail_update_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 48c40cfe3cacd262673e30dabbe89f20eea2de5b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysmailupdateprofilesp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera a descrição ou o nome de um perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@profile_id** =] *profile_id*  
 A id de perfil para atualizar. *profile_id* é **int**, com um padrão NULL. Pelo menos uma das *profile_id* ou *profile_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome do perfil.  
  
 [ **@profile_name** =] **'***profile_name***'**  
 O nome do perfil a ser atualizado ou o novo nome para o perfil. *profile_name* é **sysname**, com um padrão NULL. Pelo menos uma das *profile_id* ou *profile_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome do perfil.  
  
 [ **@description** =] **'***descrição***'**  
 A nova descrição do perfil. *Descrição* é **nvarchar (256)**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Quando a ID de perfil e o nome de perfil são especificados, o procedimento altera o nome do perfil para o nome fornecido e atualiza a descrição para o perfil. Quando somente um desses argumentos é fornecido, o procedimento atualiza a descrição para o perfil.  
  
 O procedimento armazenado **sysmail_update_profile_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Alterando a descrição de um perfil**  
  
 O exemplo a seguir altera a descrição para o perfil chamado `AdventureWorks Administrator` no **msdb** banco de dados.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@description = 'Administrative mail profile.';  
```  
  
 **B. Alterando o nome e a descrição de um perfil**  
  
 O exemplo a seguir altera o nome e a descrição do perfil com a ID de perfil `750`.  
  
```  
EXECUTE msdb.dbo.sysmail_update_profile_sp  
    @profile_id = 750  
    ,@profile_name = 'Operator'  
    ,@description = 'Profile to send alert e-mail to operators.';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Objetos de configuração do Database Mail](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Criar uma conta do Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
