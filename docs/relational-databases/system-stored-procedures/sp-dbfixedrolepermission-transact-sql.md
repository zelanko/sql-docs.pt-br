---
title: sp_dbfixedrolepermission (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbfixedrolepermission
- sp_dbfixedrolepermission_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbfixedrolepermission
ms.assetid: b8c30191-f532-49cd-83f3-c271f63ce572
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2a51fcc7108c7f6af6237d77cbad73c87ed7c6e6
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78180107"
---
# <a name="sp_dbfixedrolepermission-transact-sql"></a>sp_dbfixedrolepermission (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe as permissões de uma função de banco de dados fixa. **sp_dbfixedrolepermission** retorna informações corretas [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]no. A saída não reflete as alterações para a hierarquia de permissões que foram implementadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, consulte [funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md#fixed-database-roles), que mostram uma lista de funções de banco de dados fixas e suas permissões correspondentes.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbfixedrolepermission [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome de uma função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de banco de dados fixa válida. *role* é **sysname**, com um padrão de NULL. Se a *função* não for especificada, as permissões para todas as funções de banco de dados fixas serão exibidas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|Nome da função de banco de dados fixa|  
|**Permissão**|**nvarchar (70)**|Permissões associadas a **DbFixedRole**|  
  
## <a name="remarks"></a>Comentários  
 Para exibir uma lista das funções de banco de dados fixas, execute **sp_helpdbfixedrole**. A tabela a seguir mostra as funções de banco de dados fixas.  
  
|Função de banco de dados fixa|Descrição|  
|-------------------------|-----------------|  
|**db_owner**|Proprietários de banco de dados|  
|**db_accessadmin**|Administradores de acesso de banco de dados|  
|**db_securityadmin**|Administradores de segurança de banco de dados|  
|**db_ddladmin**|Administradores DDL (linguagem de definição de dados) de banco de dados|  
|**db_backupoperator**|Operadores de backup de banco de dados|  
|**db_datareader**|Leitores dos dados de banco de dados|  
|**db_datawriter**|Gravadores dos dados de banco de dados|  
|**db_denydatareader**|Leitores de negação dos dados de banco de dados|  
|**db_denydatawriter**|Gravadores de negação dos dados de banco de dados|  
  
 Os membros da função de banco de dados fixa **db_owner** têm as permissões de todas as outras funções de banco de dados fixas. Para exibir as permissões para funções de servidor fixas, execute **sp_srvrolepermission**.  
  
 O conjunto de resultados inclui as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que podem ser executadas, e outras atividades especiais que podem ser realizadas, por membros da função de banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir retorna as permissões para todas as funções de banco de dados porque não especifica uma função de banco de dados fixa.  
  
```  
EXEC sp_dbfixedrolepermission;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprolemember](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdbfixedrole](../../relational-databases/system-stored-procedures/sp-helpdbfixedrole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_srvrolepermission](../../relational-databases/system-stored-procedures/sp-srvrolepermission-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
