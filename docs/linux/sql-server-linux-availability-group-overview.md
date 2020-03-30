---
title: Grupos de disponibilidade para o SQL Server em Linux
description: Saiba mais sobre as características de grupos de disponibilidade Always On do SQL Server em Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: e4979fbb4e2dbbccf7ed11b744051373b0750d1f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75558621"
---
# <a name="always-on-availability-groups-on-linux"></a>Grupos de Disponibilidade AlwaysOn no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo descreve as características de AGs (Grupos de Disponibilidade AlwaysOn) em instalações do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] baseadas no Linux. Ele também aborda as diferenças entre os AGs baseados no WSFC (cluster de failover do Windows Server) e no Linux. Confira a [documentação baseada no Windows](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) para obter os conceitos básicos de AGs, pois eles funcionam da mesma forma no Windows e no Linux, exceto o WSFC.

Do ponto de vista de alto nível, os grupos de disponibilidade do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Linux são os mesmos das implementações baseadas no WSFC. Isso significa que todas as limitações e os recursos são os mesmos, com algumas exceções. As principais diferenças incluem:

-   O DTC (Coordenador de Transações Distribuídas) da Microsoft é compatível com o Linux a partir do SQL Server 2017 CU16. No entanto, ainda não há suporte para o DTC em Grupos de Disponibilidade no Linux. Se os aplicativos exigirem o uso de transações distribuídas e precisarem de um AG, implante o [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no Windows.
-   As implantações baseadas em Linux que exigem alta disponibilidade usam o Pacemaker para clustering em vez de um WSFC.
-   Ao contrário da maioria das configurações para AGs no Windows, exceto pelo cenário de Cluster de Grupo de Trabalho, o Pacemaker nunca exige o AD DS (Active Directory Domain Services).
-   Como fazer failover de um AG de um nó para outro é diferente entre o Linux e o Windows.
-   Algumas configurações, como `required_synchronized_secondaries_to_commit`, só podem ser alteradas por meio do Pacemaker no Linux, enquanto uma instalação baseada no WSFC usa o Transact-SQL.

## <a name="number-of-replicas-and-cluster-nodes"></a>Número de réplicas e nós de cluster

Um AG no [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] pode ter duas réplicas no total: uma primária e uma secundária que só podem ser usadas para fins de disponibilidade. Ele não pode ser usado para nada mais, como consultas legíveis. Um AG no [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] pode ter até nove réplicas no total: uma primária e até oito secundárias, das quais até três (incluindo a primária) podem ser síncronas. Se você estiver usando um cluster subjacente, poderá haver, no máximo, 16 nós quando o Corosync estiver envolvido. Um grupo de disponibilidade pode abranger, no máximo, nove dos 16 nós com [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] e dois com [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)].

Uma configuração de duas réplicas que exige a capacidade de fazer failover automaticamente para outra réplica exige o uso de uma réplica somente de configuração, conforme descrito em [Quorum e réplica somente de configuração](#configuration-only-replica-and-quorum). As réplicas somente de configuração foram introduzidas no [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] CU1 (atualização cumulativa 1), de modo que essa deve ser a versão mínima implantada para essa configuração.

Se o Pacemaker for usado, ele deverá ser configurado corretamente para que permaneça em funcionamento. Isso significa que o quorum e o STONITH precisam ser implementados corretamente de uma perspectiva do Pacemaker, além dos requisitos do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], como uma réplica somente de configuração.

Somente há suporte para réplicas secundárias legíveis no [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)].

## <a name="cluster-type-and-failover-mode"></a>Tipo de cluster e modo de failover

Uma novidade do [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é a introdução de um tipo de cluster para AGs. Para o Linux, há dois valores válidos: Externo e Nenhum. Um tipo de cluster Externo significa que o Pacemaker será usado sob o AG. O uso de Externo para o tipo de cluster exige que o modo de failover seja definido como Externo também (outra novidade do [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]). Há suporte para failover automático, mas, ao contrário de um WSFC, o modo de failover é definido como Externo, não automático, quando o Pacemaker é usado. Ao contrário de um WSFC, a parte do Pacemaker do AG é criada depois que o AG é configurado.

Um tipo de cluster Nenhum significa que não há nenhum requisito para o Pacemaker nem o AG o usará. Mesmo em servidores que têm o Pacemaker configurado, se um AG estiver configurado com um tipo de cluster Nenhum, o Pacemaker não verá nem gerenciará esse AG. Um tipo de cluster Nenhum só dá suporte ao failover manual de uma réplica primária para uma secundária. Um AG criado com a opção Nenhum é direcionado principalmente para o cenário de expansão de leitura, bem como para atualizações. Embora isso possa funcionar em cenários como recuperação de desastre ou disponibilidade local em que nenhum failover automático é necessário, isso não é recomendável. A história do ouvinte também é mais complexa sem o Pacemaker.

O tipo de cluster é armazenado na DMV (exibição de gerenciamento dinâmico) `sys.availability_groups` do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], nas colunas `cluster_type` e `cluster_type_desc`.

