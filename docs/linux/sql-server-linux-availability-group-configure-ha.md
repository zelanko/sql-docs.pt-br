---
title: Configurar o grupo de disponibilidade para o SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 
ms.workload: On Demand
ms.openlocfilehash: e75ae9a6f3c48f0ece0c95be9f3836c8205a1b8c
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="configure-always-on-availability-group-for-sql-server-on-linux"></a>Configurar o grupo de disponibilidade do AlwaysOn para SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este artigo descreve como criar um SQL Server AlwaysOn no grupo de disponibilidade para alta disponibilidade no Linux. Há dois tipos de configuração para grupos de disponibilidade. Um *alta disponibilidade* configuração usa um Gerenciador de cluster para fornecer continuidade de negócios. Essa configuração também pode incluir réplicas de escala de leitura. Este documento explica como criar a configuração de alta disponibilidade do grupo de disponibilidade.

Você também pode criar um *leitura escala* grupo de disponibilidade sem um Gerenciador de cluster. Essa configuração fornece apenas réplicas somente leitura para expansão de desempenho. Ele não fornece alta disponibilidade. Para criar um grupo de disponibilidade de escala de leitura, consulte [configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md).

Configurações que garantem alta disponibilidade e proteção de dados necessitam de réplicas de confirmação de duas ou três síncrona. Com três réplicas síncronas o grupo de disponibilidade podem automaticamente recuperação mesmo que um servidor não está disponível. Para obter mais informações, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). 

