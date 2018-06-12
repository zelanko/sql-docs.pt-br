---
title: Configurar um grupo de disponibilidade do SQL Server de escala de leitura no Windows | Microsoft Docs
description: ''
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: conceptual
ms.prod: sql
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.openlocfilehash: de62bd96371e93e9491b9c781da3b41f7086dc75
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34768342"
---
# <a name="configure-a-sql-server-availability-group-for-read-scale-on-windows"></a>Configurar um grupo de disponibilidade do SQL Server de escala de leitura no Windows

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

É possível configurar um AG (grupo de disponibilidade) Always On do SQL Server para cargas de trabalho de escala de leitura no Windows. Há dois tipos de arquiteturas para grupos de disponibilidade. Uma arquitetura para alta disponibilidade usa um gerenciador de clusters para oferecer uma melhor continuidade de negócios e pode incluir réplicas secundárias legíveis. Para criar essa arquitetura de alta disponibilidade, consulte [Creation and Configuration of Availability Groups on Windows](creation-and-configuration-of-availability-groups-sql-server.md) (Criação e configuração de grupos de disponibilidade no Windows). A outra arquitetura é compatível apenas com cargas de trabalho de escala de leitura. Este artigo explica como criar um grupo de disponibilidade sem um gerenciador de clusters para cargas de trabalho de leitura de escala. Essa arquitetura fornece apenas uma escala de leitura. Ela não oferece alta disponibilidade.

>[!NOTE]
>Um grupo de disponibilidade com `CLUSTER_TYPE = NONE` pode incluir réplicas hospedadas em diferentes plataformas de sistema operacional. Ele não é compatível com alta disponibilidade. Para o sistema operacional Linux, consulte [Configurar um grupo de disponibilidade do SQL Server para a escala de leitura no Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-the-ag"></a>Criar o grupo de disponibilidade

Crie o grupo de disponibilidade. Defina `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = NONE`. Os aplicativos cliente que executam cargas de trabalho de análise ou relatório podem se conectar aos bancos de dados secundários diretamente. Também é possível criar uma lista de roteamento somente leitura. As conexões com a réplica primária encaminham solicitações de conexão de leitura para cada uma das réplicas secundárias da lista de roteamento usando um mecanismo round robin.

O script Transact-SQL a seguir cria um grupo de disponibilidade chamado `ag1`. O script configura as réplicas do grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração fará o SQL Server criar automaticamente o banco de dados em cada servidor secundário após ele ser adicionado ao grupo de disponibilidade. Atualize o script a seguir para o seu ambiente. Substitua os valores `<node1>` e `<node2>` pelos nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` valor pela porta definida para o ponto de extremidade. Execute o script Transact-SQL a seguir na réplica primária do SQL Server:

```sql
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

### <a name="join-secondary-sql-servers-to-the-ag"></a>Ingressar SQL Servers secundários no grupo de disponibilidade

O script Transact-SQL a seguir ingressa um servidor em um grupo de disponibilidade chamado `ag1`. Atualize o script para o seu ambiente. Em cada réplica secundária do SQL Server, execute o seguinte script Transact-SQL para ingressar o grupo de disponibilidade:

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

Esse grupo de disponibilidade não é uma configuração de alta disponibilidade. Se precisar de alta disponibilidade, siga as instruções em [Configurar um grupo de disponibilidade Always On para o SQL Server em Linux](../../../linux/sql-server-linux-availability-group-configure-ha.md) ou [Criação e configuração de grupos de disponibilidade no Windows](creation-and-configuration-of-availability-groups-sql-server.md).

## <a name="connect-to-read-only-secondary-replicas"></a>Conectar-se a réplicas secundárias somente leitura

Há duas maneiras de se conectar a réplicas secundárias somente leitura. Os aplicativos podem conectar-se diretamente à instância do SQL Server que hospeda a réplica secundária e consulta os bancos de dados. Eles também podem usar roteamento somente leitura, que requer um ouvinte.

* [Réplicas secundárias legíveis](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)
* [Roteamento somente leitura](listeners-client-connectivity-application-failover.md#ConnectToSecondary)

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Próximas etapas

* [Configurar um grupo de disponibilidade distribuído](distributed-availability-groups-always-on-availability-groups.md)
* [Saiba mais sobre grupos de disponibilidade](overview-of-always-on-availability-groups-sql-server.md)
* [Executar um failover manual forçado](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
