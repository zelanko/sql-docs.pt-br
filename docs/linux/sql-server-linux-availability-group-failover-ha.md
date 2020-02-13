---
title: Gerenciar o failover do grupo de disponibilidade – SQL Server em Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: e887c718c76563a7fcd8388c46a3e9e684faf6d5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70304847"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Failover do grupo de disponibilidade Always On no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Dentro do contexto de um AG (grupo de disponibilidade), as funções primária e secundária das réplicas de disponibilidade, normalmente, são intercambiáveis em um processo conhecido como failover. Existem três formas de failover: failover automático (sem perda de dados), failover manual planejado (sem perda de dados) e failover manual forçado (com possível perda de dados), geralmente chamado de *failover forçado*. Os failovers automáticos e manuais planejados preservam todos os seus dados. Um AG faz failover no nível da réplica de disponibilidade. Ou seja, um AG faz failover em uma de suas réplicas secundárias (o destino de failover atual). 

Para obter informações em segundo plano sobre failover, confira [Failover e modos de failover](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Failover manual

Use as ferramentas de gerenciamento de clusters para fazer failover de um AG gerenciado por um gerenciador de clusters externo. Por exemplo, se uma solução usar o Pacemaker para gerenciar um cluster do Linux, use `pcs` para executar failovers manuais no RHEL ou no Ubuntu. No SLES, use `crm`. 

> [!IMPORTANT]
> Em operações normais, não faça failover com as ferramentas de gerenciamento do Transact-SQL ou do SQL Server como o SSMS ou o PowerShell. Quando `CLUSTER_TYPE = EXTERNAL`, o único valor aceitável para `FAILOVER_MODE` é `EXTERNAL`. Com essas configurações, todas as ações de failover manual ou automático são executadas pelo gerenciador de clusters externo. Para obter instruções para forçar o failover com possível perda de dados, confira [Forçar o failover](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Etapas do failover manual

Para fazer failover, a réplica secundária que se tornará a réplica primária deve ser síncrona. Se uma réplica secundária for assíncrona, [altere o modo de disponibilidade](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Faça failover manualmente em duas etapas.

   Primeiro, [fazer failover manualmente movendo o recurso de AG](#manualMove) do nó de cluster que tem os recursos para um novo nó.

   O cluster faz failover do recurso do AG e adiciona uma restrição de localização. Essa restrição configura o recurso para ser executado no novo nó. Remova essa restrição para fazer failover com sucesso no futuro.

   Segundo, [remover a restrição de localização](#removeLocConstraint).

#### <a name="manualMove"></a> Etapa 1. Fazer failover manualmente movendo o recurso do grupo de disponibilidade

Para fazer failover manual de um recurso do AG denominado *ag_cluster* para o nó de cluster denominado *nodeName2*, execute o comando apropriado para a sua distribuição:

- **Exemplo do RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Exemplo do SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>Depois que você fizer failover manualmente de um recurso, você precisará remover a restrição de localização adicionada automaticamente.

#### <a name="removeLocConstraint"> </a> Etapa 2. Remover a restrição de local

Durante um failover manual, o comando `move` do `pcs` ou o comando `migrate` do `crm` adiciona uma restrição de localização ao recurso a ser colocado no novo nó de destino. Para ver a nova restrição, execute o comando a seguir depois de mover manualmente o recurso:

- **Exemplo do RHEL/Ubuntu**

   ```bash
   sudo pcs constraint list --full
   ```

- **Exemplo do SLES**

   ```bash
   crm config show
   ```

Um exemplo da restrição criada devido a um failover manual. 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **Exemplo do RHEL/Ubuntu**

   No comando a seguir, `cli-prefer-ag_cluster-master` é a ID da restrição que precisa ser removida. `sudo pcs constraint list --full` retorna essa ID. 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **Exemplo do SLES**

   No comando a seguir, `cli-prefer-ms-ag_cluster` é a ID da restrição. `crm config show` retorna essa ID. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>O failover automático não adiciona uma restrição de local, portanto, nenhuma limpeza é necessária. 

Para mais informações:
- [Red Hat – gerenciamento de recursos de cluster](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html)
- [Pacemaker – mover recursos manualmente](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_manually_moving_resources_around_the_cluster.html)
 [Guia de administração do SLES – recursos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> Forçar o failover 

Um failover forçado destina-se estritamente à recuperação de desastre. Nesse caso, não é possível fazer failover com as ferramentas de gerenciamento de cluster porque o datacenter primário está inativo. Se você forçar o failover em uma réplica secundária não sincronizada, talvez ocorra alguma perda de dados. Só force o failover se for preciso restaurar imediatamente o serviço para o AG e se estiver disposto a correr o risco de perder dados.

Se você não puder usar as ferramentas de gerenciamento de cluster para interagir com o cluster – por exemplo, se o cluster não estiver respondendo devido a um evento de desastre no data center primário – talvez seja necessário forçar o failover para ignorar o gerenciador de clusters externo. Esse procedimento não é recomendado para operações regulares porque oferece o risco de perda de dados. Use-o quando as ferramentas de gerenciamento de cluster falharem ao executar a ação de failover. Funcionalmente, esse procedimento é semelhante a [executar um failover manual forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) em um AG em Windows.
 
Esse processo para forçar o failover é específico para o SQL Server em Linux.

1. Verifique se o recurso do AG não é mais gerenciado pelo cluster. 

      - Configure o recurso para o modo não gerenciado no nó de cluster de destino. Esse comando sinaliza ao agente de recurso para interromper o monitoramento e o gerenciamento de recursos. Por exemplo: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - Se a tentativa de configurar o modo de recurso como modo não gerenciado falhar, exclua o recurso. Por exemplo:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >Quando você exclui um recurso, ele também exclui todas as restrições associadas. 

1. Na instância do SQL Server que hospeda a réplica secundária, defina a variável de contexto `external_cluster` da sessão.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Faça failover do AG com o Transact-SQL. No exemplo a seguir, substitua `<MyAg>` pelo nome do seu AG. Conecte-se à instância do SQL Server que hospeda a réplica secundária de destino e execute o comando a seguir:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  Após um failover forçado, traga o AG para um estado íntegro antes de reiniciar o monitoramento e o gerenciamento dos recursos de cluster ou de recriar o recurso do AG. Examine as [Tarefas essenciais após um failover forçado](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp).

1.  Reinicie o monitoramento e o gerenciamento de recursos de cluster:

   Para reiniciar o monitoramento e o gerenciamento de recursos de cluster, execute o comando a seguir:

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   Caso tenha excluído o recurso de cluster, recrie-o. Para recriar o recurso de cluster, siga as instruções em [Criar recurso do grupo de disponibilidade](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).

>[!Important]
>Não use as etapas anteriores para tarefas de recuperação de desastre porque elas oferecem o risco de perda de dados. Em vez disso, altere a réplica assíncrona para síncrona e as instruções para [failover manual normal](#manualFailover).

## <a name="database-level-monitoring-and-failover-trigger"></a>Monitoramento em nível de banco de dados e gatilho de failover

Para `CLUSTER_TYPE=EXTERNAL`, as semânticas do gatilho de failover são diferentes em comparação com o WSFC. Quando o AG está em uma instância do SQL Server em um WSFC, a transição para fora do estado `ONLINE` do banco de dados faz com que a integridade do AG relate uma falha. Em resposta a isso, o gerenciador de clusters dispara uma ação de failover. Em Linux, a instância do SQL Server não pode se comunicar com o cluster. O monitoramento da integridade do banco de dados é feito *de fora para dentro*. Se o usuário optou por failover e monitoramento de failover em nível de banco de dados (configurando a opção `DB_FAILOVER=ON` ao criar o AG), o cluster verificará se o estado do banco de dados é `ONLINE` sempre que executar uma ação de monitoramento. O cluster consulta o estado em `sys.databases`. Para qualquer estado diferente de `ONLINE`, ele disparará um failover automaticamente (se as condições de failover automático forem atendidas). O tempo real do failover depende da frequência da ação de monitoramento, bem como do estado do banco de dados que está sendo atualizado em sys.databases.

O failover automático requer pelo menos uma réplica síncrona.

## <a name="next-steps"></a>Próximas etapas

[Configurar o cluster do Red Hat Enterprise Linux para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurar o cluster do SUSE Linux Enterprise Server para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurar o cluster do Ubuntu para recursos de cluster do grupo de disponibilidade do SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
