---
title: "Permissões do tipo GRANT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
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
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: aebb1443c7cdf98581a54b5a8a507c021719cc87
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="grant-type-permissions-transact-sql"></a>Permissões de tipo GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permissões em um tipo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GRANT permission  [ ,...n ] ON TYPE :: [ schema_name . ] type_name  
    TO <database_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
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
 Especifica uma permissão que pode ser concedida em um tipo. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 NO tipo **::** [ *schema_name***.** ] *type_name*  
 Especifica o tipo em que a permissão está sendo concedida. O qualificador de escopo (**::**) é necessária. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema (**.**) é necessária.  
  
 PARA \<database_principal > especifica a entidade à qual a permissão está sendo concedida.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS \<database_principal > especifica uma entidade da qual o principal que executa esta consulta deriva seu direito de conceder a permissão.  
  
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
 Um tipo é um protegível no nível de esquema contido no esquema pai na hierarquia de permissões.  
  
> [!IMPORTANT]  
>  **GRANT**, **DENY,** e **REVOGAR** permissões não se aplicam a tipos de sistema. Podem ser concedidas permissões a tipos definidos pelo usuário. Para obter mais informações sobre tipos definidos pelo usuário, consulte [trabalhando com tipos definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md).  
  
 As permissões mais específicas e limitadas que podem ser concedidas em um tipo são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Tipo de permissão|Implícita na permissão de tipo|Implícito na permissão de esquema|  
|---------------------|--------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|Execute|CONTROL|Execute|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se você estiver usando a opção AS, os requisitos adicionais a seguir serão aplicáveis.  
  
|AS|Permissão adicional necessária|  
|--------|------------------------------------|  
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin**função de servidor fixa.|  
|Usuário de banco de dados mapeado para um certificado|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Função de banco de dados|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
|Função de aplicativo|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir concede a permissão `VIEW DEFINITION` com `GRANT OPTION` no tipo `PhoneNumber` definido pelo usuário ao usuário `KhalidR`. `PhoneNumber`está localizado no esquema `Telemarketing`.  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Negar permissões do tipo &#40; Transact-SQL &#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [Permissões do tipo REVOKE &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

