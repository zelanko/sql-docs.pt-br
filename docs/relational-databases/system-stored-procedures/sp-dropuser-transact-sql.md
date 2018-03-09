---
title: sp_dropuser (Transact-SQL) | Microsoft Docs
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
- sp_dropuser
- sp_dropuser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_dropuser
ms.assetid: e28f18f9-7ecf-4568-89f4-fe5c520df386
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 242950773bb0eabbd8b4170a05fd228311604bdf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdropuser-transact-sql"></a>sp_dropuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um usuário de banco de dados do banco de dados atual. **sp_dropuser** fornece compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dropuser [ @name_in_db = ] 'user'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name_in_db =**] **'***usuário***'**  
 É o nome do usuário a ser removido. *usuário* é um **sysname**, sem padrão. *usuário* deve existir no banco de dados atual. Ao especificar um logon do Windows, use o nome pelo qual o banco de dados conhece o logon.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_dropuser** executa **sp_revokedbaccess** para remover o usuário de banco de dados atual.  
  
 Use **sp_helpuser** para exibir uma lista dos nomes de usuário que podem ser removidos do banco de dados atual.  
  
 Quando um usuário de banco de dados é removido, qualquer alias para esse usuário também é removido. Se o usuário possuir um esquema vazio com o mesmo nome do usuário, o esquema será descartado. Se o usuário possuir qualquer outro item protegível no banco de dados, o usuário não será descartado. A propriedade dos objetos deve ser transferida primeiro a outro principal. Para obter mais informações, consulte [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md). A remoção do usuário de banco de dados remove automaticamente as permissões associadas ao usuário e remove o usuário de todas as funções de banco de dados das quais seja membro.  
  
 **sp_dropuser** não pode ser usado para remover o proprietário do banco de dados (**dbo**) **INFORMATION_SCHEMA** usuários, ou o **convidado** usuário a partir de  **mestre** ou **tempdb** bancos de dados. Em bancos de dados `EXEC sp_dropuser 'guest'` revogar a permissão CONNECT do usuário **convidado**. Mas o próprio usuário não será descartado.  
  
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
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_grantdbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [Remover usuário &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [sp_revokedbaccess &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
