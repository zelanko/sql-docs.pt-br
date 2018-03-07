---
title: "Permissões de objeto GRANT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
- granting permissions [SQL Server], objects
- GRANT statement, objects
ms.assetid: c001c2e7-d092-43d4-8fa6-693b3ec4c3ea
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7346cb0ddd69277fd9a7336feaba766fb1ec5b0b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="grant-object-permissions-transact-sql"></a>CONCEDER permissões de objeto (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permissões em uma tabela, exibição, função com valor de tabela, procedimento armazenado, procedimento armazenado estendido, função escalar, função de agregação, fila de serviço ou sinônimo.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT <permission> [ ,...n ] ON   
    [ OBJECT :: ][ schema_name ]. object_name [ ( column [ ,...n ] ) ]  
    TO <database_principal> [ ,...n ]   
    [ WITH GRANT OPTION ]  
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
 *permissão*  
 Especifica uma permissão que pode ser concedida em um objeto contido em esquema. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ALL  
 Conceder ALL não concede todas as permissões possíveis. Conceder ALL é equivalente a conceder todas as 92 permissões [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)] aplicáveis ao objeto especificado. O significado ALL varia desta forma:  
  
- Permissões de função escalar: EXECUTE, REFERENCES.  
- Permissões de função com valor de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
- Permissões de procedimento armazenado: EXECUTE.  
- Permissões de tabela: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
- Permissões de exibição: DELETE, INSERT, REFERENCES, SELECT, UPDATE.  
  
PRIVILEGES  
 Incluído para conformidade com 92 [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]. Não altera o comportamento de ALL.  
  
*coluna*  
 Especifica o nome de uma coluna em uma tabela, exibição ou função com valor de tabela na qual a permissão está sendo concedida. Os parênteses () são necessários. Apenas permissões SELECT, REFERENCES e UPDATE podem ser concedidas em uma coluna. *coluna* pode ser especificado na cláusula de permissões ou depois do nome protegível.  
  
> [!CAUTION]  
>  Um DENY em nível de tabela não tem precedência sobre um GRANT em nível de coluna. Essa inconsistência na hierarquia de permissões foi preservada para compatibilidade com versões anteriores.  
  
 ON [objeto::] [ *schema_name* ]. *object_name*  
 Especifica o objeto no qual a permissão está sendo concedida. A frase OBJECT será opcional se *schema_name* for especificado. Se a frase OBJECT for usada, o qualificador de escopo (::) será necessário. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema (.) é necessário.  
  
 PARA \<database_principal >  
 Especifica a entidade de segurança para o qual a permissão está sendo concedida.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS \<database_principal > especifica uma entidade da qual o principal que executa esta consulta deriva seu direito de conceder a permissão.  
  
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
  
## <a name="remarks"></a>Comentários  
  
> [!IMPORTANT]  
>  Uma combinação das permissões ALTER e REFERENCE em alguns casos pode permitir ao usuário autorizado exibir dados ou executar funções não autorizadas. Por exemplo: um usuário com permissão ALTER em uma tabela e permissão REFERENCE em uma função pode criar uma coluna computada em uma função e fazer com que seja executada. Nesse caso, o usuário também precisará da permissão SELECT na coluna computada.  
  
 As informações sobre objetos são visível em várias exibições do catálogo. Para obter mais informações, consulte [exibições de catálogo de objeto &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md).  
  
 Um objeto é um protegível em nível de esquema contido pelo esquema que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um objeto são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de objeto|Implícito na permissão de objeto|Implícito na permissão de esquema|  
|-----------------------|----------------------------------|----------------------------------|  
|ALTER|CONTROL|ALTER|  
|CONTROL|CONTROL|CONTROL|  
|DELETE|CONTROL|DELETE|  
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
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se você estiver usando a opção AS, os requisitos adicionais a seguir serão aplicáveis.  
  
|AS|Permissão adicional necessária|  
|--------|------------------------------------|  
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-select-permission-on-a-table"></a>A. Concedendo a permissão SELECT em uma tabela  
 O exemplo a seguir concede a permissão `SELECT` ao usuário `RosaQdM` na tabela `Person.Address` do banco de dados `AdventureWorks2012`.  
  
```  
GRANT SELECT ON OBJECT::Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="b-granting-execute-permission-on-a-stored-procedure"></a>B. Concedendo a permissão EXECUTE em um procedimento armazenado  
 O exemplo a seguir concede a permissão `EXECUTE` no procedimento armazenado `HumanResources.uspUpdateEmployeeHireInfo` para uma função de aplicativo chamada `Recruiting11`.  
  
```  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO   
```  
  
### <a name="c-granting-references-permission-on-a-view-with-grant-option"></a>C. Concedendo a permissão REFERENCES em uma exibição com GRANT OPTION  
 O exemplo a seguir concede a permissão `REFERENCES` na coluna `BusinessEntityID` na exibição `HumanResources.vEmployee` para o usuário `Wanida` com `GRANT OPTION`.  
  
```  
GRANT REFERENCES (BusinessEntityID) ON OBJECT::HumanResources.vEmployee   
    TO Wanida WITH GRANT OPTION;  
GO  
```  
  
### <a name="d-granting-select-permission-on-a-table-without-using-the-object-phrase"></a>D. Concedendo a permissão SELECT em uma tabela sem usar a frase OBJECT  
 O exemplo a seguir concede a permissão `SELECT` ao usuário `RosaQdM` na tabela `Person.Address` do banco de dados `AdventureWorks2012`.  
  
```  
GRANT SELECT ON Person.Address TO RosaQdM;  
GO  
```  
  
### <a name="e-granting-select-permission-on-a-table-to-a-domain-account"></a>E. Concedendo a permissão SELECT em uma tabela a uma conta de domínio  
 O exemplo a seguir concede a permissão `SELECT` ao usuário `AdventureWorks2012\RosaQdM` na tabela `Person.Address` do banco de dados `AdventureWorks2012`.  
  
```  
GRANT SELECT ON Person.Address TO [AdventureWorks2012\RosaQdM];  
GO  
```  
  
### <a name="f-granting-execute-permission-on-a-procedure-to-a-role"></a>F. Concedendo a permissão EXECUTE em um procedimento a uma função  
 O seguinte exemplo cria uma função e concede a permissão `EXECUTE` à função no procedimento `uspGetBillOfMaterials` do banco de dados `AdventureWorks2012`.  
  
```  
CREATE ROLE newrole ;  
GRANT EXECUTE ON dbo.uspGetBillOfMaterials TO newrole ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Permissões de objeto DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-object-permissions-transact-sql.md)   
 [REVOGAR permissões de objeto &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-object-permissions-transact-sql.md)   
 [Exibições de catálogo de objeto &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)  
  
  

