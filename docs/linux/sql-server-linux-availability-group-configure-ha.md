---
title: Configurar o grupo de disponibilidade Always On do SQL Server para alta disponibilidade no Linux
titleSuffix: SQL Server
description: Saiba mais sobre como criar um AG (grupo de disponibilidade) Always On do SQL Server para alta disponibilidade no Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e97708fc227cbbcadfeb6fe961fce2ad9ee41765
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68027248"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configurar o grupo de disponibilidade Always On do SQL Server para alta disponibilidade no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como criar um AG (grupo de disponibilidade) Always On do SQL Server para alta disponibilidade no Linux. Há dois tipos de configuração para AGs. Uma configuração de *alta disponibilidade* usa um gerenciador de clusters para fornecer continuidade dos negócios. Essa configuração também pode incluir réplicas de escala de leitura. Este documento explica como criar o AG para alta disponibilidade.

Você também pode criar um AG sem um gerenciador de clusters para *escala de leitura*. O AG para escala de leitura fornece apenas réplicas somente leitura para expansão do desempenho. Ele não fornece alta disponibilidade. Para criar um AG para escala de leitura, confira [Configurar um grupo de disponibilidade do SQL Server para escala de leitura no Linux](sql-server-linux-availability-group-configure-rs.md).

As configurações que garantem alta disponibilidade e proteção de dados exigem duas ou três réplicas de confirmação síncronas. Com três réplicas síncronas, o AG pode se recuperar automaticamente mesmo que um servidor não esteja disponível. Para obter mais informações, confira [Alta disponibilidade e proteção de dados para configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). 

