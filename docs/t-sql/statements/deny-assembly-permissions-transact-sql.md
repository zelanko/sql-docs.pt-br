---
title: Permissões DENY de assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- assemblies [CLR integration], permissions
- DENY statement, assemblies
- denying permissions [SQL Server], assemblies
ms.assetid: be0896b3-f793-44c9-9390-1c6e58f33b2b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 40782bb4779bc2cad0b758cf5ab2c56862d9c35b
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634518"
---
# <a name="deny-assembly-permissions-transact-sql"></a>Permissões de assembly DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega permissões em um assembly.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
DENY { permission [ ,...n ] } ON ASSEMBLY :: assembly_name  
    TO database_principal [ ,...n ]   
        [ CASCADE ]  
        [ AS denying_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser negada em um assembly. Listada abaixo.  
  
 ON ASSEMBLY **::** _assembly_name_  
 Especifica o assembly no qual a permissão está sendo negada. O qualificador de escopo "::" é obrigatório.  
  
 *database_principal*  
 Especifica a entidade à qual a permissão está sendo negada. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 *denying_principal*  
 Especifica uma entidade de segurança da qual a entidade de segurança que executa essa consulta deriva seu direito de negar a permissão. Um dos seguintes:  
  
-   usuário de banco de dados  
  
-   função de banco de dados  
  
-   função de aplicativo  
  
-   usuário de banco de dados mapeado para um logon do Windows  
  
-   usuário de banco de dados mapeado para um grupo do Windows  
  
-   usuário de banco de dados mapeado para um certificado  
  
-   usuário de banco de dados mapeado para uma chave assimétrica  
  
-   usuário de banco de dados não mapeado para uma entidade do servidor.  
  
## <a name="remarks"></a>Comentários  
 Um assembly é um nível de banco de dados protegível contido no banco de dados que é pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um assembly estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de assembly|Implícito na permissão de assembly|Implícito na permissão de banco de dados|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL no assembly. Se for usada a opção AS, o principal especificado deverá ser proprietário do assembly.  
  
## <a name="see-also"></a>Consulte Também  
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
