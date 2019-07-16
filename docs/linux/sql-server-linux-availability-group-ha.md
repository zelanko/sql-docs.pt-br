---
title: SQL Server Always On padrões de implantação de grupo de disponibilidade
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 637d67767e17344d63498f8cb6a141fa78b11ecb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996442"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta as configurações de implantação com suporte para grupos de disponibilidade Always On do SQL Server em servidores Linux. Um grupo de disponibilidade dá suporte a alta disponibilidade e proteção de dados. Detecção de falhas automático, failover automático e transparente reconexão, após o failover fornecem alta disponibilidade. Réplicas sincronizadas fornecem proteção de dados. 

Em um Windows Server Failover Cluster (WSFC), uma configuração comum para alta disponibilidade usa duas réplicas síncronas e um terceiro servidor ou compartilhamento de arquivos para fornecer o quorum. A testemunha de compartilhamento de arquivos valida a configuração de grupo de disponibilidade - status de sincronização e a função da réplica, por exemplo. Essa configuração garante que a réplica secundária escolhida como o destino de failover tem os dados mais recentes e as alterações de configuração do grupo de disponibilidade. 

O WSFC sincroniza os metadados de configuração para o arbitramento de failover entre as réplicas do grupo de disponibilidade e a testemunha de compartilhamento de arquivos. Quando um grupo de disponibilidade não está em um WSFC, instâncias do SQL Server armazenam os metadados de configuração no banco de dados mestre.

Por exemplo, um grupo de disponibilidade em um cluster do Linux tem `CLUSTER_TYPE = EXTERNAL`. Não há nenhum WSFC arbitrar failover. Nesse caso, os metadados de configuração é gerenciado e mantido por instâncias do SQL Server. Como não há nenhum servidor testemunha neste cluster, uma terceira instância do SQL Server é necessário para armazenar metadados de configuração do estado. Todas as três instâncias do SQL Server juntos fornecem armazenamento de metadados distribuídos para o cluster. 

O Gerenciador de cluster pode consultar as instâncias do SQL Server no grupo de disponibilidade e orquestrar o failover para manter a alta disponibilidade. Em um cluster do Linux, o Pacemaker é o Gerenciador de cluster. 

A Atualização Cumulativa 1 do SQL Server 2017 habilita a alta disponibilidade para um grupo de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para duas réplicas síncronas, mais uma réplica somente de configuração. A réplica somente de configuração pode ser hospedada em qualquer edição do SQL Server 2017 CU1 ou posterior – incluindo o SQL Server Express edition. A réplica somente de configuração mantém informações de configuração sobre o grupo de disponibilidade no banco de dados mestre, mas não contém os bancos de dados do usuário no grupo de disponibilidade. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Como a configuração afeta as configurações de recurso padrão

