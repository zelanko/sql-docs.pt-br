---
title: "Permissões de chave assimétrica de GRANT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/12/2017
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
- granting permissions [SQL Server], asymmetric keys
- permissions [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], permissions
- GRANT statement, asymmetric keys
ms.assetid: a70e2ee6-59b0-4543-b883-e9cbae6199be
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8c7234246958d82b8c90df9e5ad54d042248cc2d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="grant-asymmetric-key-permissions-transact-sql"></a>Permissões de chave assimétrica GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permissões em uma chave assimétrica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT { permission  [ ,...n ] }   
    ON ASYMMETRIC KEY :: asymmetric_key_name   
       TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser concedida em uma chave assimétrica. Listada abaixo.  
  
 NA chave ASSIMÉTRICA **::***asymmetric_key_name*  
 Especifica a chave assimétrica na qual a permissão está sendo concedida. O qualificador de escopo "::" é obrigatório.  
  
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
 Uma chave assimétrica é um item protegível do nível do banco de dados contido pelo banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma chave assimétrica estão listadas abaixo, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Permissão de chave assimétrica|Indicado pela permissão de chave assimétrica|Implícito na permissão de banco de dados|  
|-------------------------------|------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY ASYMMETRIC KEY|  
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
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [Criar função de aplicativo &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  

