---
title: Configurar o Cluster do Ubuntu para o grupo de disponibilidade do SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 04/30/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: dd0d6fb9-df0a-41b9-9f22-9b558b2b2233
ms.openlocfilehash: 299e158968a5af247b5f04fdc66563b3a3ee4e18
ms.sourcegitcommit: 87efa581f7d4d84e9e5c05690ee1cb43bd4532dc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38999266"
---
# <a name="configure-ubuntu-cluster-and-availability-group-resource"></a>Configurar o Cluster do Ubuntu e recursos do grupo de disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica como criar um cluster de três nós no Ubuntu e adicionar um grupo de disponibilidade criado anteriormente como um recurso no cluster. Para alta disponibilidade, um grupo de disponibilidade no Linux exige três nós – veja [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md).

> [!NOTE] 
> Neste ponto, a integração do SQL Server com o Pacemaker no Linux não é tão rígida como com o WSFC no Windows. Do dentro do SQL, não há nenhum conhecimento sobre a presença do cluster, orquestração todos os está fora na e o serviço é controlado como uma instância autônoma por Pacemaker. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo no Pacemaker. Sempre em exibições de gerenciamento dinâmico que consultar informações de cluster retornam linhas vazias. Você ainda pode criar um ouvinte para usá-lo para reconexão transparente após o failover, mas você deve registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir).

As seções a seguir percorrer as etapas para configurar uma solução de cluster de failover. 

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server em nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md). 

