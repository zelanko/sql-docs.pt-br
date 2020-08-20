---
description: sp_validatelogins (Transact-SQL)
title: sp_validatelogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b3237ed7a7d585e128b678772ec6d3a010fe3d00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473429"
---
# <a name="sp_validatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Relata informações sobre usuários e grupos do Windows que são mapeadas para entidades de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não existem mais no ambiente do Windows.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**SIDs**|**varbinary (85)**|SID (identificador de segurança) do usuário ou grupo do Windows.|  
|**NT Login**|**sysname**|Nome de usuário ou do grupo do Windows.|  
  
## <a name="remarks"></a>Comentários  
 Se a entidade de nível de servidor órfão possuir um usuário do banco de dados, esse usuário deverá ser removido para que o principal de servidor órfão também possa ser removido. Para remover um usuário de banco de dados, use [drop User](../../t-sql/statements/drop-user-transact-sql.md). Se a entidade de nível de servidor possuir protegíveis no banco de dados, o proprietário dos protegíveis deverá ser transferido ou descartado. Para transferir a propriedade de protegíveis de banco de dados, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Para remover mapeamentos para usuários e grupos do Windows que não existem mais, use [drop login](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa **sysadmin** ou **securityadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe usuários e grupos do Windows que não existem mais, mas ainda têm acesso concedido a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [DROP USER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
