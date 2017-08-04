---
title: Configurar o Cluster Ubuntu para o grupo de disponibilidade do SQL Server | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7aa90eb3fd0a0ea66ea4b4fa09bd17d3e6887d7e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---

# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar o Cluster Ubuntu e recursos do grupo de disponibilidade

Este documento explica como criar um cluster de três nós no Ubuntu e adicionar um grupo de disponibilidade criado anteriormente como um recurso do cluster. Para alta disponibilidade, um grupo de disponibilidade no Linux requer três nós - consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> Neste ponto, a integração do SQL Server com Pacemaker no Linux não é como acoplada como com o WSFC no Windows. De dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração todas as está fora de e o serviço é controlado como uma instância autônoma por Pacemaker. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo em Pacemaker. Sempre em exibições de gerenciamento dinâmico que consultar informações de cluster retornará linhas vazias. Você ainda pode criar um ouvinte para usá-lo para a reconexão depois do failover transparente, mas você terá que registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso IP virtual (como explicado abaixo).

As seções a seguir percorrer as etapas para configurar uma solução de cluster de failover. 

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto níveis: 

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
>Habilitar pacemaker comando será concluído com o erro 'pacemaker inicial padrão não contém nenhum runlevels, anulando'. Isso é inofensivo, configuração de cluster pode continuar. Nós a seguir para cima com fornecedores de cluster para corrigir esse problema.

## <a name="create-the-cluster"></a>Criar o Cluster

1. Remova qualquer configuração de cluster existente de todos os nós. 

   Computadores em execução' sudo instalação apt get' instala pacemaker, corosync e pcs ao mesmo tempo e iniciar a execução de todos os 3 dos serviços.  Iniciar corosync gera um modelo ' / etc/cluster/corosync.conf' arquivo.  Para que as próximas etapas bem-sucedida esse arquivo não deve existir – portanto, a solução alternativa é interromper pacemaker / corosync e excluir ' / etc/cluster/corosync.conf', e, em seguida, as próximas etapas serão concluídas com êxito. 'destruir o cluster de computadores' faz a mesma coisa, e você pode usá-lo como uma etapa de instalação de cluster inicial de tempo.
   
   O comando a seguir remove os arquivos de configuração de cluster existentes e interrompe todos os serviços de cluster. Isso destrói permanentemente o cluster. Executá-lo como uma primeira etapa em um ambiente de pré-produção. Observe que 'cluster pcs destruir' desabilitado o serviço de pacemaker e precisa ser reabilitada. Execute o seguinte comando em todos os nós.
   
   >[!WARNING]
   >O comando destruirá qualquer recurso de cluster existente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Crie o cluster. 

   >[!WARNING]
   >Devido a um problema conhecido que o fornecedor do cluster está investigando, iniciando o cluster ('início de cluster de computadores') falhará com erro abaixo. Isso ocorre porque o arquivo de log configurado no /etc/corosync/corosync.conf é incorreto. Para solucionar esse problema, altere o arquivo de log: /var/log/corosync/corosync.log. Como alternativa, você pode criar o arquivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
