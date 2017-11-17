---
title: Credencial (Transact-SQL) no escopo do banco de dados GRANT | Microsoft Docs
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8fff82fbd6c81fea9cd9a7a95cabf35b0b8ecb7f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-database-scoped-credential-permissions-transact-sql"></a>No escopo do banco de dados de concessão de permissões de credencial (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Credencial com escopo concede permissões em um banco de dados. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT permission  [ ,...n ]    
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    TO principal [ ,...n ] [ WITH GRANT OPTION ]   
    [ AS granting_principal ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser concedida em um banco de dados de credencial com escopo. Listada abaixo.  
  
 NA CREDENCIAL no escopo do banco de dados **::***credential_name*  
 Especifica a credencial no escopo do banco de dados no qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
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
 Uma credencial no escopo do banco de dados é um banco de dados-nível protegível contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma credencial no escopo do banco de dados estão listadas abaixo, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de credencial no escopo do banco de dados|Indicado pela permissão de credencial no escopo do banco de dados|Implícito na permissão de banco de dados|  
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
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin**função de servidor fixa.|  
|Usuário de banco de dados mapeado para um certificado|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação a **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados ou associação no **sysadmin** função de servidor fixa.|  
|Função de banco de dados|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
|Função de aplicativo|A permissão ALTER na função, associação no **db_securityadmin** função fixa de banco de dados, associação ao **db_owner** fixo de função de banco de dados, ou a associação a **sysadmin**função de servidor fixa.|  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros do **sysadmin** função de servidor fixa, podem conceder qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros do **db_owner** função de banco de dados fixa, podem conceder qualquer permissão em qualquer protegível no banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="see-also"></a>Consulte também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Credencial (Transact-SQL) no escopo do banco de dados REVOKE](../../t-sql/statements/revoke-database-scoped-credential-transact-sql.md)   
 [DENY (Transact-SQL) de credencial no escopo do banco de dados](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

