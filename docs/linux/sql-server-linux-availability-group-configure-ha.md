---
title: Configurar SQL Server sempre no grupo de disponibilidade para alta disponibilidade no Linux
titleSuffix: SQL Server
description: Saiba mais sobre como criar um SQL Server sempre no grupo de disponibilidade (AG) para alta disponibilidade no Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 02/14/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux, seodec18
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 9f88178450fb5ca19e52703ad02e29d107ca562a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201955"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Configurar SQL Server sempre no grupo de disponibilidade para alta disponibilidade no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve como criar um SQL Server sempre no grupo de disponibilidade (AG) para alta disponibilidade no Linux. Há dois tipos de configuração para grupos de disponibilidade. Um *alta disponibilidade* configuração usa um Gerenciador de cluster para fornecer continuidade dos negócios. Essa configuração também pode incluir a escala de leitura de réplicas. Este documento explica como criar o grupo de disponibilidade para alta disponibilidade.

Você também pode criar um grupo de disponibilidade sem um cluster para o Gerenciador *escala de leitura*. O grupo de disponibilidade de escala de leitura só fornece réplicas somente leitura para expansão de desempenho. Além disso, ele não oferece alta disponibilidade. Para criar um grupo de disponibilidade de escala de leitura, consulte [configurar um grupo de disponibilidade do SQL Server para a escala de leitura no Linux](sql-server-linux-availability-group-configure-rs.md).

Configurações que garantem a alta disponibilidade e proteção de dados exige que réplicas de confirmação de duas ou três síncrona. Com três réplicas síncronas, o grupo de disponibilidade pode se recuperar automaticamente mesmo se um servidor não está disponível. Para obter mais informações, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). 

Todos os servidores devem ser físicos ou virtuais e servidores virtuais devem estar na mesma plataforma de virtualização. Esse requisito existe porque os agentes de isolamento são específicas à plataforma. Ver [políticas para Clusters de convidado](https://access.redhat.com/articles/29440#guest_policies).

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server em três servidores de cluster](sql-server-linux-setup.md).

   >[!IMPORTANT]
   >Todos os três servidores no AG precisam estar na mesma plataforma – física ou virtual – como alta disponibilidade do Linux usa agentes de isolamento para isolar recursos em servidores. Os agentes de isolamento são específicos para cada plataforma.

2. Crie o grupo de disponibilidade. Esta etapa é abordada neste artigo atual. 

