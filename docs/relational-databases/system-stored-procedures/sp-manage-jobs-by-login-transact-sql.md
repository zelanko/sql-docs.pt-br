---
title: sp_manage_jobs_by_login (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_manage_jobs_by_login
- sp_manage_jobs_by_login_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_manage_jobs_by_login
ms.assetid: 832ec15a-6e92-4eb5-8c4a-af4dba79fbaa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0cd3573c108cdd5a57bbb2cf6d542415710f24c
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530258"
---
# <a name="spmanagejobsbylogin-transact-sql"></a>sp_manage_jobs_by_login (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui ou reatribui trabalhos pertencentes ao logon especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_manage_jobs_by_login  
     [ @action = ] 'action'  
     [, [@current_owner_login_name = ] 'current_owner_login_name']  
     [, [@new_owner_login_name = ] 'new_owner_login_name']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @action = ] 'action'` A ação a ser tomada para o logon especificado. *ação* está **varchar(10)**, sem padrão. Quando *ação*é **excluir**, **sp_manage_jobs_by_login** exclui todos os trabalhos pertencentes a *current_owner_login_name*. Quando *ação* é **REATRIBUIR**, todos os trabalhos são atribuídos a *new_owner_login_name*.  
  
`[ @current_owner_login_name = ] 'current_owner_login_name'` O nome de logon do proprietário do trabalho atual. *current_owner_login_name* está **sysname**, sem padrão.  
  
`[ @new_owner_login_name = ] 'new_owner_login_name'` O nome de logon do novo proprietário do trabalho. Use este parâmetro somente se *ação* é **REATRIBUIR**. *new_owner_login_name* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ter o **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir reatribui todos os trabalhos de `danw` para `françoisa`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_manage_jobs_by_login  
    @action = N'REASSIGN',  
    @current_owner_login_name = N'danw',  
    @new_owner_login_name = N'françoisa' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_delete_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-job-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
