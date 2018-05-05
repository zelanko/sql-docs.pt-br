---
title: Configurar o Cluster Ubuntu para o grupo de disponibilidade do SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 37008fbf209bbdc8a610e5a21bbd599e9783c423
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar o Cluster Ubuntu e recursos do grupo de disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica como criar um cluster de três nós no Ubuntu e adicionar um grupo de disponibilidade criado anteriormente como um recurso do cluster. Para alta disponibilidade, um grupo de disponibilidade no Linux requer três nós - consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> Neste ponto, a integração do SQL Server com Pacemaker no Linux não é como acoplada como com o WSFC no Windows. De dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração todas as está fora na, e o serviço é controlado como uma instância autônoma por Pacemaker. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo em Pacemaker. Sempre em exibições de gerenciamento dinâmico que consultar informações de cluster retornam linhas vazias. Você ainda pode criar um ouvinte para usá-lo para a reconexão depois do failover transparente, mas você precisa registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir).

As seções a seguir percorrer as etapas para configurar uma solução de cluster de failover. 

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server em nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md). 

3. Configure um Gerenciador de recursos de cluster, como Pacemaker. Essas instruções são neste documento.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende da distribuição específica do Linux. 

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento, como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster do Linux usa isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende a distribuição e o ambiente. Neste momento, o isolamento não está disponível em alguns ambientes de nuvem. Consulte [políticas de suporte para Clusters de disponibilidade alta RHEL - plataformas de virtualização](https://access.redhat.com/articles/29440) para obter mais informações.

5.  [Adicione o grupo de disponibilidade como um recurso do cluster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar Pacemaker em cada nó de cluster

1. Em todos os nós, abra as portas do firewall. Abra a porta para o serviço de alta disponibilidade Pacemaker, a instância do SQL Server e o ponto de extremidade do grupo de disponibilidade. Porta TCP padrão para o servidor que executa o SQL Server é 1433.  

   ```bash
   sudo ufw allow 2224/tcp
   sudo ufw allow 3121/tcp
   sudo ufw allow 21064/tcp
   sudo ufw allow 5405/udp
        
   sudo ufw allow 1433/tcp # Replace with TDS endpoint
   sudo ufw allow 5022/tcp # Replace with DATA_MIRRORING endpoint
        
   sudo ufw reload
   ```
   
   Como alternativa, você pode desabilitar apenas o firewall:
        
   ```bash
   sudo ufw disable
   ```

1. Instale pacotes de Pacemaker. Em todos os nós, execute os seguintes comandos:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em todos os nós. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Habilitar e iniciar o serviço de pcsd e Pacemaker

O comando a seguir habilita e pacemaker e pcsd serviço é iniciado. Execute em todos os nós. Isso permite que os nós para reingressar no cluster após a reinicialização. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Habilitar pacemaker comando pode ser concluído com o erro 'pacemaker inicial padrão não contém nenhum runlevels, anulando'. Isso é inofensivo, configuração de cluster pode continuar. 

## <a name="create-the-cluster"></a>Criar o Cluster

1. Remova qualquer configuração de cluster existente de todos os nós. 

   Computadores em execução' sudo instalação apt get' instala pacemaker, corosync e pcs ao mesmo tempo e iniciar a execução de todos os 3 dos serviços.  Iniciar corosync gera um modelo ' / etc/cluster/corosync.conf' arquivo.  Para que as próximas etapas bem-sucedida esse arquivo não deve existir – portanto, a solução alternativa é interromper pacemaker / corosync e excluir ' / etc/cluster/corosync.conf', e, em seguida, próximas etapas concluída com êxito. 'destruir o cluster de computadores' faz a mesma coisa, e você pode usá-lo como uma etapa de instalação de cluster inicial de tempo.
   
   O comando a seguir remove os arquivos de configuração de cluster existentes e interrompe todos os serviços de cluster. Isso destrói permanentemente o cluster. Executá-lo como uma primeira etapa em um ambiente de pré-produção. Observe que 'cluster pcs destruir' desabilitado o serviço de pacemaker e precisa ser reabilitada. Execute o seguinte comando em todos os nós.
   
   >[!WARNING]
   >O comando destrói qualquer recurso de cluster existente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Crie o cluster. 

   >[!WARNING]
   >Devido a um problema conhecido que o fornecedor do cluster está investigando, iniciando o cluster ('início de cluster de computadores') falha com o seguinte erro. Isso ocorre porque o arquivo de log configurado no /etc/corosync/corosync.conf que é criado quando o comando de instalação de cluster é executado, é incorreto. Para contornar esse problema, altere o arquivo de log: /var/log/corosync/corosync.log. Como alternativa, você pode criar o arquivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
O comando a seguir cria um cluster de três nós. Antes de executar o script, substitua os valores entre `< ... >`. Execute o seguinte comando no nó primário. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2…> <node3>
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, você precisará usar a opção '-force' ao executar 'pcs cluster setup'. Observe que isso é equivalente à execução de 'pcs cluster destroy' e o serviço pacemaker precisa ser reabilitado usando 'sudo systemctl enable pacemaker'.


## <a name="configure-fencing-stonith"></a>Configurar isolamento (STONITH)

Fornecedores de cluster pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o Gerenciador de recursos de cluster não é possível determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster para um estado conhecido novamente. Isolamento de nível de recurso principalmente garante que não há nenhuma corrupção de dados em caso de uma interrupção ao configurar um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com DRBD (Distributed replicados o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inoperante. Isolamento de nível de nó garante que um nó não seja executado para todos os recursos. Isso é feito redefinindo o nó e a implementação de Pacemaker dele é chamada STONITH (que significa "solucionar o outro nó no cabeçalho"). Pacemaker oferece suporte a uma grande variedade de dispositivos de isolamento, por exemplo, no-break ou gerenciamento de placas de interface para servidores. Para obter mais informações, consulte [Pacemaker Clusters do zero](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) e [isolamento e Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Porque o nível de nó cercamento configuração depende muito de seu ambiente, nós desabilitamos esse tutorial (ele pode ser configurado em um momento posterior). Execute o seguinte script no nó primário: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Desabilitar STONITH é apenas para fins de teste. Se você planeja usar Pacemaker em um ambiente de produção, você deve planejar uma implementação STONITH dependendo do seu ambiente e mantê-lo habilitado. Observe que agora há sem agentes de isolamento para ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte à execução de clusters de produção nesses ambientes. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Definir propriedade de cluster cluster-nova verificação-intervalo

`cluster-recheck-interval` indica o intervalo de sondagem em que o cluster verifica para alterações nos parâmetros de recursos, restrições ou outras opções de cluster. Se uma réplica falhar, o cluster tenta reiniciar a réplica em um intervalo que está vinculado a `failure-timeout` valor e o `cluster-recheck-interval` valor. Por exemplo, se `failure-timeout` é definido como 60 segundos e `cluster-recheck-interval` é definido como 120 segundos, a reinicialização é tentada em um intervalo maior que 60 segundos, mas com menos de 120 segundos. É recomendável que você defina o tempo limite de falha para 60 e cluster--intervalo de nova verificação para um valor maior que 60 segundos. Não é recomendável definir o intervalo da nova verificação de cluster para um valor pequeno.

Para atualizar o valor da propriedade `2 minutes` executar:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se você já tiver um recurso de grupo de disponibilidade gerenciado por um cluster Pacemaker, observe que todas as distribuições que usam o mais recente disponível Pacemaker pacote 1.1.18-11.el7 introduzem uma alteração de comportamento para o cluster Iniciar falha-for-fatal configuração quando seu valor é false. Esta alteração afeta o fluxo de trabalho de failover. Se uma réplica primária passa por uma interrupção, o cluster é esperado para failover em uma das réplicas secundárias disponíveis. Em vez disso, os usuários vai notar que o cluster continua tentando iniciar a réplica primária com falha. Se esse primário nunca ficar online (devido a uma interrupção permanente), o cluster nunca failover para outra réplica secundária disponível. Devido a essa alteração, uma configuração recomendada anteriormente para definir o início falha-for-fatal não é mais válida e a configuração deve ser revertido para seu valor padrão de `true`. Além disso, o recurso de grupo de disponibilidade precisa ser atualizado para incluir o `failover-timeout` propriedade. 
>
>Para atualizar o valor da propriedade `true` executar:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Atualizar a propriedade de recurso existente do AG `failure-timeout` para `60s` executado (substituir `ag1` com o nome do recurso de grupo de disponibilidade):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instalar o agente de recursos do SQL Server para integração com Pacemaker

Execute os seguintes comandos em todos os nós. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar o recurso de grupo de disponibilidade

Para criar o recurso de grupo de disponibilidade, use `pcs resource create` de comando e defina as propriedades do recurso. Comando abaixo cria um `ocf:mssql:ag` primário/secundário de recursos para o grupo de disponibilidade com o nome `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Criar o recurso IP virtual

Para criar o recurso de endereço IP virtual, execute o seguinte comando em um nó. Use um endereço IP estático disponível da rede. Antes de executar o script, substitua os valores entre `< ... >` com um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Não há nenhum nome de servidor virtual equivalente em Pacemaker. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o endereço IP, registre o endereço do recurso IP e o nome do servidor virtual desejado no DNS. Para configurações de recuperação de desastres, registre o nome do servidor virtual desejada e o endereço IP com os servidores DNS primário e site de recuperação de desastres.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocação

Quase todas as decisões em um cluster de Pacemaker, como escolher em que um recurso deve ser executado, é feito comparando pontuações. Pontuações são calculadas por recurso e o Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode executar nesse nó). Use restrições para configurar as decisões do cluster. As restrições terão uma pontuação. Se uma restrição tem uma pontuação menor que infinito, é apenas uma recomendação. Uma pontuação de infinito significa que é obrigatório. Para garantir que a réplica primária e o recurso de ip virtual estão no mesmo host, defina uma restrição de colocação com uma pontuação de infinito. Para adicionar a restrição de colocação, execute o seguinte comando em um nó. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação

A restrição de colocação tem uma restrição de ordenação implícita. Ele move o recurso IP virtual antes de ele move o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é:

1. Problemas de usuários `pcs resource move` ao grupo de disponibilidade primário do Nó1 para o Nó2.
1. Interrompe o recurso IP virtual no node1.
1. O recurso IP virtual é iniciado no node2.

   >[!NOTE]
   >Neste ponto, o endereço IP temporariamente pontos para node2 enquanto node2 ainda é um failover anterior secundário. 
   
1. O grupo de disponibilidade primário no node1 é rebaixado para o secundário.
1. O grupo de disponibilidade secundário no node2 é promovido a primário. 

Para impedir que o endereço IP temporariamente apontando para o nó com o secundário pre-failover, adicione uma restrição de ordenação. 

Para adicionar uma restrição de ordenação, execute o seguinte comando em um nó:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão ligados como intimamente com o sistema operacional como estão em um Cluster de Failover do Windows Server (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração todos é feita por meio das ferramentas de gerenciamento de cluster. Em RHEL ou Ubuntu usar `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar o grupo de disponibilidade de alta disponibilidade](sql-server-linux-availability-group-failover-ha.md)