## <a name="required_synchronized_secondaries_to_commit"></a>secundários\_sincronizados\_com confirmação\_necessária\_

Uma novidade do [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] é uma configuração que é usada por AGs chamada `required_synchronized_secondaries_to_commit`. Isso informa ao AG o número de réplicas secundárias que precisam estar em sincronia com a primária. Isso habilita tarefas como failover automático (somente quando integrado ao Pacemaker com um tipo de cluster Externo) e controla o comportamento de tarefas como a disponibilidade da primária se o número correto de réplicas secundárias está online ou offline. Para entender mais sobre como isso funciona, confira [Alta disponibilidade e proteção de dados para configurações do grupo de disponibilidade](sql-server-linux-availability-group-ha.md). O valor `required_synchronized_secondaries_to_commit` é definido por padrão e mantido pelo Pacemaker/[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Você pode substituir esse valor manualmente.

A combinação de `required_synchronized_secondaries_to_commit` e o novo número de sequência (que é armazenado em `sys.availability_groups`) informa o Pacemaker e [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] que, por exemplo, o failover automático poderá ocorrer. Nesse caso, uma réplica secundária terá o mesmo número de sequência da primária, o que significa que ela está atualizada com todas as informações de configuração mais recentes.

Há três valores que podem ser definidos para `required_synchronized_secondaries_to_commit`: 0, 1 ou 2. Eles controlam o comportamento do que acontece quando uma réplica fica não disponível. Os números correspondem ao número de réplicas secundárias que precisam ser sincronizadas com a primária. O comportamento é o seguinte no Linux:

-   0 – as réplicas secundárias não precisam estar no estado sincronizado com a primária. No entanto, se os secundários não forem sincronizados, não haverá nenhum failover automático. 
-   1 – uma réplica secundária precisa estar em um estado sincronizado com o primária; o failover automático é possível. O banco de dados primário fica não disponível até que uma réplica síncrona secundária esteja disponível.
-   2 – ambas as réplicas secundárias em uma configuração de AG com três ou mais nós precisam ser sincronizadas com a primária; o failover automático é possível.

`required_synchronized_secondaries_to_commit` controla não apenas o comportamento de failovers com réplicas síncronas, mas a perda de dados. Com um valor igual a 1 ou 2, uma réplica secundária sempre precisa ser sincronizada, para que sempre haja redundância de dados. Isso significa que não há perda de dados.

Para alterar o valor de `required_synchronized_secondaries_to_commit`, use a seguinte sintaxe:

>[!NOTE]
>A alteração o valor faz com que o recurso seja reiniciado, o que significa uma breve interrupção. A única maneira de evitar isso é definir o recurso como não sendo gerenciado pelo cluster temporariamente.

**RHEL (Red Hat Enterprise Linux) e Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

em que *AGResourceName* é o nome do recurso configurado para o AG e *Value* é 0, 1 ou 2. Para defini-lo novamente com o padrão do Pacemaker que gerencia o parâmetro, execute a mesma instrução sem valor.

O failover automático de um AG é possível quando as seguintes condições são atendidas:

-   As réplicas primária e a secundária são definidas como movimentação de dados síncrona.
-   O secundário tem um estado igual a sincronizado (não sincronizando), o que significa que os dois estão no mesmo ponto de dados.
-   O tipo de cluster é definido como Externo. O failover automático não é possível com um tipo de cluster Nenhum.
-   O `sequence_number` da réplica secundária a se tornar a primária tem o número de sequência mais alto – em outras palavras, o `sequence_number` da réplica secundária corresponde àquele da réplica primária original.

Se essas condições forem atendidas e o servidor que hospeda a réplica primária falhar, o AG alterará a propriedade para uma réplica síncrona. O comportamento das réplicas síncronas (das quais pode haver três totais: uma primária e duas réplicas secundárias) pode continuar sendo controlado por `required_synchronized_secondaries_to_commit`. Isso funciona com AGs no Windows e no Linux, mas é configurado de forma totalmente diferente. No Linux, o valor é configurado automaticamente pelo cluster no próprio recurso do AG.

## <a name="configuration-only-replica-and-quorum"></a>Quorum e réplica somente de configuração

Outra novidade do [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] no CU1 em diante é uma réplica somente de configuração. Como o Pacemaker é diferente de um WSFC, especialmente quando se trata de quorum e a exigência de STONITH, ter apenas uma configuração de dois nós não funcionará para um AG. Para uma FCI, os mecanismos de quorum fornecidos pelo Pacemaker podem ser satisfatórios, porque toda a arbitragem de failover da FCI ocorre na camada de cluster. Para um AG, a arbitragem no Linux ocorre em [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], no qual todos os metadados são armazenados. É nesse momento que a réplica somente de configuração entra em cena.

Sem qualquer outro item, um terceiro nó e, pelo menos, uma réplica sincronizada serão necessários. A réplica somente de configuração armazena a configuração do AG no banco de dados mestre, igual às outras réplicas na configuração do AG. A réplica somente de configuração não tem os bancos de dados de usuário que participam do AG. Os dados de configuração são enviados de forma síncrona da primária. Esses dados de configuração são usados durante failovers, sejam eles automáticos ou manuais.

Para que um AG mantenha o quorum e permita failovers automáticos com um tipo de cluster Externo, ele precisa:

-   Ter três réplicas síncronas (somente [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]); ou
-   Ter duas réplicas (primária e secundária), bem como uma réplica somente de configuração.

Os failovers manuais poderão ocorrer se os tipos de cluster Externo ou Nenhum estiverem sendo usados para configurações do AG. Embora uma réplica somente de configuração possa ser definida com um AG que tem um tipo de cluster Nenhum, isso não é recomendável, pois complica a implantação. Para essas configurações, modifique `required_synchronized_secondaries_to_commit` manualmente para que ele tenha um valor igual a, pelo menos, 1, de modo que haja, no mínimo, uma réplica sincronizada.

Uma réplica somente de configuração pode ser hospedada em qualquer edição do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], incluindo o [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]. Isso minimizará os custos de licenciamento e garantirá que ele funcione com AGs no [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)]. Isso significa que o terceiro servidor necessário só precisa atender à especificação mínima do [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], já que ele não está recebendo o tráfego de transação do usuário para o AG.

