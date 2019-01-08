---
title: Determinar a frequência de sondagem - Analytics Platform System | Microsoft Docs
description: Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo do Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: eec9e3e211c68b7f56fe6829a70064317b96e646
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519572"
---
# <a name="determine-polling-frequency"></a>Determinar a frequência de sondagem
Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo do Analytics Platform System.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar a frequência de sondagem  
Como o PDW não suporta atualmente proativas notificações quando ocorrerem alertas, a solução de monitoramento precisa sondar continuamente o dispositivo de DLLs.  Internamente, o PDW sonda os componentes em intervalos diferentes:  
  
-   Cluster - 60 segundos  
  
-   Pulsação - 60 segundos  
  
-   Todos os outros componentes - cinco minutos  
  
-   Contadores de desempenho - três segundos  
  
Um intervalo comum para sondar alertas, que também é usado pelo System Center, é **a cada 15 minutos**.  Obviamente, você poderia consultar maior ou menor frequência, mas não é recomendável sondar inferior a cada seis horas.  
  
Sondagem mais frequente é aceitável, mas com muita frequência de sondagem pode sobrecarregar o [sys.dm_pdw_nodes_exec_requests](https://msdn.microsoft.com/library/ms177648(v=sql11).aspx) DMV.  Com muita frequência de sondagem pode torná-lo difícil para os usuários diagnosticar o desempenho da consulta problemas quando suas rapidamente acumula fora da exibição.  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
