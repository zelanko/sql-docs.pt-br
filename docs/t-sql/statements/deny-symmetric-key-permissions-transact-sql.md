---
title: Permissões DENY de chave simétrica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- denying permissions [SQL Server], symmetric keys
- symmetric keys [SQL Server], permissions
- permissions [SQL Server], symmetric keys
- DENY statement, symmetric keys
- encryption [SQL Server], symmetric keys
- cryptography [SQL Server], symmetric keys
ms.assetid: 52d4b12d-17be-4cbd-aa78-65332a4883b0
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abd7993f143f7740b6f845cff6a69a4f8157dfba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="deny-symmetric-key-permissions-transact-sql"></a>Permissões de chave simétrica DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em uma chave simétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY permission [ ,...n ]    
    ON SYMMETRIC KEY :: symmetric_key_name   
        TO <database_principal> [ ,...n ] [ CASCADE ]  
    [ AS <database_principal> ]   
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser negada em uma chave simétrica. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ON SYMMETRIC KEY ::*asymmetric_key_name*  
 Especifica a chave simétrica na qual a permissão está sendo negada. O qualificador de escopo (::) é necessário.  
  
 TO \<*database_principal*>  
 Especifica a entidade a partir da qual a permissão está sendo revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 AS \<database_principal>  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa essa consulta deriva seu direito de negar a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
 Especifica uma função de aplicativo.  
  
 *Database_user_mapped_to_Windows_User*  
 Especifica um usuário do banco de dados mapeado para um usuário do Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
 Especifica um usuário do banco de dados mapeado para um grupo do Windows.  
  
 *Database_user_mapped_to_certificate*  
 Especifica um usuário do banco de dados mapeado para um certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
 Especifica um usuário do banco de dados mapeado para uma chave assimétrica.  
  
 *Database_user_with_no_login*  
 Especifica um usuário do banco de dados sem nenhuma entidade de segurança correspondente no nível de servidor.  
  
## <a name="remarks"></a>Remarks  
 As informações sobre chaves simétricas podem ser visualizadas na exibição do catálogo [sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md).  
  
 Uma chave simétrica é um protegível no nível de banco de dados contido no banco de dados pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em uma chave simétrica são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de chave simétrica|Implícita na permissão de chave simétrica|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SYMMETRIC KEY|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave simétrica ou a permissão ALTER ANY SYMMETRIC KEY no banco de dados. Se você usar a opção AS, a entidade especificada deverá ser proprietária da chave simétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir nega a permissão `ALTER` na chave simétrica `SamInventory42` ao usuário do banco de dados `HamidS`.  
  
```  
USE AdventureWorks2012;  
DENY ALTER ON SYMMETRIC KEY::SamInventory42 TO HamidS;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [Permissões GRANT de chave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)   
 [Permissões REVOKE de chave simétrica &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-symmetric-key-permissions-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
