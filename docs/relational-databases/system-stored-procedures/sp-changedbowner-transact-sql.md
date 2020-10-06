---
description: sp_changedbowner (Transact-SQL)
title: sp_changedbowner (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_changedbowner
- sp_changedbowner_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_changedbowner
ms.assetid: 516ef311-e83b-45c9-b9cd-0e0641774c04
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dc4f29dba1a922b5adae32e0fc42cf714afc292f
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753478"
---
# <a name="sp_changedbowner-transact-sql"></a>sp_changedbowner (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera o proprietário do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changedbowner [ @loginame = ] 'login'  
     [ , [ @map = ] remap_alias_flag ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame =] '*logon*'  
 É a ID de logon do novo proprietário do banco de dados atual. o *logon* é **sysname**, sem padrão. o *logon* deve ser um logon já existente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um usuário do Windows. o *logon* não poderá se tornar o proprietário do banco de dados atual se ele já tiver acesso ao banco de dados por meio de uma conta de segurança de usuário existente no banco de dados. Para evitar isso, descarte primeiro o usuário do banco de dados atual.  
  
 [ @map =] *remap_alias_flag*  
 O parâmetro *remap_alias_flag* foi preterido porque os aliases de logon foram removidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O uso do parâmetro *remap_alias_flag* não causa um erro, mas não tem nenhum efeito.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Depois que sp_changedbowner for executado, o novo proprietário será conhecido como usuário dbo no banco de dados. O dbo possui permissões implícitas para executar todas as atividades no banco de dados.  
  
 O proprietário dos banco de dados do sistema mestre, modelo ou tempdb não pode ser alterado.  
  
 Para exibir uma lista de valores de *logon* válidos, execute o procedimento armazenado sp_helplogins.  
  
 A execução de sp_changedbowner apenas com o parâmetro *login* altera a propriedade do banco de dados para *logon*.  
  
 É possível alterar o proprietário de qualquer protegível usando a instrução ALTER AUTHORIZATION. Para obter mais informações, confira [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão TAKE OWNERSHIP no banco de dados. Se o novo proprietário tiver um usuário correspondente no banco de dados, a permissão IMPERSONATE será necessária no logon; caso contrário, a permissão CONTROL SERVER será necessária no servidor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir torna o logon `Albert` o proprietário do banco de dados atual.  
  
```  
EXEC sp_changedbowner 'Albert';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropalias ](./system-stored-procedures-transact-sql.md)   
 [sp_dropuser &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpdb ](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helplogins ](../../relational-databases/system-stored-procedures/sp-helplogins-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
