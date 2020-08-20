---
description: sp_dropuser (Transact-SQL)
title: sp_dropuser (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropuser
- sp_dropuser_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7456ae7c2350f8d7c7e5aa145b44b2267f22f4fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464298"
---
# <a name="sp_dropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove um usuário de banco de dados do banco de dados atual. **sp_dropuser** fornece compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [drop User](../../t-sql/statements/drop-user-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name_in_db = ] 'user'` É o nome do usuário a ser removido. o *usuário* é um **sysname**, sem padrão. o *usuário* deve existir no banco de dados atual. Ao especificar um logon do Windows, use o nome pelo qual o banco de dados conhece o logon.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropuser** executa **sp_revokedbaccess** para remover o usuário do banco de dados atual.  
  
 Use **sp_helpuser** para exibir uma lista dos nomes de usuário que podem ser removidos do banco de dados atual.  
  
 Quando um usuário de banco de dados é removido, qualquer alias para esse usuário também é removido. Se o usuário possuir um esquema vazio com o mesmo nome do usuário, o esquema será descartado. Se o usuário possuir qualquer outro item protegível no banco de dados, o usuário não será descartado. A propriedade dos objetos deve ser transferida primeiro a outro principal. Para obter mais informações, confira [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md). A remoção do usuário de banco de dados remove automaticamente as permissões associadas ao usuário e remove o usuário de todas as funções de banco de dados das quais seja membro.  
  
 **sp_dropuser** não pode ser usado para remover o proprietário do banco de dados (**dbo**) **INFORMATION_SCHEMA** usuários ou o usuário **convidado** dos bancos de dados **mestre** ou **tempdb** . Em bancos de dados que não sejam do sistema, o `EXEC sp_dropuser 'guest'` revogará a permissão Connect do **convidado**do usuário. Mas o próprio usuário não será descartado.  
  
 **sp_dropuser** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY USER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o usuário `Albert` do banco de dados atual.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_grantdbaccess ](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokedbaccess ](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
