---
title: Operar o grupo de disponibilidade do SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 07/20/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: Inactive
ms.openlocfilehash: 54c9be66075ebbc9614de0b007b5b718e976121b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="operate-ha-availability-group-for-sql-server-on-linux"></a>Operar o grupo de disponibilidade de alta disponibilidade para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

## <a name="failover"></a>O failover do grupo de disponibilidade

Use as ferramentas de gerenciamento de cluster para failover de um grupo de disponibilidade gerenciado por um Gerenciador de cluster externo. Por exemplo, se uma solução usa Pacemaker para gerenciar um cluster do Linux, use `pcs` executar failovers manuais em RHEL ou Ubuntu. No SLES use `crm`. 

> [!IMPORTANT]
> Em operações normais, não realizarão failover com ferramentas de gerenciamento de Transact-SQL ou SQL Server como o SSMS ou o PowerShell. Quando `CLUSTER_TYPE = EXTERNAL`, o único valor aceitável para `FAILOVER_MODE` é `EXTERNAL`. Com essas configurações, todas as ações de failover manual ou automática são executadas pelo Gerenciador de cluster externo. 

### <a name="manual-failover-examples"></a>Exemplos de failover manual

Failover manualmente o grupo de disponibilidade com as ferramentas de gerenciamento de cluster externo. Em operações normais, não inicie o failover com o Transact-SQL. Se as ferramentas de gerenciamento de cluster externo não responder, você pode forçar o failover do grupo de disponibilidade. Para obter instruções forçar o failover manual, consulte [Manual mover quando as ferramentas de cluster não estão respondendo](#forceManual).

Conclua o failover manual em duas etapas. 

1. Mova o recurso de grupo de disponibilidade do nó do cluster que possui os recursos para um novo nó.

   O Gerenciador de cluster move o recurso de grupo de disponibilidade e adiciona uma restrição de local. Essa restrição configura o recurso para ser executado no novo nó. Você deve remover esta restrição para mover que o manualmente ou automaticamente o failover no futuro.

2. Remova a restrição de local.

#### <a name="1-manually-fail-over"></a>1. Failover manual

Para realizar o failover manual em um recurso de grupo de disponibilidade denominado *ag_cluster* ao nó de cluster chamado *nodeName2*, execute o comando apropriado para a sua distribuição:

- **Exemplo RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Exemplo SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```



>[!IMPORTANT]
>Depois que você failover manual de um recurso, você precisa remover a restrição de local é adicionada automaticamente durante a movimentação.

#### <a name="2-remove-the-location-constraint"></a>2. Remover a restrição de local

Durante uma movimentação manual, o `pcs` comando `move` ou `crm` comando `migrate` adiciona uma restrição de local para o recurso a ser colocado no novo nó de destino. Para ver a nova restrição, execute o comando a seguir depois de mover manualmente o recurso:

- **Exemplo RHEL/Ubuntu**

   ```bash
   sudo pcs constraint --full
   ```

- **Exemplo SLES**

   ```bash
   crm config show
   ```

Você precisa remover a restrição de local para que movimentações futuras – incluindo failover automático – tenham êxito. 

Execute o comando a seguir para remover a restrição. 

- **Exemplo RHEL/Ubuntu**

   Neste exemplo `ag_cluster-master` é o nome do recurso que foi movido. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **Exemplo SLES**

   Neste exemplo `ag_cluster` é o nome do recurso que foi movido. 

   ```bash
   crm resource clear ag_cluster
   ```

Alternativamente, você pode executar o comando a seguir para remover a restrição de local.  

- **Exemplo RHEL/Ubuntu**

   No comando a seguir, `cli-prefer-ag_cluster-master` é a ID da restrição que precisa ser removida. `sudo pcs constraint --full` retorna essa ID. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
- **Exemplo SLES**

   No comando a seguir `cli-prefer-ms-ag_cluster` é a ID da restrição. `crm config show` retorna essa ID. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>O failover automático não adiciona uma restrição de local, portanto, nenhuma limpeza é necessária. 

Para obter mais informações, consulte:
- [Red Hat – gerenciamento de recursos de cluster](http://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker - mover recursos manualmente](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-pcs/html/Clusters_from_Scratch/_move_resources_manually.html)
 [guia de administração do SLES - recursos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 

### <a name="forceManual"></a>Manual mover quando as ferramentas de cluster não estão respondendo 

Em casos extremos, se um usuário não pode usar as ferramentas de gerenciamento de cluster para interagir com o cluster (ou seja, o cluster não está respondendo, ferramentas de gerenciamento de cluster tem um comportamento com falha), o usuário talvez precise fazer failover manualmente - ignorando o Gerenciador de cluster externo. Isso não é recomendado para as operações normais e deve ser usado no cluster falha ao executar a ação de failover usando as ferramentas de gerenciamento de cluster de casos.

Se você não pode fazer failover do grupo de disponibilidade com as ferramentas de gerenciamento de cluster, siga estas etapas para fazer failover de ferramentas do SQL Server:

1. Verifique se que o recurso de grupo de disponibilidade não é gerenciado pelo cluster mais. 

      - Tentativa de definir o recurso de modo não gerenciado. Isso sinaliza o gerenciamento e o agente de recurso para interromper o monitoramento de recursos. Por exemplo: 
      
      ```bash
      sudo pcs resource unmanage <**resourceName**>
      ```

      - Se a tentativa de definir o modo de recurso para o modo de não gerenciado falhar, exclua o recurso. Por exemplo:

      ```bash
      sudo pcs resource delete <**resourceName**>
      ```

      >[!NOTE]
      >Quando você exclui um recurso também exclui todas as restrições associadas. 

1. Definir manualmente a variável de contexto de sessão `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Failover do grupo de disponibilidade com o Transact-SQL. No exemplo a seguir substituir `<**MyAg**>` com o nome do seu grupo de disponibilidade. Conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute o seguinte comando:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <**MyAg**> FAILOVER;
   ```

1. Reinicie o gerenciamento e monitoramento de recursos de cluster. Execute o seguinte comando:

   ```bash
   sudo pcs resource manage <**resourceName**>
   sudo pcs resource cleanup <**resourceName**>
   ```

## <a name="database-level-monitoring-and-failover-trigger"></a>Gatilho de monitoramento e failover de nível de banco de dados

Para `CLUSTER_TYPE=EXTERNAL`, a semântica de disparador de failover é diferente em comparação com o WSFC. Quando o grupo de disponibilidade está em uma instância do SQL Server em um WSFC, fazendo a transição de `ONLINE` de estado para o banco de dados faz com que a integridade do grupo de disponibilidade relatar uma falha. Isso sinalizará o Gerenciador de cluster para disparar uma ação de failover. No Linux, a instância do SQL Server não pode se comunicar com o cluster. Monitoramento de integridade do banco de dados é feito "fora de". Se o usuário aceito para monitoramento de failover em nível de banco de dados e failover (definindo a opção `DB_FAILOVER=ON` ao criar o grupo de disponibilidade), o cluster irá verificar se o estado do banco de dados é `ONLINE` sempre que quando ele executa uma ação de monitoramento. O cluster consulta o estado em `sys.databases`. Para qualquer estado diferente de `ONLINE`, ele irá disparar um failover automaticamente (se as condições de failover automático são atendidas). O tempo real do failover depende da frequência da ação de monitoramento, bem como o estado do banco de dados que está sendo atualizado em sys. Databases.

## <a name="upgrade-availability-group"></a>Atualizar o grupo de disponibilidade

Antes de atualizar um grupo de disponibilidade, examine as práticas recomendadas em [atualizar instâncias de réplica do grupo de disponibilidade](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

As seções a seguir explicam como executar uma atualização sem interrupção com instâncias do SQL Server no Linux com grupos de disponibilidade. 

### <a name="upgrade-steps-on-linux"></a>Etapas de atualização no Linux

Quando as réplicas de grupo de disponibilidade em instâncias do SQL Server no Linux, o tipo de cluster do grupo de disponibilidade é `EXTERNAL` ou `NONE`. Um grupo de disponibilidade que é gerenciado por um Gerenciador de cluster, além de Failover de Cluster WSFC (Windows Server) é `EXTERNAL`. Pacemaker com Corosync é um exemplo de um Gerenciador de cluster externo. Um grupo de disponibilidade com o Gerenciador de cluster não tem o tipo de cluster `NONE` as etapas de atualização descritas aqui são específicas para grupos de disponibilidade do tipo de cluster `EXTERNAL` ou `NONE`.

1. Antes de começar, fazer backup de cada banco de dados.
2. Atualize instâncias do SQL Server que hospedam réplicas de secundário.

    a. Atualize primeiro réplicas secundárias assíncronas.

    b. Atualize as réplicas secundárias síncronas.

   >[!NOTE]
   >Se um grupo de disponibilidade tiver apenas assíncrona réplicas - para evitar a perda de dados altere uma réplica de síncrona e aguarde até que ele é sincronizado. Em seguida, atualize esta réplica.
   
   b. 1. Parar o recurso no nó que hospeda a réplica secundária de destino para atualização
   
   Antes de executar o comando Atualizar, pare o recurso para que o cluster não monitorá-lo e fazer failover desnecessariamente. O exemplo a seguir adiciona uma restrição de local no nó que resultará no recurso deve ser interrompida. Atualização `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica de destino para atualização.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```
   b. 2. Atualize o SQL Server na réplica secundária

   O exemplo seguinte atualiza `mssql-server` e `mssql-server-ha` pacotes.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   b. 3. Remover a restrição de local

   Antes de executar o comando Atualizar, pare o recurso para que o cluster não monitorá-lo e fazer failover desnecessariamente. O exemplo a seguir adiciona uma restrição de local no nó que resultará no recurso deve ser interrompida. Atualização `ag_cluster-master` com o nome do recurso e `nodeName1` com o nó que hospeda a réplica de destino para atualização.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Como prática recomendada, verifique se o recurso é iniciado (usando `pcs status` comando) e a réplica secundária está conectada e estado sincronizado após a atualização.

1. Depois que todas as réplicas secundárias são atualizadas, o failover manualmente para uma das réplicas secundárias síncronas.

   Para grupos de disponibilidade com `EXTERNAL` tipo de cluster, use as ferramentas de gerenciamento de cluster falha over; grupos de disponibilidade com `NONE` tipo de cluster deve usar o Transact-SQL para fazer o failover. 
   O exemplo a seguir failover em um grupo de disponibilidade com as ferramentas de gerenciamento de cluster. Substituir `<targetReplicaName>` com o nome da réplica secundária síncrona que se tornará primário:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >As etapas a seguir se aplicam somente aos grupos de disponibilidade que não têm um Gerenciador de cluster.  
   Se o tipo de cluster do grupo de disponibilidade é `NONE`, manualmente o failover. Conclua as seguintes etapas nesta ordem:

      a. O comando a seguir define a réplica primária para o secundário. Substituir `AG1` com o nome do seu grupo de disponibilidade. Execute o comando Transact-SQL na instância do SQL Server que hospeda a réplica primária.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. O comando a seguir define uma réplica secundária síncrona como primário. Execute o seguinte comando Transact-SQL na instância de destino do SQL Server - a instância que hospeda a réplica secundária síncrona.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Após o failover, atualize o SQL Server na réplica primária antiga, repetindo o mesmo procedimento descrito nas etapas b. 1-b. 3 acima.

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

1. Um para grupos de disponibilidade com um cluster externo manager - qual tipo de cluster é externo, a restrição de local que foi causada pelo failover manual de limpeza. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Retomar a movimentação de dados para a réplica secundária recém-atualizado - a réplica primária antiga. Isso é necessário quando uma instância de versão superior do SQL Server está transferindo blocos de log para uma instância de versão inferior em um grupo de disponibilidade. Execute o seguinte comando na nova réplica secundária (a réplica primária anterior).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Depois de atualizar todos os servidores, você pode failback - failover de volta para a primária original - se necessário. 

## <a name="drop-an-availability-group"></a>Remover um grupo de disponibilidade

Para excluir um grupo de disponibilidade, execute [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Se o tipo de cluster for `EXTERNAL` ou `NONE` executar o comando em cada instância do SQL Server que hospeda uma réplica. Por exemplo, para remover um grupo de disponibilidade denominada `group_name` execute o seguinte comando:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Próximas etapas

[Configurar o Cluster do Red Hat Enterprise Linux para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o Cluster do SUSE Linux Enterprise Server para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o Cluster Ubuntu para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
