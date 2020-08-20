---
description: sp_helpsrvrolemember (Transact-SQL)
title: sp_helpsrvrolemember (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrolemember
- sp_helpsrvrolemember_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrolemember
ms.assetid: d0714913-8d6b-4de3-b042-3ae9934f839d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be34b5879a21824e5e0b92fbe3187fce039d6ffa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489239"
---
# <a name="sp_helpsrvrolemember-transact-sql"></a>sp_helpsrvrolemember (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os membros de uma função de servidor fixa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsrvrolemember [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @srvrolename = ] 'role'` É o nome de uma função de servidor fixa. *role* é **sysname**, com um padrão de NULL. Se a *função*não for especificada, o conjunto de resultados incluirá informações sobre todas as funções de servidor fixas.  
  
 a *função* pode ser qualquer um dos valores a seguir.  
  
|Função de servidor fixa|Descrição|  
|-----------------------|-----------------|  
|sysadmin|Administradores de sistema|  
|securityadmin|Administradores de segurança|  
|serveradmin|Administradores de servidor|  
|setupadmin|Administradores de configuração|  
|processadmin|Administradores de processo|  
|diskadmin|Administradores de disco|  
|dbcreator|Criadores de banco de dados|  
|bulkadmin|Pode executar instruções BULK INSERT|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Nome da função de servidor|  
|MemberName|**sysname**|Nome de um membro de ServerRole|  
|MemberSID|**varbinary (85)**|Identificador de segurança de MemberName|  
  
## <a name="remarks"></a>Comentários  
 Use sp_helprolemember para exibir os membros de uma função de banco de dados.  
  
 Todos os logons são membros de públicos. sp_helpsrvrolemember não reconhece a função pública porque, internamente, não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa o público como uma função.  
  
 Para adicionar ou remover membros de funções de servidor, consulte [ALTER Server ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 sp_helpsrvrolemember não pega uma função de servidor definida pelo usuário como um argumento. Para determinar os membros de uma função de servidor definida pelo usuário, consulte os exemplos em [ALTER Server role &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir lista os membros da função de servidor fixa `sysadmin`.  
  
```  
EXEC sp_helpsrvrolemember 'sysadmin';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_helprole ](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helprolemember ](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
