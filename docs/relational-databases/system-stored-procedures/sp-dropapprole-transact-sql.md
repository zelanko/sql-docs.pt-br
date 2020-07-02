---
title: sp_dropapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropapprole_TSQL
- sp_dropapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropapprole
ms.assetid: ea1aefe6-8f7d-46e9-a3cb-7b037b393e73
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: 740bfcf83aca712dcaeb7189b226d880f7ae5a02
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717304"
---
# <a name="sp_dropapprole-transact-sql"></a>sp_dropapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove uma função de aplicativo do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [drop Application role](../../t-sql/statements/drop-application-role-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_dropapprole [@rolename = ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É a função de aplicativo a ser removida. *role* é um **sysname**, sem padrão. a *função* deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropapprole** só pode ser usada para remover funções de aplicativo. Se uma função possuir algum item protegível, a função não poderá ser descartada. Antes de descartar uma função de aplicativo que possui itens protegíveis, é necessário transferir a propriedade dos itens protegíveis primeiro ou descartá-los.  
  
 **sp_dropapprole** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a função de aplicativo `SalesApp` do banco de dados atual.  
  
```sql
EXEC sp_dropapprole 'SalesApp';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addapprole](../../relational-databases/system-stored-procedures/sp-addapprole-transact-sql.md)   
 [Descartar função de aplicativo &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changeobjectowner](../../relational-databases/system-stored-procedures/sp-changeobjectowner-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_setapprole](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
