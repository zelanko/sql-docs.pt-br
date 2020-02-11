---
title: sp_helpsrvrole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpsrvrole_TSQL
- sp_helpsrvrole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpsrvrole
ms.assetid: 5c7f39f3-c261-4f70-8beb-08242d4ac242
author: stevestein
ms.author: sstein
ms.openlocfilehash: a632e6923ab3127a363650c63533fa548d1acc12
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006123"
---
# <a name="sp_helpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de funções de servidor fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @srvrolename = ] 'role'`É o nome da função de servidor fixa. *role* é **sysname**, com um padrão de NULL. a *função* pode ser um dos valores a seguir.  
  
|Função de servidor fixa|DESCRIÇÃO|  
|-----------------------|-----------------|  
|sysadmin|Administradores de sistema|  
|securityadmin|Administradores de segurança|  
|serveradmin|Administradores de servidor|  
|setupadmin|Administradores de configuração|  
|processadmin|Administradores de processo|  
|diskadmin|Administradores de disco|  
|dbcreator|Criadores de Banco de Dados|  
|bulkadmin|Pode executar instruções BULK INSERT|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|ServerRole|**sysname**|Nome da função de servidor|  
|DESCRIÇÃO|**sysname**|Descrição de ServerRole|  
  
## <a name="remarks"></a>Comentários  
 As funções de servidor fixas são definidas no nível de servidor e possuem permissões para executar atividades administrativas específicas no nível de servidor. A funções de servidor fixas não podem ser adicionadas, removidas ou alteradas.  
  
 Para adicionar ou remover membros de funções de servidor, consulte [ALTER Server ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Todos os logons são membros de públicos. sp_helpsrvrole não reconhece a função pública porque, internamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não implementa o público como uma função.  
  
 sp_helpsrvrole não pega uma função de servidor definida pelo usuário como um argumento. Para listar as funções de servidor definidas pelo usuário, consulte os exemplos em [ALTER Server ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-the-fixed-server-roles"></a>a. Listando as funções de servidor fixas  
 A consulta a seguir retorna a lista de funções de servidor fixas.  
  
```  
EXEC sp_helpsrvrole ;  
```  
  
### <a name="b-listing-fixed-and-user-defined-server-roles"></a>B. Listando as funções de servidor fixas e definidas pelo usuário  
 A consulta a seguir retorna uma lista de funções de servidor fixas e definidas pelo usuário.  
  
```  
SELECT * FROM sys.server_principals WHERE type = 'R' ;  
```  
  
### <a name="c-returning-a-description-of-a-fixed-server-role"></a>C. Retornando uma descrição de uma função de servidor fixa  
 A consulta a seguir retorna o nome e a descrição de funções de servidor fixas `diskadmin`.  
  
```  
sp_helpsrvrole 'diskadmin' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)   
 [&#41;&#40;Transact-SQL de sp_addsrvrolemember](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsrvrolemember](../../relational-databases/system-stored-procedures/sp-dropsrvrolemember-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsrvrolemember](../../relational-databases/system-stored-procedures/sp-helpsrvrolemember-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
