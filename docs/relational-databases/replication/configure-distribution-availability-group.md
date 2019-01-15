---
title: Configurar o banco de dados de distribuição do SQL Server no grupo de disponibilidade | Microsoft Docs
ms.custom: ''
ms.date: 11/13/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b2f6defed7ad897f3464aec1b8b99391a2b9149
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126446"
---
# <a name="set-up-replication-distribution-database-in-always-on-availability-group"></a>Configurar o banco de dados de distribuição de replicação no grupo de disponibilidade Always On

Este artigo explica como configurar um banco de dados de distribuição de replicação do SQL Server em um AG (grupo de disponibilidade) Always On.

O SQL Server 2017 CU6 e o SQL Server 2016 SP2-CU3 introduzem o suporte para o banco de dados de distribuição de replicação em um AG por meio dos seguintes mecanismos:

- O AG do banco de dados de distribuição deve ter um ouvinte. Quando o publicador adiciona o distribuidor, ele usa o nome de ouvinte como o nome do distribuidor.
- Os trabalhos de replicação são criados com o nome do ouvinte como o nome do distribuidor.
- Um novo trabalho monitora o estado (primário ou secundário no AG) dos bancos de dados de distribuição e desabilita ou habilita os trabalhos de replicação com base no estado dos bancos de dados de distribuição.

Depois que um banco de dados de distribuição no AG for configurado com base nas etapas descritas abaixo, os trabalhos de tempo de execução e de configuração da replicação poderão ser executados corretamente antes e após o failover do AG do banco de dados de distribuição.

## <a name="supported-scenarios"></a>Cenários com suporte

- Configuração do banco de dados de distribuição a ser incluído em um AG.
- Configuração da replicação como publicações e assinaturas antes e após o failover do AG.
- Trabalhos de replicação funcionais antes e após o failover.
- Remoção da replicação no distribuidor e publicador quando o banco de dados de distribuição está no AG.
- Adição ou remoção de nós do AG de um banco de dados de distribuição existente.
- Um distribuidor pode ter vários bancos de dados de distribuição. Cada banco de dados de distribuição pode estar em seu próprio AG e não pode estar em qualquer AG. Vários bancos de dados de distribuição podem compartilhar um AG.
- O publicador e o distribuidor devem estar em instâncias separadas do SQL Server.
- Se o ouvinte para o grupo de disponibilidade que hospeda o banco de dados de distribuição estiver configurado para usar uma porta não padrão, será necessário configurar um alias para o ouvinte e a porta não padrão.

## <a name="limitations-or-exclusions"></a>Limitações e exclusões

- Não há suporte para o distribuidor local. Por exemplo, o publicador e o distribuidor devem ser instâncias diferentes do SQL Server. Um publicador que usa a si mesmo como distribuidor (também conhecido como distribuidor local) não pode dar suporte a bancos de dados de distribuição em um AG.
- Não há suporte para o publicador Oracle.
- Não há suporte para replicação de mesclagem.
- Não há suporte para replicação transacional com assinante de atualização imediata ou em fila.
- Não há suporte para a replicação ponto a ponto.
- Todas as instâncias do SQL Server que hospedam réplicas de banco de dados de distribuição devem ter a Atualização Cumulativa 6 do SQL Server 2017 ou posterior. 
- Todas as instâncias do SQL Server que hospedam réplicas de banco de dados de distribuição devem ter a mesma versão, exceto durante o período curto da atualização.
- O banco de dados de distribuição deve estar no modo de recuperação completa.
- Para a recuperação e para permitir o truncamento do log de transações, configure backups completos e de log de transações.
- O AG do banco de dados de distribuição deve ter um ouvinte configurado.
- As réplicas secundárias em um AG do banco de dados de distribuição podem ser síncronas ou assíncronas. O modo síncrono é recomendado e preferencial.
- Não há suporte para a replicação transacional bidirecional.
- SSMS não mostra o Banco de Dados de Distribuição como sincronizando/sincronizado quando o banco de dados de distribuição é adicionado a um grupo de disponibilidade.


   >[!NOTE]
   >Antes de executar um dos procedimentos armazenados de replicação (por exemplo – `sp_dropdistpublisher`, `sp_dropdistributiondb`, `sp_dropdistributor`, `sp_adddistributiondb`, `sp_adddistpublisher`) na réplica secundária, verifique se a réplica está totalmente sincronizada.

