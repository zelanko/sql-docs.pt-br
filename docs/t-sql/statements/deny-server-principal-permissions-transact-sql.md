---
title: "Negar permissões de entidade de servidor (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 06/09/2017
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
- DENY statement, impersonate
- permissions [SQL Server], impersonate
- impersonate [SQL Server], denying
- DENY statement, logins
- permissions [SQL Server], logins
- denying permissions [SQL Server], logins
- servers [SQL Server], permissions
- logins [SQL Server], denying access
ms.assetid: 859affa7-0567-47d1-9490-57c1abbd619b
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 15be2bfb51e6cdd9d111f052c62838c3326c61b5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="deny-server-principal-permissions-transact-sql"></a>Permissões de principal do servidor DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Nega permissões concedidas em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
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
 Especifica uma permissão que pode ser negada em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 LOGON **::** *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual a permissão está sendo negada. O qualificador de escopo (**::**) é necessária.  
  
 FUNÇÃO de servidor **::** *server_role*  
 Especifica a função de servidor na qual a permissão está sendo negada. O qualificador de escopo (**::**) é necessária.  
  
 PARA \<server_principal >  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou função de servidor ao qual a permissão está sendo concedida.  
  
 PARA *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual a permissão está sendo negada.  
  
 *SQL_Server_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_from_Windows_login*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um logon do Windows.  
  
 *SQL_Server_login_from_certificate*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado.  
  
 *SQL_Server_login_from_AsymKey*  
 Especifica o nome de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 *server_role*  
 Especifica o nome da função de servidor.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do qual o principal que executa esta consulta deriva seu direito de negar a permissão.  
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo de servidor podem ser negadas somente quando o banco de dados atual é mestre.  
  
 Obter informações sobre permissões de servidor estão disponíveis na [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição do catálogo. Obter informações sobre as entidades de servidor estão disponíveis na [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição do catálogo.  
  
 A instrução DENY falhará se CASCADE não for especificado ao negar uma permissão a uma entidade que foi concedida com GRANT OPTION.  
  
 Os logons e as funções de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são protegíveis no nível do servidor. As permissões mais específicas e limitadas que podem ser negadas em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou função de servidor são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
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
  
### <a name="a-denying-impersonate-permission-on-a-login"></a>A. Negando a permissão IMPERSONATE em um logon  
 O exemplo a seguir nega a permissão `IMPERSONATE` no logon `WanidaBenshoof` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir do usuário do Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
DENY IMPERSONATE ON LOGIN::WanidaBenshoof TO [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-denying-view-definition-permission-with-cascade"></a>B. Negando a permissão VIEW DEFINITION com CASCADE  
 O exemplo a seguir nega a permissão `VIEW DEFINITION` no logon `EricKurjan` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o logon `RMeyyappan` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A opção `CASCADE` indica que a permissão `VIEW DEFINITION` em `EricKurjan` também será negada a principais aos quais `RMeyyappan` concedeu essa permissão.  
  
```  
USE master;  
DENY VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    CASCADE;  
GO   
```  
  
### <a name="c-denying-view-definition-permission-on-a-server-role"></a>C. Negando a permissão VIEW DEFINITION em uma função de servidor  
 O exemplo a seguir nega o `VIEW DEFINITION` na função de servidor `Sales` à função de servidor `Auditors`.  
  
```  
USE master;  
DENY VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [Permissões GRANT de entidade do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-principal-permissions-transact-sql.md)   
 [Permissões REVOKE de entidade do servidor &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-principal-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

