---
description: sp_msx_set_account (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f9329879f37ee8508f45f4734a0968596348d5cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535056"
---
# <a name="sp_msx_set_account-transact-sql"></a>sp_msx_set_account (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define o nome e a senha da conta do servidor mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no servidor de destino.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_msx_set_account [ @credential_name = ] 'credential_name'  | [ @credential_id = ] credential_id  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @credential_name = ] 'credential_name'` O nome da credencial a ser usada para fazer logon no servidor mestre. O nome fornecido deve ser o nome de uma credencial existente. O *credential_name* ou *credential_id* deve ser especificado.  
  
`[ @credential_id = ] credential_id` O identificador da credencial a ser usada para fazer logon no servidor mestre. Ele deve ser um identificador para uma credencial existente. O *credential_name* ou *credential_id* deve ser especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa credenciais para armazenar as informações de nome de usuário e senha que um servidor de destino usa para fazer o logon em um servidor mestre. Este procedimento define a credencial que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para este servidor de destino usa para fazer o logon no servidor mestre.  
  
 A credencial especificada deve ser uma credencial existente. Para obter mais informações sobre como criar uma credencial, consulte [criar credencial &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Permissões de execução para **sp_msx_set_account** padrão para membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define que este servidor use a credencial `MsxAccount` para fazer o logon no servidor mestre.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_set_account @credential_name = MsxAccount ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_msx_get_account ](../../relational-databases/system-stored-procedures/sp-msx-get-account-transact-sql.md)  
  
  
