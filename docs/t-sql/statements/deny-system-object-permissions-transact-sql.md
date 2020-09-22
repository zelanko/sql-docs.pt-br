---
description: Permissões de objeto do sistema DENY (Transact-SQL)
title: Permissões DENY do objeto do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, system objects
- encryption [SQL Server], system objects
- system objects [SQL Server]
- cryptography [SQL Server], system objects
ms.assetid: 4e43f954-0982-470b-a239-08a13c61563a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: abfb423e90d8c7776fe9d2f5eb8815a37254a3b8
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688516"
---
# <a name="deny-system-object-permissions-transact-sql"></a>Permissões de objeto do sistema DENY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Nega permissões em objetos do sistema, como procedimentos armazenados, procedimentos armazenados estendidos, funções e exibições.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DENY { SELECT | EXECUTE } ON [ sys.]system_object TO principal   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 [ **sys.**]  
 O qualificador **sys** só é necessário quando você está referenciando exibições do catálogo e exibições de gerenciamento dinâmico.  
  
 *system_object*  
 Especifica o objeto no qual a permissão está sendo negada.  
  
 *principal*  
 Especifica a entidade a partir da qual a permissão está sendo revogada.  
  
## <a name="remarks"></a>Comentários  
 Essa instrução pode ser usada para negar permissões em determinados procedimentos armazenados, procedimentos armazenados estendidos, funções com valor de tabela, funções escalares, exibições, exibições do catálogo, exibições de compatibilidade, exibições INFORMATION_SCHEMA, exibições de gerenciamento dinâmico e tabelas do sistema instaladas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para cada um desses objetos de sistema, existe como um registro exclusivo no banco de dados de recursos (**mssqlsystemresource**). O banco de dados de recursos é somente leitura. Um link para o objeto é exposto como um registro no esquema **sys** de todo banco de dados.  
  
 A resolução de nome padrão resolve nomes de procedimento não qualificados para o banco de dados de recursos. Portanto, o qualificador **sys** é necessário somente ao especificar exibições do catálogo e exibições de gerenciamento dinâmico.  
  
> [!CAUTION]  
>  A negação de permissões em objetos do sistema provocará falha nos aplicativos que dependem deles. O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa exibições do catálogo e pode não funcionar como o esperado se você alterar as permissões padrão em exibições do catálogo.  
  
 Não há suporte para a negação de permissões em gatilhos e colunas de objetos do sistema.  
  
 As permissões em objetos do sistema serão preservadas nas atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Os objetos do sistema são visíveis na exibição de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) . As permissões em objetos do sistema são visíveis na exibição de catálogo [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) do banco de dados **mestre** .  
  
 A consulta a seguir retorna informações sobre permissões de objetos do sistema:  
  
```sql
SELECT * FROM master.sys.database_permissions AS dp   
    JOIN sys.system_objects AS so  
    ON dp.major_id = so.object_id  
    WHERE dp.class = 1 AND so.parent_object_id = 0 ;  
GO  
```  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir nega a permissão `EXECUTE` em `xp_cmdshell` a `public`.  
  
```sql
DENY EXECUTE ON sys.xp_cmdshell TO public;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Convenções de sintaxe do Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [Permissões GRANT do Objeto do Sistema &#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)   
 [Permissões REVOKE do objeto do sistema &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-system-object-permissions-transact-sql.md)  
  
  
