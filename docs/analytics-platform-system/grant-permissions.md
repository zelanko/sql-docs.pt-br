---
title: Conceder permissões de T-SQL
description: Conceda permissões T-SQL para operações de banco de dados em data warehouse paralelas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257469"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Conceder permissões T-SQL para data warehouse paralelos
Conceda permissões T-SQL para operações de banco de dados em data warehouse paralelas.

## <a name="grant-permissions-to-submit-database-queries"></a>Conceder permissões para enviar consultas de banco de dados
Esta seção descreve como conceder permissões a usuários e funções de banco de dados para consultar os dados no dispositivo SQL Server PDW.  
  
As instruções usadas para conceder permissões para consultar dados dependem do escopo de acesso desejado. As instruções SQL a seguir criam um logon chamado KimAbercrombie que pode acessar o dispositivo, criar um usuário de banco de dados chamado KimAbercrombie no banco de dados **AdventureWorksPDW2012** , criar uma função de banco de dados denominada PDWQueryData, adicionar o uso KimAbercrombie à função PDWQueryData e, em seguida, mostrar opções para conceder acesso à consulta, com base no acesso concedido ao objeto ou ao nível do banco de dados.  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Conceder permissões para usar o console de administração
Esta seção descreve como conceder permissões a logons para usar o console de administração do.  
  
**Usar o console de administração**  
  
Para usar o console de administração, um logon requer a permissão de **estado do servidor de exibição** no nível do servidor. A instrução SQL a seguir concede a permissão **View Server State** ao logon para `KimAbercrombie` que Kim possa usar o console de administração para monitorar o dispositivo de SQL Server PDW.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Encerrar sessões**  
  
Para conceder a um logon a permissão para encerrar sessões, conceda a permissão **ALTER ANY Connection** da seguinte maneira:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Conceder permissões para carregar dados
Esta seção descreve como conceder permissões a funções de banco de dados e a usuários de banco de dado para carregar o SQL Server PDWappliance.  
  
O script a seguir mostra quais permissões são necessárias para cada opção de carregamento. Você pode modificar isso para atender às suas necessidades específicas.  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Conceder permissões para Copiar Dados fora do dispositivo
Esta seção descreve como conceder permissões a uma função de usuário ou de banco de dados para copiar e desligar o dispositivo SQL Server PDW.  
  
Para mover dados para outro local, é necessário ter a permissão **Select** na tabela que contém os dados a serem movidos.  
  
Se o destino dos dados for outro SQL Server PDW, o usuário deverá ter a permissão **CREATE TABLE** na permissão destino e **Alterar esquema** no esquema que conterá a tabela.  
  
## <a name="grant-permissions-to-manage-databases"></a>Conceder permissões para gerenciar bancos de dados
Esta seção descreve como conceder permissões a um usuário de banco de dados para gerenciar um banco de dados no dispositivo de SQL Server PDW.  
  
Em algumas situações, uma empresa atribui um gerente para um banco de dados. O Gerenciador controla o acesso que os outros logons têm ao banco de dados, bem como a data e os objetos no banco de dado. Para gerenciar todos os objetos, funções e usuários em um banco de dados, conceda ao usuário a permissão **Control** no banco de dados. A instrução a seguir concede a permissão **Control** no banco de dados **AdventureWorksPDW2012** ao usuário `KimAbercrombie` .  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Para conceder a alguém a permissão para controlar todos os bancos de dados no dispositivo, conceda a permissão **ALTER ANY DATABASE** no banco de dados mestre.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Conceder permissões para gerenciar logons, usuários e funções de banco de dados
Esta seção descreve como conceder permissões para gerenciar logons, usuários de banco de dados e funções de banco de dados.  
  
### <a name="grant-permissions-to-manage-logins"></a><a name="PermsAdminConsole"></a>Conceder permissões para gerenciar logons  
**Adicionar ou gerenciar logons**  
  
As instruções SQL a seguir criam um logon denominado KimAbercrombie que pode criar novos logons usando a instrução [Create login](../t-sql/statements/create-login-transact-sql.md) e alteram os logons existentes usando a instrução [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md) .  
  
A permissão **ALTER ANY login** concede a capacidade de criar novos logons e remover o existente. Quando um logon existe, o logon pode ser gerenciado por logons com a permissão **ALTER ANY login** ou a permissão **ALTER** nesse logon. Um logon pode alterar a senha e o banco de dados padrão para seu próprio logon.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Conceder permissões para gerenciar sessões de logon  
A capacidade de exibir todas as sessões no servidor requer a permissão **View Server State** . A capacidade de encerrar as sessões de outros logons requer a permissão **ALTER ANY Connection** . O exemplo a seguir usa o `KimAbercrombie` logon criado anteriormente.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Conceder permissão para gerenciar usuários de banco de dados  
Criar e descartar usuários de banco de dados requer a permissão **ALTER ANY User** . O gerenciamento de usuários existentes requer a permissão **ALTER ANY User** ou **ALTER** Permission nesse usuário. O exemplo a seguir usa o `KimAbercrombie` logon criado anteriormente.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Conceder permissão para gerenciar funções de banco de dados  
Criar e descartar funções de banco de dados definidas pelo usuário requer a permissão **ALTER ANY role** . O exemplo a seguir usa o `KimAbercrombie` logon e o uso criado anteriormente.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Gráficos de permissão de logon, usuário e função  
Os gráficos a seguir podem ser confusos, mas mostram como as permissões de alavanca mais altas (como controle) incluem permissões mais granulares que podem ser concedidas separadamente (como ALTER). É uma prática recomendada sempre conceder a menor quantidade de permissões para que alguém conclua suas tarefas necessárias. Para fazer isso, conceda permissões mais específicas, em vez das permissões de nível superior.  
  
**Permissões de logon:**  
  
![Permissões para logon da segurança de APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Permissões de usuário:**  
  
![Permissões do usuário da segurança de APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Permissões de função:**  
  
![Permissões da função de segurança de APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Conceder permissões para monitorar o dispositivo
O dispositivo SQL Server PDW pode ser monitorado usando o console de administração ou exibições do sistema SQL Server PDW. Os logons exigem a permissão de **servidor do modo de exibição** de nível de servidor para monitorar o dispositivo. Os logons exigem a permissão **ALTER ANY Connection** para encerrar conexões usando o console de administração ou o comando **Kill** . Para obter informações sobre as permissões necessárias para usar o console de administração, consulte [conceder permissões para usar o console de administração &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views"></a><a name="PermsAdminConsole"></a>Conceder permissão para monitorar o dispositivo usando exibições do sistema  
As instruções SQL a seguir criam um logon chamado `monitor_login` e concedem a permissão **View Server State** ao `monitor_login` logon.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Conceder permissão para monitorar o dispositivo usando exibições do sistema e encerrar conexões  
As instruções SQL a seguir criam um logon chamado `monitor_and_terminate_login` e concedem as permissões **View Server State** e **ALTER ANY Connection** para o `monitor_and_terminate_login` logon.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Para criar logons de administrador, consulte [funções de servidor fixas](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Confira também
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[CRIAR USUÁRIO](../t-sql/statements/create-user-transact-sql.md)  
[CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)  
[Carregar](load-overview.md)  
