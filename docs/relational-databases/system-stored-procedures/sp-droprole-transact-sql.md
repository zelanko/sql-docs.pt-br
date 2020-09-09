---
description: sp_droprole (Transact-SQL)
title: sp_droprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6180676b4458a5f270f9ecab9bb35d2ed8a481c4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548076"
---
# <a name="sp_droprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove uma função de banco de dados do banco de dados atual.  
  
> [!IMPORTANT]  
>  No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , **sp_droprole** foi substituído pela instrução DROP Role. **sp_droprole** está incluído apenas para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e pode não ter suporte em uma versão futura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'` É o nome da função de banco de dados a ser removida do banco de dados atual. *role* é um **sysname**, sem padrão. a *função* já deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Somente as funções de banco de dados podem ser removidas usando **sp_droprole**.  
  
 Uma função de banco de dados com membros existentes não pode ser removida. Todos os membros de uma função de banco de dados devem ser removidos antes que ela possa ser removida. Para remover usuários de uma função, use **sp_droprolemember**. Se algum usuário ainda for membro da função, **sp_droprole** exibirá esses membros.  
  
 As funções fixas e a função **pública** não podem ser removidas.  
  
 Uma função não poderá ser removida se possuir qualquer protegível. Antes de descartar uma função de aplicativo que possui itens protegíveis, é necessário transferir a propriedade dos itens protegíveis primeiro ou descartá-los. Use ALTER AUTHORIZATION para alterar o proprietário de objetos que não devem ser removidos.  
  
 **sp_droprole** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na função.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove a função de aplicativo `Sales`.  
  
```  
EXEC sp_droprole 'Sales';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [DROP ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropapprole ](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
