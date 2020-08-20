---
description: Permissões GRANT de credencial no escopo do banco de dados (Transact-SQL)
title: Credencial GRANT no escopo do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- GRANT DATABASE SCOPED CREDENTIAL
- GRANT_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], database scoped credential
- permissions [SQL Server], database scoped credential
- database scoped credential [SQL Server], permissions
- GRANT statement, database scoped credentials
ms.assetid: 501f2c8a-6aeb-41af-bf0b-974d17af33c0
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f65bf32fb857b5039f6a48e26d48a8f49eca5a04
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472220"
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>Permissões GRANT de credencial no escopo do banco de dados (Transact-SQL)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  Concede permissões em uma credencial no escopo do banco de dados. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *permission*  
 Especifica uma permissão que pode ser concedida em uma credencial no escopo do banco de dados. Listada abaixo.  
  
 ON DATABASE SCOPED CREDENTIAL **::** _credential_name_  
 Especifica a credencial no escopo do banco de dados na qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
 *database_principal*  
 Especifica a entidade de segurança para o qual a permissão está sendo concedida. Um dos seguintes:  
  
-   usuário de banco de dados  
-   função de banco de dados  
-   função de aplicativo  
-   usuário de banco de dados mapeado para um logon do Windows  
-   usuário de banco de dados mapeado para um grupo do Windows  
-   usuário de banco de dados mapeado para um certificado  
-   usuário de banco de dados mapeado para uma chave assimétrica  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
AS *granting_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa esta consulta deriva seu direito de conceder a permissão. Um dos seguintes:  
  
-   usuário de banco de dados  
-   função de banco de dados  
-   função de aplicativo  
-   usuário de banco de dados mapeado para um logon do Windows  
-   usuário de banco de dados mapeado para um grupo do Windows  
-   usuário de banco de dados mapeado para um certificado  
-   usuário de banco de dados mapeado para uma chave assimétrica  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
## <a name="remarks"></a>Comentários  
 Uma credencial no escopo do banco de dados é um item protegível no nível do banco de dados contido pelo banco de dados pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma credencial no escopo do banco de dados estão listadas abaixo, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de credencial no escopo do banco de dados|Implícito pela permissão de credencial no escopo do banco de dados|Implícito na permissão de banco de dados|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se a opção AS for usada, esses requisitos adicionais se aplicarão.  
  
|AS *granting_principal*|Permissão adicional necessária|  
|------------------------------|------------------------------------|  
|Usuário de banco de dados|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um logon do Windows|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|A permissão IMPERSONATE no usuário, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa **db_securityadmin**, associação na função de banco de dados fixa **db_owner** ou associação na função de servidor fixa **sysadmin**.|  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 As entidades autorizadas com a permissão CONTROL SERVER, como os membros da função de servidor fixa **sysadmin**, podem conceder qualquer permissão em qualquer protegível do servidor. As entidades autorizadas com a permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa **db_owner**, podem conceder qualquer permissão para qualquer protegível do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="see-also"></a>Consulte Também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Credencial REVOKE no escopo do banco de dados (Transact-SQL)](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [Credencial no escopo do banco de dados DENY (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
