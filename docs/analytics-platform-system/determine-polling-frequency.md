---
title: Determinar a frequência de sondagem - Analytics Platform System | Microsoft Docs
description: Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e8e2a1ccf469e6c587870c0d5921014d797f87d1
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="determine-polling-frequency"></a>Determinar a frequência de sondagem
Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo Analytics Platform System.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar a frequência de sondagem  
Como o PDW não oferece suporte a notificações pró-ativo quando ocorrerem alertas, a solução de monitoramento deve sondar continuamente o dispositivo DLLs.  Internamente, o PDW pesquisa os componentes em intervalos diferentes:  
  
-   Cluster – 60 segundos  
  
-   Pulsação – 60 segundos  
  
-   Todos os outros componentes – cinco minutos  
  
-   Contadores de desempenho – três segundos  
  
É um intervalo comum de sondagem para alertas, que também é usado pelo System Center, **a cada 15 minutos**.  Obviamente, você poderia consultar maior ou menor frequência, mas não é recomendável para sondar inferior a cada seis horas.  
  
Sondagem mais frequente é aceitável, mas com muita frequência de sondagem pode sobrecarregar o [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/en-us/library/ms177648(v=sql11).aspx) DMV.  Com muita frequência de sondagem pode tornar difícil para os usuários diagnosticar o desempenho de consulta problemas quando seus rapidamente acumula fora da exibição.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
