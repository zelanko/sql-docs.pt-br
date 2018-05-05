---
title: sp_validatelogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_validatelogins
- sp_validatelogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_validatelogins
ms.assetid: 6ac52e21-e20d-469b-ad40-5aa091e06b61
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b9f47794888ad9b268971543bbbf0cdee05defbc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spvalidatelogins-transact-sql"></a>sp_validatelogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Relata informações sobre usuários e grupos do Windows que são mapeadas para entidades de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não existem mais no ambiente do Windows.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_validatelogins  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**SID**|**varbinary(85)**|SID (identificador de segurança) do usuário ou grupo do Windows.|  
|**Logon do NT**|**sysname**|Nome de usuário ou do grupo do Windows.|  
  
## <a name="remarks"></a>Remarks  
 Se a entidade de nível de servidor órfão possuir um usuário do banco de dados, esse usuário deverá ser removido para que o principal de servidor órfão também possa ser removido. Para remover um usuário de banco de dados, use [DROP USER](../../t-sql/statements/drop-user-transact-sql.md). Se a entidade de nível de servidor possuir protegíveis no banco de dados, o proprietário dos protegíveis deverá ser transferido ou descartado. Para transferir a propriedade de protegíveis de banco de dados, use [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md).  
  
 Para remover mapeamentos para usuários e grupos que não existem mais Windows, use [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** ou **securityadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir exibe usuários e grupos do Windows que não existem mais, mas ainda têm acesso concedido a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_validatelogins;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Remover usuário & #40; Transact-SQL & #41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [Remover logon & #40; Transact-SQL & #41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)  
  
  
