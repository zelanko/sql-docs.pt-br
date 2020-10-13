---
title: Operar o SQL Server em Linux do grupo de disponibilidade
description: Este artigo descreve como executar uma atualização sem interrupção com instâncias do SQL Server em Linux com grupos de disponibilidade. Antes de atualizar, examine as melhores práticas.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a95d3e53f5ca2b15e0cccf87bd267258e2f4baab
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784753"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Operar grupos de disponibilidade Always On no Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

## <a name="upgrade-availability-group"></a>Atualizar grupo de disponibilidade

Antes de atualizar um grupo de disponibilidade, examine os padrões e as práticas em [Atualizar instâncias de réplica do grupo de disponibilidade](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

As seções a seguir explicam como executar uma atualização sem interrupção com instâncias do SQL Server em Linux com grupos de disponibilidade. 

### <a name="upgrade-steps-on-linux"></a>Etapas de atualização no Linux

Quando réplicas do grupo de disponibilidade estão em instâncias do SQL Server em Linux, o tipo de cluster do grupo de disponibilidade é `EXTERNAL` ou `NONE`. Um grupo de disponibilidade gerenciado por um gerenciador de cluster ao lado WSFC (Cluster de Failover do Windows Server) é `EXTERNAL`. O Pacemaker com Corosync é um exemplo de um gerenciador de cluster externo. Um grupo de disponibilidade sem nenhum gerenciador de cluster tem o tipo de cluster `NONE` As etapas de atualização descritas aqui são específicas de grupos de disponibilidade do tipo de cluster `EXTERNAL` ou `NONE`.

A ordem na qual você atualiza instâncias depende se a função delas é secundária e se elas hospedam ou não réplicas síncronas ou assíncronas. Atualize as instâncias do SQL Server que hospedam réplicas secundárias assíncronas primeiro. Em seguida, atualize as instâncias que hospedam réplicas secundárias síncronas. 

   >[!NOTE]
   >Se um grupo de disponibilidade só tiver réplicas assíncronas, para evitar a perda de dados, altere uma réplica para síncrona e aguarde até que ela seja sincronizada. Em seguida, atualize esta réplica.
   
Antes de começar, faça backup de cada banco de dados.

1. Interrompa o recurso no nó que hospeda a réplica secundária direcionada para atualização.
   
   Antes de executar o comando de atualização, interrompa o recurso para que o cluster não o monitore e falhe desnecessariamente. O exemplo a seguir adiciona uma restrição de localização no nó que fará o recurso ser interrompido. Atualize `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica direcionada para atualização.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Atualize o SQL Server na réplica secundária.

   O exemplo a seguir atualiza os pacotes `mssql-server` e `mssql-server-ha`.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Remova a restrição de localização.

   Antes de executar o comando de atualização, interrompa o recurso para que o cluster não o monitore e falhe desnecessariamente. O exemplo a seguir adiciona uma restrição de localização no nó que fará o recurso ser interrompido. Atualize `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica direcionada para atualização.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Como melhor prática, verifique se o recurso foi iniciado (usando o comando `pcs status`) e se a réplica secundária está em um estado conectado e sincronizado após a atualização.

1. Depois que todas as réplicas secundárias forem atualizadas, faça failover manualmente para uma das réplicas secundárias síncronas.

   Para grupos de disponibilidade com o tipo e cluster `EXTERNAL`, use ferramentas de gerenciamento de cluster para fazer failover; grupos de disponibilidade com o tipo de cluster `NONE` devem usar o Transact-SQL para fazer failover. 
   O exemplo a seguir faz failover de um grupo de disponibilidade com as ferramentas de gerenciamento de cluster. Substitua `<targetReplicaName>` pelo nome da réplica secundária síncrona que se tornará primária:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >As etapas a seguir aplicam-se somente a grupos de disponibilidade que não têm um gerenciador de cluster.

   Se o tipo de cluster do grupo de disponibilidade for `NONE`, faça failover manualmente. Conclua as seguintes etapas nesta ordem:

      a. O seguinte comando define a réplica primária como secundária. Substitua `AG1` pelo nome do grupo de disponibilidade. Execute o comando Transact-SQL na instância do SQL Server que hospeda a réplica primária.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. O seguinte comando define uma réplica secundária síncrona como primária. Execute o comando Transact-SQL a seguir na instância de destino do SQL Server – a instância que hospeda a réplica secundária síncrona.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Após o failover, atualize o SQL Server na réplica primária antiga repetindo o procedimento anterior.

   O exemplo a seguir atualiza os pacotes `mssql-server` e `mssql-server-ha`.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. Para um grupo de disponibilidade com um gerenciador de cluster externo – em que o tipo de cluster é EXTERNO, limpe a restrição de localização que foi causada pelo failover manual. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Retome a movimentação de dados para a réplica secundária recém-atualizada – a réplica primária antiga. Essa etapa é necessária quando uma instância de versão mais alta do SQL Server está transferindo blocos de logs para uma instância de versão mais baixa em um grupo de disponibilidade. Execute o seguinte comando na nova réplica secundária (a réplica primária anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Após atualizar todos os servidores, você poderá fazer failback. Faça failover de volta para a primária original, se necessário. 

## <a name="drop-an-availability-group"></a>Remover um grupo de disponibilidade

Para excluir um grupo de disponibilidade, execute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Se o tipo de cluster for `EXTERNAL` ou `NONE`, execute o comando em cada instância do SQL Server que hospeda uma réplica. Por exemplo, para remover um grupo de disponibilidade denominado `group_name`, execute o seguinte comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Próximas etapas

[Configurar o cluster do Red Hat Enterprise Linux para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o cluster do SUSE Linux Enterprise Server para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o cluster do Ubuntu para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
