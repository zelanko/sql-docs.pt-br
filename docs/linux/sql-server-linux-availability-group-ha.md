---
title: "SQL Server Always On padrões de implantação de grupo de disponibilidade | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cacdf2de6c6e85c8afd0723f4dae21feab0c71cf
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este artigo apresenta as configurações de implantação com suporte para grupos de disponibilidade do SQL Server Always On em servidores Linux. Um grupo de disponibilidade dá suporte a alta disponibilidade e proteção de dados. Detecção de falha automático, failover automático e transparente reconexão depois do failover fornecem alta disponibilidade. Réplicas sincronizadas fornecem proteção de dados. 

Em um Windows Server Failover Cluster (WSFC), uma configuração comum para alta disponibilidade usa duas réplicas síncronas e um terceiro servidor ou compartilhamento de arquivos para fornecer o quorum. A testemunha de compartilhamento de arquivos valida a configuração de grupo de disponibilidade - status de sincronização e a função da réplica, por exemplo. Essa configuração garante que a réplica secundária escolhida como o destino de failover tem os dados mais recentes e alterações de configuração do grupo de disponibilidade. 

O WSFC sincroniza os metadados de configuração para o arbitramento failover entre as réplicas de grupo de disponibilidade e a testemunha de compartilhamento de arquivos. Quando um grupo de disponibilidade não está em um WSFC, instâncias do SQL Server armazenam metadados de configuração no banco de dados mestre.

Por exemplo, um grupo de disponibilidade em um cluster do Linux tem `CLUSTER_TYPE = EXTERNAL`. Não há nenhum WSFC para arbitram o failover. Nesse caso, os metadados de configuração é gerenciado e mantido por instâncias do SQL Server. Porque não há nenhum servidor testemunha neste cluster, uma terceira instância do SQL Server é necessário para armazenar metadados de estado de configuração. Juntas, todas as três instâncias do SQL Server fornecem armazenamento de metadados distribuídos para o cluster. 

O Gerenciador de cluster pode consultar instâncias do SQL Server no grupo de disponibilidade e orquestrar failover para manter a alta disponibilidade. Em um cluster do Linux, Pacemaker é o Gerenciador de cluster. 

SQL Server 2017 atualização Cumulativa 1 habilita a alta disponibilidade para um grupo de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para duas réplicas síncronas mais uma réplica somente de configuração. A única réplica de configuração pode ser hospedada em qualquer edição do SQL Server de 2017 CU1 ou posterior - incluindo o SQL Server Express edition. A única réplica de configuração mantém informações de configuração sobre o grupo de disponibilidade do banco de dados mestre, mas não contém os bancos de dados do usuário no grupo de disponibilidade. 

## <a name="how-the-configuration-affects-default-resource-settings"></a>Como a configuração afeta as configurações de recurso padrão

SQL Server 2017 apresenta o `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` configuração de recurso de cluster. Essa configuração garante o número especificado de gravação de réplicas secundárias os dados de transações para fazer logon antes da réplica primária confirma cada transação. Quando você usa um Gerenciador de cluster externo, essa configuração afeta a alta disponibilidade e proteção de dados. O valor padrão para a configuração depende da arquitetura no momento em que o recurso de cluster é criado. Quando você instala o agente de recursos do SQL Server - `mssql-server-ha` - e criar um recurso de cluster para o grupo de disponibilidade, o Gerenciador de cluster detecta a disponibilidade agrupar conjuntos e configuração `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` adequadamente. 

