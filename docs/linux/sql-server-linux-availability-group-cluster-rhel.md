---
title: 'RHEL: Configurar um grupo de disponibilidade para o SQL Server em Linux'
description: Saiba como configurar um grupo de disponibilidade ao executar o RHEL (Red Hat Enterprise Linux) para SQL Server.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 01/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: b7102919-878b-4c08-a8c3-8500b7b42397
ms.openlocfilehash: bf888d42215f3a4ee7c44b782b82c55f85afa041
ms.sourcegitcommit: 21e6a0c1c6152e625712a5904fce29effb08a2f9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2020
ms.locfileid: "75884034"
---
# <a name="configure-rhel-cluster-for-sql-server-availability-group"></a>Configurar o cluster do RHEL para o Grupo de Disponibilidade do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento explica como criar um cluster do grupo de disponibilidade de três nós para o SQL Server no Red Hat Enterprise Linux. Para alta disponibilidade, um grupo de disponibilidade em Linux exige três nós – consulte [Alta disponibilidade e proteção de dados para configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). A camada de clustering baseia-se no [complemento de HA](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/pdf/High_Availability_Add-On_Overview/Red_Hat_Enterprise_Linux-6-High_Availability_Add-On_Overview-en-US.pdf) do RHEL (Red Hat Enterprise Linux) criado com base no [Pacemaker](https://clusterlabs.org/). 

> [!NOTE] 
> O acesso à documentação completa do Red Hat exige uma assinatura válida. 

Para saber mais sobre configuração de cluster, opções de agentes de recursos e gerenciamento, acesse a [Documentação de referência do RHEL](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/index.html).

> [!NOTE] 
> O SQL Server não é tão totalmente integrado ao Pacemaker no Linux quanto ao clustering de failover do Windows Server. Uma instância do SQL Server não reconhece o cluster. O Pacemaker fornece orquestração de recursos de cluster. Além disso, o nome da rede virtual é específico do clustering de failover do Windows Server – não há um equivalente no Pacemaker. As DMVs (exibições de gerenciamento dinâmico) do grupo de disponibilidade que consultam as informações do cluster retornam linhas vazias em clusters do Pacemaker. Para criar um ouvinte de reconexão transparente após o failover, registre manualmente o nome do ouvinte em DNS com o IP usado para criar o recurso de IP virtual. 

As seções a seguir percorrem as etapas para configurar um cluster do Pacemaker e adicionar um grupo de disponibilidade como recurso no cluster para alta disponibilidade.

## <a name="roadmap"></a>Roteiro

As etapas para criar um grupo de disponibilidade em servidores Linux para alta disponibilidade são diferentes das etapas em um cluster de failover do Windows Server. A lista a seguir descreve as etapas de alto nível: 

1. [Configurar o SQL Server nos nós de cluster](sql-server-linux-setup.md).

2. [Criar o grupo de disponibilidade](sql-server-linux-availability-group-configure-ha.md). 

