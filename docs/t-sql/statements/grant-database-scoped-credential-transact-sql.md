---
title: Credencial GRANT no escopo do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/19/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 3
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: e5b235e2066ff41b8fffb24f352d9362ddd3b5a8
ms.sourcegitcommit: 00ffbc085c5a4b792646ec8657495c83e6b851b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2018
ms.locfileid: "36941572"
---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>Permissões GRANT de credencial no escopo do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Concede permissões em uma credencial no escopo do banco de dados. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser concedida em uma credencial no escopo do banco de dados. Listada abaixo.  
  
 ON DATABASE SCOPED CREDENTIAL **::***credential_name*  
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
  
## <a name="remarks"></a>Remarks  
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
  
  
