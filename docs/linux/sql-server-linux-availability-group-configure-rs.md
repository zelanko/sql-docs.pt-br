---
title: Configurar um grupo de disponibilidade do SQL Server para a escala de leitura no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e406248118933eb60e95e101c6812d61b72ad7a7
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323297"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-linux"></a>Configurar um grupo de disponibilidade do SQL Server para a escala de leitura no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode configurar um SQL Server sempre na disponibilidade de grupo (AG) para cargas de trabalho de leitura de escala no Linux. Há dois tipos de arquiteturas de grupos de disponibilidade. Uma arquitetura de alta disponibilidade usa um Gerenciador de cluster para fornecer melhor continuidade de negócios. Essa arquitetura também pode incluir leitura escala réplicas. Para criar a arquitetura de alta disponibilidade, consulte [configurar o SQL Server sempre no grupo de disponibilidade para alta disponibilidade no Linux](sql-server-linux-availability-group-configure-ha.md). Arquitetura de dá suporte a cargas de trabalho somente leitura de escala. Este artigo explica como criar um grupo de disponibilidade sem um Gerenciador de cluster para cargas de trabalho de leitura de escala. Essa arquitetura fornece a escala de leitura somente. Ele não fornece alta disponibilidade.

>[!NOTE]
>Um grupo de disponibilidade com `CLUSTER_TYPE = NONE` pode incluir réplicas hospedadas em plataformas de sistema operacional diferente. Ele não oferece suporte a alta disponibilidade. 

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Criar o grupo de disponibilidade

Crie o grupo de disponibilidade. Set `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = NONE`. Aplicativos cliente executar a análise ou cargas de trabalho de emissão de relatórios diretamente pode se conectar aos bancos de dados secundários. Você também pode criar uma lista de roteamento somente leitura. Conexões com a réplica primária para a frente leiam solicitações de conexão para cada uma das réplicas secundárias a lista de roteamento em uma forma round-robin.

Script Transact-SQL a seguir cria um grupo de disponibilidade denominado `ag1`. O script configura as réplicas de AG com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server criar automaticamente o banco de dados em cada servidor secundário depois que ela é adicionada para o grupo de disponibilidade. Atualize o script a seguir para o seu ambiente. Substitua o `<node1>` e `<node2>` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` valor com a porta configurada para o ponto de extremidade. Execute o seguinte script do Transact-SQL na réplica primária do SQL Server:

```SQL
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH ( 
            ENDPOINT_URL = N'tcp://<node2>:<5022>', 
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );
        
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-servers-to-the-ag"></a>Ingressar em servidores SQL secundários para o grupo de disponibilidade

Script Transact-SQL a seguir une um servidor a um grupo de disponibilidade denominado `ag1`. Atualize o script para o seu ambiente. Em cada réplica secundária do SQL Server, execute o seguinte script do Transact-SQL para unir o grupo de disponibilidade:

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Este grupo de disponibilidade não é uma configuração de alta disponibilidade. Se você precisar de alta disponibilidade, siga as instruções em [configurar um grupo de disponibilidade AlwaysOn para SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md). Especificamente, criar o grupo de disponibilidade com `CLUSTER_TYPE=WSFC` (no Windows) ou `CLUSTER_TYPE=EXTERNAL` (no Linux). Em seguida, integre um Gerenciador de cluster usando o Windows Server cluster de failover na Windows ou Pacemaker no Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conecte-se às réplicas secundárias somente leitura

Há duas maneiras de se conectar a réplicas secundárias somente leitura. Aplicativos podem se conectar diretamente à instância do SQL Server que hospeda a réplica secundária e os bancos de dados de consulta. Eles também podem usar o roteamento somente leitura, que requer um ouvinte.

* [Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [Roteamento somente leitura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Failover de réplica primária em um grupo de disponibilidade de escala de leitura

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Próximas etapas

* [Configurar um grupo de disponibilidade distribuída](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)
* [Saiba mais sobre grupos de disponibilidade](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)
* [Executar um failover manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)

