---
title: sp_helprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprole_TSQL
- sp_helprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprole
ms.assetid: b023103f-ccf3-44e2-b418-4be9bdd49f4a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 674da069c1c47c9e577327e9482add64353de881
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832595"
---
# <a name="sp_helprole-transact-sql"></a>sp_helprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as funções no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helprole [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome de uma função no banco de dados atual. *role* é **sysname**, com um padrão de NULL. a *função* deve existir no banco de dados atual. Se a *função* não for especificada, as informações sobre todas as funções no banco de dados atual serão retornadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**RoleName**|**sysname**|Nome da função no banco de dados atual.|  
|**RoleId**|**smallint**|ID de **roleName**.|  
|**IsAppRole**|**int**|0 = **roleName** não é uma função de aplicativo.<br /><br /> 1 = **roleName** é uma função de aplicativo.|  
  
## <a name="remarks"></a>Comentários  
 Para exibir as permissões associadas à função, use **sp_helprotect**. Para exibir os membros de uma função de banco de dados, use **sp_helprolemember**.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 A consulta a seguir retorna todas as funções no banco de dados atual.  
  
```  
EXEC sp_helprole  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [&#41;&#40;Transact-SQL de sp_addapprole](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprole](../../relational-databases/system-stored-procedures/sp-droprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprolemember](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsrvrolemember](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
