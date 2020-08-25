---
title: Determinar a frequência de sondangem
description: Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo do sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafd18a7701ed5de5018a3e8dc23bc8d5d9640fa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767035"
---
# <a name="determine-polling-frequency"></a>Determinar a frequência de sondagem
Este artigo explica como determinar a frequência de sondagem para alertas do dispositivo do sistema de plataforma de análise.  
  
## <a name="to-determine-the-polling-frequency"></a>Para determinar a frequência de sondagem  
Como o PDW atualmente não dá suporte a notificações proativas quando ocorrem alertas, a solução de monitoramento precisa sondar continuamente as DLLs do dispositivo.  Internamente, o PDW sonda os componentes em intervalos diferentes:  
  
-   Cluster-60 segundos  
  
-   Pulsação-60 segundos  
  
-   Todos os outros componentes-cinco minutos  
  
-   Contadores de desempenho-três segundos  
  
Um intervalo comum para sondar alertas, que também é usado pelo System Center, é a **cada 15 minutos**.  Obviamente, você pode consultar mais ou menos frequentemente, mas não é recomendável sondar menos do que a cada seis horas.  
  
A sondagem com mais frequência é aceitável, mas a sondagem com muita frequência pode truncar a DMV [Sys. dm_pdw_nodes_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md?view=sql-server-ver15) .  A sondagem com muita frequência pode dificultar para os usuários o diagnóstico de problemas de desempenho de consulta quando eles se sobreprimem rapidamente.  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Monitoramento de dispositivo &#40;o sistema de plataforma de análise&#41;](appliance-monitoring.md)  
