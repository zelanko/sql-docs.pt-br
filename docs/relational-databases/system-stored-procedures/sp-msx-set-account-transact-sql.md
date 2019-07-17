---
title: sp_msx_set_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_set_account
- sp_msx_set_account_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_set_account
ms.assetid: 314ec720-3a37-48f7-bb6b-8d5b894bf843
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22372412f9c3f905b8978741b556724ca880568c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108026"
---
# <a name="spmsxsetaccount-transact-sql"></a>sp_msx_set_account (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define o nome e a senha da conta do servidor mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no servidor de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @credential_name = ] 'credential_name'` O nome da credencial a ser usada para fazer logon no servidor mestre. O nome fornecido deve ser o nome de uma credencial existente. Qualquer um dos *credential_name* ou *credential_id* deve ser especificado.  
  
`[ @credential_id = ] credential_id` O identificador de credencial a ser usada para fazer logon no servidor mestre. Ele deve ser um identificador para uma credencial existente. Qualquer um dos *credential_name* ou *credential_id* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 nenhuma.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa credenciais para armazenar as informações de nome de usuário e senha que um servidor de destino usa para fazer o logon em um servidor mestre. Este procedimento define a credencial que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para este servidor de destino usa para fazer o logon no servidor mestre.  
  
 A credencial especificada deve ser uma credencial existente. Para obter mais informações sobre como criar uma credencial, consulte [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução **sp_msx_set_account** padrão para os membros da **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define que este servidor use a credencial `MsxAccount` para fazer o logon no servidor mestre.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do SQL Server Agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_msx_get_account &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
