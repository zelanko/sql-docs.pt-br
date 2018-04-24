---
title: Identificar afunilamentos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- resource bottlenecks [SQL Server]
- database monitoring [SQL Server], bottlenecks
- performance [SQL Server], bottlenecks
- tuning databases [SQL Server], bottlenecks
- monitoring server performance [SQL Server], bottlenecks
- monitoring performance [SQL Server], bottlenecks
- database performance [SQL Server], bottlenecks
- server performance [SQL Server], bottlenecks
- bottlenecks [SQL Server]
- identifying bottlenecks [SQL Server]
ms.assetid: db079e65-ee80-4105-aec9-f8230d0d6635
caps.latest.revision: 18
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 72d402371944b58fadb028e49c913b29998d0e79
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="identify-bottlenecks"></a>Identificar afunilamentos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O acesso simultâneo a recursos compartilhados provoca gargalos. Em geral, os gargalos estão presentes em todo sistema de software e são inevitáveis. Porém, demandas excessivas em recursos compartilhados causam um tempo de resposta ruim e devem ser identificadas e ajustadas.  
  
 São causas de gargalos:  
  
-   Recursos insuficientes, exigindo componentes adicionais ou atualizados.  
  
-   Recursos de mesmo tipo entre os quais as cargas de trabalho não são distribuídas de maneira uniforme; por exemplo, um disco sendo monopolizado.  
  
-   Mau funcionamento de recursos.  
  
-   Recursos incorretamente configurados.  
  
## <a name="analyzing-bottlenecks"></a>Analisando afunilamentos  
 Durações excessivas de diversos eventos são indicadores de gargalos que podem ser ajustados.  
  
 Por exemplo:  
  
-   Algum outro componente pode impedir a carga de alcançar esse componente e aumentar, assim, o tempo para a conclusão da carga.  
  
-   Solicitações de clientes podem levar mais tempo devido a congestionamento da rede.  
  
 A seguir, encontram-se cinco grandes áreas a monitorar, ao rastrear o desempenho do servidor, para identificar gargalos.  
  
|Possível área de gargalo|Efeitos no servidor|  
|------------------------------|---------------------------|  
|Uso de memória|Memória insuficiente alocado ou disponível para o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] degrada o desempenho. Os dados têm que ser lidos do disco, em vez de diretamente do cache de dados. Sistemas operacionais Microsoft Windows executam paginação excessiva, permutando dados de e para o disco, segundo a necessidade de páginas.|  
|Utilização de CPU|Uma taxa de utilização de CPU cronicamente alta pode indicar que as consultas do [!INCLUDE[tsql](../../includes/tsql-md.md)] precisam ser ajustadas ou que é necessário atualizar a CPU.|  
|Entrada/saída (E/S) de disco|[!INCLUDE[tsql](../../includes/tsql-md.md)] consultas podem ser ajustadas de modo a reduzir E/S desnecessária; por exemplo, empregando índices.|  
|Conexões de usuário|Muitos usuários podem estar acessando o servidor simultaneamente, provocando degradação do desempenho.|  
|Bloqueios|Aplicativos incorretamente projetados podem causar bloqueios e obstruir a simultaneidade, causando tempos de resposta mais longos e taxas de transferência de transações mais baixas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso da CPU](../../relational-databases/performance-monitor/monitor-cpu-usage.md)   
 [Monitorar o uso do disco](../../relational-databases/performance-monitor/monitor-disk-usage.md)   
 [Monitorar o uso da memória](../../relational-databases/performance-monitor/monitor-memory-usage.md)   
 [SQL Server, objeto General Statistics](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)   
 [SQL Server, objeto Locks](../../relational-databases/performance-monitor/sql-server-locks-object.md)  
  
  
