---
title: Permissões DENY de servidor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], servers
- denying permissions [SQL Server], servers
- servers [SQL Server], permissions
- DENY statement, servers
ms.assetid: 68d6b2a9-c36f-465a-9cd2-01d43a667e99
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de59423c368bc966fab3958fbeb4b04888f4e2a8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114775"
---
# <a name="deny-server-permissions-transact-sql"></a>Permissões de servidor DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em um servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
DENY permission [ ,...n ]   
    TO <grantee_principal> [ ,...n ]  
    [ CASCADE ]  
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
 Especifica uma permissão que pode ser negada em um servidor. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CASCADE  
 Indica que a permissão está sendo negada para o principal especificado e todos os outros principais aos quais o principal concedeu a permissão. Necessário quando o principal tem a permissão com GRANT OPTION. 
  
 TO \<server_principal>  
 Especifica o principal ao qual a permissão é negada.  
  
 AS \<grantor_principal>  
 Especifica o principal do qual o principal que executa esta consulta deriva seu direito de negar a permissão.
Use a cláusula de entidade de segurança AS para indicar que a entidade de segurança registrada como o negador da permissão deve ser uma entidade de segurança diferente da pessoa que executa a instrução. Por exemplo, suponha que o usuário Maria seja a principal_id 12 e o usuário Ricardo seja a entidade de segurança 15. Melissa executa `DENY SELECT ON OBJECT::X TO Steven WITH GRANT OPTION AS Raul;`. Agora a tabela sys.database_permissions indicará que a grantor_principal_id da instrução de negação era 15 (Ricardo), embora na verdade, a instrução tenha sido executada pelo usuário 13 (Melissa).
  
O uso de AS nessa instrução não implica a capacidade de representar outro usuário.    
  
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
 Especifica uma função de servidor.  
  
## <a name="remarks"></a>Remarks  
 As permissões no escopo de servidor podem ser negadas somente quando o banco de dados atual é mestre.  
  
 As informações sobre permissões do servidor podem ser vistas na exibição do catálogo [sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) e as informações sobre entidades de segurança do servidor podem ser vistas na exibição do catálogo [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). As informações sobre a associação de funções de servidor podem ser vistas na exibição do catálogo [sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md).  
  
 Um servidor é o nível mais alto da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um servidor são listadas na tabela a seguir.  
  
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
 Requer a permissão CONTROL SERVER ou a propriedade do protegível. Se você usar a cláusula AS, a entidade especificada deverá ser proprietária do protegível no qual as permissões estão sendo negadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-denying-connect-sql-permission-to-a-sql-server-login-and-principals-to-which-the-login-has-regranted-it"></a>A. Negando a permissão CONNECT SQL a um logon do SQL Server e a entidades de segurança aos quais o logon a concedeu novamente  
 O exemplo a seguir nega a permissão `CONNECT SQL` para o logon de `Annika` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e para os principais aos quais ela concedeu a permissão.  
  
```  
USE master;  
DENY CONNECT SQL TO Annika CASCADE;  
GO  
```  
  
### <a name="b-denying-create-endpoint-permission-to-a-sql-server-login-using-the-as-option"></a>B. Negando a permissão CREATE ENDPOINT a um logon do SQL Server usando a opção AS  
 O exemplo a seguir nega a permissão `CREATE ENDPOINT` ao usuário `ArifS`. O exemplo usa a opção `AS` para especificar `MandarP` como a entidade de segurança da qual a entidade de segurança em execução deriva a autoridade para tanto.  
  
```  
USE master;  
DENY CREATE ENDPOINT TO ArifS AS MandarP;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Permissões DENY de servidor (Transact-SQL)](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [Permissões de servidor REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  
