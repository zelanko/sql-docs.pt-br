---
title: sp_droprole (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_droprole
- sp_droprole_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_droprole
ms.assetid: 889ee074-00f8-40a9-bddb-d7d3ef0cbc19
caps.latest.revision: "23"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9549a61767035f8b2f9d26854190e9addfb397f8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdroprole-transact-sql"></a>sp_droprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove uma função de banco de dados do banco de dados atual.  
  
> [!IMPORTANT]  
>  Em [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_droprole** foi substituída pela instrução DROP ROLE. **sp_droprole** é incluído somente para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e podem não ter suporte em uma versão futura.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droprole [ @rolename= ] 'role'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@rolename =** ] **'***função***'**  
 É o nome da função de banco de dados a ser removida do banco de dados atual. *função* é um **sysname**, sem padrão. *função* já deve existir no banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Somente as funções de banco de dados podem ser removidas usando **sp_droprole**.  
  
 Uma função de banco de dados com membros existentes não pode ser removida. Todos os membros de uma função de banco de dados devem ser removidos antes que ela possa ser removida. Para remover os usuários de uma função, use **sp_droprolemember**. Se todos os usuários ainda são membros da função de **sp_droprole** exibirá esses membros.  
  
 Funções fixas e **pública** função não pode ser removida.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addrole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)   
 [Remover função &#40; Transact-SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sp_dropapprole &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
