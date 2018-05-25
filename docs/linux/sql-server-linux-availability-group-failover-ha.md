---
title: Gerenciar o failover do grupo de disponibilidade - SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/01/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 26868cfd136f3d06366a47ec7d52fa17e3c8fe39
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="always-on-availability-group-failover-on-linux"></a>Failover do grupo de disponibilidade AlwaysOn no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dentro do contexto de um grupo de disponibilidade (AG), as funções primária e secundária das réplicas de disponibilidade normalmente, são intercambiáveis em um processo conhecido como failover. Existem três formas de failover: failover automático (sem perda de dados), failover manual planejado (sem perda de dados) e failover manual forçado (com possível perda de dados), geralmente chamado de *failover forçado*. Automático e planejados failovers manuais preservar todos os seus dados. Um grupo de disponibilidade faz failover no nível de réplica de disponibilidade. Ou seja, um grupo de disponibilidade realiza failover em uma de suas réplicas secundárias (o destino de failover atual). 

Para obter informações sobre o failover, consulte [modos de Failover e o failover](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Failover manual

Use as ferramentas de gerenciamento de cluster para failover de um grupo de disponibilidade gerenciado por um Gerenciador de cluster externo. Por exemplo, se uma solução usa Pacemaker para gerenciar um cluster do Linux, use `pcs` executar failovers manuais em RHEL ou Ubuntu. No SLES use `crm`. 

> [!IMPORTANT]
> Em operações normais, não realizarão failover com ferramentas de gerenciamento de Transact-SQL ou SQL Server como o SSMS ou o PowerShell. Quando `CLUSTER_TYPE = EXTERNAL`, o único valor aceitável para `FAILOVER_MODE` é `EXTERNAL`. Com essas configurações, todas as ações de failover manual ou automática são executadas pelo Gerenciador de cluster externo. Para obter instruções para forçar o failover com potencial perda de dados, consulte [forçar o failover](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Etapas de failover manual

Para executar o failover, a réplica secundária que se tornará a réplica primária deve ser síncrona. Se uma réplica secundária é assíncrona, [alterar o modo de disponibilidade](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Executar failover manualmente em duas etapas.

   Primeiro,[ manualmente apresentarem failover movendo os recursos do AG](#manualMove) do nó do cluster que possui os recursos para um novo nó.

   O cluster de failover do recurso de grupo de disponibilidade e adiciona uma restrição de local. Essa restrição configura o recurso para ser executado no novo nó. Remova esta restrição para failover com êxito no futuro.

   Segundo, [remover a restrição de local](#removeLocConstraint).

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">Etapa 1. Realizar o failover manual failover movendo os recursos do grupo de disponibilidade

Para realizar o failover manual em um recurso do grupo de disponibilidade chamado *ag_cluster* ao nó de cluster chamado *nodeName2*, execute o comando apropriado para a sua distribuição:

- **Exemplo RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Exemplo SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>Depois que você failover manual de um recurso, você precisa remover a restrição de local é adicionada automaticamente.

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> Etapa 2. Remover a restrição de local

Durante um failover manual, o `pcs` comando `move` ou `crm` comando `migrate` adiciona uma restrição de local para o recurso a ser colocado no novo nó de destino. Para ver a nova restrição, execute o comando a seguir depois de mover manualmente o recurso:

- **Exemplo RHEL/Ubuntu**

   ```bash
   sudo pcs constraint --full
   ```

- **Exemplo SLES**

   ```bash
   crm config show
   ```

Remova a restrição de local para que futuras failovers (incluindo o failover automático) tenha êxito. 

Para remover a restrição, execute o seguinte comando: 

- **Exemplo RHEL/Ubuntu**

   Neste exemplo `ag_cluster-master` é o nome do recurso que falhou. 

   ```bash
   sudo pcs resource clear ag_cluster-master 
   ```

- **Exemplo SLES**

   Neste exemplo `ag_cluster` é o nome do recurso que falhou. 

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
 
## <a name="forceFailover"></a> Forçar o failover 

Um failover forçado é destinado estritamente a recuperação de desastres. Nesse caso, você não pode fazer failover com ferramentas de gerenciamento de cluster porque o datacenter primário está inativo. Se você forçar o failover em uma réplica secundária não sincronizada, talvez ocorra alguma perda de dados. Força o failover somente se você precisa restaurar serviço para o grupo de disponibilidade imediatamente e estiver disposto a arriscar a perda de dados.

Se você não pode usar as ferramentas de gerenciamento de cluster para interagir com o cluster - por exemplo, se o cluster não está respondendo devido a um evento de desastre no data center principal, você terá que forçar o failover para ignorar o Gerenciador de cluster externo. Esse procedimento não é recomendado para operações regulares porque ele corre o risco de perda de dados. Use esta opção quando as ferramentas de gerenciamento de cluster falharem ao executar a ação de failover. Funcionalmente, esse procedimento é semelhante ao [executando um failover manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) em um grupo de disponibilidade no Windows.
 
Esse processo para forçar o failover é específico ao SQL Server no Linux.

1. Verifique se que o recurso de grupo de disponibilidade não é gerenciado pelo cluster mais. 

      - Defina o recurso para o modo não gerenciado no nó de cluster de destino. Este comando indica que o agente de recursos para gerenciamento e monitoramento de recursos de parada. Por exemplo: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - Se a tentativa de definir o modo de recurso para o modo de não gerenciado falhar, exclua o recurso. Por exemplo:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >Quando você exclui um recurso, ele também exclui todas as restrições associadas. 

1. Na instância do SQL Server que hospeda a réplica secundária, defina a variável de contexto de sessão `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. O failover do grupo de disponibilidade com o Transact-SQL. No exemplo a seguir, substitua `<MyAg>` com o nome do seu grupo de disponibilidade. Conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute o seguinte comando:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  Após um failover forçado, coloque o grupo de disponibilidade para um estado íntegro antes de reiniciar o gerenciamento e monitoramento de recursos de cluster ou recriando o recurso de grupo de disponibilidade. Examine o [tarefas essenciais após um Failover forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp).

1.  Reiniciar o monitoramento de recursos do cluster e gerenciamento:

   Para reiniciar o monitoramento de recursos de cluster e gerenciamento, execute o seguinte comando:

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   Se você excluir o recurso de cluster, recriá-lo. Para recriar o recurso de cluster, siga as instruções em [criar o recurso de grupo de disponibilidade](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).

>[!Important]
>Não use as etapas anteriores para recuperação de desastre porque eles corre o risco de perda de dados. Em vez disso, altere a réplica assíncrona síncrona e as instruções para [normal failover manual](#manualFailover).

## <a name="database-level-monitoring-and-failover-trigger"></a>Gatilho de monitoramento e failover de nível de banco de dados

Para `CLUSTER_TYPE=EXTERNAL`, a semântica de disparador de failover é diferente em comparação com o WSFC. Quando o grupo de disponibilidade está em uma instância do SQL Server em um WSFC, fazendo a transição de `ONLINE` de estado para o banco de dados faz com que a integridade do AG relatar uma falha. Em resposta, o Gerenciador de cluster dispara uma ação de failover. No Linux, a instância do SQL Server não pode se comunicar com o cluster. Monitoramento de integridade do banco de dados é feita *fora de*. Se o usuário aceito para monitoramento de failover em nível de banco de dados e failover (definindo a opção `DB_FAILOVER=ON` ao criar o grupo de disponibilidade), o cluster irá verificar se o estado do banco de dados é `ONLINE` sempre que ele executa uma ação de monitoramento. O cluster consulta o estado em `sys.databases`. Para qualquer estado diferente de `ONLINE`, ele irá disparar um failover automaticamente (se as condições de failover automático são atendidas). O tempo real do failover depende da frequência da ação de monitoramento, bem como o estado do banco de dados que está sendo atualizado em sys. Databases.

O failover automático exige pelo menos uma réplica de síncrona.

## <a name="next-steps"></a>Próximas etapas

[Configurar o Cluster do Red Hat Enterprise Linux para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o Cluster do SUSE Linux Enterprise Server para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o Cluster Ubuntu para recursos de Cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
