---
title: Configurar uma escala de leitura para um grupo de disponibilidade
description: Configure o Grupo de Disponibilidade AlwaysOn para cargas de trabalho de escala de leitura no Windows.
ms.custom: seodec18
author: MashaMSFT
ms.author: mathoma
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: high-availability
ms.openlocfilehash: 3ff0064a228cb756614dec2ff54a91f4f03d374c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67991158"
---
# <a name="configure-read-scale-for-an-always-on-availability-group"></a>Configurar a escala de leitura para um Grupo de Disponibilidade AlwaysOn

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

É possível configurar um grupo de disponibilidade AlwaysOn do SQL Server para cargas de trabalho de escala de leitura no Windows. Há dois tipos de arquitetura para grupos de disponibilidade:
* Uma arquitetura para alta disponibilidade que usa um gerenciador de clusters para oferecer uma melhor continuidade de negócios e que pode incluir réplicas secundárias legíveis. Para criar essa arquitetura de alta disponibilidade, consulte [Criar e configurar grupos de disponibilidade no Windows](creation-and-configuration-of-availability-groups-sql-server.md). 
* Uma arquitetura que dá suporte apenas a cargas de trabalho de escala de leitura. 

Este artigo explica como criar um grupo de disponibilidade sem um gerenciador de clusters para cargas de trabalho de escala de leitura. Essa arquitetura fornece apenas uma escala de leitura. Ela não oferece alta disponibilidade.

>[!NOTE]
>Um grupo de disponibilidade com `CLUSTER_TYPE = NONE` pode incluir réplicas hospedadas em diferentes plataformas de sistema operacional. Ele não é compatível com alta disponibilidade. Para o sistema operacional Linux, consulte [Configurar um grupo de disponibilidade do SQL Server para a escala de leitura no Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md).

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-an-availability-group"></a>Criar um grupo de disponibilidade

Crie um grupo de disponibilidade. Defina `CLUSTER_TYPE = NONE`. Além disso, defina cada réplica com `FAILOVER_MODE = NONE`. Aplicativos cliente que executam cargas de trabalho de análises ou de relatórios podem conectar-se diretamente aos bancos de dados secundários. Também é possível criar uma lista de roteamento somente leitura. As conexões com a réplica primária encaminham solicitações de conexão de leitura para cada uma das réplicas secundárias da lista de roteamento usando um mecanismo round robin.

O script Transact-SQL a seguir cria um grupo de disponibilidade chamado `ag1`. O script configura as réplicas do grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração fará o SQL Server criar automaticamente o banco de dados em cada servidor secundário após ele ser adicionado ao grupo de disponibilidade. 

Atualize o script a seguir para o seu ambiente. Substitua os valores `<node1>` e `<node2>` pelos nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` valor pela porta que você definiu para o ponto de extremidade. Execute o script Transact-SQL a seguir na réplica primária do SQL Server:

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

### <a name="join-secondary-sql-server-instances-to-the-availability-group"></a>Ingressar instâncias secundárias do SQL Server no grupo de disponibilidade

O script Transact-SQL a seguir ingressa um servidor em um grupo de disponibilidade chamado `ag1`. Atualize o script para o seu ambiente. Para ingressar no grupo de disponibilidade, execute o seguinte script Transact-SQL em cada réplica secundária do SQL Server:

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

Esse grupo de disponibilidade não é uma configuração de alta disponibilidade. Se precisar de alta disponibilidade, siga as instruções em [Configurar um grupo de disponibilidade AlwaysOn para o SQL Server em Linux](../../../linux/sql-server-linux-availability-group-configure-ha.md) ou [Criação e configuração de grupos de disponibilidade no Windows](creation-and-configuration-of-availability-groups-sql-server.md).

## <a name="connect-to-read-only-secondary-replicas"></a>Conectar-se a réplicas secundárias somente leitura

Há duas maneiras para se conectar a réplicas secundárias somente leitura:
* Os aplicativos podem conectar-se diretamente à instância do SQL Server que hospeda a réplica secundária e consulta os bancos de dados. Para obter mais informações, consulte [Réplicas secundárias legíveis](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).
* Aplicativos também podem usar roteamento somente leitura, que requer um ouvinte. Para obter mais informações, consulte [Roteamento somente leitura](listeners-client-connectivity-application-failover.md#ConnectToSecondary).

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>Próximas etapas

* [Configurar um grupo de disponibilidade distribuído](distributed-availability-groups-always-on-availability-groups.md)
* [Saiba mais sobre grupos de disponibilidade](overview-of-always-on-availability-groups-sql-server.md)
* [Executar um failover manual forçado](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)