3. Configure um Gerenciador de recursos de cluster, como o Pacemaker.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende a distribuição Linux específica. Consulte os links a seguir para obter instruções específicas de distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster do Linux usa o isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende da distribuição e o ambiente. Atualmente, o isolamento não está disponível em alguns ambientes de nuvem. Para obter mais informações, consulte [políticas de suporte para Clusters de disponibilidade alta RHEL - plataformas de virtualização](https://access.redhat.com/articles/29440).
   
   >Para o SLES, confira [extensão de alta disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. Adicione o grupo de disponibilidade como um recurso no cluster.  

   A maneira de adicionar o grupo de disponibilidade como um recurso do cluster depende a distribuição do Linux. Consulte os links a seguir para obter instruções específicas de distribuição: 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>Criar o grupo de disponibilidade

Os exemplos nesta seção explicam como criar o grupo de disponibilidade usando o Transact-SQL. Você também pode usar o Assistente de grupo de disponibilidade SQL Server Management Studio. Quando você cria um grupo de disponibilidade com o assistente, ele retornará um erro quando você unir as réplicas no AG. Para corrigir esse problema, conceda `ALTER`, `CONTROL`, e `VIEW DEFINITIONS` para o pacemaker no grupo de disponibilidade em todas as réplicas. Depois que as permissões são concedidas na réplica primária, Junte-se a nós para o grupo de disponibilidade por meio do assistente, mas para alta disponibilidade funcionar corretamente, conceder permissão em todas as réplicas.

Para uma configuração de alta disponibilidade que garante que o failover automático, o grupo de disponibilidade requer pelo menos três réplicas. Qualquer uma das seguintes configurações pode dar suporte a alta disponibilidade:

- [Três réplicas síncronas](sql-server-linux-availability-group-ha.md#threeSynch)

- [Duas réplicas síncronas além de uma réplica de configuração](sql-server-linux-availability-group-ha.md#twoSynch)

Para obter informações, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

>[!NOTE]
>Os grupos de disponibilidade podem incluir mais de réplicas síncronas ou assíncronas. 

Crie o grupo de disponibilidade para alta disponibilidade no Linux. Use o [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) com `CLUSTER_TYPE = EXTERNAL`. 

* Grupo de disponibilidade – `CLUSTER_TYPE = EXTERNAL` Especifica que uma entidade de cluster externo gerencia o grupo de disponibilidade. O pacemaker é um exemplo de uma entidade de cluster externo. Quando o tipo de cluster do grupo de disponibilidade é externo, 

* Conjunto de réplicas primárias e secundárias `FAILOVER_MODE = EXTERNAL`. 
   Especifica que a réplica interage com um Gerenciador de cluster externo, como o Pacemaker. 

Os scripts de Transact-SQL a seguir criam um grupo de disponibilidade para alta disponibilidade chamado `ag1`. O script configura as réplicas do grupo de disponibilidade com `SEEDING_MODE = AUTOMATIC`. Essa configuração faz com que o SQL Server para criar automaticamente o banco de dados em cada servidor secundário. Atualize o script a seguir para o seu ambiente. Substitua os `<node1>`, `<node2>`, ou `<node3>` valores com os nomes das instâncias do SQL Server que hospedam as réplicas. Substitua o `<5022>` com a porta que você definiu para os ponto de extremidade de espelhamento de dados. Para criar o grupo de disponibilidade, execute o seguinte comando Transact-SQL na instância do SQL Server que hospeda a réplica primária.

Execute **apenas uma** dos seguintes scripts: 

- [Criar grupo de disponibilidade com três réplicas síncronas](#threeSynch).
- [Criar grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração](#configOnly)
- [Criar grupo de disponibilidade com duas réplicas síncronas](#readScale).

<a name="threeSynch"></a>

- Criar grupo de disponibilidade com três réplicas síncronas

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
   >Após executar o script anterior para criar um grupo de disponibilidade com três réplicas síncronas, não execute o script a seguir:

- Crie grupo de disponibilidade com duas réplicas síncronas e uma réplica de configuração:

   >[!IMPORTANT]
   >Essa arquitetura permite que qualquer edição do SQL Server para hospedar a réplica de terceiro. Por exemplo, a terceira réplica pode ser hospedada no SQL Server Enterprise Edition. Na Enterprise Edition, o tipo de ponto de extremidade só é válida é `WITNESS`. 

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

- Criar grupo de disponibilidade com duas réplicas síncronas

   Inclua duas réplicas com o modo de disponibilidade síncronos. Por exemplo, o script a seguir cria um grupo de disponibilidade chamado `ag1`. `node1` e `node2` hospedam réplicas no modo síncrono, com a propagação automática e failover automático.

   >[!IMPORTANT]
   >Apenas execute o script a seguir para criar um grupo de disponibilidade com duas réplicas síncronas. Não execute o script a seguir se você executou o script anterior. 

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


Você também pode configurar um grupo de disponibilidade com `CLUSTER_TYPE=EXTERNAL` usando SQL Server Management Studio ou o PowerShell. 

### <a name="join-secondary-replicas-to-the-ag"></a>Unir réplicas secundárias para o grupo de disponibilidade

O usuário de pacemaker requer `ALTER`, `CONTROL`, e `VIEW DEFINITION` permissões no grupo de disponibilidade em todas as réplicas. Para conceder permissões, execute o seguinte script de Transact-SQL depois que o grupo de disponibilidade é criado na réplica primária e cada réplica secundária imediatamente depois de serem adicionados ao grupo de disponibilidade. Antes de executar o script, substitua `<pacemakerLogin>` com o nome da conta de usuário do pacemaker.

```Transact-SQL
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

Script Transact-SQL a seguir une a uma instância do SQL Server para um grupo de disponibilidade denominado `ag1`. Atualize o script para o seu ambiente. Em cada instância do SQL Server que hospeda uma réplica secundária, execute o seguinte Transact-SQL para unir o grupo de disponibilidade.

```Transact-SQL
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>Depois de criar o grupo de disponibilidade, você deve configurar a integração com uma tecnologia de cluster como o Pacemaker para alta disponibilidade. Para uma configuração de escala de leitura usando grupos de disponibilidade, começando com [!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)], não é necessário configurar um cluster.

Se você seguiu as etapas neste documento, você terá um AG que ainda não está clusterizado. A próxima etapa é adicionar o cluster. Esta configuração é válida para cenários de balanceamento de carga-de escala de leitura, ele não foi concluído para alta disponibilidade. Para alta disponibilidade, você precisará adicionar o grupo de disponibilidade como um recurso de cluster. Ver [próximas etapas](#next-steps) para obter instruções. 

## <a name="notes"></a>Observações

>[!IMPORTANT]
>Depois de configurar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, é possível usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão acoplados como intimamente com o sistema operacional enquanto estiverem em um Windows Server Failover Cluster (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração de todos os é feita por meio das ferramentas de gerenciamento de cluster. No Ubuntu ou RHEL usar `pcs`. No SLES usar `crm`. 

>[!IMPORTANT]
>Se o grupo de disponibilidade é um recurso de cluster, há um problema conhecido na versão atual em que o failover forçado com perda de dados para uma réplica assíncrona não funciona. Isso será corrigido na próxima versão. Failover manual ou automático para uma réplica síncrona é bem-sucedida.


## <a name="next-steps"></a>Próximas etapas

[Configurar o Cluster do Red Hat Enterprise Linux para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o Cluster do SUSE Linux Enterprise Server para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o Cluster do Ubuntu para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
