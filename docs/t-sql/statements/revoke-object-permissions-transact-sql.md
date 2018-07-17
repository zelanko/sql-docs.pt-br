---
title: Permissões REVOKE do objeto (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- table permissions [SQL Server], revoking
- REVOKE statement, objects
- revoking permissions to access tables
- object permissions [SQL Server], revoking
ms.assetid: 99c7146e-d2e7-4f1a-80ff-21a05bc5e8bb
caps.latest.revision: 33
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 441e27b035be3dc4c9cf781bb6c1078f3c74bfce
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36942592"
---
# <a name="revoke-object-permissions-transact-sql"></a>permissões de objeto REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga permissões em uma tabela, exibição, função com valor de tabela, procedimento armazenado, procedimento armazenado estendido, função escalar, função de agregação, fila de serviço ou sinônimo. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        { FROM | TO } <database_principal> [ ,...n ]   
    [ CASCADE ]  
    [ AS <database_principal> ]  
  
<permission> ::=  
    ALL [ PRIVILEGES ] | permission [ ( column [ ,...n ] ) ]  
  
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
 Especifica uma permissão que pode ser revogada em um objeto contido em esquema. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ALL  
 Revogar ALL não revoga todas as possíveis permissões. Revogar ALL é equivalente a revogar todas as 92 permissões [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] aplicáveis ao objeto especificado. O significado ALL varia desta forma:  
  
 Permissões de função escalar: EXECUTE, REFERENCES.  
  
 Permissões de função com valor de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 Permissões de procedimento armazenado: EXECUTE.  
  
 Permissões de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 Permissões de exibição: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
 PRIVILEGES  
 Incluído para conformidade com 92 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]. Não altera o comportamento de ALL.  
  
 *column*  
 Especifica o nome de uma coluna em uma tabela, exibição ou função com valor de tabela na qual a permissão está sendo revogada. Os parênteses ( ) são necessários. Apenas permissões SELECT, REFERENCES e UPDATE podem ser negadas em uma coluna. *column* pode ser especificada na cláusula de permissões ou depois do nome protegível.  
  
 ON [ OBJECT :: ] [ *schema_name* ] . *object_name*  
 Especifica o objeto no qual a permissão está sendo revogada. A frase OBJECT será opcional se *schema_name* for especificado. Se a frase OBJECT for usada, o qualificador de escopo (::) será necessário. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema (.) será obrigatório.  
  
 { FROM | TO } \<database_principal> Especifica a entidade de segurança da qual a permissão está sendo revogada.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS \<database_principal> Especifica uma entidade de segurança por meio da qual a entidade de segurança que executa essa consulta obtém seu direito de revogar a permissão.  
  
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
 As informações sobre objetos são visível em várias exibições do catálogo. Para obter mais informações, veja [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Um objeto é um protegível em nível de esquema contido pelo esquema que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em um objeto são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de objeto|Implícito na permissão de objeto|Implícito na permissão de esquema|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|Delete (excluir)|CONTROL|Delete (excluir)|  
|Execute|CONTROL|Execute|  
|INSERT|CONTROL|INSERT|  
|RECEIVE|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|RECEIVE|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|VIEW CHANGE TRACKING|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no objeto.  
  
 Se a cláusula AS for usada, o principal especificado deverá ser proprietário do objeto no qual as permissões estão sendo revogadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-revoking-select-permission-on-a-table"></a>A. Revogando a permissão SELECT em uma tabela  
 O exemplo a seguir revoga a permissão `SELECT` do usuário `RosaQdM` na tabela `Person.Address` do `AdventureWorks2012` banco de dados.  
  
```  
USE AdventureWorks2012;  
REVOKE SELECT ON OBJECT::Person.Address FROM RosaQdM;  
GO  
```  
  
### <a name="b-revoking-execute-permission-on-a-stored-procedure"></a>B. Revogando a permissão EXECUTE em um procedimento armazenado  
 O exemplo a seguir revoga a permissão `EXECUTE` no procedimento armazenado `HumanResources.uspUpdateEmployeeHireInfo` de uma função de aplicativo chamada `Recruiting11`.  
  
```  
USE AdventureWorks2012;  
REVOKE EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    FROM Recruiting11;  
GO   
```  
  
### <a name="c-revoking-references-permission-on-a-view-with-cascade"></a>C. Revogando a permissão REFERENCES em uma exibição com CASCADE  
 O exemplo a seguir revoga a permissão `REFERENCES` da coluna `BusinessEntityID` na exibição `HumanResources.vEmployee` do usuário `Wanida` com `CASCADE`.  
  
```  
USE AdventureWorks2012;  
REVOKE REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    FROM Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

