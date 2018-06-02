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
ms.openlocfilehash: 39597e0e4623a3006709acde7fe54f97545c362f
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707614"
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
  
Sondagem mais frequente é aceitável, mas com muita frequência de sondagem pode sobrecarregar o [sys.dm_pdw_nodes_exec_requests](http://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV.  Com muita frequência de sondagem pode tornar difícil para os usuários diagnosticar o desempenho de consulta problemas quando seus rapidamente acumula fora da exibição.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
