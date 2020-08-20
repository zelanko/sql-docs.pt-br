---
description: sp_helprolemember (Transact-SQL)
title: sp_helprolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 360b700d6fe123c3a87ddb45878a3806e5671bee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464176"
---
# <a name="sp_helprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os membros direto de uma função no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] ' role '` É o nome de uma função no banco de dados atual. *role* é **sysname**, com um padrão de NULL. a *função* deve existir no banco de dados atual. Se a *função* não for especificada, todas as funções que contêm pelo menos um membro do banco de dados atual serão retornadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|Nome da função no banco de dados atual.|  
|**MemberName**|**sysname**|Nome de um membro de **DbRole.**|  
|**MemberSID**|**varbinary (85)**|Identificador de segurança de **MemberName.**|  
  
## <a name="remarks"></a>Comentários  
 Se o banco de dados contiver funções aninhadas, **MemberName** poderá ser o nome de uma função. **sp_helprolemember** não mostra a associação obtida por meio de funções aninhadas. Por exemplo, se User1 for um membro da Role1, e a Role1 for um membro da Role2, `EXEC sp_helprolemember 'Role2'` retornará a Role1, mas não os membros da Role1 (User1 neste exemplo). Para retornar associações aninhadas, você deve executar **sp_helprolemember** repetidamente para cada função aninhada.  
  
 Use **sp_helpsrvrolemember** para exibir os membros de uma função de servidor fixa.  
  
 Use [IS_ROLEMEMBER &#40;&#41;Transact-SQL ](../../t-sql/functions/is-rolemember-transact-sql.md) para verificar a associação de função para um usuário especificado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe os membros da função `Sales`.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addrolemember ](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droprolemember ](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprole ](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsrvrolemember ](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
