---
title: Determinar a frequência de sondagem (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 062c0e3d-f7d0-44f1-aeab-a9bd17dc6fdd
caps.latest.revision: 7
ms.openlocfilehash: e67ab38c12000f3d78a9179a177ce5f673b8eaa2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="determine-polling-frequency"></a>Determinar a frequência de sondagem
Este tópico explica como determinar a frequência de sondagem para alertas de dispositivo de PDW do SQL Server.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar a frequência de sondagem  
Como o PDW não oferece suporte a notificações pró-ativo quando ocorrerem alertas, a solução de monitoramento deve sondar continuamente o dispositivo DLLs.  Internamente, o PDW pesquisa os componentes em intervalos diferentes:  
  
-   Cluster – 60 segundos  
  
-   Pulsação – 60 segundos  
  
-   Todos os outros componentes – 5 minutos  
  
-   Contadores de desempenho – 3 segundos  
  
É um intervalo comum de sondagem para alertas, que também é usado pelo System Center, **a cada 15 minutos**.  Obviamente, você poderia consultar maior ou menor frequência, mas não é recomendável para sondar inferior a cada 6 horas.  
  
Sondagem mais frequente é aceitável, mas com muita frequência de sondagem pode sobrecarregar o [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Isso pode tornar difícil para os usuários diagnosticar problemas de desempenho de consulta se há consultar rapidamente acumula fora da exibição.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