Se a configuração, o parâmetro do agente de recursos com suporte `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é definido como o valor que fornece alta disponibilidade e proteção de dados. Para obter mais informações, consulte [entender o SQL Server agent de recurso para pacemaker](#pacemakerNotify).

As seções a seguir explicam o comportamento padrão para o recurso de cluster. 

Escolha um design de grupo de disponibilidade para atender aos requisitos de negócios específicos para alta disponibilidade, proteção de dados e escala de leitura.

As configurações a seguir descrevem os padrões de design do grupo de disponibilidade e os recursos de cada padrão. Esses padrões de design se aplicam a grupos de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para soluções de alta disponibilidade. 

- **Três réplicas síncronas**
- **Duas réplicas síncronas**
- **Duas réplicas síncronas e uma única réplica de configuração**

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Três réplicas síncronas

Esta configuração consiste em três réplicas síncronas. Por padrão, ele fornece alta disponibilidade e proteção de dados. Ela também pode fornecer dimensionamento de leitura.

![Três réplicas][3]

Um grupo de disponibilidade com réplicas síncronas três pode fornecer proteção de dados, alta disponibilidade e escala de leitura. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura|Alta disponibilidade & </br> Proteção de dados | Proteção de dados
|:---|---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 |1<sup>*</sup>|2
|Interrupção principal | Failover manual. Pode ocorrer perda de dados. Novo primário é R / w. |Failover automático. Novo primário é R / w. |Failover automático. Novo primário não está disponível para transações de usuário até que o antigo primário recupera e associa o grupo de disponibilidade como secundário. 
|Interrupção de uma réplica secundária  | É primário R / w. Nenhum failover automático se o principal falhar. |É primário R / w. Nenhum failover automático se primário falha também. | Primário não está disponível para transações de usuário. 
<sup>*</sup>Padrão

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Duas réplicas síncronas

Essa configuração permite que a proteção de dados. Como as outras configurações de grupo de disponibilidade, ele pode habilitar a escala de leitura. A configuração de duas réplicas síncronas não fornece alta disponibilidade automática. 

![Duas réplicas síncronas][1]

Um grupo de disponibilidade com duas réplicas síncronas fornece proteção de dados e a escala de leitura. A tabela a seguir descreve o comportamento de disponibilidade. 

| |escala de leitura |Proteção de dados
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupção principal | Failover manual. Pode ocorrer perda de dados. Novo primário é R / w.| Failover automático. Novo primário não está disponível para transações de usuário até que o antigo primário recupera e associa o grupo de disponibilidade como secundário.
|Interrupção de uma réplica secundária  |Primário é R/W, em execução exposto a perda de dados. |Primário não está disponível para transações de usuário até que recupera secundária.
<sup>*</sup>Padrão

>[!NOTE]
>O cenário anterior é o comportamento antes do SQL Server de 2017 atualização Cumulativa 1. 

<a name = "configOnly"></a>

## <a name="two-synchronous-replicas-and-a-configuration-only-replica"></a>Duas réplicas síncronas e uma única réplica de configuração

Um grupo de disponibilidade com réplicas síncronas dois (ou mais) e uma réplica somente configuração fornece proteção de dados e também pode fornecer alta disponibilidade. O diagrama a seguir representa essa arquitetura:

![Grupo de disponibilidade somente da configuração][2]

1. Replicação síncrona de dados de usuário para a réplica secundária. Ele também inclui metadados de configuração do grupo de disponibilidade.
2. Replicação síncrona de metadados de configuração do grupo de disponibilidade. Ele não inclui dados de usuário.

No diagrama de grupo de disponibilidade, uma réplica primária envia dados de configuração para a réplica secundária e a única réplica de configuração. A réplica secundária também recebe dados de usuário. A única réplica de configuração não recebe dados de usuário. A réplica secundária está no modo de disponibilidade síncrona. A única réplica de configuração não contém os bancos de dados no grupo de disponibilidade - somente os metadados sobre o grupo de disponibilidade. Dados de configuração na réplica apenas configuração sincronicamente serão confirmados.

>[!NOTE]
>Um grupo de availabilility com a réplica apenas de configuração é novo para o SQL Server de 2017 CU1. Todas as instâncias do SQL Server no grupo de disponibilidade devem ser SQL Server 2017 CU1 ou posterior. 

O valor padrão para `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0. A tabela a seguir descreve o comportamento de disponibilidade. 

| |Alta disponibilidade & </br> Proteção de dados | Proteção de dados
|:---|---|---
|`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT=`|0 <sup>*</sup>|1
|Interrupção principal | Failover automático. Novo primário é R / w. | Failover automático. Novo primário não está disponível para transações de usuário. 
|Interrupção de réplica secundária | Primário está R/W, em execução exposto a perda de dados (se o principal falha e não pode ser recuperado). Nenhum failover automático se primário falha também. | Primário não está disponível para transações de usuário. Nenhuma réplica façam failover para se primário falha também. 
|Interrupção de réplica apenas de configuração | É primário R / w. Nenhum failover automático se primário falha também. | É primário R / w. Nenhum failover automático se primário falha também. 
|Secundário síncrono + configuração somente paralisação de réplica| Primário não está disponível para transações de usuário. Nenhum failover automático. | Primário não está disponível para transações de usuário. Nenhuma réplica para failover para se primário falha também. 
<sup>*</sup>Padrão

>[!NOTE]
>A instância do SQL Server que hospeda a réplica apenas de configuração também pode hospedar outros bancos de dados. Ele também pode participar como um banco de dados somente de configuração para mais de um grupo de disponibilidade. 

## <a name="requirements"></a>Requisitos

* Todas as réplicas de um grupo de disponibilidade com uma única réplica de configuração devem ser SQL Server 2017 atualização Cumulativa 1 ou posterior.
* Qualquer edição do SQL Server pode hospedar uma réplica apenas de configuração, incluindo o SQL Server Express. 
* O grupo de disponibilidade precisa de pelo menos uma réplica secundária - além da réplica primária.
* Réplicas somente de configuração não são considerados o número máximo de réplicas por instância do SQL Server. SQL Server standard edition permite até três réplicas, SQL Server Enterprise Edition permite até 9.