O comando a seguir cria um cluster de três nós. Antes de executar o script, substitua os valores entre `**< ... >**`. Execute o seguinte comando no nó primário. 

   ```bash
   sudo pcs cluster auth **<node1>** **<node2>** **<node3>** -u hacluster -p **<password for hacluster>**
   sudo pcs cluster setup --name **<clusterName>** **<node1>** **<node2…>** **<node3>**
   sudo pcs cluster start --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, você precisará usar a opção '-force' ao executar 'pcs cluster setup'. Observe que isso é equivalente à execução de 'pcs cluster destroy' e o serviço pacemaker precisa ser reabilitado usando 'sudo systemctl enable pacemaker'.


## <a name="configure-fencing-stonith"></a>Configurar isolamento (STONITH)

Fornecedores de cluster pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o Gerenciador de recursos de cluster não é possível determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster para um estado conhecido novamente. Isolamento de nível de recurso principalmente garante que não há nenhuma corrupção de dados em caso de uma interrupção ao configurar um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com DRBD (Distributed replicados o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inoperante. Isolamento de nível de nó garante que um nó não seja executado para todos os recursos. Isso é feito redefinindo o nó e a implementação de Pacemaker dele é chamada STONITH (que significa "solucionar o outro nó no cabeçalho"). Pacemaker oferece suporte a uma grande variedade de dispositivos de isolamento, por exemplo, no-break ou gerenciamento de placas de interface para servidores. Para obter mais detalhes, consulte [Pacemaker Clusters do zero](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) e [isolamento e Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Porque o nível de nó cercamento configuração depende muito de seu ambiente, vamos desabilitar a ele para este tutorial (ele pode ser configurado em um momento posterior). Execute o seguinte script no nó primário: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Desabilitar STONITH é apenas para fins de teste. Se você planeja usar Pacemaker em um ambiente de produção, você deve planejar uma implementação STONITH dependendo do seu ambiente e mantê-lo habilitado. Observe que agora há sem agentes de isolamento para ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte à execução de clusters de produção nesses ambientes. Estamos trabalhando em uma solução para essa lacuna que estarão disponível em versões futuras.

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Defina a propriedade cluster Iniciar falha-for-fatal como false

`start-failure-is-fatal`Indica se uma falha ao iniciar um recurso em um nó adicional impede as tentativas de iniciar nesse nó. Quando definido como `false`, o cluster decidirá se deseja tentar iniciar no mesmo nó novamente com base no limite do recurso atual falha contagem e a migração. Portanto, após o failover, Pacemaker tentará iniciar o recurso de grupo de disponibilidade no primeiro primário depois que a instância do SQL está disponível. Pacemaker será rebaixar a réplica secundária e ele será automaticamente reingressar no grupo de disponibilidade. 

Para atualizar o valor da propriedade `false` executar o script a seguir:

```bash
sudo pcs property set start-failure-is-fatal=false
```


>[!WARNING]
>Após um failover automático, quando `start-failure-is-fatal = true` o Gerenciador de recursos de tentar iniciar o recurso. Se falhar na primeira tentativa, você precisa executar manualmente `pcs resource cleanup <resourceName>` para a contagem de falhas do recurso de limpeza e redefinir a configuração.

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instalar o agente de recursos do SQL Server para integração com Pacemaker

Execute os seguintes comandos em todos os nós. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar o recurso de grupo de disponibilidade

Para criar o recurso de grupo de disponibilidade, use `pcs resource create` de comando e defina as propriedades do recurso. Comando abaixo cria um `ocf:mssql:ag` mestre/escravo de recursos para o grupo de disponibilidade com o nome `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Criar o recurso IP virtual

Para criar o recurso de endereço IP virtual, execute o seguinte comando em um nó. Use um endereço IP estático disponível da rede. Antes de executar o script, substitua os valores entre `**< ... >**` com um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=**<10.128.16.240>**
```

Não há nenhum nome de servidor virtual equivalente em Pacemaker. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o endereço IP, registre o endereço do recurso IP e o nome do servidor virtual desejado no DNS. Para configurações de recuperação de desastres, registre o nome do servidor virtual desejada e o endereço IP com os servidores DNS primário e site de recuperação de desastres.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocação

Quase todas as decisões em um cluster de Pacemaker, como escolher em que um recurso deve ser executado, é feito comparando pontuações. Pontuações são calculadas por recurso e o Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode executar nesse nó). É possível manipular as decisões de cluster com restrições. As restrições terão uma pontuação. Se uma restrição tem uma pontuação menor que infinito, é apenas uma recomendação. Uma pontuação de infinito significa é obrigatória. Queremos garantir que primária do grupo de disponibilidade e virtual recurso ip são executados no mesmo host, portanto definiremos uma restrição de colocação com uma pontuação de infinito. Para adicionar a restrição de colocação, execute o seguinte comando em um nó. 

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


