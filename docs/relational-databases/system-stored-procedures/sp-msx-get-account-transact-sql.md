---
title: sp_msx_get_account (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_get_account_TSQL
- sp_msx_get_account
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_get_account
ms.assetid: 7b478049-e2d0-4bac-865a-b97fd1d8dfbc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ddb3d983b37bdad5db334073fe168b518aaee77a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893461"
---
# <a name="sp_msx_get_account-transact-sql"></a>sp_msx_get_account (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lista informações sobre a credencial que o servidor de destino usa para fazer o logon no servidor mestre.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_msx_get_account  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o seguinte conjunto de resultados:  
  
|Nome da coluna|Type|Descrição|  
|-----------------|----------|-----------------|  
|msx_connection|**int**|Número de conexão do servidor mestre.|  
|msx_credential_id|**int**|ID da credencial usada para esta conexão de servidor mestre.|  
|msx_credential_name|**sysname**|Nome da credencial usada para esta conexão de servidor mestre.|  
|msx_login_name|**nvarchar(4000)**|Nome de domínio e nome de usuário do usuário Windows para a credencial.|  
  
## <a name="remarks"></a>Comentários  
 Retornará um conjunto de resultados vazio se não forem especificadas credenciais para este servidor de destino. Para definir a credencial, use sp_msx_set_account.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista informações sobre a credencial que este servidor de destino usa para fazer o logon no servidor mestre.  
  
```  
USE msdb ;  
GO  
  
EXECUTE dbo.sp_msx_get_account ;  
GO  
```  
  
 Aqui está um exemplo de conjunto de resultados:  
  
 `msx_connection msx_credential_id msx_credential_name  msx_login_name`  
  
 `-------------- ----------------- -------------------- ------------------------------`  
  
 `1              65538             MsxAccount           AdventureWorks2012\MsxAccount`  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Agent procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [CRIAR CREDENCIAl &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_msx_set_account](../../relational-databases/system-stored-procedures/sp-msx-set-account-transact-sql.md)  
  
  
