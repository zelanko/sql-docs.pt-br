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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 204668e8983ed3503e1a5697c47a4abde92d26cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750509"
---
# <a name="sp_helpsrvrole-transact-sql"></a>sp_helpsrvrole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista de funções de servidor fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsrvrole [ [ @srvrolename = ] 'role' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @srvrolename = ] 'role'`É o nome da função de servidor fixa. *role* é **sysname**, com um padrão de NULL. a *função* pode ser um dos valores a seguir.  
  
|Função de servidor fixa|Description|  
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
|Description|**sysname**|Descrição de ServerRole|  
  
## <a name="remarks"></a>Comentários  
 As funções de servidor fixas são definidas no nível de servidor e possuem permissões para executar atividades administrativas específicas no nível de servidor. A funções de servidor fixas não podem ser adicionadas, removidas ou alteradas.  
  
 Para adicionar ou remover membros de funções de servidor, consulte [ALTER Server ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 Todos os logons são membros de públicos. sp_helpsrvrole não reconhece a função pública porque, internamente, não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implementa o público como uma função.  
  
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
  
  
