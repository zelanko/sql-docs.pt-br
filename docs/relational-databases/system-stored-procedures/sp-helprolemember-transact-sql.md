---
title: sp_helprolemember (Transact-SQL) | Microsoft Docs
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
- sp_helprolemember_TSQL
- sp_helprolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helprolemember
ms.assetid: 42797510-aa5d-4564-85ac-27418419af9c
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: fbe422aff07694ee7358f3be9906890d795f46b7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sphelprolemember-transact-sql"></a>sp_helprolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre os membros direto de uma função no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helprolemember [ [ @rolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'** *função* **'**  
 É o nome de uma função do banco de dados atual. *função* é **sysname**, com um padrão NULL. *função* deve existir no banco de dados atual. Se *função* não for especificado, todas as funções que contêm pelo menos um membro do banco de dados atual serão retornadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**DbRole**|**sysname**|Nome da função no banco de dados atual.|  
|**Nome do membro**|**sysname**|Nome de um membro de **DbRole.**|  
|**MemberSID**|**varbinary(85)**|Identificador de segurança do **MemberName.**|  
  
## <a name="remarks"></a>Remarks  
 Se o banco de dados contiver funções aninhadas, **MemberName** pode ser o nome de uma função. **sp_helprolemember** não mostra a associação obtida através das funções aninhadas. Por exemplo, se User1 for um membro da Role1, e a Role1 for um membro da Role2, `EXEC sp_helprolemember 'Role2'` retornará a Role1, mas não os membros da Role1 (User1 neste exemplo). Para retornar associações aninhadas, você deve executar **sp_helprolemember** repetidamente para cada função aninhada.  
  
 Use **sp_helpsrvrolemember** para exibir os membros de uma função de servidor fixa.  
  
 Use [IS_ROLEMEMBER &#40;Transact-SQL&#41; ](../../t-sql/functions/is-rolemember-transact-sql.md) para verificar a associação de função para um usuário especificado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe os membros da função `Sales`.  
  
```  
EXEC sp_helprolemember 'Sales';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [sp_droprolemember & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_helprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [sp_helpsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
