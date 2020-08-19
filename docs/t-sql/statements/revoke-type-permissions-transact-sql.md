---
description: Permissões de tipo REVOKE (Transact-SQL)
title: Permissões REVOKE de tipo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statement, types
- permissions [SQL Server], types
- type permissions [SQL Server]
ms.assetid: 3969c7e9-ca10-4c67-971b-25d2dfccf650
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 3565cb96bc39b1f51cf5c1c64a25abf1766ad695
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426478"
---
# <a name="revoke-type-permissions-transact-sql"></a>Permissões de tipo REVOKE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Revoga permissões em um tipo.  
  
  ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]   
    ON TYPE :: [ schema_name ]. type_name   
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
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *permission*  
 Especifica uma permissão que pode ser revogada em um tipo. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ON TYPE **::** [ *schema_name* ] **.** *type_name*  
 Especifica o tipo no qual a permissão está sendo revogada. O qualificador de escopo ( **::** ) é obrigatório. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema ( **.** ) será obrigatório.  
  
 { FROM | TO } \<database_principal> Especifica a entidade de segurança da qual a permissão está sendo revogada.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS \<database_principal> Especifica uma entidade de segurança da qual a entidade de segurança que está executando essa consulta deriva o seu direito de revogar a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Especifica uma função de aplicativo.  
  
 *Database_user_mapped_to_Windows_User*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica um usuário do banco de dados mapeado para um usuário do Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica um usuário do banco de dados mapeado para um grupo do Windows.  
  
 *Database_user_mapped_to_certificate*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica um usuário do banco de dados mapeado para um certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 Especifica um usuário do banco de dados mapeado para uma chave assimétrica.  
  
 *Database_user_with_no_login*  
 Especifica um usuário do banco de dados sem nenhuma entidade de segurança correspondente no nível de servidor.  
  
## <a name="remarks"></a>Comentários  
 Um tipo é um protegível no nível de esquema contido no esquema pai na hierarquia de permissões.  
  
> [!IMPORTANT]  
>  As permissões **GRANT**, **DENY,** e **REVOKE** não se aplicam a tipos de sistema. Podem ser concedidas permissões a tipos definidos pelo usuário. Para obter mais informações sobre tipos definidos pelo usuário, veja [Trabalhando com tipos definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md).  
  
 As permissões mais específicas e limitadas que podem ser revogadas em um tipo são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Tipo de permissão|Implícita na permissão de tipo|Implícito na permissão de esquema|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|Execute|CONTROL|Execute|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no tipo. Se você usar a cláusula AS, a entidade especificada deverá ser proprietária do tipo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir revoga a permissão `VIEW DEFINITION` no tipo definido pelo usuário `PhoneNumber` no usuário `KhalidR`. A opção `CASCADE` indica que a permissão `VIEW DEFINITION` também será revogada nas entidades de segurança às quais `KhalidR` a concedeu. `PhoneNumber` está localizado no esquema `Telemarketing`.  
  
```  
REVOKE VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    FROM KhalidR CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões GRANT de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/grant-type-permissions-transact-sql.md)   
 [Permissões DENY de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Protegíveis](../../relational-databases/security/securables.md)  
  
  

