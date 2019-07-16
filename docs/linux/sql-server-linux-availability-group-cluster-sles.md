---
title: Configurar o Cluster SLES para o grupo de disponibilidade do SQL Server
titleSuffix: SQL Server
description: Saiba como criar clusters de grupo de disponibilidade do SQL Server no SUSE Linux Enterprise Server (SLES)
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: 063adf4f1f180138150484e4ac9fc397ef886f5d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003564"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configurar o Cluster SLES para o grupo de disponibilidade do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia fornece instruções para criar um cluster de três nós para o SQL Server no SUSE Linux Enterprise Server (SLES) 12 SP2. Para alta disponibilidade, um grupo de disponibilidade no Linux exige três nós – veja [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). A camada de clustering é baseada no SUSE [alta disponibilidade de extensão (HAE)](https://www.suse.com/products/highavailability) criado na parte superior da [Pacemaker](https://clusterlabs.org/). 

Para obter mais informações sobre a configuração de cluster, opções de recurso do agente, gerenciamento, as práticas recomendadas e recomendações, consulte [SUSE Linux Enterprise alta disponibilidade extensão 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>Neste ponto, a integração do SQL Server com o Pacemaker no Linux não é tão rígida como com o WSFC no Windows. O serviço do SQL Server no Linux não é o reconhecimento de cluster. Pacemaker controla todas a orquestração dos recursos de cluster, incluindo o recurso de grupo de disponibilidade. No Linux, você não deve depender sempre na disponibilidade grupo exibições de gerenciamento dinâmico (DMVs) que fornecem informações de cluster, como DM hadr_cluster. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo no Pacemaker. Você ainda pode criar um ouvinte para usá-lo para reconexão transparente após o failover, mas você terá que registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso IP virtual (conforme explicado nas seções a seguir).


## <a name="roadmap"></a>Roteiro

O procedimento para criar um grupo de disponibilidade para alta disponibilidade é diferente entre servidores Linux e um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server em nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-failover-ha.md). 

3. Configure um Gerenciador de recursos de cluster, como o Pacemaker. Essas instruções são neste documento.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende a distribuição Linux específica. 

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento como STONITH para alta disponibilidade. Os exemplos neste artigo não usam agentes de isolamento. Eles são para teste e validação somente. 
   
   >Um cluster Pacemaker usa o isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende da distribuição e o ambiente. Neste momento, o isolamento não está disponível em alguns ambientes de nuvem. Ver [extensão de alta disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Adicione o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Pré-requisitos

Para concluir o seguinte cenário de ponta a ponta, você precisa de três máquinas para implantar o cluster de três nós. As etapas a seguir descrevem como configurar esses servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster 

A primeira etapa é configurar o sistema operacional em nós de cluster. Para este passo a passo, use o SLES 12 SP2 com uma assinatura válida para o complemento de alta disponibilidade.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Instalar e configurar o serviço do SQL Server em cada nó de cluster

1. Instalar e configurar o serviço do SQL Server em todos os nós. Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).

1. Designe um nó como primários e de outros nós como secundários. Use estes termos em todo este guia.

