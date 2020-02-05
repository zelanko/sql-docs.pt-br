---
title: Padrões de implantação do grupo de disponibilidade – SQL Server em Linux
description: Conheça as configurações de implantação compatíveis com os grupos de disponibilidade Always On do SQL Server em servidores Linux.
ms.custom: seo-lt-2019
ms.date: 04/17/2019
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.openlocfilehash: 2fea849a46dea302dccba3ae8648db3654c35798
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75558467"
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidade e proteção de dados para configurações do grupo de disponibilidade

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artigo apresenta as configurações de implantação compatíveis com os grupos de disponibilidade Always On do SQL Server em servidores Linux. Um grupo de disponibilidade dá suporte à alta disponibilidade e à proteção de dados. Detecção automática de falhas, failover automático e reconexão transparente após o failover fornecem alta disponibilidade. As réplicas sincronizadas fornecem proteção de dados. 

Em um WSFC (cluster de failover do Windows Server), uma configuração comum para alta disponibilidade usa duas réplicas síncronas e um terceiro servidor ou compartilhamento de arquivo para fornecer quorum. A testemunha de compartilhamento de arquivo valida a configuração do grupo de disponibilidade – status de sincronização e a função da réplica, por exemplo. Essa configuração garante que a réplica secundária escolhida como o destino de failover tenha as alterações mais recentes de configuração de dados e grupo de disponibilidade. 

O WSFC sincroniza os metadados de configuração para arbitragem de failover entre as réplicas do grupo de disponibilidade e a testemunha de compartilhamento de arquivo. Quando um grupo de disponibilidade não está em um WSFC, as Instâncias do SQL Server armazenam os metadados de configuração no banco de dados mestre.

Por exemplo, um grupo de disponibilidade em um cluster do Linux tem `CLUSTER_TYPE = EXTERNAL`. Não há um WSFC para arbitrar o failover. Nesse caso, os metadados de configuração são gerenciados e mantidos pelas Instâncias do SQL Server. Como não há nenhum servidor testemunha nesse cluster, uma terceira Instância do SQL Server é necessária para armazenar os metadados do estado de configuração. Todas as três instâncias do SQL Server juntas fornecem armazenamento de metadados distribuído para o cluster. 

O gerenciador de cluster pode consultar as instâncias do SQL Server no grupo de disponibilidade e orquestrar o failover para manter a alta disponibilidade. Em um cluster do Linux, o Pacemaker é o gerenciador de cluster. 

O SQL Server 2017 CU 1 permite alta disponibilidade para um grupo de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para duas réplicas síncronas, mais uma réplica somente de configuração. A réplica somente de configuração pode ser hospedada em qualquer edição do SQL Server 2017 CU1 ou posterior – incluindo o SQL Server Express Edition. A réplica somente de configuração mantém as informações de configuração sobre o grupo de disponibilidade no banco de dados mestre, mas não contém os bancos de dados de usuário no grupo de disponibilidade. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Como a configuração afeta as configurações de recurso padrão

