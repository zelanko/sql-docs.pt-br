---
title: Configurar o Cluster do RHEL para o grupo de disponibilidade do SQL Server | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 06/14/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: ec5ed0ce61c1b1f48ecc148326b9a1906ff95122
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670815"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Configurar o Cluster do RHEL para o grupo de disponibilidade do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica como criar um cluster do grupo de disponibilidade de três nós para o SQL Server no Red Hat Enterprise Linux. Para alta disponibilidade, um grupo de disponibilidade no Linux exige três nós – veja [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). A camada de clustering é baseada no Red Hat Enterprise Linux (RHEL) [complemento HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) criado na parte superior da [Pacemaker](https://clusterlabs.org/). 

> [!NOTE] 
> Acesso à documentação completa do Red Hat requer uma assinatura válida. 

Para obter mais informações sobre a configuração de cluster, opções de agentes de recursos e gerenciamento, visite [documentação de referência do RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> SQL Server não é rigorosamente integrado com o Pacemaker no Linux quanto com o clustering de failover do Windows Server. Uma instância do SQL Server não está ciente do cluster. Pacemaker fornece orquestração de recurso de cluster. Além disso, o nome de rede virtual é específico ao clustering de failover do Windows Server - não há nenhum equivalente no Pacemaker. Exibições de gerenciamento dinâmico disponibilidade grupo (DMVs) que consultar informações de cluster retornam linhas vazias nos clusters do Pacemaker. Para criar um ouvinte para reconexão transparente após o failover, registre manualmente o nome do ouvinte no DNS com o IP usado para criar o recurso IP virtual. 

As seções a seguir percorrer as etapas para configurar um cluster do Pacemaker e adicionar um grupo de disponibilidade como recurso no cluster de alta disponibilidade.

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server em nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md). 

