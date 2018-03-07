---
title: "Permissões de texto completo GRANT (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/17/2017
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
- granting permissions [SQL Server], full-text
- full-text search [SQL Server], permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
- GRANT statement, full-text permissions
ms.assetid: fdb64e09-222a-47fe-b08b-999264ca261d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 673092fc5f3523d0448e477ceda10ea491224982
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="grant-full-text-permissions-transact-sql"></a>Permissões de texto completo GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Concede permissões em um catálogo de texto completo ou em uma lista de palavras irrelevantes de texto completo.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
GRANT permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 É o nome de uma permissão. Os mapeamentos válidos de permissões para protegíveis são descritos na seção "Comentários", posteriormente neste tópico.  
  
 NO catálogo de texto completo **:: * text_catalog_name completo*  
 Especifica o catálogo de texto completo no qual a permissão está sendo concedida. O qualificador de escopo **::** é necessária.  
  
 EM FULLTEXT STOPLIST **:: * text_stoplist_name completo*  
 Especifica a lista de palavras irrelevantes de texto completo no qual a permissão está sendo concedida. O qualificador de escopo **::** é necessária.  
  
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
  
## <a name="fulltext-catalog-permissions"></a>Permissões FULLTEXT CATALOG  
 Um catálogo de texto completo é um protegível em nível de banco de dados contido no banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um catálogo de texto completo estão listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão do catálogo de texto completo|Implícito na permissão de catálogo de texto completo|Implícito na permissão de banco de dados|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>Permissões FULLTEXT STOPLIST  
 Uma lista de palavras irrelevantes de texto completo é um protegível em nível de banco de dados contido no banco de dados que é seu pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma lista de palavras irrelevantes de texto completo estão listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissões de lista de palavras irrelevantes de texto completo|Implícito na lista de palavras irrelevantes de texto completo|Implícito na permissão de banco de dados|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou a entidade de segurança especificada com a opção AS) deve ter a própria permissão com GRANT OPTION ou uma permissão superior que tenha a permissão que está sendo concedida implícita.  
  
 Se a opção AS for usada, esses requisitos adicionais se aplicarão.  
  
|AS *granting_principal*|Permissão adicional necessária|  
|------------------------------|------------------------------------|  
|Usuário de banco de dados|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um logon do Windows|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um grupo do Windows|Associação no grupo do Windows, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para um certificado|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados mapeado para uma chave assimétrica|Associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Usuário de banco de dados não mapeado para nenhuma entidade de segurança de servidor|Permissão IMPERSONATE no usuário, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de banco de dados|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
|Função de aplicativo|Permissão ALTER na função, associação na função de banco de dados fixa db_securityadmin, associação na função de banco de dados fixa db_owner ou associação na função de servidor fixa sysadmin.|  
  
 Os proprietários de objetos podem conceder permissões nos objetos de sua propriedade. Principais com a permissão CONTROL em um item protegível podem conceder permissão nesse item.  
  
 Os usuários autorizados da permissão CONTROL SERVER, como os membros da função de servidor fixa sysadmin, podem conceder qualquer permissão em qualquer protegível do servidor. Os usuários autorizados da permissão CONTROL em um banco de dados, como os membros da função de banco de dados fixa db_owner, podem conceder qualquer permissão para qualquer item de segurança do banco de dados. Os usuários autorizados da permissão CONTROL em um esquema podem conceder qualquer permissão em qualquer objeto dentro do esquema.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-permissions-to-a-full-text-catalog"></a>A. Concedendo permissões a um catálogo de texto completo  
 O seguinte exemplo concede a `Ted` a permissão `CONTROL` no catálogo de texto completo `ProductCatalog`.  
  
```  
GRANT CONTROL  
    ON FULLTEXT CATALOG :: ProductCatalog  
    TO Ted ;  
```  
  
### <a name="b-granting-permissions-to-a-stoplist"></a>B. Concedendo permissões a uma lista de palavras irrelevantes  
 O seguinte exemplo concede a `Mary` a permissão `VIEW DEFINITION` na lista de palavras irrelevantes de texto completo `ProductStoplist`.  
  
```  
GRANT VIEW DEFINITION  
    ON FULLTEXT STOPLIST :: ProductStoplist  
    TO Mary ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CRIAR o catálogo de texto completo &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
