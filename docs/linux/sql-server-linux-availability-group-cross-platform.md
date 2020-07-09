---
title: Configurar o Grupo de Disponibilidade Always On do SQL Server no Windows e no Linux
description: Configure o Grupo de Disponibilidade do SQL Server com réplicas no Windows e no Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 2eec1f7f24f8465fb5d2bd4406de4c11aef8a518
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773595"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configurar o Grupo de Disponibilidade Always On do SQL Server no Windows e no Linux (multiplataforma)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/applies-to-version/sqlserver2017.md)]

Este artigo explica as etapas para criar um AG (grupo de disponibilidade) Always On com uma réplica em um Windows Server e a outra réplica em um servidor Linux. Essa configuração é multiplataforma porque as réplicas estão em sistemas operacionais diferentes. Use essa configuração para migrar de uma plataforma para a outra ou para DR (recuperação de desastre). Essa configuração não é compatível com alta disponibilidade porque não há solução de cluster para gerenciar uma configuração multiplataforma. 

![Nenhum Híbrido](./media/sql-server-linux-availability-group-overview/image1.png)

Antes de continuar, você deve estar familiarizado com a instalação e a configuração para instâncias do SQL Server no Windows e no Linux. 

## <a name="scenario"></a>Cenário

Neste cenário, dois servidores estão em sistemas operacionais diferentes. Um Windows Server 2016 chamado `WinSQLInstance` hospeda a réplica primária. Um servidor Linux chamado `LinuxSQLInstance` hospeda a réplica secundária.

## <a name="configure-the-ag"></a>Configurar o AG 

As etapas para criar o AG são as mesmas que para criar um AG para cargas de trabalho de escala de leitura. O tipo de cluster AG é NONE, porque não há gerenciador de cluster. 

   >[!NOTE]
   >Para os scripts neste artigo, colchetes angulares `<` e `>` identificam os valores que você precisa substituir para o seu ambiente. Os colchetes angulares em si não são necessários para os scripts. 

