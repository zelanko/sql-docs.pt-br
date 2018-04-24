---
title: Serviços de PDW status - Analytics Platform System | Microsoft Docs
description: Parallel Data Warehouse (PDW) dos serviços de status para Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e2252bb821f9522515f1625b0fc118323cb50d1f
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Status dos serviços de Parallel Data Warehouse para Analytics Platform System
Parallel Data Warehouse **Status de serviços** página no Gerenciador de configuração do sistema do Microsoft Analytics Platform mostra o status atual de todos os serviços do SQL Server PDW e fornece a capacidade de parar e iniciar os serviços do PDW. Este é o único método suportado para iniciar e interromper os serviços do PDW. Observe que componentes individuais ou serviços não podem ser iniciados independentemente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Para iniciar ou parar os serviços de aplicativo  
  
1.  Para iniciar os serviços do dispositivo, clique em **iniciar dispositivo**.  
  
2.  Para interromper os serviços do dispositivo, clique em **dispositivo parar**.  
  
Não é necessário clicar em **aplicar** quando iniciar e parar os serviços de aplicativo usando **iniciar dispositivo** e **dispositivo parar**.  
  
![DWConfig Appliance PDW Services](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> Também interromper a região PDW impede que o agente do PDW (sqldwagent) em nós da região de HDInsight. A região de HDInsight ainda está funcional, mas o monitoramento de integridade não estará disponível. (O agente PDW exige o nó de controle do PDW para relatar o monitoramento de integridade).  
  
## <a name="see-also"></a>Consulte também  
[Ligar o dispositivo de APS ou desligar &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
