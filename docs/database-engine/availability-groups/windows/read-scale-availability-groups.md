---
title: Grupos de disponibilidade de escala de leitura | Microsoft Docs
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6dfa046a07b9fd5a3eddbe474b5ea63c1163c26c
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="read-scale-availability-groups"></a>Grupos de disponibilidade de escala de leitura
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Além de reunir as melhores funcionalidades de HA do SQL Server, um grupo de disponibilidade é uma solução abrangente que também oferece soluções de dimensionamento integradas. Em um aplicativo de banco de dados típico, há vários clientes executando vários tipos de cargas de trabalho e, às vezes, isso pode levar a afunilamentos, devido a restrições de recursos. Libere recursos e alcance uma maior taxa de transferência da carga de trabalho OLTP ou ofereça um melhor desempenho e escala em cargas de trabalho somente leitura. Faça isto aproveitando a mais rápida tecnologia de replicação para o SQL Server – criar um grupo de bancos de dados replicados para descarregar cargas de trabalho de relatório e análise para as réplicas somente leitura. 

Com os Grupos de Disponibilidade, uma ou mais réplicas secundárias podem ser configuradas para dar suporte ao acesso somente leitura aos bancos de dados secundários.

Os aplicativos cliente que executam cargas de trabalho de análise ou relatório podem se conectar aos bancos de dados secundários diretamente. Outra opção é que o cliente pode configurar uma lista de roteamento somente leitura e se conectar à primária que encaminhará a solicitação de conexão para cada uma das réplicas secundárias da lista de roteamento de forma round robin.

## <a name="read-scale-availability-groups-without-cluster"></a>Grupos de disponibilidade de escala de leitura sem cluster

No [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] e anterior, todos os grupos de disponibilidade exigiam um cluster. O cluster fornecia continuidade dos negócios – HADR (alta disponibilidade e recuperação de desastre). Além disso, as réplicas secundárias podiam ser configuradas para operações de leitura. A configuração e operação de um cluster implicava muita sobrecarga operacional, caso o HA não fosse a meta. O SQL Server 2017 introduz grupos de disponibilidade de escala de leitura sem um cluster. 

Se o requisito de negócios é conservar recursos para cargas de trabalho críticas executadas na primária, os usuários agora podem usar o roteamento somente leitura ou se conectar diretamente às réplicas secundárias legíveis, sem depender da integração com uma tecnologia de clustering. Essas novas funcionalidades estão disponíveis para o SQL Server 2017 em execução em plataformas Windows e Linux.

>[!IMPORTANT]
>Essa não é uma configuração de alta disponibilidade. Não há nenhuma infraestrutura para monitorar e coordenar a detecção de falhas e o failover automático. Para os usuários que precisam das funcionalidades de HADR, use um gerenciador de cluster (WSFC no Windows ou Pacemaker no Linux). 

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Usar grupos de disponibilidade distribuídos para a escala de leitura geográfica

Soluções separadas geograficamente podem implementar soluções de escala de leitura com grupos de disponibilidade distribuídos. Isso permite o descarregamento de cargas de trabalho de leitura da réplica primária para as réplicas secundárias legíveis, para sites que estão mais próximos à origem das cargas de trabalho de leitura. Isso não só reduz a utilização de recursos na primária, mas também ajuda com a taxa de transferência de leitura, reduzindo a latência de rede e aproveitando os recursos dedicados.

Um único grupo de disponibilidade distribuído pode ter até 17 réplicas secundárias legíveis. Para maior capacidade de dimensionamento, faça uma corrente margarida de vários grupos de disponibilidade e aumente o número de réplicas legíveis ainda mais. Também implante dois grupos de disponibilidade distribuídos do mesmo grupo de disponibilidade para leituras de baixa latência em ambientes geograficamente dispersos.




## <a name="next-steps"></a>Próximas etapas 

[Configurar o grupo de disponibilidade de escala de leitura no Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md)

## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