- Todas as réplicas secundárias em um AG do banco de dados de distribuição devem ser legíveis.
- Todos os nós no AG do banco de dados de distribuição precisam usar a mesma conta de domínio para executar o SQL Server Agent, e essa conta de domínio precisa ter o mesmo privilégio em cada nó.
- Se os agentes de replicação forem executados em uma conta proxy, ela precisará existir em cada nó do AG do banco de dados de distribuição e ter o mesmo privilégio em cada nó.
- Faça alterações nas propriedades do distribuidor ou do banco de dados de distribuição em todas as réplicas que participam do AG do banco de dados de distribuição.
- Faça alterações nos trabalhos de replicação por meio de procedimentos armazenados do msdb ou do SQL Server Management Studio em todas as réplicas que participam do AG do banco de dados de distribuição.
- A configuração do distribuidor no publicador precisa ser feita com scripts. O assistente de replicação não pode ser usado. Há suporte para assistentes de replicação e folhas de propriedade para outras finalidades.
- A configuração do AG para bancos de dados de distribuição só pode ser feita por meio de scripts.
- A configuração de bancos de dados de distribuição em um AG precisa ser uma nova configuração de replicação. Não há suporte para a alternância de um banco de dados de distribuição existente para um AG. Também quando um banco de dados de distribuição é retirado de um AG, ele pode deixar de funcionar como um banco de dados de distribuição válido e deve ser removido.

## <a name="configuration-architecture"></a>Arquitetura de configuração

Os nomes de servidor e as configurações a seguir são usados nos exemplos deste artigo.

- DIST1, DIST2 e DIST3 são servidores do distribuidor;
- PUB é o servidor do publicador;
- Depois que o AG do banco de dados de distribuição for formado, o nome do ouvinte será DISTLISTENER;
- DIST1 deve ser a réplica primária inicial do AG do banco de dados de distribuição.

## <a name="configure-distributor-distribution-database-and-publisher"></a>Configurar o distribuidor, o banco de dados de distribuição e o publicador

Este exemplo configura um novo distribuidor e publicador e coloca o banco de dados de distribuição em um AG.

### <a name="distributors-workflow"></a>Fluxo de trabalho dos distribuidores

1. Configurar DIST1, DIST2 e DIST3 como distribuidores com `sp_adddistributor @@servername`. Especifique a senha para o `distributor_admin` por meio do `@password`. O `@password` deve ser idêntico em DIST1, DIST2, DIST3.
2. Crie o banco de dados de distribuição em DIST1 com `sp_adddistributiondb`. O nome do banco de dados de distribuição é `distribution`. Altere o modo de recuperação do banco de dados `distribution` de simples para completo.
3. Crie um AG para o banco de dados `distribution` com réplicas em DIST1, DIST2 e DIST3. Preferencialmente, todas as réplicas são síncronas. Configure réplicas secundárias para serem legíveis ou permitirem a leitura. Neste momento, os bancos de dados de distribuição são o AG, DIST1 é a réplica primária e DIST2 e DIST3 são réplicas secundárias.
4. Configure um ouvinte chamado `DISTLISTENER` para o AG.
5. Para a recuperação e para permitir o truncamento do log de transações, configure backups completos e de log de transações.
6. No DIST2 e DIST3, execute:

   ```sql
   sp_adddistributiondb 'distribution'
   ```

1. Para adicionar `PUB` como publicador em DIST1, execute:
   
   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   O valor de `@working_directory` deve ser um caminho de rede independente de DIST1, DIST2 e DIST3.

1. No DIST2 e DIST3, execute:  

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   O valor de `@working_directory` deve ser o mesmo da etapa anterior.

### <a name="publisher-workflow"></a>Fluxo de trabalho do fornecedor

