---
title: Permissões GRANT do objeto do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], system objects
- system objects [SQL Server]
- GRANT statement, system objects
ms.assetid: 9d4e89f4-478f-419a-8b50-b096771e3880
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 39130687751acab7c86051625f41db644b567a8c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33069783"
---
# <a name="grant-system-object-permissions-transact-sql"></a>Permissões de objeto do sistema GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissões em objetos do sistema como procedimentos armazenados do sistema, procedimentos armazenados estendidos, funções e exibições.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GRANT { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
## <a name="arguments"></a>Argumentos  
 [ sys.] .  
 O qualificador sys só é necessário quando você está referenciando exibições do catálogo e exibições de gerenciamento dinâmico.  
  
 *system_object*  
 Especifica o objeto no qual a permissão está sendo concedida.  
  
 *principal*  
 Especifica a entidade de segurança para o qual a permissão está sendo concedida.  
  
## <a name="remarks"></a>Remarks  
 Essa instrução pode ser usada para conceder permissões em determinados procedimentos armazenados, procedimentos armazenados estendidos, funções com valor de tabela, funções escalares, exibições, exibições do catálogo, exibições de compatibilidade, exibições INFORMATION_SCHEMA, exibições de gerenciamento dinâmico e tabelas do sistema instaladas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ara cada um desses objetos do sistema existe como um registro exclusivo no banco de dados de recursos do servidor (mssqlsystemresource). O banco de dados de recursos é somente leitura. Um link para o objeto é exposto como um registro no esquema sys de todo banco de dados. A permissão para executar ou selecionar um objeto do sistema pode ser concedida, negada e revogada.  
  
 A concessão de permissão para executar ou selecionar um objeto não transmite necessariamente todas as permissões necessárias para usar o objeto. A maioria dos objetos executa operações para as quais são necessárias permissões adicionais. Por exemplo, um usuário ao qual é concedida a permissão EXECUTE no sp_addlinkedserver não pode criar um servidor vinculado a menos que o usuário também seja membro da função de servidor fixa sysadmin.  
  
 A resolução de nome padrão resolve nomes de procedimento não qualificados para o banco de dados de recursos. Portanto, o qualificador sys é necessário somente quando você está especificando exibições do catálogo e exibições de gerenciamento dinâmico.  
  
 A concessão de permissões em gatilhos e em colunas de objetos do sistema não possui suporte.  
  
 As permissões em objetos do sistema serão preservadas nas atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os objetos do sistema são visíveis na exibição de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) . As permissões em objetos do sistema são visíveis na exibição de catálogo [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) do banco de dados mestre.  
  
 A consulta a seguir retorna informações sobre permissões de objetos do sistema:  
  
```  
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-select-permission-on-a-view"></a>A. Concedendo a permissão SELECT em uma exibição  
 O exemplo a seguir concede a permissão de logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `Sylvester1` para selecionar uma exibição que lista logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois, o exemplo concede a permissão adicional necessária para exibir metadados nos logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não sejam de propriedade do usuário.  
  
```  
USE AdventureWorks2012;  
GRANT SELECT ON sys.sql_logins TO Sylvester1;  
GRANT VIEW SERVER STATE to Sylvester1;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-an-extended-stored-procedure"></a>B. Concedendo a permissão EXECUTE em um procedimento armazenado estendido  
 O exemplo a seguir concede a permissão `EXECUTE` em `xp_readmail` para `Sylvester1`.  
  
```  
GRANT EXECUTE ON xp_readmail TO Sylvester1;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.system_objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [Permissões REVOKE do objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)   
 [Permissões DENY de objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/deny-system-object-permissions-transact-sql.md)  
  
  
