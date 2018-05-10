---
title: Permissões GRANT de tipo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], types
- granting permissions [SQL Server], types
- GRANT statement, types
- type permissions [SQL Server]
ms.assetid: 14bd2fb3-1446-49c0-be87-c6a670317ed0
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0b2b0f79808be5eb940429e2d6b38004703bcbea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="grant-type-permissions-transact-sql"></a>Permissões de tipo GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permissões em um tipo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 *permission*  
 Especifica uma permissão que pode ser concedida em um tipo. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ON TYPE **::** [ *schema_name***.** ] *type_name*  
 Especifica o tipo em que a permissão está sendo concedida. O qualificador de escopo (**::**) é obrigatório. Se *schema_name* não for especificado, o esquema padrão será usado. Se *schema_name* for especificado, o qualificador de escopo de esquema (**.**) será obrigatório.  
  
 TO \<database_principal> Especifica a entidade de segurança para a qual a permissão está sendo concedida.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS \<database_principal> Especifica uma entidade de segurança por meio da qual a entidade de segurança que executa essa consulta obtém seu direito de conceder a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]
  
 Especifica uma função de aplicativo.  
  
 *Database_user_mapped_to_Windows_User*  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um usuário do Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um grupo do Windows.  
  
 *Database_user_mapped_to_certificate*  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para um certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica um usuário do banco de dados mapeado para uma chave assimétrica.  
  
 *Database_user_with_no_login*  
 Especifica um usuário do banco de dados sem nenhuma entidade de segurança correspondente no nível de servidor.  
  
## <a name="remarks"></a>Remarks  
 Um tipo é um protegível no nível de esquema contido no esquema pai na hierarquia de permissões.  
  
> [!IMPORTANT]  
>  As permissões **GRANT**, **DENY,** e **REVOKE** não se aplicam a tipos de sistema. Podem ser concedidas permissões a tipos definidos pelo usuário. Para obter mais informações sobre tipos definidos pelo usuário, veja [Trabalhando com tipos definidos pelo usuário no SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md).  
  
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
|Usuário de banco de dados|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um logon do Windows|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir concede a permissão `VIEW DEFINITION` com `GRANT OPTION` no tipo `PhoneNumber` definido pelo usuário ao usuário `KhalidR`. `PhoneNumber` está localizado no esquema `Telemarketing`.  
  
```  
GRANT VIEW DEFINITION ON TYPE::Telemarketing.PhoneNumber   
    TO KhalidR WITH GRANT OPTION;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões DENY de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/deny-type-permissions-transact-sql.md)   
 [Permissões REVOKE de tipo &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-type-permissions-transact-sql.md)   
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Securables](../../relational-databases/security/securables.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  

