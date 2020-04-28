---
title: Status de serviços do PDW
description: Status dos serviços do PDW (data warehouse paralelo) para o Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400850"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Status dos serviços de data warehouse paralelos para o Analytics Platform System
A página status do Parallel data warehouse **Services** na Configuration Manager de Microsoft Analytics Platform System mostra o status atual de todos os serviços de SQL Server PDW e fornece a capacidade de parar e iniciar os serviços do PDW. Esse é o único método com suporte para iniciar e parar os serviços do PDW. Observe que componentes ou serviços individuais não podem ser iniciados de forma independente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar ou parar os serviços de dispositivo  
  
1.  Para iniciar os serviços de dispositivo, clique em **Iniciar dispositivo**.  
  
2.  Para interromper os serviços de dispositivo, clique em **parar dispositivo**.  
  
Não é necessário clicar em **aplicar** ao iniciar e parar os serviços de dispositivo usando **Start Appliance** e **Stop Appliance**.  
  
![Serviços PDW do dispositivo DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Parar a região do PDW também interrompe o agente do PDW (sqldwagent) nos nós. O agente PDW requer que o nó de controle do PDW relate o monitoramento de integridade.  
  
## <a name="see-also"></a>Consulte Também  
[Ligar ou desligar o dispositivo APS &#40;o sistema de plataforma de análise&#41;](power-the-aps-appliance-on-or-off.md)  
  
