---
description: sysmail_update_profile_sp (Transact-SQL)
title: sysmail_update_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profile_sp
- sysmail_update_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profile_sp
ms.assetid: eaedf7ce-a8d5-4ab9-99e0-d77d5be19e90
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 78a123514e990499f191cbc6742870647adebc5e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454732"
---
# <a name="sysmail_update_profile_sp-transact-sql"></a>sysmail_update_profile_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera a descrição ou o nome de um perfil do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_update_profile_sp [ [ @profile_id = ] profile_id , ] [ [ @profile_name = ] 'profile_name' , ]  
    [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @profile_id = ] profile_id` A ID do perfil a ser atualizada. *profile_id* é **int**, com um padrão de NULL. Pelo menos um dos *profile_id* ou *profile_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome do perfil.  
  
`[ @profile_name = ] 'profile_name'` O nome do perfil a ser atualizado ou o novo nome do perfil. *profile_name* é **sysname**, com um padrão de NULL. Pelo menos um dos *profile_id* ou *profile_name* deve ser especificado. Se ambos forem especificados, o procedimento alterará o nome do perfil.  
  
`[ @description = ] 'description'` A nova descrição para o perfil. a *Descrição* é **nvarchar (256)**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando a ID de perfil e o nome de perfil são especificados, o procedimento altera o nome do perfil para o nome fornecido e atualiza a descrição para o perfil. Quando somente um desses argumentos é fornecido, o procedimento atualiza a descrição para o perfil.  
  
 O procedimento armazenado **sysmail_update_profile_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser executado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 **A. Alterando a descrição de um perfil**  
  
 O exemplo a seguir altera a descrição para o perfil nomeado `AdventureWorks Administrator` no banco de dados **msdb** .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail objetos de configuração](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [Criar uma conta de Database Mail](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
