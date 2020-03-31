---
title: Conceder permissões T-SQL
description: Conceda permissões T-SQL para operações de banco de dados no Parallel Data Warehouse.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bbe78979c393490a52e1051fe158ae138f93dcc
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79289694"
---
# <a name="grant-t-sql-permissions-for-parallel-data-warehouse"></a>Conceda permissões T-SQL para o Data Warehouse Paralelo
Conceda permissões T-SQL para operações de banco de dados no Parallel Data Warehouse.

## <a name="grant-permissions-to-submit-database-queries"></a>Conceder permissões para enviar consultas de banco de dados
Esta seção descreve como conceder permissões às funções do banco de dados e aos usuários para consultar dados no aparelho SQL Server PDW.  
  
As declarações utilizadas para conceder permissões para consultar dados dependem do escopo de acesso desejado. As seguintes instruções SQL criam um login chamado KimAbercrombie que pode acessar o aparelho, criam um usuário de banco de dados chamado KimAbercrombie no banco de dados **AdventureWorksPDW2012,** criam uma função de banco de dados chamada PDWQueryData, adicionam o uso do KimAbercrombie à função PDWQueryData e, em seguida, mostram opções para conceder acesso à consulta, com base no acesso ao objeto ou ao nível do banco de dados.  
  
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
  
## <a name="grant-permissions-to-use-the-admin-console"></a>Conceder permissões para usar o console de admin
Esta seção descreve como conceder permissões a logins para usar o Console de Admin.  
  
**Use o console de admin**  
  
Para usar o Console de Admin, um login requer a permissão do servidor DE **NÍVEL VIEW SERVER STATE.** A seguinte declaração SQL concede a permissão **do ESTADO DO SERVIDOR DE VISTA** ao login `KimAbercrombie` para que Kim possa usar o Console De Dmin para monitorar o aparelho PDW do Servidor SQL.  
  
```sql  
USE master;  
GO  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
GO  
```  
  
**Sessões de Matar**  
  
Para conceder a um login a permissão para matar sessões, conceda a permissão **ALTER ANY CONNECTION** da seguinte forma:  
  
```sql  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
## <a name="grant-permissions-to-load-data"></a>Conceder permissões para carregar dados
Esta seção descreve como conceder permissões a funções de banco de dados e usuários de banco de dados para carregar dados no PDWappliance do SQL Server.  
  
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
  
## <a name="grant-permissions-to-copy-data-off-the-appliance"></a>Conceder permissões para copiar dados do aparelho
Esta seção descreve como conceder permissões a uma função de usuário ou banco de dados para copiar dados do aparelho SQL Server PDW.  
  
Para mover dados para outro local, é necessário permissão **SELECT** na tabela que contém os dados a serem movidos.  
  
Se o destino dos dados for outro PDW do Servidor SQL, o usuário deverá ter permissão **CREATE TABLE** no destino e a permissão **ALTER SCHEMA** no esquema que conterá a tabela.  
  
## <a name="grant-permissions-to-manage-databases"></a>Conceder permissões para gerenciar bancos de dados
Esta seção descreve como conceder permissões a um usuário de banco de dados para gerenciar um banco de dados no aparelho SQL Server PDW.  
  
Em algumas situações, uma empresa atribui um gerente a um banco de dados. O gerente controla o acesso que outros logins têm ao banco de dados, bem como os dados e objetos no banco de dados. Para gerenciar todos os objetos, funções e usuários em um banco de dados, conceda ao usuário a permissão **CONTROL** no banco de dados. A seguinte declaração concede a permissão **CONTROL** no banco de `KimAbercrombie`dados **AdventureWorksPDW2012** ao usuário .  
  
```sql
USE AdventureWorksPDW2012;  
GO  
GRANT CONTROL ON DATABASE:: AdventureWorksPDW2012 TO KimAbercrombie;  
```  
  
Para conceder a alguém a permissão para controlar todas as bases de dados do aparelho, conceda a permissão **ALTER ANY DATABASE** no banco de dados mestre.  
  
## <a name="grant-permissions-to-manage-logins-users-and-database-roles"></a>Conceder permissões para gerenciar logins, usuários e funções de banco de dados
Esta seção descreve como conceder permissões para gerenciar logins, usuários de banco de dados e funções de banco de dados.  
  
### <a name="grant-permissions-to-manage-logins"></a><a name="PermsAdminConsole"></a>Conceder permissões para gerenciar logins  
**Adicionar ou gerenciar logins**  
  
As seguintes instruções SQL criam um Login chamado KimAbercrombie que pode criar novos logins usando a instrução [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md) e alterar os logins existentes usando a instrução [ALTER LOGIN.](../t-sql/statements/alter-login-transact-sql.md)  
  
A permissão **ALTER ANY LOGIN** concede a capacidade de criar novos logins e soltar exisiting. Uma vez que um login exista, o login pode ser gerenciado por logins com a permissão **ALTER ANY LOGIN** ou a permissão **ALTER** nesse login. Um login pode alterar a senha e o banco de dados padrão para seu próprio login.  
  
```sql 
CREATE LOGIN KimAbercrombie   
WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
GO  
  