Quando uma réplica somente de configuração é usada, ela tem o seguinte comportamento:

-   Por padrão, `required_synchronized_secondaries_to_commit` é definido como 0. Isso pode ser modificado manualmente para 1, se desejado.
-   Se a primária falhar e `required_synchronized_secondaries_to_commit` for 0, a réplica secundária se tornará a nova primária e ficará disponível para leitura e gravação. Se o valor for 1, ocorrerá um failover automático, mas não serão aceitas novas transações enquanto a outra réplica estiver online.
-   Se uma réplica secundária falhar e `required_synchronized_secondaries_to_commit` for 0, a réplica primária ainda aceitará transações, mas se a primária falhar nesse ponto, não haverá proteção para os dados nem um failover possível (manual ou automático), já que uma réplica secundária não está disponível.
-   Se as réplicas somente de configuração falharem, o AG funcionará normalmente, mas nenhum failover automático será possível.
-   Se uma réplica secundária síncrona e a réplica somente de configuração falharem, a primária não poderá aceitar transações e não haverá nenhum lugar para ela fazer failover.

No CU1, há um bug conhecido no log, no arquivo corosync.log, gerado por meio do `mssql-server-ha`. Se uma réplica secundária não puder se tornar a primária devido ao número de réplicas necessárias disponíveis, a mensagem atual indicará "Era esperado receber um número de sequência, mas somente dois foram recebidos. Não há réplicas suficientes online para promover a réplica local com segurança." Os números devem ser revertidos e devem indicar "Era esperado receber dois números de sequência, mas somente um foi recebido. Não há réplicas suficientes online para promover a réplica local com segurança." 

## <a name="multiple-availability-groups"></a>Vários grupos de disponibilidade 

Mais de um AG pode ser criado por conjunto de servidores ou cluster do Pacemaker. A única limitação são os recursos do sistema. A propriedade do AG é mostrada pelo mestre. Diferentes AGs podem pertencer a diferentes nós; eles não precisam estar em execução no mesmo nó.

## <a name="drive-and-folder-location-for-databases"></a>Localização da unidade e da pasta para bancos de dados

