---
title: Status do serviços PDW (Analytics Platform System)
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
ms.assetid: 3fc9bee2-c372-4c4a-956c-fb54215d8918
caps.latest.revision: 14
ms.openlocfilehash: 727adf27c5118130682d8d63eb120c67380ac20d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-services-status"></a>Status de serviços do PDW
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
  