3. Configurar um gerenciador de recursos de cluster, como o Pacemaker. Estas instruções são descritas neste documento.
   
   A maneira de configurar um gerenciador de recursos de cluster depende da distribuição específica do Linux. 

   >[!IMPORTANT]
   >Os ambientes de produção exigem um agente de isolamento, como o STONITH para alta disponibilidade. As demonstrações desta documentação não usam agentes de isolamento. As demonstrações se destinam apenas a teste e validação.
   
   >Um cluster do Linux usa o isolamento para retornar o cluster a um estado conhecido. A maneira de configurar o isolamento depende da distribuição e do ambiente. Atualmente, o isolamento não está disponível em alguns ambientes de nuvem. Para saber mais, confira [Políticas de suporte para clusters de alta disponibilidade do RHEL – plataformas de virtualização](https://access.redhat.com/articles/29440).

5. [Adicione o grupo de disponibilidade como um recurso no cluster](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).  

## <a name="configure-high-availability-for-rhel"></a>Configurar a alta disponibilidade do RHEL

Para configurar a alta disponibilidade do RHEL, habilite a assinatura de alta disponibilidade e configure o Pacemaker.

### <a name="enable-the-high-availability-subscription-for-rhel"></a>Habilitar a assinatura de alta disponibilidade para RHEL

Cada nó no cluster deve ter uma assinatura apropriada para RHEL e o complemento de alta disponibilidade. Examine os requisitos em [Como instalar pacotes de cluster de alta disponibilidade no Red Hat Enterprise Linux](https://access.redhat.com/solutions/45930). Siga estas etapas para configurar a assinatura e repositórios:

1. Registre o sistema.

   ```bash
   sudo subscription-manager register
   ```

   Forneça seu nome de usuário e senha.   

1. Liste os pools disponíveis para registro.

   ```bash
   sudo subscription-manager list --available
   ```

   Na lista de pools disponíveis, observe a ID do pool para a assinatura de alta disponibilidade.

1. Atualize o seguinte script. Substitua `<pool id>` pela ID do pool para alta disponibilidade da etapa anterior. Execute o script para anexar a assinatura.

   ```bash
   sudo subscription-manager attach --pool=<pool id>
   ```

1. Habilite o repositório.

   ```bash
   sudo subscription-manager repos --enable=rhel-ha-for-rhel-7-server-rpms
   ```

Para saber mais, confira [Pacemaker – O cluster de alta disponibilidade e software livre](https://clusterlabs.org/pacemaker/). 

Após configurar a assinatura, conclua as seguintes etapas para configurar o Pacemaker:

### <a name="configure-pacemaker"></a>Configurar o Pacemaker

Após registrar a assinatura, conclua as etapas a seguir para configurar o Pacemaker:
   
[!INCLUDE [RHEL-Configure-Pacemaker](../includes/ss-linux-cluster-pacemaker-configure-rhel.md)]

Após configurar o Pacemaker, use `pcs` para interagir com o cluster. Execute todos os comandos em um nó do cluster. 

## <a name="configure-fencing-stonith"></a>Configurar isolamento (STONITH)

Os fornecedores do cluster do Pacemaker exigem que o STONITH esteja habilitado e que um dispositivo de isolamento esteja definido para uma configuração de cluster com suporte. STONITH significa “acerte o outro nó na cabeça” (“shoot the other node in the head”). Quando o gerenciador de recursos de cluster não puder determinar o estado de um nó ou de um recurso em um nó, o isolamento traz o cluster para um estado conhecido novamente.

Um dispositivo STONITH fornece um agente de isolamento. [Como configurar o Pacemaker no Red Hat Enterprise Linux no Azure](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-pacemaker/#1-create-the-stonith-devices) fornece um exemplo de como criar um dispositivo STONITH para esse cluster no Azure. Modifique as instruções de seu ambiente.

O isolamento de nível de recurso verifica se não há dados corrompidos em caso de interrupção por meio da configuração de um recurso. Por exemplo, você poderá usar o isolamento no nível do recurso para marcar o disco em um nó como desatualizado quando o link de comunicação ficar inativo. 

O isolamento no nível do nó verifica se um nó não executa nenhum recurso. Isso é feito redefinindo o nó. O Pacemaker dá suporte a uma grande variedade de dispositivos de isolamento. Os exemplos incluem no-break ou cartões de interface de gerenciamento para servidores.

Para saber mais sobre o STONITH e o isolamento, configure os artigos a seguir:

* [Clusters do Pacemaker do zero](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/index.html)
* [Isolamento e STONITH](https://clusterlabs.org/doc/crm_fencing.html)
* [Complemento de alta disponibilidade do Red Hat com Pacemaker: isolamento](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-fencing-HAAR.html)

>[!NOTE]
>Como a configuração de isolamento no nível do nó depende muito do seu ambiente, desabilite-a para este tutorial (ela pode ser configurada posteriormente). O script a seguir desabilita o isolamento no nível do nó:
>
>```bash
>sudo pcs property set stonith-enabled=false
>``` 
>
>A desabilitação do STONITH destina-se apenas a fins de teste. Se você pretende usar o Pacemaker em um ambiente de produção, deve planejar uma implementação do STONITH dependendo do ambiente e mantê-lo habilitado.

## <a name="set-cluster-property-cluster-recheck-interval"></a>Defina a propriedade de cluster cluster-recheck-interval

`cluster-recheck-interval` indica o intervalo de sondagem segundo o qual o cluster verifica se há alterações nos parâmetros de recurso, restrições ou outras opções de cluster. Se uma réplica ficar inativa, o cluster tentará reiniciar a réplica em um intervalo associado ao valor `failure-timeout` e ao valor `cluster-recheck-interval`. Por exemplo, se `failure-timeout` for definido como 60 segundos e `cluster-recheck-interval` for definido como 120 segundos, será realizada uma tentativa de reinicialização em um intervalo superior a 60 segundos, mas inferior a 120 segundos. Recomendamos que você defina failure-timeout como 60 segundos e cluster-recheck-interval com um valor superior a 60 segundos. Não é recomendável definir cluster-recheck-interval como um valor pequeno.

Para atualizar o valor da propriedade para `2 minutes`, execute:

```bash
sudo pcs property set cluster-recheck-interval=2min
```

> [!IMPORTANT] 
> Todas as distribuições (incluindo o RHEL 7.3 e 7.4) que usam o pacote mais recente disponível do Pacemaker 1.1.18-11.el7 introduzem uma alteração de comportamento para a configuração de cluster start-failure-is-fatal quando seu valor é falso. Essa alteração afeta o fluxo de trabalho de failover. Se uma réplica primária apresentar uma interrupção, o cluster deverá fazer failover para uma das réplicas secundárias disponíveis. Em vez disso, os usuários observarão que o cluster continua tentando iniciar a réplica primária com falha. Se a primária nunca ficar online (devido a uma interrupção permanente), o cluster nunca fará failover para outra réplica secundária disponível. Devido a essa alteração, a configuração recomendada anteriormente para definir start-failure-is-fatal não é mais válida e a configuração precisa ser revertida de volta para seu valor padrão `true`. Além disso, o recurso do AG precisa ser atualizado para incluir a propriedade `failover-timeout`. 

Para atualizar o valor da propriedade para `true`, execute:

```bash
sudo pcs property set start-failure-is-fatal=true
```

Para atualizar a propriedade `failure-timeout` do recurso `ag_cluster` para `60s`, execute:

```bash
pcs resource update ag_cluster meta failure-timeout=60s
```


Para saber mais sobre as propriedades de cluster do Pacemaker, confira [Propriedades de clusters do Pacemaker](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-clusteropts-HAAR.html).

## <a name="create-a-sql-server-login-for-pacemaker"></a>Criar um logon do SQL Server para o Pacemaker

[!INCLUDE [SQL-Create-SQL-Login](../includes/ss-linux-cluster-pacemaker-create-login.md)]

## <a name="create-availability-group-resource"></a>Criar recurso do grupo de disponibilidade

Para criar o recurso do grupo de disponibilidade, use o comando `pcs resource create` e defina as propriedades do recurso. O comando a seguir cria um recurso do tipo mestre/subordinado `ocf:mssql:ag` para o grupo de disponibilidade com o nome `ag1`.

```bash
sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s master notify=true
```

> [!NOTE]
> Com a disponibilidade do **RHEL 8**, a sintaxe create foi alterada. Se você está usando o **RHEL 8**, a terminologia `master` foi alterada para `promotable`. Use o seguinte comando create em vez do comando acima: `sudo pcs resource create ag_cluster ocf:mssql:ag ag_name=ag1 meta failure-timeout=60s promotable notify=true`

[!INCLUDE [required-synchronized-secondaries-default](../includes/ss-linux-cluster-required-synchronized-secondaries-default.md)]

<a name="createIP"></a>

## <a name="create-virtual-ip-resource"></a>Criar recurso de IP virtual

Para criar o recurso de endereço IP virtual, execute o comando a seguir em um nó. Use um endereço IP estático disponível da rede. Substitua o endereço IP entre `<10.128.16.240>` por um endereço IP válido.

```bash
sudo pcs resource create virtualip ocf:heartbeat:IPaddr2 ip=<10.128.16.240>
```

Não há nome do servidor virtual equivalente no Pacemaker. Para usar uma cadeia de conexão que aponte para um nome do servidor de cadeia de caracteres, em vez de um endereço IP, registre o endereço de recurso do IP virtual e o nome do servidor virtual desejado no DNS. Para configurações de DR, registre o nome do servidor virtual e o endereço IP desejados com os servidores DNS nos sites primário e de DR.

## <a name="add-colocation-constraint"></a>Adicionar restrição de colocalização

Quase todas as decisões em um cluster do Pacemaker, como escolher o local em que um recurso deve ser executado, são feitas pela comparação de pontuações. As pontuações são calculadas por recurso. O gerenciador de recursos de cluster escolhe o nó com a pontuação mais alta para um recurso específico. Se um nó tiver uma pontuação negativa para um recurso, o recurso não poderá ser executado nesse nó.

Em um cluster do Pacemaker, você pode manipular as decisões do cluster com restrições. As restrições têm uma pontuação. Se uma restrição tiver uma pontuação menor que `INFINITY`, o Pacemaker a considerará uma recomendação. A opção de `INFINITY` é obrigatória.

Para verificar se a réplica primária e o recurso de IP virtual são executados no mesmo host, defina uma restrição de colocalização com pontuação igual a INFINITY. Para adicionar a restrição de colocalização, execute o comando a seguir em um nó.

### <a name="rhel-7"></a>RHEL 7

Quando você cria o recurso `ag_cluster` no RHEL 7, ele o cria como `ag_cluster-master`. Use o seguinte comando para o RHEL 7:

```bash
sudo pcs constraint colocation add virtualip ag_cluster-master INFINITY with-rsc-role=Master
```

### <a name="rhel-8"></a>RHEL 8

Quando você cria o recurso `ag_cluster` no RHEL 8, ele o cria como `ag_cluster-clone`. Use o seguinte comando para o RHEL 8:

```bash
sudo pcs constraint colocation add virtualip with master ag_cluster-clone INFINITY with-rsc-role=Master
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

### <a name="rhel-7"></a>RHEL 7

```bash
sudo pcs constraint order promote ag_cluster-master then start virtualip
```

### <a name="rhel-8"></a>RHEL 8

```bash
sudo pcs constraint order promote ag_cluster-clone then start virtualip
```

>[!IMPORTANT]
>Depois de configurar o cluster e adicionar o grupo de disponibilidade como um recurso de cluster, você não poderá usar o Transact-SQL para fazer failover dos recursos de grupo de disponibilidade. Os recursos de cluster do SQL Server em Linux não são acoplados tão firmemente com o sistema operacional como são em um WSFC (cluster de failover do Windows Server). O serviço SQL Server não reconhece a presença do cluster. Toda a orquestração é feita por meio das ferramentas de gerenciamento de cluster. No RHEL ou no Ubuntu, use `pcs` e, no SLES, use as ferramentas `crm`. 

Faça failover manualmente do grupo de disponibilidade com `pcs`. Não inicie o failover com Transact-SQL. Para obter instruções, confira [Failover](sql-server-linux-availability-group-failover-ha.md#failover).

## <a name="next-steps"></a>Próximas etapas

[Operar grupo de disponibilidade de HA](sql-server-linux-availability-group-failover-ha.md)
