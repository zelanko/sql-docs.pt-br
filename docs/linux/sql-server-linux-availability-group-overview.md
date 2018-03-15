---
title: Sempre em grupos de disponibilidade para o SQL Server no Linux | Microsoft Docs
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 54fec5a177d5edf463853d230a56c28eeb1b0f7c
ms.sourcegitcommit: 6b1618aa3b24bf6759b00a820e09c52c4996ca10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2018
---
# <a name="always-on-availability-groups-on-linux"></a>Sempre em grupos de disponibilidade no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve as características dos grupos de disponibilidade AlwaysOn (grupos de disponibilidade) em baseados em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalações. Ele também aborda as diferenças entre o cluster de failover do Windows Server (WSFC) e Linux-com base em grupos de disponibilidade. Consulte o [documentação baseados em Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) para as Noções básicas de grupos de disponibilidade, como eles funcionam da mesma no Windows e Linux, exceto o WSFC.

Do ponto de vista de alto nível, grupos de disponibilidade sob [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux são os mesmos em implementações de WSFC. Isso significa que todos os recursos e limitações são os mesmos, com algumas exceções. As principais diferenças incluem:

-   Não há suporte para o coordenador de transações distribuídas (DTC) da Microsoft em Linux em [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se os aplicativos exigem o uso de transações distribuídas e precisam de um grupo de disponibilidade, implante [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Windows.
-   Implantações baseadas em Linux usam Pacemaker em vez de um WSFC.
-   Ao contrário da maioria das configurações para grupos de disponibilidade no Windows, exceto o cenário de Cluster do grupo de trabalho, Pacemaker nunca requer os serviços de domínio Active Directory (AD DS).
-   Como a falha de um grupo de disponibilidade de um nó para outro é diferente entre o Linux e Windows.
-   Algumas configurações, como `required_synchronized_secondaries_to_commit` só pode ser alterado por meio de Pacemaker no Linux, enquanto uma instalação com base no WSFC usa Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Número de réplicas e os nós de cluster

Um grupo de disponibilidade em [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] pode ter duas réplicas total: um primário e um secundário que pode ser usado apenas para fins de disponibilidade. Ele não pode ser usado para qualquer outra coisa, como consultas legíveis. Um grupo de disponibilidade em [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] pode ter até nove réplicas total: uma primária e até oito secundários, das quais até três (inclusive o primário) podem ser síncrona. Se usar um cluster subjacente, pode haver um máximo de 16 nós total quando Corosync estiver envolvido. Um grupo de disponibilidade pode incluir no máximo nove de 16 nós com [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]e duas com [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Uma configuração de duas réplicas que requer a capacidade de failover automaticamente para outra réplica requer o uso de uma réplica somente para configuração, conforme descrito em [quorum e réplica somente configuração](#configuration-only-replica-and-quorum). Réplicas de configuração foram introduzidas no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] atualização cumulativa 1 (CU1), que deve ser a versão mínima implantada para essa configuração.

Se Pacemaker for usado, ele deve ser configurado corretamente para que ele permaneça em execução. Isso significa que quorum e STONITH devem ser implementado corretamente da perspectiva Pacemaker, além de qualquer [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requisitos como uma réplica somente para configuração.

Somente há suporte para réplicas secundárias legíveis com [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Modo de failover e o tipo de cluster

Novo para [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é a introdução de um tipo de cluster para grupos de disponibilidade. Para o Linux, há dois valores válidos: externo e None. Um tipo de cluster de externos significa que será usada Pacemaker sob o grupo de disponibilidade. Usando externo para o tipo de cluster exige que o modo de failover seja definida como externo também (também novo no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Há suporte para failover automático, mas ao contrário de um WSFC, o modo de failover é definido como externo, não é automático, quando Pacemaker é usado. Ao contrário de um WSFC, a parte Pacemaker do AG é criada depois que o grupo de disponibilidade está configurado.

Um tipo de cluster de None significa que não há nenhum requisito para, nem o grupo de disponibilidade usará, Pacemaker. Mesmo em servidores que têm Pacemaker configurado, se um grupo de disponibilidade for configurado com um tipo de cluster de None, Pacemaker será não consulte ou gerenciar esse grupo de disponibilidade. Um tipo de cluster de None só dá suporte a failover manual de um primário para uma réplica secundária. Um grupo de disponibilidade criado com nenhum se destina, principalmente para a leitura de expansão cenário, bem como atualizações. Enquanto ele pode funcionar em cenários como recuperação de desastres ou disponibilidade local em que nenhum failover automático é necessário, não é recomendável. A história do ouvinte também é mais complexa sem Pacemaker.

Tipo de cluster é armazenado na [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] exibição de gerenciamento dinâmico (DMV) `sys.availability_groups`, nas colunas `cluster_type` e `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>necessário\_sincronizados\_secundários\_para\_confirmação

Novo para [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é uma configuração que é usada por grupos de disponibilidade chamados `required_synchronized_secondaries_to_commit`. Isso informa o grupo de disponibilidade, o número de réplicas secundárias que devem ser em sincronia com o primário. Isso permite que itens como o failover automático (somente quando integrado ao Pacemaker com um tipo de cluster de externos) e controla o comportamento de coisas como a disponibilidade da réplica primária se o número correto de réplicas secundárias estiver online ou offline. Para saber mais sobre como isso funciona, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). O `required_synchronized_secondaries_to_commit` valor é definido por padrão e mantido pelo Pacemaker /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Manualmente, você pode substituir esse valor.

A combinação de `required_synchronized_secondaries_to_commit` e o novo número de sequência (que é armazenado em `sys.availability_groups`) informa Pacemaker e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que, por exemplo, o failover automático poderá ocorrer. Nesse caso, uma réplica secundária teria o mesmo número de sequência do primário, que significa que é atualizado com as últimas informações de configuração.

Há três valores que podem ser definidos para `required_synchronized_secondaries_to_commit`: 0, 1 ou 2. Eles controlam o comportamento do que acontece quando uma réplica se tornar indisponível. Os números correspondem ao número de réplicas secundárias que devem ser sincronizados com o primário. O comportamento é o seguinte no Linux:

-   0 – sem failover automático será possível porque nenhuma réplica secundária é necessária para ser sincronizada. O banco de dados primário está disponível em todos os momentos.
-   1 – uma réplica secundária deve estar em um estado sincronizado com o primário; é possível o failover automático. O banco de dados primário não está disponível até que uma réplica de síncrona secundária está disponível.
-   2 – ambas as réplicas secundárias em uma configuração de AG três ou mais nós devem ser sincronizadas com o primário; é possível o failover automático.

`required_synchronized_secondaries_to_commit` Controla não apenas o comportamento de failover com réplicas síncronas, mas a perda de dados. Com um valor de 1 ou 2, uma réplica secundária sempre é necessária para ser sincronizada, que sempre será a redundância de dados. Isso significa que nenhuma perda de dados.

Para alterar o valor de `required_synchronized_secondaries_to_commit`, use a seguinte sintaxe:

>[!NOTE]
>A alteração do valor faz com que o recurso de reinicialização, que significa que uma breve interrupção. A única maneira de evitar isso é definir o recurso a não ser gerenciado pelo cluster temporariamente.

**Red Hat Enterprise Linux (RHEL) e Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

onde *AGResourceName* é o nome do recurso configurado para o grupo de disponibilidade e *valor* é 0, 1 ou 2. Para defini-lo para o valor padrão de Pacemaker Gerenciando o parâmetro, execute a instrução mesmo sem nenhum valor.

Failover automático de um grupo de disponibilidade é possível quando as seguintes condições forem atendidas:

-   O principal e a réplica secundária são definidos como a movimentação de dados síncrono.
-   O secundário tem um estado de sincronização (não Sincronizando), que significa que as duas estejam no mesmo ponto de dados.
-   O tipo de cluster é definido como externo. Failover automático não é possível com um tipo de cluster de None.
-   O `sequence_number` da réplica secundária se torne o primário tem o maior número de sequência – em outras palavras, a réplica secundária `sequence_number` corresponde da réplica primária original.

Se essas condições forem atendidas e o servidor que hospeda a réplica primária falha, o grupo de disponibilidade irá alterar a propriedade a uma réplica de síncrona. O comportamento de réplicas síncronas (do qual pode haver três total: uma primária e duas réplicas secundárias) adicional pode ser controlado por `required_synchronized_secondaries_to_commit`. Isso funciona com grupos de disponibilidade no Windows e Linux, mas será configurado completamente diferente. No Linux, o valor é configurado automaticamente pelo cluster no próprio recurso AG.

## <a name="configuration-only-replica-and-quorum"></a>Quorum e réplica somente configuração

Também novo no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] a partir de CU1 é uma réplica somente para configuração. Como Pacemaker é diferente de um WSFC, especialmente quando se trata de quorum e exigindo STONITH, ter apenas uma configuração de dois nós não funcionará quando se trata de um grupo de disponibilidade. Para uma FCI, os mecanismos de quorum fornecidos pelo Pacemaker podem ser bem, porque todos os arbitragem de failover FCI ocorre na camada do cluster. Para um grupo de disponibilidade, arbitragem em Linux ocorre em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], onde todos os metadados são armazenados. Isso é que a réplica somente configuração entra em cena.

Sem qualquer outra coisa, um terceiro nó e pelo menos uma réplica sincronizada seria necessárias. Isso não funcionaria para [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)], pois ele pode ter apenas duas réplicas que participa de um grupo de disponibilidade. A réplica somente configuração armazena a configuração do grupo de disponibilidade no banco de dados mestre, mesmo que outras réplicas na configuração do grupo de disponibilidade. A réplica somente configuração não tem os bancos de dados de usuário participam do grupo de disponibilidade. Os dados de configuração são enviados de forma síncrona do primário. Esses dados de configuração, em seguida, são usados durante failovers, independentemente de estarem automática ou manual.

Para um grupo de disponibilidade manter o quorum e habilitar failovers automáticos com um tipo de cluster de externo, ele o deverá:

-   Ter três réplicas síncronas ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] somente); ou
-   Ter duas réplicas (primárias e secundárias), bem como uma única réplica de configuração.

Failovers manuais pode acontecer se externo está em uso ou nenhum tipos para configurações de grupo de disponibilidade do cluster. Enquanto uma réplica somente configuração pode ser configurada com um grupo de disponibilidade que tem um tipo de cluster de None, não convém, pois ele complica a implantação. Para essas configurações, modifique manualmente `required_synchronized_secondaries_to_commit` tenha um valor pelo menos 1, para que haja pelo menos uma réplica sincronizada.

Uma réplica somente configuração pode ser hospedada em qualquer edição do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], incluindo [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Isso reduzirá os custos de licenciamento e garante que ele funciona com grupos de disponibilidade em [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Isso significa que a terceira necessárias server só precisa atender as especificações mínimas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], pois ele não está recebendo tráfego de transação do usuário para o grupo de disponibilidade.

Quando uma réplica somente configuração é usada, ela tem o seguinte comportamento:

-   Por padrão, `required_synchronized_secondaries_to_commit` é definido como 0. Isso pode ser modificado manualmente para 1 se desejado.
-   Se o principal falhar e `required_synchronized_secondaries_to_commit` for 0, a réplica secundária se tornará o novo primário e estar disponível para leitura e gravação. Se o valor for 1, ocorrerá failover automático, mas não aceitará novas transações até que outra réplica está online.
-   Se uma réplica secundária falhar e `required_synchronized_secondaries_to_commit` é 0, a réplica primária ainda aceita transações, mas se o principal falhar neste momento, não há nenhuma proteção de dados nem de failover possíveis (manual ou automático), já que uma réplica secundária não está disponível.
-   Se as réplicas somente configuração falhar, o grupo de disponibilidade funcionará normalmente, mas sem failover automático será possível.
-   Se uma réplica secundária síncrona e a réplica somente configuração falharem, o primário não pode aceitar transações, e não têm para o primário falhar ao.

CU1 há um bug conhecido no log no arquivo corosync.log que é gerado por meio de `mssql-server-ha`. Se uma réplica secundária não é capaz de se tornar primário devido ao número de réplicas necessários disponíveis, a mensagem atual diz "esperados para receber os números de sequência de 1, mas recebeu apenas 2. Não há réplicas estão on-line com segurança promover a réplica local." Os números devem ser revertidos, e ele deve indicar "esperados para receber 2 números de sequência, mas recebeu apenas 1. Não há réplicas estão on-line com segurança promover a réplica local." 

## <a name="multiple-availability-groups"></a>Vários grupos de disponibilidade 

Mais de um grupo de disponibilidade pode ser criado por cluster Pacemaker ou conjunto de servidores. A única limitação é que os recursos do sistema. Propriedade AG é mostrada pelo mestre. Grupos de disponibilidade diferentes podem ser possuídos por nós diferentes; nem todos precisam estar em execução no mesmo nó.

## <a name="drive-and-folder-location-for-databases"></a>Unidade e uma pasta local para bancos de dados

Como em grupos de disponibilidade com base em Windows, a estrutura de unidade e a pasta para os bancos de dados de usuário participando de um grupo de disponibilidade deve ser idêntica. Por exemplo, se os bancos de dados do usuário estão em `/var/opt/mssql/userdata` no servidor A, essa mesma pasta deve existir no servidor B. A única exceção a isso é observada na seção [interoperabilidade com grupos de disponibilidade com base em Windows e réplicas](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>O ouvinte no Linux

O ouvinte é funcionalidade opcional para um grupo de disponibilidade. Ele fornece um único ponto de entrada para todas as conexões (leitura/gravação para a réplica primária e/ou réplicas somente leitura para o secundário) para que os aplicativos e usuários finais não precisa saber qual servidor está hospedando os dados. Em um WSFC, essa é a combinação de um recurso de nome de rede e um recurso IP, que é registrado no AD DS (se necessário), bem como o DNS. Em combinação com o próprio recurso de grupo de disponibilidade, ele fornece essa abstração. Para obter mais informações sobre um ouvinte, consulte [ouvintes, conectividade de cliente e Failover de aplicativo](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

O ouvinte no Linux está configurado de forma diferente, mas sua funcionalidade é o mesmo. Não há nenhum conceito de um recurso de nome de rede no Pacemaker, nem é um objeto criado no AD DS; Há apenas um recurso de endereço IP criado no Pacemaker que pode ser executados em qualquer um de nós. Uma entrada associada ao recurso IP do ouvinte no DNS com um "nome amigável" precisa ser criado. O recurso IP para o ouvinte só ficará ativo no servidor que hospeda a réplica primária para o grupo de disponibilidade.

Se Pacemaker for usada e um recurso de endereço IP é criado que está associado com o ouvinte, haverá uma breve interrupção como o endereço IP para em um servidor e inicia em outro, se ele é o failover automático ou manual. Enquanto isso fornece a abstração pela combinação de um único nome e endereço IP, ele não mascara a interrupção. Um aplicativo deve ser capaz de lidar com a desconexão por ter algum tipo de funcionalidade para detectar isso e reconectar-se.

No entanto, a combinação do nome DNS e endereço IP é ainda não o suficiente para fornecer todas as funcionalidades que fornece um ouvinte em um WSFC, como roteamento somente leitura para réplicas secundárias. Ao configurar um grupo de disponibilidade, um "ouvinte" ainda precisa ser configurado em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Isso pode ser visto no assistente, bem como a sintaxe Transact-SQL. Há duas maneiras que isso pode ser configurado para funcionar da mesma maneira como no Windows:

-   Para um grupo de disponibilidade com um tipo de cluster de externo, o endereço IP associado "escuta" criada no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve ser o endereço IP do recurso criado no Pacemaker.
-   Para um grupo de disponibilidade criado com um tipo de cluster de None, use o endereço IP associado com a réplica primária.

A instância associada com o endereço IP fornecido, em seguida, torna-se o coordenador de coisas como solicitações de roteamento somente leitura de aplicativos.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilidade com grupos de disponibilidade com base em Windows e réplicas 

Um grupo de disponibilidade que tem um tipo de cluster de externo ou um que seja WSFC não pode ter suas réplicas cruzada plataformas. Isso é verdadeiro se o grupo de disponibilidade é [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] ou [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Isso significa que em uma configuração de grupo de disponibilidade tradicional com um cluster subjacente, uma réplica não pode ser um WSFC e a outra no Linux com Pacemaker.

Um grupo de disponibilidade com um tipo de cluster de NONE pode ter suas réplicas ultrapassar os limites do sistema operacional, portanto poderá haver ambas as réplicas com base em Linux e Windows o mesmo grupo de disponibilidade. Um exemplo é mostrado aqui onde a réplica primária é baseado no Windows, enquanto o secundário está em um das distribuições do Linux.

![Híbrido None](./media/sql-server-linux-availability-group-overview/image1.png)

Um grupo de disponibilidade distribuído também pode atravessar limites de sistema operacional. Os grupos de disponibilidade subjacentes são associados pelas regras de como eles são configurados, como aquele configurado com externo que está sendo somente Linux, mas o grupo de disponibilidade que ele é adicionado ao pode ser configurado com um WSFC. Considere o seguinte exemplo:

![Híbrido Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Próximas etapas
[Configurar o grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md)

[Adicionar grupo de disponibilidade do recurso de Cluster em RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Adicionar grupo de disponibilidade do recurso de Cluster em SLES](sql-server-linux-availability-group-cluster-sles.md)

[Adicionar grupo de disponibilidade do recurso de Cluster no Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurar um grupo de disponibilidade da plataforma cruzada](sql-server-linux-availability-group-cross-platform.md)

