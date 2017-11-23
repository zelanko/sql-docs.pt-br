---
title: Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 10/20/2017
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
ms.openlocfilehash: bd3fa34a4fbfe40dfe184f7d5cf0e1f64372c8f2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="configure-read-scale-availability-group-for-sql-server-on-linux"></a>Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Você pode configurar um grupo de disponibilidade de escala de leitura para o SQL Server no Linux. Há duas arquiteturas de grupos de disponibilidade. Um *alta disponibilidade* arquitetura usa um Gerenciador de cluster para fornecer melhor continuidade de negócios. Essa arquitetura também pode incluir leitura escala réplicas. Para criar a arquitetura de alta disponibilidade, consulte [configurar sempre no grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md).

Este documento explica como criar um *leitura escala* grupo de disponibilidade sem um Gerenciador de cluster. Essa arquitetura fornece apenas a escala de leitura somente. Ele não fornece alta disponibilidade.

[!INCLUDE [Create prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Criar o grupo de disponibilidade

Crie o grupo de disponibilidade. Set `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = NONE`. Aplicativos cliente executar a análise ou cargas de trabalho de emissão de relatórios diretamente pode se conectar aos bancos de dados secundários. Você também pode criar uma lista de roteamento somente leitura. Conexões com a réplica primária encaminhar solicitações de leitura conexão para cada uma das réplicas secundárias de lista de roteamento de forma round robin.

Script Transact-SQL a seguir cria um nome de grupo de disponibilidade `ag1`. O script configura as réplicas de grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server criar automaticamente o banco de dados em cada servidor secundário depois que ela é adicionada ao grupo de disponibilidade. Atualize o script a seguir para o seu ambiente. Substitua o `**<node1>**` e `**<node2>**` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `**<5022>**` com a porta configurada para o ponto de extremidade. Execute o Transact-SQL a seguir na réplica primária do SQL Server:

```SQL
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

```SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

Isso não é uma configuração de alta disponibilidade, se você precisar de alta disponibilidade, siga as instruções em [Configurar grupo de disponibilidade AlwaysOn para SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md). Especificamente, crie o grupo de disponibilidade com `CLUSTER_TYPE=WSFC` (no Windows) ou `CLUSTER_TYPE=EXTERNAL` (no Linux) e integrar com um Gerenciador de cluster - o WSFC no Windows ou Pacemaker no Linux.

## <a name="connect-to-read-only-secondary-replicas"></a>Conecte-se às réplicas secundárias somente leitura

Há duas maneiras de se conectar a réplicas secundária somente leitura. Aplicativos podem se conectar diretamente à instância do SQL Server que hospeda a réplica secundária e os bancos de dados de consulta, ou eles podem usar o roteamento somente leitura. roteamento somente leitura requer um ouvinte.

[Réplicas secundárias legíveis](../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)

[roteamento somente leitura](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-primary-replica-on-read-scale-availability-group"></a>O failover de réplica primária no grupo de disponibilidade de escala de leitura

[!INCLUDE[Force Failover](../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Próximas etapas

[Configurar um grupo de disponibilidade distribuído](..\database-engine\availability-groups\windows\distributed-availability-groups-always-on-availability-groups.md)

[Saiba mais sobre grupos de disponibilidade](..\database-engine\availability-groups\windows\overview-of-always-on-availability-groups-sql-server.md)

[Executar um Failover Manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md).