O SQL Server 2017 apresenta a configuração de recurso de cluster `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`. Essa configuração garante que o número especificado de réplicas secundárias grave os dados de transação no log antes que a réplica primária confirme cada transação. Quando você usa um gerenciador de cluster externo, essa configuração afeta a alta disponibilidade e a proteção de dados. O valor padrão da configuração depende da arquitetura no momento em que o recurso de cluster é criado. Quando você instala o agente de recursos do SQL Server – `mssql-server-ha` – e cria um recurso de cluster para o grupo de disponibilidade, o gerenciador de cluster detecta a configuração do grupo de disponibilidade e define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` de acordo. 

Se houver suporte na configuração, o parâmetro do agente de recursos `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` será definido com o valor que fornece alta disponibilidade e proteção de dados. Para obter mais informações, confira [Noções básicas do agente de recursos do SQL Server para o Pacemaker](#pacemakerNotify).

As seções a seguir explicam o comportamento padrão para o recurso de cluster. 

Escolha um design de grupo de disponibilidade de acordo com seus requisitos empresariais específicos de alta disponibilidade, proteção de dados e escala de leitura.

As configurações a seguir descrevem os padrões de design do grupo de disponibilidade e as funcionalidades de cada padrão. Esses padrões de design se aplicam a grupos de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para soluções de alta disponibilidade. 

- **Três réplicas síncronas**
- **Duas réplicas síncronas**
- **Duas réplicas síncronas e uma réplica somente de configuração**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Três réplicas síncronas

Essa configuração consiste em três réplicas síncronas. Por padrão, ela fornece alta disponibilidade e proteção de dados. Ela também pode fornecer escala de leitura.

![Três réplicas][3]

Um grupo de disponibilidade com três réplicas síncronas pode fornecer escala de leitura, alta disponibilidade e proteção de dados. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura|Alta disponibilidade e </br> proteção de dados | Proteção de dados|
|:---|---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>\*</sup>|2|
|Interrupção principal |Failover automático. A nova primária é R/W. |Failover automático. A nova primária é R/W. |Failover automático. A nova primária não estará disponível para transações de usuário enquanto a primária anterior não se recuperar e ingressar no grupo de disponibilidade como secundária. |
|Interrupção de uma réplica secundária  | A primária é R/W. Nenhum failover automático se a primária falhar. |A primária é R/W. Nenhum failover automático se a primária falhar também. | A primária não está disponível para transações de usuário. |

<sup>\*</sup> Padrão

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Duas réplicas síncronas

Essa configuração habilita a proteção de dados. Assim como as outras configurações de grupo de disponibilidade, ela pode habilitar a escala de leitura. A configuração de duas réplicas síncronas não fornece alta disponibilidade automática. Uma configuração de duas réplicas só é aplicável ao SQL Server 2017 RTM e não é mais compatível com versões superiores (CU1 e posterior) do SQL Server 2017.

![Duas réplicas síncronas][1]

Um grupo de disponibilidade com duas réplicas síncronas fornece escala de leitura e proteção de dados. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura |Proteção de dados|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupção principal | Failover manual. Pode ocorrer perda de dados. A nova primária é R/W.| Failover automático. A nova primária não estará disponível para transações de usuário enquanto a primária anterior não se recuperar e ingressar no grupo de disponibilidade como secundária.|
|Interrupção de uma réplica secundária  |A primária é R/W; execução exposta à perda de dados. |A primária não estará disponível para transações de usuário enquanto o secundário não se recuperar.|

<sup>\*</sup> Padrão

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Duas réplicas síncronas e uma réplica somente de configuração

Um grupo de disponibilidade com duas (ou mais) réplicas síncronas e uma réplica somente de configuração fornece proteção de dados e também pode fornecer alta disponibilidade. O seguinte diagrama representa essa arquitetura:

![Grupo de disponibilidade somente de configuração][2]

1. Replicação síncrona de dados do usuário para a réplica secundária. Ela também inclui metadados de configuração do grupo de disponibilidade.
2. Replicação síncrona de metadados de configuração do grupo de disponibilidade. Ela não inclui dados do usuário.

No diagrama do grupo de disponibilidade, uma réplica primária envia dados de configuração por push para a réplica secundária e a réplica somente de configuração. A réplica secundária também recebe dados do usuário. A réplica somente de configuração não recebe dados do usuário. A réplica secundária está no modo de disponibilidade síncrona. A réplica somente de configuração não contém os bancos de dados no grupo de disponibilidade – apenas os metadados sobre o grupo de disponibilidade. Os dados de configuração na réplica somente de configuração são confirmados de forma síncrona.

> [!NOTE]
> Um grupo de disponibilidade com réplica somente de configuração é uma novidade do SQL Server 2017 CU1. Todas as instâncias do SQL Server do grupo de disponibilidade precisam ter o SQL Server 2017 CU1 ou posterior. 

O valor padrão de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0. A tabela a seguir descreve o comportamento de disponibilidade. 

| |Alta disponibilidade e </br> proteção de dados | Proteção de dados|
|:---|---|---|
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>\*</sup>|1|
|Interrupção principal | Failover automático. A nova primária é R/W. | Failover automático. A nova primária não está disponível para transações de usuário. |
|Interrupção de uma réplica secundária | A primária é R/W; execução exposta à perda de dados (se a primária falhar e não puder ser recuperada). Nenhum failover automático se a primária falhar também. | A primária não está disponível para transações de usuário. Nenhuma réplica para failover se a primária falhar também. |
|Interrupção de réplica somente de configuração | A primária é R/W. Nenhum failover automático se a primária falhar também. | A primária é R/W. Nenhum failover automático se a primária falhar também. |
|Interrupção de réplica somente de configuração + secundária síncrona| A primária não está disponível para transações de usuário. Sem failover automático. | A primária não está disponível para transações de usuário. Nenhuma réplica para failover se a primária falhar também. |

<sup>\*</sup> Padrão

> [!NOTE]
> A instância do SQL Server que hospeda a réplica somente de configuração também pode hospedar outros bancos de dados. Ela também pode participar como um banco de dados somente de configuração para mais de um grupo de disponibilidade. 

## <a name="requirements"></a>Requisitos

- Todas as réplicas de um grupo de disponibilidade com uma réplica somente de configuração precisam ter o SQL Server 2017 CU 1 ou posterior.
- Qualquer edição do SQL Server pode hospedar uma réplica somente de configuração, incluindo o SQL Server Express. 
- O grupo de disponibilidade precisa de, pelo menos, uma réplica secundária, além da réplica primária.
- As réplicas somente de configuração não são consideradas no número máximo de réplicas por instância do SQL Server. O SQL Server Standard permite até três réplicas, enquanto a SQL Server Enterprise Edition permite até nove.

## <a name="considerations"></a>Considerações

- Não mais de uma réplica somente de configuração por grupo de disponibilidade. 
- Uma réplica somente de configuração não pode ser uma réplica primária.
- Não é possível modificar o modo de disponibilidade de uma réplica somente de configuração. Para fazer a alteração de uma réplica somente de configuração para uma réplica secundária síncrona ou assíncrona, remova a réplica somente de configuração e adicione uma réplica secundária com o modo de disponibilidade necessário. 
- Uma réplica somente de configuração é síncrona com os metadados do grupo de disponibilidade. Não há dados do usuário. 
- Um grupo de disponibilidade com uma réplica primária e uma réplica somente de configuração, mas nenhuma réplica secundária não é válida. 
- Não é possível criar um grupo de disponibilidade em uma instância do SQL Server Express Edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Noções básicas do agente de recursos do SQL Server para o Pacemaker

O SQL Server 2017 CTP 1.4 adicionou o `sequence_number` ao `sys.availability_groups` para permitir que o Pacemaker identifique o grau de atualização das réplicas secundárias em relação à réplica primária. `sequence_number` é um BIGINT que aumenta de forma monotônica e que representa o grau de atualização da réplica de grupo de disponibilidade local. O Pacemaker atualiza o `sequence_number` a cada alteração de configuração de grupo de disponibilidade. Exemplos de alterações de configuração incluem failover, adição de réplica ou remoção. O número é atualizado na primária e então replicado para as réplicas secundárias. Portanto, uma réplica secundária que tem uma configuração atualizada tem o mesmo número de sequência da primária. 

Quando o Pacemaker decide promover uma réplica a primária, ele primeiro envia uma *notificação de pré-promoção* a todas as réplicas. As réplicas retornam o número de sequência. Em seguida, quando o Pacemaker tenta efetivamente promover uma réplica como primária, a réplica apenas se promove se o seu número de sequência for o mais alto de todos os números de sequência. Se o seu próprio número de sequência não corresponde ao número de sequência mais alto, a réplica rejeita a operação de promoção. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Esse processo exige, pelo menos, uma réplica disponível para promoção com o mesmo número de sequência da primária anterior. O agente de recursos do Pacemaker define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`, de modo que, pelo menos, uma réplica secundária síncrona esteja atualizada e disponível para ser o destino de um failover automático por padrão. Com cada ação de monitoramento, o valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é calculado (e atualizado, se necessário). O valor `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é o 'número de réplicas síncronas' dividido por 2. No tempo de failover, o agente de recursos exige (réplicas `total number of replicas` - `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`) para responder à notificação de pré-promoção. A réplica com o `sequence_number` mais alto é promovida a primária. 

Por exemplo, um grupo de disponibilidade com três réplicas síncronas – uma réplica primária e duas réplicas secundárias síncronas.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 1; (3 / 2 -> 1).

- O número necessário de réplicas para responder à ação de pré-promoção é 2; (3 - 1 = 2). 

Nesse cenário, duas réplicas precisam responder para que o failover seja disparado. Para um failover automático bem-sucedido após uma interrupção da réplica primária, ambas as réplicas secundárias precisam estar atualizadas e responder à notificação de pré-promoção. Se elas estiverem online e forem síncronas, elas terão o mesmo número de sequência. O grupo de disponibilidade promove uma delas. Se apenas uma das réplicas secundárias responder à ação de pré-promoção, o agente de recursos não poderá garantir que o secundário que respondeu tenha o sequence_number mais alto e um failover não seja disparado.

> [!IMPORTANT]
> Quando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0, há risco de perda de dados. Durante uma interrupção da réplica primária, o agente de recursos não dispara um failover automaticamente. Você pode aguardar a recuperação da primária ou fazer failover manualmente usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Você pode optar por substituir o comportamento padrão e impedir que o recurso de grupo de disponibilidade defina `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automaticamente.

O script a seguir define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` como 0 em um grupo de disponibilidade chamado `<**ag1**>`. Antes da execução, substitua `<**ag1**>` pelo nome do grupo de disponibilidade.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para reverter isso para o valor padrão, com base na execução da configuração do grupo de disponibilidade:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

> [!NOTE]
> Quando você executa os comandos anteriores, o primário é temporariamente rebaixado a secundário e promovido novamente. A atualização de recursos faz com que todas as réplicas sejam interrompidas e reiniciadas. O novo valor para `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é definido apenas depois que as réplicas são reiniciadas, não instantaneamente.

## <a name="see-also"></a>Confira também

[Grupos de disponibilidade no Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
