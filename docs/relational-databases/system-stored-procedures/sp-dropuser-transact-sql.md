---
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d96004357962ee822df7458a30d740fc836de658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62723871"
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um usuário de banco de dados do banco de dados atual. **sp_dropuser** fornece compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name_in_db = ] 'user'` É o nome de usuário a ser removido. *usuário* é um **sysname**, sem padrão. *usuário* deve existir no banco de dados atual. Ao especificar um logon do Windows, use o nome pelo qual o banco de dados conhece o logon.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropuser** executa **sp_revokedbaccess** para remover o usuário de banco de dados atual.  
  
 Use **sp_helpuser** para exibir uma lista dos nomes de usuário que podem ser removidos do banco de dados atual.  
  
 Quando um usuário de banco de dados é removido, qualquer alias para esse usuário também é removido. Se o usuário possuir um esquema vazio com o mesmo nome do usuário, o esquema será descartado. Se o usuário possuir qualquer outro item protegível no banco de dados, o usuário não será descartado. A propriedade dos objetos deve ser transferida primeiro a outro principal. Para obter mais informações, confira [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md). A remoção do usuário de banco de dados remove automaticamente as permissões associadas ao usuário e remove o usuário de todas as funções de banco de dados das quais seja membro.  
  
 **sp_dropuser** não pode ser usado para remover o proprietário do banco de dados (**dbo**) **INFORMATION_SCHEMA** usuários, ou o **convidado** usuário o **mestre**  ou **tempdb** bancos de dados. Em bancos de dados `EXEC sp_dropuser 'guest'` revogará a permissão CONNECT do usuário **convidado**. Mas o próprio usuário não será descartado.  
  
 **sp_dropuser** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY USER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o usuário `Albert` do banco de dados atual.  
  
```  
EXEC sp_dropuser 'Albert';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
