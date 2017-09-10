---
title: Esquema DENY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- denying permissions [SQL Server], schemas
- schemas [SQL Server], permissions
- permissions [SQL Server], schemas
- DENY statement, schemas
ms.assetid: 300a67c4-d226-4653-9e9f-7ae4d53fcf33
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7d4d3e3709ff4ad38d8b033afe1569d9c234bfa2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="deny-schema-permissions-transact-sql"></a>Permissões de esquema DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em um esquema.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY permission  [ ,...n ] } ON SCHEMA :: schema_name  
    TO database_principal [ ,...n ]   
    [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode negada em um esquema. Para obter uma lista dessas permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 ESQUEMA ON **::** esquema*Name*  
 Especifica o esquema no qual a permissão está sendo negada. O qualificador de escopo **::** é necessária.  
  
 *database_principal*  
 Especifica a entidade à qual a permissão está sendo negada. *database_principal* pode ser um dos seguintes:  
  
-   Usuário de banco de dados  
-   Função de banco de dados  
-   Função de aplicativo  
-   Usuário de banco de dados mapeado para um logon do Windows  
-   Usuário de banco de dados mapeado para um grupo do Windows  
-   Usuário de banco de dados mapeado para um certificado  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
*denying_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa essa consulta deriva seu direito de negar a permissão. *denying_principal* pode ser um dos seguintes:  
  
-   Usuário de banco de dados  
-   Função de banco de dados  
-   Função de aplicativo  
-   Usuário de banco de dados mapeado para um logon do Windows  
-   Usuário de banco de dados mapeado para um grupo do Windows  
-   Usuário de banco de dados mapeado para um certificado  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
-   Usuário do banco de dados não mapeado para um principal de servidor.  
  
## <a name="remarks"></a>Comentários  
 Um esquema é um protegível no nível de banco de dados contido no banco de dados pai da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um esquema são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
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
 Requer a permissão CONTROL no esquema. Se você estiver usando a opção AS, a entidade especificada deverá ser proprietária do esquema.  
  
## <a name="see-also"></a>Consulte também  
 [Criar esquema &#40; Transact-SQL &#41;](../../t-sql/statements/create-schema-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

