---
title: Configurar SLES Cluster para o grupo de disponibilidade do SQL Server | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 05/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 50a2633790b9878a8be2a9a3c417fc877a37633d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configurar SLES Cluster para o grupo de disponibilidade do SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este guia fornece instruções para criar um cluster de três nós para o SQL Server no SUSE Linux Enterprise Server (SLES) 12 SP2. Para alta disponibilidade, um grupo de disponibilidade no Linux requer três nós - consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). A camada de clustering é baseada no SUSE [alta disponibilidade extensão (HAE)](https://www.suse.com/products/highavailability) criado na parte superior do [Pacemaker](http://clusterlabs.org/). 

Para obter mais detalhes sobre a configuração de cluster, opções do recurso de agente, gerenciamento, as práticas recomendadas e recomendações, consulte [SUSE Linux Enterprise alta disponibilidade extensão 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>Neste ponto, a integração do SQL Server com Pacemaker no Linux não é como acoplada como com o WSFC no Windows. O serviço do SQL Server no Linux não está ciente do cluster. Pacemaker controla todas a orquestração os recursos de cluster, incluindo o recurso de grupo de disponibilidade. No Linux, você não deve depender sempre em disponibilidade grupo exibições de gerenciamento dinâmico (DMVs) que fornecem informações de cluster, como sys.DM hadr_cluster. Além disso, o nome de rede virtual é específico para o WSFC, não há nenhum equivalente do mesmo em Pacemaker. Você ainda pode criar um ouvinte para usá-lo para a reconexão depois do failover transparente, mas você terá que registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso IP virtual (como explicado abaixo).


## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto níveis: 

1. [Configurar o SQL Server em nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-failover-ha.md). 

3. Configure um Gerenciador de recursos de cluster, como Pacemaker. Essas instruções são neste documento.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende da distribuição específica do Linux. 

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento, como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster Pacemaker usa isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende a distribuição e o ambiente. Neste momento, o isolamento não está disponível em alguns ambientes de nuvem. Consulte [extensão de alta disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Adicione o grupo de disponibilidade como um recurso do cluster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Pré-requisitos

Para completar o cenário de ponta a ponta abaixo você precisa de três máquinas para implantar o cluster de três nós. As etapas abaixo descrevem como configurar esses servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster 

A primeira etapa é configurar o sistema operacional em nós de cluster. Para este passo a passo, use SLES 12 SP2 com uma assinatura válida para o complemento de alta disponibilidade.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Instalar e configurar o serviço do SQL Server em cada nó de cluster

1. Instalar e configurar o serviço do SQL Server em todos os nós. Para obter instruções detalhadas, consulte [instalar o SQL Server no Linux](sql-server-linux-setup.md).

1. Designe um nó como primários e de outros nós como secundários. Use estes termos em todo este guia.

1. Certifique-se de nós que serão parte do cluster podem se comunicar entre si.

   A exemplo a seguir mostra `/etc/hosts` com adições para três nós denominados SLES1, SLES2 e SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Todos os nós de cluster devem ser capazes de acessar umas às outras por meio do SSH. Ferramentas como o `hb_report` ou `crm_report` (para solução de problemas) e histórico Explorer do Hawk exigem acesso SSH passwordless entre os nós, caso contrário, eles só poderá coletar dados do nó atual. No caso de você usar uma porta SSH não padrão, use a opção -X (consulte `man` página). Por exemplo, se a porta SSH é 3479, invoque um `crm_report` com:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Para obter informações adicionais, consulte o [SLES Administration Guide - seção diverso](http://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurar um grupo de disponibilidade do AlwaysOn

Em servidores Linux configurar o grupo de disponibilidade e, em seguida, configure os recursos de cluster. Para configurar o grupo de disponibilidade, consulte [Configurar grupo de disponibilidade AlwaysOn para SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar Pacemaker em cada nó de cluster

1. Instalar a extensão de alta disponibilidade

   Para referência, consulte [instalando o SUSE Linux Enterprise Server e a extensão de alta disponibilidade](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Instale o pacote de agente de recurso do SQL Server em ambos os nós.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurar o primeiro nó

   Consulte [instruções de instalação do SLES](http://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Faça logon como `root` para a máquina virtual que você deseja usar como nó de cluster ou física.
2. Inicie o script de inicialização, executando:
   ```bash
   sudo ha-cluster-init
   ```

   Se o NTP não tiver sido configurado para iniciar no momento da inicialização, será exibida uma mensagem. 

   Se você optar por continuar mesmo assim, o script será automaticamente gerar chaves para acesso SSH e para a ferramenta de sincronização Csync2 e iniciar os serviços necessários para ambos. 

3. Para configurar a camada de comunicação do cluster (Corosync): 

   A. Insira um endereço de rede para associar a. Por padrão, o script irá propor o endereço de rede de eth0. Como alternativa, digite um endereço de rede diferente, por exemplo, o endereço de bond0. 

   B. Insira um endereço de multicast. O script propõe um endereço aleatório que você pode usar como padrão. 

   c. Insira uma porta de multicast. O script propõe 5405 como padrão. 

   d. Para configurar `SBD ()`, insira um caminho persistente para a partição de seu dispositivo de bloco que você deseja usar para SBD. O caminho deve ser consistente em todos os nós no cluster. 
   Por fim, o script iniciará o serviço de Pacemaker para colocar o cluster de um nó online e habilitar a interface de gerenciamento da Web Hawk2. A URL a ser usado para Hawk2 é exibida na tela. 

4. Para todos os detalhes do processo de instalação, verifique `/var/log/sleha-bootstrap.log`. Agora você tem um cluster de um nó em execução. Verifique o status do cluster com o status de crm:

   ```bash
   sudo crm status
   ```

   Você também pode ver a configuração de cluster com `crm configure show xml` ou `crm configure show`.

5. O procedimento de inicialização cria um usuário do Linux denominado hacluster com senha linux. Assim que possível, substitua a senha padrão com um seguro: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Adicionar nós ao cluster existente

Se você tiver um cluster executando o com um ou mais nós, adicione mais nós de cluster com o script de inicialização de ha cluster-junção. O script precisa apenas de acesso para um nó de cluster existente e concluirá automaticamente a configuração básica no computador atual. Siga as etapas abaixo:

Se você tiver configurado os nós de cluster existentes com o `YaST` módulo de cluster, verifique se os seguintes pré-requisitos foram atendidos antes de executar `ha-cluster-join`:
- O usuário raiz no de nós existentes tem as chaves de SSH em vigor para logon passwordless. 
- `Csync2`é configurado em nós existentes. Para obter detalhes, consulte Configurando Csync2 com YaST. 

1. Faça logon como raiz para o computador físico ou virtual deve ingressar no cluster. 
2. Inicie o script de inicialização, executando: 

   ```bash
   sudo ha-cluster-join
   ```

   Se o NTP não tiver sido configurado para iniciar no momento da inicialização, será exibida uma mensagem. 

3. Se você optar por continuar mesmo assim, você será solicitado para o endereço IP de um nó existente. Insira o endereço IP. 

4. Se você já não tiver configurado um acesso SSH passwordless entre os dois computadores, você também será solicitado a senha raiz do nó existente. 

   Depois de fazer logon nó especificado, o script irá copiar a configuração de Corosync, configure SSH e `Csync2`e o colocará a máquina atual online como novo nó de cluster. Além disso, ele iniciará o serviço necessário para Hawk. Se você tiver configurado o armazenamento compartilhado com `OCFS2`, ele criará automaticamente o diretório de montagem para o `OCFS2` sistema de arquivos. 

5. Repita as etapas acima para todos os computadores que você deseja adicionar ao cluster. 

6. Para obter detalhes sobre o processo, consulte `/var/log/ha-cluster-bootstrap.log`. 

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
   >`admin_addr`é o recurso de cluster IP virtual que é configurado durante a instalação de cluster de um nó inicial.

Depois de adicionar todos os nós, verifique se você precisa ajustar a política não de quorum nas opções de cluster global. Isso é especialmente importante para clusters de dois nós. Para obter mais informações, consulte a seção 4.1.2, opção nenhum quorum política. 

## <a name="set-cluster-property-start-failure-is-fatal-to-false"></a>Defina a propriedade cluster Iniciar falha-for-fatal como false

`Start-failure-is-fatal`Indica se uma falha ao iniciar um recurso em um nó adicional impede as tentativas de iniciar nesse nó. Quando definido como `false`, o cluster decidirá se deseja tentar iniciar no mesmo nó novamente com base no limite do recurso atual falha contagem e a migração. Portanto, após o failover, Pacemaker tentará iniciar o recurso de grupo de disponibilidade no primeiro primário depois que a instância do SQL está disponível. Pacemaker cuidará de rebaixamento a réplica secundária e ele será automaticamente reingressar no grupo de disponibilidade. Além disso, se `start-failure-is-fatal` é definido como `false`, o cluster voltará para os limites de failcount configurado configurados com o limite de migração, você precisa fazer se padrão para o limite de migração é atualizado adequadamente.

Para atualizar o valor da propriedade para executar false:
```bash
sudo crm configure property start-failure-is-fatal=false
sudo crm configure rsc_defaults migration-threshold=5000
```
Se a propriedade tem o valor padrão de `true`, se a primeira tentativa de iniciar o recurso falhar, a intervenção do usuário é necessária após um failover automático para a contagem de falhas do recurso de limpeza e redefinir a configuração usando: `sudo crm resource cleanup <resourceName>` comando.

Para obter mais detalhes sobre propriedades do cluster Pacemaker consulte [configurar recursos de Cluster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

# <a name="configure-fencing-stonith"></a>Configurar isolamento (STONITH)
Fornecedores de cluster pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. Quando o Gerenciador de recursos de cluster não é possível determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster para um estado conhecido novamente.
Isolamento de nível de recurso principalmente garante que não há nenhuma corrupção de dados em caso de uma interrupção ao configurar um recurso. Você pode usar o isolamento de nível de recurso, por exemplo, o link de comunicação com DRBD (Distributed replicados o dispositivo de bloco) para marcar o disco em um nó como desatualizado quando fica inoperante.
Isolamento de nível de nó garante que um nó não seja executado para todos os recursos. Isso é feito redefinindo o nó e a implementação de Pacemaker dele é chamada STONITH (que significa "solucionar o outro nó no cabeçalho"). Pacemaker oferece suporte a uma grande variedade de dispositivos de isolamento, por exemplo, no-break ou gerenciamento de placas de interface para servidores.
Para obter mais detalhes, consulte [Pacemaker Clusters do zero](http://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html), [isolamento e Stonith](http://clusterlabs.org/doc/crm_fencing.html) e [documentação SUSE HA: isolamento e STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html).

Em tempo de inicialização do cluster, STONITH será desabilitado se nenhuma configuração é detectada. Ele pode ser habilitado mais tarde executando o comando abaixo

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>Desabilitar STONITH é apenas para fins de teste. Se você planeja usar Pacemaker em um ambiente de produção, você deve planejar uma implementação STONITH dependendo do seu ambiente e mantê-lo habilitado. Observe que SUSE não fornece isolamento agentes para ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte à execução de clusters de produção nesses ambientes. Estamos trabalhando em uma solução para essa lacuna que estarão disponível em versões futuras.


## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar os recursos de cluster do SQL Server

Consulte [SLES administração Guid](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

### <a name="create-availability-group-resource"></a>Criar o recurso de grupo de disponibilidade

O comando a seguir cria e configura o recurso de grupo de disponibilidade para 3 réplicas do grupo de disponibilidade [ag1]. A monitorar operações e tempos limite precisa ser especificado explicitamente no SLES baseada no fato de que tempos limite é altamente dependente de carga de trabalho e precisa ser cuidadosamente ajustadas para cada implantação.
Execute o comando em um de nós no cluster:

1. Execute `crm configure` para abrir o prompt de crm:

   ```bash
   sudo crm configure 
   ```

1. No prompt do crm, execute o comando a seguir para configurar as propriedades do recurso.

   ```bash
primitive ag_cluster \
   ocf:mssql:ag \
   params ag_name="ag1" \
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

### <a name="create-virtual-ip-resource"></a>Criar o recurso IP virtual

Se você não criou o recurso IP virtual quando você executou `ha-cluster-init` você pode criar esse recurso agora. O comando a seguir cria um recurso IP virtual. Substituir `<**0.0.0.0**>` com um endereço disponível da rede e `<**24**>` com o número de bits na máscara de sub-rede CIDR. Execute em um nó.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Adicionar restrição de colocação
Quase todas as decisões em um cluster de Pacemaker, como escolher em que um recurso deve ser executado, é feito comparando pontuações. Pontuações são calculadas por recurso e o Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode executar nesse nó). É possível manipular as decisões de cluster com restrições. As restrições terão uma pontuação. Se uma restrição tem uma pontuação menor que infinito, é apenas uma recomendação. Uma pontuação de infinito significa é obrigatória. Queremos garantir que primária do grupo de disponibilidade e virtual recurso ip são executados no mesmo host, portanto definiremos uma restrição de colocação com uma pontuação de infinito. 

Para definir a restrição de colocação para o IP virtual ser executado no mesmo nó como o mestre, execute o seguinte comando em um nó:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação
A restrição de colocação tem uma restrição de ordenação implícita. Ele move o recurso IP virtual antes de ele move o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é: 

1. Recurso de problemas do usuário migrar para o mestre de grupo de disponibilidade do Nó1 para o Nó2.
2. Interrompe o recurso IP virtual no nó 1.
3. O recurso IP virtual é iniciado no nó 2. Neste ponto, o endereço IP temporariamente aponta para o nó 2 enquanto o nó 2 ainda é um failover anterior secundário. 
4. O mestre de grupo de disponibilidade no nó 1 é rebaixado para slave.
5. Os subordinados do grupo de disponibilidade no nó 2 é promovido a mestre. 

Para impedir que o endereço IP temporariamente apontando para o nó com o secundário pre-failover, adicione uma restrição de ordenação. Para adicionar uma restrição de ordenação, execute o seguinte comando em um nó: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão ligados como intimamente com o sistema operacional como estão em um Cluster de Failover do Windows Server (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração todos é feita por meio das ferramentas de gerenciamento de cluster. SLES usar `crm`. 

O failover manualmente o grupo de disponibilidade com `crm`. Não inicie o failover com o Transact-SQL. Para obter instruções, consulte [Failover](sql-server-linux-availability-group-failover-ha.md#failover).


Para obter detalhes adicionais, consulte:
- [Gerenciar recursos de cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [HA conceitos](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Referência rápida pacemaker](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar o grupo de disponibilidade de alta disponibilidade](sql-server-linux-availability-group-failover-ha.md)