Como ocorre em AGs baseados no Windows, a estrutura de pastas e unidade para os bancos de dados de usuário que participam de um AG devem ser idênticas. Por exemplo, se os bancos de dados de usuário estiverem em `/var/opt/mssql/userdata` no Servidor A, essa mesma pasta deverá existir no Servidor B. A única exceção a isso é indicada na seção [Interoperabilidade com réplicas e grupos de disponibilidade baseados no Windows](#interoperability-with-windows-based-availability-groups-and-replicas).

## <a name="the-listener-under-linux"></a>O ouvinte no Linux

O ouvinte é uma funcionalidade opcional para um AG. Ele fornece um ponto único de entrada para todas as conexões (leitura/gravação para a réplica primária e/ou somente leitura para réplicas secundárias), de modo que os aplicativos e os usuários finais não precisem saber qual servidor está hospedando os dados. Em um WSFC, essa é a combinação de um recurso de nome de rede e um recurso de IP, que é então registrado no AD DS (se necessário), bem como no DNS. Em combinação com o próprio recurso do AG, ele fornece essa abstração. Para obter mais informações sobre um ouvinte, confira [Ouvintes, conectividade de cliente e failover de aplicativo](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md).

O ouvinte no Linux é configurado de forma diferente, mas sua funcionalidade é a mesma. Não há nenhum conceito de um recurso de nome de rede no Pacemaker, nem um objeto é criado no AD DS; há apenas um recurso de endereço IP criado no Pacemaker que pode ser executado em qualquer um dos nós. Uma entrada associada ao recurso de IP para o ouvinte no DNS com um "nome amigável" precisa ser criada. O recurso de IP para o ouvinte estará ativo somente no servidor que hospeda a réplica primária para esse grupo de disponibilidade.

Se o Pacemaker for usado e um recurso de endereço IP for criado e associado ao ouvinte, haverá uma breve interrupção, pois o endereço IP é interrompido em um servidor e começa no outro, seja ele um failover automático ou manual. Embora isso forneça abstração por meio da combinação de um único nome e endereço IP, ele não mascara a interrupção. Um aplicativo precisa conseguir lidar com a desconexão tendo algum tipo de funcionalidade para detectar isso e se reconectar.

No entanto, a combinação do nome DNS e do endereço IP ainda não é suficiente para fornecer toda a funcionalidade oferecida por um ouvinte em um WSFC, como o roteamento somente leitura para réplicas secundárias. Ao configurar um AG, um "ouvinte" ainda precisa ser configurado no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Isso pode ser visto no assistente, bem como na sintaxe Transact-SQL. Há duas maneiras de configurar isso para que funcione como no Windows:

-   Para um AG com um tipo de cluster Externo, o endereço IP associado ao "ouvinte" criado no [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deve ser o endereço IP do recurso criado no Pacemaker.
-   Para um AG criado com um tipo de cluster Nenhum, use o endereço IP associado à réplica primária.

A instância associada ao endereço IP fornecido torna-se o coordenador de tarefas como solicitações de roteamento somente leitura dos aplicativos.

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Interoperabilidade com réplicas e grupos de disponibilidade baseados no Windows 

Um AG que tem um tipo de cluster Externo ou um que é o WSFC não pode ter suas réplicas entre plataformas. Isso será verdadeiro se o AG for [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] ou [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)]. Isso significa que, em uma configuração tradicional do AG com um cluster subjacente, uma réplica não pode estar em um WSFC e a outra no Linux com o Pacemaker.

Um AG com um tipo de cluster NENHUM pode ter suas réplicas entre limites do sistema operacional e, portanto, pode haver réplicas baseadas no Linux e no Windows no mesmo AG. Um exemplo é mostrado aqui, em que a réplica primária é baseada no Windows, enquanto o secundário está em uma das distribuições do Linux.

![Nenhum Híbrido](./media/sql-server-linux-availability-group-overview/image1.png)

Uma AG distribuída também pode cruzar os limites do sistema operacional. Os AGs subjacentes são associados pelas regras de como eles são configurados, como um configurado com Externo sendo somente Linux, mas o AG no qual ele ingressou pode ser configurado usando um WSFC. Considere o exemplo a seguir:

![AG de Dist. Híbrida](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>Próximas etapas
[Configurar um grupo de disponibilidade para o SQL Server em Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar um grupo de disponibilidade de escala de leitura para o SQL Server em Linux](sql-server-linux-availability-group-configure-rs.md)

[Adicionar um recurso de cluster de grupo de disponibilidade no RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Adicionar um recurso de cluster de grupo de disponibilidade no SLES](sql-server-linux-availability-group-cluster-sles.md)

[Adicionar um recurso de cluster de grupo de disponibilidade no Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

[Configurar um grupo de disponibilidade multiplataforma](sql-server-linux-availability-group-cross-platform.md)

