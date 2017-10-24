---
title: "Permissões de banco de dados Principal REVOKE (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- REVOKE statement, roles
- database user permissions [SQL Server]
- REVOKE statement, users
- application roles [SQL Server], permissions
ms.assetid: c45e1086-c25b-48bb-a764-4a893e983db2
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: eee64655f9ac49775692d88ff6bcd95fd7ff28f4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-database-principal-permissions-transact-sql"></a>Permissões de principal do banco de dados REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoga permissões concedidas ou negadas em um usuário de banco de dados, função de banco de dados ou função de aplicativo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
       | [ ROLE :: database_role ]  
       | [ APPLICATION ROLE :: application_role ]  
    }  
    { FROM | TO } <database_principal> [ ,...n ]  
        [ CASCADE ]  
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
 *permissão*  
 Especifica uma permissão que pode ser revogada no principal de banco de dados. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 USUÁRIO::*database_user*  
 Especifica a classe e o nome do usuário no qual a permissão está sendo revogada. O qualificador de escopo (**::**) é necessária.  
  
 FUNÇÃO::*database_role*  
 Especifica a classe e o nome da função na qual a permissão está sendo revogada. O qualificador de escopo (**::**) é necessária.  
  
 FUNÇÃO de aplicativo::*application_role*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Especifica a classe e o nome da função de aplicativo na qual a permissão está sendo revogada. O qualificador de escopo (**::**) é necessária.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS \<database_principal > especifica uma entidade da qual o principal que executa esta consulta deriva seu direito de revogar a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Especifica uma função de aplicativo.  
  
 *Database_user_mapped_to_Windows_User*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um usuário do Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um grupo do Windows.  
  
 *Database_user_mapped_to_certificate*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para uma chave assimétrica.  
  
 *Database_user_with_no_login*  
 Especifica um usuário do banco de dados sem nenhuma entidade de segurança correspondente no nível de servidor.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="database-user-permissions"></a>Permissões do usuário do banco de dados  
 Um usuário do banco de dados é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em um usuário de banco de dados são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do usuário do banco de dados|Indicado pela permissão do usuário do banco de dados|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>Permissões da função de banco de dados  
 Uma função de banco de dados é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma função de banco de dados são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão da função de banco de dados|Indicado pela permissão da função de banco de dados|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>Permissões de função de aplicativo  
 Uma função de aplicativo é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma função de aplicativo são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de função de aplicativo|Indicado pela permissão de função de aplicativo|Implícito na permissão de banco de dados|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no principal especificado ou uma permissão mais alta que implica a permissão CONTROL.  
  
 Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros do **db_owner** função de banco de dados fixa, podem conceder qualquer permissão em qualquer protegível no banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-revoking-control-permission-on-a-user-from-another-user"></a>A. Revogando a permissão CONTROL em um usuário a partir de outro usuário  
 O exemplo a seguir revoga a permissão `CONTROL` no usuário `Wanida` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a partir do usuário `RolandX`.  
  
```  
USE AdventureWorks2012;  
REVOKE CONTROL ON USER::Wanida FROM RolandX;  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-on-a-role-from-a-user-to-which-it-was-granted-with-grant-option"></a>B. Revogando a permissão VIEW DEFINITION em uma função de um usuário para o qual foi concedida a permissão WITH GRANT OPTION  
 O exemplo a seguir revoga a permissão `VIEW DEFINITION` na função `SammamishParking` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] a partir do usuário de banco de dados `JinghaoLiu`. A opção `CASCADE` é especificada porque ao usuário `JinghaoLiu` foi concedida a permissão `VIEW DEFINITION` `WITH GRANT OPTION`.  
  
```  
USE AdventureWorks2012;  
REVOKE VIEW DEFINITION ON ROLE::SammamishParking   
    FROM JinghaoLiu CASCADE;  
GO  
```  
  
### <a name="c-revoking-impersonate-permission-on-a-user-from-an-application-role"></a>C. Revogando a permissão PERSONATE em um usuário de uma função de aplicativo  
 O exemplo a seguir revoga a permissão `IMPERSONATE` no usuário `HamithaL` da função de aplicativo `AccountsPayable17` do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
```  
USE AdventureWorks2012;  
REVOKE IMPERSONATE ON USER::HamithaL FROM AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>Consulte também  
 [CONCEDER permissões de entidade de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)   
 [Negar permissões de Principal de banco de dados &#40; Transact-SQL &#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [database_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [Criar função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Criar função &#40; Transact-SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  


