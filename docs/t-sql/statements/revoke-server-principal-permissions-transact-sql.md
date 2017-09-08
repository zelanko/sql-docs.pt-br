---
title: "Permissões de entidade de servidor REVOKE (Transact-SQL) | Microsoft Docs"
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
- REVOKE statement, impersonation
- permissions [SQL Server], impersonation
- permissions [SQL Server], logins
- impersonate [SQL Server], revoking
- logins [SQL Server], revoking
- REVOKE statement, logins
ms.assetid: 75409024-f150-4326-af16-9d60e900df18
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 13dca8052ad8bc74491136c941677606ccecbe3c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="revoke-server-principal-permissions-transact-sql"></a>Permissões do principal do servidor REVOKE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Revoga as permissões concedidas ou negadas em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
REVOKE [ GRANT OPTION FOR ] permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    { FROM | TO } <server_principal> [ ,...n ]  
    [ CASCADE ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey     
    | server_role  
```  
  
## <a name="arguments"></a>Argumentos  
 *permissão*  
 Especifica uma permissão que pode ser revogada em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 LOGON **::** *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual a permissão está sendo revogada. O qualificador de escopo (**::**) é necessária.  
  
 FUNÇÃO de servidor **::** *server_role*  
 Especifica a função de servidor na qual a permissão está sendo revogada. O qualificador de escopo (**::**) é necessária.  
  
 {DO | PARA} \<server_principal > especifica o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon ou função de servidor do qual a permissão está sendo revogada.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 *server_role*  
 Especifica o nome de uma função de servidor definida pelo usuário.  
  
 GRANT OPTION  
 Indica que o direito de conceder a permissão especificada a outros principais será revogado. A permissão em si não será revogada.  
  
> [!IMPORTANT]  
>  Se a entidade de segurança tiver a permissão especificada sem a opção GRANT, a própria permissão será revogada.  
  
 CASCADE  
 Indica que a permissão que está sendo revogada também é revogada de outros principais aos quais ela foi concedida ou negada por esse principal.  
  
> [!CAUTION]  
>  A revogação em cascata de uma permissão WITH GRANT OPTION concedida revogará as opções GRANT e DENY dessa permissão.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do qual o principal que executa esta consulta deriva seu direito de revogar a permissão.  
  
## <a name="remarks"></a>Comentários  
 Os logons e as funções de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são protegíveis no nível do servidor. As permissões mais específicas e limitadas que podem ser revogadas em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou função de servidor são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
|Logon do SQL Server ou função de servidor|Sugerido pelo logon do SQL Server ou função de servidor|Implícito na permissão de servidor|  
|------------------------------------------------|-----------------------------------------------------------|----------------------------------|  
|CONTROL|CONTROL|CONTROL SERVER|  
|IMPERSONATE|CONTROL|CONTROL SERVER|  
|VIEW DEFINITION|CONTROL|VIEW ANY DEFINITION|  
|ALTER|CONTROL|ALTER ANY LOGIN<br /><br /> ALTER ANY SERVER ROLE|  
  
## <a name="permissions"></a>Permissões  
 Para logons, requer a permissão CONTROL no logon ou a permissão ALTER ANY LOGIN no servidor.  
  
 Para funções de servidor, requer a permissão CONTROL na função de servidor ou a permissão ALTER ANY SERVER ROLE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-revoking-impersonate-permission-on-a-login"></a>A. Revogando a permissão IMPERSONATE em um logon  
 O exemplo a seguir revoga a permissão `IMPERSONATE` no logon `WanidaBenshoof` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir do usuário do Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
REVOKE IMPERSONATE ON LOGIN::WanidaBenshoof FROM [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-revoking-view-definition-permission-with-cascade"></a>B. Revogando a permissão VIEW DEFINITION com CASCADE  
 O exemplo a seguir revoga a permissão `VIEW DEFINITION` do logon `EricKurjan` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir do logon `RMeyyappan` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção `CASCADE` indica que a permissão `VIEW DEFINITION` em `EricKurjan` também será revogada a partir dos principais aos quais `RMeyyappan` concedeu essa permissão.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON LOGIN::EricKurjan FROM RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-revoking-view-definition-permission-on-a-server-role"></a>C. Revogando a permissão VIEW DEFINITION em uma função de servidor  
 O exemplo a seguir revoga o `VIEW DEFINITION` na função de servidor `Sales` à função de servidor `Auditors`.  
  
```  
USE master;  
REVOKE VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [Permissões GRANT de entidade do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [Permissões DENY de entidade do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  


