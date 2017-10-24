---
title: "REVOGAR permissões de chave simétrica (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
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
- symmetric keys [SQL Server], permissions
- permissions [SQL Server], symmetric keys
- REVOKE statement, symmetric keys
ms.assetid: 091da030-a768-4aa3-9509-cc23bd719cea
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cf946b948a1bd79fbcf017833e708e545c6ffba5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-symmetric-key-permissions-transact-sql"></a>Permissões de chave simétrica REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Revoga permissões concedidas e negadas em uma chave simétrica.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ]    
    ON SYMMETRIC KEY :: symmetric_key_name   
        { TO | FROM } <database_principal> [ ,...n ]   
    [ CASCADE ]  
    [ AS <database_principal> ]  
  
<database_principal> ::=   
        Database_user   
    | Database_role   
    | Application_role   
    | Database_user_mapped_to_Windows_User   
    | Database_user_mapped_to_Windows_Group   
    | Database_user_mapped_to_certificate   
    | Database_user_mapped_to_asymmetric_key   
    | Database_user_with_no_login   
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser revogada em uma chave simétrica. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CHAVE SIMÉTRICA de ON:: *asymmetric_key_name*  
 Especifica a chave simétrica na qual a permissão está sendo revogada. O qualificador de escopo (::) é necessário.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 {PARA | FROM} \< *database_principal*>  
 Especifica a entidade a partir da qual a permissão está sendo revogada.  
  
 AS \<database_principal > especifica uma entidade da qual o principal que executa esta consulta deriva seu direito de revogar a permissão.  
  
 *Database_user*  
 Especifica um usuário do banco de dados.  
  
 *Database_role*  
 Especifica uma função de banco de dados.  
  
 *Application_role*  
 Especifica uma função de aplicativo.  
  
 *Database_user_mapped_to_Windows_User*  
 Especifica um usuário do banco de dados mapeado para um usuário do Windows.  
  
 *Database_user_mapped_to_Windows_Group*  
 Especifica um usuário do banco de dados mapeado para um grupo do Windows.  
  
 *Database_user_mapped_to_certificate*  
 Especifica um usuário do banco de dados mapeado para um certificado.  
  
 *Database_user_mapped_to_asymmetric_key*  
 Especifica um usuário do banco de dados mapeado para uma chave assimétrica.  
  
 *Database_user_with_no_login*  
 Especifica um usuário do banco de dados sem nenhuma entidade de segurança correspondente no nível de servidor.  
  
## <a name="remarks"></a>Comentários  
 Informações sobre chaves simétricas são visíveis no [symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md) exibição do catálogo.  
  
 A instrução falhará se CASCADE não for especificado ao revogar uma permissão de uma entidade à qual ela foi concedida com GRANT OPTION especificado.  
  
 Uma chave simétrica é um protegível no nível de banco de dados contido no banco de dados pai na hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em uma chave simétrica são listadas na tabela a seguir, junto com as permissões mais gerais que as incluem implicitamente.  
  
|Permissão de chave simétrica|Implícita na permissão de chave simétrica|Implícito na permissão de banco de dados|  
|------------------------------|-----------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY SYMMETRIC KEY|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL na chave simétrica ou a permissão ALTER ANY SYMMETRIC KEY no banco de dados. Se você usar a opção AS, a entidade especificada deverá ser proprietária da chave simétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir revoga a permissão `ALTER` na chave simétrica `SamInventory42` do usuário `HamidS` e de todas as entidades às quais `HamidS` concedeu a permissão `ALTER`.  
  
```  
USE AdventureWorks2012;  
REVOKE ALTER ON SYMMETRIC KEY::SamInventory42 TO HamidS CASCADE;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [symmetric_keys & #40; Transact-SQL & #41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [CONCEDER permissões de chave simétrica & #40; Transact-SQL & #41;](../../t-sql/statements/grant-symmetric-key-permissions-transact-sql.md)   
 [Negar permissões de chave simétrica & #40; Transact-SQL & #41;](../../t-sql/statements/deny-symmetric-key-permissions-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Hierarquia de criptografia](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  


