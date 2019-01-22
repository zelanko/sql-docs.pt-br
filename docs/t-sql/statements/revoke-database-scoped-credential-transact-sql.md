---
title: Credencial REVOKE no escopo do banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- REVOKE DATABASE SCOPED CREDENTIAL
- REVOKE_DATABASE_SCOPED_CREDENTIAL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVOKE statements, database scoped credentials
- revoking permissions [SQL Server], database scoped credentials
ms.assetid: b73233c5-9afa-48ca-ba34-a9f86b9b1d2e
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d0a4ea1f4977440ee53835f3c96ab5e60b3083ba
ms.sourcegitcommit: c6e71ed14198da67afd7ba722823b1af9b4f4e6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2019
ms.locfileid: "54326097"
---
# <a name="revoke-database-scoped-credential-transact-sql"></a>Credencial REVOKE no escopo do banco de dados (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  Revoga permissões em uma credencial no escopo do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON DATABASE SCOPED CREDENTIAL :: credential_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 GRANT OPTION FOR  
 Indica que a habilidade de conceder a permissão especificada será revogada. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 *permission*  
 Especifica uma permissão que pode ser revogada em uma credencial no escopo do banco de dados. Listada abaixo.  
  
 ON CERTIFICATE **::**_credential_name_  
 Especifica a credencial no escopo do banco de dados na qual a permissão está sendo revogada. O qualificador de escopo "::" é obrigatório.  
  
 *database_principal*  
 Especifica a entidade a partir da qual a permissão está sendo revogada. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também será revogada em outros principais aos quais ela foi concedida por este principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *revoking_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que está executando essa consulta deriva seu direito de revogar a permissão. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
## <a name="remarks"></a>Remarks  
 Uma credencial no escopo do banco de dados é um item protegível no nível do banco de dados contido pelo banco de dados pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma credencial no escopo do banco de dados estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de credencial no escopo do banco de dados|Implícito pela permissão de credencial no escopo do banco de dados|Implícito na permissão de banco de dados|  
|----------------------------|---------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão CONTROL na credencial no escopo do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [REVOKE (Transact-SQL)](../../t-sql/statements/revoke-transact-sql.md)      
 [Credencial GRANT no escopo do banco de dados (Transact-SQL)](../../t-sql/statements/grant-database-scoped-credential-transact-sql.md)   
 [Credencial no escopo do banco de dados DENY (Transact-SQL)](../../t-sql/statements/deny-database-scoped-credential-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