SQL Server 2017 apresenta o `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` configuração de recurso de cluster. Essa configuração garante que o número especificado de gravação de réplicas secundárias os dados de transações para fazer logon antes da réplica primária confirma cada transação. Quando você usa um Gerenciador de cluster externo, essa configuração afeta a alta disponibilidade e proteção de dados. O valor padrão para a configuração depende da arquitetura no momento em que o recurso de cluster é criado. Quando você instala o agente de recursos do SQL Server - `mssql-server-ha` - e criar um recurso de cluster para o grupo de disponibilidade, o Gerenciador de cluster detecta a disponibilidade de grupo configuração e conjuntos de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` adequadamente. 

Se houver suporte pela configuração, o parâmetro de agente do recurso `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é definido como o valor que fornece alta disponibilidade e proteção de dados. Para obter mais informações, consulte [agente de recursos de compreender o SQL Server para pacemaker](#pacemakerNotify).

As seções a seguir explicam o comportamento padrão para o recurso de cluster. 

Escolha um design de grupo de disponibilidade para atender aos requisitos específicos de negócios para alta disponibilidade, proteção de dados e escala de leitura.

As configurações a seguir descrevem os padrões de design de grupo de disponibilidade e os recursos de cada padrão. Esses padrões de design se aplicam a grupos de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para soluções de alta disponibilidade. 

- **Três réplicas síncronas**
- **Duas réplicas síncronas**
- **Duas réplicas síncronas e uma réplica somente de configuração**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Três réplicas síncronas

Essa configuração consiste em três réplicas síncronas. Por padrão, ele fornece alta disponibilidade e proteção de dados. Ele também pode fornecer a escala de leitura.

![Três réplicas][3]

Um grupo de disponibilidade com três réplicas síncronas pode fornecer proteção de dados, alta disponibilidade e escala de leitura. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura|Alta disponibilidade & </br> proteção de dados | proteção de dados|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|Interrupção principal |Failover automático. A nova primária é R / w. |Failover automático. A nova primária é R / w. |Failover automático. Novo primário não está disponível para transações de usuário até que o antigo primário se recupere e ingresse o grupo de disponibilidade como secundária. |
|Interrupção de uma réplica secundária  | Primária é R / w. Nenhum failover automático se o principal falhar. |Primária é R / w. Nenhum failover automático se a primária falha também. | Primário não está disponível para transações de usuário. |

<sup>\*</sup> Padrão

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Duas réplicas síncronas

Essa configuração permite que a proteção de dados. Como as outras configurações de grupo de disponibilidade, ele pode habilitar a escala de leitura. A configuração de duas réplicas síncronas não oferece alta disponibilidade automático. Uma configuração de duas réplicas só é aplicável ao SQL Server 2017 RTM e não é mais compatível com superior (CU1 e além) versões do SQL Server 2017...

![Duas réplicas síncronas][1]

Um grupo de disponibilidade com duas réplicas síncronas fornece proteção de dados e escala de leitura. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura |proteção de dados|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupção principal | Failover manual. Pode ocorrer perda de dados. A nova primária é R / w.| Failover automático. Novo primário não está disponível para transações de usuário até que o antigo primário se recupere e ingresse o grupo de disponibilidade como secundária.|
|Interrupção de uma réplica secundária  |Primária é R/W, executar exposto à perda de dados. |Primário não está disponível para transações de usuário até que a secundária se recuperar.|

<sup>\*</sup> Padrão

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Duas réplicas síncronas e uma réplica somente de configuração

Um grupo de disponibilidade com réplicas síncronas de duas (ou mais) e uma réplica somente de configuração fornece proteção de dados e também pode fornecer alta disponibilidade. O diagrama a seguir representa essa arquitetura:

![Grupo de disponibilidade somente de configuração][2]

1. Replicação síncrona de dados do usuário para a réplica secundária. Ele também inclui metadados de configuração do grupo de disponibilidade.
2. Replicação síncrona de metadados de configuração do grupo de disponibilidade. Ele não inclui dados de usuário.

No diagrama de grupo de disponibilidade, uma réplica primária envia dados de configuração para a réplica secundária e a réplica somente de configuração. A réplica secundária também recebe dados de usuário. A réplica somente de configuração não recebe dados de usuário. A réplica secundária está no modo de disponibilidade síncronos. A réplica somente de configuração não contém os bancos de dados no grupo de disponibilidade – apenas os metadados sobre o grupo de disponibilidade. Dados de configuração na réplica somente configuração sincronicamente serão confirmados.

> [!NOTE]
> Um grupo de availabilility com réplica somente configuração é novo no SQL Server 2017 CU1. Todas as instâncias do SQL Server no grupo de disponibilidade devem ser a CU1 do SQL Server 2017 ou posterior. 

O valor padrão para `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0. A tabela a seguir descreve o comportamento de disponibilidade. 

| |Alta disponibilidade & </br> proteção de dados | proteção de dados|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupção principal | Failover automático. A nova primária é R / w. | Failover automático. Novo primário não está disponível para transações de usuário. |
|Interrupção da réplica secundária | Primária é R/W, executar exposto à perda de dados (se o principal falha e não pode ser recuperado). Nenhum failover automático se a primária falha também. | Primário não está disponível para transações de usuário. Nenhuma réplica para fazer failover para se a primária falhar também. |
|Interrupção de réplica somente configuração | Primária é R / w. Nenhum failover automático se a primária falha também. | Primária é R / w. Nenhum failover automático se a primária falha também. |
|Secundário síncrono + configuração apenas paralisação de réplica| Primário não está disponível para transações de usuário. Nenhum failover automático. | Primário não está disponível para transações de usuário. Nenhuma réplica para o failover para se primário falhar também. |

<sup>\*</sup> Padrão

> [!NOTE]
> A instância do SQL Server que hospeda a réplica somente de configuração também pode hospedar outros bancos de dados. Ele também pode participar como um banco de dados somente de configuração para mais de um grupo de disponibilidade. 

## <a name="requirements"></a>Requisitos

- Todas as réplicas em um grupo de disponibilidade com uma réplica somente de configuração devem ser SQL Server 2017 CU 1 ou posterior.
- Qualquer edição do SQL Server pode hospedar uma réplica somente de configuração, incluindo o SQL Server Express. 
- O grupo de disponibilidade precisa de pelo menos uma réplica secundária - além da réplica primária.
- Réplicas de somente de configuração não contam para o número máximo de réplicas por instância do SQL Server. SQL Server standard edition permite até três réplicas, o SQL Server Enterprise Edition permite até 9.

## <a name="considerations"></a>Considerações

- Única réplica por grupo de disponibilidade não mais de uma configuração. 
- Uma réplica somente de configuração não pode ser uma réplica primária.
- Não é possível modificar o modo de disponibilidade de uma réplica somente de configuração. Para alterar de uma réplica somente de configuração para uma réplica secundária síncrona ou assíncrona, remover a réplica somente de configuração e adicionar uma réplica secundária com o modo de disponibilidade necessários. 
- Uma réplica somente de configuração é sincronizada com os metadados do grupo de disponibilidade. Não há nenhum dado de usuário. 
- Um grupo de disponibilidade com uma réplica primária e a réplica somente uma configuração, mas nenhuma réplica secundária não é válido. 
- Você não pode criar um grupo de disponibilidade em uma instância do SQL Server Express edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Entender o agente de recursos do SQL Server para pacemaker

SQL Server 2017 CTP 1.4 adicionou `sequence_number` para `sys.availability_groups` para permitir que o Pacemaker identificar o grau de atualização secundária réplicas estão com a réplica primária. `sequence_number` é um BIGINT monotônica que representa o grau de atualização a réplica do grupo de disponibilidade local. Atualizações do pacemaker a `sequence_number` com cada alteração de configuração do grupo de disponibilidade. Failover, a adição de réplica ou a remoção são exemplos de alterações de configuração. O número é atualizado na primária, então replicado para réplicas secundárias. Portanto, uma réplica secundária que tem a configuração atualizada tem o mesmo número de sequência que o primário. 

Quando o Pacemaker decide promover uma réplica para primária, ele primeiro envia uma *pré-promoção* notificação para todas as réplicas. As réplicas de retornam o número de sequência. Em seguida, quando o Pacemaker tentar efetivamente promover uma réplica para primária, a réplica apenas promoverá em si se o seu número de sequência é o mais alto de todos os números de sequência. Se o seu próprio número de sequência não coincide com o número de sequência mais alto, a réplica rejeitará a operação de promoção. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Esse processo requer pelo menos uma réplica disponível para promoção com o mesmo número de sequência que a primária anterior. Os conjuntos de agente de recursos Pacemaker `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` , de modo que pelo menos uma réplica secundária síncrona está atualizado e disponível para ser o destino de um failover automático por padrão. Com cada ação de monitoramento, o valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` calculada (e atualizado, se necessário). O `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` valor é 'número de réplicas síncronas' dividido por 2. No momento do failover, requer que o agente de recursos (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` réplicas) para responder à notificação pré-promoção. A réplica com a mais alta `sequence_number` é promovido a primário. 

Por exemplo, um grupo de disponibilidade com três réplicas síncronas — uma réplica primária e duas réplicas secundárias síncronas.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 1; (3 / 2 -> 1).

- O número necessário de réplicas para responder à ação de pré-promoção é 2; (3 - 1 = 2). 

Nesse cenário, duas réplicas precisam responder para o failover ser disparado. Para failover automático bem-sucedida após uma interrupção da réplica primária, ambas as réplicas secundárias precisam ser atualizadas e responder a notificação pré-promoção. Se eles estiverem online e síncronas, eles têm o mesmo número de sequência. O grupo de disponibilidade promove um deles. Se apenas uma das réplicas secundárias responde de pré-promoção em ação, o agente de recursos não pode garantir que a secundária que respondeu tem o sequence_number mais alto e um failover não será acionado.

> [!IMPORTANT]
> Quando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0, há risco de perda de dados. Durante uma interrupção da réplica primária, o agente de recursos não dispara automaticamente um failover. Você pode esperar do site primário para recuperar ou failover manualmente usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Você pode optar por substituir o comportamento padrão e impedir que o recurso de grupo de disponibilidade configuração `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automaticamente.

O script a seguir conjuntos `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como 0 em um grupo de disponibilidade denominado `<**ag1**>`. Antes da execução, substitua `<**ag1**>` pelo nome do grupo de disponibilidade.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para reverter para o valor padrão, com base na configuração de grupo de disponibilidade execute:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> Quando você executa os comandos anteriores, o primário é temporariamente rebaixado para secundária, promovido novamente. A atualização de recurso faz com que todas as réplicas parar e reiniciar. O novo valor para`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é definido apenas depois que as réplicas forem reiniciadas, não instantaneamente.

## <a name="see-also"></a>Confira também

[Grupos de disponibilidade no Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