## <a name="considerations"></a>Considerações

* Única réplica por grupo de disponibilidade não mais de uma configuração. 
* Uma única réplica de configuração não pode ser uma réplica primária.
* Você não pode modificar o modo de disponibilidade de uma réplica somente de configuração. Para alterar de uma única réplica de configuração para uma réplica secundária síncrona ou assíncrona, remover a réplica apenas de configuração e adicionar uma réplica secundária com o modo de disponibilidade exigido. 
* Uma única réplica de configuração é síncrona com os metadados do grupo de disponibilidade. Não há nenhum dado de usuário. 
* Um grupo de disponibilidade com uma réplica primária e a réplica apenas uma configuração, mas nenhuma réplica secundária não é válido. 
* Você não pode criar um grupo de disponibilidade em uma instância do SQL Server Express edition. 

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Entender o agente de recursos do SQL Server para pacemaker

SQL Server 2017 CTP 1.4 adicionado `sequence_number` para `sys.availability_groups` para permitir Pacemaker identificar secundário atualizado como réplicas estão com a réplica primária. `sequence_number`é um BIGINT aumentando de forma monotônica que representa atualizado como a réplica do grupo de disponibilidade local. Atualizações de pacemaker a `sequence_number` com cada alteração de configuração do grupo de disponibilidade. Exemplos de alterações de configuração incluem o failover, a adição de réplica ou a remoção. O número é atualizado na réplica primária e replicado para réplicas secundárias. Assim, uma réplica secundária que tem a configuração atualizada tem o mesmo número de sequência do primário. 

Quando decide Pacemaker promover uma réplica primária, ele primeiro envia um *previamente promover* notificação para todas as réplicas. As réplicas de retornam o número de sequência. Em seguida, quando na verdade tenta Pacemaker promover uma réplica primária, a réplica apenas promove próprio se o seu número de sequência é o mais alto de todos os números de sequência. Se o seu próprio número de sequência não coincide com o maior número de sequência, a réplica rejeita a operação de promoção. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Esse processo requer pelo menos uma réplica disponível para promoção com o mesmo número de sequência do primário anterior. Os conjuntos de agente do recurso Pacemaker `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` , de forma que pelo menos uma réplica secundária síncrona está atualizado e disponível para ser o destino de um failover automático por padrão. Com cada ação de monitoramento, o valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` calculada (e atualizados, se necessário). O `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` valor é 'número de réplicas síncronas' dividido por 2. No momento do failover, o agente de recursos requer (`total number of replicas`  -  `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` réplicas) para responder ao previamente promover a notificação. A réplica com o mais alto `sequence_number` é promovido a primário. 

Por exemplo, um grupo de disponibilidade com três réplicas síncronas - uma réplica primária e duas réplicas secundárias síncronas.

- `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`é 1; (3 / 2 -> 1).

- O número necessário de réplicas para responder para promover previamente a ação é 2; (3 - 1 = 2). 

Nesse cenário, duas réplicas precisam responder para o failover deve ser disparada. Para failover automático bem-sucedida após uma interrupção de réplica primária, ambas as réplicas secundárias precisam ser atualizadas e responder a promover previamente a notificação. Se eles estiverem online e síncrona, eles têm o mesmo número de sequência. O grupo de disponibilidade promove um deles. Se apenas uma das réplicas secundárias responde para o promover previamente ação, o agente de recursos não pode garantir que o secundário que respondeu tem o sequence_number mais alto e um failover não será disparado.

>[!IMPORTANT]
>Quando `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é 0, há risco de perda de dados. Durante uma interrupção da réplica primária, o agente de recursos não aciona automaticamente um failover. Você pode esperar para o site primário recuperar ou failover manualmente usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Você pode optar por substituir o comportamento padrão e impedir que o recurso de grupo de disponibilidade da configuração `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` automaticamente.

O script a seguir define `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` 0 em um grupo de disponibilidade denominada `<**ag1**>`. Antes de executar a substituição `<**ag1**>` com o nome do seu grupo de disponibilidade.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para reverter para o valor padrão, com base na configuração do grupo de disponibilidade execute:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Quando você executa os comandos anteriores, primário está temporariamente rebaixado para o secundário, depois promovido novamente. A atualização de recurso faz com que todas as réplicas parar e reiniciar. O novo valor para`REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` é definida apenas uma vez réplicas forem reiniciadas, não instantaneamente.

## <a name="see-also"></a>Consulte também

[Grupos de disponibilidade no Linux](sql-server-linux-availability-group-overview.md)

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[2]: ./media/sql-server-linux-availability-group-ha/2-configuration-only.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
[4]: ./media/sql-server-linux-availability-group-ha/configuration-only-example.png