1. Certifique-se de nós que fazem parte do cluster podem se comunicar entre si.

   A exemplo a seguir mostra `/etc/hosts` com adições para três nós denominados SLES1, SLES2 e SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Todos os nós de cluster devem ser capazes de acessar um ao outro via SSH. Ferramentas como `hb_report` ou `crm_report` (para solução de problemas) e o Gerenciador de histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, eles podem apenas coletar dados do nó atual. No caso de você usar uma porta SSH não padrão, use a opção -X (consulte `man` página). Por exemplo, se a porta SSH é 3479, invoque um `crm_report` com:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Para obter mais informações, consulte o [guia de administração do SLES - seção diversos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurar um grupo de disponibilidade Always On

Em servidores Linux, configure o grupo de disponibilidade e, em seguida, configurar os recursos de cluster. Para configurar o grupo de disponibilidade, consulte [Configurar grupo de disponibilidade AlwaysOn para SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. Instalar a extensão de alta disponibilidade

   Para referência, consulte [instalando o SUSE Linux Enterprise Server e a extensão de alta disponibilidade](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Instale o pacote do agente de recursos do SQL Server em ambos os nós.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurar o primeiro nó

   Consulte [instruções de instalação do SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Faça logon como `root` para a máquina física ou virtual que deseja usar como nó de cluster.
2. Inicie o script de inicialização, executando:
   ```bash
   sudo ha-cluster-init
   ```

   Se o NTP não foi configurado para iniciar no momento da inicialização, será exibida uma mensagem. 

   Se você decidir continuar mesmo assim, o script gera chaves de acesso do SSH e para a ferramenta de sincronização Csync2 automaticamente e iniciar os serviços necessários para ambos. 

3. Para configurar a camada de comunicação de cluster (Corosync): 

   a. Insira um endereço de rede para associar a. Por padrão, o script propõe o endereço de rede de eth0. Como alternativa, insira um endereço de rede diferente, por exemplo, o endereço do bond0. 

   b. Insira um endereço de multicast. O script propõe um endereço aleatório que você pode usar como padrão. 

   c. Insira uma porta de multicast. O script propõe 5405 como padrão. 

   d. Para configurar `SBD ()`, insira um caminho persistente para a partição do seu dispositivo de bloco que você deseja usar para SBD. O caminho deve ser consistente em todos os nós no cluster. 
   Por fim, o script iniciará o serviço Pacemaker para colocar o cluster de um nó online e habilitar a interface de gerenciamento da Web Hawk2. A URL a ser usado para Hawk2 é exibida na tela. 

4. Para todos os detalhes do processo de instalação, verifique `/var/log/sleha-bootstrap.log`. Agora você tem um cluster de um nó em execução. Verifique o status do cluster com o status de crm:

   ```bash
   sudo crm status
   ```

   Você também pode ver a configuração de cluster com `crm configure show xml` ou `crm configure show`.

5. O procedimento de inicialização cria um usuário do Linux denominado hacluster com o linux com a senha. Assim que possível, substitua a senha padrão com seguro: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Adicionar nós ao cluster existente

Se você tiver um cluster em execução com um ou mais nós, adicione mais nós de cluster com o script de inicialização de ha-cluster-join. O script precisa apenas de acesso a um nó de cluster existente e concluirá automaticamente a configuração básica no computador atual. Use as seguintes etapas:

Se você tiver configurado os nós de cluster existentes com o `YaST` módulo de cluster, verifique se os seguintes pré-requisitos foram atendidos antes de executar `ha-cluster-join`:
- O usuário raiz em nós existentes possui chaves SSH em vigor para o logon sem senha. 
- `Csync2` é configurado em nós existentes. Para obter mais informações, consulte Configurando Csync2 com YaST. 

1. Faça logon como raiz para o computador físico ou máquina virtual deve ingressar no cluster. 
2. Inicie o script de inicialização, executando: 

   ```bash
   sudo ha-cluster-join
   ```

   Se o NTP não foi configurado para iniciar no momento da inicialização, será exibida uma mensagem. 

3. Se você decidir continuar mesmo assim, você será solicitado para o endereço IP de um nó existente. Insira o endereço IP. 

4. Se você já não tiver configurado um acesso SSH sem senha entre as duas máquinas, você também será solicitado a senha raiz do nó existente. 

   Depois de fazer logon nó especificado, o script copia a configuração do Corosync, configura o SSH e `Csync2`e coloca o computador atual online como novo nó de cluster. Além disso, ele inicia o serviço necessário para Hawk. Se você tiver configurado o armazenamento compartilhado com `OCFS2`, ele também cria automaticamente o diretório de ponto de montagem para o `OCFS2` sistema de arquivos. 

5. Repita as etapas anteriores para todos os computadores que você deseja adicionar ao cluster. 

6. Para obter detalhes sobre o processo, verifique `/var/log/ha-cluster-bootstrap.log`. 

1. Verifique o status do cluster com `sudo crm status`. Se você tiver adicionado um segundo nó, a saída será semelhante ao seguinte:

   ```bash
   sudo crm status
   
   3 nodes configured
   1 resource configured
   Online: [ SLES1 SLES2 SLES3]
   Full list of resources:   
   admin_addr     (ocf::heartbeat:IPaddr2):       Started node1
   ```

   >[!NOTE]
   >`admin_addr` é o recurso de cluster IP virtual que é configurado durante a instalação de cluster inicial de um nó.

Depois de adicionar todos os nós, verifique se você precisa ajustar a política não de quorum nas opções de cluster global. Isso é especialmente importante para clusters de dois nós. Para obter mais informações, consulte a seção 4.1.2, a opção não-quorum-policy. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Definir propriedade de cluster cluster-verificar novamente-intervalo

`cluster-recheck-interval` indica o intervalo de sondagem em que o cluster verifica para alterações nos parâmetros de recursos, restrições ou outras opções de cluster. Se uma réplica ficar inativo, o cluster tenta reiniciar a réplica em um intervalo que é associado pela `failure-timeout` valor e o `cluster-recheck-interval` valor. Por exemplo, se `failure-timeout` é definido como 60 segundos e `cluster-recheck-interval` é definido como 120 segundos, a reinicialização é tentada em um intervalo que é maior que 60 segundos e menos de 120 segundos. É recomendável que você defina o tempo limite de falha como 60 e cluster-verificar novamente intervalo como um valor maior que 60 segundos. Não é recomendável definir o intervalo de nova verificação de cluster para um valor pequeno.

Para atualizar o valor da propriedade `2 minutes` executar:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se você já tiver um recurso de grupo de disponibilidade gerenciado por um cluster Pacemaker, observe que todas as distribuições que usam o mais recente disponível Pacemaker pacote 1.1.18-11.el7 introduzem uma alteração de comportamento para o cluster Iniciar falha-for-fatal configuração quando seu valor é false. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária sofrer uma interrupção, o cluster é esperado para o failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários perceberão que o cluster continua tentando iniciar a réplica primária com falha. Se esse principal nunca ficar online (devido a uma interrupção permanente), o cluster será nunca fará failover para outra réplica secundária disponível. Por causa dessa alteração, uma configuração recomendada anteriormente para definir o início falha-for-fatal não é mais válida e a configuração precisa ser revertido para seu valor padrão de `true`. Além disso, o recurso AG precisa ser atualizado para incluir o `failover-timeout` propriedade. 
>
>Para atualizar o valor da propriedade `true` executar:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>Atualizar sua propriedade de recurso existente do AG `failure-timeout` à `60s` executado (substituir `ag1` com o nome do recurso de grupo de disponibilidade): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Para obter mais informações sobre as propriedades de cluster do Pacemaker, consulte [configurar recursos de Cluster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

## <a name="configure-fencing-stonith"></a>Configurar o isolamento (STONITH)
Fornecedores de cluster do pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o cluster resource manager não pode determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster em um estado conhecido novamente.

Isolamento de nível de recurso principalmente garante que não há nenhum dano de dados durante uma interrupção por meio da configuração de um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com o DRBD (distribuído replicado o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inativo.

Isolamento de nível de nó garante que um nó não é executado todos os recursos. Isso é feito redefinindo o nó e a implementação do Pacemaker dele é chamada de STONITH (o que significa "acertar o outro nó no cabeçalho"). Pacemaker dá suporte a uma grande variedade de dispositivos, como uma fonte de alimentação ininterrupta fornecimento ou gerenciamento de placas de interface para servidores de isolamento.

Para obter mais informações, consulte [Clusters do Pacemaker do zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/), [isolamento e Stonith](https://clusterlabs.org/doc/crm_fencing.html) e [documentação HA do SUSE: Isolamento e STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

No momento da inicialização de cluster, o STONITH será desabilitado se nenhuma configuração é detectada. Ele pode ser habilitado mais tarde executando o seguinte comando:

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>Desabilitar o STONITH é apenas para fins de teste. Se você planeja usar o Pacemaker em um ambiente de produção, você deve planejar uma implementação de STONITH dependendo do seu ambiente e mantenha-a habilitada. SUSE fornece agentes de isolamento para todos os ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte para clusters de produção em execução nesses ambientes. Estamos trabalhando em uma solução para essa lacuna que estarão disponível em versões futuras.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar os recursos de cluster para o SQL Server

Consulte [Guid de administração do SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>Habilitar o Pacemaker

Habilite o Pacemaker para que ele será iniciado automaticamente.

Execute o seguinte comando em todos os nós no cluster.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>Criar recurso de grupo de disponibilidade

O comando a seguir cria e configura o recurso de grupo de disponibilidade para três réplicas de grupo de disponibilidade [ag1]. As operações de monitor e os tempos limite deve ser especificado explicitamente no SLES, com base no fato de que tempos limite é altamente dependentes de carga de trabalho e precisa ser cuidadosamente ajustadas para cada implantação.
Execute o comando em um de nós no cluster:

1. Executar `crm configure` para abrir o prompt de crm:

   ```bash
   sudo crm configure 
   ```

1. No prompt de crm, execute o seguinte comando para configurar as propriedades do recurso.

   ```bash
   primitive ag_cluster \
      ocf:mssql:ag \
      params ag_name="ag1" \
      meta failure-timeout=60s \
      op start timeout=60s \
      op stop timeout=60s \
      op promote timeout=60s \
      op demote timeout=10s \
      op monitor timeout=60s interval=10s \
      op monitor timeout=60s interval=11s role="Master" \
      op monitor timeout=60s interval=12s role="Slave" \
      op notify timeout=60s
   ms ms-ag_cluster ag_cluster \
      meta master-max="1" master-node-max="1" clone-max="3" \
     clone-node-max="1" notify="true" \
   commit
      ```

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

### <a name="create-virtual-ip-resource"></a>Criar recurso de IP virtual

Se você não criou o recurso IP virtual quando você executou `ha-cluster-init` agora você pode criar esse recurso. O comando a seguir cria um recurso IP virtual. Substitua `<**0.0.0.0**>` com um endereço disponível da sua rede e `<**24**>` com o número de bits na máscara de sub-rede CIDR. Execute em um nó.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Adicionar restrição de colocação
Quase todas as decisões em um cluster Pacemaker, como escolher onde um recurso deve ser executado, é feita comparando as pontuações. As pontuações são calculadas por recurso e o Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode ser executado nesse nó.) É possível manipular as decisões do cluster com as restrições. Restrições têm uma pontuação. Se uma restrição tiver uma pontuação inferior a infinito, é apenas uma recomendação. Uma pontuação de infinito significa que ele é uma necessidade. Queremos garantir que primária do grupo de disponibilidade e o virtual recurso ip sejam executados no mesmo host, portanto, definimos uma restrição de colocação, com uma pontuação de infinito. 

Para definir a restrição de colocação para o IP virtual ser executado no mesmo nó como o mestre, execute o seguinte comando em um nó:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação
A restrição de colocação possui uma restrição de ordenação implícita. Ele move o recurso IP virtual antes de mover o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é: 

1. O recurso de problemas do usuário migre para o mestre do grupo de disponibilidade do Nó1 para o node2.
2. Interrompe o recurso IP virtual no nó 1.
3. O recurso IP virtual é iniciado no nó 2. Neste ponto, o endereço IP temporariamente aponta para o nó 2 enquanto o nó 2 ainda é um pré-failover secundário. 
4. O mestre do grupo de disponibilidade no nó 1 é rebaixado para servidor subordinado.
5. O subordinado do grupo de disponibilidade no nó 2 é promovido a mestre. 

Para impedir que o endereço IP temporariamente apontando para o nó com o secundário antes do failover, adicione uma restrição de ordenação. Para adicionar uma restrição de ordenação, execute o seguinte comando em um nó: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão acoplados como intimamente com o sistema operacional enquanto estiverem em um Windows Server Failover Cluster (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração de todos os é feita por meio das ferramentas de gerenciamento de cluster. No SLES usar `crm`. 

Failover manual do grupo de disponibilidade com `crm`. Não inicie o failover com o Transact-SQL. Para obter mais informações, consulte [Failover](sql-server-linux-availability-group-failover-ha.md#failover).


Para obter mais informações, consulte:
- [Gerenciar recursos de cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [Alta disponibilidade conceitos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Referência rápida do pacemaker](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar o grupo de disponibilidade de alta disponibilidade](sql-server-linux-availability-group-failover-ha.md)