3. Configure um Gerenciador de recursos de cluster, como o Pacemaker. Essas instruções são neste documento.
   
   A maneira de configurar um Gerenciador de recursos de cluster depende a distribuição Linux específica. 

   >[!IMPORTANT]
   >Ambientes de produção exigem um agente de isolamento como STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações são para teste e validação somente. 
   
   >Um cluster do Linux usa o isolamento para retornar o cluster para um estado conhecido. A maneira de configurar o isolamento depende da distribuição e o ambiente. Atualmente, o isolamento não está disponível em alguns ambientes de nuvem. Para obter mais informações, consulte [políticas de suporte para Clusters de disponibilidade alta RHEL - plataformas de virtualização](https://access.redhat.com/articles/29440).

5. [Adicione o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Configurar a alta disponibilidade para RHEL

Para configurar a alta disponibilidade do RHEL, habilitar a assinatura de alta disponibilidade e, em seguida, configure o Pacemaker.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Habilitar a assinatura de alta disponibilidade para RHEL

Cada nó do cluster deve ter uma assinatura apropriada para RHEL e a alta disponibilidade adicionar. Examine os requisitos descritos em [como instalar pacotes de cluster de alta disponibilidade no Red Hat Enterprise Linux](https://access.redhat.com/solutions/45930). Siga estas etapas para configurar a assinatura e repositórios:

1. Registre o sistema.

   ```bash
   sudo subscription-manager register
   ```

   Forneça seu nome de usuário e senha.   

1. Liste os pools disponíveis para o registro.

   ```bash
   sudo subscription-manager list --available
   ```

   Na lista de pools disponíveis, observe a ID do pool para a assinatura de alta disponibilidade.

1. Atualize o script a seguir. Substitua `<pool id>` com a ID do pool para alta disponibilidade da etapa anterior. Execute o script para anexar a assinatura.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Habilite o repositório.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Para obter mais informações, consulte [Pacemaker – o software livre, Cluster de alta disponibilidade](https://www.opensourcerers.org/pacemaker-the-open-source-high-availability-cluster/). 

Depois de configurar a assinatura, conclua as seguintes etapas para configurar o Pacemaker:

### <a name="configure-pacemaker"></a>Configurar o Pacemaker

Depois de registrar a assinatura, conclua as seguintes etapas para configurar o Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Depois que o Pacemaker é configurado, use `pcs` para interagir com o cluster. Execute todos os comandos em um nó do cluster. 

## <a name="configure-fencing-stonith"></a>Configurar o isolamento (STONITH)

Fornecedores de cluster do pacemaker exigem STONITH esteja habilitado e um dispositivo de isolamento configurado para uma configuração de cluster com suporte. STONITH significa "envie outro nó no cabeçalho". Quando o cluster resource manager não pode determinar o estado de um nó ou de um recurso em um nó, o isolamento traz o cluster para um estado conhecido novamente.

Isolamento de nível de recursos garante que não há nenhum dano de dados em caso de interrupção por meio da configuração de um recurso. Por exemplo, você pode usar o isolamento de nível de recurso para marcar o disco em um nó como desatualizado quando o link de comunicação fica inativo. 

Isolamento de nível de nó garante que um nó não é executado todos os recursos. Isso é feito redefinindo o nó. Pacemaker dá suporte a uma grande variedade de dispositivos de isolamento. Os exemplos incluem uma fonte de alimentação ininterrupta fornecimento ou gerenciamento de placas de interface para servidores.

Para obter informações sobre STONITH e isolamento, consulte os seguintes artigos:

* [Clusters do pacemaker do zero](https://clusterlabs.org/doc/en-US/Pacemaker/1.1-plugin/html/Clusters_from_Scratch/ch05.html)
* [Isolamento e STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Complemento de alta disponibilidade do Red Hat com o Pacemaker: de isolamento](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

Como o nível do nó de configuração de isolamento depende muito do seu ambiente, desabilite-o para este tutorial (ele pode ser configurado mais tarde). O script a seguir desabilita o isolamento de nível de nó:

```bash
sudo pcs property set stonith-enabled=false
```
  
>[!IMPORTANT]
>Desabilitar o STONITH é apenas para fins de teste. Se você planeja usar o Pacemaker em um ambiente de produção, você deve planejar uma implementação de STONITH dependendo do seu ambiente e mantenha-a habilitada. RHEL não fornece isolamento agentes para todos os ambientes de nuvem (incluindo o Azure) ou Hyper-V. Consequentemente, o fornecedor do cluster não oferece suporte para clusters de produção em execução nesses ambientes. Estamos trabalhando em uma solução para essa lacuna que estarão disponível em versões futuras.

## <a name="set-cluster-property-cluster-recheck-interval"></a>Definir propriedade de cluster cluster-verificar novamente-intervalo

`cluster-recheck-interval` indica o intervalo de sondagem em que o cluster verifica para alterações nos parâmetros de recursos, restrições ou outras opções de cluster. Se uma réplica ficar inativo, o cluster tenta reiniciar a réplica em um intervalo que é associado pela `failure-timeout` valor e o `cluster-recheck-interval` valor. Por exemplo, se `failure-timeout` é definido como 60 segundos e `cluster-recheck-interval` é definido como 120 segundos, a reinicialização é tentada em um intervalo que é maior que 60 segundos e menos de 120 segundos. É recomendável que você defina o tempo limite de falha como 60 e cluster-verificar novamente intervalo como um valor maior que 60 segundos. Não é recomendável definir o intervalo de nova verificação de cluster para um valor pequeno.

Para atualizar o valor da propriedade `2 minutes` executar:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Todas as distribuições (incluindo RHEL 7.3 e 7.4) que usam o mais recente disponível Pacemaker pacote 1.1.18-11.el7 introduzem uma alteração de comportamento para a configuração de cluster inicial falha-for-fatal quando seu valor é false. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária sofrer uma interrupção, o cluster é esperado para o failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários perceberão que o cluster continua tentando iniciar a réplica primária com falha. Se esse principal nunca ficar online (devido a uma interrupção permanente), o cluster será nunca fará failover para outra réplica secundária disponível. Por causa dessa alteração, uma configuração recomendada anteriormente para definir o início falha-for-fatal não é mais válida e a configuração precisa ser revertido para seu valor padrão de `true`. Além disso, o recurso AG precisa ser atualizado para incluir o `failover-timeout` propriedade. 

Para atualizar o valor da propriedade `true` executar:

```bash
sudo pcs property set start-failure-is-fatal=true
```

Para atualizar o `ag1` propriedade de recurso `failure-timeout` para `60s` executar:

```bash
pcs resource update ag1 meta failure-timeout=60s
```


Para obter informações sobre as propriedades de cluster do Pacemaker, consulte [propriedades de Clusters do Pacemaker](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Crie um logon do SQL Server para Pacemaker

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar recurso de grupo de disponibilidade

Para criar o recurso de grupo de disponibilidade, use `pcs resource create` de comando e defina as propriedades do recurso. O comando a seguir cria um `ocf:mssql:ag` primário/secundário de recursos para o grupo de disponibilidade com o nome `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=30s master notify=true
``` 

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Criar recurso de IP virtual

Para criar o recurso de endereço IP virtual, execute o seguinte comando em um nó. Use um endereço IP estático disponível da rede. Substitua o endereço IP entre `<10.128.16.240>` com um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Não há nenhum nome de servidor virtual equivalente no Pacemaker. Para usar uma cadeia de caracteres de conexão que aponta para um nome de servidor de cadeia de caracteres em vez de um endereço IP, registre o endereço do recurso IP virtual e o nome do servidor virtual desejado no DNS. Para configurações de recuperação de desastres, registre o nome do servidor virtual desejada e o endereço IP com os servidores DNS no primário e site de recuperação de Desastre.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocação

Quase todas as decisões em um cluster Pacemaker, como escolher onde um recurso deve ser executado, é feita comparando as pontuações. As pontuações são calculadas por recurso. O Gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um determinado recurso. Se um nó tiver uma pontuação negativa para um recurso, o recurso não pode ser executado nesse nó.

Em um cluster pacemaker, você pode manipular as decisões do cluster com as restrições. Restrições têm uma pontuação. Se uma restrição tiver uma pontuação inferior a `INFINITY`, Pacemaker considera a ele como recomendação. Uma pontuação de `INFINITY` é obrigatório.

Para garantir que a réplica primária e os recursos de ip virtual executam no mesmo host, defina uma restrição de colocação, com uma pontuação de infinito. Para adicionar a restrição de colocação, execute o seguinte comando em um nó.

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

## <a name="add-ordering-constraint"></a>Adicionar restrição de ordenação

A restrição de colocação possui uma restrição de ordenação implícita. Ele move o recurso IP virtual antes de mover o recurso de grupo de disponibilidade. Por padrão, a sequência de eventos é:

1. Problemas do usuário `pcs resource move` ao grupo de disponibilidade primário do Nó1 para o node2.
1. Interrompe o recurso IP virtual no nó 1.
1. O recurso IP virtual é iniciado no nó 2.
  
   >[!NOTE]
   >Neste ponto, o endereço IP temporariamente aponta para o nó 2 enquanto o nó 2 ainda é um pré-failover secundário. 
   
1. O grupo de disponibilidade primário no nó 1 é rebaixado para secundária.
1. O grupo de disponibilidade secundário no nó 2 é promovido a primária. 

Para impedir que o endereço IP temporariamente apontando para o nó com o secundário antes do failover, adicione uma restrição de ordenação. 

Para adicionar uma restrição de ordenação, execute o seguinte comando em um nó:

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

>[!IMPORTANT]
>Depois de configurar o cluster e adicione o grupo de disponibilidade como um recurso de cluster, você não pode usar o Transact-SQL para fazer failover os recursos do grupo de disponibilidade. Recursos de cluster do SQL Server no Linux não estão acoplados como intimamente com o sistema operacional enquanto estiverem em um Windows Server Failover Cluster (WSFC). Serviço do SQL Server não está ciente da presença do cluster. Orquestração de todos os é feita por meio das ferramentas de gerenciamento de cluster. No Ubuntu ou RHEL, use `pcs` e em uso do SLES `crm` ferramentas. 

Failover manual do grupo de disponibilidade com `pcs`. Não inicie o failover com o Transact-SQL. Para obter instruções, consulte [Failover](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Próximas etapas

[Operar o grupo de disponibilidade de alta disponibilidade](sql-server-linux-availability-group-failover-ha.md)
