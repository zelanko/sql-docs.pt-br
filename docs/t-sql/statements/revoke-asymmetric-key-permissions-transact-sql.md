---
title: "REVOGAR permissões de chave assimétrica (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/10/2016
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
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d4f9f08fda905261e188bb90f8d85fd0a48b2f2c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>Permissões de chave assimétrica REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoga permissões em uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
    { TO | FROM } database_principal [ ,...n ]  
    [ CASCADE ]  
    [ AS revoking_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 GRANT OPTION FOR  
 Indica que a habilidade de conceder a permissão especificada será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 *permissão*  
 Especifica uma permissão que pode ser revogada em um assembly. Listada abaixo.  
  
 NA chave ASSIMÉTRICA **::***asymmetric_key_name*  
 Especifica a chave assimétrica na qual a permissão está sendo revogada. O qualificador de escopo **::** é necessária.  
  
 *database_principal*  
 Especifica a entidade a partir da qual a permissão está sendo revogada. Um dos seguintes:  
  
-   Usuário de banco de dados  
  
-   Função de banco de dados  
  
-   Função de aplicativo  
  
-   Usuário de banco de dados mapeado para um logon do Windows  
  
-   Usuário de banco de dados mapeado para um grupo do Windows  
  
-   Usuário de banco de dados mapeado para um certificado  
  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
  
-   Usuário de banco de dados não mapeado para um principal do servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal. A permissão em si não será revogada.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *revoking_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que está executando essa consulta deriva seu direito de revogar a permissão. Um dos seguintes:  
  
-   Usuário de banco de dados  
  
-   Função de banco de dados  
  
-   Função de aplicativo  
  
-   Usuário de banco de dados mapeado para um logon do Windows  
  
-   Usuário de banco de dados mapeado para um grupo do Windows  
  
-   Usuário de banco de dados mapeado para um certificado  
  
-   Usuário de banco de dados mapeado para uma chave assimétrica  
  
-   Usuário de banco de dados não mapeado para um principal do servidor.  
  
## <a name="remarks"></a>Comentários  
 Uma chave assimétrica é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser revogadas em uma chave assimétrica estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de chave assimétrica|Indicado pela permissão de chave assimétrica|Implícito na permissão de banco de dados|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave assimétrica.  
  
## <a name="see-also"></a>Consulte também  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Criar função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

