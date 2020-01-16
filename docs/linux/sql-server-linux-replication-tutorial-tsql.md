---
title: Configurar a Replicação do SQL Server em Linux
description: Este tutorial mostra como configurar a replicação de instantâneo do SQL Server no Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/09/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions'
ms.openlocfilehash: acc3f556371c52d02789a03813a28606435d86cd
ms.sourcegitcommit: 56fb0b7750ad5967f5d8e43d87922dfa67b2deac
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2019
ms.locfileid: "75001961"
---
# <a name="configure-replication-with-t-sql"></a>Configurar a replicação com T-SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

Neste tutorial, configure a replicação de instantâneo do SQL Server no Linux com duas instâncias do SQL Server usando Transact-SQL. O publicador e o distribuidor serão a mesma instância e o assinante estará em uma instância separada.

> [!div class="checklist"]
> * Habilitar agentes de Replicação do SQL Server em Linux
> * Criar banco de dados de exemplo
> * Configurar a pasta de instantâneo para acesso aos agentes do SQL Server
> * Configurar o distribuidor
> * Configurar o publicador
> * Configurar a publicação e artigos
> * Configurar o assinante 
> * Executar os trabalhos de replicação

Todas as configurações de replicação podem ser definidas com [procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

## <a name="prerequisites"></a>Prerequisites
Neste tutorial, você precisará de:

- Duas instâncias do SQL Server com a versão mais recente do SQL Server em Linux
- Uma ferramenta para emitir consultas T-SQL para configurar a replicação, como SQLCMD ou SSMS

   Confira [Usar o SSMS para gerenciar o SQL Server em Linux](./sql-server-linux-manage-ssms.md).

   >[!NOTE]
   >[!INCLUDE[SQL Server 2017](../includes/sssqlv14-md.md)] ([CU18](https://support.microsoft.com/help/4527377)) e posteriores são compatíveis com a Replicação do SQL Server para instâncias do SQL Server em Linux.

## <a name="detailed-steps"></a>Etapas detalhadas

1. Habilitar agentes de Replicação do SQL Server em Linux. Nas duas máquinas de host, execute os seguintes comandos no terminal. 

   ```bash
   sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
   sudo systemctl restart mssql-server
   ```

1. Criar a tabela e um banco de dados de exemplo. No editor, crie um banco de dados de exemplo e uma tabela que atuará como os artigos de uma publicação.

   ```sql
   CREATE DATABASE Sales
   GO
   USE [SALES]
   GO 
   CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
   GO 
   INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
   ```

   Na outra instância do SQL Server, o assinante, crie o banco de dados para receber os artigos.

   ```sql
   CREATE DATABASE Sales
   GO
   ```

1. Crie a pasta de instantâneo para os SQL Server Agents lerem/gravarem no distribuidor, crie a pasta de instantâneo e permita acesso ao usuário 'mssql' 

   ```bash
   sudo mkdir /var/opt/mssql/data/ReplData/
   sudo chown mssql /var/opt/mssql/data/ReplData/
   sudo chgrp mssql /var/opt/mssql/data/ReplData/
   ```

1. Configure o distribuidor. Neste exemplo, o publicador também será o distribuidor. Execute os seguintes comandos no publicador para configurar a instância para distribuição também.

   ```sql
   DECLARE @distributor AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @distributor = N'<distributor instance name>'--in this example, it will be the name of the publisher
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 
   
   use master
   exec sp_adddistributor @distributor = @distributor -- this should be the hostname

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   exec sp_adddistributiondb @database = N'distribution', @log_file_size = 2, @deletebatchsize_xact = 5000, @deletebatchsize_cmd = 2000, @security_mode = 0, @login = @distributorlogin, @password = @distributorpassword
   GO

   DECLARE @snapshotdirectory AS nvarchar(500)
   SET @snapshotdirectory = N'/var/opt/mssql/data/ReplData/'

   -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
   use [distribution] 
   if (not exists (select * from sysobjects where name = 'UIProperties' and type = 'U ')) 
          create table UIProperties(id int) 
   if (exists (select * from ::fn_listextendedproperty('SnapshotFolder', 'user', 'dbo', 'table', 'UIProperties', null, null))) 
          EXEC sp_updateextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties' 
   else 
         EXEC sp_addextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties'
   GO
   ```

1. Configurar o editor. Execute os seguintes comandos de TSQL no editor.

   ```sql
   DECLARE @publisher AS sysname
   DECLARE @distributorlogin AS sysname
   DECLARE @distributorpassword AS sysname
   -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
   SET @publisher = N'<instance name>' 
   SET @distributorlogin = N'<distributor login>'
   SET @distributorpassword = N'<distributor password>'
   -- Specify the distribution database. 

   -- Adding the distribution publishers
   exec sp_adddistpublisher @publisher = @publisher, 
   @distribution_db = N'distribution', 
   @security_mode = 0, 
   @login = @distributorlogin, 
   @password = @distributorpassword, 
   @working_directory = N'/var/opt/mssql/data/ReplData', 
   @trusted = N'false', 
   @thirdparty_flag = 0, 
   @publisher_type = N'MSSQLSERVER'
   GO
   ```

1. Configure o trabalho de publicação. Execute os seguintes comandos de TSQL no editor.

   ```sql
   DECLARE @replicationdb AS sysname
   DECLARE @publisherlogin AS sysname
   DECLARE @publisherpassword AS sysname
   SET @replicationdb = N'Sales'
   SET @publisherlogin = N'<Publisher login>'
   SET @publisherpassword = N'<Publisher Password>'

   use [Sales]
   exec sp_replicationdboption @dbname = N'Sales', @optname = N'publish', @value = N'true'
   
   -- Add the snapshot publication
   exec sp_addpublication 
   @publication = N'SnapshotRepl', 
   @description = N'Snapshot publication of database ''Sales'' from Publisher ''<PUBLISHER HOSTNAME>''.',
   @retention = 0, 
   @allow_push = N'true', 
   @repl_freq = N'snapshot', 
   @status = N'active', 
   @independent_agent = N'true'

   exec sp_addpublication_snapshot @publication = N'SnapshotRepl', 
   @frequency_type = 1, 
   @frequency_interval = 1, 
   @frequency_relative_interval = 1, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 8, 
   @frequency_subday_interval = 1, 
   @active_start_time_of_day = 0,
   @active_end_time_of_day = 235959, 
   @active_start_date = 0, 
   @active_end_date = 0, 
   @publisher_security_mode = 0, 
   @publisher_login = @publisherlogin, 
   @publisher_password = @publisherpassword
   ```

1. Criar artigos da tabela de vendas Execute os seguintes comandos TSQL no publicador.

   ```sql
   use [Sales]
   exec sp_addarticle 
   @publication = N'SnapshotRepl', 
   @article = N'customer', 
   @source_owner = N'dbo', 
   @source_object = N'customer', 
   @type = N'logbased', 
   @description = null, 
   @creation_script = null, 
   @pre_creation_cmd = N'drop', 
   @schema_option = 0x000000000803509D,
   @identityrangemanagementoption = N'manual', 
   @destination_table = N'customer', 
   @destination_owner = N'dbo', 
   @vertical_partition = N'false'
   ```

1. Configure a assinatura. Execute os seguintes comandos de TSQL no editor.

   ```sql
   DECLARE @subscriber AS sysname
   DECLARE @subscriber_db AS sysname
   DECLARE @subscriberLogin AS sysname
   DECLARE @subscriberPassword AS sysname
   SET @subscriber = N'<Instance Name>' -- for example, MSSQLSERVER
   SET @subscriber_db = N'Sales'
   SET @subscriberLogin = N'<Subscriber Login>'
   SET @subscriberPassword = N'<Subscriber Password>'

   use [Sales]
   exec sp_addsubscription 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @destination_db = @subscriber_db, 
   @subscription_type = N'Push', 
   @sync_type = N'automatic', 
   @article = N'all', 
   @update_mode = N'read only', 
   @subscriber_type = 0

   exec sp_addpushsubscription_agent 
   @publication = N'SnapshotRepl', 
   @subscriber = @subscriber,
   @subscriber_db = @subscriber_db, 
   @subscriber_security_mode = 0, 
   @subscriber_login = @subscriberLogin,
   @subscriber_password = @subscriberPassword,
   @frequency_type = 1,
   @frequency_interval = 0, 
   @frequency_relative_interval = 0, 
   @frequency_recurrence_factor = 0, 
   @frequency_subday = 0, 
   @frequency_subday_interval = 0, 
   @active_start_time_of_day = 0, 
   @active_end_time_of_day = 0, 
   @active_start_date = 0, 
   @active_end_date = 19950101
   GO
   ```

1. Execute trabalhos do agente de replicação. Execute a seguinte consulta para obter uma lista de trabalhos:

   ```sql
   SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
   ```

   Execute o trabalho de replicação de instantâneo para gerar o instantâneo:

   ```sql
   USE msdb;   
   --generate snapshot of publications, for example
   EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
   GO
   ```

   Execute o trabalho de replicação de instantâneo para gerar o instantâneo:

   ```sql
   USE msdb;
   --distribute the publication to subscriber, for example
   EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
   GO
   ```

1. Conectar assinante e consultar dados replicados.    

   No assinante, verifique se a replicação está funcionando executando a consulta a seguir:

   ```sql
   SELECT * from [Sales].[dbo].[CUSTOMER]
   ```

Neste tutorial, você configurou a replicação de instantâneo do SQL Server no Linux com duas instâncias do SQL Server usando Transact-SQL.

> [!div class="checklist"]
> * Habilitar agentes de Replicação do SQL Server em Linux
> * Criar banco de dados de exemplo
> * Configurar a pasta de instantâneo para acesso aos agentes do SQL Server
> * Configurar o distribuidor
> * Configurar o publicador
> * Configurar a publicação e artigos
> * Configurar o assinante 
> * Executar os trabalhos de replicação

## <a name="see-also"></a>Confira também

Para obter informações detalhadas sobre a replicação, confira [Documentação da Replicação do SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="next-steps"></a>Próximas etapas

[Conceitos: Replicação do SQL Server em Linux](sql-server-linux-replication.md)

[Procedimentos armazenados de replicação](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).
