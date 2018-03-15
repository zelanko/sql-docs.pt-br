---
title: "Permissões DENY do objeto (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- DENY statement, objects
- table permissions [SQL Server]
ms.assetid: 0b8d3ddc-38c0-4241-b7bb-ee654a5081aa
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: dc405b480d063ff6990182f9a66cc6f4e35c3a5a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="deny-object-permissions-transact-sql"></a>Permissões de objeto DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em um membro da classe OBJECT de protegíveis. Esses são membros da classe OBJECT: tabelas, exibições, funções com valor de tabela, procedimentos armazenados, procedimentos armazenados estendidos, funções escalares, funções de agregação, filas de serviço e sinônimos.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
        TO <database_principal> [ ,...n ]   
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
 Especifica uma permissão que pode ser negada em um objeto contido em esquema. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ALL  
 A negação de ALL não nega todas as possíveis permissões. A negação de ALL é equivalente a negar todas as permissões ANSI-92 aplicáveis ao objeto especificado. O significado ALL varia desta forma:  
  
 - Permissões de função escalar: EXECUTE, REFERENCES.  
 - Permissões de função com valor de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Permissões de procedimento armazenado: EXECUTE.  
 - Permissões de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
 - Permissões de exibição: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
PRIVILEGES  
 Incluído para conformidade com o ANSI-92. Não altera o comportamento de ALL.  
  
*column*  
 Especifica o nome de uma coluna em uma tabela, exibição ou função com valor de tabela na qual a permissão está sendo negada. Os parênteses **( )** são necessários. Apenas permissões SELECT, REFERENCES e UPDATE podem ser negadas em uma coluna. *column* pode ser especificada na cláusula de permissões ou depois do nome protegível.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para compatibilidade com versões anteriores.  
  
 ON [ OBJECT **::** ] [ *schema_name* ] **.** *object_name*  
 Especifica o objeto no qual a permissão está sendo negada. A frase OBJECT será opcional se *schema_name* for especificado. Se a frase OBJECT for usada, o qualificador de escopo (**::**) será necessário. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema (**.**) será obrigatório.  
  
 TO \<database_principal>  
 Especifica a entidade à qual a permissão está sendo negada.  
  
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
 As informações sobre objetos são visível em várias exibições do catálogo. Para obter mais informações, veja [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Um objeto é um protegível em nível de esquema contido pelo esquema que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um objeto são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
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
  
 Se a cláusula AS for usada, o principal especificado deverá ser proprietário do objeto no qual as permissões estão sendo negadas.  
  
## <a name="examples"></a>Exemplos  
Os exemplos a seguir usam o banco de dados AdventureWorks.
  
### <a name="a-denying-select-permission-on-a-table"></a>A. Negação da permissão SELECT em uma tabela  
 O exemplo a seguir nega a permissão `SELECT` ao usuário `RosaQdM` na tabela `Person.Address`.  
  
```  
DENY SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-denying-execute-permission-on-a-stored-procedure"></a>B. Negação da permissão EXECUTE em um procedimento armazenado  
 O exemplo a seguir nega a permissão `EXECUTE` no procedimento armazenado `HumanResources.uspUpdateEmployeeHireInfo` para uma função de aplicativo chamada `Recruiting11`.  
  
```  
DENY EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-denying-references-permission-on-a-view-with-cascade"></a>C. Negação da permissão REFERENCES em uma exibição com CASCADE  
 O exemplo a seguir nega a permissão `REFERENCES` na coluna `BusinessEntityID` na exibição `HumanResources.vEmployee` para o usuário `Wanida` com `CASCADE`.  
  
```  
DENY REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões de objeto GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)   
 [Permissões de Objeto REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  
