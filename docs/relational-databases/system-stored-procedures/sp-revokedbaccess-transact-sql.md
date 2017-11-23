---
title: sp_revokedbaccess (Transact-SQL) | Microsoft Docs
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
- sp_revokedbaccess_TSQL
- sp_revokedbaccess
dev_langs: TSQL
helpviewer_keywords: sp_revokedbaccess
ms.assetid: c997cfa1-539d-485c-a664-9c6f76bfe0c2
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e2802cbef18844b9b33b453db661d11c372d3654
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sprevokedbaccess-transact-sql"></a>sp_revokedbaccess (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove um usuário de banco de dados do banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md) em vez disso.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_revokedbaccess [ @name_in_db = ] 'name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@name_in_db =** ] **'***nome***'**  
 É o nome do usuário do banco de dados a ser removido. *nome* é um **sysname** sem nenhum padrão. *nome* pode ser o nome de um logon de servidor, um logon do Windows ou um grupo do Windows e deve existir no banco de dados atual. Ao especificar um logon do Windows ou um grupo do Windows, especifique o nome pelo qual o logon ou grupo é conhecido no banco de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Quando o usuário de banco de dados é removido, as permissões e os aliases que dependem do usuário também são removidos.  
  
 **sp_revokedbaccess** pode remover apenas os usuários de banco de dados do banco de dados atual. Antes de remover um usuário que possui objetos no banco de dados atual, é necessário transferir a propriedade dos objetos ou descartá-los do banco de dados. Para obter mais informações, consulte [ALTER AUTHORIZATION &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 **sp_revokedbaccess** não pode ser executado em uma transação definida pelo usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY USER no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o usuário de banco de dados mapeado para `Edmonds\LolanSo` do banco de dados atual.  
  
```  
EXEC sp_revokedbaccess 'Edmonds\LolanSo';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Remover usuário &#40; Transact-SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
