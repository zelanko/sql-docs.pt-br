---
title: Grupos de disponibilidade de escala de leitura | Microsoft Docs
ms.custom: 
ms.date: 10/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: "9"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d2d3eb4751cee7ab0258554f3b176b73a7cd12e5
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="read-scale-availability-groups"></a>Grupos de disponibilidade de escala de leitura
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Um grupo de disponibilidade é uma solução abrangente que oferece funcionalidades de alta disponibilidade para o SQL Server, além de soluções integradas de dimensionamento. Em um aplicativo de banco de dados típico, vários clientes executam diversos tipos de cargas de trabalho. Às vezes, pode ocorrer o desenvolvimento de gargalos devido às restrições de recursos. Você pode liberar recursos e obter uma taxa de transferência maior para a carga de trabalho OLTP. Você também pode fornecer melhor desempenho e escala em cargas de trabalho somente leitura. Aproveite a tecnologia de replicação mais rápida para o SQL Server e crie um grupo de bancos de dados replicados para descarregar cargas de trabalho de relatórios e de análises para réplicas somente leitura. 

Com os grupos de disponibilidade, uma ou mais réplicas secundárias podem ser configuradas para dar suporte ao acesso somente leitura aos bancos de dados secundários.

Os aplicativos cliente que executam cargas de trabalho de análises ou de relatórios podem conectar-se aos bancos de dados secundários diretamente. Você também pode configurar uma lista de roteamento somente leitura e conectar-se ao banco de dados primário. Em seguida, a solicitação de conexão é encaminhada para cada uma das réplicas secundárias da lista de roteamento usando um mecanismo round robin.

## <a name="read-scale-availability-groups-without-cluster"></a>Grupos de disponibilidade de escala de leitura sem cluster

No [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] e anteriores, todos os grupos de disponibilidade exigiam um cluster. O cluster fornecia continuidade dos negócios para HADR (alta disponibilidade e recuperação de desastre). Além disso, as réplicas secundárias eram configuradas para operações de leitura. Se a meta não fosse a alta disponibilidade, uma sobrecarga operacional considerável seria consumida para configurar e operar um cluster. O SQL Server 2017 introduz grupos de disponibilidade de escala de leitura sem um cluster. 

Se seus requisitos de negócios estiverem relacionados a conservar recursos para cargas de trabalho críticas executadas na réplica primária, você poderá usar o roteamento somente leitura ou conectar-se diretamente a réplicas secundárias legíveis. Você não precisa depender da integração a nenhuma tecnologia de clustering. Essas novas funcionalidades estão disponíveis para o SQL Server 2017 em execução em plataformas Windows e Linux.

>[!IMPORTANT]
>Essa não é uma configuração de alta disponibilidade. Não há nenhuma infraestrutura para monitorar e coordenar a detecção de falhas e o failover automático. Sem um cluster, o SQL Server não pode fornecer o RTO (objetivo de tempo de recuperação) baixo fornecido por uma solução de alta disponibilidade automatizada. Se você precisar de funcionalidades de alta disponibilidade, use um gerenciador de cluster (clustering de failover do Windows Server failover clustering no Windows ou Pacemaker no Linux). 
>
>O grupo de disponibilidade de escala de leitura pode fornecer a funcionalidade de recuperação de desastre. Quando as réplicas somente leitura estão no modo de confirmação síncrona, elas fornecem um RPO (objetivo de ponto de recuperação) igual a zero. Para fazer failover em um grupo de disponibilidade de escala de leitura, veja [Fazer failover da réplica primária em um grupo de disponibilidade de escala de leitura](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly).

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Usar grupos de disponibilidade distribuídos para a escala de leitura geográfica

Soluções separadas geograficamente podem implementar soluções de escala de leitura com grupos de disponibilidade distribuídos. Você pode usá-las para descarregar cargas de trabalho de leitura da réplica primária para as réplicas secundárias legíveis para sites que estão mais próximos à origem das cargas de trabalho de leitura. Os grupos de disponibilidade distribuídos reduzem a utilização de recursos na réplica primária. Eles também ajudam com a taxa de transferência de leitura reduzindo a latência de rede e aproveitando recursos dedicados.

Um único grupo de disponibilidade distribuído pode ter até 17 réplicas secundárias legíveis. Para uma capacidade de dimensionamento maior, faça uma corrente margarida de vários grupos de disponibilidade para aumentar ainda mais o número de réplicas legíveis. É possível também implantar dois grupos de disponibilidade distribuídos do mesmo grupo de disponibilidade para leituras de baixa latência em ambientes geograficamente dispersos.




## <a name="next-steps"></a>Próximas etapas 

[Configurar um grupo de disponibilidade de escala de leitura no Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>Consulte também 
 [Visão geral de grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) 
  
  