Todos os servidores devem ser físicos ou virtuais e os servidores virtuais devem estar na mesma plataforma de virtualização. Esse requisito ocorre porque os agentes de isolamento são específicos da plataforma. Confira [Políticas para clusters de convidados](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Roteiro

As etapas para criar um AG em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A seguinte lista descreve as etapas de alto nível: 

1. [Configurar o SQL Server em três servidores de cluster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Os três servidores do AG precisam estar na mesma plataforma – física ou virtual – porque a alta disponibilidade do Linux usa agentes de isolamento para isolar os recursos nos servidores. Os agentes de isolamento são específicos para cada plataforma.

2. Crie o grupo de disponibilidade. Esta etapa é abordada no presente artigo. 

3. Configurar um gerenciador de recursos de cluster, como o Pacemaker.
   
   A maneira de configurar um gerenciador de recursos de cluster depende da distribuição específica do Linux. Confira os links a seguir para obter instruções específicas para cada distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Os ambientes de produção exigem um agente de isolamento, como o STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações se destinam apenas a teste e validação. 
   
   >Um cluster do Linux usa o isolamento para retornar o cluster a um estado conhecido. A maneira de configurar o isolamento depende da distribuição e do ambiente. Atualmente, o isolamento não está disponível em alguns ambientes de nuvem. Para obter mais informações, confira [Políticas de suporte para clusters de alta disponibilidade do RHEL – plataformas de virtualização](https://access.redhat.com/articles/29440).
   
   >Para o SLES, confira [Extensão de alta disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Adicione o AG como um recurso no cluster.  

   A maneira de adicionar o AG como um recurso no cluster depende da distribuição do Linux. Confira os links a seguir para obter instruções específicas para cada distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Criar o grupo de disponibilidade

Os exemplos desta seção explicam como criar o grupo de disponibilidade usando o Transact-SQL. Você também pode usar o assistente de grupo de disponibilidade do SQL Server Management Studio. Quando você cria um AG com o assistente, ele retorna um erro ao unir as réplicas ao AG. Para corrigir isso, conceda `ALTER`, `CONTROL` e `VIEW DEFINITIONS` ao pacemaker no AG em todas as réplicas. Depois que as permissões forem concedidas na réplica primária, una os nós ao AG por meio do assistente, mas para que a HA funcione corretamente, conceda permissão em todas as réplicas.

Para uma configuração de alta disponibilidade que garanta o failover automático, o AG requer pelo menos três réplicas. Qualquer uma das configurações a seguir pode dar suporte à alta disponibilidade:

- [Três réplicas síncronas](sql-server-linux-availability-group-ha.md#threeSynch)

- [Duas réplicas síncronas mais uma réplica de configuração](sql-server-linux-availability-group-ha.md#twoSynch)

Para obter informações, confira [Alta disponibilidade e proteção de dados para configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Os grupos de disponibilidade podem incluir réplicas síncronas ou assíncronas adicionais. 

Crie o AG para alta disponibilidade no Linux. Use o [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) com `CLUSTER_TYPE = EXTERNAL`. 

* Grupo de disponibilidade – `CLUSTER_TYPE = EXTERNAL` Especifica que uma entidade de cluster externa gerencia o AG. O pacemaker é um exemplo de entidade de cluster externa. Quando o tipo de cluster AG é externo, 

* Configure as réplicas primária e secundária como `FAILOVER_MODE = EXTERNAL`. 
   Especifica que a réplica interage com um gerenciador de clusters externo, como Pacemaker. 

Os scripts Transact-SQL a seguir criam um AG para alta disponibilidade chamado `ag1`. O script configura as réplicas do grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server crie automaticamente o banco de dados em cada servidor secundário. Atualize o script a seguir para o seu ambiente. Substitua os valores `<node1>`, `<node2>` e `<node3>` pelos nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` pela porta definida para o ponto de extremidade de espelhamento de dados. Para criar o AG, execute o Transact-SQL a seguir na instância do SQL Server que hospeda a réplica primária.

Execute **apenas** um dos scripts a seguir: 

- [Criar grupo de disponibilidade com três réplicas síncronas](#threeSynch).
- [Criar grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração](#configOnly)
- [Criar grupo de disponibilidade com duas réplicas síncronas](#readScale).

<a name="threeSynch"></a>

- Criar AG com três réplicas síncronas

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Depois de executar o script anterior para criar um AG com três réplicas síncronas, não execute o script a seguir:

<a name="configOnly"></a>
- Criar AG com duas réplicas síncronas e uma réplica de configuração:

   >[!IMPORTANT]
   >Essa arquitetura permite que qualquer edição do SQL Server hospede a terceira réplica. Por exemplo, a terceira réplica pode ser hospedada no SQL Server Enterprise Edition. Na Edição Enterprise, o único tipo de ponto de extremidade válido é `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Criar AG com duas réplicas síncronas

   Inclua duas réplicas com o modo de disponibilidade síncrona. Por exemplo, o script a seguir cria um AG chamado `ag1`. `node1` e `node2` hospedam réplicas no modo síncrono, com propagação automática e failover automático.

   >[!IMPORTANT]
   >Execute apenas o script a seguir para criar um AG com duas réplicas síncronas. Não execute o script a seguir se tiver executado algum dos scripts anteriores. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


Você também pode configurar um AG com `CLUSTER_TYPE=EXTERNAL` usando o SQL Server Management Studio ou do PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Una réplicas secundárias ao AG

O usuário do pacemaker requer as permissões `ALTER`, `CONTROL` e `VIEW DEFINITION` no grupo de disponibilidade em todas as réplicas. Para conceder as permissões, execute o seguinte script Transact-SQL depois que o grupo de disponibilidade for criado na réplica primária e em cada réplica secundária imediatamente depois que elas forem adicionadas ao grupo de disponibilidade. Antes de executar o script, substitua `<pacemakerLogin>` pelo nome da conta de usuário do pacemaker.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

O script Transact-SQL a seguir une uma instância do SQL Server a um AG chamado `ag1`. Atualize o script para o seu ambiente. Em cada instância do SQL Server que hospeda uma réplica secundária, execute o script Transact-SQL a seguir para unir ao AG.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Depois de criar o AG, você deve configurar a integração com uma tecnologia de cluster como o pacemaker para alta disponibilidade. Para uma configuração de escala de leitura usando AGs, começando com [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], a configuração de um cluster não é necessária.

Caso tenha seguido as etapas deste documento, você terá um AG que ainda não está clusterizado. A próxima etapa é adicionar o cluster. Essa configuração é válida para cenários de escala de leitura/balanceamento de carga; ela não é completa para alta disponibilidade. Para alta disponibilidade, é preciso adicionar o AG como um recurso de cluster. Confira as [próximas etapas](#next-steps) para obter instruções. 

## <a name="notes"></a>Observações

>[!IMPORTANT]
>Depois de configurar o cluster e adicionar o AG como um recurso de cluster, você não poderá usar o Transact-SQL para fazer failover dos recursos de AG. Os recursos de cluster do SQL Server em Linux não são acoplados tão firmemente com o sistema operacional como são em um WSFC (cluster de failover do Windows Server). O serviço SQL Server não reconhece a presença do cluster. Toda a orquestração é feita por meio das ferramentas de gerenciamento de cluster. No RHEL ou no Ubuntu, use `pcs`. No SLES, use `crm`. 

>[!IMPORTANT]
>Se o AG for um recurso de cluster, haverá um problema conhecido na versão atual em que o failover forçado com perda de dados para uma réplica assíncrona não funciona. Isso será corrigido na próxima versão. O failover manual ou automático para uma réplica síncrona é feito com sucesso.


## <a name="next-steps"></a>Próximas etapas

[Configurar o cluster do Red Hat Enterprise Linux para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o cluster do SUSE Linux Enterprise Server para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o cluster do Ubuntu para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
