---
title: Permissões de entidade de segurança de banco de dados GRANT
description: Conceda permissões em um usuário de banco de dados, função de banco de dados ou função de aplicativo.
titleSuffix: SQL Server (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 03/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], permissions
- permissions [SQL Server], database roles
- granting permissions [SQL Server], database users
- granting permissions [SQL Server], application roles
- granting permissions [SQL Server], database roles
- database user permissions [SQL Server]
- permissions [SQL Server], application roles
- permissions [SQL Server], database users
- GRANT statement, users
- GRANT statement, roles
- application roles [SQL Server], permissions
ms.assetid: 012588a2-cbe1-48f0-a731-b4a2b83203d5
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f67acd0d94ed59a45c8e8d2cbeff0b8cfd9bd68d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246155"
---
# <a name="grant-database-principal-permissions-transact-sql"></a>Permissões de principal do banco de dados GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Concede permissões em um usuário de banco de dados, uma função de banco de dados ou uma função de aplicativo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT permission [ ,...n ]    
    ON   
    {  [ USER :: database_user ]  
     | [ ROLE :: database_role ]  
     | [ APPLICATION ROLE :: application_role ]  
    }  
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
 Especifica uma permissão que pode ser concedida na entidade do banco de dados. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 USER ::*database_user*  
 Especifica a classe e o nome do usuário no qual a permissão está sendo concedida. O qualificador de escopo (::) é necessário.  
  
 ROLE ::*database_role*  
 Especifica a classe e o nome da função na qual a permissão está sendo concedida. O qualificador de escopo (::) é necessário.  
  
 APPLICATION ROLE ::*application_role*  
   
 Especifica a classe e o nome da função de aplicativo na qual a permissão está sendo concedida. O qualificador de escopo (::) é necessário.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS \<database_principal>  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa esta consulta deriva seu direito de conceder a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
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
 Informações sobre as entidades de banco de dados estão visíveis na exibição do catálogo [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Informações sobre permissões do nível de banco de dados estão visíveis na exibição do catálogo [sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md).  
  
## <a name="database-user-permissions"></a>Permissões do usuário do banco de dados  
 Um usuário do banco de dados é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um usuário de banco de dados estão listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do usuário do banco de dados|Indicado pela permissão do usuário do banco de dados|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|IMPERSONATE|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY USER|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="database-role-permissions"></a>Permissões da função de banco de dados  
 Uma função de banco de dados é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um função de banco de dados estão listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão da função de banco de dados|Indicado pela permissão da função de banco de dados|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="application-role-permissions"></a>Permissões de função de aplicativo  
 Uma função de aplicativo é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma função de aplicativo são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de função de aplicativo|Indicado pela permissão de função de aplicativo|Implícito na permissão de banco de dados|  
|---------------------------------|--------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY APPLICATION ROLE|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se você estiver usando a opção AS, os requisitos adicionais a seguir serão aplicáveis.  
  
|AS *granting_principal*|Permissão adicional necessária|  
|------------------------------|------------------------------------|  
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um usuário do Windows|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação à função de banco de dados fixa db_securityadminfixed, associação à função de banco de dados fixa db_owner ou associação à função de servidor fixa sysadmin.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadminfixed, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
  
 As entidades que têm a permissão CONTROL em um protegível podem conceder a permissão nesse protegível.  
  
 Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem conceder qualquer permissão para qualquer item de segurança do banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-control-permission-on-a-user-to-another-user"></a>a. Concessão da permissão CONTROL em um usuário para outro usuário  
 O exemplo a seguir concede a permissão `CONTROL` no usuário `AdventureWorks2012``Wanida` para o usuário `RolandX`.  
  
```  
GRANT CONTROL ON USER::Wanida TO RolandX;  
GO  
```  
  
### <a name="b-granting-view-definition-permission-on-a-role-to-a-user-with-grant-option"></a>B. Concessão da permissão VIEW DEFINITION em uma função para um usuário com GRANT OPTION  
 O exemplo a seguir concede permissão `VIEW DEFINITION` em `AdventureWorks2012` função `SammamishParking` junto com `GRANT OPTION` para usuário de banco de dados `JinghaoLiu`.  
  
```  
GRANT VIEW DEFINITION ON ROLE::SammamishParking   
    TO JinghaoLiu WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-impersonate-permission-on-a-user-to-an-application-role"></a>C. Concessão da permissão IMPERSONATE em um usuário para uma função de aplicativo  
 O exemplo a seguir concede permissão no usuário `IMPERSONATE``HamithaL` para `AdventureWorks2012` função de aplicativo `AccountsPayable17`.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
```  
GRANT IMPERSONATE ON USER::HamithaL TO AccountsPayable17;  
GO    
```  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões DENY da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/deny-database-principal-permissions-transact-sql.md)   
 [Permissões REVOKE da entidade de segurança do banco de dados &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-database-principal-permissions-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
  
  
