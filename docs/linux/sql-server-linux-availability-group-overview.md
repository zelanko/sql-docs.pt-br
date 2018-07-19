---
title: Sempre em grupos de disponibilidade para o SQL Server no Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: 7de4097fdc843097cbd2865e4a4f3986c392ac04
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38045094"
---
# <a name="always-on-availability-groups-on-linux"></a>Sempre em grupos de disponibilidade no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve as características dos grupos de disponibilidade AlwaysOn (grupos de disponibilidade) em baseado em Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalações. Ele também aborda as diferenças entre o cluster de failover do Windows Server (WSFC) e o Linux --com base em grupos de disponibilidade. Consulte a [documentação baseada em Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) para as Noções básicas de grupos de disponibilidade, como eles funcionam da mesma no Windows e Linux, exceto para o WSFC.

Do ponto de vista de alto nível dos grupos de disponibilidade em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux são os mesmos enquanto eles estiverem em implementações baseadas no WSFC. Isso significa que todos os recursos e limitações são os mesmos, com algumas exceções. As principais diferenças incluem:

-   Não há suporte para o Microsoft Distributed Transaction Coordinator (DTC) em Linux no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. Se seus aplicativos exigem o uso de transações distribuídas e precisam de um grupo de disponibilidade, implante [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Windows.
-   Implantações baseadas em Linux usam Pacemaker em vez de um WSFC.
-   Ao contrário da maioria das configurações para grupos de disponibilidade no Windows, exceto para o cenário de Cluster do grupo de trabalho, o Pacemaker nunca requer os serviços de domínio do Active Directory (AD DS).
-   Como fazer um grupo de disponibilidade de um nó para outro é diferente entre o Linux e Windows.
-   Determinadas configurações, como `required_synchronized_secondaries_to_commit` só pode ser alterado por meio do Pacemaker no Linux, enquanto uma instalação com base em WSFC usa Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Número de réplicas e os nós de cluster

Um grupo de disponibilidade no [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] pode ter duas réplicas total: uma primária e uma secundária que pode ser usada apenas para fins de disponibilidade. Ele não pode ser usado para qualquer outra coisa, como consultas legíveis. Um grupo de disponibilidade no [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] pode ter até nove réplicas no total: uma primária e até oito secundários, que até três (incluindo primário) pode ser síncrona. Se usar um cluster subjacente, pode haver um máximo de 16 nós total quando Corosync está envolvido. Um grupo de disponibilidade pode abranger de 16 nós no máximo nove [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]e duas com [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Uma configuração de duas réplicas que requer a capacidade de fazer failover automaticamente para outra réplica requer o uso de uma réplica somente de configuração, conforme descrito em [réplica somente de configuração e o quorum](#configuration-only-replica-and-quorum). Réplicas somente de configuração foram introduzidas no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] atualização cumulativa 1 (CU1), portanto, que deve ser a versão mínima implantada para essa configuração.

Se o Pacemaker é usado, ele deve ser configurado corretamente para que ele permaneça em funcionamento. Isso significa que de quorum e STONITH devem ser implementadas corretamente da perspectiva do Pacemaker, além de quaisquer [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] requisitos como uma réplica somente de configuração.

Somente há suporte para réplicas secundárias legíveis com [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Modo de failover e o tipo de cluster

Novo no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é a introdução de um tipo de cluster para grupos de disponibilidade. Para o Linux, há dois valores válidos: External e None. Um tipo de cluster externo significa que o Pacemaker será usado sob o grupo de disponibilidade. Externo está em uso para o tipo de cluster exige que o modo de failover seja definida como externo também (também nesta nova [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Há suporte para failover automático, mas ao contrário de um WSFC, o modo de failover é definido como externo, não é automático, quando o Pacemaker é usado. Ao contrário de um WSFC, a parte do Pacemaker do AG é criada depois que o grupo de disponibilidade for configurado.

Um tipo de cluster None significa que não há nenhum requisito para, nem o grupo de disponibilidade usará, Pacemaker. Mesmo em servidores que têm o Pacemaker configurado, se um grupo de disponibilidade for configurado com um tipo de cluster nenhum, Pacemaker será veja nem gerenciar esse grupo de disponibilidade. Um tipo de cluster nenhum só dá suporte a failover manual do primário para uma réplica secundária. Um grupo de disponibilidade criado com nenhum é destinado para a escala de leitura-out de cenário, bem como atualizações. Embora ele pode funcionar em cenários como recuperação de desastres ou disponibilidade local em que nenhum failover automático é necessário, ele não é recomendável. A história do ouvinte também é mais complexa sem o Pacemaker.

Tipo de cluster é armazenado na [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] exibição de gerenciamento dinâmico (DMV) `sys.availability_groups`, nas colunas `cluster_type` e `cluster_type_desc`.

## <a name="requiredsynchronizedsecondariestocommit"></a>obrigatório\_sincronizadas\_secundários\_para\_confirmação

Novo no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é uma configuração que é usada por grupos de disponibilidade chamados `required_synchronized_secondaries_to_commit`. Isso informa o grupo de disponibilidade, o número de réplicas secundárias que devem estar em sincronia com o primário. Isso permite que os itens como failover automático (somente quando integrado ao Pacemaker com um tipo de cluster externo) e controla o comportamento de coisas como a disponibilidade da réplica primária se o número correto de réplicas secundárias estiver online ou offline. Para saber mais sobre como isso funciona, consulte [alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade](sql-server-linux-availability-group-ha.md). O `required_synchronized_secondaries_to_commit` valor é definido por padrão e mantido pelo Pacemaker /[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Você pode substituir esse valor manualmente.

A combinação de `required_synchronized_secondaries_to_commit` e o novo número de sequência (que é armazenado no `sys.availability_groups`) informa ao Pacemaker e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que, por exemplo, o failover automático pode acontecer. Nesse caso, uma réplica secundária teria o mesmo número de sequência que o primário, que significa que é atualizado com as últimas informações de configuração.

Há três valores que podem ser definidas para `required_synchronized_secondaries_to_commit`: 0, 1 ou 2. Eles controlam o comportamento do que acontece quando uma réplica se tornar indisponível. Os números correspondem ao número de réplicas secundárias que devem ser sincronizados com o primário. O comportamento é o seguinte no Linux:

-   0 – nenhum failover automático é possível, pois nenhuma réplica secundária é necessária a serem sincronizados. O banco de dados primário está disponível em todos os momentos.
-   1 – uma réplica secundária deve ser em um estado sincronizado com o primário; failover automático será possível. O banco de dados primário não está disponível até que uma réplica síncrona secundária está disponível.
-   2 – ambas as réplicas secundárias em uma configuração de AG três ou mais nós devem ser sincronizadas com o primário; failover automático será possível.

`required_synchronized_secondaries_to_commit` Controla não apenas o comportamento de failover com réplicas síncronas, mas a perda de dados. Com um valor de 1 ou 2, uma réplica secundária sempre é necessária para a sincronização, portanto, sempre haverá redundância de dados. Isso significa que nenhuma perda de dados.

Para alterar o valor de `required_synchronized_secondaries_to_commit`, use a seguinte sintaxe:

>[!NOTE]
>Alterando o valor faz com que o recurso seja reiniciado, ou seja, uma breve interrupção. A única maneira de evitar isso é definir o recurso a não ser gerenciado pelo cluster temporariamente.

**Red Hat Enterprise Linux (RHEL) e Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

em que *AGResourceName* é o nome do recurso configurado para o grupo de disponibilidade, e *valor* é 0, 1 ou 2. Para configurá-lo para o padrão do Pacemaker Gerenciando o parâmetro, execute a instrução mesma sem nenhum valor.

Failover automático de um grupo de disponibilidade é possível quando as seguintes condições forem atendidas:

-   A réplica primária e secundária são definidos como a movimentação de dados síncrona.
-   O secundário tem um estado de sincronizados (não Sincronizando), o que significa que os dois estão no mesmo ponto de dados.
-   O tipo de cluster é definido como externo. Failover automático não é possível com um tipo de cluster nenhum.
-   O `sequence_number` da réplica secundária se torne o primário tem o maior número de sequência – em outras palavras, a réplica secundária `sequence_number` corresponde da réplica primária original.

Se essas condições forem atendidas e o servidor que hospeda a réplica primária falhar, o grupo de disponibilidade terão sua propriedade alterada para uma réplica síncrona. O comportamento de réplicas síncronas (do qual pode haver três total: uma primária e duas réplicas secundárias) pode ser ainda mais controlado por `required_synchronized_secondaries_to_commit`. Isso funciona com grupos de disponibilidade no Windows e Linux, mas é configurado de forma completamente diferente. No Linux, o valor é configurado automaticamente pelo cluster no próprio recurso de grupo de disponibilidade.

## <a name="configuration-only-replica-and-quorum"></a>Quorum e a réplica somente de configuração

Também nesta nova [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] a partir da atualização cumulativa 1 para é uma réplica somente de configuração. Como o Pacemaker é diferente de um WSFC, especialmente quando se trata de quorum e exigindo o STONITH, ter apenas uma configuração de dois nós não funcionará quando se trata de um grupo de disponibilidade. Para uma FCI, os mecanismos de quorum fornecidos pelo Pacemaker podem ser muito bem, porque todos os arbitragem de failover FCI ocorre na camada do cluster. Para um grupo de disponibilidade, arbitragem no Linux acontece em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], onde todos os metadados são armazenados. Isso é que a réplica somente configuração entra em cena.

Sem qualquer outra coisa, um terceiro nó e pelo menos uma réplica sincronizada seria necessárias. Isso não funcionaria para [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)], já que ele só pode ter duas réplicas que participam de um grupo de disponibilidade. A réplica somente configuração armazena a configuração do grupo de disponibilidade no banco de dados mestre, mesmo que outras réplicas na configuração do grupo de disponibilidade. A réplica somente configuração não tem os bancos de dados de usuário participam do AG. Os dados de configuração são enviados de forma síncrona do primário. Esses dados de configuração, em seguida, são usados durante failovers, independentemente de estarem automática ou manual.

Para um grupo de disponibilidade manter o quorum e habilitar failovers automáticos com um tipo de cluster externo, ele o deverá:

-   Tem três réplicas síncronas ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] somente); ou
-   Ter duas réplicas (primárias e secundárias), bem como uma réplica somente de configuração.

Failovers manuais pode acontecer se o externo está em uso ou None tipos para as configurações do grupo de disponibilidade do cluster. Enquanto uma réplica somente configuração pode ser configurada com um grupo de disponibilidade que tem um tipo de cluster nenhum, não é recomendável, pois ele complica a implantação. Para essas configurações, modifique manualmente `required_synchronized_secondaries_to_commit` para ter um valor pelo menos 1, para que haja pelo menos uma réplica sincronizada.

Uma réplica somente configuração pode ser hospedada em qualquer edição do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], incluindo [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Isso reduzirá os custos de licenciamento e garante que ele funciona com grupos de disponibilidade em [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Isso significa que o terceiro necessário servidor apenas precisa atender as especificações mínimas para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], já que ele não está recebendo o tráfego de transação do usuário para o grupo de disponibilidade.

Quando uma réplica somente configuração é usada, ela tem o seguinte comportamento:

-   Por padrão, `required_synchronized_secondaries_to_commit` é definido como 0. Isso pode ser modificado manualmente como 1 se desejado.
-   Se o principal falhar e `required_synchronized_secondaries_to_commit` for 0, a réplica secundária se tornará o novo primário e estar disponível para leitura e gravação. Se o valor for 1, ocorrerá o failover automático, mas não aceitará novas transações até que a outra réplica está online.
-   Se uma réplica secundária falhar e `required_synchronized_secondaries_to_commit` é 0, a réplica primária ainda aceita transações, mas se o primário falhar nesse ponto, não há nenhuma proteção para os dados nem possíveis de failover (manual ou automático), uma vez que uma réplica secundária não está disponível.
-   Se as réplicas somente de configuração falhar, o grupo de disponibilidade funcionarão normalmente, mas sem failover automático será possível.
-   Se uma réplica secundária síncrona e a réplica somente configuração falharem, o primário não pode aceitar as transações, e há um lugar para o primário falhe ao.

Na atualização cumulativa 1 para há um bug conhecido no registro em log no arquivo corosync.log que é gerado por meio de `mssql-server-ha`. Se uma réplica secundária não for capaz de se tornar o primário devido ao número de réplicas necessárias disponíveis, a mensagem atual diz "deve receber números de sequência 1 mas recebidas apenas 2. Não há réplicas estão online com segurança, promover a réplica local." Os números devem ser revertidos e deverá indicar "deve receber números de sequência de 2, mas recebeu apenas 1. Não há réplicas estão online com segurança, promover a réplica local." 

## <a name="multiple-availability-groups"></a>Vários grupos de disponibilidade 

Mais de um grupo de disponibilidade pode ser criado por cluster Pacemaker ou conjunto de servidores. A única limitação é que os recursos do sistema. Propriedade do grupo de disponibilidade é mostrada pelo mestre. Grupos de disponibilidade diferentes podem ser possuídos por nós diferentes; nem todos precisam estar em execução no mesmo nó.

## <a name="drive-and-folder-location-for-databases"></a>Unidade e a pasta local para bancos de dados

Como em grupos de disponibilidade com base em Windows, a estrutura de unidade e a pasta para os bancos de dados de usuário participam de um grupo de disponibilidade deve ser idêntica. Por exemplo, se os bancos de dados do usuário estão em `/var/opt/mssql/userdata` no servidor A, a mesma pasta deve existir no servidor B. A única exceção a isso é observada na seção [interoperabilidade com grupos de disponibilidade com base no Windows e réplicas](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>O ouvinte no Linux

O ouvinte é uma funcionalidade opcional para um grupo de disponibilidade. Ele fornece um único ponto de entrada para todas as conexões (leitura/gravação para a réplica primária e/ou réplicas somente leitura para o secundário) para que os aplicativos e usuários finais não precisam saber qual servidor está hospedando os dados. Em um WSFC, isso é a combinação de um recurso de nome de rede e um recurso IP, que, em seguida, é registrado no AD DS (se necessário), bem como o DNS. Em combinação com o recurso de grupo de disponibilidade em si, ele fornece essa abstração. Para obter mais informações sobre um ouvinte, consulte [ouvintes, conectividade de cliente e Failover de aplicativo](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

O ouvinte no Linux é configurado de forma diferente, mas sua funcionalidade é o mesmo. Não há nenhum conceito de um recurso de nome de rede no Pacemaker, nem é um objeto criado no AD DS; Há apenas um recurso de endereço IP criado no Pacemaker que pode ser executados em qualquer um de nós. Uma entrada associada com o recurso de IP para o ouvinte no DNS com um "nome amigável" precisa ser criado. O recurso de IP para o ouvinte só estará ativo no servidor que hospeda a réplica primária para o grupo de disponibilidade.

Se o Pacemaker é usado e um recurso de endereço IP é criado que está associado com o ouvinte, haverá uma breve interrupção como o endereço IP para em um servidor e inicia em outro, se ele é o failover automático ou manual. Enquanto isso fornece a abstração através da combinação de um único nome e endereço IP, ele não mascara a interrupção. Um aplicativo deve ser capaz de lidar com a desconexão por ter algum tipo de funcionalidade para detectar isso e se reconectar.

No entanto, a combinação do nome DNS e endereço IP é ainda não o suficiente para fornecer toda a funcionalidade que fornece um ouvinte em um WSFC, como o roteamento somente leitura para réplicas secundárias. Ao configurar um grupo de disponibilidade, um "ouvinte" ainda precisa ser configurado no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Isso pode ser visto no assistente, bem como a sintaxe Transact-SQL. Há duas maneiras de que isso pode ser configurado para funcionar da mesma maneira que no Windows:

-   Para um grupo de disponibilidade com um tipo de cluster externo, o endereço IP associado com o "ouvinte" criado no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve ser o endereço IP do recurso criado no Pacemaker.
-   Para um grupo de disponibilidade criado com um tipo de cluster nenhum, use o endereço IP associado com a réplica primária.

A instância associada com o endereço IP fornecido, em seguida, torna-se o coordenador para coisas como as solicitações de roteamentos somente leitura de aplicativos.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilidade com grupos de disponibilidade com base no Windows e réplicas 

Um grupo de disponibilidade que tem um tipo de externo ou um que seja WSFC cluster não pode ter suas réplicas de plataformas cruzadas. Isso é verdadeiro se o grupo de disponibilidade está [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] ou [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Isso significa que em uma configuração de grupo de disponibilidade tradicional com um cluster subjacente, uma réplica não pode estar em um WSFC e a outra no Linux com o Pacemaker.

Um grupo de disponibilidade com um tipo de cluster nenhum pode ter suas réplicas ultrapassam os limites do sistema operacional, portanto, pode haver ambas as réplicas com base em Linux e Windows no mesmo AG. Um exemplo é mostrado aqui onde a réplica primária é baseado em Windows, enquanto o secundário está em uma das distribuições do Linux.

![Híbrido None](./media/sql-server-linux-availability-group-overview/image1.png)

Um grupo de disponibilidade distribuído também pode cruzar os limites do sistema operacional. Os grupos de disponibilidade subjacentes são vinculados pelas regras para como eles são configurados, tal como configurado com externo que está sendo somente para Linux, mas o grupo de disponibilidade que ele está associado a poderia ser configurado usando um WSFC. Considere o seguinte exemplo:

![Híbrido Dist AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article “x”].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Próximas etapas
[Configurar o grupo de disponibilidade para o SQL Server no Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar o grupo de disponibilidade de escala de leitura para o SQL Server no Linux](sql-server-linux-availability-group-configure-rs.md)

[Adicionar grupo de disponibilidade do recurso de Cluster no RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Adicionar grupo de disponibilidade do recurso de Cluster em SLES](sql-server-linux-availability-group-cluster-sles.md)

[Adicionar grupo de disponibilidade do recurso de Cluster no Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurar um grupo de disponibilidade de plataforma cruzada](sql-server-linux-availability-group-cross-platform.md)

