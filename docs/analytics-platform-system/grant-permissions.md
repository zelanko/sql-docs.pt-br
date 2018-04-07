---
title: Conceder Permissões
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.openlocfilehash: 35542a9ea2544f0bdd357d3609937e1596e00a3f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="grant-permissions"></a>Conceder Permissões

## <a name="grant-permissions-to-submit-database-queries"></a>Conceder permissões para enviar consultas de banco de dados
Esta seção descreve como conceder permissões a funções de banco de dados e os usuários para consultar dados no dispositivo do SQL Server PDW.  
  
As instruções usadas para conceder permissões para consultar dados dependem do escopo de acesso desejado. Instruções SQL a seguir criam um logon denominado KimAbercrombie que pode acessar o dispositivo, crie um usuário de banco de dados chamado KimAbercrombie no **AdventureWorksPDW2012** de banco de dados, crie uma função de banco de dados denominada PDWQueryData, adiciona o uso KimAbercrombie para a função PDWQueryData e Mostrar opções para conceder acesso de consulta com base em se o acesso é concedido no objeto, ou no nível de banco de dados.  
  
```sql  
USE master;  
GO  
  
CREATE LOGIN KimAbercrombie WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
USE AdventureWorksPDW2012;  
GO  
  
CREATE USER KimAbercrombie;  
GO  
  
CREATE ROLE PDWQueryData;  
GO  
  
EXEC sp_addrolemember 'PDWQueryData', 'KimAbercrombie'  
GO  
  
-- If the permission is granted against a table or view only, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO PDWQueryData;  
GO  
  
-- If the permission is granted for the database, use this syntax:  
GRANT SELECT ON DATABASE::AdventureWorksPDW2012 TO PDWQueryData;  
GO  
  
-- If KimAbercrombie is the only user that needs to access a table, use this syntax:  
GRANT SELECT ON OBJECT::AdventureWorksPDW2012..DimEmployee TO KimAbercrombie;  
GO  
```  
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Conceder permissões para usar o Console de administração
Esta seção descreve como conceder permissões para os logons para usar o Console de administração.  
  
**Use o Console de administração**  
  
Para usar o Console do administrador de um logon requer que o nível de servidor **VIEW SERVER STATE** permissão. A instrução SQL a seguir concede a **VIEW SERVER STATE** permissão ao logon `KimAbercrombie` para que Kim pode usar o Console de administração para monitorar o utilitário do SQL Server PDW.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Interrompa as sessões**  
  
Para conceder a permissão para eliminar as sessões de um logon, conceda o **ALTER ANY CONNECTION** permissão da seguinte maneira:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Conceder permissões para carregar dados
Esta seção descreve como conceder permissões a usuários de banco de dados e funções de banco de dados para carregar dados para o SQL Server PDWappliance.  
  
A seguir mostra script quais permissões são necessárias para cada opção de carregamento. Você pode modificar para atender às suas necessidades específicas.  
  
```sql  
-- Create server login for the examples that follow.  
USE master;  
CREATE LOGIN BI_ETLUser WITH PASSWORD = '******';  
  
--Grant BULK Load permissions   
GRANT ADMINISTER BULK OPERATIONS TO BI_ETLUser;  
  
--Grant Staging database permissions  
USE stagedb;  
CREATE USER BI_ETLUser for login BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
EXEC sp_addrolemember 'db_ddladmin','BI_ETLUser';  
  
-- The CREATE TABLE permission is required for the database hosting the temporary table.  
-- This may be the staging database (if specified) or destination database.   
-- The CREATE permission is not required if loading in fastappend mode.  
GRANT CREATE TABLE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in append or fastappend mode, the INSERT permission is required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
  
-- If loading in reload mode, the INSERT and DELETE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT DELETE ON database::stagedb TO BI_ETLUser;  
  
-- If loading in upsert mode, the INSERT and UPDATE permissions are required on the destination table.  
GRANT INSERT ON database::stagedb TO BI_ETLUser;  
GRANT UPDATE ON database::stagedb TO BI_ETLUser;  
  
-- Destination DB  
USE tpch_1gb;  
CREATE USER BI_ETLUser FOR LOGIN BI_ETLUser;  
EXEC sp_addrolemember 'db_datareader','BI_ETLUser';  
EXEC sp_addrolemember 'db_datawriter','BI_ETLUser';  
```  
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Conceder permissões para copiar os dados do dispositivo
Esta seção descreve como conceder permissões a uma função de usuário ou banco de dados para copiar dados de dispositivo de PDW do SQL Server.  
  
Mover dados para outro local exige **selecione** permissão na tabela que contém os dados a ser movido.  
  
Se o destino de dados é outro SQL Server PDW, o usuário deve ter **CREATE TABLE** permissão no destino e **ALTER SCHEMA** permissão no esquema que contém a tabela.  
  
