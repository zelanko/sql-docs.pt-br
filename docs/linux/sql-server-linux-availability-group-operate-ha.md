---
title: Operar o grupo de disponibilidade do SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 98493c945f4f43e45b1f314f1500eb50a04c8e5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66713415"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Sempre operam em grupos de disponibilidade no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>Atualizar grupo de disponibilidade

Antes de atualizar um grupo de disponibilidade, examine os padrões e práticas na [atualizar instâncias de réplica do grupo de disponibilidade](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

As seções a seguir explicam como executar uma atualização sem interrupção com instâncias do SQL Server no Linux com grupos de disponibilidade. 

### <a name="upgrade-steps-on-linux"></a>Etapas de atualização no Linux

Quando as réplicas de grupo de disponibilidade estão em instâncias do SQL Server no Linux, o tipo de cluster do grupo de disponibilidade é `EXTERNAL` ou `NONE`. Um grupo de disponibilidade que é gerenciado por um Gerenciador de cluster, além de Windows Server Failover Cluster (WSFC) é `EXTERNAL`. Pacemaker com Corosync é um exemplo de um Gerenciador de cluster externo. Um grupo de disponibilidade sem nenhum Gerenciador de cluster tem o tipo de cluster `NONE` as etapas de atualização descritas aqui são específicas para grupos de disponibilidade do tipo de cluster `EXTERNAL` ou `NONE`.

A ordem na qual você pode atualizar instâncias depende de sua função não secundário e se eles hospedam réplicas síncronas ou assíncronas. Atualize instâncias do SQL Server que hospedam réplicas secundárias assíncronas pela primeira vez. Em seguida, atualize as instâncias que hospedam as réplicas secundárias síncronas. 

   >[!NOTE]
   >Se um grupo de disponibilidade tiver apenas assíncrona réplicas, para evitar qualquer perda de dados altere uma réplica para síncrona e aguarde até que ele é sincronizado. Em seguida, atualize esta réplica.
   
Antes de começar, faça backup de cada banco de dados.

1. Interrompa o recurso no nó que hospeda a réplica secundária de destino para atualização.
   
   Antes de executar o comando Atualizar, pare o recurso para que o cluster não irá monitorá-lo e fazer desnecessariamente. O exemplo a seguir adiciona uma restrição de local no nó que resultará no recurso a ser interrompida. Atualização `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica de destino para atualização.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Atualize o SQL Server na réplica secundária.

   O exemplo seguinte atualiza `mssql-server` e `mssql-server-ha` pacotes.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Remova a restrição de local.

   Antes de executar o comando Atualizar, pare o recurso para que o cluster não irá monitorá-lo e fazer desnecessariamente. O exemplo a seguir adiciona uma restrição de local no nó que resultará no recurso a ser interrompida. Atualização `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica de destino para atualização.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Como prática recomendada, verifique se o recurso for iniciado (usando `pcs status` comando) e a réplica secundária está conectada e estado sincronizado após a atualização.

1. Depois que todas as réplicas secundárias forem atualizadas, faça failover manualmente para uma das réplicas secundárias síncronas.

   Para grupos de disponibilidade com `EXTERNAL` tipo de cluster, use as ferramentas de gerenciamento de cluster falhe over; grupos de disponibilidade com `NONE` tipo de cluster deve usar o Transact-SQL para fazer failover. 
   O exemplo a seguir faz failover em um grupo de disponibilidade com as ferramentas de gerenciamento de cluster. Substitua `<targetReplicaName>` com o nome da réplica secundária síncrona que se tornará primário:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >As etapas a seguir se aplicam somente aos grupos de disponibilidade que não têm um Gerenciador de cluster.

   Se o tipo de cluster do grupo de disponibilidade está `NONE`, manualmente o failover. Conclua as seguintes etapas nesta ordem:

      a. O comando a seguir define a réplica primária para o secundário. Substitua `AG1` com o nome do seu grupo de disponibilidade. Execute o comando Transact-SQL na instância do SQL Server que hospeda a réplica primária.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. O comando a seguir define uma réplica secundária síncrona para o primário. Execute o seguinte comando do Transact-SQL na instância de destino do SQL Server - a instância que hospeda a réplica secundária síncrona.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Após o failover, atualize o SQL Server na réplica primária antiga, repetindo o procedimento anterior.

   O exemplo seguinte atualiza `mssql-server` e `mssql-server-ha` pacotes.

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

1. Um para grupos de disponibilidade com um Gerenciador de cluster externo - onde o tipo de cluster é EXTERNAL, limpe a restrição de local que foi causada pelo failover manual. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Retomar a movimentação de dados para a réplica secundária recém-atualizado - a réplica primária antiga. Essa etapa é necessária quando uma instância de versão superior do SQL Server está sendo transferido blocos de log para uma instância de versão inferior em um grupo de disponibilidade. Execute o seguinte comando na nova réplica secundária (a réplica primária anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Depois de atualizar todos os servidores, você poderá fazer failback. Efetue o failover novamente para a primária original - se necessário. 

## <a name="drop-an-availability-group"></a>Remover um grupo de disponibilidade

Para excluir um grupo de disponibilidade, execute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Se for o tipo de cluster `EXTERNAL` ou `NONE` execute o comando em cada instância do SQL Server que hospeda uma réplica. Por exemplo, para remover um grupo de disponibilidade chamado `group_name` execute o seguinte comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Próximas etapas

[Configurar o Cluster do Red Hat Enterprise Linux para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o Cluster do SUSE Linux Enterprise Server para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o Cluster do Ubuntu para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