GRANT ALTER ANY LOGIN TO KimAbercrombie;  
```  
  
### <a name="grant-permissions-to-manage-login-sessions"></a>Conceder permissões para gerenciar sessões de login  
Para ter a capacidade de visualizar todas as sessões no servidor requer a permissão **DO ESTADO DO SERVIDOR DE EXIBIÇÃO.** A capacidade de encerrar as sessões de outros logins requer a permissão **ALTER ANY CONNECTION.** O exemplo a `KimAbercrombie` seguir usa o login criado anteriormente.  
  
```sql  
-- Grant permissions to view sessions and queries  
GRANT VIEW SERVER STATE TO KimAbercrombie;  
  
-- Grant permission to end sessions  
GRANT ALTER ANY CONNECTION TO KimAbercrombie;  
```  
  
### <a name="grant-permission-to-manage-database-users"></a>Permissão de concessão para gerenciar usuários de banco de dados  
A criação e a queda de usuários de banco de dados requer a permissão **ALTER ANY USER.** O gerenciamento dos usuários existentes requer a permissão **ALTER ANY USER** ou a permissão **ALTER** nesse usuário. O exemplo a `KimAbercrombie` seguir usa o login criado anteriormente.  
  
```sql  
-- Create a user  
USE AdventureWorksPDW2012;  
GO  
CREATE USER KimAbercrombie;  
  
-- Grant permissions to create and drop users   
GRANT ALTER ANY USER TO KimAbercrombie;  
```  
  
### <a name="grant-permisson-to-manage-database-roles"></a>Conceder permisson para gerenciar funções de banco de dados  
Criar e soltar funções de banco de dados definidas pelo usuário requer a permissão **ALTER ANY ROLE.** O exemplo a `KimAbercrombie` seguir usa o login e o uso criados anteriormente.  
  
```sql  
USE AdventureWorksPDW2012;  
GO  
-- Grant permissions to create and drop roles  
GRANT ALTER ANY ROLE TO KimAbercrombie;  
```  
  
### <a name="login-user-and-role-permission-charts"></a>Gráficos de permissão de login, usuário e função  
Os gráficos a seguir podem ser confusos, mas mostram como permissões de alavanca mais altas (como CONTROL) incluem permissões mais granulares que podem ser concedidas separadamente (como ALTER). É uma prática recomendada sempre conceder a menor quantidade de permissões para alguém completar suas tarefas necessárias. Para fazer isso, conceda permissões mais específicas, em vez das permissões de nível superior.  
  
**Permissões de login:**  
  
![Permissões para logon da segurança de APS](./media/grant-permissions/APS_security_login_perms.png "APS_security_login_perms")  
  
**Permissões de usuário:**  
  
![Permissões do usuário da segurança de APS](./media/grant-permissions/APS_security_user_perms.png "APS_security_user_perms")  
  
**Permissões de função:**  
  
![Permissões da função de segurança de APS](./media/grant-permissions/APS_security_role_perms.png "APS_security_role_perms")  
  
<!-- MISSING LINKS
For a list of all permissions, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  
  
-->

## <a name="grant-permissions-to-monitor-the-appliance"></a>Conceder permissões para monitorar o aparelho
O aparelho SQL Server PDW pode ser monitorado usando as visualizações do sistema Admin Console ou SQL Server PDW. Os logins exigem a permissão **do SERVIDOR VIEW SERVER STATE** para monitorar o aparelho. Os logins exigem a permissão **ALTER ANY CONNECTION** para encerrar as conexões usando o console de admin ou o comando **KILL.** Para obter informações sobre as permissões necessárias para usar o Console De Dmin, consulte [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](#grant-permissions-to-use-the-admin-console).  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views"></a><a name="PermsAdminConsole"></a>Conceder permissão para monitorar o aparelho usando visualizações do sistema  
As seguintes instruções SQL criam um login `monitor_login` nomeado `monitor_login` e concede a permissão do ESTADO DO SERVIDOR DE **VISTA** ao login.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_login WITH PASSWORD='Password4321';  
GRANT VIEW SERVER STATE TO monitor_login;  
GO  
```  
  
### <a name="grant-permission-to-monitor-the-appliance-by-using-system-views-and-to-terminate-connections"></a>Conceder permissão para monitorar o aparelho usando visualizações do sistema e para encerrar conexões  
As seguintes instruções SQL criam um login `monitor_and_terminate_login` nomeado e concede o ESTADO DO SERVIDOR DE **VISTA** e ALTERA Quaisquer permissões DE **CONEXÃO** ao `monitor_and_terminate_login` login.  
  
```sql  
USE master;  
GO  
CREATE LOGIN monitor_and_terminate_login WITH PASSWORD='Password1234';   
GRANT VIEW SERVER STATE TO monitor_and_terminate_login;   
GRANT ALTER ANY CONNECTION TO monitor_and_terminate_login;  
GO  
```  
  
Para criar logins de admin, consulte [Funções de servidor fixo](pdw-permissions.md#fixed-server-roles).  
  
## <a name="see-also"></a>Confira também
[CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)  
[CRIAR USUÁRIO](../t-sql/statements/create-user-transact-sql.md)  
[CRIAR PAPEL](../t-sql/statements/create-role-transact-sql.md)  
[Carregar](load-overview.md)  
