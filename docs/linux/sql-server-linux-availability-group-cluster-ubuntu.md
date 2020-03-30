---
title: Configurar um cluster do Ubuntu para um grupo de disponibilidade
titleSuffix: SQL Server on Linux
description: Saiba como criar um cluster de três nós no Ubuntu e adicionar um recurso de grupo de disponibilidade criado anteriormente ao cluster.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 8dd55f8cb9546c7ec91632d40d2eb6b46ffd4d90
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558481"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar o cluster do Ubuntu e o recurso do grupo de disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica como criar um cluster de três nós no Ubuntu e adicionar um grupo de disponibilidade criado anteriormente como um recurso no cluster. Para alta disponibilidade, um grupo de disponibilidade em Linux exige três nós – consulte [Alta disponibilidade e proteção de dados para configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> Neste ponto, a integração do SQL Server com o Pacemaker em Linux não está tão acoplada quanto a do WSFC em Windows. De dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, toda a orquestração ocorre de fora para dentro e o serviço é controlado como uma instância autônoma pelo Pacemaker. Além disso, o nome da rede virtual é específico do WSFC; não há equivalente ao mesmo no Pacemaker. As exibições de gerenciamento dinâmico Always On que consultam as informações do cluster retornam linhas vazias. Você ainda poderá criar um ouvinte para usá-lo para reconexão transparente após o failover, mas será necessário registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso de IP virtual (conforme explicado nas seções a seguir).