Para adicionar o ouvinte de AG do banco de dados `distribution` como o distribuidor, em PUB, execute: 

   ```sql
   sp_adddistributor @distributor = 'DISTLISTENER', @password = <distributor_admin password> 
   ```

   O valor de @password deve ser aquele especificado quando os distribuidores foram configurados no fluxo de trabalho do distribuidor.

## <a name="remove-distributor-and-publisher"></a>Remover o distribuidor e o publicador

Este exemplo remove o publicador e o distribuidor quando o banco de dados de distribuição está no AG.

### <a name="publisher-workflow"></a>Fluxo de trabalho do fornecedor

Em PUB, remova todas as assinaturas e publicações desse publicador e, em seguida, chame `sp_dropdistributor`.

### <a name="distributors-workflow"></a>Fluxo de trabalho dos distribuidores

Neste exemplo, DIST1 é o primário atual do AG do banco de dados `distribution`. DIST2 e DIST3 são réplicas secundárias.

1. No DIST2 e DIST3, execute:

   ```sql
   sp_dropdistpublisher 'PUB',  @no_checks = 1
   ```

1. Em DIST1, execute:

   ```sql
   sp_dropdistpublisher 'PUB'
   ```

1. Exclua o AG.
2. Em DIST2 e DIST3, altere o banco de dados `distribution` para o modo read_write restaurando o banco de dados com a recuperação.
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION
   ```

1. Para remover o banco de dados `distribution` e manter o diretório de instantâneo, execute: 

   ```sql
   sp_dropdistributiondb 'distribution' , @former_ag_secondary=1
   ```

  Este procedimento remove todos os trabalhos pendentes nesta réplica.

1. Para remover o banco de dados `distribution` de DIST1, execute

   ```sql
   sp_dropdistributiondb 'distribution'
   ``` 

1. Se não houver nenhum outro banco de dados de distribuição no AG, execute `sp_dropdistributor` em DIST1, DIST2 e DIST3.

## <a name="add-a-replica-to-distribution-database-ag"></a>Adicionar uma réplica ao AG do banco de dados de distribuição

Este exemplo adiciona um novo distribuidor a uma configuração de replicação existente com o banco de dados de distribuição no AG. Neste exemplo, um banco de dados de distribuição existente está em um AG. DIST1 e DIST2 são os distribuidores, `distribution` é o banco de dados de distribuição no AG e PUB é o publicador. Adicione DIST3 como uma réplica no AG.

### <a name="distributors-workflow"></a>Fluxo de trabalho dos distribuidores

1. DIST3 deve ser configurado como um distribuidor por meio de `sp_adddistributor @@servername`. A senha de `distributor_admin` deve ser especificada por meio do parâmetro @password. A senha deve ser a mesma que foi especificada para DIST1 e DIST2.
2. Adicione DIST3 ao AG do banco de dados de distribuição atual.
3. No DIST3, execute:

   ```sql
   sp_adddistributiondb 'distribution'
   ```

4. No DIST3, execute: 

   ```sql
   sp_adddistpublisher @publisher= 'PUB', @distribution_db= 'distribution', @working_directory= '<network path>'
   ```

   O valor de `@working_directory` deve ser o mesmo especificado para DIST1 e DIST2.

4. Em DIST3, você precisa recriar servidores vinculados aos assinantes.

## <a name="remove-a-replica-from-distribution-database-ag"></a>Remover uma réplica do AG do banco de dados de distribuição

Este exemplo remove um distribuidor de um AG do banco de dados de distribuição atual enquanto o restante das réplicas no AG do banco de dados de distribuição não é afetado. Neste exemplo, um banco de dados de distribuição está no AG. DIST1, DIST2 e DIST3 são os distribuidores, `distribution` é o banco de dados de distribuição no AG e PUB é o publicador. Remova DIST3 do AG.

### <a name="distributors-workflow"></a>Fluxo de trabalho dos distribuidores

1. Verifique se o DIST3 é um secundário do AG do banco de dados `distribution`.
2. Remova DIST3 do AG do banco de dados `distribution`.
3. Em DIST3, altere o banco de dados `distribution` para o modo read_write restaurando o banco de dados com a recuperação. Por exemplo, execute o seguinte comando:  
   
   ```sql
   RESTORE DATABASE distribution WITH RECOVERY, KEEP_REPLICATION.
   ```
   
1. Para remover todos os trabalhos órfãos em DIST3, execute: 

   ```sql
   sp_dropdistpublisher 'PUB', @no_checks = 1
   ```

1. No DIST3, execute:

   ```sql
   sp_dropdistributiondb 'distribution', @former_ag_secondary=1
   ```

1. No DIST3, execute: 

   ```sql
   sp_dropdistributor
   ```

## <a name="remove-a-publisher-from-distribution-database-ag"></a>Remover um publicador do AG do banco de dados de distribuição

Este exemplo remove um publicador de um AG do banco de dados de distribuição atual do distribuidor enquanto o restante dos publicadores atendidos por esse AG do banco de dados de distribuição não é afetado. Neste exemplo, uma configuração existente tem o banco de dados de distribuição em um AG. DIST1, DIST2 e DIST3 são os distribuidores, `distribution` é o banco de dados de distribuição no AG e PUB1 e PUB2 são os publicadores atendidos pelo banco de dados `distribution`. O exemplo remove PUB1 desses distribuidores.

### <a name="publisher-workflow"></a>Fluxo de trabalho do fornecedor

Em PUB1, remova todas as assinaturas e publicações desse publicador e, em seguida, chame `sp_dropdistributor`.

### <a name="distributor-workflow"></a>Fluxo de trabalho do Distribuidor

DIST1 é o primário atual do AG do banco de dados `distribution`.

1. No DIST2 e DIST3, execute:

   ```sql
   sp_dropdistpublisher 'PUB1',  @no_checks = 1
   ```

1. Em DIST1, execute:

   ```sql
   sp_dropdistpublisher 'PUB1'
   ```

1. Neste ponto, pode haver trabalhos órfãos relacionados ao PUB1 em DIST2 ou DIST3. Sempre que ocorrer um failover em DIST2 e DIST3, os trabalhos órfãos relacionados a todas as publicações de PUB1 serão removidos pelo trabalho `Monitor and sync replication agent jobs`.

## <a name="add-subscription"></a>Adicionar assinatura

Este exemplo trata da configuração correta das informações de assinante entre distribuidores. O exemplo adiciona um assinante. DIST1 é a réplica primária atual do banco de dados de distribuição no AG e DIST2 e DIST3 são réplicas secundárias do banco de dados de distribuição no AG. O nome do assinante é SUB.

### <a name="publisher-workflow"></a>Fluxo de trabalho do fornecedor

Em PUB, adicione a assinatura como normalmente faria ao assinante `SUB`.

### <a name="distributor-workflow"></a>Fluxo de trabalho do Distribuidor

Em DIST2 e DIST3, adicione um servidor vinculado para 'SUB', caso ele não esteja registrado no DIST2 ou DIST3 anteriormente. Veja abaixo um TSQL de exemplo para a criação do servidor vinculado:

   ```sql 
   EXEC master.dbo.sp_addlinkedserver@server =N'SUB', @srvproduct=N'SQL Server'
   /* For security reasons the linked server remote logins password is changed with ######## */
   EXEC master.dbo.sp_addlinkedsrvlogin@rmtsrvname=N'SUB', @useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL
   ```

## <a name="add-a-pull-subscription"></a>Adicionar uma assinatura pull

### <a name="subscriber-workflow"></a>Fluxo de trabalho do Assinante

Para adicionar uma assinatura pull a uma publicação com o banco de dados de distribuição em um AG, use o nome de ouvinte do AG no parâmetro `@distributor` de `sp_addpullsubscription_agent`.

## <a name="sample-t-sql-create-distribution-db-in-ag"></a>T-SQL de exemplo – Criar BD de distribuição no AG

O script a seguir permite um banco de dados de distribuição em um grupo de disponibilidade. 

```sql
--- WorkFlow to Enable Distribution Database In AG.

