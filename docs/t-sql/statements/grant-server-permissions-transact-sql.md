---
title: Permissões GRANT do servidor (Transact-SQL) | Microsoft Docs
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
- GRANT statement, servers
- permissions [SQL Server], servers
- servers [SQL Server], permissions
- granting permissions [SQL Server], servers
ms.assetid: 7e880a5a-3bdc-491f-a167-7a9ed338be7f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3262749d33b2fa5c371e7c950aeffeb42087b8f6
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700974"
---
# <a name="grant-server-permissions-transact-sql"></a>Permissões de servidor GRANT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Concede permissões em um servidor. 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GRANT permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ] [ WITH GRANT OPTION ]  
    [ AS <grantor_principal> ]  
  
<grantee_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
  
<grantor_principal> ::= SQL_Server_login   
    | SQL_Server_login_mapped_to_Windows_login  
    | SQL_Server_login_mapped_to_Windows_group  
    | SQL_Server_login_mapped_to_certificate  
    | SQL_Server_login_mapped_to_asymmetric_key  
    | server_role  
```  
  
## <a name="arguments"></a>Argumentos  
 *permission*  
 Especifica uma permissão que pode ser concedida em um servidor. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 TO \<grantee_principal> Especifica a entidade de segurança para a qual a permissão está sendo concedida.  
  
 AS \<grantor_principal> Especifica a entidade de segurança da qual a entidade de segurança que executa essa consulta obtém seu direito de conceder a permissão.  
  
 WITH GRANT OPTION  
 Indica que o principal também terá a capacidade de conceder a permissão especificada a outros principais.  
  
 *SQL_Server_login*  
 Especifica um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *SQL_Server_login_mapped_to_Windows_login*  
 Especifica um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um logon do Windows.  
  
 *SQL_Server_login_mapped_to_Windows_group*  
 Especifica um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um grupo do Windows.  
  
 *SQL_Server_login_mapped_to_certificate*  
 Especifica um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para um certificado do Windows.  
  
 *SQL_Server_login_mapped_to_asymmetric_key*  
 Especifica um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mapeado para uma chave assimétrica.  
  
 *server_role*  
 Especifica uma função de servidor definida pelo usuário.  
  
## <a name="remarks"></a>Remarks  
 As permissões no escopo de servidor podem ser concedidas somente quando o banco de dados atual é mestre.  
  
 As informações sobre permissões do servidor podem ser vistas na exibição do catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) e as informações sobre entidades de segurança do servidor podem ser vistas na exibição do catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). As informações sobre a associação de funções de servidor podem ser vistas na exibição do catálogo [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md).  
  
 Um servidor é o nível mais alto da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser concedidas em um servidor são listadas na tabela a seguir.  
  
|Permissões de servidor|Implícito na permissão de servidor|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|Criar grupo de disponibilidade<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="remarks"></a>Remarks  
 As três permissões de servidor a seguir foram adicionadas ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Permissão **CONNECT ANY DATABASE**  
 Conceda **CONNECT ANY DATABASE** a um logon que deve se conectar a todos os bancos de dados que existem atualmente e a quaisquer novos bancos de dados que possam ser criados no futuro. Não concede nenhuma permissão em qualquer banco de dados além da conexão. Combine com **SELECT ALL USER SECURABLES** ou **VIEW SERVER STATE** para permitir que um processo de auditoria exiba todos os dados ou todos os estados do banco de dados na instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Permissão **IMPERSONATE ANY LOGIN**  
 Quando concedida, permite que um processo de camada intermediária represente a conta de clientes que se conecta a ela, uma vez que ela se conecta aos bancos de dados. Quando negada, um logon com altos privilégios pode ser impedido de representar outros logons. Por exemplo, um logon com a permissão **CONTROL SERVER** pode ser impedido de representar outros logons.  
  
 Permissão **SELECT ALL USER SECURABLES**  
 Quando concedida, um logon, como um auditor, pode exibir dados em todos os bancos de dados aos quais o usuário pode se conectar. Quando negada, impede o acesso a objetos, a menos que eles estejam no esquema **sys**.  
  
## <a name="permissions"></a>Permissões  
 O concessor (ou o principal especificado com a opção AS) deve ter a permissão em si com GRANT OPTION ou uma permissão superior que implique na concessão da permissão. Membros da função de servidor fixa sysadmin podem conceder qualquer permissão.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-granting-a-permission-to-a-login"></a>A. Concedendo uma permissão a um logon  
 O exemplo a seguir concede a permissão `CONTROL SERVER` o logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de `TerryEminhizer`.  
  
```  
USE master;  
GRANT CONTROL SERVER TO TerryEminhizer;  
GO  
```  
  
### <a name="b-granting-a-permission-that-has-grant-permission"></a>B. Concedendo uma permissão que possui a permissão GRANT  
 O exemplo a seguir concede `ALTER ANY EVENT NOTIFICATION` ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de `JanethEsteves` com o direito para conceder essa permissão a outro logon.  
  
```  
USE master;  
GRANT ALTER ANY EVENT NOTIFICATION TO JanethEsteves WITH GRANT OPTION;  
GO  
```  
  
### <a name="c-granting-a-permission-to-a-server-role"></a>C. Concedendo uma permissão a uma função de servidor  
 O exemplo seguinte cria duas funções de servidor nomeadas `ITDevAdmin` and `ITDevelopers`. Concede a permissão `ALTER ANY DATABASE` à função de servidor definida pelo usuário `ITDevAdmin` inclusive a opção `WITH GRANT` de forma que a função de servidor `ITDevAdmin` pode reatribuir a permissão `ALTER ANY DATABASE`. O exemplo concede a permissão `ITDevelopers` para usar a permissão `ALTER ANY DATABASE` da função de servidor `ITDevAdmin`.  
  
```  
USE master;  
CREATE SERVER ROLE ITDevAdmin ;  
CREATE SERVER ROLE ITDevelopers ;  
GRANT ALTER ANY DATABASE TO ITDevAdmin WITH GRANT OPTION ;  
GRANT ALTER ANY DATABASE TO ITDevelopers AS ITDevAdmin ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões DENY de servidor &#40;Transact-SQL&#41;](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [Permissões de servidor REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

