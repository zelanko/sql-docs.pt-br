---
title: Permissões GRANT de entidade de segurança do servidor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- impersonate [SQL Server], granting
- granting permissions [SQL Server], logins
- permissions [SQL Server], impersonate
- permissions [SQL Server], logins
- GRANT statement, impersonation
- GRANT statement, logins
- logins [SQL Server], granting access
- granting permissions [SQL Server], impersonation
ms.assetid: 4cbed281-5e1e-4d8b-b410-4c18a6cd0205
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 81a8422cbab7eb10d0c74ad5cd758817a665eaa6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68050778"
---
# <a name="grant-server-principal-permissions-transact-sql"></a>Permissões de entidade de segurança do servidor GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissões em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GRANT permission [ ,...n ] }   
    ON   
    { [ LOGIN :: SQL_Server_login ]  
      | [ SERVER ROLE :: server_role ] }   
    TO <server_principal> [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS SQL_Server_login ]   
  
<server_principal> ::=   
    SQL_Server_login  
    | SQL_Server_login_from_Windows_login   
    | SQL_Server_login_from_certificate   
    | SQL_Server_login_from_AsymKey   
    | server_role  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser concedida em um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 LOGON **::** *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual a permissão está sendo concedida. O qualificador de escopo ( **::** ) é obrigatório.  
  
 SERVER ROLE **::** *server_role*  
 Especifica a função de servidor definida pelo usuário ao qual a permissão está sendo concedida. O qualificador de escopo ( **::** ) é obrigatório.  
  
 TO \<server_principal> Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a função de servidor ao qual a permissão está sendo concedida.  
  
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
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 AS *SQL_Server_login*  
 Especifica o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do qual o principal que executa esta consulta deriva seu direito de conceder a permissão.  
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo de servidor podem ser concedidas somente quando o banco de dados atual é mestre.  
  
 As informações sobre permissões do servidor são visíveis na exibição do catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md). As informações sobre entidades de segurança do servidor são visíveis na exibição do catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md).  
  
 Os logons e as funções de servidor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são protegíveis no nível do servidor. As permissões mais específicas e limitadas que podem ser concedidas a um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou função de servidor são listadas na tabela a seguir, junto com as permissões mais gerais que as contêm implicitamente.  
  
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
  
### <a name="a-granting-impersonate-permission-on-a-login"></a>a. Concedendo a permissão IMPERSONATE em um logon  
 O exemplo a seguir concede a permissão `IMPERSONATE` no logon `WanidaBenshoof` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir do usuário do Windows `AdvWorks\YoonM`.  
  
```  
USE master;  
GRANT IMPERSONATE ON LOGIN::WanidaBenshoof to [AdvWorks\YoonM];  
GO  
```  
  
### <a name="b-granting-view-definition-permission-with-grant-option"></a>B. Concedendo a permissão VIEW DEFINITION com GRANT OPTION  
 O exemplo a seguir concede `VIEW DEFINITION` no logon `EricKurjan` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao logon `RMeyyappan` do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com `GRANT OPTION`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON LOGIN::EricKurjan TO RMeyyappan   
    WITH GRANT OPTION;  
GO   
```  
  
### <a name="c-granting-view-definition-permission-on-a-server-role"></a>C. Concedendo a permissão VIEW DEFINITION em uma função de servidor  
 O exemplo a seguir concede `VIEW DEFINITION` na função de servidor `Sales` à função de servidor `Auditors`.  
  
```  
USE master;  
GRANT VIEW DEFINITION ON SERVER ROLE::Sales TO Auditors ;  
GO   
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [Procedimentos armazenados de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  