-- SECTION 1 ---- CONFIGURE THE DISTRIBUTOR SERVERS

-- Step1 - Configure the Distribution DB nodes (AG Replicas) to act as a distributor
:Connect SQLNode1
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go 
:Connect SQLNode2
sp_adddistributor @distributor = @@ServerName, @password = 'Pass@word1'
Go

-- Step2 - Configure the Distribution Database
:Connect SQLNode1
USE master
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO
Alter Database [DistributionDB] Set Recovery Full
Go
Backup Database [DistributionDB] to Disk = 'Nul'
Go
-- Step 3 - Create AG for the Distribution DB.
:Connect SQLNode1
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode2
USE [master]
GO
CREATE ENDPOINT [Hadr_endpoint] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)   
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE
, ENCRYPTION = REQUIRED ALGORITHM AES)
GO

:Connect SQLNode1
-- Create the Availability Group
CREATE AVAILABILITY GROUP [DistributionDB_AG]
FOR DATABASE [DistributionDB]
REPLICA ON 'SQLNode1'
WITH (ENDPOINT_URL = N'TCP://SQLNode1.contoso.com:5022', 
         FAILOVER_MODE = AUTOMATIC, 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
         BACKUP_PRIORITY = 50, 
         SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
         SEEDING_MODE = AUTOMATIC),
