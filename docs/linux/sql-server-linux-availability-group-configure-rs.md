---
title: "Configurar o grupo de disponibilidade de expansão de leitura para o SQL Server no Linux | Microsoft Docs"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: cf249ff8e6d2e82d1cf413bdec0272e3796b72cb
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-read-scale-out-availability-group-for-sql-server-on-linux"></a>Configurar o grupo de disponibilidade de expansão de leitura para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Você pode configurar um grupo de disponibilidade de expansão de leitura para o SQL Server no Linux. Há duas arquiteturas de grupos de disponibilidade. Um *alta disponibilidade* arquitetura usa um Gerenciador de cluster para fornecer melhor continuidade de negócios. Essa arquitetura também pode incluir leitura réplicas de expansão. Para criar a arquitetura de alta disponibilidade, consulte [configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md).

Este documento explica como criar um *expansão leitura* grupo de disponibilidade sem um Gerenciador de cluster. Essa arquitetura fornece somente leitura expansão apenas. Ele não fornece alta disponibilidade.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Criar o grupo de disponibilidade

Crie o grupo de disponibilidade. Set `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = NONE`. Aplicativos cliente executar a análise ou cargas de trabalho de emissão de relatórios diretamente pode se conectar aos bancos de dados secundários. Você também pode criar uma lista de roteamento somente leitura. Conexões com a réplica primária encaminhar solicitações de leitura conexão para cada uma das réplicas secundárias de lista de roteamento de forma round robin.

Script Transact-SQL a seguir cria um nome de grupo de disponibilidade `ag1`. O script configura as réplicas de grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server criar automaticamente o banco de dados em cada servidor secundário depois que ela é adicionada ao grupo de disponibilidade. Atualize o script a seguir para o seu ambiente. Substitua o `**<node1>**` e `**<node2>**` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `**<5022>**` com a porta configurada para o ponto de extremidade. Execute o Transact-SQL a seguir na réplica primária do SQL Server:

```Transact-SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'**<node1>**' WITH (
            ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'**<node2>**' WITH ( 
            ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-availability-group"></a>Ingressar em servidores SQL secundários ao grupo de disponibilidade

Script Transact-SQL a seguir une um servidor a um grupo de disponibilidade denominado `ag1`. Atualize o script para o seu ambiente. Em cada réplica secundária do SQL Server, execute o seguinte Transact-SQL para ingressar no grupo de disponibilidade.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Isso não é uma configuração de alta disponibilidade, se você precisar de alta disponibilidade, siga as instruções em [Configurar grupo de disponibilidade AlwaysOn para SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md). Especificamente, crie o grupo de disponibilidade com `CLUSTER_TYPE=WSFC` (no Windows) ou `CLUSTER_TYPE=EXTERNAL` (no Linux) e integrar com um Gerenciador de cluster - o WSFC no Windows ou Pacemaker no Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conecte-se às réplicas secundárias somente leitura

Há duas maneiras de se conectar a réplicas secundária somente leitura. Aplicativos podem se conectar diretamente à instância do SQL Server que hospeda a réplica secundária e os bancos de dados de consulta, ou eles podem usar o roteamento somente leitura. roteamento somente leitura requer um ouvinte.

[Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[roteamento somente leitura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-out-availability-group"></a>O failover de réplica primária no grupo de disponibilidade de expansão de leitura

Cada grupo de disponibilidade tiver apenas uma réplica primária. A réplica primária permite que as leituras e gravações. Para alterar a réplica da qual é o primário, você pode fazer failover. Em um grupo de disponibilidade para alta disponibilidade, o Gerenciador de cluster automatiza o processo de failover. Em um grupo de disponibilidade de expansão de leitura, o processo de failover é manual. Há duas maneiras de fazer failover a réplica primária em um grupo de disponibilidade de leitura de escala.

- Forçado manual falhar em perda de dados

- Failover manual sem perda de dados

### <a name="forced-fail-over-with-data-loss"></a>Forçado failover com perda de dados

Use este método quando a réplica primária não está disponível e não pode ser recuperada. Você pode encontrar mais informações sobre failover forçado com perda de dados em [executar um Failover Manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).

Force o failover com perda de dados, conecte-se à instância do SQL que hospeda a réplica secundária de destino e executar:
```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] FORCE_FAILOVER_ALLOW_DATA_LOSS;
```

### <a name="manual-fail-over-without-data-loss"></a>Failover manual sem perda de dados

Use esse método quando a réplica primária está disponível, mas você precisa temporariamente ou permanentemente a alterar a configuração e alterar a instância do SQL Server que hospeda a réplica primária. Antes de emitir falha manual em, certifique-se de que a réplica secundária de destino é atualizada, para que não haja nenhuma perda de dados. 

As etapas a seguir descrevem como failover manual sem perda de dados:

1. Verifique a confirmação síncrona de réplica secundária de destino.

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] MODIFY REPLICA ON N'**<node2>*' WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);
   ```
1. Atualização `required_synchronized_secondaries_to_commit`como 1.

   Essa configuração garante que todas as transações ativas é confirmada para a réplica primária e pelo menos um secundário síncrono. O grupo de disponibilidade está pronto para failover quando o synchronization_state_desc é SINCRONIZADA e o sequence_number é o mesmo para ambos os primário e réplica secundária de destino. Execute esta consulta para verificar:

   ```Transact-SQL
   SELECT ag.name, 
      drs.database_id, 
      drs.group_id, 
      drs.replica_id, 
      drs.synchronization_state_desc, 
      ag.sequence_number
   FROM sys.dm_hadr_database_replica_states drs, sys.availability_groups ag
   WHERE drs.group_id = ag.group_id; 
   ```

1. Rebaixe a réplica primária para a réplica secundária. Depois que a réplica primária é rebaixada, ele é somente leitura. Execute este comando na instância do SQL que hospeda a réplica primária para atualizar a função para SECUNDÁRIO:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY); 
   ```

1. Promova a réplica secundária de destino para o primário. 

   ```Transact-SQL
   ALTER AVAILABILITY GROUP distributedag FORCE_FAILOVER_ALLOW_DATA_LOSS; 
   ```  

   > [!NOTE] 
   > Para excluir um grupo de disponibilidade, use [DROP AVAILABILITY GROUP](https://docs.microsoft.com/en-us/sql/t-sql/statements/drop-availability-group-transact-sql). Para um grupo de disponibilidade criado com CLUSTER_TYPE NONE ou externo, o comando tem de ser executada em todas as partes de réplicas do grupo de disponibilidade.

## <a name="next-steps"></a>Próximas etapas

[Configurar o grupo de disponibilidade distribuída](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Saiba mais sobre grupos de disponibilidade](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)


