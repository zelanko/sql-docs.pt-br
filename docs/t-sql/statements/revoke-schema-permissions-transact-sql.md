---
title: "REVOGAR permissões de esquema (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
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
- REVOKE statement, schema
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
ms.assetid: a1fabf35-1f42-48db-b0b8-7181f413ba3a
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5519096183afdc88ed800dfb7aa97539499abbe5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-schema-permissions-transact-sql"></a>Permissões de esquema REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoga permissões em um esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission  [ ,...n ]   
    ON SCHEMA :: schema_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser revogada em um esquema. As permissões que podem ser revogadas em um esquema são listadas na seção "Comentários", posteriormente neste tópico.  
  
 GRANT OPTION FOR  
 Indica que o direito de conceder a permissão especificada diretamente a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 ESQUEMA ON **::** esquema*Name*  
 Especifica o esquema no qual a permissão está sendo revogada. O qualificador de escopo **::** é necessária.  
  
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
>  Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
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
  
## <a name="remarks"></a>Comentários  
 Um esquema é um item protegível em nível de banco de dados contido no banco de dados pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um esquema são listadas na tabela a seguir, juntamente com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de esquema|Implícito na permissão de esquema|Implícito na permissão de banco de dados|  
|-----------------------|----------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SCHEMA|  
|CONTROL|CONTROL|CONTROL|  
|CREATE SEQUENCE|ALTER|ALTER ANY SCHEMA|  
|DELETE|CONTROL|DELETE|  
|Execute|CONTROL|Execute|  
|INSERT|CONTROL|INSERT|  
|REFERENCES|CONTROL|REFERENCES|  
|SELECT|CONTROL|SELECT|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|UPDATE|CONTROL|UPDATE|  
|VIEW CHANGE TRACKING|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no esquema.  
  
## <a name="see-also"></a>Consulte também  
 [Criar esquema &#40; Transact-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

