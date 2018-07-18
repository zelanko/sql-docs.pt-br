---
title: Permissões GRANT de assembly (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], assemblies
- assemblies [CLR integration], permissions
- GRANT statement, assemblies
ms.assetid: dce1e027-f859-4967-bdda-16a95ae460d0
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 10e703ec003d953802cf472e02872f5dc3af423a
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37782107"
---
# <a name="grant-assembly-permissions-transact-sql"></a>Permissões de assembly GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permissões em um assembly.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT { permission [ ,...n ] } ON ASSEMBLY :: assembly_name  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser concedida em um assembly. Listada abaixo.  
  
 ON ASSEMBLY **::***assembly_name*  
 Especifica o assembly no qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
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
 Um assembly é um nível de banco de dados protegível contido no banco de dados que é pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um assembly estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de assembly|Implícito na permissão de assembly|Implícito na permissão de banco de dados|  
|-------------------------|------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASSEMBLY|  
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
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
