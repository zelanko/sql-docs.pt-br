---
title: "Negar permissões de servidor (Transact-SQL) | Microsoft Docs"
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
- permissions [SQL Server], servers
- denying permissions [SQL Server], servers
- servers [SQL Server], permissions
- DENY statement, servers
ms.assetid: 68d6b2a9-c36f-465a-9cd2-01d43a667e99
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 424e0188b20d15831debf1e19ff17179fa3472c7
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="deny-server-permissions-transact-sql"></a>Permissões de servidor DENY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Nega permissões em um servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 *permissão*  
 Especifica uma permissão que pode ser negada em um servidor. Para obter uma lista de permissões, consulte a seção Comentários mais adiante neste tópico.  
  
 CASCADE  
 Indica que a permissão que está sendo negada também é negada a outros principais aos quais ela foi concedida por esse principal.  
  
 PARA \<server_principal >  
 Especifica o principal ao qual a permissão é negada.  
  
 AS \<grantor_principal >  
 Especifica o principal do qual o principal que executa esta consulta deriva seu direito de negar a permissão.  
  
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
  
## <a name="remarks"></a>Comentários  
 As permissões no escopo de servidor podem ser negadas somente quando o banco de dados atual é mestre.  
  
 Informações sobre permissões de servidor podem ser exibidas no [server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição de catálogo e obter informações sobre as entidades de servidor podem ser exibidos no [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md) exibição do catálogo. Informações sobre associação de funções de servidor podem ser exibidas no [server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md) exibição do catálogo.  
  
 Um servidor é o nível mais alto da hierarquia de permissões. As permissões mais específicas e limitadas que podem ser negadas em um servidor são listadas na tabela a seguir.  
  
|Permissões de servidor|Implícito na permissão de servidor|  
|-----------------------|----------------------------------|  
|ADMINISTER BULK OPERATIONS|CONTROL SERVER|  
|ALTER ANY AVAILABILITY GROUP<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER ANY CONNECTION|CONTROL SERVER|  
|ALTER ANY CREDENTIAL|CONTROL SERVER|  
|ALTER ANY DATABASE|CONTROL SERVER|  
|ALTER ANY ENDPOINT|CONTROL SERVER|  
|ALTER ANY EVENT NOTIFICATION|CONTROL SERVER|  
|ALTER ANY EVENT SESSION|CONTROL SERVER|  
|ALTER ANY LINKED SERVER|CONTROL SERVER|  
|ALTER ANY LOGIN|CONTROL SERVER|  
|ALTER ANY SERVER AUDIT|CONTROL SERVER|  
|ALTER ANY SERVER ROLE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|ALTER RESOURCES|CONTROL SERVER|  
|ALTER SERVER STATE|CONTROL SERVER|  
|ALTER SETTINGS|CONTROL SERVER|  
|ALTER TRACE|CONTROL SERVER|  
|AUTHENTICATE SERVER|CONTROL SERVER|  
|CONNECT ANY DATABASE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|CONNECT SQL|CONTROL SERVER|  
|CONTROL SERVER|CONTROL SERVER|  
|CREATE ANY DATABASE|ALTER ANY DATABASE|  
|CREATE AVAILABILITY GROUP<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY AVAILABILITY GROUP|  
|CREATE DDL EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|CREATE ENDPOINT|ALTER ANY ENDPOINT|  
|CREATE SERVER ROLE<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|ALTER ANY SERVER ROLE|  
|CREATE TRACE EVENT NOTIFICATION|ALTER ANY EVENT NOTIFICATION|  
|EXTERNAL ACCESS ASSEMBLY|CONTROL SERVER|  
|IMPERSONATE ANY LOGIN<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SELECT ALL USER SECURABLES<br /><br /> **Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|CONTROL SERVER|  
|SHUTDOWN|CONTROL SERVER|  
|UNSAFE ASSEMBLY|CONTROL SERVER|  
|VIEW ANY DATABASE|VIEW ANY DEFINITION|  
|VIEW ANY DEFINITION|CONTROL SERVER|  
|VIEW SERVER STATE|ALTER SERVER STATE|  
  
## <a name="remarks"></a>Comentários  
 As três permissões de servidor a seguir foram adicionadas ao [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 **CONECTAR a qualquer banco de dados** permissão  
 Conceda **CONNECT ANY DATABASE** a um logon que deve se conectar a todos os bancos de dados que existem atualmente e a quaisquer novos bancos de dados que possam ser criados no futuro. Não concede nenhuma permissão em qualquer banco de dados além da conexão. Combinar com **SELECT ALL USER SECURABLES** ou **VIEW SERVER STATE** para permitir que um processo de auditoria exibir todos os dados ou todos os estados de banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **REPRESENTAR qualquer logon** permissão  
 Quando concedida, permite que um processo de camada intermediária represente a conta de clientes que se conecta a ela, uma vez que ela se conecta aos bancos de dados. Quando negada, um logon com altos privilégios pode ser impedido de representar outros logons. Por exemplo, um logon com a permissão **CONTROL SERVER** pode ser impedido de representar outros logons.  
  
 **Selecione todos os PROTEGÍVEIS de usuário** permissão  
 Quando concedida, um logon, como um auditor, pode exibir dados em todos os bancos de dados aos quais o usuário pode se conectar. Quando negada, impede o acesso a objetos, a menos que o **sys** esquema.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CONTROL SERVER ou a propriedade do protegível. Se você usar a cláusula as, o principal especificado deve ser proprietário do protegível no qual as permissões estão sendo negadas.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [Negar permissões de servidor (Transact-SQL)](../../t-sql/statements/deny-server-permissions-transact-sql.md)   
 [REVOGAR permissões de servidor &#40; Transact-SQL &#41;](../../t-sql/statements/revoke-server-permissions-transact-sql.md)   
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)  
  
  

