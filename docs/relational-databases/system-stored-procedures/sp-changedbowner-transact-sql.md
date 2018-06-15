---
title: sp_changedbowner (Transact-SQL) | Microsoft Docs
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
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cb7d6df77a581b82ca79e1962c80df827ffd1718
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238253"
---
# <a name="spchangedbowner-transact-sql"></a>sp_changedbowner (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o proprietário do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame=] '*login*'  
 É a ID de logon do novo proprietário do banco de dados atual. *logon* é **sysname**, sem padrão. *logon* deve ser um já existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou usuário do Windows. *logon* não pode ser o proprietário do banco de dados atual se já tiver acesso ao banco de dados por meio de uma conta de segurança de usuário existente no banco de dados. Para evitar isso, descarte primeiro o usuário do banco de dados atual.  
  
 [ @map=] *remap_alias_flag*  
 O *remap_alias_flag* parâmetro é preterido porque foram removidos aliases de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usando o *remap_alias_flag* parâmetro não causa um erro, mas não tem nenhum efeito.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Depois que sp_changedbowner for executado, o novo proprietário será conhecido como usuário dbo no banco de dados. O dbo possui permissões implícitas para executar todas as atividades no banco de dados.  
  
 O proprietário dos banco de dados do sistema mestre, modelo ou tempdb não pode ser alterado.  
  
 Para exibir uma lista de válidos *login* valores, execute o procedimento armazenado sp_helplogins.  
  
 Execução de sp_changedbowner somente com o *login* para propriedade de banco de dados de alterações do parâmetro *logon*.  
  
 É possível alterar o proprietário de qualquer protegível usando a instrução ALTER AUTHORIZATION. Para obter mais informações, confira [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão TAKE OWNERSHIP no banco de dados. Se o novo proprietário tiver um usuário correspondente no banco de dados, a permissão IMPERSONATE será necessária no logon; caso contrário, a permissão CONTROL SERVER será necessária no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir torna o logon `Albert` o proprietário do banco de dados atual.  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [sp_dropalias &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropalias-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helplogins &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
