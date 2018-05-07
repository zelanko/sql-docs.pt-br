---
title: sysmail_help_profile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4aa2e8bb227da4fdb3305c96de0be04cd4a877ea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações sobre um ou mais perfis de email.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@profile_id** =] *profile_id*  
 A id do perfil do qual retornar informações. *profile_id* é **int**, com um padrão NULL.  
  
 [ **@profile_name** =] **'***profile_name***'**  
 O nome do perfil do qual retornar informações. *profile_name* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna um conjunto de resultados com as seguintes colunas.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Description|  
|**profile_id**|**Int**|A ID de perfil para o perfil.|  
|**name**|**sysname**|O nome de perfil para o perfil.|  
|**Descrição**|**nvarchar(256)**|A descrição para o perfil.|  
  
## <a name="remarks"></a>Remarks  
 Quando for especificado um nome de perfil ou a id do perfil, **sysmail_help_profile_sp** retorna informações sobre esse perfil. Caso contrário, **sysmail_help_profile_sp** retorna informações sobre cada perfil na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.  
  
 O procedimento armazenado **sysmail_help_profile_sp** está no **msdb** banco de dados e pertence a **dbo** esquema. O procedimento deve ser executado com um nome de três partes se o banco de dados atual não é **msdb**.  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para esse procedimento usam como padrão membros do **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 **A. Listando todos os perfis**  
  
 O exemplo a seguir mostra a lista de todos os perfis na instância.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 Conjunto de resultados de exemplo, reformatado para comprimento de linha:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B. Listando um perfil específico**  
  
 O exemplo a seguir mostra as informações de listagem para o perfil `AdventureWorks Administrator`.  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 Conjunto de resultados de exemplo, reformatado para comprimento de linha:  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>Consulte também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Procedimentos armazenados do Database Mail &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
