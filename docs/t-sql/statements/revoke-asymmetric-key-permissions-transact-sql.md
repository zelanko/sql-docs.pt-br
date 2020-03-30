---
title: Permissões REVOKE de chave assimétrica (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- REVOKE statement, asymmetric keys
ms.assetid: 1a1063e8-ffc7-4775-a40d-e155740ad7b2
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: baf3fd0a03beb185a43180599352b6f64f8044cc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68082365"
---
# <a name="revoke-asymmetric-key-permissions-transact-sql"></a>Permissões de chave assimétrica REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoga permissões em uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 *permission*  
 Especifica uma permissão que pode ser revogada em um assembly. Listada abaixo.  
  
 ON ASYMMETRIC KEY **::** _asymmetric_key_name_  
 Especifica a chave assimétrica na qual a permissão está sendo revogada. O qualificador de escopo **::** é obrigatório.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