## <a name="grant-permissions-to-manage-databases"></a>Conceder permissões para gerenciar bancos de dados
Esta seção descreve como conceder permissões a um usuário de banco de dados para gerenciar um banco de dados no dispositivo do SQL Server PDW.  
  
Em algumas situações, uma empresa atribui um gerente de um banco de dados. O Gerenciador controla o acesso de outros logons para o banco de dados, bem como os dados e objetos no banco de dados. Para gerenciar todos os objetos, funções, e os usuários em um banco de dados concedam ao usuário o **controle** no banco de dados. A instrução a seguir concede a **controle** permissão a **AdventureWorksPDW2012** banco de dados para o usuário `KimAbercrombie`.  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Para conceder a alguém a permissão para controlar todos os bancos de dados no dispositivo, conceda o **ALTER ANY DATABASE** no banco de dados mestre.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Conceder permissões para gerenciar logons, usuários e funções de banco de dados
Esta seção descreve como conceder permissões para gerenciar logons, usuários de banco de dados e funções de banco de dados.  
  
### <a name="PermsAdminConsole"></a>Conceder permissões para gerenciar logons  
**Adicionar ou gerenciar logons**  
  
Instruções SQL a seguir criam um logon denominado KimAbercrombie que pode criar novos logons usando o [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) instrução e alterar os logons existentes usando o [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) instrução.  
  
O **ALTER ANY LOGIN** permissão concede a capacidade de criar novos logons e remover existente. Uma vez que exista um logon, o logon pode ser gerenciado por logons com o **ALTER ANY LOGIN** permissão ou o **ALTER** permissão no logon. Um logon pode alterar o banco de dados padrão e a senha para seu próprio logon.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Conceder permissões para gerenciar sessões de logon  
Para ter a capacidade de exibir todas as sessões no servidor exige o **VIEW SERVER STATE** permissão. A capacidade de encerrar as sessões de outros logons requer o **ALTER ANY CONNECTION** permissão. O exemplo a seguir usa o `KimAbercrombie` logon criado anteriormente.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Conceder permissão para gerenciar usuários de banco de dados  
Criar e remover usuários do banco de dados requerem o **ALTER ANY USER** permissão. O gerenciamento de usuários existentes requer o **ALTER ANY USER** permissão ou o **ALTER** permissão no usuário em questão. O exemplo a seguir usa o `KimAbercrombie` logon criado anteriormente.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Conceder permissão para gerenciar funções de banco de dados  
Criar e Cancelar funções de banco de dados definido pelo usuário, é necessário o **ALTER ANY ROLE** permissão. O exemplo a seguir usa o `KimAbercrombie` login e use criado anteriormente.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Logon, usuário e gráficos de permissão de função  
Os gráficos a seguir podem ser confusos, mas eles mostram as permissões de nível superior como (como controle) inclui as permissões mais granulares que podem ser concedidas separadamente (como ALTER). É uma prática recomendada sempre conceder o mínimo de permissões para um usuário concluir suas tarefas necessárias. Para fazer isso, conceda as permissões mais específicas, em vez das permissões de nível superior.  
  
**Permissões de logon:**  
  
![Permissões de logon de segurança de APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Permissões de usuário:**  
  
![Permissões de usuário de segurança de APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Permissões de função:**  
  
![Permissões de função de segurança de APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Conceder permissões para monitorar o dispositivo
O dispositivo de PDW do SQL Server pode ser monitorado usando o Console do administrador ou o SQL Server PDW exibições do sistema. Logons exigem o nível de servidor **VIEW SERVER STATE** permissão para monitorar o dispositivo. Logons exigem o **ALTER ANY CONNECTION** permissão para encerrar conexões usando o Console de administração ou a **KILL** comando. Para obter informações sobre as permissões necessárias para usar o Console de administração, consulte [conceder permissões para usar o Console de administração &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="PermsAdminConsole"></a>Conceder permissão para monitorar o dispositivo por meio de exibições do sistema  
Instruções SQL a seguir criam um logon denominado `monitor_login` e concede a **VIEW SERVER STATE** permissão para o `monitor_login` logon.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Conceder permissão para monitorar o dispositivo por meio de exibições do sistema e para encerrar conexões  
Instruções SQL a seguir criam um logon denominado `monitor_and_terminate_login` e concede a **VIEW SERVER STATE** e **ALTER ANY CONNECTION** permissões para o `monitor_and_terminate_login` logon.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Para criar logons de administrador, consulte [funções de servidor fixas](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Consulte também
[CRIAR UM LOGON](../t-sql/statements/create-login-transact-sql.md)  
[CRIAR USUÁRIO](../t-sql/statements/create-user-transact-sql.md)  
[CRIAR FUNÇÃO](../t-sql/statements/create-role-transact-sql.md)  
[Carga](load-overview.md)  
