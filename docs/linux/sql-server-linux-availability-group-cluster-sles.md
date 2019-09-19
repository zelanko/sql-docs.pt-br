---
title: Configurar o cluster do SLES para o Grupo de Disponibilidade do SQL Server
titleSuffix: SQL Server
description: Saiba como criar clusters de grupo de disponibilidade para o SQL Server no SLES (SUSE Linux Enterprise Server)
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 85180155-6726-4f42-ba57-200bf1e15f4d
ms.openlocfilehash: a14ad2d77b21dba2fd14ea7856aa7199bc081bbe
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2019
ms.locfileid: "70809822"
---
# <a name="configure-sles-cluster-for-sql-server-availability-group"></a>Configurar o cluster do SLES para o Grupo de Disponibilidade do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este guia fornece instruções para criar um cluster de três nós para o SQL Server no SLES (SUSE Linux Enterprise Server) 12 SP2. Para alta disponibilidade, um grupo de disponibilidade no Linux exige três nós – confira [Alta disponibilidade e proteção de dados para configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). A camada de clustering baseia-se no [HAE (Extensão de Alta Disponibilidade)](https://www.suse.com/products/highavailability) do SUSE criado com base no [Pacemaker](https://clusterlabs.org/). 

Para obter mais informações sobre configuração de cluster, opções do agente de recursos, gerenciamento, melhores práticas e recomendações, confira a [Extensão de Alta Disponibilidade do SUSE Linux Enterprise 12 SP2](https://www.suse.com/documentation/sle-ha-12/index.html).

>[!NOTE]
>Neste ponto, a integração do SQL Server com o Pacemaker no Linux não está tão acoplada quanto a do WSFC no Windows. O serviço SQL Server em Linux não reconhece clusters. O Pacemaker controla toda a orquestração dos recursos de cluster, incluindo o recurso de grupo de disponibilidade. No Linux, você não deve confiar em DMVs (exibições de gerenciamento dinâmico) do Grupo de Disponibilidade Always On que fornecem informações de cluster como sys.dm_hadr_cluster. Além disso, o nome da rede virtual é específico do WSFC; não há equivalente ao mesmo no Pacemaker. Você ainda poderá criar um ouvinte para usá-lo para reconexão transparente após o failover, mas será necessário registrar manualmente o nome do ouvinte no servidor DNS com o IP usado para criar o recurso de IP virtual (conforme explicado nas seções a seguir).


## <a name="roadmap"></a>Roteiro

O procedimento para criação de um grupo de disponibilidade para alta disponibilidade é distinto em servidores Linux e em um cluster de failover do Windows Server. A seguinte lista descreve as etapas de alto nível: 

1. [Configurar o SQL Server nos nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-failover-ha.md). 

3. Configurar um gerenciador de recursos de cluster, como o Pacemaker. Estas instruções são descritas neste documento.
   
   A maneira de configurar um gerenciador de recursos de cluster depende da distribuição específica do Linux. 

   >[!IMPORTANT]
   >Os ambientes de produção exigem um agente de isolamento, como o STONITH para alta disponibilidade. Os exemplos deste artigo não usam agentes de isolamento. Eles se destinam apenas a teste e validação. 
   
   >Um cluster do Pacemaker usa o isolamento para retornar o cluster a um estado conhecido. A maneira de configurar o isolamento depende da distribuição e do ambiente. No momento, o isolamento não está disponível em alguns ambientes de nuvem. Confira [Extensão de Alta Disponibilidade do SUSE Linux Enterprise](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing).

5. [Adicionar o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server). 

## <a name="prerequisites"></a>Prerequisites

Para concluir o cenário de ponta a ponta a seguir, você precisará de três computadores para implantar o cluster de três nós. As etapas a seguir descrevem como configurar esses servidores.

## <a name="setup-and-configure-the-operating-system-on-each-cluster-node"></a>Instalar e configurar o sistema operacional em cada nó de cluster 

A primeira etapa é configurar o sistema operacional nos nós de cluster. Para esse passo a passo, use o SLES 12 SP2 com uma assinatura válida para o complemento de HA.

### <a name="install-and-configure-sql-server-service-on-each-cluster-node"></a>Instalar e configurar o serviço SQL Server em cada nó de cluster

1. Instalar e configurar o serviço SQL Server em todos os nós. Para obter instruções detalhadas, confira [Instalar o SQL Server em Linux](sql-server-linux-setup.md).

1. Designe um nó como primário e outros nós como secundários. Use esses termos em todo este guia.

1. Verifique se os nós que farão parte do cluster podem se comunicar entre si.

   O exemplo a seguir mostra `/etc/hosts` com adições para três nós chamados SLES1, SLES2 e SLES3.

   ```
   127.0.0.1   localhost
   10.128.16.33 SLES1
   10.128.16.77 SLES2
   10.128.16.22 SLES3
   ```

   Todos os nós de cluster precisam conseguir acessar um ao outro via SSH. Ferramentas como `hb_report` ou `crm_report` (para solução de problemas) e Gerenciador de Histórico do Hawk exigem acesso SSH sem senha entre os nós, caso contrário, elas só podem coletar dados do nó atual. Caso você use uma porta SSH não padrão, use a opção -X (confira a página `man`). Por exemplo, se a porta SSH for 3479, invoque um `crm_report` com:

   ```bash
   sudo crm_report -X "-p 3479" [...]
   ```

   Para obter mais informações, confira a [seção Diversos – Guia de Administração do SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.misc).


## <a name="create-a-sql-server-login-for-pacemaker"></a>Criar um logon do SQL Server para o Pacemaker

[!INCLUDE [SLES-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="configure-an-always-on-availability-group"></a>Configurar um Grupo de Disponibilidade Always On

Em servidores Linux, configure o grupo de disponibilidade e, em seguida, configure os recursos de cluster. Para configurar o grupo de disponibilidade, confira [Configurar um Grupo de Disponibilidade Always On para o SQL Server em Linux](sql-server-linux-availability-group-configure-ha.md)

## <a name="install-and-configure-pacemaker-on-each-cluster-node"></a>Instalar e configurar o Pacemaker em cada nó de cluster

1. Instalar a extensão de Alta Disponibilidade

   Para referência, confira [Como instalar o SUSE Linux Enterprise Server e a Extensão de Alta Disponibilidade](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.installation)

1. Instale o pacote do agente de recursos do SQL Server em ambos os nós.

   ```bash
   sudo zypper install mssql-server-ha
   ```

## <a name="set-up-the-first-node"></a>Configurar o primeiro nó

   Veja as [instruções de instalação do SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/install-quick/install-quick.html#sec.ha.inst.quick.setup.1st-node)

1. Faça logon como `root` no computador físico ou na máquina virtual que deseja usar como o nó de cluster.
2. Inicie o script de inicialização executando:
   ```bash
   sudo ha-cluster-init
   ```

   Se o NTP não tiver sido configurado para ser iniciado no momento da inicialização, uma mensagem será exibida. 

   Se você decidir continuar mesmo assim, o script gerará automaticamente chaves para acesso SSH e para a ferramenta de sincronização Csync2 e iniciará os serviços necessários para ambos. 

3. Para configurar a camada de comunicação do cluster (Corosync): 

   A. Insira um endereço de rede para associação. Por padrão, o script propõe o endereço de rede eth0. Como alternativa, insira outro endereço de rede, por exemplo, o endereço bond0. 

   B. Insira um endereço multicast. O script propõe um endereço aleatório que pode ser usado como padrão. 

   c. Insira uma porta multicast. O script propõe 5405 como o padrão. 

   d. Para configurar `SBD ()`, insira um caminho persistente para a partição do dispositivo de bloqueio que você deseja usar para o SBD. O caminho precisa ser consistente em todos os nós no cluster. 
   Por fim, o script iniciará o serviço Pacemaker para colocar o cluster de um nó online e habilitará a interface de gerenciamento da Web Hawk2. A URL a ser usada para o Hawk2 é exibida na tela. 

4. Para obter detalhes sobre o processo de instalação, confira `/var/log/sleha-bootstrap.log`. Agora você tem um cluster de um nó em execução. Verifique o status do cluster com crm status:

   ```bash
   sudo crm status
   ```

   Você também poderá ver a configuração do cluster com `crm configure show xml` ou `crm configure show`.

5. O procedimento de inicialização cria um usuário do Linux chamado hacluster com a senha linux. Substitua a senha padrão por uma segura assim que possível: 

   ```bash
   sudo passwd hacluster
   ```

## <a name="add-nodes-to-the-existing-cluster"></a>Adicionar nós ao cluster existente

Se você tiver um cluster em execução com um ou mais nós, adicione mais nós de cluster com o script de inicialização ha-cluster-join. O script precisa apenas ter acesso a um nó de cluster existente e concluirá a configuração básica no computador atual automaticamente. Use as seguintes etapas:

Se você tiver configurado os nós de cluster existentes com o módulo de cluster `YaST`, verifique se os seguintes pré-requisitos são atendidos antes de executar `ha-cluster-join`:
- O usuário raiz nos nós existentes tem chaves SSH em vigor para o logon sem senha. 
- `Csync2` está configurado nos nós existentes. Para obter mais informações, confira Como configurar o Csync2 com o YaST. 

1. Faça logon como raiz no computador físico ou na máquina virtual que deverá ingressar no cluster. 
2. Inicie o script de inicialização executando: 

   ```bash
   sudo ha-cluster-join
   ```

   Se o NTP não tiver sido configurado para ser iniciado no momento da inicialização, uma mensagem será exibida. 

3. Se você decidir continuar mesmo assim, insira o endereço IP de um nó existente. Insira o endereço IP. 

4. Se você ainda não tiver configurado um acesso SSH sem senha entre ambos os computadores, você também deverá fornecer a senha raiz do nó existente. 

   Depois que você fizer logon no nó especificado, o script copiará a configuração do Corosync, configurará o SSH e `Csync2` e colocará o computador atual online como o novo nó de cluster. Além disso, ele iniciará o serviço necessário para o Hawk. Se você tiver configurado o armazenamento compartilhado com `OCFS2`, ele também criará automaticamente o diretório de ponto de montagem para o sistema de arquivos do `OCFS2`. 

5. Repita as etapas anteriores para todos os computadores que deseja adicionar ao cluster. 

6. Para obter detalhes sobre o processo, confira `/var/log/ha-cluster-bootstrap.log`. 

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
   >`admin_addr` é o recurso de cluster de IP virtual que é definido durante a configuração inicial do cluster de um nó.

Depois de adicionar todos os nós, verifique se você precisa ajustar a no-quorum-policy nas opções globais de cluster. Isso é especialmente importante para clusters de dois nós. Para obter mais informações, confira a seção 4.1.2, Opção no-quorum-policy. 

## <a name="set-cluster-property-cluster-recheck-interval"></a>Definir a propriedade de cluster cluster-recheck-interval

`cluster-recheck-interval` indica o intervalo de sondagem segundo o qual o cluster verifica se há alterações nos parâmetros de recurso, restrições ou outras opções de cluster. Se uma réplica ficar inativa, o cluster tentará reiniciar a réplica em um intervalo associado ao valor `failure-timeout` e ao valor `cluster-recheck-interval`. Por exemplo, se `failure-timeout` for definido como 60 segundos e `cluster-recheck-interval` for definido como 120 segundos, será realizada uma tentativa de reinicialização em um intervalo superior a 60 segundos, mas inferior a 120 segundos. Recomendamos que você defina failure-timeout como 60 segundos e cluster-recheck-interval com um valor superior a 60 segundos. Não é recomendável definir cluster-recheck-interval como um valor pequeno.

Para atualizar o valor da propriedade para `2 minutes`, execute:

```bash
crm configure property cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Se você já tiver um recurso de grupo de disponibilidade gerenciado por um cluster do Pacemaker, observe que todas as distribuições que usam o pacote mais recente disponível do Pacemaker 1.1.18-11.el7 introduzem uma alteração de comportamento para a configuração de cluster start-failure-is-fatal quando seu valor é falso. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária apresentar uma interrupção, o cluster deverá fazer failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários observarão que o cluster continua tentando iniciar a réplica primária com falha. Se a primária nunca ficar online (devido a uma interrupção permanente), o cluster nunca fará failover para outra réplica secundária disponível. Devido a essa alteração, a configuração recomendada anteriormente para definir start-failure-is-fatal não é mais válida e a configuração precisa ser revertida de volta para seu valor padrão `true`. Além disso, o recurso do AG precisa ser atualizado para incluir a propriedade `failover-timeout`. 
>
>Para atualizar o valor da propriedade para `true`, execute:
>
>```bash
>crm configure property start-failure-is-fatal=true
>```
>
>Atualize a propriedade do recurso do AG existente `failure-timeout` para a execução de `60s` (substitua `ag1` pelo nome do recurso de grupo de disponibilidade): 
>
>```bash
>crm configure edit ag1
># In the text editor, add `meta failure-timeout=60s` after any `param`s and before any `op`s
>```

Para obter mais informações sobre as propriedades de cluster do Pacemaker, confira [Como configurar recursos de cluster](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_config_crm_resources.html).

## <a name="configure-fencing-stonith"></a>Configurar o isolamento (STONITH)
Os fornecedores de cluster do Pacemaker exigem que o STONITH seja habilitado e um dispositivo de isolamento definido para uma configuração de cluster compatível. Quando o gerenciador de recursos de cluster não pode determinar o estado de um nó ou de um recurso em um nó, o isolamento é usado para colocar o cluster em um estado conhecido novamente.

O isolamento no nível do recurso garante principalmente que não haja dados corrompidos durante uma interrupção pela configuração de um recurso. Você pode usar o isolamento no nível do recurso, por exemplo, com o DRBD (Dispositivo de Bloco Replicado Distribuído) para marcar o disco em um nó como desatualizado quando o link de comunicação ficar inativo.

O isolamento no nível do nó garante que um nó não execute nenhum recurso. Isso é feito pela redefinição do nó e pela implementação do Pacemaker do que é chamado STONITH (que significa "acertar a cabeça do outro nó"). O Pacemaker dá suporte a uma grande variedade de dispositivos de isolamento, como no-break ou adaptadores de rede de gerenciamento para servidores.

Para obter mais informações, consulte:

- [Clusters do Pacemaker do zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/)
- [Isolamento e STONITH](https://clusterlabs.org/doc/crm_fencing.html)
- [Documentação sobre HA do SUSE: Isolamento e STONITH](https://www.suse.com/documentation/sle_ha/book_sleha/data/cha_ha_fencing.html)

No momento da inicialização do cluster, o STONITH será desabilitado se nenhuma configuração for detectada. Ele poderá ser habilitado mais tarde pela execução do seguinte comando:

```bash
sudo crm configure property stonith-enabled=true
```
  
>[!IMPORTANT]
>A desabilitação do STONITH destina-se apenas a fins de teste. Se pretender usar o Pacemaker em um ambiente de produção, você deverá planejar uma implementação do STONITH dependendo do ambiente e mantê-lo habilitado. O SUSE não fornece agentes de isolamento para nenhum ambiente de nuvem (incluindo o Azure) ou o Hyper-V. Consequentemente, o fornecedor do cluster não dá suporte para a execução de clusters de produção nesses ambientes. Estamos trabalhando em uma solução para essa lacuna que estará disponível em versões futuras.

## <a name="configure-the-cluster-resources-for-sql-server"></a>Configurar os recursos de cluster para o SQL Server

Veja o [Guia de Administração do SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.manual_config)

## <a name="enable-pacemaker"></a>Habilitar o Pacemaker

Habilite o Pacemaker para que ele seja iniciado automaticamente.

Execute o comando a seguir em cada nó do cluster.

```bash
systemctl enable pacemaker
```

### <a name="create-availability-group-resource"></a>Criar um recurso do grupo de disponibilidade

O comando a seguir cria e configura o recurso de grupo de disponibilidade para três réplicas do grupo de disponibilidade [ag1]. As operações e os tempos limite do monitor precisam ser especificados explicitamente no SLES com base no fato de que os tempos limite são altamente dependentes da carga de trabalho e precisam ser ajustados cuidadosamente para cada implantação.
Execute o comando em um dos nós do cluster:

1. Execute `crm configure` para abrir o prompt do CRM:

   ```bash
   sudo crm configure 
   ```

1. No prompt do CRM, execute o comando a seguir para configurar as propriedades do recurso.

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

### <a name="create-virtual-ip-resource"></a>Criar um recurso de IP virtual

Caso não tenha criado o recurso de IP virtual quando executou `ha-cluster-init`, crie esse recurso agora. O comando a seguir cria um recurso de IP virtual. Substitua `<**0.0.0.0**>` por um endereço disponível na rede e `<**24**>` pelo número de bits na máscara de sub-rede CIDR. Execução em um nó.

```bash
crm configure \
primitive admin_addr \
   ocf:heartbeat:IPaddr2 \
   params ip=<**0.0.0.0**> \
      cidr_netmask=<**24**>
```

### <a name="add-colocation-constraint"></a>Adicionar uma restrição de colocalização
Quase todas as decisões em um cluster do Pacemaker, como escolher o local em que um recurso deve ser executado, são feitas pela comparação de pontuações. As pontuações são calculadas por recurso e o gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um recurso específico. (Se um nó tiver uma pontuação negativa para um recurso, o recurso não poderá ser executado nesse nó.) Podemos manipular as decisões do cluster com restrições. As restrições têm uma pontuação. Se uma restrição tiver uma pontuação menor que INFINITY, ela será apenas uma recomendação. Uma pontuação igual a INFINITY significa que ela é obrigatória. Queremos garantir que o primário do grupo de disponibilidade e o recurso de IP virtual sejam executados no mesmo host e, portanto, definimos uma restrição de colocalização com uma pontuação igual a INFINITY. 

Para definir a restrição de colocalização para o IP virtual ser executado no mesmo nó do mestre, execute o seguinte comando em um nó:

```bash
crm configure
colocation vip_on_master inf: \
    admin_addr ms-ag_cluster:Master
commit
```

### <a name="add-ordering-constraint"></a>Adicionar uma restrição de ordenação
A restrição de colocalização tem uma restrição de ordenação implícita. Ela move o recurso de IP virtual antes de mover o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é: 

1. O usuário emite a migração do recurso para o mestre do grupo de disponibilidade de node1 para node2.
2. O recurso de IP virtual é interrompido no nó 1.
3. O recurso de IP virtual é iniciado no nó 2. Neste ponto, o endereço IP aponta temporariamente para o nó 2, enquanto o nó 2 ainda é um secundário de pré-failover. 
4. O mestre do grupo de disponibilidade no nó 1 é rebaixado a servidor subordinado.
5. O servidor subordinado do grupo de disponibilidade no nó 2 é promovido a mestre. 

Para impedir que o endereço IP aponte temporariamente para o nó com o secundário de pré-failover, adicione uma restrição de ordenação. Para adicionar uma restrição de ordenação, execute o comando a seguir em um nó: 

```bash
crm crm configure \
   order ag_first inf: ms-ag_cluster:promote admin_addr:start
```


>[!IMPORTANT]
>Depois de configurar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, você não poderá usar o Transact-SQL para fazer failover dos recursos de grupo de disponibilidade. Os recursos de cluster do SQL Server em Linux não são acoplados tão firmemente com o sistema operacional como são em um WSFC (cluster de failover do Windows Server). O serviço SQL Server não reconhece a presença do cluster. Toda a orquestração é feita por meio das ferramentas de gerenciamento de cluster. No SLES, use `crm`. 

Faça failover manual de um grupo de disponibilidade com `crm`. Não inicie o failover com o Transact-SQL. Para obter mais informações, confira [Failover](sql-server-linux-availability-group-failover-ha.md#failover).


Para obter mais informações, consulte:
- [Como gerenciar recursos de cluster](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.config.crm).   
- [Conceitos de HA](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.concepts)
- [Referência rápida do Pacemaker](https://github.com/ClusterLabs/pacemaker/blob/master/doc/pcs-crmsh-quick-ref.md) 

<!---[!INCLUDE [Pacemaker Concepts](..\includes\ss-linux-cluster-pacemaker-concepts.md)]--->

## <a name="next-steps"></a>Próximas etapas

[Operar grupo de disponibilidade de HA](sql-server-linux-availability-group-failover-ha.md)