Todos os servidores devem ser físicos ou virtuais e servidores virtuais devem ter a mesma plataforma de virtualização. Esse requisito é como os agentes de isolamento são específicas à plataforma. Consulte [políticas para Clusters convidados](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Roadmap

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto níveis: 

1. [Configurar o SQL Server em três servidores de cluster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Todos os três servidores no grupo de disponibilidade precisam ser a mesma plataforma - físico ou virtual - como alta disponibilidade do Linux usa agentes de isolamento para isolar recursos de servidores. Os agentes de isolamento são específicos para cada plataforma.

2. Crie o grupo de disponibilidade. Esta etapa é abordada neste artigo atual. 

3. Configure um Gerenciador de recursos de cluster, como Pacemaker.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende da distribuição específica do Linux. Consulte os links a seguir para obter instruções específicas de distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento, como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster do Linux usa isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende a distribuição e o ambiente. Atualmente, o isolamento não está disponível em alguns ambientes de nuvem. Para obter mais informações, consulte [políticas de suporte para Clusters de disponibilidade alta RHEL - plataformas de virtualização](https://access.redhat.com/articles/29440).
   
   >Para SLES, consulte [extensão de alta disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Adicione o grupo de disponibilidade como um recurso do cluster.  

   A maneira de adicionar o grupo de disponibilidade como um recurso do cluster depende a distribuição de Linux. Consulte os links a seguir para obter instruções específicas de distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-availability-group"></a>Criar o grupo de disponibilidade

Há duas configurações de grupo de disponibilidade com suporte para o SQL Server no Linux.

- [Três réplicas síncronas](sql-server-linux-availability-group-ha.md#threeSynch)

- [Duas réplicas síncronas](sql-server-linux-availability-group-ha.md#twoSynch)

Para obter informações, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

Crie o grupo de disponibilidade para alta disponibilidade no Linux. Use o [criar grupo de disponibilidade](https://docs.microsoft.com/en-us/sql/t-sql/statements/create-availability-group-transact-sql) com `CLUSTER_TYPE = EXTERNAL`. 

* O grupo de disponibilidade - `CLUSTER_TYPE = EXTERNAL` Especifica que uma entidade de cluster externo gerencia o grupo de disponibilidade. Pacemaker é um exemplo de uma entidade de cluster externo. Quando o tipo de cluster do grupo de disponibilidade é externo, 

* Conjunto de réplicas primárias e secundárias `FAILOVER_MODE = EXTERNAL`. 
   Especifica que a réplica interage com um Gerenciador de cluster externo, como Pacemaker. 

Os scripts de Transact-SQL a seguir cria um grupo de disponibilidade para alta disponibilidade chamado `ag1`. O script configura as réplicas de grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server criar automaticamente o banco de dados em cada servidor secundário. Atualize o script a seguir para o seu ambiente. Substitua o `**<node1>**`, `**<node2>**`, ou `**<node3>**` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `**<5022>**` com a porta que você definiu para os ponto de extremidade do espelhamento de dados. Para criar o grupo de disponibilidade, execute o Transact-SQL a seguir na instância do SQL Server que hospeda a réplica primária.

Executar **apenas um** dos scripts a seguir: 

- [Criar grupo de disponibilidade com réplicas síncronas três](#threeSynch).
- [Criar grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração](#configOnly)
- [Criar grupo de disponibilidade com duas réplicas síncronas](#readScale).

<a name="threeSynch"></a>

- Criar grupo de disponibilidade com três réplicas síncronas

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'**<node1>**' 
            WITH (
               ENDPOINT_URL = N'tcp://**<node1>:**<5022>**',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node2>**' 
            WITH ( 
               ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'**<node3>**'
           WITH( 
              ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >Após executar o script anterior para criar um grupo de disponibilidade com três réplicas síncronas, não execute o script a seguir:

- Crie grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração:

   >[!IMPORTANT]
   >Essa arquitetura permite que qualquer edição do SQL Server para hospedar a réplica de terceira. Por exemplo, a terceira réplica pode ser hospedada no SQL Server Enterprise Edition. Na Enterprise Edition, é o tipo de ponto de extremidade válido apenas `WITNESS`. 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'**<node1>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node1>**:**<5022>**', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node2>**' WITH (  
          ENDPOINT_URL = N'tcp://**<node2>**:**<5022>**',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'**<node3>**' WITH ( 
          ENDPOINT_URL = N'tcp://**<node3>**:**<5022>**', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- Criar grupo de disponibilidade com duas réplicas síncronas

   Inclua duas réplicas com o modo de disponibilidade síncrona. Por exemplo, o script a seguir cria um grupo de disponibilidade chamado `ag1`. `node1`e `node2` hospedam réplicas de modo síncrono, com failover automático e a propagação automática.

   >[!IMPORTANT]
   >Somente execute o script a seguir para criar um grupo de disponibilidade com duas réplicas síncronas. Não execute o script a seguir se você executou o script anterior. 

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


Você também pode configurar um grupo de disponibilidade com `CLUSTER_TYPE=EXTERNAL` usando o SQL Server Management Studio ou PowerShell. 

### <a name="join-secondary-replicas-to-the-availability-group"></a>Unir réplicas secundárias ao grupo de disponibilidade

Script Transact-SQL a seguir une a uma instância do SQL Server a um grupo de disponibilidade denominado `ag1`. Atualize o script para o seu ambiente. Em cada instância do SQL Server que hospeda uma réplica secundária, execute o seguinte Transact-SQL para ingressar no grupo de disponibilidade.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Depois de criar o grupo de disponibilidade, você deve configurar a integração com uma tecnologia de cluster como Pacemaker para alta disponibilidade. Para uma configuração de escala de leitura usando grupos de disponibilidade, começando com [!INCLUDE [SQL Server version](..\includes\sssqlv14-md.md)], não é necessário configurar um cluster.

Se você seguiu as etapas neste documento, você tem um grupo de disponibilidade ainda não está clusterizado. A próxima etapa é adicionar o cluster. Essa configuração é inválida para cenários de balanceamento de carga-de escala de leitura, ele não foi concluído para alta disponibilidade. Para alta disponibilidade, você precisa adicionar o grupo de disponibilidade como um recurso de cluster. Consulte [próximas etapas](#next-steps) para obter instruções. 

## <a name="notes"></a>Observações

>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão ligados como intimamente com o sistema operacional como estão em um Cluster de Failover do Windows Server (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração todos é feita por meio das ferramentas de gerenciamento de cluster. Em RHEL ou Ubuntu usar `pcs`. SLES usar `crm`. 

>[!IMPORTANT]
>Se o grupo de disponibilidade é um recurso de cluster, há um problema conhecido na versão atual, em que o failover forçado com perda de dados para uma réplica assíncrona não funciona. Isso será corrigido na próxima versão. Failover manual ou automático para uma réplica de síncrona terá êxito. 


## <a name="next-steps"></a>Próximas etapas

[Configurar o Cluster do Red Hat Enterprise Linux para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o Cluster do SUSE Linux Enterprise Server para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o Cluster Ubuntu para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