1. Instale o SQL Server 2017 no Windows Server 2016, habilite os Grupos de Disponibilidade Always On usando o SQL Server Configuration Manager e defina a autenticação de modo misto. 

   >[!TIP]
   >Se você estiver validando essa solução no Azure, coloque os dois servidores no mesmo conjunto de disponibilidade para garantir que eles estejam separados no data center. 

   **Habilitar Grupos de Disponibilidade**

   Para obter instruções, confira [Habilitar e desabilitar Grupos de Disponibilidade AlwaysOn (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Habilitar Grupos de Disponibilidade](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   O SQL Server Configuration Manager observa que o computador não é um nó em um cluster de failover. 

   Depois de habilitar os Grupos de Disponibilidade, reinicie o SQL Server.

   **Definir autenticação de modo misto**

   Para obter instruções, confira [Alterar o modo de autenticação do servidor](../database-engine/configure-windows/change-server-authentication-mode.md#change-authentication-mode-with-ssms).

1. Instale o SQL Server 2017 no Linux. Para obter instruções, confira [Instalar o SQL Server](sql-server-linux-setup.md). Habilite `hadr` via mssql-conf.

   Para habilitar o `hadr` via mssql-conf de um prompt de shell, emita o seguinte comando:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Depois de habilitar `hadr`, reinicie a instância do SQL Server.  

   A imagem a seguir mostra essa etapa completa.

   ![Habilitar Grupos de Disponibilidade do Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Configure o arquivo de hosts em ambos os servidores ou registre os nomes de servidor com DNS.

1. Abra portas de firewall para TPC 1433 e 5022 no Windows e no Linux.

1. Na réplica primária, crie um logon de banco de dados e uma senha.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. Na réplica primária, crie uma chave mestra e um certificado e, em seguida, faça backup do certificado com uma chave privada.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. Copie o certificado e a chave privada para o servidor Linux (réplica secundária) em `/var/opt/mssql/data`. Você pode usar o `pscp` para copiar os arquivos para o servidor Linux. 

1. Defina o grupo e a propriedade da chave privada e o certificado como `mssql:mssql`.

   O script a seguir define o grupo e a propriedade dos arquivos. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   No diagrama, a propriedade e o grupo a seguir são definidos corretamente para o certificado e a chave.

   ![Habilitar Grupos de Disponibilidade do Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. Na réplica secundária, crie um logon de banco de dados e uma senha e crie uma chave mestra.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. Na réplica secundária, restaure o certificado que você copiou para `/var/opt/mssql/data`. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. Na réplica primária, crie um ponto de extremidade.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >O firewall deve estar aberto para a porta TCP do ouvinte. No script anterior, a porta é 5022. Use qualquer porta TCP disponível. 

1. Na réplica secundária, crie o ponto de extremidade. Repita o script anterior na réplica secundária para criar o ponto de extremidade. 

1. Na réplica primária, crie o AG com `CLUSTER_TYPE = NONE`. O script de exemplo usa `SEEDING_MODE = AUTOMATIC` para criar o AG. 

   >[!NOTE]
   >Quando a instância do Windows do SQL Server usa caminhos diferentes para arquivos de dados e de log, a propagação automática falha na instância do Linux do SQL Server porque esses caminhos não existem na réplica secundária. Para usar o script a seguir para um AG multiplataforma, o banco de dados requer o mesmo caminho para os arquivos de log e de dados no Windows Server. Como alternativa, você pode atualizar o script para definir `SEEDING_MODE = MANUAL` e, em seguida, fazer backup e restaurar o banco de dados com o `NORECOVERY` para propagar o banco de dados. 
   >
   >Esse comportamento se aplica a imagens do Azure Marketplace. 
   >
   >Para saber mais sobre a propagação automática, confira [Propagação Automática – Layout de Disco](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Antes de executar o script, atualize os valores para seus AGs.

      * Substitua `<WinSQLInstance>` pelo nome do servidor da instância do SQL Server da réplica primária.

      * Substitua `<LinuxSQLInstance>` pelo nome do servidor da instância do SQL Server da réplica secundária. 

   Para criar o AG, atualize os valores e execute o script na réplica primária.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   Para obter mais informações, confira [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. Na réplica secundária, ingresse no AG.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Crie um banco de dados para o AG. As etapas de exemplo usam um banco de dados chamado `<TestDB>`. Se você estiver usando a propagação automática, defina o mesmo caminho para os arquivos de dados e de log. 

   Antes de executar o script, atualize os valores para seu banco de dados.

      * Substitua `<TestDB>` pelo nome do seu banco de dados.

      * Substitua `<F:\Path>` pelo caminho do banco de dados e dos arquivos de log. Use o mesmo caminho para os arquivos de log e de banco de dados. 

      Você também pode usar os caminhos padrão. 

    Para criar seu banco de dados, execute o script. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Faça um backup completo do banco de dados. 

1. Se você não estiver usando a propagação automática, restaure o banco de dados no servidor de réplica secundária (Linux). [Migrar um banco de dados do SQL Server do Windows para o Linux usando o recurso de backup e restauração](sql-server-linux-migrate-restore-database.md). Restaure o banco de dados `WITH NORECOVERY` na réplica secundária. 

1. Adicione o banco de dados ao AG. Atualize o script de exemplo. Substitua `<TestDB>` pelo nome do seu banco de dados. Na réplica primária, execute a consulta SQL para adicionar o banco de dados ao AG.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Verifique se o banco de dados está sendo preenchido na réplica secundária. 

## <a name="fail-over-the-primary-replica"></a>Fazer failover da réplica primária

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

Este artigo analisou as etapas para criar um AG multiplataforma para dar suporte a cargas de trabalho de migração ou de escala de leitura. Ele pode ser usado para recuperação manual de desastre. Ele também explicou como fazer failover do AG. Um AG multiplataforma usa o tipo de cluster `NONE` e não é compatível com alta disponibilidade porque não há nenhuma ferramenta de cluster entre plataformas. 

## <a name="next-steps"></a>Próximas etapas

[Visão geral de Grupos de Disponibilidade AlwaysOn](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Noções básicas de disponibilidade do SQL Server para implantações do Linux](sql-server-linux-ha-basics.md)