3. Configure um Gerenciador de recursos de cluster, como o Pacemaker. Essas instruções são neste documento.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende a distribuição Linux específica. 

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster do Linux usa o isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende da distribuição e o ambiente. Neste momento, o isolamento não está disponível em alguns ambientes de nuvem. Ver [políticas de suporte para Clusters de disponibilidade alta RHEL - plataformas de virtualização](https://access.redhat.com/articles/29440) para obter mais informações.

5.  [Adicione o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource). 

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. Em todos os nós, abra as portas de firewall. Abra a porta para o serviço de alta disponibilidade do Pacemaker, instância do SQL Server e o ponto de extremidade do grupo de disponibilidade. Porta TCP padrão para o servidor que executa o SQL Server é 1433.  

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

1. Instale os pacotes do Pacemaker. Em todos os nós, execute os seguintes comandos:

   ```bash
   sudo apt-get install pacemaker pcs fence-agents resource-agents
   ```

2. Defina a senha do usuário padrão criado ao instalar pacotes do Pacemaker e do Corosync. Use a mesma senha em todos os nós. 

   ```bash
   sudo passwd hacluster
   ```

## <a name="enable-and-start-pcsd-service-and-pacemaker"></a>Habilitar e iniciar o serviço pcsd e o Pacemaker

O comando a seguir habilita e inicia o pacemaker e do serviço pcsd. Execute em todos os nós. Isso permite que os nós reingressem no cluster após a reinicialização. 

```bash
sudo systemctl enable pcsd
sudo systemctl start pcsd
sudo systemctl enable pacemaker
```
>[!NOTE]
>Enable pacemaker comando pode ser concluído com o erro 'pacemaker padrão de início não contém nenhum runlevels, anulando'. Isso é inofensivo, configuração de cluster pode continuar. 

## <a name="create-the-cluster"></a>Criar o Cluster

1. Remova qualquer configuração de cluster existente de todos os nós. 

   Computadores em execução' sudo apt-get install' instala PCs, corosync e pacemaker ao mesmo tempo e inicia a execução de todos os 3 dos serviços.  Iniciar o corosync gera um modelo de ' / etc/cluster/corosync.conf' arquivo.  Ter as próximas etapas bem-sucedida deste arquivo não deve existir – portanto, a solução alternativa é interromper o pacemaker / corosync e excluir ' / etc/cluster/corosync.conf', e, em seguida, as próximas etapas concluída com êxito. 'pcs cluster destroy' faz a mesma coisa, e você pode usá-lo como uma etapa de configuração de cluster inicial de tempo.
   
   O comando a seguir remove os arquivos de configuração de cluster existentes e interrompe todos os serviços de cluster. Isso destrói permanentemente o cluster. Executá-lo como uma primeira etapa em um ambiente de pré-produção. Observe que ' pcs cluster destroy' desabilitado o serviço pacemaker e precisa ser reabilitado. Execute o seguinte comando em todos os nós.
   
   >[!WARNING]
   >O comando destrói quaisquer recursos de cluster existente.

   ```bash
   sudo pcs cluster destroy 
   sudo systemctl enable pacemaker
   ```

1. Crie o cluster. 

   >[!WARNING]
   >Devido a um problema conhecido que o fornecedor do cluster está investigando, começando no cluster ('pcs cluster start') falha com erro a seguir. Isso ocorre porque o arquivo de log configurado no /etc/corosync/corosync.conf que é criado quando o comando de instalação de cluster é executado, é incorreto. Para contornar esse problema, altere o arquivo de log: /var/log/corosync/corosync.log. Como alternativa, você pode criar o arquivo /var/log/cluster/corosync.log.
 
   ```Error
   Job for corosync.service failed because the control process exited with error code. 
   See "systemctl status corosync.service" and "journalctl -xe" for details.
   ```
  
O comando a seguir cria um cluster de três nós. Antes de executar o script, substitua os valores entre `< ... >`. Execute o seguinte comando no nó primário. 

   ```bash
   sudo pcs cluster auth <node1> <node2> <node3> -u hacluster -p <password for hacluster>
   sudo pcs cluster setup --name <clusterName> <node1> <node2…> <node3>
   sudo pcs cluster start --all
   sudo pcs cluster enable --all
   ```
   
   >[!NOTE]
   >Se você tiver configurado um cluster anteriormente nos mesmos nós, você precisará usar a opção '-force' ao executar 'pcs cluster setup'. Observe que isso é equivalente à execução de 'pcs cluster destroy' e o serviço pacemaker precisa ser reabilitado usando 'sudo systemctl enable pacemaker'.


## <a name="configure-fencing-stonith"></a>Configurar o isolamento (STONITH)

Fornecedores de cluster do pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o cluster resource manager não pode determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster em um estado conhecido novamente. Isolamento de nível de recurso principalmente garante que não há nenhum dano de dados em caso de interrupção por meio da configuração de um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com o DRBD (distribuído replicado o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inativo. Isolamento de nível de nó garante que um nó não é executado todos os recursos. Isso é feito redefinindo o nó e a implementação do Pacemaker dele é chamada de STONITH (o que significa "acertar o outro nó no cabeçalho"). Pacemaker dá suporte a uma grande variedade de dispositivos de isolamento, por exemplo, no-break ou gerenciamento de placas de interface para servidores. Para obter mais informações, consulte [Clusters do Pacemaker do zero](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html) e [isolamento e Stonith](http://clusterlabs.org/doc/crm_fencing.html) 

Porque o nível do nó de configuração de isolamento depende muito do seu ambiente, podemos desabilitá-lo para este tutorial (ele pode ser configurado em um momento posterior). Execute o seguinte script no nó primário: 

```bash
sudo pcs property set stonith-enabled=false
```

>[!IMPORTANT]
>Desabilitar o STONITH é apenas para fins de teste. Se você planeja usar o Pacemaker em um ambiente de produção, você deve planejar uma implementação de STONITH dependendo do seu ambiente e mantenha-a habilitada. Observe que agora não há nenhum agente de isolamento para todos os ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte para clusters de produção em execução nesses ambientes. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Definir propriedade de cluster cluster-verificar novamente-intervalo

`cluster-recheck-interval` indica o intervalo de sondagem em que o cluster verifica para alterações nos parâmetros de recursos, restrições ou outras opções de cluster. Se uma réplica ficar inativo, o cluster tenta reiniciar a réplica em um intervalo que é associado pela `failure-timeout` valor e o `cluster-recheck-interval` valor. Por exemplo, se `failure-timeout` é definido como 60 segundos e `cluster-recheck-interval` é definido como 120 segundos, a reinicialização é tentada em um intervalo que é maior que 60 segundos e menos de 120 segundos. É recomendável que você defina o tempo limite de falha como 60 e cluster-verificar novamente intervalo como um valor maior que 60 segundos. Não é recomendável definir o intervalo de nova verificação de cluster para um valor pequeno.

Para atualizar o valor da propriedade `2 minutes` executar:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se você já tiver um recurso de grupo de disponibilidade gerenciado por um cluster Pacemaker, observe que todas as distribuições que usam o mais recente disponível Pacemaker pacote 1.1.18-11.el7 introduzem uma alteração de comportamento para o cluster Iniciar falha-for-fatal configuração quando seu valor é false. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária sofrer uma interrupção, o cluster é esperado para o failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários perceberão que o cluster continua tentando iniciar a réplica primária com falha. Se esse principal nunca ficar online (devido a uma interrupção permanente), o cluster será nunca fará failover para outra réplica secundária disponível. Por causa dessa alteração, uma configuração recomendada anteriormente para definir o início falha-for-fatal não é mais válida e a configuração precisa ser revertido para seu valor padrão de `true`. Além disso, o recurso AG precisa ser atualizado para incluir o `failover-timeout` propriedade. 
>
>Para atualizar o valor da propriedade `true` executar:
>
>```bash
>sudo pcs property set start-failure-is-fatal=true
>```
>
>Atualizar sua propriedade de recurso existente do AG `failure-timeout` à `60s` executado (substituir `ag1` com o nome do recurso de grupo de disponibilidade):
>
>```bash
>pcs resource update ag1 meta failure-timeout=60s
>```

## <a name="install-sql-server-resource-agent-for-integration-with-pacemaker"></a>Instalar o agente de recursos do SQL Server para integração com o Pacemaker

Execute os seguintes comandos em todos os nós. 

```bash
sudo apt-get install mssql-server-ha
```

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar recurso de grupo de disponibilidade

Para criar o recurso de grupo de disponibilidade, use `pcs resource create` de comando e defina as propriedades do recurso. Comando abaixo cria um `ocf:mssql:ag` primário/secundário de recursos para o grupo de disponibilidade com o nome `ag1`. 

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s --master meta notify=true

```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

## <a name="create-virtual-ip-resource"></a>Criar recurso de IP virtual

Para criar o recurso de endereço IP virtual, execute o seguinte comando em um nó. Use um endereço IP estático disponível da rede. Antes de executar o script, substitua os valores entre `< ... >` com um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Não há nenhum nome de servidor virtual equivalente no Pacemaker. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres e não usar o endereço IP, registre o endereço do recurso IP e o nome do servidor virtual desejado no DNS. Para configurações de recuperação de desastres, registre o nome do servidor virtual desejada e o endereço IP com os servidores DNS no primário e site de recuperação de Desastre.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocação

Quase todas as decisões em um cluster Pacemaker, como escolher onde um recurso deve ser executado, é feita comparando as pontuações. As pontuações são calculadas por recurso e o Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode ser executado nesse nó.) Use restrições para configurar as decisões do cluster. Restrições têm uma pontuação. Se uma restrição tiver uma pontuação inferior a infinito, é apenas uma recomendação. Uma pontuação de infinito significa que ele é obrigatório. Para garantir que a réplica primária e o recurso de ip virtual estão no mesmo host, defina uma restrição de colocação, com uma pontuação de infinito. Para adicionar a restrição de colocação, execute o seguinte comando em um nó. 

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação

A restrição de colocação possui uma restrição de ordenação implícita. Ele move o recurso IP virtual antes de mover o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é:

1. Problemas do usuário `pcs resource move` ao grupo de disponibilidade primário do Nó1 para o node2.
1. Interrompe o recurso IP virtual no node1.
1. O recurso IP virtual é iniciado no node2.

   >[!NOTE]
   >Neste ponto, o endereço IP temporariamente pontos para o node2 enquanto node2 ainda é um pré-failover secundário. 
   
1. O grupo de disponibilidade primário no node1 é rebaixado para secundária.
1. O grupo de disponibilidade secundário no node2 é promovido a primária. 

Para impedir que o endereço IP temporariamente apontando para o nó com o secundário antes do failover, adicione uma restrição de ordenação. 

Para adicionar uma restrição de ordenação, execute o seguinte comando em um nó:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão acoplados como intimamente com o sistema operacional enquanto estiverem em um Windows Server Failover Cluster (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração de todos os é feita por meio das ferramentas de gerenciamento de cluster. No Ubuntu ou RHEL usar `pcs`. 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar o grupo de disponibilidade de alta disponibilidade](sql-server-linux-availability-group-failover-ha.md)