N'SQLNode2' WITH (ENDPOINT_URL = N'TCP://SQLNode2.contoso.com:5022', 
     FAILOVER_MODE = AUTOMATIC, 
     AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
     BACKUP_PRIORITY = 50, 
     SECONDARY_ROLE(ALLOW_CONNECTIONS = ALL), 
     SEEDING_MODE = AUTOMATIC);
 GO


:Connect SQLNode2
ALTER AVAILABILITY GROUP [DistributionDB_AG] JOIN
GO  
ALTER AVAILABILITY GROUP [DistributionDB_AG] GRANT CREATE ANY DATABASE
Go

--STEP4 - Create the Listener for the Availability Group. This is very important.
:Connect SQLNode1

USE [master]
GO
ALTER AVAILABILITY GROUP [DistributionDB_AG]
ADD LISTENER N'DistributionDBList' (
WITH IP
((N'10.0.0.8', N'255.255.255.0')) , PORT=1500);
GO

-- STEP 5 - Enable SQLNode1 also as a Distributor
:CONNECT SQLNODE2
EXEC sp_adddistributiondb @database = 'DistributionDB', @security_mode = 1;
GO

--STEP 6 - On all Distributor Nodes Configure the Publisher Details 
:CONNECT SQLNODE1
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO
:CONNECT SQLNODE2
EXEC sp_addDistPublisher @publisher = 'SQLNode4', @distribution_db = 'DistributionDB', 
    @working_directory = '\\sqlfileshare\Dist_Work_Directory\'
GO

-- SECTION 2 ---- CONFIGURE THE PUBLISHER SERVER
:CONNECT SQLNODE4
EXEC sp_addDistributor @distributor = 'DistributionDBList', -- Listener for the Distribution DB.    
    @password = 'Pass@word1'
Go

-- SECTION 3 ---- CONFIGURE THE SUBSCRIBERS 
-- On Publisher, create the publication as one would normally do.
-- On the Secondary replicas of the Distribution DB, add the Subscriber as a linked server.
:CONNECT SQLNODE2
EXEC master.dbo.sp_addlinkedserver @server = N'SQLNODE5', @srvproduct=N'SQL Server'
 /* For security reasons the linked server remote logins password is changed with ######## */
EXEC master.dbo.sp_addlinkedsrvlogin @rmtsrvname=N'SQLNODE5',@useself=N'True',@locallogin=NULL,@rmtuser=NULL,@rmtpassword=NULL 
```

## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Proteger o Distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
## <a name="next-steps"></a>Próximas etapas
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)  
 [Desabilitar a publicação e a distribuição](disable-publishing-and-distribution.md)  
 [Habilitar um banco de dados para replicação (SQL Server Management Studio)](enable-a-database-for-replication-sql-server-management-studio.md) 
