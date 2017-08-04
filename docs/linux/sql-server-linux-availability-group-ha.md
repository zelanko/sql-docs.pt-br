---
title: "SQL Server Always On padrões de implantação de grupo de disponibilidade | Microsoft Docs"
ms.custom: 
ms.date: 06/16/2017
ms.prod: sql-linux
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8e2d26fd9ce79fc8c47c7499313648d565ae1b97
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---

# <a name="high-availability-and-data-protection-for-availability-group-configurations"></a>Alta disponibilidade e proteção de dados para as configurações de grupo de disponibilidade

Este artigo apresenta as configurações de implantação com suporte para grupos de disponibilidade do SQL Server Always On em servidores Linux. Um grupo de disponibilidade dá suporte a alta disponibilidade e proteção de dados. Detecção de falha automático, failover automático e transparente reconexão depois do failover fornecem alta disponibilidade. Réplicas sincronizadas fornecem proteção de dados. 

>[!NOTE]
>Além de alta disponibilidade e proteção de dados, um grupo de disponibilidade também pode fornecer recuperação de desastres, migração de plataforma entre e expansão de leitura. Este artigo aborda principalmente a implementações de alta disponibilidade e proteção de dados. 

Com o Windows Server failover clustering, uma configuração comum para alta disponibilidade usa duas réplicas síncronas e um [testemunha de compartilhamento de arquivos](http://technet.microsoft.com/library/cc731739.aspx). A testemunha de compartilhamento de arquivos valida a configuração de grupo de disponibilidade - status de sincronização e a função da réplica, por exemplo. Essa configuração garante que a réplica secundária escolhida como o destino de failover tem os dados mais recentes e alterações de configuração do grupo de disponibilidade. 

As soluções de alta disponibilidade atual para Linux não acomodar uma testemunha externa como a testemunha de compartilhamento de arquivos em um cluster de failover do Windows Server. Quando não há nenhum cluster de failover do Windows Server, a configuração do grupo de disponibilidade é armazenada no banco de dados mestre instâncias participantes do SQL Server. Portanto, o grupo de disponibilidade requer pelo menos três réplicas síncronas para alta disponibilidade e proteção de dados. Depois de criar um grupo de disponibilidade em servidores Linux, crie um recurso de cluster. As configurações de recursos de cluster determinam a configuração de alta disponibilidade.

Escolha um design de grupo de disponibilidade para atender aos requisitos de negócios específicos para alta disponibilidade, proteção de dados e expansão de leitura.

>[!IMPORTANT]
>As configurações a seguir descrevem os padrões de design do grupo de disponibilidade e os recursos de cada padrão. Esses padrões de design se aplicam a grupos de disponibilidade com `CLUSTER_TYPE = EXTERNAL` para soluções de alta disponibilidade. 

Os padrões de design são duas configurações de grupo de disponibilidade. As configurações incluem:

- **Três réplicas síncronas**

- **Duas réplicas síncronas**

## <a name="how-the-configuration-affects-default-resource-settings"></a>Como a configuração afeta as configurações de recurso padrão

A configuração de recurso de cluster `required_synchronized_secondaries_to_commit` garante que cada transação é gravada em um número mínimo de logs de réplica secundária antes de confirmar a transação na réplica primária. Essa configuração pode afetar a alta disponibilidade e proteção de dados, dependendo da configuração. Quando você instala o agente de recursos do SQL Server - `mssql-server-ha` - e criar um recurso de cluster para o grupo de disponibilidade, o Gerenciador de cluster detecta a disponibilidade agrupar conjuntos e configuração `required_synchronized_secondaries_to_commit` adequadamente. 

Se a configuração, o parâmetro do agente de recursos com suporte `required_synchronized_secondaries_to_commit` é definido como o valor que fornece alta disponibilidade e proteção de dados. Para obter mais informações, consulte [entender o SQL Server agent de recurso para pacemaker](#pacemakerNotify).

As seções a seguir explicam o comportamento padrão para o recurso de cluster. 

<a name="threeSynch"></a>

## <a name="three-synchronous-replicas"></a>Três réplicas síncronas

Esta configuração consiste em três réplicas síncronas. Por padrão, ele fornece alta disponibilidade e proteção de dados. Ela também pode fornecer expansão de leitura.

![Três réplicas][3]

A tabela a seguir descreve a alta disponibilidade e dados comportamento de proteção com base nas configurações de um grupo de disponibilidade com réplicas síncronas três: 

|`required_synchronized_secondaries_to_commit`|0 |1 \*|2
| --- |:---:|:---:|:---:
|Failover automático após a interrupção da réplica primária| |✔| 
|Réplica primária disponível após uma interrupção de réplica secundária|✔|✔| 
|Réplica primária disponível após duas falhas de réplica secundária|✔| |
|Failover manual após a interrupção da réplica primária - possível perda de dados|✔| | 

\*Quando o grupo de disponibilidade é adicionado como um recurso em um cluster de configuração padrão.

<a name="twoSynch"></a>

## <a name="two-synchronous-replicas"></a>Duas réplicas síncronas

Essa configuração permite que a proteção de dados. Como as outras configurações de grupo de disponibilidade, ele pode habilitar a leitura de expansão. A configuração de duas réplicas síncronas não fornece alta disponibilidade automática. 

![Duas réplicas síncronas][1]

Essa configuração requer dois servidores. Esses servidores preenchem a função da réplica primária e secundária. 

A configuração de duas réplicas síncronas é otimizada para dados de proteção e distribuir a carga de trabalho de leitura para bancos de dados. Por padrão, o recurso é configurado para proteção de dados. Essa configuração não fornece alta disponibilidade porque se qualquer instância do SQL Server falhar, o banco de dados não está totalmente disponível ou há risco de perda de dados. 

A tabela a seguir descreve o comportamento de proteção de dados de acordo com os valores possíveis para um grupo de disponibilidade com duas réplicas síncronas: 

|`required_synchronized_secondaries_to_commit`|0 \*|1 
| --- |:---|:---
|Failover automático após a interrupção da réplica primária| |✔ \*\* | 
|Réplica primária disponível após a interrupção da réplica secundária|✔| |

\*Quando o grupo de disponibilidade é adicionado como um recurso em um cluster de configuração padrão.

\*\*Nessa configuração, após a interrupção da réplica primária do grupo de disponibilidade automático failover. Aplicativos não é possível conectar-se ao grupo de disponibilidade até que a réplica primária está novamente on-line - agora como uma réplica secundária. 

A configuração de duas réplicas síncronas pode ser mais econômicos porque ela requer apenas duas instâncias do SQL Server em dois servidores.

<a name="pacemakerNotify"></a>

## <a name="understand-sql-server-resource-agent-for-pacemaker"></a>Entender o agente de recursos do SQL Server para pacemaker

SQL Server 2017 CTP 1.4 adicionado `sequence_number` para `sys.availability_groups` para permitir Pacemaker identificar secundário atualizado como réplicas estão com a réplica primária. `sequence_number`é um BIGINT aumentando de forma monotônica que representa atualizado como a réplica do grupo de disponibilidade local. Atualizações de pacemaker a `sequence_number` com cada alteração de configuração do grupo de disponibilidade. Exemplos de alterações de configuração incluem o failover, a adição de réplica ou a remoção. O número é atualizado na réplica primária e replicado para réplicas secundárias. Assim, uma réplica secundária que tem a configuração atualizada tem o mesmo número de sequência do primário. 

Quando decide Pacemaker promover uma réplica primária, ele primeiro envia um *previamente promover* notificação para todas as réplicas. As réplicas de retornam o número de sequência. Em seguida, quando na verdade tenta Pacemaker promover uma réplica primária, a réplica apenas promove próprio se o seu número de sequência é o mais alto de todos os números de sequência. Se o seu próprio número de sequência não coincide com o maior número de sequência, a réplica rejeita a operação de promoção. Dessa maneira, somente a réplica com o maior número de sequência pode ser promovida a primária, garantindo que não haverá perda de dados. 

Esse processo requer pelo menos uma réplica disponível para promoção com o mesmo número de sequência do primário anterior. Os conjuntos de agente do recurso Pacemaker `required_synchronized_secondaries_to_commit` , de forma que pelo menos uma réplica secundária síncrona está atualizado e disponível para ser o destino de um failover automático por padrão. Com cada ação de monitoramento, o valor de `required_synchronized_secondaries_to_commit` calculada (e atualizados, se necessário). O `required_synchronized_secondaries_to_commit` valor é 'número de réplicas síncronas' dividido por 2. No momento do failover, o agente de recursos requer (`total number of replicas`  -  `required_synchronized_secondaries_to_commit` réplicas) para responder ao previamente promover a notificação. A réplica com o mais alto `sequence_number` é promovido a primário. 

Por exemplo, um grupo de disponibilidade com três réplicas síncronas - uma réplica primária e duas réplicas secundárias síncronas.

- `required_synchronized_secondaries_to_commit`é 1; (3 / 2 -> 1).

- O número necessário de réplicas para responder para promover previamente a ação é 2; (3 - 1 = 2). 

Nesse cenário, duas réplicas precisam responder para o failover deve ser disparada. Para failover automático bem-sucedida após uma interrupção de réplica primária, ambas as réplicas secundárias precisam ser atualizadas e responder a promover previamente a notificação. Se eles estiverem online e síncrona, eles têm o mesmo número de sequência. O grupo de disponibilidade promove um deles. Se apenas uma das réplicas secundárias responde para o promover previamente ação, o agente de recursos não pode garantir que o secundário que respondeu tem o sequence_number mais alto e um failover não será disparado.

>[!IMPORTANT]
>Quando `required_synchronized_secondaries_to_commit` é lá 0 é o risco de perda de dados. Durante uma interrupção da réplica primária, o agente de recursos não aciona automaticamente um failover. Você pode esperar para o site primário recuperar ou failover manualmente usando `FORCE_FAILOVER_ALLOW_DATA_LOSS`.

Você pode optar por substituir o comportamento padrão e impedir que o recurso de grupo de disponibilidade da configuração `required_synchronized_secondaries_to_commit` automaticamente.

O script a seguir define `required_synchronized_secondaries_to_commit` 0 em um grupo de disponibilidade denominada `<**ag1**>`. Antes de executar a substituição `<**ag1**>` com o nome do seu grupo de disponibilidade.

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=0
```

Para reverter para o valor padrão, com base na configuração do grupo de disponibilidade execute:

```bash
sudo pcs resource update <**ag1**> required_synchronized_secondaries_to_commit=
```

>[!NOTE]
>Quando você executa os comandos anteriores, primário está temporariamente rebaixado para o secundário, depois promovido novamente. A atualização de recurso faz com que todas as réplicas parar e reiniciar. O novo valor para`required_synchronized_secondaries_to_commit` é definida apenas uma vez réplicas forem reiniciadas, não instantaneamente.

<!--Image references-->
[1]: ./media/sql-server-linux-availability-group-ha/1-read-scale-out.png
[3]: ./media/sql-server-linux-availability-group-ha/3-three-replica.png