As seções a seguir descrevem as etapas necessárias para configurar uma solução de cluster de failover. 

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server nos nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar um gerenciador de recursos de cluster, como o Pacemaker. Estas instruções são descritas neste documento.
   
   A maneira de configurar um gerenciador de recursos de cluster depende da distribuição específica do Linux. 

   >[!IMPORTANT]
   >Os ambientes de produção exigem um agente de isolamento, como o STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações se destinam apenas a teste e validação. 
   >
   >Um cluster do Linux usa o isolamento para retornar o cluster a um estado conhecido. A maneira de configurar o isolamento depende da distribuição e do ambiente. No momento, o isolamento não está disponível em alguns ambientes de nuvem. Confira [Políticas de suporte para clusters de alta disponibilidade do RHEL – plataformas de virtualização](https://access.redhat.com/articles/29440) para obter mais informações.
   >
   >O isolamento normalmente é implementado no sistema operacional e depende do ambiente. Encontre instruções sobre isolamento na documentação do distribuidor do sistema operacional.

5.  [Adicione o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. Em todos os nós, abra as portas do firewall. Abra a porta para o serviço de alta disponibilidade do Pacemaker, a instância do SQL Server e o ponto de extremidade do grupo de disponibilidade. A porta TCP padrão para o servidor que executa o SQL Server é a 1433.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   Como alternativa, você pode simplesmente desabilitar o firewall:
        
   ```bash
   sudo ufw disable
   ```

1. Instale os pacotes do Pacemaker. Em todos os nós, execute os comandos a seguir:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em todos os nós. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Habilite e inicie o serviço pcsd e o Pacemaker

O comando a seguir habilita e inicia o serviço pcsd e o pacemaker. Execute em todos os nós. Isso permite que os nós reingressem no cluster após a reinicialização. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>O comando para habilitar o pacemaker pode ser concluído com o erro 'pacemaker Default-Start contains no runlevels, aborting'. Isso é inofensivo, a configuração do cluster pode continuar. 

## <a name="create-the-cluster"></a>Crie o cluster

1. Remova todas as configurações de cluster existentes de todos os nós. 

   A execução do comando 'sudo apt-get install pcs' instala o pacemaker, o corosync e o pcs ao mesmo tempo e começa a executar os 3 serviços.  A inicialização do corosync gera um arquivo de modelo '/etc/cluster/corosync.conf'.  Para que as próximas etapas tenham sucesso, esse arquivo não deve existir; portanto, a solução alternativa é interromper o pacemaker/corosync e excluir '/etc/cluster/corosync.conf'. Com isso, as próximas etapas serão concluídas com sucesso. O comando 'pcs cluster destroy' faz a mesma coisa e pode ser usado como uma etapa de configuração de cluster inicial de execução única.
   
   O comando a seguir remove todos os arquivos de configuração de cluster existentes e interrompe todos os serviços de cluster. Isso destrói permanentemente o cluster. Execute-o como uma primeira etapa em um ambiente prévio ao de produção. Observe que o comando 'pcs cluster destroy' desabilitou o serviço pacemaker e precisa ser reabilitado. Execute o seguinte comando em todos os nós.
   
   >[!WARNING]
   >O comando destrói todos os recursos de cluster existentes.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Crie o cluster. 

   >[!WARNING]
   >Devido a um problema conhecido que o fornecedor de clustering está investigando, a inicialização do cluster ('pcs cluster start') falha com o erro a seguir. Isso ocorre porque o arquivo de log configurado em /etc/corosync/corosync.conf, criado quando o comando de configuração do cluster é executado, está errado. Para contornar esse problema, altere o arquivo de log para: /var/log/corosync/corosync.log. Como alternativa, você pode criar o arquivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
O comando a seguir cria um cluster de três nós. Antes de executar o script, substitua os valores entre `< ... >`. Execute o comando a seguir no nó primário. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2...> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, você precisará usar a opção '-force' ao executar 'pcs cluster setup'. Observe que isso é equivalente à execução de 'pcs cluster destroy' e o serviço pacemaker precisa ser reabilitado usando 'sudo systemctl enable pacemaker'.


## <a name="configure-fencing-stonith"></a>Configurar isolamento (STONITH)

Os fornecedores do cluster do Pacemaker exigem que o STONITH esteja habilitado e que um dispositivo de isolamento esteja definido para uma configuração de cluster com suporte. Quando o gerenciador de recursos de cluster não pode determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster em um estado conhecido novamente. O isolamento no nível do recurso garante principalmente que não haja dados corrompidos em caso de interrupção pela configuração de um recurso. Você pode usar o isolamento no nível do recurso, por exemplo, com o DRBD (Dispositivo de Bloco Replicado Distribuído) para marcar o disco em um nó como desatualizado quando o link de comunicação ficar inativo. O isolamento no nível do nó verifica se um nó não executa nenhum recurso. Isso é feito pela redefinição do nó e pela implementação do Pacemaker do que é chamado STONITH (que significa "acertar a cabeça do outro nó"). O pacemaker é compatível com uma grande variedade de dispositivos de isolamento, como no-break ou cartões de interface de gerenciamento para servidores. Para obter mais informações, confira [Clusters do Pacemaker do zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/) e [Isolamento e STONITH](https://clusterlabs.org/doc/crm_fencing.html) 

Como a configuração de isolamento no nível do nó depende muito do seu ambiente, nós a desabilitamos para este tutorial (ela pode ser configurada posteriormente). Execute o script a seguir no nó primário: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>A desabilitação do STONITH destina-se apenas a fins de teste. Se você pretende usar o Pacemaker em um ambiente de produção, deve planejar uma implementação do STONITH dependendo do ambiente e mantê-lo habilitado. Contate o fornecedor do sistema operacional para obter informações sobre os agentes de isolamento em qualquer distribuição específica. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Defina a propriedade de cluster cluster-recheck-interval

`cluster-recheck-interval` indica o intervalo de sondagem segundo o qual o cluster verifica se há alterações nos parâmetros de recurso, restrições ou outras opções de cluster. Se uma réplica ficar inativa, o cluster tentará reiniciar a réplica em um intervalo associado ao valor `failure-timeout` e ao valor `cluster-recheck-interval`. Por exemplo, se `failure-timeout` for definido como 60 segundos e `cluster-recheck-interval` for definido como 120 segundos, será realizada uma tentativa de reinicialização em um intervalo superior a 60 segundos, mas inferior a 120 segundos. Recomendamos que você defina failure-timeout como 60 segundos e cluster-recheck-interval com um valor superior a 60 segundos. Não é recomendável definir cluster-recheck-interval como um valor pequeno.

Para atualizar o valor da propriedade para `2 minutes`, execute:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se você já tiver um recurso de grupo de disponibilidade gerenciado por um cluster do Pacemaker, observe que todas as distribuições que usam o pacote mais recente disponível do Pacemaker 1.1.18-11.el7 introduzem uma alteração de comportamento para a configuração de cluster start-failure-is-fatal quando seu valor é falso. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária apresentar uma interrupção, o cluster deverá fazer failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários observarão que o cluster continua tentando iniciar a réplica primária com falha. Se a primária nunca ficar online (devido a uma interrupção permanente), o cluster nunca fará failover para outra réplica secundária disponível. Devido a essa alteração, a configuração recomendada anteriormente para definir start-failure-is-fatal não é mais válida e a configuração precisa ser revertida de volta para seu valor padrão `true`. Além disso, o recurso do AG precisa ser atualizado para incluir a propriedade `failover-timeout`. 
>
>Para atualizar o valor da propriedade para `true`, execute:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Atualize a propriedade do recurso do AG existente `failure-timeout` para a execução de `60s` (substitua `ag1` pelo nome do recurso de grupo de disponibilidade):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instale o agente de recursos do SQL Server para integração com o Pacemaker

Execute os seguintes comandos em todos os nós. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Criar um logon do SQL Server para o Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar recurso do grupo de disponibilidade

Para criar o recurso do grupo de disponibilidade, use o comando `pcs resource create` e defina as propriedades do recurso. O comando abaixo cria um recurso do tipo mestre/subordinado `ocf:mssql:ag` para o grupo de disponibilidade com o nome `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Criar recurso de IP virtual

Para criar o recurso de endereço IP virtual, execute o comando a seguir em um nó. Use um endereço IP estático disponível da rede. Antes de executar o script, substitua os valores entre `< ... >` por um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Não há nome do servidor virtual equivalente no Pacemaker. Para usar uma cadeia de conexão que aponte para um nome de servidor de cadeia de caracteres e não usar o endereço IP, registre o endereço de recurso do IP e o nome do servidor virtual desejado no DNS. Para configurações de DR, registre o nome do servidor virtual e o endereço IP desejados com os servidores DNS nos sites primário e de DR.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocalização

Quase todas as decisões em um cluster do Pacemaker, como escolher o local em que um recurso deve ser executado, são feitas pela comparação de pontuações. As pontuações são calculadas por recurso e o gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um recurso específico. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não poderá ser executado nesse nó.) Use restrições para configurar as decisões do cluster. As restrições têm uma pontuação. Se uma restrição tiver uma pontuação menor que INFINITY, ela será apenas uma recomendação. Uma pontuação igual a INFINITY significa que ela é obrigatória. Para garantir que a réplica primária e o recurso de IP virtual estejam no mesmo host, defina uma restrição de colocalização com pontuação igual a INFINITY. Para adicionar a restrição de colocalização, execute o comando a seguir em um nó. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação

A restrição de colocalização tem uma restrição de ordenação implícita. Ela move o recurso de IP virtual antes de mover o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é:

1. O usuário emite `pcs resource move` ao grupo de disponibilidade primário do node1 para o node2.
1. O recurso de IP virtual é interrompido no nó 1.
1. O recurso de IP virtual é iniciado no nó 2.

   >[!NOTE]
   >Neste ponto, o endereço IP aponta temporariamente para o nó 2, enquanto o nó 2 ainda é um secundário de pré-failover. 
   
1. O grupo de disponibilidade primário no nó 1 é rebaixado para secundário.
1. O grupo de disponibilidade secundário no nó 2 é promovido para primário. 

Para impedir que o endereço IP aponte temporariamente para o nó com o secundário de pré-failover, adicione uma restrição de ordenação. 

Para adicionar uma restrição de ordenação, execute o comando a seguir em um nó:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Depois de configurar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, você não poderá usar o Transact-SQL para fazer failover dos recursos de grupo de disponibilidade. Os recursos de cluster do SQL Server em Linux não são acoplados tão firmemente com o sistema operacional como são em um WSFC (cluster de failover do Windows Server). O serviço SQL Server não reconhece a presença do cluster. Toda a orquestração é feita por meio das ferramentas de gerenciamento de cluster. No RHEL ou no Ubuntu, use `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar grupo de disponibilidade de HA](sql-server-linux-availability-group-failover-ha.md)

